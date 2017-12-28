# 第 4 章 返回结果的 HTTP 状态码
### 4.1 状态码告知从服务端返回的请求结果
- 正常: 2xx
- 错误: 4xx or 5xx
数字中的第一位指定响应类别, 后两位无分类
 


|  | 类别 | 原因短语 |
| :-: | :-: | :-: |
| 1XX  | Informational(信息性状态码) | 接收的请求正在处理 |
| 2XX | Success(成功状态码) | 请求正常处理完毕  |
| 3XX | Redirection(重定向状态码) | 需要进行附加操作以完成请求 |
| 4XX | Client Error(客户端错误状态码) | 服务端无法处理请求 |
| 5XX  | Server Error(服务端错误状态码) | 服务端处理请求出错 |

经常使用的只有 **14** 种

### 4.2 2XX 成功
- 200 OK
- 204 No Content
- 206 Partial Content : 进行了范围请求, 响应报文中包含由 Content-Range 指定范围的实体内容

### 4.3 3XX 重定向
- 301 Moved Permanently 永久性重定向
- 302 Found 临时性重定向 
- 303 See Other  --> GET
- 304 Not Modified
- 307 Temporary Redirect 临时重定向, 与302相同,但会遵循浏览器标准,不会从 POST 变成 GET

### 4.4 4XX 客户端错误
- 400 Bad Request 请求报文中存在语法错误
- 401 Unauthorized 未认证或认证失败
- 403 Fobidden 请求资源的访问被服务器拒绝了/未获得文件系统的访问权限
- 404 Not Found 服务器上无法找到请求的资源

### 4.5 5XX 服务器错误
- 500 Internal Server Error 服务端执行请求时发生了故障
- 503 Service Unavailable  服务器暂时处于超负载或正在进行停机维护, 现在无法处理请求 

Ps: 有时返回的状态码与状况不一致


