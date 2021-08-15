# thymeleaf

thymeleaf是模版引擎，用于将model和view合成html。

##### thymeleaf中表达式

- `@{}`:URL，链接
- `${}`:变量表达式
- `#{}`：Message表达式，主要是从国际化配置文件中取值。



##### 普通字符串和表达式的拼接

`| String ,${exp}|`



##### 判断

`th:if =""`满足条件才显示



##### 迭代

`th:each="${collection}"`