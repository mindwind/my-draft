###### jvm command
```shell
编译
javac -d classes -sourcepath src -classpath classes:lib/test.jar src/test/Test1.java src/test/Test2.java

执行
java -classpath classes:lib/test.jar test.Test

显示默认参数
java -XX:+PrintCommandLineFlags -version
```


###### jvm cpu 
```shell
占用 cpu 最高的线程
top -p pid -H

线程栈导出
jstack -F pid > stack.log
```


###### jvm memory 
```shell
dump 内存
jmap -F -dump:format=b,file=heap.dump pid

显示内存使用情况，该命令会触发 gc 生产系统慎用
jmap -histo:live pid | head

分析 dump 文件
jhat -J-mx4096m -port 7000 heap.dump
```


###### jvm options
```shell

```
