# Bean

Bean是Spring中的对象，被Spring容器管理。

Spring通过使用容器对Bean进行管理，降低Bean之间的耦合度

### 容器

Spring容器(Container):负责创建对象，装配对象，配置对象并管理对象的生命周期。

容器是Spring框架的核心，它使用DI管理构成应用的组件，并创建相互依赖的组件之间的关联。

#### Spring容器的分类

- BeanFactory
  - 最简单的容器，提供基本的DI支持
- Application Context
  - 基于BeanFactory实现，提供应用框架级别的服务。

### Bean的生命周期

在传统Java应用中，对象的生命周期很简单。使用对对象进行实例化(如new)，然后该对象就可以使用了。一旦该bean不再被使用，则Java自动进行垃圾回收。

在Spring中使用容器对Bean的生命周期进行管理。

Spring中bean的生命周期

- 实例化bean
- 填充属性
- Bean可以使用
- 容器关闭，Bean被销毁

同时Bean还可以通过实现接口，对Bean的生命周期进行自定义

---

##### 将使类能够被扫描的注解

- `@Component`：下面三个都是基于`@Component`的，主要的差异是表示不同的组件
- `@Service`:用于Service层
- `@Repository`:用于DAO层
- `@Controller`:



`@Bean`也可以产生Bean，不过该注解作用于方法上，Spring通过该方法得到一个Bean



