---
title: Nginx start
categories:
- Nginx
tags:
- cli
---

# Intro

从0开始学nginx

<!--more-->

# Command Line

- `-?` | `-h` 打印帮助

- `-c *file*` — 使用一个指定的配置文件

- `-e *file*` — 使用指定的文件存储error log

- `-g directives` 设置全局配置指令

  ```sh
  nginx -g "pid /var/run/nginx.pid; worker_processes `sysctl -n hw.ncpu`;"
  ```

- `-p *prefix*` — 设置保存服务器配置的路径 (default value is `*/usr/local/nginx*`).

- `-q` — 压缩非错误信息

- `-s signal` 发送信号

  ```
  - `stop` — shut down quickly
  - `quit` — shut down gracefully
  - `reload` — reload configuration, start the new worker process with a new configuration, gracefully shut down old worker processes.
  - `reopen` — reopen log files
  ```

- `-t` — 检查配置文件语法

- `-T` — 与 `-t` 一致, 另外输出配置文件

- `-v` — print nginx version.

- `-V` — print nginx version, compiler version, and configure parameters.







----

References

http://nginx.org/en/docs