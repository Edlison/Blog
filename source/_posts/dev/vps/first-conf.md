---
title: configure new VPS
categories: 
- VPS
tags: 
- linux
- ubuntu
---

# user

## add new user

```sh
adduser ubuntu  # new user's direction automatically
useradd ubuntu  # need to new dir manually
```

## add user to admin group / edit sudoers

```sh
groupadd superadmin
usermod -g superadmin ubuntu
```

```sh
adduser ubuntu --ingroup sudo  # new user and assign to sudo group
```

```sh
vim /etc/sudoers
```

## user state

```sh
id ubuntu
```

# upload public key

```sh
ssh-keygen
```

new file `authorized_keys` and paste your own public key into this file.

# change login method

```sh
cd /etc/ssh
vim sshd_config
```

```
RSAAuthentication yes
PubkeyAuthentication yes
PermitRootLogin yes
PasswordAuthentication no
```

