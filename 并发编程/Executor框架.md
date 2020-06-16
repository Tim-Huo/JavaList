### Executor框架的结构：

1. **任务：**包括被执行任务需要实现的接口：Runnable接口或Callable接口。
2. **任务的执行：**包括任务执行机制的核心接口Executor，以及继承自Executor的

ExecutorService接口。Executor框架有两个关键类实现了ExecutorService接口（ThreadPoolExecutor和ScheduledThreadPoolExecutor）。

3. **异步计算的结果：**包括接口Future和实现Future接口的FutureTask类。

**注：****由于FutureTask实现了Runnable，程序员也可以创建FutureTask，然后直接交给ExecutorService执行。**

### 通过Executor框架的工具类Executors，可以创建3种类型的ThreadPoolExecutor：

1. **FixedThreadPool：**可重用固定线程数的线程池。是线程池的核心实现类，用来执行被提交的任务。
  * 可控制线程最大并发数（同时执行的线程数）
  * 超出的线程会在队列中等待
1. **SingleThreadExecutor：**单个线程的线程池。
  * 有且仅有一个工作线程执行任务
  * 所有任务按照指定顺序执行，即遵循队列的入队出队规则
1. **CachedThreadPool：**大小无界的线程池。
  * 线程数无限制
  * 有空闲线程则复用空闲线程，若无空闲线程则新建线程 一定程序减少频繁创建/销毁线程，减少系统开销
1. **ScheduledThreadPool：**定时线程池。

创建一个定时线程池，支持定时及周期性任务执行。

### 线程池的5种状态：

1、线程池的初始化状态是RUNNING，能够接收新任务，以及对已添加的任务进行处理。

2、线程池处在SHUTDOWN状态时，不接收新任务，但能处理已添加的任务。  调用线程池的shutdown()接口时，线程池由RUNNING -> SHUTDOWN。

3、线程池处在STOP状态时，不接收新任务，不处理已添加的任务，并且会中断正在处理的任务。 调用线程池的shutdownNow()接口时，线程池由(RUNNING or SHUTDOWN ) -> STOP。

4、当所有的任务已终止，ctl记录的”任务数量”为0，线程池会变为Tidying状态。当线程池变为TIDYING状态时，会执行钩子函数terminated()。

5、当线程池在SHUTDOWN状态下，阻塞队列为空并且线程池中执行的任务也为空时，就会由 SHUTDOWN -> Tidying。

6、线程池彻底终止，就变成TERMINATED状态。线程池处在TIDYING状态时，执行完terminated()之后，就会由 TIDYING -> TERMINATED。

## ![图片](https://uploader.shimo.im/f/gK76YMUPjMoEaWTk.png!thumbnail)各种场景下怎么设置线程数

### 1、高并发、任务执行时间短的业务怎样使用线程池？

线程池线程数可以设置为CPU核数+1，减少线程上下文的切换。

### 2、并发不高、任务执行时间长的业务怎样使用线程池？

* 假如是业务时间长集中在IO操作上，也就是IO密集型的任务，因为IO操作并不占用CPU，所以不要让所有的CPU闲下来，可以适当加大线程池中的线程数目（2 * CPU核数），让CPU处理更多的业务。
* * 假如是业务时间长集中在计算操作上，也就是CPU密集型任务，和（1）CPU核数+1 一样吧，线程池中的线程数设置得少一些，减少线程上下文的切换
### 并发高、业务执行时间长的业务怎样使用线程池？

解决这种类型任务的关键不在于线程池而在于整体架构的设计。

### newFixedThreadPool和newSingleThreadExecutor：

上面两个主要问题是堆积的请求处理队列可能会耗费非常大的内存，甚至OOM。

![图片](https://uploader.shimo.im/f/88kDyi3TMxgF60HB.png!thumbnail)![图片](https://uploader.shimo.im/f/ZxIKwx3pV01ujx2T.png!thumbnail)

### newCachedThreadPool和newScheduledThreadPool：

上面两个主要问题是最大线程数是Integer.MAX_VALUE，可能会创建数量非常多的线程，甚至OOM。

![图片](https://uploader.shimo.im/f/aahBBGn5PWkhMkiV.png!thumbnail)

