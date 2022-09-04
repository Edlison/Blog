---
title: Metamod 和 ScourceMod 的关系
---

# Intro

转载

> 妹他(meta)mod | 索尔斯mod的关系和妹他mod的编写

# Diff

很久以前，Metamod:Source和Sourcemod这两个东西都还没有，服务器插件都是用相关游戏的sdk生成的dll，并将*.vdf文件放入addons文件夹来引导该dll来嵌入服务器使用的内存空间，以改变游戏功能(用英语来说就是黑客，只不过这个黑客功能是valve官方发布的)，但是用sdk生成dll的步骤及其复杂，不少人连visual studio都没装好就弃坑了，而且sdk源码还是有错误的，需要自己修复，插件编写界一片死寂。。 后来，插件编写界里一个叫AlliedModders的团队冒出了一个可怕的想法，他们想把sdk源码的错误全部都修复，以及为开发者提供一些简单的c++接口来挂钩游戏功能（仍然可以用sdk中的功能），看似慌得一批，其实稳如老狗，他们成功了，插件编写界顿时就活了起来，猿们安居乐业，开开心心写游戏插件，这就是Metamod:Source的由来，他继承了sdk无所不至的功能并且修复了一大堆valve犯下的错误（感谢AlliedModders）

然而AlliedModders的野心并不只这些，他们希望不会c++的人去学习pawn语言也能成为插件程序猴，于是他们封装了大部分底层的c++代码，并做出一个叫Sourcemod的平台，因为AlliedModders提供了sourcemod插件的编写和编译，Metamod:source的教程又晦涩难懂，所以大部分猿们都跑去了sourcemod编写插件，至此AlliedModders已经完成了他们的目标，就此止步，开始更新和维护sourcemod与metamod:source 相信不少读者恍然大悟了，想用官方的sourcemod，你还得装metamod，还是那句话，作为一个好人，其实我发表这篇文章最主要的是我碰到过一个被植入后台程序的sourcemod整合包，那包好生厉害，把机器信息什么的发到尾号为49的qq邮箱，还好发现得早，把机器信息换成一教育信发送了出去（现在成为了队友），希望大家多多注意个人信息的安全，少下载那些来源不明，下载量极少的插件平台，上面文章有什么错误的地方，还请多多指教









---

References

https://tieba.baidu.com/p/5386814052?red_tag=2856250620