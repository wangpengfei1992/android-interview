如何保证service在后台不被kill？

利用的系统广播是Intent.ACTION_TIME_TICK，这个广播每分钟发送一次，我们可以每分钟检查一次Service的运行状态，ActivityManager.getRuningServices()获取所有活动的service,根据名字用equals判断其中没有这个service了，就重新启动Service。

横竖屏切换Activity生命周期的调用次数：

(1)orientation：消除横竖屏的影响

(2)keyboardHidden：消除键盘的影响

(3)screenSize：消除屏幕大小的影响

无Configchanges配置，横屏一次，竖屏2次

Configchanges=oritation 横竖屏各一次

Configchanges=oritation|keybordhidden 不调用生命周期，只调用onConfigerationChanged()方法


Static可用于修饰在哪些地方？

静态变量，方法，静态内部类，静态代码块，静态导包


Fragment 如何实现类似 Activity 栈的压栈和出栈效果的？

Fragment 的事物管理器内部维持了一个双向链表结构，该结构可以记录我们每次 add 的Fragment 和 replace 的 Fragment，然后当我们点击 back 按钮的时候会自动帮我们实现退栈操作。


你如何评价Android系统？优缺点？

优点：

开放性：开发的平台允许任何移动终端厂商加入到Android联盟中来，有丰富的软件，硬件。
挣脱运营商的束缚；接入google服务。

缺点：硬件、屏幕太多难适配；安全和隐私，信息被google监视


context的引用：

不要让生命周期长的对象引用activitycontext，即保证引用activity的对象要与activity本身生命周期是一样的。

对于生命周期长的对象，可以使用applicationcontext。
避免非静态的内部类，尽量使用静态类，避免生命周期问题，注意内部类对外部对象引用导致的生命周期变化。


按照图片尺寸让imageview自适应：
通过DisplayMetrics获取屏幕的宽，根据每行显示几列得到每个图片的宽度，根据需要的比例设置图片的高度。


Android cup型号有哪些？

Android 设备的CPU类型(通常称为”ABIs”)，目前有7中类型：

mips / mips64: 极少用于手机可以忽略

x86: 平板、模拟器用得比较多。

x86_64: 64位的平板，x86占有量很低。

armeabi:  第5代、第6代的ARM处理器，早期的手机用的比较多，缺少对浮点数计算的硬件支持，在需要大量计算时有性能瓶颈

armeabi-v7a: ARM v7 目前主流版本，一般市面上的骁龙系列或者麒麟系列的处理器绝大部分都是这种架构

arm64-v8a: 第8代64位处理器，所谓的ARMv8架构，就是在MIPS64架构上增加了ARMv7架构中已经拥有的的TrustZone技术、虚拟化技术及NEON advanced SIMD技术等特性，研发成的。


App进程保活

1.白色保活

启动一个前台的Service进程，这样会在系统的通知栏生成一个Notification，用来让用户知道有这样一个app在运行着，哪怕当前的app退到了后台。

2.灰色保活

同时启动两个id相同的前台Service，然后再将后启动的Service做stop处理；它不会在系统通知栏处出现一个Notification，看起来就如同运行着一个后台Service进程一样。


merge和viewstub使用区别？

merge标签作为跟标签，不会增加view嵌套层数，一般与include一起使用
ViewStub是一个不可见的,实际上是把宽高设置为0的View。ViewStub 标签最大的优点是当你需要时才会加载。
inflate()方法只能调用一次。


	<ViewStub
	android:id="@+id/stub_import"
	<!--android:inflateId：重写ViewStub的父布局控件的Id-->
	android:inflatedId="@+id/panel_import"
	< <!--android:layout：设置ViewStub被inflate的布局-->
	android:layout="@layout/progress_overlay"
	android:layout_width="fill_parent"
	android:layout_height="wrap_content"
	android:layout_gravity="bottom" />

	-------------------------------------------------

	//当你想加载布局时，可以使用下面其中一种方法：
	((ViewStub) findViewById(R.id.stub_import)).setVisibility(View.VISIBLE);
	// or
	View importPanel = ((ViewStub) findViewById(R.id.stub_import)).inflate();



Android中跨进程通讯的几种方式？

AIDL   广播   ContentProvider

SharedPreferences存储位置和格式是什么？

SharedPreferences 将数据文件写在了手机内存私有的目录中该app的文件夹下。在data\data\程序包名\shared_prefs目录，为shapsname.xml文件。

	<?xml version='1.0' encoding='utf-8' standalone='yes'>
	<map>
	<string name="name">小明</string>
	</map>



SharedPreferences sharedPreferences = this.getSharedPreferences("test", MODE_PRIVATE);
其中getSharedPreferences方法第二个参数就是对文件权限的描述。

这个参数有四个可选值：

Activity.MODE_PRIVATE：表示该文件是私有数据，只能被应用本身访问，在该模式下，写入的内容会覆盖原文件的内容

Activity.MODE_APPEND：也是私有数据，新写入的内容会追加到原文件中

Activity.MODE_WORLD_READABLE：表示当前文件可以被其他应用读取

Activity.MODE_WORLD_WRITEABLE：表示当前文件可以被其他应用写入

SharedPreferences是线程安全的吗?

获取加了同步锁，是线程安全的


主流网络请求框架库对比分析：

![](https://mmbiz.qpic.cn/mmbiz_png/82jN7o40p6l4NdPbnfaGibUO8zwegIkm2Rz4lLay4HnLLNFFsI76MOyA0LpqIFibOoIDru3ZaRHuoIJeZPtruLzg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


Glide与Picasso的使用区别：

Glide库要比Picasso大3倍，picasso更轻量级

Glide使用可以传入Activity或fragment，可以让glide加载的声明周期与页面同步。

Glide支持加载Gif，picasso不支持


App异常退出时，打印日志，重新启动怎么做？
在Application中注册UncaughtExceptionHandler，当发生崩溃会回调uncaughtException()方法，此时在其中做打印日志，重新启动等操作。

	public class MyApplication extends Application {

	private static MyApplication application;
	@Override
	public void onCreate() {
	super.onCreate();
	application = this;
	// 程序崩溃时触发线程 以下用来捕获程序崩溃异常
	Thread.setDefaultUncaughtExceptionHandler(handler);
	}
	private Thread.UncaughtExceptionHandler handler = new Thread.UncaughtExceptionHandler() {
	@Override
	public void uncaughtException(Thread t, Throwable e) {
	restartApp(); //发生崩溃异常时,重启应用
	}
	};
	private void restartApp() {
	Intent intent = new Intent(this, MainActivity.class);
	PendingIntent restartIntent = PendingIntent.getActivity(
	application.getApplicationContext(), 0, intent,Intent.FLAG_ACTIVITY_NEW_TASK);
	//退出程序
	AlarmManager mgr = (AlarmManager)application.getSystemService(Context.ALARM_SERVICE);
	mgr.set(AlarmManager.RTC, System.currentTimeMillis() + 1000,
	restartIntent); // 1秒钟后重启应用

	//结束进程之前可以把你程序的注销或者退出代码放在这段代码之前
	android.os.Process.killProcess(android.os.Process.myPid());
	}

	}



自定义view绘制优化：
1、尽量避免在onDraw()中做多了事，减少绘制内容。
2、尽量少调用invalidate()，这样会少调用onDraw()
3、使用硬件加速，提升绘制性能。在view引入的布局中加入android:layerType="hardware"属性。


Recyclerview比Listview强大的地方

1、自带横向滑动，瀑布流布局。可通过自定义Layoutoutmanager制定强大的布局方式。

2、封装了Viewholder，自带复用ConvertView。

3、addItemAnimation()，加入动画方便。

4、有局部刷新，有notifyItemChanged()，notifyItemRemove()方法。

Android子线程为什么不能更新UI？

Android不允许子线程更新UI是因为UI访问是没有加锁的，多个线程访问UI不是线程安全的
检测机制：ViewRootImpl中的checkThread()方法进行判断。



	void checkThread() {
	if (mThread != Thread.currentThread()) {
	throw new CalledFromWrongThreadException(
	"Only the original thread that created a view hierarchy can touch its views.");
	}
	}



Serializable和Parcelable的理解和区别

对象为什么需要序列化？
序列化后才能保存对象到本地文件，在网络中传输，在进程中传输。


Serializable和Parcelable的区别：

1.两者最大的区别在于 存储媒介的不同，Serializable 使用 I/O 读写存储在硬盘上，而 Parcelable 是直接 在内存中读写。很明显，内存的读写速度通常大于 IO 读写，所以Parcelable效率更高。

2.Serializable在序列化的时候会产生大量的临时变量，从而引起频繁的GC（内存回收）。

3.Parcelable不能保存到本地和网络传输，这种情况要使用Serializable，如果只是对象传递优先使用Parcelable。

4.Parcelable会生成大量的模板代码，使用没有Serializable方便。


什么是Android动态布局？

将原本xml布局文件中设置的属性改为在代码中进行相应设置，xml布局属性在代码里有一一对应的方法。
设置位置和大小根据LayoutParams属性来设置，可以设置在父view中的左上右下边距，宽高尺寸。


Activity Window View之间是什么关系？

Activity创建出来后，随机会new一个PhoneWindow。当Activity调用setContentView()，会创建一个Decorview，将DecorView作为整个应用窗口的根视图。内部有一个垂直LinearLayout，上面一个view是ActionBar,下面就是id为content的Framelayout，将setContentView()中的view添加到这个FrameLayout中。


SparseArray与Hashmap的区别？

SparseArray内部属性：
private int[] mKeys;
private Object[] mValues;
SparseArray内部是存放了2个数组作为键值对的存储，int[]数组存放key，Object[]数组存放value，不使用额外的结构体（Entry)，单个元素的存储成本下降，会比Hashmap更节省内存。
SparseArray操作效率比Hashmap低。


json与xml的优缺点比较

json数据量小，传输更快，解析简单；xml解析复杂，xml描述性更好。


res/drawable、res/raw、/assets下的区别

res文件夹和assets文件夹区别：

1.res下创建文件，能将ID注册在R文件中，即能通过R.res.xx获取属性。assets需要用径路来使用文件。

2.res下，打包时自动只打包用的上的文件，没用上的文件不打包；assets文件夹里，无论是否在项目中用到，会被原封不动的打包到APK。

3.res/raw,res/assets下图片不会被压缩，res/drawable下会被压缩。


Android长连接怎么处理心跳机制?

维护任何一个长连接都需要心跳机制，客户端发送一个心跳给服务器，服务器给客户端一个心跳应答，这样就形成客户端服务器的一次完整的握手。