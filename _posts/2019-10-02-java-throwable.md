---
layout: default
title:  "java throwable"
date:   2016-12-07 09:00:00 +0200
published: 2016-12-07 09:00:00 +0200
comments: true
categories: integration
tags: [messaging, integration, iot]
---

Object--->Throwable

1. Error:程序自身无法处理，一般这种情况建议终止程序，属于JVM的管辖范围
2. Exception：
    1. RuntimeException：运行时异常，程序员的责任
    2. 非RuntimeException：受查异常，编译器的责任


**常见运行时异常RuntimeException**

 - 空指针异常
 - 类型转换异常
 - 传递非法参数异常
 - 下标越界异常
 - 数字格式异常

**非RuntimeException**

 - ClassNotFoundException
 - IOException

**Error**

 - StackOverflowError
 - OutOfMemoryError
