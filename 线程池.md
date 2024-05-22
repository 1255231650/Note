### 创建线程的方法

1.  继承Thread类并重写run方法

    实现简单，不可继承其他类

2.  实现Runnable接口并重写run方法

    避免了单继承，更灵活

3.  实现Callable接口并重写callfangfa

    可以获取执行结果的返回值，并可以抛出异常

4.  使用Executors工具类创建线程池

### 为什么要有线程池

线程的创建和销毁很好使很浪费性能，使用线程池实现线程复用来解决这个问题

\*\* 好处： \*\*

*   减低资源消耗
*   提高响应速度
*   提高线程的可管理性

### 创建线程池的方法

    public ThreadPoolExecutor(
    	int corePoolSize,						//核心线程数
        int maximumPoolSize,					//最大线程数
        long keepAliveTime,						//线程空闲时间
        TimeUnit unit,							//keep
        BlockingQueue<Runnable> workQueue,		//工作队列
        ThreadFactory threadFactory,			//线程工厂
        RejectedExecutionHandler handle			//拒绝策略
    )

### 线程池处理任务的流程

1.  核心线程池未满，创建一个新的线程执行任务
2.  核心线程池已满，工作队列未满，将任务存储在工作队列中
3.  工作队列已满，线程数小于最大线程数就创建一个新线程处理任务
4.  超过最大线程数，按照拒绝策列来处理任务

### 线程池的执行和关闭

*   执行任务：submit()和execute()方法

    execute()只能执行Runnable类型的任务。没有返回值，不能判断执行成功与否。

    submit()可以执行Runnable和Callable类型的任务。用于提交需要返回值的任务。返回一个Future判断是否执行成功。方便Exception
*   关闭线程池：shutdown()或shutdownNow()方法

    shutdownNow：先将线程池的状态设置为STOP，然后尝试停止正在执行或暂停的线程，并返回执行的列表

    shutdown：只是将线程池的状态设置为SHUTDOWN，然后终端没有正在执行任务的线程。通常使用shutdown来关闭线程池，如果任务不一定要执行完可调用shutdownNow

