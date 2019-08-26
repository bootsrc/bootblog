# 使用jetty来启动自己的项目

VM options "webapp"  的配置

调试位置
```text
org.eclipse.jetty:jetty-webapp.jar

org.eclipse.jetty.webapp.WebInfConfiguration

line 502

 if (!web_app.exists() || !web_app.isDirectory())
断点放在web_app可以看到现在取到的webapp的值， 如果这个值不是javaweb项目的webapp路径。那就需要修改下。


解决办法是在IDEA的debug的VM options里面增加 -Dwebapp=xxxxx/webapp
即可
```