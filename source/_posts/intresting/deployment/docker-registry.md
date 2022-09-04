---
title: Docker commit to self-hosted registry
categories:
- Docker
---

# Intro

提交image到私有仓库.

<!--more-->

# Commit

先将容器提交为一个新的镜像

```sh
docker commit container_id new_image_name
```

登录

```sh
docker login https://registry.edlison.com
```

相当于重命名

```sh
docker tag image_name registry.edlison.com/edlison/image:tag
```

push

```sh
docker push registry.edlison.com/edlison/image:tag
```

