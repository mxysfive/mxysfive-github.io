[TOC]

# 总线



> 本讲主要介绍总线的相关概念

## 总线的基本概念

> 什么是总线？

总线是连接各个部件的信息传输线，是各各部件共享的传输介质

总线上信息的传输，分为**串行**和**并行**

- 串行方法下，比特一个接一个的通过总线传输到接收段。接收方一个一个接收
- 并行方法下，往往是***一横排多个数据线***，比特并行地从一段传到另一端。接收端一排一排的接受。带来的问题是如果传输距离过长，传输的信号就会变形，所以并行往往适合短距离的传输。

## 单总线模型

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2F97GyjX59AQJ8bfv2DmFU%2F%E5%8D%95%E6%80%BB%E7%BA%BF.jpg?alt=media&token=507bdb07-9de6-4750-933e-93449cb48fc7)

单总线模型的特点是：

​	每一时刻，只能有一对设备使用总线

所有设备信息的交换都用一条总线，设备之间会激烈地争抢总线的使用权，很明显带来系统瓶颈

## 以CPU为核心的双总线模型

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2FMBQHKCFH7MYgq4q5hDRJ%2F%E5%8F%8C%E6%80%BB%E7%BA%BF.jpg?alt=media&token=ee0271e4-ed0c-4b51-b32d-75cd7c583da3)

特点：

​	适配了CPU与主存之间频繁的数据、指令传输，引入一条单独的总线于CPU和主存之间

**仍然有一个问题**：主存和IO设别之间没有直接相连的总线，这意味着如果有二者之间的数据传输，需要通过CPU来进行，这会十分影响CPU的工作效率

## 以存储器为中心的双总线模型

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2FUJ8XEXKeKUOPp650zcfp%2F%E5%AD%98%E5%82%A8%E5%99%A8%E4%B8%BA%E4%B8%AD%E5%BF%83.jpg?alt=media&token=7c1ca915-0758-4404-ac28-978ffacd6df8)

特点：

- 保证了主存于CPU之间单独的数据传输能力
- CPU可以直接与IO设备之间传输数据
- 主存可以直接与IO设备之间传输数据

## 总线的分类

### 片内总线

​	芯片内部的总线，是芯片内部的数据传输介质

### 系统总线

​	是系统见各个部件的信息传输线，具体分为三类

> 【注】传输的方向是以CPU为基准的，即相对于CPU，数据是朝哪个方向传输的

- 数据总线 

  ​	双向， 负责传输数据， 与机器字长，存储字长有关，注意是有关不是相等

- 地址总线

  ​	单向， 与存储地址， IO地址有关

- 控制总线

  ​	有出、有入 负责设备之间状态的反馈，设备之间写作传递的一些信号值通过控制总线来做

  ​	出方向：存储器读，存储器写，总线许可，中断确认

  ​	入：中断请求，总线请求

- 通信总线

  ​	用于本计算机和其他计算机系统的通讯的数据传输介质。同样地，有并行和串行两种数据传输方式

## 总线特性以及性能指标

总线特性

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2Fpt6R7DQyBTMZBkBqNZIz%2F%E6%80%BB%E7%BA%BF%E7%89%B9%E6%80%A7.jpg?alt=media&token=e9263c99-f201-4c0e-bab3-b29a23d05740)

## 总线性能指标

- **总线宽度**： 实际上就是数据线的根数，代表了总线一次能传输多少数据的位数
- **标准传输率**：每秒传输的最大字节数（MBps）
- **时钟同步/异步**: 同步传输，不同步传输，后续会具体介绍
- **总线复用**：地址线和数据线共用，比如IBM8086
- **信号线数**：地址线，数据线，控制线之和
- **总线控制方式**：突发、自动、仲裁、逻辑、计数
- **其他**：负载能力

## 总线结构

这部分主要是介绍一些常识，涉及到的概念会以后讲。

### 三总线结构

在高速IO设备和主存储器当中引入DMA（Directly Memory Access）

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2F6aDhlFpy5d3rybJ7lqLQ%2FDMA%E6%9E%B6%E6%9E%84.jpg?alt=media&token=55aecab9-8110-4088-bbf2-eeca07b093e6)

### 四总线架构

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2FKJM7ol14PiOUOj0oLXYg%2F4%E6%80%BB%E7%BA%BF.jpg?alt=media&token=c52b0e78-25e7-4471-9ef0-06fceecd2864)



## 总线控制（重难点）

多个设备可能同时发出占用总线的请求，如何决定哪个设备使用总线呢？

占用了总线如何完成通信的正确性

总线的判优控制

> 基本概念

- 主设备（模块）：对总线有控制权
- 从设备（模块）：响应从主设备发来的请求

> 【注】一个主线可以有多个主设备也可以有多个从设备。 有些设备可能既是主设备又是从设备。

总线判优方式

- 集中式：所有的判优逻辑放到一个集中的设备来处理，分为链式查询，计数器定时查询，独立请求方式。下面有详细介绍
- 分布式：每个设备引入自己的判优模块或者各个设备的端口上

链式查询方式

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2FDYVIKsi5MhSHUb23D846%2F%E9%93%BE%E5%BC%8F%E6%9F%A5%E8%AF%A2.jpg?alt=media&token=4f36e7c3-c143-4dbf-abd1-15cb3afa7d3d)

### 链式查询执行流程：

1. 当某个想要占用总线时，通过BR线发出请求。（这里注意一个小问题，就是这是总线是一个数据线本质上，控制部件中的接收设备仅仅能感知到的是电信号的变化。并不能智能地得出是哪个IO接口提出的占用请求）
2. 若总线此时不在忙，则通过BG线，以此轮询每个IO接口，就算有多个IO接口同时请求，BG线也只找到第一个（即离总线控制部件最近的）请求的IO接口。详见如图，接口1和n都同时请求了总线的使用权。
3. 拿到控制权的接口通过BS总线宣告总线忙，表示此时对总线的占用

特点：

- 可拓展性好，直接往线上串联就好
- 位置靠后的设备（即可以理解成优先级低的设备）可能发生**饿死**的现象
- 故障敏感，如果BG线出了问题，判优过程则无法继续下去

### 计数器定时查询方式

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2F9ASGKhmgWNkqtIM2eJc5%2F%E8%AE%A1%E6%97%B6%E5%99%A8%E6%9F%A5%E8%AF%A2.jpg?alt=media&token=88ff8f03-45d8-46bf-9611-6fa37dc11387)

1. 流程类似，不再赘述。主要看看计数器的功能
2. 当总线不忙时，即总线可以被某一设备使用时，计数器就会使用，计数器的值通过设备地址这条线进行输出。（由于你每个**IO接口**都是被**二进制编号**了的，当你通过**设备地址线**拿到这个计数器的**值**后，你就可以知道当前计数器询**问的是不是你这个IO接口了**）。
3. 如果没有发出过请求，则计数器自动自加1，同时重新输出设备地址，直到计数器的值和接口编号发生第一次匹配后则停止计数器的自加操作。
4. 之后就是通过总线忙这条线表达对总线的占用。

特点：

- 要给设备用二进制编号，编好顺序
- 更灵活的设置优先级，比如让每次询问都从上次结束的下一个位置开始（最后一个的后一个是第一个），这样可以避免饿死现象的发生

### 独立请求的方式

![img](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fbb0VWPrIP2j94KFxPSno%2Fuploads%2FtMEw42O4uR7wN1e6pTn3%2F%E7%8B%AC%E7%AB%8B%E8%AF%B7%E6%B1%82.jpg?alt=media&token=c1719899-11f6-4da2-8cea-e2e8c6351bc7)

这个就比较好理解了，每个IO接口有自己的BG & BR，控制器内部有**排队器，**所有的请求都会被送到排队器里来决定，**优点是可以设计灵活的排队算法。**



## 总线通信控制

> 总线通信的目的是：解决通信双方的协调配合问题

![总线传输周期]()

### 总线通讯的四种方式

- 同步通信：由统一时钟控制主设备从设备之间的传输，要求有**定宽，定距的时钟周期**来通信
- 异步通信：从设备采用应答机制，没有统一的时钟控制
- 半同步通信：同步、异步结合，主要解决设备之间**数据访问、传输速度不同**带来的问题
- 分离式通信：最牛的通讯方式，充分发挥总线性能



### 同步通信

> 核心理解是要在固定时间点上给出固定的操作，通过时钟脉冲的高低电平来控制各个功能的开始结束点

#### 同步输入

![同步输入](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%90%8C%E6%AD%A5%E6%95%B0%E6%8D%AE%E8%BE%93%E5%85%A5.jpg)

比如在第一个时钟上升沿给出地址，在第二个时钟给出读信号，第三个时钟开始从从模块读入数据

**有个前提就是从模块必须把数据放到DataBus上，然后t3读入数据，t4撤销总线信号，释放总线**

#### 同步输出

![同步输出](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%90%8C%E6%AD%A5%E8%BE%93%E5%87%BA.jpg)

T1上沿之前准备好地址，这是欲输出位置的地址，在T1下沿之前准备好数据，把数据放到DataBus上，在T2上沿之前发出写命令。

T4上沿结束控制总线喝数据总线的命令。

> 适用场景：主从模块之间距离比较短，且数据存取时间较为一致

### 异步通信

![异步](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%BC%82%E6%AD%A5.jpg)

- 不互锁：主设备发了以后，从设备应答，一段时间后主设备就撤销通信请求。 这样的通信可靠性比较低
- 半互锁：主设备请求，从设备应答，同时从设备的应答信号发给主设备，如果收到从设备的应答信号，则主设备撤销，否则一直等待下去。 **问题是：从设备不管主设备是否收到自己的应答信号，隔一段时间自己就关了，这样可能造成主设备一直请求（因为它在等从设备的应答信号）
- 类似三次握手，可靠的通信方式

### 半同步通信

同步异步相结合的一种通信方式

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%90%8C%E6%AD%A5%E5%BC%82%E6%AD%A5%E7%BC%9D%E5%90%88.jpg)



#### 半同步通信，以输入为例

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%8D%8A%E5%90%8C%E6%AD%A5%E8%BE%93%E5%85%A5.jpg)

> 只有当从模块准备好时，才会给WAIT信号线发一个高电平，此时主模块就知道从模块已经把数据放到DataBus上了

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%8D%8A%E5%90%8C%E6%AD%A5%E7%A4%BA%E6%84%8F%E5%9B%BE.jpg)

这种方式允许不同速度的主从设备进行信息交换。



### 分离式通讯

一个总线的传输周期可分为三部分，其中有一部分总线时空闲的。

- 主模块发地址，发命令  **占用总线**
- 从模块准备数据  （从模块自己准备自己的数据，比如磁盘定位数据这种操作）**不占用总线**
- 从模块向主模块发数据  **占用总线**

> 分离式通信的核心就是主从设备将准备数据的时间让出给其它的设备对，让其他设备对可以工作。很好理解，不再赘述

#### 分离通信的特点

- 各个模块都有可能做主设备
- 实现方式是采用同步通信方式，不等对方回答
- 各模块准备数据时，这对模块不占用总线
- 总线被占用时，无空闲。（老师的解释是总线一旦被占用总是再传输控制指令或者传数据）



# 存储器

> 存储器可分为哪些类型，下两图分别是以存取方式和在计算机中位置为原则作为分类标准的

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%AD%98%E5%8F%96%E6%96%B9%E5%BC%8F.jpg)

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E4%BD%8D%E7%BD%AE%E5%88%86%E7%B1%BB.jpg)





> 现代存储器层次结构为什么要分层：为了填补不同设别间设备的鸿沟

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E5%AD%98%E5%82%A8%E5%B1%82%E6%AC%A1.jpg)

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/2%E4%B8%AA%E5%B1%82%E6%AC%A1.jpg)

> 上面的就不赘述了都是宏观的尝试



## 主存储器

### 主存的基本构成

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E4%B8%BB%E5%AD%98%E7%BB%84%E6%88%90%E5%9B%BE.jpg)



### 主存与CPU的联系

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E4%B8%BB%E5%AD%98CPU.jpg)

> 由上图可以看出，MDR MAR 实际上是嵌入在CPU中的，但仍然在逻辑上属于主存的一部分

### 主存中存储单元地址的分配

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E4%B8%BB%E5%AD%98%E5%9C%B0%E5%9D%80%E5%88%86%E9%85%8D.jpg)

- 大端存储：高位字节在低地址
- 小端存储：低位字节在低地址

> 记忆方法：把W当成2B，4B  注意看为什么按字寻址的话，可寻址的字会少呢？注意看图，字地址实际上是字节地址的子集，字地址可不是自己重新按0，1，2，3.....独立编号的

### 主存储器的技术指标

![](https://cs-dbop-1312160430.cos.ap-beijing.myqcloud.com/OrganizationPrinciple/%E4%B8%BB%E5%AD%98%E6%8C%87%E6%A0%87.jpg)

> 课堂上老师说注意区分存期时间和存取周期不是一回事，一般存取周期要长于存取时间