---
title: CSGO 服务器配置文件
categories:
- Game
tags:
- csgo
---

# Intro

服务器配置文件

<!--more-->

# 加载顺序

重启服务器或更换地图即可刷新**插件**及**配置文件**.

`autoexec.cfg` 会在游戏启动时自动加载

`server.cfg` 服务器的默认配置

# 手动加载

可以加载任意cfg

```
rcon exec xxxx.cfg
```

# 配置解释

```
// CSGO服务器登录令牌
sv_setsteamaccount "71A7171EDA96CEXXX060722ECA822EDA"

// 系统参数
hostname "Edlison Server"                                                 // 服务器名称将显示在服务器浏览器中。
rcon_password "123456"                                  // CS:GO远程控制台密码，修改为自己定义的密码
sv_password ""                                          // 服务器连接密码，在连接服务器时输入，不要密码可以留空

sv_lan "0"                                 // 应始终设置此选项，以便您知道它未打开
sv_region "255"                            // 服务器所在区域注册参数,255=全球,0=美国东部,1=美国西部,2=南美洲,3=欧洲,4=亚洲,5=澳洲,6=中东,7=非洲
sv_tags "aim and fire"                          // Server标签。用于在客户端浏览服务器时向其提供额外信息

// 服务器参数
mp_friendlyfire "0"                         // 队友伤害 1=启用,0=禁用
//ff_damage_reduction_grenade "0"           // 减少手榴弹对队友造成的伤害。
//ff_damage_reduction_bullets "0"           // 减少射击时对队友造成的伤害。
//ff_damage_reduction_other "0"             // 减少非子弹/手榴弹对队友造成的伤害
mp_autoteambalance "1"                      // 自动平衡团队
mp_autokick "0"                             // 踢挂机或故意击杀队友的玩家。
mp_tkpunish "0"                             // 启用故意击杀队友惩罚。
sv_alltalk "1"                              // 玩家可以听到所有其他玩家的语音通信，不受团队限制
sv_deadtalk "0"                             // 死亡玩家可以对活着的玩家说话（语音、文本）。
sv_full_alltalk "1"                         // 任何玩家（包括观战玩家）都可以与任何其他玩家通话
sv_pausable "0"                             // 将服务器设置为可暂停。如果设为1，任何人都可以暂停。
mp_limitteams "2"                           // 最大数量团队可能失衡。0已关闭。
sv_voiceenable "1"                          // 已启用并禁用语音聊天。默认值：1，启用。
sv_allow_lobby_connect_only "0"             // 如果设置为1，则只允许配对游戏，不允许直接连接。
sv_allow_wait_command "1"                   // 是否允许连接到此服务器的客户端上的等待命令
sv_cheats "0"                               // 允许服务器使用外挂
sv_alternateticks "0"                       // 如果设置为1，则服务器仅模拟偶数记号上的实体。
sv_downloadurl"http://121.22.5.222:8081/csgo"       // 客户端可以下载丢失文件的网站
sv_forcepreload "0"                         // 强制服务器端预加载。
sv_friction "4"                             // 世界摩擦。默认值4
sv_pure "0"                                 // 0关闭，1使用白名单，2强制默认。
sv_consistency "0"                          // 0关闭并允许外观，1打开并强制默认值。
//sv_pure_kick_clients "1"                  // 如果设置为1，服务器将使用不匹配的文件来踢客户端。
//sv_pure_trace "0"                         // 如果设置为1，则每当客户端验证文件的CRC时，服务器都会打印一条消息。


// 游戏参数
mp_freezetime "6"                           // 回合开始时，让玩家保持静止的时间是多少秒
mp_afterroundmoney "0"                      // 每轮后向每位玩家支付的金额
mp_playercashawards "1"                     // 玩家可以通过执行游戏中的动作来赚钱
mp_teamcashawards "1"                       // 团队可以通过执行游戏中的动作来赚钱
mp_maxrounds "30"                           // 每张地图的最大回合数
mp_timelimit "0"                            // 整个地图需要多少分钟
mp_roundtime "2"                            // 每轮需要多少分钟。
mp_freezetime"5"                            // 当回合开始时，需要多少秒让玩家保持静止
mp_buytime "45"                             // 回合开始后玩家可以购买物品的秒数。
mp_forcecamera "1"                          // 设置为1，仅供团队观看。
mp_defuser_allocation "2"                   // 如何在开始或结束时将defuser分配给CT：0=无，1=随机，2=所有人
mp_death_drop_defuser "1"                   // 玩家死亡时丢弃装备
mp_death_drop_grenade "2"                   // 玩家死亡时丢弃哪个手榴弹：0=无，1=最佳，2=当前或最佳
mp_death_drop_gun "1"                       // 玩家死亡时丢弃哪支枪：0=无，1=最佳，2=当前或最佳
mp_buytime "45"                             // 回合开始后玩家可以购买物品的秒数。
mp_c4timer "45"                             // 从C4待命到爆炸有多长时间
mp_do_warmup_period "1"                     // 是否在比赛开始时进行热身。
mp_force_pick_time "15"                     // 玩家在自动组队之前在组队屏幕上进行选择的时间量
mp_halftime_duration "15"                   // 中场休息持续的秒数
mp_join_grace_time "15                      // 回合开始后允许玩家加入游戏的秒数
mp_match_end_restart "1"                    // 在比赛结束时，执行重新启动，而不是加载新地图
mp_maxrounds "30"                           // 每张地图的最大回合数
mp_playercashawards "1"                     // 玩家可以通过执行游戏中的动作来赚钱
mp_playerid "0"                             // 控制玩家在状态栏中看到的信息：0所有名称；1玩家名称；2没有名称
mp_playerid_delay "0"                       // 状态栏中显示信息的延迟秒数
mp_playerid_hold "0"                        // 秒数以保持在状态栏中显示旧信息
mp_restartgame "0"                          // 如果非零，游戏将在指定的秒数内重新启动
mp_round_restart_delay "7"                  // 获胜后重新开始回合前的延迟秒数
mp_roundtime "3"                            // 每轮需要多少分钟。
mp_warmuptime "25"                          // 如果为真，则在每场比赛开始时会有一个热身期/回合，以便连接。
mp_win_panel_display_time "5"               // 显示比赛/半场之间win panel的时间量


// 电脑玩家参数
bot_difficulty 1                           // 定义机器人加入游戏的技能。值为：0=简单，1=正常，2=困难，3=专家。
bot_chatter "off"                          // 控制机器人说话的方式。允许值：“off”、“radio”、“minimal”或“normal”
bot_join_after_player 1                    // 如果非零，则bot将等待玩家加入后再进入游戏。
bot_quota 10                               // 决定游戏中的机器人总数。
bot_quota_mode "fill"                      // 确定配额的类型。允许值：“normal”、“fill”和“match”


// 日志参数

//log on                                    // 是否开启日志记录
sv_log_onefile "0"                          // 只将服务器信息记录到一个文件中。
sv_logbans "0"                              // Log服务器日志中的服务器禁止。
sv_logecho "1"                              // 将日志信息回显到控制台。
sv_logfile "1"                              // Log日志文件中的服务器信息。
sv_logflush "0"                             // 每次写入时将日志文件刷新到磁盘（慢）。
sv_logsdir "0"                              // game目录中存储服务器日志的文件夹。


// 服务器网络参数
sv_maxcmdrate "200"                         // 服务器cmd最大带宽使用量
sv_maxrate "128000"                         // 服务器最大带宽使用量，默认值非常小，因此会造成choke值异常，此处建议改为128000
sv_mincmdrate "10"                          // 服务器cmd最小带宽使用量
sv_minrate "80000"                          // 服务器最小带宽使用量，与上面同理，此处建议改为80000


// 人物跳跃移动参数
sv_accelerate "5.5"                         // 人物移动速度，默认值为10，快到恶心，此处建议修改为5.5
sv_friction "4"                             // 世界摩擦。默认值4
sv_staminajumpcost ".1"                     // 跳跃的体魄惩罚。默认值.1
sv_staminalandcost ".1"                     // 着陆的耐力惩罚。默认值.1
sv_staminamax "80"                          // 最大体魄惩罚。默认值80
sv_staminarecoveryrate "50"                 // 体力恢复的速率（单位/秒）。默认值50

// 金钱参数
mp_startmoney "400"                         // 每位玩家重置时获得的金钱数量。
mp_maxmoney "16000"                         // 玩家账户中允许的最大金钱数量。                                
cash_team_terrorist_win_bomb "2200"         // 爆破模式获胜获得金钱数量。
cash_team_elimination_hostage_map "2200"    // 玩家消灭所有人质时的收入。
cash_team_elimination_bomb_map "2200"       // 炸弹爆炸后团队将赢得多少金钱。
cash_team_win_by_time_running_out "2200"    // 时间结束时团队将赢得多少金钱。
cash_team_win_by_defusing_bomb "2200"       // 拆除炸弹后团队将赢得多少金钱。
cash_team_win_by_hostage_rescue "2200"      // 当所有人质获救后，团队将赢得多少金钱。
cash_team_loser_bonus "2000"                // 玩家失败时玩家将赢得多少金钱。
cash_team_loser_bonus_consecutive_rounds "500" // 当玩家连续失败时，玩家将赢得多少金钱。
cash_team_rescued_hostage "100"             // 当团队解救人质时，团队将赢得多少。
cash_team_hostage_alive        "0"                 // 当人质还活着时，团队将赢得多少金钱
cash_team_planted_bomb_but_defused "200"    // 当团队放置了炸弹并被拆除时，团队将赢得多少
cash_team_hostage_interaction "50"          // 当人质获救时，团队将赢得多少金钱
cash_player_killed_teammate "-3300"         // 当队友被杀时，玩家将损失多少
cash_player_killed_enemy_default "200"      // 玩家在杀死敌人时会赢多少钱
cash_player_killed_enemy_factor        "0.5"       // 玩家在杀敌时会赢多少钱
cash_player_bomb_planted "200"              // 放置炸弹后玩家将赢得多少。
cash_player_bomb_defused "200"              // 炸弹解除后玩家将赢得多少钱
cash_player_rescued_hostage "200"           // 解救人质时玩家会赢多少钱
cash_player_interact_with_hostage "0"       // 玩家在与人质互动时会赢多少钱
cash_player_damage_hostage "-30"            // 玩家在伤害人质时会损失多少
cash_player_killed_hostage "-1000"          // 当人质被杀时，玩家将释放多少钱


// 投票参数
sv_allow_votes "1"                          // 打开和关闭服务器投票。
sv_vote_allow_spectators "0"                // 允许观众投票
sv_vote_command_delay "2"                   // 票通过后多长时间，直到动作发生
sv_vote_creation_time "120"                 // 某人可以单独进行投票的频率。
sv_vote_failure_timer "300"                 // 失败的投票在这么长时间内不能重新提交
sv_vote_quorum_ratio "0"                    // 为解决某个问题而需要投票的玩家的最小比率。
sv_vote_timer_duration "15"                 // 允许对一个问题进行投票的时间
```

# 附录

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220120015509.png)







----

References

https://xiongtianqi.cn/thread-304550-1-1.html

https://www.csgo.com.cn/news/gamenews/20170825/205831.shtml