- [常见环境变量](#常见环境变量)
  - [Linux](#linux)

# 常见环境变量

## Linux

1. `HOME` 用户家目录
2. `MAIL` 邮件保存路径
3. `LANG` 系统语言、语系名称
4. `RANDOM` 生成一个随机数字
5. `PS1` Bash解释器的提示符
6. `PATH` 定义解释器搜索用户执行命令的路径
7. `EDITOR` 用户默认的文本编辑器
8. `LD_LIBRARY_PATH` 库默认加载路径
9. `C_INCLUDE_PATH` gcc默认的include目录
10. `CPLUS_INCLUDE_PATH` g++默认的include目录
11. `LD_LIBRARY_PATH` 指定动态链接库的位置so文件，一般在安装软件出错时用到
12. `PYTHONPATH` 指定python安装包的路径
13. `PERL5LIB` 指定perl安装包的路径
14. `MACHTYPE` 用来显示主机类型的GNU标识。一般是主机架构-公司-系统-gnu。
15. `PWD` 记录当前目录
16. `OLDPWD` 记录之前的目录。
17. `HOSTTYPE` 用来显示主机的架构，是i386、i686、还是x86、x64等。
18. `HOSTNAME` 用来显示主机名
19. `HISTFILE` 记录history命令记录文件的位置。运行history命令将打印已经运行过的命令列表，即便重启机器后还可以保存以前的命令记录。因为执行过的命令会记录在`/root/.bash_history`文件中。可以执行 `cat /root/.bash_history` 查看以前执行过的命令。
20. `HISTSIZE` 实际上linux并不会针对每次运行命令后就立即将命令记录写入HISTFILE对应的文件中去，而是通过命令缓冲区来记录所有已经运行过的命令，只有在缓冲区满了或者退出Shell时才将缓冲区记录写入HISTFILE对于的文件中。而缓冲区的大小需要通过HISTSIZE去定义。
21. `HISTFILESIZE` 用来设置HISTFILESIZE文件记录命令的行数。这样可以限制.bash_history文件大小，避免出现文件过大的情况，不好处理。
22. `HISTCMD` 记录下一条命令在history命令中的编号。
23. `FUNCNAME` 在用户函数体内部，记录当前函数体的函数名。
24. `EUID` 记录当前用户的UID。root用户值为0。
25. `BASH_VERSION` Bash Shell的版本号
26. `BASH` Bash Shell的全路径
