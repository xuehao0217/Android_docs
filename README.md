# Android_docs
Android性能优化文章

# 1：App启动速度优化
Android性能优化（一）之启动加速35%

http://www.jianshu.com/p/f5514b1a826c

Android冷启动白屏解析，带你一步步分析和解决问题

http://blog.csdn.net/guolin_blog/article/details/51019856

Android APP启动优化

http://wuxiaolong.me/2017/03/13/appStart/

App启动速度优化之耗时检测处理

http://www.jianshu.com/p/a0e242d57360



上面几篇文章基本上描述了应用的启动流程，如何优化白屏，以及一些SDK的懒加载等等...



美团Android DEX自动拆包及动态加载简介

https://tech.meituan.com/mt-android-auto-split-dex.html

Android MultiDex初次启动APP优化

http://blog.csdn.net/synaric/article/details/53540760

其实你不知道MultiDex到底有多坑

http://t.cn/RjjhD95



这3篇可以帮助你对multidex做一定的了解，以及提供了优化方案供参考。



当然了，在检测启动优化上，除了利用adb命令去检测总时间，还有就是去发现耗时的方法，可以利用TraceView，或者打开StrictMode，如果你喜欢使用Log，还可以去使用hugo，或者自己写一个类似的AOP日志框架。



关于TraceView的使用可以参考：



TraceView 简介及其案例实战

https://www.cnblogs.com/sunzn/p/3192231.html

使用 TraceView 找到卡顿的元凶

http://blog.csdn.net/u011240877/article/details/54347396

Android App优化之提升你的App启动速度之实例挑战

http://www.jianshu.com/p/4f10c9a10ac9



StrictMode比较简单，就不描述了，hugo是Jake大神的一个开源库，主要是利用aspectJ，源码很少，也比较简单，不过使用起来还不错，直接看readme就够了，感兴趣可以看下~



https://github.com/JakeWharton/hugo
# 2：UI流畅度优化
谈到UI流畅度，一般就是不要在主进程去做耗时的操作，提升UI的绘制速度（减少View的布局层级，避免过渡绘制等）...TraceView、Lint、Hugo、StrictMode等...



这里很容易想起Google在15年初google发布了Android性能优化典范，还好视频还被我找到了，文末有下载...



对于优化方案可参考：



Android性能优化（二）之布局优化面面观

http://www.jianshu.com/p/4f44a178c547

Android UI性能优化实战 识别绘制中的性能问题

http://blog.csdn.net/lmj623565791/article/details/45556391/

性能优化之布局优化

http://www.trinea.cn/android/layout-performance/

Android性能调优

http://www.trinea.cn/android/android-performance-demo/



当然了对于UI卡顿，不可避免的要引入检测的方案：



一般有监听Looper的日志

利用Choreographer



可参考我之前编写的：



Android UI性能优化 检测应用中的UI卡顿



当然也相应的有一些开源工具：



https://github.com/markzhai/AndroidPerformanceMonitor [方式1]

https://github.com/wasabeef/Takt [方式2]

https://github.com/friendlyrobotnyc/TinyDancer [方式2]

# 3：内存优化
内存优化那么主要就是去消除应用中的内存泄露、避免内存抖动；常用工具就是AS自带的内存检测，可以很好的发现内存抖动；leakcanary可以非常方便的帮助我们发现内存泄露；MAT可以做更多的内存分析。



当然了，你还可以了解一些内存相关的基础知识。



Android性能优化（三）之内存管理

http://www.jianshu.com/p/c4b283848970

Android性能优化第（二）篇---Memory Monitor检测内存泄露

http://www.jianshu.com/p/ef9081050f5c

内存泄露实例分析 -- Android内存优化第四弹

http://www.jianshu.com/p/cbe2ee08ca02

Android最佳性能实践(一)——合理管理内存

http://blog.csdn.net/guolin_blog/article/details/42238627

Android最佳性能实践(二)——分析内存的使用情况

http://blog.csdn.net/guolin_blog/article/details/42238633

Android性能优化-内存泄漏的8个Case

Android 内存优化总结&实践

https://mp.weixin.qq.com/s/2MsEAR9pQfMr1Sfs7cPdWQ

Android内存优化之OOM

http://hukai.me/android-performance-oom/

Android应用内存泄露分析、改善经验总结

https://zhuanlan.zhihu.com/p/20831913

内存泄露从入门到精通三部曲之基础知识篇

http://dev.qq.com/topic/59152c9029d8be2a14b64dae

内存泄露从入门到精通三部曲之排查方法篇

http://dev.qq.com/topic/591522d9142eee2b6b9735a2

手把手教你在Android Studio 3.0上分析内存泄漏

# 4：apk瘦身
关于Apk瘦身，主要由以下几个方式：



利用ProGuard压缩代码去除无用资源

andresguard进一步压缩与混淆资源

第三方开源库的瘦身，仅保留自己需要的部分

极致的图片压缩与webp的使用

合理配置去除不必要的配置，仅保留中文配置等...

so的优化与配置，只保留一类so

动态下发一些资源:字库、so、换肤包等；



以上仅有7比较麻烦，需要服务端的配合，此外对于动态下发So，可以参考tinker对So热修复部分代码。



其余都是常规方式，且1 ，5，6都比较简单，build.gradle最下配置即可，当然了也有一些参考文章：



App瘦身最佳实践

http://www.jianshu.com/p/8f14679809b3#

Android APP终极瘦身指南

http://t.cn/RGjNpam

Android性能优化（十）之App瘦身攻略

http://www.jianshu.com/p/99f3c09982d4

[Android技术专题]APK瘦身看这一篇文章就够了

http://www.jianshu.com/p/6be4f98162d7

安装包立减1M--微信Android资源混淆打包工具

http://t.cn/RjjVe4f

爱奇艺Android移动客户端app瘦身经验

http://t.cn/RjjfzrY

Android Webp 完全解析 快来缩小apk的大小吧

App优化攻略-用TextView显示图片

Android IconFont全攻略
# 5：电量优化
电量优化说实在的关注度较低，一般情况就是合理的使用一些传感器、谨慎的使用Wake Lock、减少后台的不要的操作等...检测可以利用battery-historian 



Android性能优化（九）之不可忽视的电量

http://www.jianshu.com/p/5d83d8649c98

Android性能优化之电量篇

http://hukai.me/android-performance-battery/

Android性能优化-电量优化

Android性能优化系列之电量优化

http://blog.csdn.net/u012124438/article/details/74617649

Android App优化之电池省着用

http://www.jianshu.com/p/c55ef05c0047

https://github.com/google/battery-historian




最后，好文非常多，本文希望仅起到抛砖引入的效果，感谢所有作者~



这里提供一下该ppt的下载以及Google的性能优化典范视频，链接：https://pan.baidu.com/s/1kVHyCUb，懒得复制的可以公众号内回复1118即可。



对了，腾讯有个非常强大的手机上的“集成调测环境”，就是手机上的软件，可以用于性能检测，叫GT。

http://gt.tencent.com/download.html



当然本文全部内容也已经同步到了wanandroid，有需要可以关键词搜索。


