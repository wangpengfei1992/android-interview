## okhttp ##

学习网站： [https://github.com/sucese/android-open-framework-analysis/blob/master/doc/Android%E5%BC%80%E6%BA%90%E6%A1%86%E6%9E%B6%E6%BA%90%E7%A0%81%E9%89%B4%E8%B5%8F%EF%BC%9AOkhttp.md](https://github.com/sucese/android-open-framework-analysis/blob/master/doc/Android%E5%BC%80%E6%BA%90%E6%A1%86%E6%9E%B6%E6%BA%90%E7%A0%81%E9%89%B4%E8%B5%8F%EF%BC%9AOkhttp.md)

### 1.请求响应流程 ###

1. 请求的封装
2. 请求的发送
3. 请求的调度


### 2.连接机制 ###

1. 建立连接
2. 连接池


### 3.缓存机制 ###

1. 缓存策略
2. 缓存管理


### 4.拦截器 ###


## Okhttp的子系统层级结构图 ##

![](https://raw.githubusercontent.com/sucese/android-open-framework-analysis/master/art/okhttp/okhttp_structure.png)


**网络配置层**：利用Builder模式配置各种参数，例如：超时时间、拦截器等，这些参数都会由Okhttp分发给各个需要的子系统。

**重定向层**：负责重定向。

**Header拼接层**：负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。

**HTTP缓存层**：负责读取缓存以及更新缓存。

**连接层**：连接层是一个比较复杂的层级，它实现了网络协议、内部的拦截器、安全性认证，连接与连接池等功能，但这一层还没有发起真正的连接，它只是做了连接器一些参数的处理。

**数据响应层**：负责从服务器读取响应的数据。


###  请求的发送  ###

RealCall将请求分为两种：

同步请求
异步请求

异步比同步多一个在线程处理的过程，实际上都是通过getResponseWithInterceptorChain()方法获取响应的结果。

### 请求的调度  ###

通过Dispatcher 维护3个队列;

readyAsyncCalls：准备运行的异步请求
runningAsyncCalls：正在运行的异步请求
runningSyncCalls：正在运行的同步请求

### 请求的处理 ###

![](https://raw.githubusercontent.com/sucese/android-open-framework-analysis/master/art/okhttp/request_and_response_sequence.png)

Interceptor将网络请求、缓存、透明压缩等功能统一了起来，它的实现采用**责任链模式**，各司其职， 每个功能都是一个Interceptor，上一级处理完成以后传递给下一级，它们最后连接成了一个Interceptor.Chain。

Interceptor的种类有：

RetryAndFollowUpInterceptor：负责重定向。

BridgeInterceptor：负责把用户构造的请求转换为发送给服务器的请求，把服务器返回的响应转换为对用户友好的响应。

CacheInterceptor：负责读取缓存以及更新缓存。

ConnectInterceptor：负责与服务器建立连接。

CallServerInterceptor：负责从服务器读取响应的数据。


以上便是Okhttp整个请求与响应的具体流程，**可以发现拦截器才是Okhttp核心功能所在**，我们来逐一分析每个拦截器的实现。

### CacheInterceptor ###

CacheInterceptor就是用来负责读取缓存以及更新缓存的。

整个方法的流程如下所示：

1.读取候选缓存，具体如何读取的我们下面会讲。

2.创建缓存策略，强制缓存、对比缓存等，关于缓存策略我们下面也会讲。

3.根据策略，不使用网络，又没有缓存的直接报错，并返回错误码504。

4.根据策略，不使用网络，有缓存的直接返回。

5.前面两个都没有返回，继续执行下一个Interceptor，即ConnectInterceptor。

6.接收到网络结果，如果响应code式304，则使用缓存，返回缓存结果。

7.读取网络结果。

8.对数据进行缓存。

9.返回网络读取的结果。


## 连接机制 ##
连接的创建是在StreamAllocation对象统筹下完成的，主要用来管理两个关键角色：

RealConnection：真正建立连接的对象，利用Socket建立连接。

ConnectionPool：连接池，用来管理和复用连接。

### 创建连接 ###

整个流程如下：

1.查找是否有完整的连接可用：

- Socket没有关闭
- 输入流没有关闭
- 输出流没有关闭
- Http2连接没有关闭

2.连接池中是否有可用的连接，如果有则可用。

3.如果没有可用连接，则自己创建一个。

4.开始TCP连接以及TLS握手操作。

5.将新创建的连接加入连接池。

### 连接池 ###

频繁的进行建立Sokcet连接（TCP三次握手）和断开Socket（TCP四次分手）是非常消耗网络资源和浪费时间的，HTTP中的keepalive连接对于 降低延迟和提升速度有非常重要的作用。

Okhttp支持5个并发KeepAlive，默认链路生命为5分钟(链路空闲后，保持存活的时间)，连接池有ConectionPool实现，对连接进行回收和管理。

ConectionPool在内部维护了一个线程池，来清理连接，(循环清理)

整个方法的流程如下所示：

1.查询此连接内部的StreanAllocation的引用数量。

2.标记空闲连接。

3.如果空闲连接超过5个或者keepalive时间大于5分钟，则将该连接清理掉。

4.返回此连接的到期时间，供下次进行清理。

5.全部都是活跃连接，5分钟时候再进行清理。

6.没有任何连接，跳出循环。

7.关闭连接，返回时间0，立即再次进行清理。


### 缓存机制 ###

#### 请求的缓存 ####

![](https://raw.githubusercontent.com/sucese/android-open-framework-analysis/master/art/okhttp/http_cache_structure.png)


HTTP的缓存可以分为两种：

强制缓存：需要服务端参与判断是否继续使用缓存，当客户端第一次请求数据是，服务端返回了缓存的过期时间（Expires与Cache-Control），没有过期就可以继续使用缓存，否则则不适用，无需再向服务端询问。

对比缓存：需要服务端参与判断是否继续使用缓存，当客户端第一次请求数据时，服务端会将缓存标识（Last-Modified/If-Modified-Since与Etag/If-None-Match）与数据一起返回给客户端，客户端将两者都备份到缓存中 ，再次请求数据时，客户端将上次备份的缓存 标识发送给服务端，服务端根据缓存标识进行判断，如果返回304，则表示通知客户端可以继续使用缓存。
强制缓存优先于对比缓存。


缓存机制是**基于DiskLruCache**做的


