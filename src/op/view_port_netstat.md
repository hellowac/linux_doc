# netstat

更多参考: <https://www.yiibai.com/linux/netstat.html>

`netstat -tunlp` 用于显示 `tcp`，`udp` 的端口和进程等相关情况。

`netstat` 查看端口占用语法格式：

```shell
netstat -tunlp | grep 端口号
```

- `-t` (tcp) 仅显示tcp相关选项
- `-u` (udp)仅显示udp相关选项
- `-n` 拒绝显示别名，能显示数字的全部转化为数字
- `-l` 仅列出在Listen(监听)的服务状态
- `-p` 显示建立相关链接的程序名

例如查看 `8000` 端口的情况，使用以下命令：

```shell
# netstat -tunlp | grep 8000
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      26993/nodejs   
```

更多命令：

```python
netstat -ntlp   // 查看当前所有tcp端口
netstat -ntulp | grep 80   // 查看所有80端口使用情况
netstat -ntulp | grep 3306   // 查看所有3306端口使用情况
```
