**OkHttp 是一个高效的 Http 请求框架，旨在简化客户端网络请求，提高请求效率。**

## 使用方式
1. 创建 OkHttpClient 对象
2. 构建 Request
3. 调用 OkHttpClient 执行 request 请求
4. 同步阻塞或者异步回调方式接收结果

**在使用过程中，对于 OkHttpClient 应该缓存下来或者使用单例模式以便复用。**

