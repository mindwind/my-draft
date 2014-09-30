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


