---
title: CSGO Addons SourceMod
categories:
- Game
tags:
- csgo
---

# Intro

CSGO SourceMod插件设定

<!--more-->

# General

目录`csgo/addons`

# Config

## 添加管理

```sh
vim csgo/addons/sourcemod/configs/admins_simple.ini

auth:identity	flag
```

## 添加插件

直接复制到 `csgo/addons/sourcemod`

## 自定义Menu

```sh
vim csgo/addons/sourcemod/configs/adminmenu_custom.txt
```

```
"Commands"		// 列表跟目录
{
	"ServerCommands"		// 添加在二级目录ServerCommands下
	{
		"Load Workshop Map"		// 自定义的名字
		{
			"cmd"		"sm_wml"
			"admin"		"sm_changemap"
		}
		"Refresh Workshop Map List"
		{
			"cmd"		"sm_wml_reload"
			"admin"		"sm_changemap"
		}
		"Start Next Workshop Map Vote"
		{
			"cmd"		"sm_wml_vote_now"
			"admin"		"sm_changemap"
		}
	}
}
```

参考官方[wiki](http://wiki.alliedmods.net/Custom_Admin_Menu_%28SourceMod%29) 

## 地图

地图目录 `csgo/maps`

创意工坊 `csgo/maps/workshop/collection_id`

```
// 切换地图指令
rcon map workshop/20xxxxxxxx/squid_game
rcon map de_dust2

rcon changelevel2 workshop/20xxxxxxxx/squid_game
rcon changelevel2 de_dust2
```

服务端和客户端的文件地址是完全一致的, 可以手动上传到服务器.

# 关闭插件

可以直接删除

或者将`addons/plugins/xxx.smx` 移动到 `addons/plugins/disabled/xxx.smx` 

# Manage SourceMod

[link](https://wiki.alliedmods.net/Managing_your_Sourcemod_installation/zh) 

```
sm
sm version
sm plugins
sm plugins list
sm plugins reload 1
sm plugins refresh
sm plugins unload funvotes
sm plugins load funvotes
sm exts list
```

- /configs 这是sourcemod和插件默认放置配置文件的地方。

- /plugins 所有插件（.smx文件）都会在sourcemod启动时自动加载。当地图更改时如果文件发生了改变，也会重新加载。

- /plugins/disabled 在这个子文件夹中的插件不会被加载。如果你想要禁用一个插件，就把它从父文件夹中剪切进去。反之亦然。你会发现这个文件夹中有一些你可能想安装的官方插件
- /scripting 你能看到一些插件的源码。安装插件并不需要放置任何文件在这里，但是我们强烈推荐不要仅仅安装smx文件，最好也带上相应的sp文件。

# Admin Command

[link](https://wiki.alliedmods.net/Admin_Commands_(SourceMod)/zh) 

## 基础命令

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220120025315.png)

## 扩展命令

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220120025153.png)

## 投票命令

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220120025419.png)

# War Mod

[link](https://wiki.alliedmods.net/War_Mode_(SourceMod)/zh) 

**模版文件**

`sm_warmode_on.cfg`:

```
// 本文件会卸载全部插件
// 重新加载“安全”的部分
// 然后再禁止其他插件的加载
sm plugins unload_all
sm plugins load basebans.smx
sm plugins load basecommands.smx
sm plugins load admin-flatfile.smx
sm plugins load adminhelp.smx
sm plugins load adminmenu.smx
sm plugins load_lock
```

`sm_warmode_off.cfg`:

```
// 本文件回解除插件的锁定
// 并刷新加载所有的插件
sm plugins load_unlock
sm plugins refresh
```

# Manage Map

[link](https://wiki.alliedmods.net/Managing_your_Sourcemod_installation/zh) 







---

References

https://dpii.club/archives/287

