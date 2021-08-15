# HTTP 缓存

HTTP缓存的作用是当web缓存发现请求的资源已被存储，它会拦截请求，返回该资源的拷贝，而不会去源服务器重新下载资源。

这样能够减少响应时间，缓解服务器压力，减少网络流量。

web缓存主要分为两类

- 私有缓存：浏览器缓存
  - 私有缓存只能用于单独的终端，即浏览器缓存，这些缓存为浏览过的文档提供向后向前导航，保存网页，查看源码等功能，可以避免再次向服务器发起多余的请求。
- 共享缓存：代理缓存，CDN
  - 可被多个终端共同使用的缓存

----

#### HTTP的缓存控制

HTTP/1.1定义的`Cache-Control`头用来区分对缓存机制的支持情况，请求头和响应头都支持这个熟悉。通过为它提供不同的值来定义缓存策略。

- `Cache-Control:no-store`:不使用缓存，每次客户端请求都会下载完整的响应内容。
- `Cache-Control:no-cache`:缓存但重新验证，每次客户端请求都会带有本地缓存验证字段发送到服务器，服务器验证缓存是否过期，若未过期则返回状态码304(Not modified)。
  - 在请求报文中加入`if-Modified-Since`和`if-None-Match`两个属性用于服务器检验是否过期

##### 私有和公共缓存

- `Cache-Control:private`:只有特定用户可以缓存，中间人不能缓存。
- `Cache-Control:public`:可被中间人缓存。

---

##### Reference

- [HTTP缓存](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Caching)

