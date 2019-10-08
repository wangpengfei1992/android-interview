## RxJava ##

### RxJava是什么 ###

一个在**Java VM上使用**，**可观测的序列**来组成**异步的**、**基于事件**的程序库。


### RxJava 好在哪 ###

一个词：**简洁**。

Android 创造的 AsyncTask 和Handler ，其实都是为了让异步代码更加简洁。RxJava 的优势也是简洁，但它的简洁的与众不同之处在于，随着程序逻辑变得越来越复杂，它依然能够保持简洁。

### 关键方法 ###

subscribeOn(Schedulers.io) //指定suscribe（订阅处理事件） 发生在io线程

observeOn(Schedulers.main)//指定回调事件发生的线程

map(String,Bitmap)  //将String对象，进过方法后返回Bitmap对象

flatmap(String,Oberseable(String))

//和map的共同点，都是返回一个对象

//不同点是，flatmap返回一个Observable对象，且并不是回调到Observer方法中

1.传入对象，创建Observable

2.激活Observable,发送事件

3.所有事件，统一汇总到一个Observable中

4.汇总后，发送给Observer

**常用的方法**

flatmap  map  filter  subscribeOn  observeOn  subscribe  lift(变换)

**事件方法类型**

create() , just() , from() 等 --- **事件产生**

map() , flapMap() , scan() , filter()  zip()等 -- **事件加工**

subscribe() -- **事件消费**


### 对象 ###

观察者模式，android常见的是点击事件的监听

Observable(被观察者) 

Observer(观察者)  

subscribe(订阅)

Subscriber(Observer的抽象类)


### 线程 ###

Schedulers.io( io 线程 无数量上限的线程池，可以重用空闲的线程)  
 
Schedulers.main(主线程)  

Schedulers.newThread(新线程，总是启用新线程，并在新线程执行操作)

**observeOn()回调线程可以多次切换** **subscribeOn() 只能切换一次**

### 回调方法Action ###

Action1和Action0 是接口，只有一个方法call().可以指定观察者只执行部分方法（onNext(),onComplete(),onError()）;Action1 有一个参数无返回值，Action0 无参数无返回值。
  还有Action2,Action3...........

### 其他常见的事件 ###

**Map**是RxAndroid中最简单的一个变换操作符了, 它的作用就是对Observable发送的每一个事件应用一个函数, 使得每一个事件都按照指定的函数去变化。

**Zip**通过一个函数将多个Observable发送的事件结合到一起，然后发送这些组合到一起的事件. 它按照严格的顺序应用这个函数。它只发射与发射数据项最少的那个Observable一样多的数据。

**from**在Rxndroid的from操作符到2.0已经被拆分成了3个，fromArray, fromIterable, fromFuture接收一个集合作为输入，然后每次输出一个元素给subscriber。


**filter**条件过滤，去除不符合某些条件的事件。

**take**最多保留的事件数。

**doOnNext**如果你想在处理下一个事件之前做某些事，就可以调用该方法

**debounce** 防抖动

学习网址：[https://www.jianshu.com/p/7eb5ccf5ab1e](https://www.jianshu.com/p/7eb5ccf5ab1e)


### RxJava 的适用场景 ###

- 与 Retrofit 的结合
- RxBinding
- 各种异步操作（例如数据库的读写、大图片的载入、文件压缩/解压等各种需要放在后台工作的耗时操作）
- RxBus（思想是使用 RxJava 来实现了 EventBus ）


