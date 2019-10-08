## RxAndroid ##

RxAndroid是RxJava的一个针对Android平台的扩展。它包含了一些能够简化Android开发的工具。


### 常用的 ###

1. **AndroidSchedulers**提供了针对Android的线程系统的调度器。需要在UI线程中运行某些代码？很简单，只需要使用AndroidSchedulers.mainThread():


2.  **AndroidObservable**，它提供了跟多的功能来配合Android的生命周期。bindActivity()和bindFragment()方法默认使用AndroidSchedulers.mainThread()来执行观察者代码，这两个方法会在Activity或者Fragment结束的时候通知被观察者停止发出新的消息。


3. AndroidObservable.fromBroadcast()方法，它允许你创建一个类似BroadcastReceiver的Observable对象。


4.  **ViewObservable**,使用它可以给View添加了一些绑定。如果你想在每次点击view的时候都收到一个事件，可以使用ViewObservable.clicks()，或者你想监听TextView的内容变化，可以使用ViewObservable.text()



### RxAndroid的一些使用场景 ###


1. 界面需要等到多个接口并发取完数据，再更新


2. 界面按钮需要防止连续点击的情况

3. 响应式的界面 比如勾选了某个checkbox，自动更新对应的preference