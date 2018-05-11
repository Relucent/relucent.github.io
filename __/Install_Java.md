# Linux下Java安装与配置

## 一、卸载系统自带的JDK

 如果Linux已经自带OpenJdk，我们需要将它卸载掉，然后再安装需要的JDK  
 查看Linux自带的JDK是否已安装，输入如下命令查看JAVA版本信息  

	java -version

 然后输入以下命令，查看JDK信息  

	rpm -qa|grep java  

会输出（以下只是举例子，可能有多项）

	java-1.5.0-openjdk-1.5.0-1.23.1.1.1.el.x86_64
	tzdata-java-2012c-l.el6.noarch

 这时候我们可以使用yum命令卸载JDK  

	yum -y remove java-1.5.0-openjdk-1.5.0-1.23.1.1.1.el.x86_64
	yum -y remove tzdata-java-2012c-l.el6.noarch

## 二、安装JDK

1.下载我们需要的JDK。

JDK下载地址：  
http://www.oracle.com/technetwork/java/javase/downloads/index.html  
http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html  
http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html  

我下载的是  jdk-8u152-linux-x64.tar.gz  

2.创建java程序的安装目录目录

	mkdir /usr/java  


3.下载的tar.gz复制到/usr/java目录下

	cp jdk-8u152-linux-x64.tar.gz /usr/java

4.查看/usr/java目录

	cd /usr/java  
	ls -a  

5.解压文件，输入如下命令  

	tar -zxvf jdk-8u152-linux-x64.tar.gz

6.解压后，在 `/usr/java` 目录下就会生成一个新的目录 `jdk1.8.0_152`

7.配置环境变量，输入如下命令，进入配置文件

	vi /etc/profile  

查找到
	
	export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

(按a键，进入插入编辑模式) 将这行下增加三行配置信息，如下：

	export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL
	export JAVA_HOME=/usr/java/jdk1.8.0_152
	export PATH=$JAVA_HOME/bin:$PATH
	export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools/jar

修改完之后，按ESC 再输入 :wq  保存并退出VI编辑

8.为了让配置文件立刻生效，输入如下命令：

source /etc/profile 

9.然后验证JAVA是否安装成功，输入如下命令：
java -version

如果输出java版本信息，说明安装成功了，否则可能是profile的配置有错误


## 其他说明

1.如果是非root用户，如果出现类似 Permission denied 的错误提示，一般是权限不够。可以修改文件夹权限，例如：

	chmod +x  /usr/java/jdk1.8.0_152/bin/java


2.如果下载的JAVA安装包是rpm 格式的话，那么安装命令为

	rpm -ivh jdk-8u152-linux-x64.rpm  


3.Linux下*.tar.gz文件解压缩命令说明

压缩命令   
命令格式 tar  -zcvf 压缩文件名.tar.gz 被压缩文件名   
压缩文件名和被压缩文件名都可加入路径  

解压缩命令  
命令格式：tar -zxvf 压缩文件名.tar.gz
解压缩后的文件默认放在当前的目录。