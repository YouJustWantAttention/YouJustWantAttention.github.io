---
layout: default
titile: 第三章 Socket-UDP快速入门
published: 2019-10-04
tags: [Socket网络编程]
---

*UDP：user datagram protocol*
- 用户数据协议，而非连接协议，不需要连接

**为什么不可靠**
- 数据发送之后不做备份
- 头部仅加了复用和数据校验
- 发送端发送数据，服务器端从网络中抓取数据（UDP中其实没有标准的c/s）
- 结构简单、无校验、速度快、容易丢包、可广播   

**能做什么**
- DNS、TFTP、SNMP
- 视频、音频、普通数据（无关紧要）

<u>数据大于65507的时候手动分包</u>

**UDP核心API**
- DatagramSocket：  
    - 接收与发送UDP的类
    - 不同于TCP，UDP没有合并到Socket API中
    - recive（DatagramPacket d）
    - send（DatagramPacket p）
- DatagramPacket

**广播地址**
- 255.255.255.255是受限广播地址
- C网的广播地址：XXX.XXX.XXX.255（最后为255）
- D类的广播地址为多播预留

<u>一个32位IP地址可以用一个int类型存储</u>


