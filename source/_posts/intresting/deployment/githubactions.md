---
title: auto upload cos by Github Actions
categories: 
- VPS
tags: 
- ci
---

# tencent cos

1. 开通cos的api账号
2. 将api密钥添加到github项目secret

## workflows

```yaml
# This is a basic workflow to help you get started with Actions

name: homepage-ci

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      # Runs a single command using the runners shell
      - name: Install coscmd
        run: sudo pip install coscmd

      # Runs a set of commands using the runners shell
      - name: Configure coscmd
        env: 
          SECRETID: ${{ secrets.SECRETID }}
          SECRETKEY: ${{ secrets.SECRETKEY }}
          BUCKET: homepage-1304875656
          REGION: ap-shanghai
        run: coscmd config -a $SECRETID -s $SECRETKEY -b $BUCKET -r $REGION
      - name: Upload file
        run: coscmd upload -r ./ / --ignore "./.git/*"
```



---

Reference

https://cloud.tencent.com/developer/article/1545303