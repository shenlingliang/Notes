# Mybatis

MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。

#### 核心组件

- `SqlSessionFactory`:即Sql连接工厂
- `SqlSession`：用于向数据库执行SQL
- Mapper接口，用`@Mapper`标注的接口，提供用于映射的java方法
- xml配置文件，用于配置Mapper接口方法映射到的Sql方法



##### `#,$`的区别

`#{}`表示一个占位符号 相当于jdbc中的?符号， `#{}`实际上是向预编译好的sql语句中填入数据

`${}`需要先拼成SQL语句再进行编译



因此`#{}`能够更好的防止sql注入，能使用`#{}`时尽量使用`#`