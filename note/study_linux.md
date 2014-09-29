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
