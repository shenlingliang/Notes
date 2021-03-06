# Linux 信号

信号(signal)是linux进程间通信的一种机制，全称为软中断信号，也称为软中断。



信号是进程通信的一种忙时，与其他方式相比，信号是一些固定的常量，传递的信息很有限，但是也便于管理。



### 信号的产生

信号由内核管理，产生的方式多种多样。可以因为内核自身发现错误，生成信号。或由其他进程发出信号，由内核传递给指定进程。



### 信号的生效过程

内核中每一个进程都有一个表来保存信号。内核需要将信号传递给某个进程时，就在该进程对应的表中写入信号。而当该进程从用户态陷入内核态，再次切换到用户态之前，会对表进行检查，如果有信号，则进程会优先处理信号。(我们也可以编写代码，让进程阻塞或忽略一些信号)



#### 常见信号

| 信号         | 作用                                                         |
| ------------ | ------------------------------------------------------------ |
| SIGHUP   1   | 终端挂起或控制进程终止。当用户推出命令行时，由该进程启动的所有进程都会收到这个信号，默认动作为终止进程 |
| SIGINT   2   | 键盘中断。用户按下组合键，用户终端向正在运行中的进程发送此信号。默认动作为终止进程。 |
| SIGKILL 9    | 无条件终止进程                                               |
| SIGTERM   15 | 程序结束信号，该信号可被阻塞和终止，以便程序完成退出前的工作。 |

