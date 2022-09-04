---
title: Network
catagories:
- Notebook
tags:
- tcp
- ip
---

# Intro

网络的知识很多都忘了, 记录一些自己一直搞混的概念.

<!--more-->

# 代理的区别

http_proxy是在应用层上的代理, 仅代理http流量.

socks5是在传输层上的代理, 可以代理一切应用层的流量.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211210035849.png)

# SSL TLS 协议

SSL/TLS是一种密码通信框架.

SSL(Secure Socket Layer)安全套接层, 是1994年由Netscape公司设计的一套协议，并与1995年发布了3.0版本.

TLS(Transport Layer Security)传输层安全是IETF在SSL3.0基础上设计的协议, 实际上相当于SSL的后续版本.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211210035901.png)

# Socket WebSocket

Socket 套接字, 是计算机之间进行通信的一种约定. 

>socket起源于Unix，而Unix/Linux基本哲学之一就是“一切皆文件”，都可以用“打开open –> 读写write/read –> 关闭close”模式来操作。
 　我的理解就是Socket就是该模式的一个实现：即socket是一种特殊的文件，一些socket函数就是对其进行的操作（读/写IO、打开、关闭）。
 　Socket()函数返回一个整型的Socket描述符，随后的连接建立、数据传输等操作都是通过该Socket实现的。

WebSocket 是一种网络通信协议, 因为 HTTP 协议有一个缺陷, 通信只能由客户端发起.

WebSocket 可以实现服务器主动向客户端推送信息, 客户端也可以主动向服务器推送信息, 双向平等对话.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211210040436.png)

---

Reference

https://zhuanlan.zhihu.com/p/33889997

https://zhuanlan.zhihu.com/p/133375078

https://www.jianshu.com/p/066d99da7cbd

http://www.ruanyifeng.com/blog/2017/05/websocket.html

