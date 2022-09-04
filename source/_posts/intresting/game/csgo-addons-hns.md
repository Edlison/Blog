---
title: CSGO HNS 插件
categories:
- Game
tags:
- csgo
---

# Intro

HNS模式用到的插件

<!--more-->

# HNS

[Link](https://forums.alliedmods.net/showthread.php?t=239132) 

# Jumpstats

## KZTimer Jumpstats

[Link](https://forums.alliedmods.net/showthread.php?t=252392) 

`database.cfg`

```
"kzjumpstats"
    {
        "driver"            "sqlite"
        "host"                "localhost"
        "database"            "kzjumpstats-sqlite"
        "user"                "root"
        "pass"                ""
    }
```

结合`hns.cfg`

```
min - client msg
pro - client perfect quake sound,  green chat msg
leet - client godlike quake sound, red chat msg

js_dist_min_bhop 250
js_dist_pro_bhop 255
js_dist_leet_bhop 260
js_dist_min_multibhop 250
js_dist_pro_multibhop 255
js_dist_leet_multibhop 260
js_dist_min_lj 235
js_dist_pro_lj 240
js_dist_leet_lj 245
js_dist_min_wj 235
js_dist_pro_wj 240
js_dist_leet_wj 245
js_dist_min_dropbhop 235
js_dist_pro_dropbhop 240
js_dist_leet_dropbhop 245
```

指令

```
Client commands:
!stats - displays your jumpstats (menu)
!jumptop - top menu (top 20 lj,wj,bhop,multibhop,dropbhop) (menu)
!speed/!showkeys - displays speed, keys and last jump distance (center panel)
!ljblock - registers a lj block
!sync - on/off strafe sync in chat
!sound - on/off quake sounds
!colorchat - on/off jumpstats messages of others in chat

Admin commands (z flag):
!resetjumpstats,
!resetallljrecords, !resetallljblockrecords, !resetallbhoprecords, resetallwjrecords, !resetallmultibhoprecords, resetalldropbhoprecords
!resetplayerjumpstats (for given steamid)
!resetljrecord, !resetwjrecord, !resetbhoprecord, !resetdropbhoprecord, !resetmultibhoprecord (for given steamid)
```



## amuJS

[Link](https://forums.alliedmods.net/showthread.php?p=2665776) 

`database.cfg`

```
"amuJS"
    {
        "driver"              "sqlite"
        "host"                "localhost"
        "database"            "kzjumpstats-sqlite"
        "user"                "root"
        "pass"                ""
    }
    "amuJSb"
    {
        "driver"              "sqlite"
        "host"                "localhost"
        "database"            "bkzjumpstats-sqlite"
        "user"                "root"
        "pass"                ""
    }
```

关闭`DistBug` 

`sm_distbug` 

# Server Config

```
sv_staminalandcost 0
sv_maxspeed 320
sv_staminajumpcost 0
sv_gravity 800
sv_airaccelerate 100
sv_friction 4.5
sv_accelerate 6.0
sv_maxvelocity 2000
sm_cvar sv_enablebunnyhopping 0
```







---

References

https://forums.alliedmods.net/showthread.php?t=239132

https://github.com/ceLoFaN/hidenseek-csgo

https://forums.alliedmods.net/showthread.php?p=2665776

https://github.com/amuDev/amuJS