# org.codehaus.classworlds



jar包依赖为
```text
<!-- For launcher -->
<dependency>
    <groupId>org.codehaus.plexus</groupId>
    <artifactId>plexus-classworlds</artifactId>
    <version>2.4.4-HEXNOVA</version>
</dependency>
```

start shell关键点
```shell script
CLASSPATH="$PROJECT_HOME/libs/plexus-classworlds-2.4.4-HEXNOVA.jar"
MAIN_CLASS="org.codehaus.classworlds.Launcher"


```

你需要定义一个classpath.classworlds文件。
```text
main is com.example.launcher.ServerLauncher from link

[link]
load ${project.home}/libs/*.jar
load ${project.home}/conf
load ${project.home}/classes

```
在启动jvm的shell脚本中增加如下参数
```shell script
-Dclassworlds.conf=\"yourFilePath/classpath.classworlds\""
```
