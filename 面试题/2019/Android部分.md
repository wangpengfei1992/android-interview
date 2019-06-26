四大组件是哪四个？ABCS(Activity,Braodcast,ContentProvider,Service)

2.1 Activity
1.Activity是什么？

2.典型情况下的Activity生命周期？

3.异常情况下的Activity的生命周期 & 数据如何保存和恢复？

4.从Activity A跳转到Activity B之后，然后再点击back建之后，它们的生命周期调用流程是什么？

5.如何统计Activity的工作时间？

6.给我说说Activity的启动模式 & 使用场景。

7.如何在任意位置关掉应用所有Activity & 如何在任意位置关掉指定的Activity？

8.Activity的启动流程(从源码角度解析)？

9.启动一个其它应用的Activity的生命周期分析。

10.Activity任务栈是什么？在项目中有用到它吗？说给我听听

11.什么情况下Activity不走onDestory?

12.什么情况下Activity会单独执行onPause?

13.a->b->c界面，其中b是SingleInstance的，那么c界面点back返回a界面，为什么？

14.如果一个Activity弹出一个Dialog,那么这个Acitvity会回调哪些生命周期函数呢？

15.Activity之间如何通信 & Activity和Fragment之间通信 & Activity和Service之间通信？

16.说说Activity横竖屏切换的生命周期。

17.前台切换到后台，然后在回到前台时Activity的生命周期。

18.下拉状态栏时Activity的生命周期？

19.Activity与Fragment的生命周期比较？

20.了解哪些Activity常用的标记位Flags？

21.谈谈隐式启动和显示启动Activity的方式？

22.Activity用Intent传递数据和Bundle传递数据的区别？为什么不用HashMap呢？

23.在隐式启动中Intent可以设置多个action,多个category吗 & 顺便讲讲它们的匹配规则？

24.Activity可以设置为对话框的形式吗？

25.如何给Activity设置进入和退出的动画？

26.Activity使用Intent传递数据是否有限制 & 如果传递一个复杂的对象，例如一个复杂的控件对象应该怎么做？

2.2 BroadcastReceiver
1.广播是什么？

2.广播的注册方式有哪些？

3.广播的分类 & 特性 & 使用场景？

4.说说系统广播和本地广播的原理 & 区别 & 使用场景。

5.有两个应用注册了一样的广播，一个是静态，一个是动态，连优先级也一样，那么当广播从系统发出来后，哪个应用先接收到广播？

2.3 ContentProvider
1.什么是内容提供者？

2.说说如何创建自己应用的内容提供者 & 使用场景。

3.说说ContentProvider的原理。

4.ContentProvider,ContentResolver,ContentObserver之间的关系？

5.说说ContentProvider的权限管理。

2.4 Service
1.什么是Service?

2.说说Service的生命周期。

3.Service和Thread的区别？

4.Android 5.0以上的隐式启动问题及其解决方案。

5.给我说说Service保活方案

6.IntentService是什么 & 原理 & 使用场景 & 和Service的区别。

7.创建一个独立进程的Service应该怎样做？

8.Service和Activity之间如何通信？

9.说说你了解的系统Service。

10.谈谈你对ActivityManagerService的理解。

11.在Activtiy中创建一个Thread和在一个Service中创建一个Thread的区别？

2.5 Handler
1.子线程一定不能更新UI吗？

2.给我说说Handler的原理

3.Handler导致的内存泄露你是如何解决的？

4.如何使用Handler让子线程和子线程通信？

5.你能给我说说Handler的设计原理？

6.HandlerThread是什么 & 原理 & 使用场景？

7.IdleHandler是什么？

8.一个线程能否创建多个Handler,Handler和Looper之间的对应关系？

9.为什么Android系统不建议子线程访问UI？

10.Looper死循环为什么不会导致应用卡死？

11.使用Handler的postDealy后消息队列有什么变化？

12.可以在子线程直接new一个Handler出来吗？

13.Message对象创建的方式有哪些 & 区别？

2.6 AsyncTask
1.AsyncTask是什么？能解决什么问题

2.给我谈谈AsyncTask的三个泛型参数作用 & 它的一些方法作用。

3.给我说说AsyncTask的原理。

4.你觉得AsyncTask有不足之处吗？

2.7 Fragment
1.Android中v4包下Fragment和app包下Fragment的区别是什么？

2.Fragment的生命周期 & 请结合Activity的生命周期再一起说说。

3.说说Fragment如何进行懒加载。

4.ViewPager + Fragment结合使用会出现内存泄漏吗 & 如何解决？

5.Fragment如何和Activity进行通信 & Fragment之间如何进行通信？

6.给我谈谈Fragment3种切换的方式以及区别 & 使用场景。

7.getFragmentManager,getSupportFragmentManager,getChildFragmentManager之间的区别？

8.FragmentPagerAdapter和FragmentStatePagerAdapter区别？

9.Fragment如何实现类似Activity栈的压栈和出栈效果的？

2.8 序列化
1.什么是序列化 & 能用来干什么？

2.Android中序列化方式有几种？说说它们的区别。

3.如果想要序列化的类中某些字段不序列化，那么应该怎么做？

2.9 IPC
1.说说你对Android多进程开发的认识？

2.Android中进程间通信的方式有哪些？

3.什么是AIDL?如何创建一个AIDL。

2.10 文件存储
1.说说Android中数据持久化的方式 & 使用场景。

2.接触过MMKV吗？说说SharedPreference和它的区别。

3.第三方数据库框架用过哪些？有没有自己封装过一个SQLite的库？

4.SQLite是线程安全的吗 & SharedPreference是线程安全的吗？

5.请简单的给我说说什么是三级缓存？

6.SharedPreference的apply和commit的区别。

7.谈谈你对SQLite事务的认识。

8.千奇百怪的SQL语句考察。

9.SharePreference跨进程使用会怎么样？如何保证跨进程使用安全？

10.谈谈SQLite升级要注意哪些地方？

2.11 ListView & RecyclerView
1.ListView是什么？如何使用？

2.RecyclerView是什么？如何使用？如何返回不一样的Item。

3.ListView和RecycyclerView的区别是什么？

4.分别讲讲你对ListView & RecyclerView的优化经验。

5.给我说说RecyclerView的回收复用机制

6.说说你是如何给ListView & RecyclerView加上拉刷新 & 下拉加载更多机制。

7.谈谈你是如何对ListView & RecycleView进行局部刷新的？

8.谈谈如何进行分页加载？

9.ScrollView下嵌套一个ListView通常会出现什么问题？

10.一个ListView或者一个RecyclerView在显示新闻数据的时候，出现图片错位，可能的原因有哪些 & 如何解决？

2.12 图片编程
1.你对Bitmap了解吗？它在内存中如何存在？

2.有关Bitmap导致OOM的原因知道吗？如何优化？

3.给我谈谈图片压缩。

4.LruCache & DiskLruCache原理。

5.说说你平常会使用的一些第三方图片加载库,最好给我谈谈它的原理。

6.如果让你设计一个图片加载库，你会如何设计？

7.有一张非常大的图片,你如何去加载这张大图片？

8.你知道Android中处理图片的一些库吗(OpenCv & GPUImage ...)？

9.如何计算一张图片在内存中占用的大小？

2.13 WebView
1.WebView是什么？

2.WebView会导致内存泄露吗？原因是什么？解决方式有哪些？

3.你知道Hybrid开发吗？说说你的相关经验。

4.说说WebSettings & WebViewClient & WebChromeClient这三个类的作用 & 用法。

5.说说你了解的Hybrid框架。

2.14 ViewPager
1.什么是ViewPager?说说它的那些适配器。

2.你了解ViewPager2吗？和ViewPager 1有哪些区别？

3.ViewPager + Fragment结合使用存在的内存泄漏的原因是什么？如何解决？

2.15 View事件分发机制
1.什么是事件分发机制？主要用来解决什么问题？

2.给我说说事件分发的流程 & 你项目解决事件冲突的一些案例。

3.多点触摸事件平时接触过吗？如何监听用户第二个手指，第三个...？

4.OnTouchListener & OnTouchEvent & onClickListener三者之间的关系？

5.谈谈你对MotionEvent的认识？Cancel事件是什么情况下触发的？

6.能给我谈谈Android中坐标体系吗？

2.16 View绘制机制
1.说说View绘制流程。

2.说说Activity View树结构。

3.自定义View的方式有哪些?给我说说你之前项目中的案例。

4.invalidate和postvalidate的区别？

5.说说你在自定义View时常常重写的一些方法？

6.说说自定义View中如何自定义属性？

7.requestLayout(),onLayout(),onDraw(),drawChild()区别和联系？

8.如何计算出一个View的嵌套层级？

9.自定义View如何考虑机型适配？

2.17 布局
1.说说Android中有哪些布局 & 特点。

2.你知道布局文件到控件对象的过程吗？

3.有这么一个布局需求，一个文本控件放在屏幕一半的一半的中间位置，你如何进行布局？

4.LinearLayout,FrameLayout,RelativeLayout性能对比，为什么？

2.18 Binder
1.什么是Binder？用来干什么？

2.给我具体讲讲Binder机制。

2.19 动画机制
1.Android中的动画分为哪些种类 & 特点 & 缺点。

2.知道SVG & 矢量动画吗？

3.给我说说转场动画。

4.给我谈谈插值器 & 估值器 的作用。

5.说说Android动画框架实现的原理。

2.20 JNI
1.什么是JNI?它主要用来干什么。

2.Java Native方法如何和Native函数进行绑定的？

3.JNI如何实现数据传递？

4.如何全局捕获Native发生的异常？

5.只有C/C++能编写Native库吗？

2.21 Window & Appliction & Context
1.说说你对Android中Window的理解。

2.说说你对Application的理解 & 生命周期。

3.Android中有哪些上下文 & 区别 & 作用。

4.谈谈你对Android中Context的理解。

2.22 通知
1.Android 8.0如何适配通知？

2.自定义通知流程？

2.23 对话框(Dialog & DialogFragment & PopWindow)
1.说说Android中对话框可以用哪些方式完成？

2.24 蓝牙
1.说说最新的蓝牙版本？新版本的特性是什么？

2.25 冷启动&热启动
1.什么是冷启动 & 什么是热启动 & 它们的流程？

2.如何优化冷启动？

3.启动页白屏，黑屏，太慢如何解决？

2.26 悬浮窗
1.在做悬浮窗的时候你遇到了什么困难(主要指悬浮窗权限适配)？

2.如何制作一个悬浮窗？

2.27 Android版本
1.最新的Android版本多少知道吗？有哪些特性

2.说说更新较大的Android版本。

2.28 Android Studio
1.你现在比较常用Android Studio那个版本 & 用的Gradle版本是多少？

2.如何理解gradle?

3.说说Android Studio中大致项目结构？

4.混淆是什么 & 为什么需要进行混淆 & 混淆的原理 & 为什么Java反射常常会和混淆冲突？

2.29 UI卡顿优化
1.ANR是什么？导致原因有哪些？

2.谈谈你项目中避免ANR的一些经验。

3.分别说说Activity & BroadcastReceiver & Serice最长可耗时时间为多少？

2.30 内存优化
1.什么是OOM & 什么是内存泄漏 & 什么是内存抖动？

2.谈谈你项目中内存优化的一些经验。

2.31 屏幕适配
1.说说Android中一些屏幕单位。

2.谈谈你项目中的一些屏幕适配的经验。

3.今日头条的轻量级适配方案了解吗 & 给我说说原理。

2.32 多渠道打包 & apk签名
1.apk为什么需要签名？

2.多渠道打包是什么 & 有类似经验吗？

3.简述多渠道打包及原理和常用操作？

2.33 项目架构
1.说说你用过的项目架构？

2.分别给我说说MVC,MVP,MVVM特点和区别。

3.以登陆界面为例子,设计MVP架构。

4.谈谈AndroidManifest.xml文件的理解。

2.34 Android前沿知识
1.谷歌新出的Flutter知道吗？

2.谷歌新出的官方开发语言Kotlin了解吗 & 和Java相比它有哪些特点。

3.谈谈Kotlin中协程的认识？

2.35 音视频开发(高薪)
1.之前有过音视频开发经验吗 & 说说用哪些开源架子开发的。

2.FFmpeng了解过吗？

3.Android中播放视频音频的方式有哪些？

4.Android中播放网络地址视频有哪些出色的开源库？

5.流媒体服务器了解吗？

6.谈谈你对编码格式的理解。

7.MediaPlayer和SoundPool的区别？

8.视频硬解码和软解码的区别？

2.36 其它Android部分有关面试题
1.说说一个app的启动流程(从源码角度讲解)。

2.你知道无论是Kotlin或者是Java,程序运行的主要入口都是main()方法，那么Android的main方法在哪里？

3.Android Hock技术了解吗？

4.简述Android中的加固和使用平台？

5.谈谈你对Apk瘦身的经验？

6.为什么子线程不能更新UI？

7.你知道如何定位内存泄漏吗？

8.说说System.exit(0),onDestory(),Activity.finish()的区别？

9.在OnResume或者之前获取View的宽高为多少 & 为什么？

10.Art & Dvm 区别，特别是谈谈GC的区别。

11.说说你用的二维码框架 & 有过优化经验吗？

12.谈谈App多进程的好处 & 缺点。

13.说说AMS是怎么找到启动指定的Activity？

14.View的getWidth和getMeasureWidth有啥区别？

15.有插件化或者热修复经验吗？说说它的原理。

16.断点续传了解吗？谈谈你是如何通过多线程实现断点续传的。

17.给我谈谈你对SurfaceView的认识。

18.什么情况下你会使用到ScrollView。

19.低版本SDK如何使用高版本API？

20.AlertDialog,PopWindow,Activity之间的区别？

21.Application和Activity,Context的区别？

22.谈谈Android中多线程通信方式？

23.说说Android大体的架构图，试着画出来。

24.知道SpareArray吗？

25.Activity除了setContentView可以设置布局，还有其它方式吗？

26.Android为每个应用程序分配的内存大小为多少？

27.Android进程保活方案？

28.谈谈Android系统安装apk的过程？

29.Activity,Window,View三者的关系？

30.ActivityThread,ActivityManagerService,WindowManagerService的工作原理？

31.PackageManagerService的工作原理？

32.PowerManagerService的工作原理？

33.在桌面点击一个未启动的App的流程 & 点击一个已启动的App的流程？

34.Android中进程分为哪些种类？

35.什么是埋点，懂点它的原理吗？

36.进程和Application生命周期之间的关系？

37.App相互唤醒的有哪些方式？

38.Android中如何开启多进程？应用是否可以开启N个进程？

39.谈谈消息推送的方式有哪些？

40.谈谈你对Root权限的理解。

41.谈谈项目如何进行国际化？

42.谈谈你对Intent和IntentFilter的理解。

43.一条最长的短信息约占多少byte？


Q1：ListView和RecyclerView的使用，就问我它们有什么区别？

Q2：既然RecyclerView在很多方面能取代ListView，Google为什么没把ListView划上一条过时的横线？

Q3：你用过MVP，那你知道Dagger2吧，介绍下吧？

Q4：HashMap的内部实现原理？

Q5：Activity生命周期，有哪些启动模式，以及应用场景？

Q6：你用过AsyncTask，那你跟我说说AsyncTask的内部实现原理？

Q7：AsyncTask内部维护了一个线程池，是串行还是并行，怎么维护的？

Q8：那你说说线程池的四种初始化吧？

Q9：你用过MD，你知道怎么定义一个Behavior吗？

Q10：RecyclerView的拖拽怎么实现的？

Q11：写一个SingTop，有哪三个条件？

Q12：一个按升序排列好的数组int[] arry = {-5,-1,0,5,9,11,13,15,22,35,46},输入一个x，int x = 31，在数据中找出和为x的两个数，例如 9 + 22 = 31，要求算法的时间复杂度为O(n);

Q13：如何向一个数据库具有int类型A，B，C，D四列的表中随机插入10000条数据？如何按升序取出A列中前10个数？

Q14：service两种启动方式有什么区别？

Q15：说说三级缓存、Handler机制 ？