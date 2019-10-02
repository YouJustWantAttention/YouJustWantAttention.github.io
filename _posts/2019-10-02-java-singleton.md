---
layout: default
title: Java中的单例模式
published: 2019-10-02
category: 设计模式
tags: [设计模式]
---
# lazyLoad-unThreadSafe

```java
public class SingleTon {
    private static SingleTon instance = null;
    private SingleTon(){};
    public static SingleTon getInstance(){
        if(instance == null)
            instance = new SingleTon();
        return instance;
    }
}
```
**优点：懒加载启动快，资源占用小，使用时才实例化，无锁。
缺点：非线程安全。**

# lazyLoad-threadSafe
```java
public class SingleTon {
    private static SingleTon instance = null;
    private SingleTon(){};
    //加锁
    public static synchronized SingleTon getInstance(){
        if(instance == null)
            instance = new SingleTon();
        return instance;
    }
}
```
 **优点：同上，但加锁了。
 缺点：synchronized 为独占排他锁，并发性能差。即使在创建成功以后，获取实例仍然是串行化操作。**

# double-check

```java
public class SingleTon {
	// volatile
    private volatile static SingleTon instance = null;
    private SingleTon() {};
    public static SingleTon getInstance() {
        if (instance == null)
            synchronized (SingleTon.class) {
            	//double-check
                if(instance == null)
                    instance = new SingleTon();
            }
        return instance;
    }
}
```
**优点：懒加载，线程安全。
 注：实例必须有 ==volatile== 关键字修饰，其保证初始化完全。还要注意==第二次的null判断==**
# Eager Singleton

```java
public class SingleTon {
    private static SingleTon instance = new SingleTon();
    private SingleTon(){};
    public static SingleTon getInstance() {
        return instance;
    }
}
```
**优点：饿汉模式天生是线程安全的，使用时没有延迟。
 缺点：启动时即创建实例，启动慢，有可能造成资源浪费。**

# Holder
```java
public class SingleTon {
    private static class SingletonHolder{
        private static SingleTon instance = new SingleTon();
    }
    private SingleTon(){};

    public static SingleTon getInstance() {
        return SingletonHolder.instance;
    }
}
```
** 优点：将懒加载和线程安全完美结合的一种方式（无锁）。（推荐）**

# Enum

```java
public enum Singleton {
    INSTANCE;
    public void whateverMethod(){};
}
```
==注意声明的是enum，不是class==
**我们定义的一个枚举，在第一次被真正用到的时候，会被虚拟机加载并初始化，而这个初始化过程是线程安全的。而我们知道，解决单例的并发问题，主要解决的就是初始化过程中的线程安全问题。所以，由于枚举的以上特性，枚举实现的单例是天生线程安全的。**
