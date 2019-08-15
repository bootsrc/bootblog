# MPush简介

###基于Netty的开源实时消息推送系统

* 官网：[https://mpusher.github.io](https://mpusher.github.io)
* 文档：[http://mpush.mydoc.io](http://mpush.mydoc.io)

后端基于Netty，辅以redis，zookeeper。 Android端使用NIO， iOS端使用原生端Socket编程

* Netty： 服务器端提供Nio Socket服务
* Redis: 存放每个userId对应端客户端所在机器的路由。
* zookeeper: 存放每个机器的节点元数据，如ip和port
* App-server: 自己的应用项目
* mpush-client.jar: App-server需要引用的一个jar包，相当于一个服务器端的sdk，封装了跟mpush-boot的访问接口.
* mpush-client-java.jar: Android端端sdk jar包。
