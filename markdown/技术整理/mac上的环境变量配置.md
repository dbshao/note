1.打开终端,输入： cd ~

会进入~文件夹

2.然后输入：touch .bash_profile

回车执行后，

2.再输入：open -e .bash_profile

会在TextEdit中打开这个文件（如果以前没有配置过环境变量，那么这应该是一个空白文档）。如果有内容，请在结束符前输入，如果没有内容，请直接输入如下语句：

export PATH=${PATH}:/usr/local/mysql/bin

然后，保存，退出TextEdit（一定是退出），关闭终端并退出。
