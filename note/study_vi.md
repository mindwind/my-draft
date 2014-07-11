命令模式
********
	 0               行首
	 $               行末
	 G               最后一行
	 gg              到第一行
	 ctrl + f        前翻一页
	 ctrl + b        后翻一页
	 n               重复前一个搜索动作
	 N               反向进行前一个搜索动作
	 x               Del
	 X               Backspace
	 dd              整行删除
	 ndd             n位数字，删除光标所在行下n行
	 yy              复制光标所在行
	 nyy             n为数字，复制光标所在行下n行
	 p               粘贴已复制数据在光标下一行
	 u               复原前一个动作redo
	 .               重复前一个动作
	 ctrl + v        区块选择，选中后按 y 复制，按 d 可删除选中区块
	 fx              行内搜索，向后搜索
	 Fx              行内搜索，向前搜索




底行模式
********
/word                     向下搜索关键字
?word                     向上搜索关键字
:n1,n2s/word1/word2/g     在n1和n2行之间搜索word1并用word2替换
:1,$s/word1/word2/g       全部用word2替换word1
:w                        保存
:w filename               另存
:q!                       退出不存储
:wq                       保存并退出
:set nu                   显示行号
:set nonu                 取消行号
:!command                 暂时离开vi命令模式执行os命令 e.g. :!ls /work
:sp                       多窗口分割 ctrl+w+上下箭头来切换窗口
:%s/hello/&/g             统计hello这个词的个数
:%s/^M//                  替换
:1,$d                     删除全部内容
:linenum                  跳到指定行
