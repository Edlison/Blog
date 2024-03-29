---
title: Microsoft Admin API
categories:
- MS
---

# Intro

添加用户后还需要登录用户进入OneDrive才会分配空间

<!--more-->

# Compose

```yaml
version: '3'

services: 
    msadmin: 
        image: logr/microsoft:latest
        ports:
            - 8099:8099
        volumes: 
            - ./config:/config
            - ./db:/root/.graph/db
```

# Config

命名为`application-dev.yml`放入config目录下

```yaml
spring:
  mail: # 邮件配置，自行修改
    host: smtp.qq.com # smtp.qq.com
    username: 123@qq.com # 发送邮箱地址
    password:  123 # 发送邮箱密码
  output:
    ansi:
      enabled: always
  h2:
    console:
      settings:
        web-allow-others: true
      path: /h2-console
      enabled: false
  datasource:
    # 初始化数据导入
#    data: classpath*:db/data.sql
#    sql-script-encoding: utf-8

    initialization-mode: always
    continue-on-error: true

    # h2 内存数据库 配置
    driver-class-name: org.h2.Driver
    url: jdbc:h2:${graph.db.path}
    username: graph
    password: 123456
  jackson:
    date-format: yyyy-MM-dd HH:mm
    time-zone: GMT+8
  jpa:
    hibernate:
      ddl-auto: update
    properties:
      hibernate:
        format_sql: false
    show-sql: false
#  redis: # redis 配置
#    database: 0
#    host: 127.0.0.1
#    port: 6379

# 程序自定义配置
graph:
  cache:
    token: default # token 缓存方式默认内存，redis 方式 需要配置 redis
    timeout: # 缓存超时时间  单位分钟
      user: 60 # 默认一小时
      license: 1440 # 默认一天
      domain: 1440 # 默认一天
  db:
    path: ${user.home}/.graph/db/graph

  # 后台登陆配置
  userName: edlison # 登陆账户,自行修改
  password: yourpwd # 登陆密码，自行修改

  # 邀请注册配置
  invite: mjj,mjj2 # 可以被注册的账号类型，为下面 configs.appName 的配置（必填，','分隔）
  inviteSub: # 为空表示全部
  inviteDomain: # 为空表示使用默认域名，格式：xxx.onmicrosoft.com
  usageLocation: HK,US #（此处会针对上面的配置覆盖）可选择的地区，用','分隔，首个将成为默认值，为空表示只使用HK（可以为空）

  # api配置
  configs:
  - appName: mjj # 自定义该账号的类型（建议使用英文：默认域名前缀，必填）
    appId: mjj # 应用程序(客户端) ID client（必填）
    appTenant: mjj # 目录(租户) tenant（必填）
    appSecret: mjj # secrets（必填）
    admin: mjj # 全局管理员账号（可以为空）
    usageLocation: HK,US #（此处会针对上面的配置覆盖）可选择的地区，用','分隔，首个将成为默认值，为空表示只使用HK（可以为空）
  - appName: mjj2 # 账号2配置，如果不需要请删除
    appId: mjj2
    appTenant: mjj2
    appSecret: mjj2
    domain: mjj2
    admin: mjj2
    usageLocation: US #（此处会针对上面的配置覆盖）可选择的地区，用','分隔，首个将成为默认值，为空表示只使用HK（可以为空）
  subscribed: # 订阅类型，自行添加其他
  - skuName: STANDARDWOFFPACK_STUDENT
    displayName: A1 学生版
    skuId: 314c4481-f395-4525-be8b-2ec4bb1e9d91
  - skuName: STANDARDWOFFPACK_FACULTY
    displayName: A1 教师版
    skuId: 94763226-9b3c-4e75-a931-5c89701abe66
  - skuName: OFFICE_365_A1_PLUS_FOR_STUDENT
    displayName: A1P 学生版
    skuId: e82ae690-a2d5-4d76-8d30-7c6e01e6022e
  - skuName: OFFICE_365_A1_PLUS_FOR_FACULTY
    displayName: A1P 教师版
    skuId: 78e66a63-337a-4a9a-8959-41c6654dfb56
  - skuName: M365EDU_A3_STUUSEBNFT_RPA1
    displayName: A3 无人值守版
    skuId: 1aa94593-ca12-4254-a738-81a5972958e8
  - skuName: Office_365_E3Y
    displayName: E3Y
    skuId: 6fd2c87f-b296-42f0-b197-1e91e994b900
  - skuName: DEVELOPERPACK_E5
    displayName: E5 开发者订阅
    skuId: c42b9cae-ea4f-4ab7-9717-81576235ccac
```







----

Reference

https://github.com/6mb/Microsoft-365-Admin