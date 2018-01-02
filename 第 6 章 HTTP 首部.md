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
##### Accept-Charset



