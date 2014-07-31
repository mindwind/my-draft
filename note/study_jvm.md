## jvm command
```shell
编译
javac -d classes -sourcepath src -classpath classes:lib/test.jar src/test/Test1.java src/test/Test2.java

执行
java -classpath classes:lib/test.jar test.Test

显示默认参数
java -XX:+PrintCommandLineFlags -version
```


## jvm cpu 
```shell
占用 cpu 最高的线程
top -p pid -H

线程栈导出
jstack -F pid > stack.log
```


## jvm memory 
```shell
dump 内存
jmap -F -dump:format=b,file=heap.dump pid

显示内存使用情况，该命令会触发 gc 生产系统慎用
jmap -histo:live pid | head

分析 dump 文件
jhat -J-mx4096m -port 7000 heap.dump
```


## jvm options
选项说明
```
-X  非标准选项 
-XX 非稳定选项

-XX:+<option>         启用选项
-XX:-<option>         不启用选项
-XX:<option>=<number> 给选项设置一个数字类型值，可跟单位，例如 32k, 1024m, 2g
-XX:<option>=<string> 给选项设置一个字符串值，例如-XX:HeapDumpPath=./dump.core
```

### behavioral
```shell
-XX:-AllowUserSignalHandlers  
    Do not complain if the application installs signal handlers. (Relevant to Solaris and Linux only.)

-XX:-DisableExplicitGC
    By default calls to System.gc() are enabled (-XX:-DisableExplicitGC). 
    Use -XX:+DisableExplicitGC to disable calls to System.gc().
    Note that the JVM still performs garbage collection when necessary.

-XX:+FailOverToOldVerifier
    Fail over to old verifier when the new type checker fails. (Introduced in 6.)

-XX:+HandlePromotionFailure
    The youngest generation collection does not require a guarantee of full promotion of all live objects. 
    (Introduced in 1.4.2 update 11) [5.0 and earlier: false.]

-XX:+MaxFDLimit
    Bump the number of file descriptors to max. (Relevant  to Solaris only.)
```
