#  第 3 章 HTTP 报文内的 http 信息

### HTTP 报文
用于 HTTP 协议交互的信息
### 编码提升传输速率
##### 内容编码: 指明应用在实体内容上的编码格式,并保持实体信息原样压缩
-  gzip (GNU zip)
- compress (UNIX 系统的标准压缩)
- deflate (zlib)
- identity (不进行编码)

##### 分块传输编码: 把实体主体分块的功能
每一块都会用十六进制来标记块的大小,而实体主体的最后一块会使用"0(CR+LF)"来标记
##### 多部分对象集合:
- multipart / form-data : 表单上传
- multipart / byteranges: “状态码 206（Partial Content，部分内容）响应报文”

> `eg.` 
>  Content-Type: multipart / form-data;boundary=AaB03x 
> --AaB03x 
>  “Content-Disposition: form-data; name="field1”
>   --AaB03x
>  备注:
>  使用 boundary 字符串来划分多部分对象集合指明的各类实体

##### 获取部分内容的范围请求
范围请求(Range request): 指定范围的请求
eg. 使用 Range: bytes=5001-10000

##### 内容协商 Content Negotiation
访问相同的 URI,根据具体情况(例如语言,字符集,编码方式...)返回不同的内容
类型:
- 服务器驱动协商: 服务的直接根据请求头部自行处理
- 客户端驱动协商: 用户手动切换
- 透明协商: 上述两种的结合体


