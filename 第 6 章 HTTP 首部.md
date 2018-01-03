# 第 6 章 HTTP 首部

### 6.1 HTTP 报文首部
- 报文首部: 在客户端和服务端处理时起至关重要的作用的信息几乎都在里面. HTTP 协议的请求和响应报文里必定包含 HTTP 首部
- 报文主体: 所需要的用户和资源的信息都在里面

### 6.2 HTTP 首部字段
结构: `字段名: 字段值`
eg. Content-Type: text/html
ps. 字段值对应单个 HTTP 首部字段可以有多个值. Keep-Alive: timeout=15,max=100
首部字段类型:
- 通用首部字段 General Header Fields
- 请求首部字段 Request Header Fields 
- 响应首部字段 Response Header Fields
-  实体首部字段 Entity Header Field


表 6-1：通用首部字段

|首部字段名	|说明|
| :-: | :-: | :-: |
|Cache-Control	|控制缓存的行为|
|Connection	|逐跳首部、连接的管理|
|Date	|创建报文的日期时间|
|Pragma	|报文指令|
|Trailer	|报文末端的首部一览|
|Transfer-Encoding	|指定报文主体的传输编码方式|
|Upgrade	|升级为其他协议|
|Via	|代理服务器的相关信息|
|Warning	|错误通知|

表 6-2：请求首部字段

|首部字段名	|说明|
| :-: | :-: | :-: |
|Accept	|用户代理可处理的媒体类型|
|Accept-Charset	|优先的字符集|
|Accept-Encoding	|优先的内容编码|
|Accept-Language	|优先的语言（自然语言）|
|Authorization	|Web认证信息|
|Expect	|期待服务器的特定行为|
|From	|用户的电子邮箱地址|
|Host	|请求资源所在服务器|
|If-Match	|比较实体标记（ETag）|
|If-Modified-Since	|比较资源的更新时间|
|If-None-Match	|比较实体标记（与 If-Match 相反）|
|If-Range	|资源未更新时发送实体 Byte 的范围请求|
|If-Unmodified-Since	|比较资源的更新时间（与If-Modified-Since相反）|
|Max-Forwards	|最大传输逐跳数|
|Proxy-Authorization	|代理服务器要求客户端的认证信息|
|Range	|实体的字节范围请求|
|Referer	|对请求中 URI 的原始获取方
TE	传输编码的优先级|
|User-Agent	|HTTP 客户端程序的[…]|

表 6-3：响应首部字段

|首部字段名	|说明|
| :-: | :-: | :-: |
|Accept-Ranges	|是否接受字节范围请求|
|Age	|推算资源创建经过时间|
|ETag	|资源的匹配信息|
|Location	|令客户端重定向至指定URI|
|Proxy-Authenticate	|代理服务器对客户端的认证信息|
|Retry-After	|对再次发起请求的时机要求|
|Server	HTTP|服务器的安装信息|
|Vary	|代理服务器缓存的管理信息|
|WWW-Authenticate	|服务器对客户端的认证信息|
表 6-4：实体首部字段

|首部字段名	|说明|
| :-: | :-: | :-: |
|Allow	|资源可支持的HTTP方法|
|Content-Encoding|	实体主体适用的编码方式|
|Content-Language	|实体主体的自然语言|
|Content-Length	|实体主体的大小（单位：字节）|
|Content-Location	|替代对应资源的URI|
|Content-MD5	|实体主体的报文摘要|
|Content-Range	|实体主体的位置范围|
|Content-Type	|实体主体的媒体类型|
|Expires	|实体主体过期的日期时间|
|Last-Modified	|资源的最后修改日期时间|

### 6.3 HTTP/1.1 通用首部字段
##### 6.3.1 Cache-Control
控制缓存行为
指令参数可选,多个指令之间通过","分隔
```
 Cache-Control: private, max-age=0, no-cache
```

缓存请求指令

|指令|参数|说明|
| :-: | :-: | :-: |
|no-cache|无|强制向源服务器再次验证|
|no-store|无|不缓存请求或响应的任何内容|
|max-age=[second]|必须|响应的最大 Age 值|
|max-stale(=[second])|可省|接收已过期的响应|
|min-fresh=[second]|必须|期望在指定的时间内的响应仍有效|
|no-transform|无|代理不可更改媒体类型|
|only-if-cached|无|从缓存获取资源|
|cache-extension|-|新指令标记(token)|

缓存响应指令

|指令|参数|说明|
| :-: | :-: | :-: |
|public|无|可向任意方提供响应的缓存|
|private|可省|仅向特定用户返回响应|
|no-cache|无|强制向源服务器再次验证|
|no-store|无|不缓存请求或响应的任何内容|
|no-transform|无|代理不可更改媒体类型|
|must-revalidate]|无|可缓存但必须再向源服务器进行确认|
|proxy-revalidate|无|要求中间缓存服务器对缓存的响应有效性再进行确认|
|max-age=[second]|必须|响应的最大 Age 值|
|s-maxage=[second]|必须|公共缓存服务器响应的最大 Age 值|
|cache-extension|-|新指令标记(token)|

##### 6.3.2 Connection
- 控制不再转发给代理的首部字段 Connection: Upgrade
- 管理持久连接  Connection: Keep-Alive /close

##### 6.3.3 Date
表明创建 HTTP 报文的日期和时间
```
Date: Tue, 03 Jul 2012 04:40:59 GMT
```
##### 6.3.4 Pragma
该首部字段属于通用首部字段，但只用在客户端发送的请求中。客户端会要求所有的中间服务器不返回缓存的资源
```
Cache-Control: no-cache
Pragma: no-cache
```
##### Trailer
事先说明报文主体后记录了哪些首部字段
##### Transfer-Encoding
规定了传输报文主体时采用的编码方式
##### Upgrade
首部字段 Upgrade 用于检测 HTTP 协议及其他协议是否可使用更高的版本进行通信，其参数值可以用来指定一个完全不同的通信协议。
##### Via
使用首部字段 Via 是为了追踪客户端与服务器之间的请求和响应报文的传输路径
##### Warning
告知用户一些与缓存相关的问题的警告
格式:
```
Warning: [警告码][警告的主机:端口号]“[警告内容]”([日期时间])
```
HTTP/1.1 警告码

|警告码|	警告内容	|说明|
| :-:  | :-:   |  :-:  |
|110	|Response is stale（响应已过期）	|代理返回已过期的资源|
|111	|Revalidation failed（再验证失败）	|代理再验证资源有效性时失败（服务器无法到达等原因）|
|112	|Disconnection operation（断开连接操作）	|代理与互联网连接被故意切断|
|113	|Heuristic expiration（试探性过期）	|响应的使用期超过24小时（有效缓存的设定时间大于24小时的情况下）|
|199	|Miscellaneous warning（杂项警告）	|任意的警告内容|
|214	|Transformation applied（使用了转换）	|代理对内容编码或媒体类型等执行了某些处理时|
|299	|Miscellaneous persistent warning（持久杂项警告）	|任意的警告内容|

### 6.4 请求首部字段
##### 6.4.1 Accept
通知服务器用户代理能够处理的媒体类型及媒体类型的相对优先级
- 文本文件
   ```
   text/html,text/plain,text/css...
   ```
- 图片文件
  ```
  image/jpeg,image/gif,image/png....
 ```
- 视频文件
  ```
  video/mpeg,video/quicktime...
  ```
- 应用程序使用的二进制文件 
  ```
  application/octet-stream;q=0.333, application/zip...
  ```
> 若想要给显示的媒体类型增加优先级，则使用 q= 来额外表示权重值 1，用分号（;）进行分隔。权重值 q 的范围是 0~1（可精确到小数点后 3 位），且 1 为最大值。不指定权重 q 值时，默认权重为 q=1.0。
优先返回权重值最高的媒体类型

##### 6.4.2 Accept-Charset
通知服务器用户代理支持的字符集及字符集的相对优先顺序. 可一次性指定多种字符集
```
Accept-Charset:iso-8859-5,unicode-1-1;q=0.8
```
##### 6.4.3 Accept-Encoding
通知服务器用户代理支持的内容编码及内容编码的优先级顺序. 可一次性指定多种内容编码
```
Accept-Encoding:gzip,deflace;q=0.8
```
##### 6.4.4 Accept-Language
通知服务器用户代理能够处理的自然语言集及自然语言集的优先级顺序. 可一次性指定多种自然语言集
```
Accept-Language:zh-cn,zh,en;q=0.8
```
##### 6.4.5 Authorization
用来告知服务器，用户代理的认证信息（证书值）
```
Authorization: Basic dWVub3NlbjpwYXNzd29yZA==
```
##### 6.4.6 Except
用来告知服务器, 期望出现的某种特定行为
##### 6.4.7 From
用来告知服务器使用用户代理的用户的电子邮件地址
##### 6.4.8 Host
首部字段 Host 会告知服务器，请求的资源所处的互联网主机名和端口号
##### 6.4.9 If-Match
只有当 If-Match 的字段值跟 ETag 值匹配一致时，服务器才会接受请求.它会告知服务器匹配资源所用的实体标记（ETag）值
##### 6.4.10 If-Modified-Since
如果在 If-Modified-Since 字段指定的日期时间后，资源发生了更新，服务器会接受请求
##### 6.4.11 If-None-Match
只有在 If-None-Match 的字段值与 ETag 值不一致时，可处理该请求。与 If-Match 首部字段的作用相反
##### 6.4.12 If-Range
首部字段 If-Range 属于附带条件之一。它告知服务器若指定的 If-Range 字段值（ETag 值或者时间）和请求资源的 ETag 值或时间相一致时，则作为范围请求处理。反之，则返回全体资源
##### 6.4.13 If-Unmodified-Since
如果在 If-Modified-Since 字段指定的日期时间后，资源没有发生更新，服务器会接受请求
##### 6.4.14 Max-Forwards
当服务器接收到 Max-Forwards 值为 0 的请求时，则不再进行转发，而是直接返回响应
##### 6.4.15 Proxy-Authorization
接收到从**代理服务器**发来的认证质询时，客户端会发送包含首部字段 Proxy-Authorization 的请求，以告知服务器认证所需要的信息
##### 6.4.16 Range
告知服务器资源的指定范围
##### 6.4.17 Referer
告知服务器请求的原始资源的 URI
##### 6.4.18 TE
告知服务器客户端能够处理响应的**传输编码**方式及相对优先级
##### 6.4.19 User-Agent
将创建请求的浏览器和用户代理名称等信息传达给服务器

### 6.5 响应首部字段
##### 6.5.1 Accept-Ranges
告知客户端服务器是否能处理范围请求
- 可处理 Accept-Ranges: bytes
- 不可处理 Accept-Ranges: none
##### 6.5.2 Age
告知客户端,源服务器在多久前创建了响应.字段值的单位为秒
##### 6.5.3 Etag
告知客户端实体标识.唯一.服务器会为每份资源分配对应的 ETag 值
- 强 ETag: 无论实体发生多么细微的变化都会改变   `ETag: "usagi-1234"`
- 弱 ETag: 根本性改变  `ETag: W/"usagi-1234`

##### 6.5.4 Location
将响应接收方引导至某个与请求 URI 位置不同的资源
##### 6.5.5 Proxy-Authenricate
把代理服务器所要求的认证信息发送给客户端
##### 6.5.6 Retry-After
告知客户端应该在多久之后再次发送请求
##### 6.5.7 Server
告知客户端当前服务器上安装的 HTTP 服务器应用程序的信息
##### 6.5.8 Vary
当代理服务器接收到带有 Vary 首部字段指定获取资源的请求时，如果使用的 Accept-Language 字段的值相同，那么就直接从缓存返回响应。反之，则需要先从源服务器端获取资源后才能作为响应返回
##### 6.5.9 WWW-Authenticate
它会告知客户端适用于访问请求 URI 所指定资源的认证方案（Basic 或是 Digest）和带参数提示的质询（challenge）。状态码 401 Unauthorized 响应中，肯定带有首部字段 WWW-Authenticate
### 6.6 实体首部字段
##### 6.6.1 Allow
通知客户端能够支持 Request-URI 指定资源的所有 HTTP 方法
##### 6.6.2 Content-Encoding
告知客户端服务器对实体的主体部分选用的内容编码方式
##### 6.6.3 Content-Language
实体主体使用的自然语言
##### 6.6.4 Content-Length
实体主体部分的大小,单位字节
##### 6.6.5 Content-Location
给出与报文主体部分相对应的 URI
##### 6.6.6 Content-MD5
##### 6.6.7 Content-Type
s实体主体内对象的媒体类型
##### 6.6.9 Expires
将资源失效的日期告知客户端
##### 6.6.10 Last-Modified
指明资源最终被修改的时间
### 6.7 为 Cookie 服务的首部字段
##### 6.7.1 Set-Cookie
当服务器准备开始管理客户端的状态时, 会实现告知各种信息
Set-Cookie 字段的属性

| 属性  | 说明 |
| :-: | :-: |
| name=VALUE| 赋予 Cookie 的名称和其值, must|
| expires=DATE| Cookie 的有效期(若不明确指定则默认为浏览器关闭前为止)|
| path=PATH|将服务器上的文件目录作为 Cookied 的适用对象(若不指定则默认为文档的文件目录)|
| domain=域名| 作为 Cookie 适用对象的域名(若不指定则默认为创建 Cookie 的服务器的域名)|
|secure| 仅在 HTTPS 安全通信时才会发送 Cookie|
| HttpOnly|加以限制,使 Cookie 不能被 javascript 脚本访问|
##### Cookie
告知服务器,当客户端想获得 HTTP 状态管理支持时,就会在请求中包含从服务器接收到的 Cookie. 接收到多个 Cookie时, 同样可以多个 Cookie 形式发送.
### 6.8 其他首部字段
##### 6.8.1 X-Frame-Options
首部字段 X-Frame-Options 属于 HTTP **响应首部**，用于控制网站内容在其他 Web 网站的 Frame 标签内的显示问题。其主要目的是为了防止点击劫持（clickjacking）攻击。
- Deny: 拒绝
- SAMEORIGE: 仅同源域名下的页面(Top-level-browsing-context)匹配时许可

##### 6.8.2 X-XSS-Protection
首部字段 X-XSS-Protection 属于 HTTP 响应首部，它是针对跨站脚本攻击（XSS）的一种对策，用于控制浏览器 XSS 防护机制的开关
- 0: 将 XSS 过滤设置成无效状态
- 1: 将 XSS 过滤设置成有效状态

##### 6.8.3 DNT 
属于 HTTP 请求头部, Do not Track. 拒绝个人信息被收集
- 0: 同意
- 1: 拒绝
##### P3P
属于 HTTP 响应首部, The Platform for Privacy Preferences. 


