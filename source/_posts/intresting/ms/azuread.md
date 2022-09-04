---
title: Azure Active Dictionary
categories:
- MS
---

# Intro

对Azure AD的一些理解

<!--more-->

# 空全局

## 创建租户

进入Azure Active Dictionary

初始域名就是之后进入Admin Center的域名

## 新建用户

创建一个该域名下的全局管理员

退出当前账号

登录创建的全局管理员

进入用户删除用于创建租户的账号

## 问题

有的账号无法创建租户, 显示没有权限

# 注册应用

相当于是申请API

## 申请备用权限API

1. 注册应用
2. API权限->添加权限->MicrosoftGraph->应用程序权限

```
主要需要这几个权限 搜索添加
Administrative Directory EduAdministration Files RoleManagement User
```

3. 搜索添加->代表主机信息授予管理员同意
4. 证书和密码->添加客户端密码

通过应用程序ID和密码值就可以请求API

## 申请Cloudreve挂载API

1. 注册应用
2. 添加客户端密码

在获取授权的时候需要有权限的用户登录, 因此感觉只是被分配了订阅的用户授权这个API, 然后Cloudreve又可以访问应用API, 从而访问用户的OneDrive

一个应用注册对应一个用户? or 已给应用注册可以用多个用户授权?

# 理解

Azure Active Dictionary就是Admin Center的后台

可以实现更细致和复杂的操作, 如设置API







----

Reference

https://hostloc.com/thread-829547-1-1.html