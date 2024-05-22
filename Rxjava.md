本质上是一个实现异步操作的库。

使用的是通用形式的观察者模式。

### Rxjava中的四个基本概念

Observable(可观察者，即被观察者)、Observer(观察者)、subscribe(订阅)、事件

### 事件回调方法

onNext():

onCompleted():事件队列完结，之后不会再有新的onNext()发出

onError():事件异常队列，在事件处理过程中出异常时被触发

### 基本实现

1.  创建Observer

    Observer或Subscrober。二者基本使用方式一样，区别在于Subscriber有两个增加的方法：onStart()和unsubscribe()

2.  &#x20;创建Observable

    Observable即被观察者，他决定什么时候处罚怎样的事件。Rxjava使用create()方法创建一个Observable

    *   just(T....)：将传入的参数一次发送出来
    *   from(T\[])/from(Iterable)：将传入的数组或Iterable拆分成具体对象后，一次发送出来

3.  使用subscribe()方法将Observable和Observer联结起来
    `observable.subscribe(observer);
    // 或者：
    observable.subscribe(subscriber);`

    subscribe()还支持不完整定义的回调`
    Action1 onNextAction = new Action1() {
    // onNext()
    @Override
    public void call(String s) {
    System.out.println(s);
    }
    };
    Action1 onErrorAction = new Action1() {
    // onError()
    @Override
    public void call(Throwable throwable) {
    // Error handling
    }
    };
    Action0 onCompletedAction = new Action0() {
    // onCompleted()
    @Override
    public void call() {
    System.out.println("completed");
    }
    };
    // 自动创建 Subscriber ，并使用 onNextAction 来定义 onNext()
    observable.subscribe(onNextAction);
    // 自动创建 Subscriber ，并使用 onNextAction 和 onErrorAction 来定义 onNext() 和 onError()
    observable.subscribe(onNextAction, onErrorAction);
    // 自动创建 Subscriber ，并使用 onNextAction、 onErrorAction 和 onCompletedAction 来定义 onNext()、 onError() 和 onCompleted()
    observable.subscribe(onNextAction, onErrorAction, onCompletedAction);`

### 线程控制

**使用Scheduler控制线程。**

*   `Schedulers.immediate()`: 直接在当前线程运行，相当于不指定线程。这是默认的 `Scheduler`；
*   `Schedulers.io()`: IO 操作所使用的 `Scheduler`；
*   `Schedulers.computation()`: 计算所使用的 `Scheduler`;
*   `Schedulers.newThread()`: 总是启用新线程，并在新线程执行操作。
*   另外， Android 还有一个专用的 `AndroidSchedulers.mainThread()`，它指定的操作将在 Android 主线程运行。

**使用subscribeOn()和observeOn()对线程进行控制**

*   subscribeOn()：指定subscribe()所发生的线程，或者叫事件产生线程
*   observeOn()：指定Subscriber所运行在的线程。或者叫事件消费线程

**Scheduler的原理**

当使用了多个subscribeOn()的时候，只有第一个subscribeOn()起作用

### 变换

Rxjava提供了对事件序列进行变换的支持。

所谓变换，就是将事件序列中的对象或整个序列进行加工处理，转换成不同的事件或事件序列。

*   map()：
*   flatMap()：
*   throttleFirst()：在每次事件触发后的一定时间间隔内丢弃新的事件。常用作去抖动过滤。

**变换的原理？？？lift**

*   compose()：针对Observable自身进行变换

