## Http 概述

Http(HyperText transfer protocol):超文本传输协议。

- 是一个用于传输HTML的应用层协议
- 是一个C/S协议
- 是一个无状态协议

----

#### HTTP的基本性质

- Http是可扩展的
  - 在HTTP/1.0中出现的HTTP headers让协议扩展变得非常容易。 只要客户端和服务端保文中新Header的语义一致，就能够轻松的扩展新功能。
- HTTP是无状态的
  - HTTP只负责发送和处理请求，并不会记录状态
  - 想要记录状态，就需要在请求header中加入独一无二cookies，以记录状态
- HTTP和连接
  - 连接是由传输层负责的，而HTTP作为应用层协议，对传输层协议只有一个要求，即可靠性，一个请求被发送就需要收到回应，即使是错误信息。
  - 因此为了优化TCP的固有缺点导致的HTTP协议缺陷，Google研发了一种以可靠UDP为基础，能够提供更高效的传输的协议QUIC

---

#### HTTP报文

HTTP有两种报文类型，请求和响应，每种都有其特定的格式

##### 请求

![](https://markdown-1259282458.cos.ap-nanjing.myqcloud.com/img/20210727164522.png)

- 请求头
  - 请求方法
    - GET
    - PUT
    - HEAD
    - PUT
    - DELETE
    - OPTIONS
    - TRACE
    - CONNECT
  - 资源路径：
    - 如`/app/index.html`
  - HTTP版本
    - 如`HTTP/1.1`,表示采用HTTP1.1协议
- Headers
  - key: value的结构
- 请求数据

##### 响应

![](https://markdown-1259282458.cos.ap-nanjing.myqcloud.com/img/20210727170729.png)

- 响应头
  - HTTP版本
  - 状态码
  - 状态信息
- Headers

---

Reference

1. [HTTP概述](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview)
2. [HTTP请求报文和响应报文](https://www.cnblogs.com/biyeymyhjob/archive/2012/07/28/2612910.html)

