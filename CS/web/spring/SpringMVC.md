## SpringMVC

#### MVC模式

MVC是一种使用MVC(Model_view_controller)设计创建Web应用程序的模式

- Model：表示后台应用程序，包含数据和各种操作
- View：返回给用户的结果
- Controller：接收用户请求，调用模型完成用户请求的控制器

---

SpringMVC是Spring中的web模块，用于处理用户请求和发出响应。它是基于MVC模式实现的。

#### SpringMVC流程

![](https://markdown-1259282458.cos.ap-nanjing.myqcloud.com/img/20210420223846.png)

1. DispatcherServlet收到用户请求后将请求发送到处理器映射(controller mapping) 
2. 处理器映射根据请求的URL信息向DispatchServlet返回一个控制器
3. DispatcherServlet将请求发送到对应的controller进行处理
4. 处理得到model(用户需要的数据)以及显示信息的逻辑视图名
5. DispatcherServlet将逻辑视图名发送到视图解析器得到一个匹配的特定视图实现
6. 视图+model 得到给用户的响应

---

Spring 一个项目一般分为3层

- 表现层 ：mvc工作在表现层。Controller层
- 业务层： 业务层负责处理Controller传来的要求，调用数据层进行数据操作。Service层
- 数据层： DAO层

---

模版引擎-Thymeleaf

负责由模版文件和model生成View

