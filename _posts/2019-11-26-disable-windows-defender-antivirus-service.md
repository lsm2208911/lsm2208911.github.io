---
layout:     post
title:      "关闭Windows Defender Antivirus Service"
subtitle:   "让你的电脑起飞"
date:       2019-11-26
author:     "无力去闹"
header-img: "img/post-bg-js-version.jpg"
tags:
    - MYSQL
---
1. 如果是专业版，Windows+R打开运行，输入“gpedit.msc”回车，打开策略组，在策略组定位到"计算机配置 >管理模板 >Windows组件 >Windows  Defender",
查看“关闭Windwos defender”的配置，双击在属性中改为启用。

2. Windows+R打开运行，输入“gpedit.msc”回车，打开注册表，在注册表定位到HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender，在右侧将DisableAntiSpyware项的数值改为1。

注意：在更改注册表前对注册表进行备份。

参考：[怎样禁用Windows Defender Antivirus Service](https://answers.microsoft.com/zh-hans/protect/forum/protect_defender-protect_start-windows_10/%E6%80%8E%E6%A0%B7%E7%A6%81%E7%94%A8windows/1767fde3-ce37-4e60-8afd-1e319347dc1a)