---
title: Action部署Hexo的问题
categories:
- Notebook
---

# 问题

## 主题的submodules在这个场景下很鸡肋

- 如果使用submodules来管理本地的config无法同步
- 如果不使用submodules来管理, 自动部署会修改全部文件的修改时期, 导致所有文章发布日期全部一致

