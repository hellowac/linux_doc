- [环境变量](#环境变量)
  - [Linux系统](#linux系统)
    - [添加环境变量](#添加环境变量)
    - [删除环境变量](#删除环境变量)
  - [Linux的变量种类](#linux的变量种类)
  - [设置变量的三种方法](#设置变量的三种方法)
    - [编辑`/etc/profile`](#编辑etcprofile)
    - [编辑用户目录下`.bash_profile`](#编辑用户目录下bash_profile)
    - [运行`export`命令](#运行export命令)
  - [环境变量的查看](#环境变量的查看)
    - [使用`echo`命令](#使用echo命令)
    - [使用`env`命令](#使用env命令)
    - [使用set查看](#使用set查看)
  - [常用的环境变量](#常用的环境变量)

# 环境变量

参考: <https://zh.wikipedia.org/wiki/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F>

**环境变量**（environment variables）一般是指在操作系统中用来指定操作系统运行环境的一些参数，如：`临时文件夹位置`和`系统文件夹位置`等。

**环境变量** 是在操作系统中一个具有特定名字的对象，它包含了一个或者多个应用程序所将使用到的信息。例如`Windows`和`DOS`操作系统中的`path`环境变量，当要求系统运行一个程序而没有告诉它程序所在的完整路径时，系统除了在当前目录下面寻找此程序外，还应到`path`中指定的路径去找。用户通过设置环境变量，来更好的运行进程。

## Linux系统

`shell环境`依赖于多个文件的设置。当`shell`被调用时，它从两个初始文件读取命令。`/etc/profile`包含了**系统变量**，它由系统管理员维护，由系统管理员设置`本地系统变量`和`特殊命令`。普通用户的`启动信息文件`(`$HOME/.bash_project`)由各用户自己维护，该文件可以被修改以实现任何特定的系统初始化。

只有在特定的情况下才读取`profile`文件，确切的说是在用户登陆的时候。当运行`shell脚本`或`subshell`以后，就无须再读`profile`。虽然所有`profile`都可选的，但是基本上所有系统都有`/etc/profile`.

如果定义了变量`ENV`且已经传递到环境中，则所有的`bash shell`都要读取并调用由这个变量指定的文件所包含的命令。这个文件用来定义所有`bash shell`的特征，而不仅仅是登陆到`shell`。这个文件的典型的名字是`$HOME/.bashrc`。

当用（系统管理员）新建用户时，`.bash_profile`、`bashrc`和其他公共的环境文件模板将复制到`/etc/skel`这个目录下面。可以编辑这些初始化设置，也可以在此目录下添加附加的文件。

(常见的有`HOSTNAME`,`SHELL`,`HISTSIZE`,`PERL5LIB`,`USER`,`PATH`,`PWD`,`LANG`,`HOME`, `LD_LIBRARY_PATH`(指定动态链接库的位置so文件，一般在安装软件出错时用到)，`PYTHONPATH`（指定python安装包的路径）, `PERL5LIB`（指定perl安装包的路径）)

使用`set`命令显示所有本地定义的`Shell变量`

```bash
> set
'!'=0
'#'=0
'$'=15864
'*'=(  )
-=569JNRXZghiklms
0=/bin/zsh
'?'=0
@=(  )
ARGC=0
BG
CDPATH=''
...
```　　

使用`readonly`命令设置只读变量,变量就不可以被修改或清除

**环境变量的设置位于`/etc/profile`文件**

### 查看环境变量

```bash
> # 查看当前全部的环境变量:
> env
> # 查看特定环境变量: echo ＋$变量名
> echo $PATH 
```

### 添加环境变量

例如要将 `/home/admin/code/lib/include` 加入到环境变量 **LD_LIBRARY_PATH** 中，可以在`shell`中输入:

```bash
> # 这要写绝对路径
> export LD_LIBRARY_PATH=/home/admin/code/lib/include
```

### 删除环境变量

```bash
> unset LD_LIBRARY_PATH
> # 万一设置错了，或者更改可使用，或取消设置。
```

## Linux的变量种类

按变量的生存周期来划分，Linux变量可分为两类：

1. **永久的**：需要修改配置文件，变量永久生效。
2. **临时的**：使用`export`命令声明即可，变量在关闭shell时失效。

## 设置变量的三种方法

### 编辑`/etc/profile`

【**对所有用户生效(永久的)**】

用VI在文件/etc/profile文件中增加变量，该变量将会对Linux下所有用户有效，并且是“永久的”。

例如：编辑/etc/profile文件，添加CLASSPATH变量

```bash
\> # vi /etc/profile
export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib
```

**注**：修改文件后要想马上生效还要运行`source /etc/profile`不然只能在下次重进此用户时生效。

### 编辑用户目录下`.bash_profile`

【**对单一用户生效(永久的)**】

用`VI`在用户目录下的`.bash_profile`文件中增加变量，改变量仅会对当前用户有效，并且是 **“永久的”**。

例如：编辑`guok`用户目录(`/home/guok`)下的`.bash_profile`

`$ vi /home/guok/.bash.profile`

添加如下内容：

`export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib`

**注**：修改文件后要想马上生效还要运行 `source /home/guok/.bash_profile` 不然只能在下次重进此用户时生效。

### 运行`export`命令

【只**对当前shell(BASH)有效(临时的)**】

在`shell`的命令行下直接使用 `[export 变量名=变量值]` 定义变量

该变量只在当前的`shell(BASH)`或其`子shell(BASH)`下是有效的。

`shell`关闭了，变量也就失效了，再打开新`shell`时就没有这个变量，需要使用的话还需要重新定义。

## 环境变量的查看

### 使用`echo`命令

使用`echo`命令查看单个环境变量。例如：

```bash
> echo $PATH
```

### 使用`env`命令

使用`env`查看所有环境变量。例如

```bash
> env
```

### 使用set查看

使用`set`查看所有本地定义的环境变量。

```bash
> set
'!'=0
'#'=0
'$'=15864
'*'=(  )
-=569JNRXZghiklms
0=/bin/zsh
'?'=0
@=(  )
ARGC=0
...
```

`unset` 可以删除指定的环境变量。

## 常用的环境变量

**PATH**: 决定了shell将到哪些目录中寻找命令或程序

**HOME**: 当前用户主目录

**HISTSIZE**:　历史记录数

**LOGNAME**: 当前用户的登录名

**HOSTNAME**:　指主机的名称

**SHELL**: 当前用户Shell类型

**LANGUGE** 或 **LANG**: 语言相关的环境变量，多语言可以修改此环境变量

**MAIL**:　当前用户的邮件存放目录

**PS1**:　基本提示符，对于`root`用户是`#`，对于`普通用户`是`$`
