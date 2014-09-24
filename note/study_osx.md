## 命令
```
重定向端口 80 -> 8080                                                     
sudo ipfw add 100 fwd 127.0.0.1,8080 tcp from any to any 80 in


查看监听端口
sudo lsof -i -P| grep -i "listen"
```

## 配置
```
jdk home 路径
/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home


开启 vim 语法颜色
1. 将vim的环境文件copy 到自己常用用户的主目录下比如你的用户叫 mindwind
   cp /usr/share/vim/vimrc ~mindwind/.vimrc 

2. 修改.vimrc文件归读写属性
   sudo chmod 777 .vimrc

3. 在.vimrc文件最后加上 
   syntax on


命令别名
1. 在用户目录下建立.bash_profile，添加别名
   alias ls="ls -G"
   alias ll="ls -l"
```
