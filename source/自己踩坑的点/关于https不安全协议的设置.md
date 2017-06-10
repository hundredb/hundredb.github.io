title: 关于https不安全协议的设置
date: 2017-5-32 10:00:00
categories: 
- 踩坑
tags: 
- 踩坑

---

关于weak的不小心使用


# 前言

由于没有设置安全协议,导致没法访问外网
```

2017-06-08 15:31:55.323024+0800 QHZC[826:135213] [INFO] -[QHBaseViewController apiRequestFailed:error:](524) requestKey:8 error:Error Domain=NSURLErrorDomain Code=-1022 "The resource could not be loaded because the App Transport Security policy requires the use of a secure connection." UserInfo={NSUnderlyingError=0x17425c6b0 {Error Domain=kCFErrorDomainCFNetwork Code=-1022 "(null)"}, NSErrorFailingURLStringKey=http://test.wealth.jushenghua.com:8080/los/wss-intf-portal.updateSession?, NSErrorFailingURLKey=http://test.wealth.jushenghua.com:8080/los/wss-intf-portal.updateSession?, NSLocalizedDescription=The resource could not be loaded because the App Transport Security policy requires the use of a secure connection.}
```

# 正文

问题查找的过程
1. 由于逐步寻找断点,一直卡在网络请求,但是由于偶然一个原因,点击了一下按钮事件也是消失了
2. 所以估计是初始化或者全局化没有了,要不就是遮层,遮挡住了,所以这个问题以后要注意,由于粗心复制导致的

![使用weak例子](http://okbqg56m9.bkt.clouddn.com/3.gif)
![使用strong](http://okbqg56m9.bkt.clouddn.com/2.gif)

