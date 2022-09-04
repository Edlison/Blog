---
title: 设计模式
categories:
- Notebooks
tags:
- java
- design-pattern
---

# Intro

软件构造课再学设计模式

<!--more-->

# UML

## 类

名字层

变量层[变量名:类型]

方法层[方法名(参数):类型]

> public: +
>
> protect: #
>
> private: -

## 接口

名字层[<<Interface>> + 斜体名字]

**常量**层[常量名:类型]

方法层[方法名(参数):类型]

> public: + 接口只能public且不能有变量

## 继承关系

A类继承B类.

实线+三角

## 关联关系

A类中的成员变量是由B类声明的.

实线+箭头

## 实现关系

A类实现B接口

虚线+三角

## 依赖关系

A类中的某个方法是由B类声明的.

虚线+箭头

## 注释

虚线连接一个文本框.

# Java中的Interface与Abstract

Interface没有数据成员变量, 只有静态常量. 方法只可以被定义不能实现.

Abstract Class可以有数据成员. 方法可以只定义(abstract func), 也可以实现.

Abstract是介于Interface和Class之间的产物.

# 设计模式

## 工厂方法模式

### 角色

- 抽象产品
- 具体产品
- 抽象工厂
- 具体工厂

### 解释

具体产品实现抽象产品

具体工厂实现抽象工厂

具体工厂内部实例化具体产品

## 虚拟工厂模式

### 角色

- 抽象产品
- 具体产品
- 抽象工厂
- 具体工厂

### 解释

与工厂方法基本一致.

区别在于有m个产品, 每个产品有n个产品线.

需要n个具体工厂, 来生产m个产品.

## 观察者模式

### 角色

- 虚拟主题
- 具体主题
- 虚拟观察者
- 具体观察者

### 解释

每个具体主题下有观察者的数据成员, 且依赖于观察者(通过方法添加到数据成员中).

每个具体观察者有主题的数据成员, 实例化时传入主题.

## 适配器模式

### 角色

- 目标
- 适配器
- 被适配物品

### 解释

场景: 只有一个3口插座, 空调(3口), 电视(2口), 都需要接入. 通过适配器来实现2口转3口.

目标有一个需要被实现的方法`connect()`

2口转3口适配器实现3口插座

空调实现3口插座

电视实现2口插座

```java
Plug3Out plug3Out;

AirConditioner airConditioner = new AirConditioner();
plug3Out = airConditioner;
plug3Out.connect();

Television television = new Television();
TreeOutAdapter chargerAdapter = new TreeOutAdapter(television);
plug3Out = chargerAdapter;
plug3Out.connect();
```

适配器和被适配物品都要实现目标.

因此适配器的方法实现其实是调用传入的被适配物品.

适配器本质上是一个传入了实现2口插座的物品, 实现了3口插座的适配器.













