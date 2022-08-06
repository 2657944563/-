# CAS

## 简介

​		一种无锁的算法理念，使用对比然后赋值的思维，当数据的值改变了那么重新执行。

## 使用

​		配合volatile可以实现无所并发，适用于线程数少，多核CPU的场景下，当线程大于CPU还是会造成上下文切换导致性能有所下降。

## 特点

1. CAS是基于乐观锁的思想，最乐观的估计，不怕别的线程来修改共享变量 ，就算修改了也没关系，重试即可
2. synchronized是基于悲观锁的思想，最悲观的情况需要防止别的线程修改共享变量，等待自己操作完再让别人操作
3. CAS的体现是无锁并发，无阻塞并发
   1. 因为没有使用synchronized，所以线程不会主动阻塞
   2. 如果竞争激烈，重试必然会很多，效率反而下降

![image-20220321182613593](C:\Users\2657944563\Desktop\Java思维导图\image-20220321182613593.png)

# 原子整数

## 简介

Java的JUC(java.until.concurrent)包下提供了可以进行原子操作的类

## 三个原子整数类

Atomic Integer，Atomic Boolean，Atomic Long

### AtomicInteger

一些方法的记录

- #### updateAndGet(x->( x + 10))

  - 用于原子性执行一些算术运算

- compareAndSet(num1 , num2)
  - 如果num1与对象值相等，那么赋值num2给对象

# 原子引用

## 简介

用于解决ABA问题

## 三个原子引用类

Atomic Reference,Atomic Markable Reference,Atomic Stamped Reference

### Atomic Stamped Reference

一个拥有版本号的原子引用类，构造方法需要传入一个版本号，CAS方法的时候可以额外判断版本号(stamp)

# 原子数组

## 简介

提供对数组的原子操作

### AtomicLongArray

### AtomicIntegerArray

### AtomicReferenceArray

# 原子类字段

## 简介

提供类中成员变量的原子引用，使用必须将被保护的原子类设置**volatile**关键字

### AtomicReferenceFieldUpdater

### AtomicIntegerFiledUpdater

### AtomicLongFiledUpdater



# 原子累加器

## 简介

提供累加功能的原子操作，性能优秀，与原子整数类做同样的操作有4-5倍的效率

## 底层

当有竞争累加的时候，会开辟多个累加单元，最后将这些结果汇总。减少了CAS的重试

### 	LongAdder

### 	LongAccumulator

### 	DoubleAdder

### 	DoubleAccumulator