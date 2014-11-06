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
```


### 配置
```
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
```
