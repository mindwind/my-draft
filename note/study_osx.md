## 命令
重定向端口 80 -> 8080
sudo ipfw add 100 fwd 127.0.0.1,8080 tcp from any to any 80 in

查看监听端口
sudo lsof -i -P| grep -i "listen"


## 配置
JDK HOME 路径
/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home

开启 vim 语法颜色
  1. cp /usr/share/vim/vimrc ~mindwind/.vimrc
     将vim的环境文件copy 到自己常用用户的主目录下比如你的用户叫 mindwind
  2. sudo chmod 777 .vimrc
     修改.vimrc文件归读写属性
  3. syntax on
     在.vimrc文件最后加上

命令别名（在用户目录下建立.bash_profile 并添加别名）
  1. alias ls="ls -G"
  2. alias ll="ls -l"

Terminal 命令颜色
export CLICOLOR=1
export LSCOLORS=Exfxcxdxbxegedabagacad
export GREP_OPTIONS='--color=auto'
export TERM="xterm-color"
PS1='\[\e[0;33m\]\u\[\e[0m\]@\[\e[0;32m\]\h\[\e[0m\]:\[\e[0;34m\]\w\[\e[0m\]\$ '
添加到 ~/.bash_profile 中
