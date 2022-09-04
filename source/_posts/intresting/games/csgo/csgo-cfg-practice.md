---
title: CSGO Practice cfg
categories:
- Game
tags:
- csgo
---

# Intro

投掷训练cfg配置

# cfg

```
ammo_grenade_limit_total 6    //可携带的手雷数
mp_afterroundmoney 32000    //每回合结束后增加的金额
mp_autoteambalance 0    //关闭自动进行人数平衡
mp_buytime 3600    //购买时间
mp_buy_anywhere 1    //允许在任何地方购买
mp_death_drop_defuser 1    //玩家死后不掉落拆弹器
mp_death_drop_grenade 1 //玩家死后不掉落手雷
mp_death_drop_gun 1    //玩家死后不掉落枪支
mp_forcecamera 0    //不限制观察者所观看的队伍
mp_free_armor 2    //免费给予防弹衣和头盔 1=给予防弹衣 2=给予防弹衣和头盔
mp_freezetime 0    //冻结时间
mp_friendlyfire 1    //开启右伤
mp_ignore_round_win_conditions 1    //忽略胜利条件
mp_limitteams 0    //不限制队伍
mp_maxmoney 32000    //最大金额
mp_respawn_on_death_ct 1    //反恐精英死后即刻复活
mp_respawn_on_death_t 1    //恐怖分子死后即刻复活
mp_roundtime 60.00    //每回合时间
mp_roundtime_hostage 60.00    //解救人质地图每回合时间
mp_roundtime_defuse 60.00    //拆除炸弹地图每回合时间
mp_startmoney 32000    //初始金额
mp_teammates_are_enemies 1    //任何人都为目标
mp_warmuptime 0    //热身时间为0秒
sv_alltalk 1 //开启全局语言
//sv_enablebunnyhopping 1 //允许连跳
//sv_autobunnyhopping 1 //开启自动连跳
sv_grenade_trajectory 1    //显示手雷的抛物线
sv_grenade_trajectory_dash 0    //手雷抛物线的形状
sv_grenade_trajectory_thickness 1    //手雷抛物线的厚度
sv_grenade_trajectory_time 20    //手雷抛物线的显示时间
sv_infinite_ammo 2    //无限备用弹夹
sv_showimpacts 1    //显示弹道,红色为客户端,蓝色为服务器
sv_showimpacts_time 15    //弹道的显示时间

mp_restartgame 1    //重新开始游戏

bot_kick    //踢出BOT
bot_stop 1    //BOT为静止状态
```

服务器在开启道具轨迹的时候有问题, 用户看不见轨迹.

完美平台使用投掷道具插件来解决.

自建服务器可以通过`cl_grenadepreview 1` 来弥补, 在按住左键可以显示落点.

