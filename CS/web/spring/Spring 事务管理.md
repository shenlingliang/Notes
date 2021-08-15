# 事务管理

#### 什么是事务

一组要么一起完成被提交，或者一起失败被回滚的操作称为事务。

**事务的特性**

- 原子性：事务不可再分，要么全部执行，要么全部回滚
- 一致性：执行事务前后，其他事务对数据库的访问获取的结果都相同。
- 隔离性：未提交事务的修改对其他事务不可见。
- 持久性：事务提交后它对数据库的修改是持久的，即使数据库崩溃也不会丢失。

**并发事务带来的问题**

- 脏读：可以读取到其他事务未提交的数据
- 丢失修改：事务A开始对某行数据进行修改，在提交前又有另一个事务B开始对该行数据进行修改，在A提交之后，B也提交，就丢失了A的修改。
- 不可重复读：事务执行过程中，多次读取某行数据，结果不同
- 幻读：事务执行过程中对某范围数据进行计数，之后再次进行计数，结果不同。出现插入或删除。

**事务的隔离级别**(由低到高)

![](https://markdown-1259282458.cos.ap-nanjing.myqcloud.com/img/20210810163508.png)

---

### Spring的事务管理

Spring并不直接管理事务，而是提供了多种事务管理的接口，把具体的事务管理交给持久化机制所提供的事务来实现。

Spring提供3种事务管理接口

- `PlatformTransactionManager`:事务管理器
- `TransactionDefinition`:事务定义信息(定义事务属性)
  - 包含事务隔离级别，传播行为，超时，只读，回滚规则。
- `TranscationStatus`:事务运行状态

#### PlatformTransactionManager

```java
public interface PlatformTransactionManager extends TransactionManager {
    TransactionStatus getTransaction(@Nullable TransactionDefinition var1) throws TransactionException;

    void commit(TransactionStatus var1) throws TransactionException;

    void rollback(TransactionStatus var1) throws TransactionException;
}
```

事务管理器，不同的持久化平台有不同的事务管理器

- iBatis/Spring JDBC 为`org.springframework.jdbc.datasource.DataSourceTransactionManager`

#### TransactionDefinition

```java
public interface TransactionDefinition {
    int PROPAGATION_REQUIRED = 0;
    int PROPAGATION_SUPPORTS = 1;
    int PROPAGATION_MANDATORY = 2;
    int PROPAGATION_REQUIRES_NEW = 3;
    int PROPAGATION_NOT_SUPPORTED = 4;
    int PROPAGATION_NEVER = 5;
    int PROPAGATION_NESTED = 6;
    int ISOLATION_DEFAULT = -1;
    int ISOLATION_READ_UNCOMMITTED = 1;
    int ISOLATION_READ_COMMITTED = 2;
    int ISOLATION_REPEATABLE_READ = 4;
    int ISOLATION_SERIALIZABLE = 8;
    int TIMEOUT_DEFAULT = -1;

    default int getPropagationBehavior() {
        return 0;
    }

    default int getIsolationLevel() {
        return -1;
    }

    default int getTimeout() {
        return -1;
    }

    default boolean isReadOnly() {
        return false;
    }

    @Nullable
    default String getName() {
        return null;
    }

    static TransactionDefinition withDefaults() {
        return StaticTransactionDefinition.INSTANCE;
    }
}
```

这个接口给出了事务属性定义的模版

事务属性是事务的一些基本配置，主要包括

- 隔离级别：定义了一个事务可能受其他并发事务影响的程度。
  - Spring中给出了5种隔离级别，多了一种使用数据库的隔离级别
- 传播行为：定义事务方法调用另外一个事务方法时，事务应该如何传播(事务嵌套的情况)
  - 支持当前事务的情况：
    - `TransactionDefinition.PROGAGATION_REQUIRED`:当前无事务就创建新事务，有事务就加入到事务中(Required,要求有事务，因此无事务就创建，有事务就加入)
    - `TransactionDefinition.PROGAGATION_SUPPORTS`:当前有事务则加入，如果不存在就以非事务执行
    - `TransactionDefinition.PROGAGATION_MANDATORY`：当前有事务就加入当前事务，当前无就抛出异常
  - 不支持当前事务的情况：
    - `TransactionDefinition.PROGAGATION_REQUIRES_NEW`：必须新建事务，如果当前存在事务就挂起当前事务
    - `TransactionDefinition.PROGAGATION_NOT_SUPPORTED`：不支持嵌套调用，当前存在事务则挂起，不存在事务以非事务方式运行
    - `TransactionDefinition.PROGAGATION_NEVER`：不允许嵌套调用，嵌套就抛出异常。
  - `TransactionDefinition.PROGAGATION_NESTED`:若当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；当前无事务则创建新的事务。
- 回滚规则：定义哪些异常回滚，那些不会
- 是否只读：事务对资源是否只是读操作
- 事务超时：一个事务允许执行的最长时间

#### TransactionStatus

```java
public interface TransactionStatus extends TransactionExecution, SavepointManager, Flushable {
    boolean hasSavepoint();

    void flush();
}

```

