---
layout: post
title: 渗透合集
date: 2020-10-29
tags: 渗透 工具
---

### 渗透流程
* [渗透流程参考文章](https://my.oschina.net/u/4588149/blog/4684434)


### 前期信息探测

1. 确认是否真实 ip：
[国外多地访问](https://asm.saas.broadcom.com/en/ping.php)

2. 绕过查真实ip(还没用过，待测)：
* [fuckcdn](https://github.com/Tai7sy/fuckcdn)
* 翻历史解析记录

3. CMS 探测：
[CMSScan](https://github.com/ajinabraham/CMSScan)

4. 目录扫描：
* [dirmap](https://github.com/H4ckForJob/dirmap)
* dirbuster

5. Nikto

6. Xray


### 中期

1. sql 注入
sqlmap

2. xss
* [XSStrike](https://github.com/s0md3v/XSStrike)
* [xss绕过](https://www.freebuf.com/articles/web/195507.html)

3. csrf

4. 字典：
* [cupp](https://github.com/Mebus/cupp.git)
* [SecLists](https://github.com/danielmiessler/SecLists)
* [fuzzDicts](https://github.com/TheKingOfDuck/fuzzDicts)


### 应急

1. [应急手册](https://bypass007.github.io/Emergency-Response-Notes/)


### CTF
1. [笔记](https://github.com/w181496/Web-CTF-Cheatsheet)


### 其他

1. 代理池：
* [IPProxyPool](https://github.com/qiyeboy/IPProxyPool)
* [Proxy_Pool](https://github.com/TideSec/Proxy_Pool)

3. 集合
[SecToolSet](https://github.com/bollwarm/SecToolSet)

4. 网络设备默认密码：
```
天融信防火墙，不需要证书 登录地址:https://192.168.1.254 用户名:superman 密码:talent 技术支持热线：8008105119
天融信防火墙，不需要证书 登录地址:https://192.168.1.254：8080 用户名:superman 密码:talent！23 遇到设备需要把旧设备配置备份下来，再倒入新设备基于console口登陆，用户名，密码跟web界面一致 system config reset 清除配置 save 保存 联想网御防火墙，需要证书（最好用IE浏览器登录）
登录地址:https://10.1.5.254:8889 用户名:admin 密码:leadsec@7766、administrator、bane@7766 技术支持热线：4008107766 010-56632666
深信服防火墙（注安全设备管理地址不是唯一的） https://10.251.251.251
https://10.254.254.254 用户名：admin 密码：admin 技术支持热线：4006306430
启明星辰 https://10.1.5.254:8889 用户名：admin 密码：bane@7766
https://10.50.10.45:8889 用户名：admin 密码：admin@123 电脑端IP：10.50.10.44/255.255.255.0 技术支持热线：4006243900
juniper 登录地址:https://192.168.1.1 用户名:netscreen 密码:netscreen
Cisco 登录地址:https://192.168.0.1 用户名:admin 密码:cisco
Huawei 登录地址:http://192.168.0.1 用户名:admin 密码:Admin@123
H3C 登录地址:http://192.168.0.1 用户名:admin 密码:admin 技术支持热线：4006306430
绿盟IPS https://192.168.1.101 用户名: weboper 密码: weboper 配置重启生效
网神防火墙GE1口 https://10.50.10.45 用户名：admin 密码：firewall 技术支持热线：4006108220
深信服VPN： 51111端口 delanrecover
华为VPN：账号：root 密码：mduadmin
华为防火墙： admin Admin@123 eudemon
eudemon Juniper防火墙： netscreen netscreen
迪普 192.168.0.1 默认的用户名和密码（admin/admin_default)
山石 192.168.1.1 默认的管理账号为hillstone，密码为hillstone
安恒的明御防火墙 admin/adminadmin
某堡垒机 shterm/shterm
天融信的vpn test/123456
```