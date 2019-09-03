---
title: AsyncTask doInBackground 不执行
tags:
- Android
- AsyncTask
categories: Android
description: AsyncTask doInBackground 不执行
---

前提：
本来在需求的时候，突然测试提了一个bug
相册页面的预览图不展示了，但是我好几个版本没有修改了，why
谁改我的代码了，
然后去查没人改啊，
后来定位到asyncTask 的doInBackground 不执行，

why ？

后来发现用了 AsyncTask.excute()
这个用的是单线程的线程池，并且是多个AsyncTask 公用的，
才能保持动作的顺序执行。

我的问题：
前面有人用AsyncTask做了耗时操作，到相册页面还没有执行完，然后我的task 就要等待
然后就不行了

解决问题：
private ExecutorService cropExecutor = Executors.newSingleThreadExecutor();
asyncTask.executeOnExecutor(cropExecutor);
不用公用的那个AsyncTask的线程池，自己建一个。



参考文章：
https://www.cnblogs.com/kobe8/p/3781340.html
https://www.jianshu.com/p/78b42b3f0cb4
