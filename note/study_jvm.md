###### jvm 命令
```shell
编译
javac -d classes -sourcepath src -classpath classes:lib/test.jar src/test/Test1.java src/test/Test2.java

执行
java -classpath classes:lib/test.jar test.Test

显示默认参数
java -XX:+PrintCommandLineFlags -version
```
