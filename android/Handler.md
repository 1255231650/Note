需要先调用Looper.prepare()才能创建Handler。

主线程会自动调用Looper.prepare()方法。

### 发送消息

new一个Message对象，调用handler.sendMessage方法发送出去。
