# HTTP常见状态码

- 1xx：服务器收到请求，要求请求者继续执行操作
  - `100`:Coutinue，继续，客户端应继续进行请求
  - `101`:Switching Protocols ,切换协议，服务器根据客户端的请求切换协议
- 2xx：成功，操作被成功接收并处理
  - `200`:OK,请求成功。一般用于GET与POST请求。
  - `201`:Created,已成功请求并创建了新的资源
  - `202`:Accepted,已接受。已接受请求，但未处理完成
  - `203`:Non-Authoritative Information,非授权信息。请求成功，但返回的meta信息不再原始的服务器，而是一个副本
  - `204`:No Content,无内容。服务器成功处理，但未返回内容。
  - `205`:Reset Content,重置内容。服务器处理成功，用户终端应该重置文档视图，一般用于清除浏览器表单
  - `206`:Partial Content。服务器成功处理了部分GET请求
- 3xx：重定向，需要进一步的操作以完成请求
  - `301`:Move Permanently 永久移动
  - `302`:Found 临时移动
  - `304`:Not Modified,请求资源未修改，可以使用缓存
  - `305`:Use Proxy,需要使用代理
- 4xx：客户端错误
  - `400`:Bad Request 客户端请求的语法错误，服务器无法理解
  - `401`:Unauthorized 需要进行身份认证
  - `403`:Forbidden 服务器拒绝执行
  - `404`:Not Found
- 5xx：服务器错误
  - `500`:Internal Server Error，服务器内部错误，无法完成请求
  - `501`:Not Implemented ，服务器不支持请求的功能
  - `502`:Bad Gateway,