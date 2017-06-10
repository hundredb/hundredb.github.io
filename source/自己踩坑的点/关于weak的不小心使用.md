title: 关于weak的不小心使用
date: 2017-5-32 10:00:00
categories: 
- 踩坑
tags: 
- 踩坑

---

关于weak的不小心使用


# 前言

由于在`ProductCustomInfoViewController`里面的vc使用了weak,导致了两个问题
1. 发送网络请求,没有收到回馈的信息
2. 点击事件没有反应

![](http://okbqg56m9.bkt.clouddn.com/Snip20170531_1.png)

# 正文

问题查找的过程
1. 由于逐步寻找断点,一直卡在网络请求,但是由于偶然一个原因,点击了一下按钮事件也是消失了
2. 所以估计是初始化或者全局化没有了,要不就是遮层,遮挡住了,所以这个问题以后要注意,由于粗心复制导致的

![使用weak例子](http://okbqg56m9.bkt.clouddn.com/3.gif)
![使用strong](http://okbqg56m9.bkt.clouddn.com/2.gif)

