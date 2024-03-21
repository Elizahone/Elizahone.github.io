# hadoop

- [Java安装与配置环境变量](#Java安装与配置环境变量)
- [Hadoop安装与配置](#Hadoop安装与配置)
- [伪分布式配置](#伪分布式配置)
- 

## Java安装与配置环境变量
由于hadoop集群是用Java编写的，故想运行 **hadoop** 必须先安装 **Java** 环境， 安装方法如下：
	***方法一：***
		直接使用各自Linux发行版的包管理器安装，如 Debian 和 Ubuntu 的 **apt 或 apt-get** , ArchLinux的**pacman**，Centos 的 **yum** 。该方法较为简单，请自行查阅自己系统的安装方式。
	 ***方法二：***
		 官网自行下载Java压缩包，如果你的Linux有浏览器，可以在浏览器中直接下载。若没有，可在 Windows 中下载，然后借用 ssh 传至 Linux 虚拟机中（或实体机）具体 SSH 配置请查阅 [SSH配置](#SSH配置)
		 在Windows中打开powershell或cmd，输入如下命令：即可将文件传至Linux中的 home 目录中
```powershell
scp path/to/Java user@xxx.xxx.xxx.xxx:~/
# 例如：
scp ./jdk-11.0.2.tar.gz hadoop@192.168.16.100:~/
```
随后即可在Linux中解压安装包，并配置环境变量，命令如下：
```shell
# 首先来到压缩包所在目录 如 ~/
tar -zxvf path/to/Java.tar.gz -C path/to/Java
```
`path/to/Java.tar.gz`代表Java压缩包的路径，相对或绝对路径均可。
`-C` 后的路径是你要将压缩吧解压到的路径，可根据需要自行更改。本指南将安装到 `/opt/Java`中，因此，上方命令应 个性化 为 ： `tar -zxvf ./jdk-11.0.2_linux-x64_bin.tar.gz -C /opt/Java`

入下所示：
![[Pasted image 20240321175524.png]]

**接着配置环境变量**：
配置环境变量需要修改 home 目录下的 .bashrc 文件，某些系统可能还存在~/.bash_profile， 建议修改 `~/.bash_profile`， 如果没有，请修改 `~/.bashrc
```shell
# 来到家目录 ~
cd ~
nvim .bash_profile
# 在文件最后写下如下命令
JAVA_HOME=/opt/Java/jdk-11.0.2
export PATH=$PATH:$JAVA_HOME/bin
```
关于`JAVA_HOME` 请赋值为自己JAVA安装的路径，切忌照葫芦画瓢
输入 `java -version` 查看是否安装成功

![[Pasted image 20240321180425.png]]

## Hadoop安装与配置

根据上面提到的 Java 安装方法二，同理发送文件到Linux，下面仅给出命令， 考虑到书上将hadoop安装到`/usr/local`中，以下命令将如此实现，但本人是将 hadoop安装至 `/opt` 中。
```shell
tar -zxvf path/to/hadoop.tar.gz -C /usr/local/
# 接着进入 /usr/local/ 目录中
cd /usr/local/
# 按书中所述，改名，以便操作
chown -R usrname ./hadoop
```
`chown`的意思为`change owner`, `-R` 意味着 `recursive`递归，即将 `./hadoop`中所有文件都更改所有者权限。注意`usrname`请自行更改。
tips：如遇到不懂的命令，可以使用 `help command` 或者 `man command` 查看帮助文档

完成以上操作基本上不会出现问题，使用下方命令查看是否安装成功
```shell
# 进入hadoop安装目录
cd /usr/local/hadoop
./bin/hadoop version
```
如遇到报错`ERROR: JAVA_HOME is not set and could not be found.` 请修改`./etc/hadoop/hadoop-env.sh` 在最后加上 
```shell
export JAVA_HOME=/opt/Java//opt/Java/jdk-11.0.2
```
注意：JAVA_HOME 内容根据实际情况填写

完成上述步骤基本已经安装完成。

## 伪分布式配置
由于书中案例给的足够详细，便在此不再赘述，请见 [厦门大学提供的文档](https://dblab.xmu.edu.cn/blog/2441/)

## 分布式集群配置
。。。。。
