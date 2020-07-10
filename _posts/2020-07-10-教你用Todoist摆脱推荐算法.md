---
layout:     post
title:      教你用Todoist摆脱推荐算法
subtitle:    
date:       2020-07-10
author:     郭翼天
header-img: img/封面.png
catalog: true
tags:
    - bilibili
    - sql
---

## 前按
>近来发现本人拿B站娱乐的时间已经远远大于学东西的时间，同时b站视频下的相关推荐总是能精准的命中我感兴趣的点，在不知觉之间已经沿着视频推荐链走了很远。为解决现状，找到一篇文章：\
>https://sspai.com/post/61022\
>尝试对其进行复现。在复现中，也能发现关注列表中的很多up只是为了看他的某一支视频，着实没有关注的必要。
在拉去fetcher表的时候，也精简了一半的关注。现在唯一需要解决的，若这条工作流长久的这么工作下去，我的硬盘能否吃得下？


## 流程汇总
1. **事件的触发**\
使用webhook服务，如果up主更新视频，则触发trigger

2. **任务的建立**\
使用todoist的原因在于ifttt提供todoist的服务

3. **获取事件**\
使用rsshub对up主的视频进行爬取

4. **数据存储**\
存储爬取到的视频链接以便于检索视频

5. **同步**\
利用win自带的任务计划程序


## Step 1：触发

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglxloqni9j307905qwec.jpg)


webhook可以理解为一个反向的api。类似于Siri，webhook处于一个时刻监听的状态，当满足特定条件时，webhook会发送一个url。这里我们直接使用ifttt的webhook接口。

## Step 2：建立任务
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglxlp306jj30ip06ljr7.jpg)

todoist是一个你的需求都能在这满足的软件，有着出色的UI和体贴的功能。上手也不难。同时与ifttt的兼容性极好。通过设置参数可以与Email，ios reminder等进行关联，提升工作效率。

## Step 3：工作流建立
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglxlpwaprj30a702b07g.jpg)

IFTTT（if this then that），是一个服务类网站，无需翻墙。通过将两种服务进行条件连接，来实现用户的需求。其中提供的服务种类多，适配性良好，被广大网友喜爱。同时也建立了很多骚操作，如“if my girlfriend text me 'go home late tonight' than create a group on facebook named 'beers!' meanwhile inviting my buddies”


## Step4：存储
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglxlphkjqj308p07d3yk.jpg)

利用db，我使用的是mysql提供的服务，同时使用navicat进行图形化管理。使用sqlalchemy包在python上使用mysql。


## Step5：同步
原文中使用的是vps服务，但因为vps服务为macos平台的，在这里使用win的任务计划程序可以达到相同的目的。设置为每15分钟同步一次之后，就可以等待任务上门了。

<center>fetcher表 ↓</center>

![fetcher表](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglxlq9smcj30rd0653yn.jpg)



<center>bilivideo表 ↓</center>

![bilivideo表](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglxlqsl2sj30nk05fmxa.jpg)

## 总结
本次实现最大的困难在于数据库整体框架的建立。从mysql的下载开始，到了解sqlalchemy的语法，读懂原作者程序，进行windows化的改造。真正用到的知识倒是不难，难的在于知识点的广阔繁杂。这种连点成线的能力有助于加深知识的应用记忆。最后，附上几张成果图。
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglyjid26yj31400u0go9.jpg)
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gglyjgycztj31400u0wip.jpg)