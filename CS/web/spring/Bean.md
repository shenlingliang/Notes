## Bean

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

Bean的生命周期从创建完成后，一直驻留在应用上下文中直到该应用上下文被摧毁。`Context.close()`



---

在应用开发中，我们希望各个模块相互关联，共同完成一个复杂的业务，但是我们又希望他们的联系不那么紧密，以至于导致修改其中一个模块就需要对另一个模块进行修改。

在Spring中，对象无需自己查找或创建与其所关联的其他对象，而是通过容器来对各个对象的依赖进行管理，通过容器吧需要相互协作的对象引用赋予各个对象。



创建应用对象之间协作关系的行为通常称为装配(wiring)

Spring中提供了3种装配bean的方式

- XML中进行显式配置
- Java中进行显式配置
- 隐式的bean发现机制和自动装配机制

#### 自动化装配bean

Spring从两个角度来实现自动化装配：

- 组件扫描(component scanning):spring会自动发现应用上下文中所创建的bean
  - `@Component(beanid)`:使用这个注解来表示Spring要为这个类创建一个bean
  - `@ComponentScan`:在Spring中启用组件扫描，该注解默认扫描与配置类同包中的组件。
- 自动装配(auto wiring):spring会自动满足bean之间的依赖
  - `Autowired`:
    - 寻找满足条件的bean进行注入
    - 可以用于修饰方法，构造器，setter，属性

#### 显式装配

尽管在很多场景下通过组件扫描和自动装配实现Spring的自动化配置是更为推荐的方式，但有时我们无法通过自动化装配完成配置，因此需要显式配置Spring

- JavaConfig：通过创建一个config类，进行配置
- XML

进行显示配置的时候，JavaConfig是更好的方案，因为它更强大，类型安全，且对重构友好。

创建一个JavaConfig类的关键在于为其添加`@Configuration`注解，该注解表明这个类是一个配置类，该类包含应该如何在Spring应用上下文中创建bean的细节。

要在JavaConfig中声明bean，我们需要编写一个方法，这个方法会创建所需类型的实例，然后给这个方法添加`@Bean`注解。

```java
@Bean
public CompactDisc sgtPeppers(){
		return new SgtPeppers();
}
```

`@Bean`注解会告诉Spring这个方法会返回一个对象，该对象要注册为Spring应用上下文中的Bean。方法体中包含了返回的bean的创建逻辑。

默认情况下产生的bean ID于带有`@Bean`的方法名相同。可以通过将注解变为`@Bean("name")`修改

**借助JavaConfig实现注入**

在JavaConfig中装配Bean最简单的方法就是引用创建bean的方法。

```java
@Bean
public CdPlayer(){
		return new CDPlayer(sgtPeppers());
}
@Bean
public anotherCdPlayer(){
  	return new CDPlayer(sgtPeppers());
}
```

这里的`sgtPeppers()`就是上面定义的用来生成`sgtPeppers`bean的方法。

此处因为`sgtPeppers()`是使用`@Bean`注解的方法，Spring会拦截所有对它的调用，并确保直接返回该方法是创建的Bean。因此上面两个cd播放器都是用同一个bean创建的。(Spring中Bean默认是单例)



----

### 高级装配

#### 环境与profile

在开发过程中，我们通常会需要将程序从一个环境迁移到另一个环境。如从开发环境`dev`迁移到测试环境`test`,而迁移后某些环境相关的做法可能就不再适用了，因此我们需要根据环境的不同，有这不同的配置。而如果为不同的环境创建不同的配置类，有些过于复杂。

在spring中可以通过环境不同，创建不同的bean。

spring中通过profile实现，通过将不同bean配置到不同profile中，激活不同的profile就会创建不同的bean。

可以通过`@Profile`指定某些bean属于哪个profile。

```java
@Bean
@Profile("prod")
public DataSource datasource(){
		return new ...;
}
```

如果一个bean被profile注解，那么它只会在该profile激活时被创建，若没有被profile注解，那么每个profile都会创建该bean。

而若要激活profile需要设置`spring.profiles.active`,`spring.profiles.default`

#### 条件化的bean

如果我们希望一个或多个bean只有应用的类路径下包含特定的库时才创建，或者我们希望某个bean只有当另外某个特定的bean声明了之后才会创建。我们需要使用`@Coniditional`注解，只有当给定条件计算为true时，该bean才会被创建

```java
@Bean
@Conditional(MagicExistsCondition.class)
public MagicBean magicBean(){
		return new MagicBean();
}
public interface Condition{
  	boolean matches (ConditionContext ctxt,AnnotatedTypeMetadata metadata);
}
```

其中`MagicExistsConditon`实现了`Condition`接口

#### bean的作用域

在默认情况下，Spring应用上下文中所有的bean都是以单例形式创建的。

但有时候，当所使用的类是易变的(mutable)，那使用单例就是不安全的。因此Spring定义了多种作用域，可以基于这些作用域创建bean：

- 单例(singleton):在整个应用中，只创建bean的一个实例
- 原型(prototype):每次注入或通过spring上下问获取时，都会创建一个新的bean实例
- 会话(session):在web应用中，为每个会话创建一个bean实例
- 请求(Request):在web应用中，为每个请求创建一个bean实例

spring中默认使用单例，若需要使用其他作用域要使用`@Scope`,它可与`@Component,@Bean`一起使用

```java
@Component
@Scope(ConfigurableBeanFactroy.SCOPE_PROTOTYPE)
public class Notepad{}
```

#### 运行时注入值

在spring中我们也经常需要将值注入到bean中，而除了在编译时就定下来注入的值，我们还可以在运行时进行值的注入。Spring提供了两种在运行时求值的方法：

- 属性占位符(Property placeholder)
  - Spring一直支持将属性定义到外部属性的文件中，并使用占位符值将其插入到spring bean中
  - 在spring装配中，占位符的形式为使用`${...}`包装的属性名称
- Spring表达式语言
  - `#{expression}`