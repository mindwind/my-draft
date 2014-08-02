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
    Bump the number of file descriptors to max. (Relevant to Solaris only.)

-XX:PreBlockSpin=10
    Spin count variable for use with -XX:+UseSpinning. (Introduced in 1.4.2.)
    Controls the maximum spin iterations allowed before entering operating system thread synchronization code.

-XX:-RelaxAccessControlCheck
    Relax the access control checks in the verifier. (Introduced in 6.)

-XX:+ScavengeBeforeFullGC
    Do young generation GC prior to a full GC. (Introduced in 1.4.1.)

-XX:+UseAltSigs	
    Use alternate signals instead of SIGUSR1 and SIGUSR2 for VM internal signals. (Introduced in 1.3.1 update 9, 1.4.1. Relevant to Solaris only.) 

-XX:+UseBoundThreads
    Bind user level threads to kernel threads. (Relevant to Solaris only.)

-XX:-UseConcMarkSweepGC	
    Use concurrent mark-sweep collection for the old generation. (Introduced in 1.4.1)

-XX:+UseGCOverheadLimit	
    Use a policy that limits the proportion of the VM's time that is spent in GC before an OutOfMemory error is thrown. (Introduced in 6.)

-XX:+UseLWPSynchronization
    Use LWP-based instead of thread based synchronization. (Introduced in 1.4.0. Relevant to Solaris only.)

-XX:-UseParallelGC	
    Use parallel garbage collection for scavenges. (Introduced in 1.4.1)

-XX:-UseParallelOldGC	
    Use parallel garbage collection for the full collections. 
    Enabling this option automatically sets -XX:+UseParallelGC. (Introduced in 5.0 update 6.)

-XX:-UseSerialGC	
    Use serial garbage collection. (Introduced in 5.0.)

-XX:-UseSpinning
    Enable naive spinning on Java monitor before entering operating system thread synchronizaton code. 
    (Relevant to 1.4.2 and 5.0 only.) [1.4.2, multi-processor Windows platforms: true]

-XX:+UseTLAB
    Use thread-local object allocation (Introduced in 1.4.0, known as UseTLE prior to that.) [1.4.2 and earlier, x86 or with -client: false]

-XX:+UseSplitVerifier
    Use the new type checker with StackMapTable attributes. (Introduced in 5.0.)[5.0: false]

-XX:+UseThreadPriorities	
    Use native thread priorities.

-XX:+UseVMInterruptibleIO	
    Thread interrupt before or with EINTR for I/O operations results in OS_INTRPT. (Introduced in 6. Relevant to Solaris only.)
```


