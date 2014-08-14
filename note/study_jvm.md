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
```
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
    Use alternate signals instead of SIGUSR1 and SIGUSR2 for VM internal signals. 
    (Introduced in 1.3.1 update 9, 1.4.1. Relevant to Solaris only.) 

-XX:+UseBoundThreads
    Bind user level threads to kernel threads. (Relevant to Solaris only.)

-XX:-UseConcMarkSweepGC	
    Use concurrent mark-sweep collection for the old generation. (Introduced in 1.4.1)

-XX:+UseGCOverheadLimit	
    Use a policy that limits the proportion of the VM's time that is spent in GC 
    before an OutOfMemory error is thrown. (Introduced in 6.)

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
    Use thread-local object allocation (Introduced in 1.4.0, known as UseTLE prior to that.) 
    [1.4.2 and earlier, x86 or with -client: false]

-XX:+UseSplitVerifier
    Use the new type checker with StackMapTable attributes. (Introduced in 5.0.)[5.0: false]

-XX:+UseThreadPriorities	
    Use native thread priorities.

-XX:+UseVMInterruptibleIO	
    Thread interrupt before or with EINTR for I/O operations results in OS_INTRPT. 
    (Introduced in 6. Relevant to Solaris only.)
```

### performance
```
-XX:+AggressiveOpts
    Turn on point performance compiler optimizations that are expected to be default in upcoming releases. (Introduced in 5.0 update 6.)

-XX:CompileThreshold=10000
    Number of method invocations/branches before compiling [-client: 1,500]

-XX:LargePageSizeInBytes=4m 
    Sets the large page size used for the Java heap. (Introduced in 1.4.0 update 1.) [amd64: 2m.]

-XX:MaxHeapFreeRatio=70
    Maximum percentage of heap free after GC to avoid shrinking.

-XX:MaxNewSize=size
    Maximum size of new generation (in bytes). Since 1.4, MaxNewSize is computed as a function of NewRatio. [1.3.1 Sparc: 32m; 1.3.1 x86: 2.5m.]

-XX:MaxPermSize=64m
    Size of the Permanent Generation.  [5.0 and newer: 64 bit VMs are scaled 30% larger; 1.4 amd64: 96m; 1.3.1 -client: 32m.]

-XX:MinHeapFreeRatio=40
    Minimum percentage of heap free after GC to avoid expansion.

-XX:NewRatio=2
    Ratio of old/new generation sizes. [Sparc -client: 8; x86 -server: 8; x86 -client: 12.]-client: 4 (1.3) 8 (1.3.1+), x86: 12]

-XX:NewSize=2m
    Default size of new generation (in bytes) [5.0 and newer: 64 bit VMs are scaled 30% larger; x86: 1m; x86, 5.0 and older: 640k]

-XX:ReservedCodeCacheSize=32m
    Reserved code cache size (in bytes) - maximum code cache size. 
    [Solaris 64-bit, amd64, and -server x86: 2048m; in 1.5.0_06 and earlier, Solaris 64-bit and amd64: 1024m.]

-XX:SurvivorRatio=8
    Ratio of eden/survivor space size [Solaris amd64: 6; Sparc in 1.3.1: 25; other Solaris platforms in 5.0 and earlier: 32]

-XX:TargetSurvivorRatio=50
    Desired percentage of survivor space used after scavenge.

-XX:ThreadStackSize=512
    Thread Stack Size (in Kbytes). (0 means use default stack size) [Sparc: 512; Solaris x86: 320 (was 256 prior in 5.0 and earlier); 
    Sparc 64 bit: 1024; Linux amd64: 1024 (was 0 in 5.0 and earlier); all others 0.]

-XX:+UseBiasedLocking
    Enable biased locking. For more details, see this tuning example. (Introduced in 5.0 update 6.) [5.0: false]

-XX:+UseFastAccessorMethods
    Use optimized versions of Get<Primitive>Field.

-XX:-UseISM
    Use Intimate Shared Memory. [Not accepted for non-Solaris platforms.] 

-XX:+UseLargePages
    Use large page memory. (Introduced in 5.0 update 5.) 

-XX:+UseMPSS
    Use Multiple Page Size Support w/4mb pages for the heap. Do not use with ISM as this replaces the need for ISM.
   (Introduced in 1.4.0 update 1, Relevant to Solaris 9 and newer.) [1.4.1 and earlier: false]

-XX:+UseStringCache
    Enables caching of commonly allocated strings.

-XX:AllocatePrefetchLines=1
    Number of cache lines to load after the last object allocation using prefetch instructions generated in JIT compiled code.
    Default values are 1 if the last allocated object was an instance and 3 if it was an array.

-XX:AllocatePrefetchStyle=1
    Generated code style for prefetch instructions.
    0 - no prefetch instructions are generate*d*,
    1 - execute prefetch instructions after each allocation,
    2 - use TLAB allocation watermark pointer to gate when prefetch instructions are executed.

-XX:+UseCompressedStrings
    Use a byte[] for Strings which can be represented as pure ASCII. (Introduced in Java 6 Update 21 Performance Release) 

-XX:+OptimizeStringConcat
    Optimize String concatenation operations where possible. (Introduced in Java 6 Update 20)  
```


