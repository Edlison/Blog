---
title: Minecraft Java客户端
categories:
- Game
tags:
- Minecraft
---

# Intro

MacOS使用Java客户端, 盗版.

<!--more-->

# Java环境

Java在Mac下默认安装在`/Library/Java/JavaVirtualMachine/jdk-xxx` 

`.zshrc`配置

```sh
# Java settings
JAVA_8_HOME=$(/usr/libexec/java_home -v 1.8)
JAVA_11_HOME=$(/usr/libexec/java_home -v 11)
JAVA_17_HOME=$(/usr/libexec/java_home -v 17)
export JAVA_HOME=$JAVA_17_HOME
export PATH=$JAVA_HOME/bin:$PATH
export CLASS_PATH=$JAVA_HOME/lib
```

`java` 与 `javac` 的版本需要一致

```sh
java -version
javac -version
```

版本问题会报错`A JNI error` 

# 盗版客户端

下载启动器[HMCL](http://hmcl.huangyuhui.net/) 

启动

```sh
java -jar HMCL.jar
```

选择对应的版本下载







---

References

http://hmcl.huangyuhui.net/