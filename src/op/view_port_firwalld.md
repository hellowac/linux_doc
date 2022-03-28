# firewall-cmd

linux开放指定端口命令

## 方式一

1. 开启防火墙

    `systemctl start firewalld`

2. 开放指定端口

    `firewall-cmd --zone=public --add-port=1935/tcp --permanent`

    命令含义：

    ```shell
    `--zone` #作用域
    `--add-port=1935/tcp`  #添加端口，格式为：端口/通讯协议
    `--permanent`  #永久生效，没有此参数重启后失效
    ```

3. 重启防火墙

    `firewall-cmd --reload`

4. 查看端口号

    `netstat -ntlp`   //查看当前所有tcp端口·

    `netstat -ntulp |grep 1935`   //查看所有1935端口使用情况·

## 方式二

```shell
# 开放端口:8080

/sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
```

## 方式三

```shell
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT

service iptables restart
```
