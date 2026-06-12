
### 1. 答案

答：

1. 定义：监听并分发 IO 事件的模型，本质是一种线程模式/模型
2. 作用： 解决传统阻塞 IO 中一个连接对应一个线程的问题
3. 分类：
    
    ① 单线程模式：一个线程处理所有连接的IO事件
    
    ② 多线程模式：多个线程处理所有连接的IO事件（实现：NioEventLoopGroup不需要任何参数，默认启动2倍CPU核数的线程）
    
    ③ 主从多线程模式：
    
    Boss是主 Reactor，Worker是从 Reactor
    
    主Reactor负责处理 Accept事件，然后把 Channel 注册到从 Reactor上，从Reactor负责Channel生命周期内的所有l/O事件
    

### 2. 辅助理解

1. 文章参考：[03 引导器作用：客户端和服务端启动都要做些什么？](https://learn.lianglianglee.com/%e4%b8%93%e6%a0%8f/Netty%20%e6%a0%b8%e5%bf%83%e5%8e%9f%e7%90%86%e5%89%96%e6%9e%90%e4%b8%8e%20RPC%20%e5%ae%9e%e8%b7%b5-%e5%ae%8c/03%20%20%e5%bc%95%e5%af%bc%e5%99%a8%e4%bd%9c%e7%94%a8%ef%bc%9a%e5%ae%a2%e6%88%b7%e7%ab%af%e5%92%8c%e6%9c%8d%e5%8a%a1%e7%ab%af%e5%90%af%e5%8a%a8%e9%83%bd%e8%a6%81%e5%81%9a%e4%ba%9b%e4%bb%80%e4%b9%88%ef%bc%9f.md)
2. 实现
    
    ① 单线程模式
    
    ```java
    EventLoopGroup group = new NioEventLoopGroup(1);
    
    ServerBootstrap b = new ServerBootstrap();
    
    b.group(group)
    ```
    
    ② 多线程模式
    
    ```java
    EventLoopGroup group = new NioEventLoopGroup();
    
    ServerBootstrap b = new ServerBootstrap();
    
    b.group(group)
    ```
    
    ③ 主从多线程模式
    
    ```java
    EventLoopGroup bossGroup = new NioEventLoopGroup();
    
    EventLoopGroup workerGroup = new NioEventLoopGroup();
    
    ServerBootstrap b = new ServerBootstrap();
    
    b.group(bossGroup, workerGroup)
    
    ```