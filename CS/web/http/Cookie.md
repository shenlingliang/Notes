# Cookies

HTTP Cookies是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向服务器发起请求时被携带并发送到服务器。*Cookies使基于无状态的HTTP，能够跟踪用户状态*。

Cookies的主要作用

- 会话状态管理(如用户登录状态，购物车，游戏分数等)
- 个性化设置(用户自定义设置，主题)
- 浏览器行为跟踪(用户行为分析)

#### 创建Cookies

当服务器收到HTTP请求时，服务器可以在响应头里添加一个`Set-Cookie`选项。浏览器收到响应后将Cookie保存下，以后对该服务器发送请求都将Cookie信息加入到请求中发送给服务器。

---

#### Cookie与Session

Cookie和session都是用来解决HTTP协议不保持会话状态的问题。

Cookie是服务器发送给客户端的数据，客户端在发送请求时，就把这个数据带在请求中最为身份标识

Session是服务器用于保存会话信息的，可以根据Cookie中信息找到对应的Session
