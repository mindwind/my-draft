## linux 常用命令

### 文件描述符
```
- ulimit -a
  查看本用户允许打开文件数 [open files]

- ulimit -n
  open files   (-n) 70000
  修改本用户允许打开文件数

- vim /etc/security/limits.conf
  所有用户打开文件数配置，如下：
  * soft nofile 102400
  * hard nofile 102400
  第一列表示域名，可用用户名或组名（@开头），通配符 * 表示全部
  第二列表示类型，值可以是 soft 或 hard
  第三列表示项目，nofile（Number of Open File）表示打开文件数
  第四列表示取值，如 102400

- cat /proc/sys/fs/file-nr
  1792	0	793580
  第一个值代表已分配的文件句柄
  第二个值代表已使用的文件句柄
  第三个值代表文件句柄的最大值

- lsof -p pid | wc -l
  查看某一进程打开的文件数（含设备和 socket 文件）

- lsof -u tomcat | wc -l
  查看用户 tomcat 打开的文件数

- lsof -u root -a -U
  仅列出root 的所有程序开启的 socket 文件

- lsof +d /dev
  列出目前系统上面所有被使用周边设备文件

- lsof -u root | grep tomcat
  列出属于 root tomcat 这支程序所开启的文件
```


### 时间
```
- at -f test.sh now + 5minutes
  5分钟后执行 test.sh

- at -f test.sh 23:00 2013-01-14
  指定时间执行 test.sh

- atq  
  查询目前主机上面有多少 at job

- atrm 5
  将第 5 个 job 移除

- crontab 0 12 * * *  command
  在每天的 12:00 发信给自己
  0 12 * * * mail dmtsai -s "at 12:00" < /home/dmtsai/.bashrc
  代表意: 分钟 小时 日期 月 周 指令
  数字范围  0-59   0-23    1-31   1-12  0-7   command
  0 3,6 * * *   command
  时间参数还是有五栏,不过第二栏是 3,6 ,代表 3 和 6 都适用
  20 8-12 * * * command
  8 点到 12 点间的每小时的 20 分都进行一项工作
  */n * * * *   command
  那个 n 代表数字，亦即是 [每隔 n 单位间隔] 的意思，例如每 n 分钟进行一次

- crontab -l
  查询使用者目前的 crontab 内容

- crontab -r
  删除全部内容

- date -s 08/14/12
  设置日期

- date -s 18:22:20
  设置时间
```


### 权限
```
- chown -R user:group dir/file
  递归改变目录或文件拥有者和群组

- chgrp -R groupname dir/file
  递归改变目录或文件的群组

- chmod -R 755 dir/file
  r=4, w=2, x=1 改变权限

- groupadd group1
  新增 group1 组

- groupmod -n mygroup group1
  改变组名，将 group1 重命名为 mygroup

- groupdel group1
  删除 group1 组

- gpasswd -A vbird1 group1
  root用户将 vbird1 设置为 group1 的群组管理员

- gpasswd -a vbird3 testgroup
  群组管理员将 vbird3 加入群组

- id user
  查询某人或自己的相关 UID/GID 等信息

- passwd test1
  修改密码

- passwd -l test1
  锁定

- passwd -u test1
  解锁

- su - username 
  切换身份, run a shell with substitute user and group IDs  

- useradd test1 
  创建账户

- useradd -g testgroup test2
  创建账号并添加到分组

- usermod -e "2009-12-31" vbird2 
  修改账号属性，用户 vbird2 密码在 2009/12/31 失效

- userdel -r vbird2 
  删除 vbird2 ,连同家目录一起删除
```


### 文件
```
- chattr +AS file/dir
  配置文件隐藏属性，+A 不写 atime 提高 io 性能，+S 立即同步到磁盘

- cp srcfile destfile
  拷贝文件

- cp -au srcfile/dir destfile/dir
  备份文件（完整copy文件属性且只在源文件比目标文件新时覆盖）

- cp -s srcfile destfile
  创建symbolic link

- cat /proc/cpuinfo
  查看cpu信息

- cat filename
  完整查看文件

- cat /proc/version
  查看内核版本

- cat -n x.log | grep '21:58:' | more
  查看日志文件

- find /home mtime +3(-3,3)
  查找3天前（3天内，第3天）变动过的文件

- find /home -user test
  查找 test 用户的文件

- find /home -name filename
  按文件名查找

- find /home -size +1G
  查找大于1G的文件

- find /home -exec command {} \;
  find 之后额外指令（-exec和\;之间，{}代表find的结果）

- file filename
  观察文件类型（纯文本、二进制）

- ls -alht
  查看文件详细信息（按合适的大小单位分行排列和时间排序）

- lsattr file/dir
  查看文件隐藏属性

- ln -s target linkName
  建立符号链接（不加-s 建立hard link）

- locate somefile.txt
  定位文件

- less -N file
  查看文件内容（显示行号 space=向下翻页， b=向上翻页， /word 搜索）

- mkdir -m 755 /t1
  创建目录并预设权限

- mkdir -p /t1/t2/t3
  递归建立多层目录

- split -b 300k /etc/termcap prefix 
  按字节拆分文件

- split -l 500 /etc/termcap prefix 
  按行数拆分文件

- scp -r /src/dir root@ip:/dst/dir         
  远程拷贝，复制目录  从本地到远程

- scp /src/file root@ip:/dst/dir           
  远程拷贝，复制文件  从本地到远程

- scp -r root@ip:/src/dir /dst/dir         
  远程拷贝，复制目录  从远程到本地

- scp root@ip:/src/file /dst/file          
  远程拷贝，复制文件  从远程到本地

- tar -czf file.tar.gz file/dir                          
  打包压缩 

- tar -zpcvf /tmp/etc.tar.gz /etc > /tmp/log.txt 2>&1 &  
  重定向后台执行

- tar -czf - file/dir                                   
  打包压缩到当前目录，日志输出到stdout

- tar -xzf file.tar.gz                                   
  解压到当前目录

- tar -xvf file.tar.gz -C ./dst                          
  解压到到dst目录

- test -e /dmtsai && echo "exist" || echo "not exist"    
  测试文件是否存在

- test -f /dmtsai && echo "file"  || echo "not file"      
  测试是否文件 

- test -d /dmtsai && echo "dir"   || echo "not dir"        
  测试是否目录

- wc -l filename                           
  查看文件行数   
  e.g. ps -ef | grep java | wc -l   统计 java 进程数
```



### 执行
```
- batch
  要在系统平均负载量降到 0.8 以下时执行某项一次性的任务，使用 batch 命令
  键入 batch 命令后，at> 提示就会出现。键入要执行的命令，按 [Enter] 键，然后键入 Ctrl-D；类似于at命令的操作；

- bg %3
  在背景状态下执行 3 号 job

- fg %1
  将背景任务恢复到前景 fg %jobnumber

- jobs -l
  查看背景任务

- kill -l
  查看kill 信号列表

- killall -9 java
  强制杀掉所有java进程
  e.g.: ps aux|grep 'test'|grep -v 'grep'|awk '{print $2}' | xargs kill -9

- nohup ./sleep500.sh &
  Run a command immune to hangups, with output to a non-tty

- nice -n -5 vi &
  Run a program with modified scheduling priority

- rpm -ivh                           
  安装 rpm 包

- rpm --force -ivh 
  强制安装，忽略冲突

- shutdown -h now   
  立刻关机

- shutdown -h 23:30 
  今晚23点半关机

- shutdown -h +10   
  十分钟后关机

- shutdown -r now   
  立刻重启

- sudo -u sshd touch /tmp/mysshd
  Execute a command as another user, 默认sudo以root用户执行

- write vbird1 pts/2 
  向其他用户发送消息

- wall "I will shutdown my linux server…"  
  广播消息

- xargs
  find /sbin -perm +7000 | xargs ls -l
  build and execute command lines from standard input
```



### 字符串
```
- cut -d ':' -f 2
  按冒号分割, 取分割后第二个域
  echo $PATH | cut -d ':' -f 2

- cut -c 12-
  按字符数按列切割，
  export | cut -c 12-
  export | cut -c 12-30

- grep 'word' filename
  在文件中查找 word

- grep -v 'word' filename
  查找不包含word的文档

- cat /etc/hosts|tr -d '\r' > /tmp/hosts 
  删除hosts文件中的'\r'字符，并重定向到/tmp/hosts文件
  tr: translate or delete character
```


### 配置
```
- sysctl                                        
  Configure kernel parameters at runtime，配置文件 /etc/sysctl.conf

- sysctl -w net.ipv4.tcp_tw_recycle=1                  
  开启TCP连接中TIME-WAIT sockets的快速回收

- sysctl -a                                            
   Display all values currently available.

- sysctl -w net.ipv4.ip_local_port_range=1025 65535    
  设置本地端口使用范围

- sesearch -a -t httpd_sys_content_t 
  SELinux policy query tool

- seinfo -b | grep httpd 
  查看SELinux policy和规则设定

- setenforce                          
  Modify the mode SELinux is running in
  setenforce 1/Enforcing   强制模式
  setenforce 0/Permissive  宽容模式

- sestatus 
  查看 SELinux Policy 对应配置 vi /etc/selinux/config

- chsh -l
  查看系统支持的 shell
  echo $SHELL  查看正在使用的 shell

- chsh -s /bin/csh
  修改使用的 shell 程序

- chkconfig --list | more
  列出目前系统上面所有被 chkconfig 管理的服务

- chkconfig --level 345 atd on
  让 atd 这个服务在 run level 为 3, 4, 5 时启动
  linux os 将操作环境分为以下7个等级:
  0: 开机(请不要切换到此等级)
  1: 单人使用者模式的文字界面
  2: 多人使用者模式的文字界面,不具有网络档案系统(NFS)功能
  3: 多人使用者模式的文字界面,具有网络档案系统(NFS)功能
  4: 某些发行版的 linux 使用此等级进入x windows system
  5: 某些发行版的 linux 使用此等级进入x windows system
  6: 重新启动

- ethtool eth0
  查看网卡信息

- more /etc/services
  查看 linux 服务

- more /etc/resolv.conf
  查看 dns 配置

- more /etc/sysconfig/network-scripts/ifcfg-eth0
  查看网卡配置

- modinfo cifs
  Program to show information about a Linux Kernel module

- modprobe cifs
  加载 cifs 模块

- modprobe -r cifs
  移除 cifs 模块

- mesh y/n
  Control write access to your terminal, Allow write access to your terminal, or disallow.

- renice 10 pid                      
  Alter priority of running processes

- route add default gw 10.28.171.1   
  增加默认网关

- ulimit -u  65535 
  修改单个用户允许的最大进程数
```


### 诊断
```
- free -m
  观察内存情况(单位 M)

- free -g
  观察内存情况(单位 G)

- fuser -uv /var/gdm/.gdmfifo
  找出使用该档案、目录的程序

- lsof -i TCP:8080
  查找特定端口打开的进程

- lsof -i TCP:1-1024
  查找指定端口范围的进程

- ldd $(which sshd httpd)
  library dependency discovery 依赖库寻找

- lsmod
  系统会显示出目前已经存在于核心当中的模块

- lsb_release -a
  查看 linux 发行版本

- netstat -nplt
  找出目前系统上已在监听的网络联机及其PID

- netstat -an | grep 'ESTABLISHED' | wc -l
  查看建立的连接数

- netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
  统计连接状态

- nslookup baidu.com
  查看域名对应的ip

- ps aux | grep tomcat
  查看 tomcat 进程
  USER     PID     %CPU    %MEM     VSZ      COMMAND
  USER   : 该 process 属亍那个使用者账号的?
  PID    : 该 process 的程序标识符。
  %CPU   : 该 process 使用掉的 CPU 资源百分比;
  %MEM   : 该 process 所占用的物理内存百分比;
  VSZ    : 该 process 使用掉的虚拟内存量 (Kbytes)
  RSS    : 该 process 占用的固定的内存量 (Kbytes)
  TTY    : 该 process 是在哪个终是本机上面的登入者程序,若为 pts/0 等等,则表示为由网络连接主机的程序。
  STAT   : 该程序目前的状态僵尸进程，X-死掉的进程
  START  : 该 process 启动时间;
  TIME   : 该 process 实际使用 CPU 运作的时间。
  COMMAND: 该程序的实际指令

- ps -eo lstart,etime,pid | grep pid
  查看进程启动和运行时间

- pstree 
  查看程序之间的相关性

- pwdx pid                           
  查看进程工作目录 e.g. ps -ef|awk '{print $2}'|grep -v PID | xargs pwdx

- pidof init syslogd
  Find the process ID of a running program.

- top -d 2 -p 1678 
  动态观察进程 pid=1678 每隔 2 秒刷新一次

- top -p 12453 -H 
  观察进程 12453 中线程的 cpu 占用情况

- top
  ? : 显示在 top 当中可以输入的指令
  1 : 多核 cpu 切换
  P : 以 cpu 的使用资源排序显示
  M : 以 memory 的使用资源排序显示
  N : 以 pid 来排序
  T : 由该 process 使用的 cpu 时间累积 (TIME+) 排序
  k : 给予某个 pid 一个信号 (signal)
  r : 给予某个 pid 重新制订一个 nice 值
  q : 离开 top
  
  输出结果说明:
  第一行: 总体情况
    14:00:24                       - 当前时间
    up 2 days, 23:13               - 开机以来运行时间
    8 users                        - 当前用户数
    load average: 0.01, 0.01, 0.00 - 1, 5, 15 分钟的系统平均负载
  
  第二行: 进程任务
    Tasks: 165 total, 1 running, 164 sleeping, 0 stopped, 0 zombie
  
  第三行: Cpu(s)
    0.2%us  -  用户空间占用 cpu 百分比
    0.2%sy  -  内核空间占用 cpu 百分比 
    0.0%ni  -  用户进程空间内改变过优先级的进程占用 cpu 百分比
    99.5%id -  空闲 cpu 百分比
    0.0%wa  -  等待 i/o 的 cpu 时间百分比  
    0.0%hi  -  硬中断
    0.2%si  -  软中断

  第四行: Mem
    2023568k total
    1976384k used
    47184k   free  
    126288k  buffers （用作内核缓存的内存量）

  第五行: Swap
    4063224k total
    744080k  used
    3319144k free

  PID    USER     PR     NI     VIRT     RES     SHR     S     %CPU     %MEM     TIME+    COMMAND                
   1     root     15     0     10368     592     560     S     0.0      0.0      0:01.14   init   
  3892   root     23     0     2047m     328m    10m     S     0.7      2.1      1163:00   java
  
  PID  - 进程 id
  USER - 进程所属用户     
  PR   - Priority 的简写，程序的优先执行顸序，越小越早被执行
  NI   - Nice 的简写，也是越小越早被执行; nice 值范围为 -20 ~ 19 PRI(new) = PRI(old) + nice
  VIRT - 进程使用的虚拟内存总量，默认单位kb，VIRT = SWAP + RES
  SHR  - 共享内存大小，默认单位kb
  S    - 进程状态
  TIME - CPU 使用时间的累加     

- uname -a 
  查阅系统核心相关信息 等同于 cat /proc/version   

- vmstat 5                                
  reports information about processes, memory, paging, block IO, traps, and cpu activity with 5 seconds delay.

       procs -----------memory----------  --swap--  ----io----  --system--   -----cpu------
       r b     swpd free  buff   cache      si so      bi bo     in   cs     us sy id wa st
       0 0     136  84944 141268 13801476   0  0       8  66     1    1      1  0  99 0  0
       0 0     136  83952 141276 13802656   0 0        0 380     1108 975    1  0  99 0  0

       
       procs
         r:    The number of processes waiting for run time.
         b:    The number of processes in uninterruptible sleep.
       
       memory
         swpd:   The amount of virtual memory used.
         free:   The amount of idle memory.
         buff:   The amount of memory used as buffers.
         cache:  The amount of memory used as cache.
         inapt:  The amount of inactive memory. (-a option)
         active: The amount of active memory. (-a option)

       swap
         si:     Amount of memory swapped in from disk (/s).
         so:     Amount of memory swapped to disk (/s).

       io
         bi:     Blocks received from a block device (blocks/s).
         bo:     Blocks sent to a block device (blocks/s).

       system
         in:     The number of interrupts per second, including the clock.
         cs:     The number of context switches per second.
       
       cpu
         These are percentages of total CPU time.
         us:     Time spent running non-kernel code. (user time, including nice time)
         sy:     Time spent running kernel code. (system time)
         id:     Time spent idle. Prior to Linux 2.5.41, this includes IO-wait time.
         wa:     Time spent waiting for IO. Prior to Linux 2.5.41, included in idle.
         st:     Time stolen from a virtual machine. Prior to Linux 2.6.11, unknown.
```
