# Docker 单机版安装步骤

安装环境：CentOS7.3   
Docker版本：17.0.3 

1. 使用root权限登录系统  

2. 下载并上传安装包  

	libcgroup-0.41-13.el7.x86_64.rpm 
	setools-libs-3.3.8-1.1.el7.x86_64.rpm    
	checkpolicy-2.5-4.el7.x86_64.rpm  
	libtool-ltdl-2.4.2-22.el7_3.x86_64.rpm  
	audit-libs-python-2.7.6-3.el7.x86_64.rpm   
	python-IPy-0.75-6.el7.noarch.rpm   
	libsemanage-python-2.5-8.el7.x86_64.rpm   
	policycoreutils-python-2.5-17.1.el7.x86_64.rpm   
	docker-ce-selinux-17.03.1.ce-1.el7.centos.noarch.rpm   
	docker-ce-17.03.1.ce-1.el7.centos.x86_64.rpm  


3. 执行安装命令  

```
	yum install -y libcgroup-0.41-13.el7.x86_64.rpm setools-libs-3.3.8-1.1.el7.x86_64.rpm  checkpolicy-2.5-4.el7.x86_64.rpm  libtool-ltdl-2.4.2-22.el7_3.x86_64.rpm audit-libs-python-2.7.6-3.el7.x86_64.rpm python-IPy-0.75-6.el7.noarch.rpm libsemanage-python-2.5-8.el7.x86_64.rpm  policycoreutils-python-2.5-17.1.el7.x86_64.rpm docker-ce-selinux-17.03.1.ce-1.el7.centos.noarch.rpm docker-ce-17.03.1.ce-1.el7.centos.x86_64.rpm
```


4. 验证

```
docker -v
```

5. 启动docker

		systemctl start docker.service

6. 验证docker已经正常安装

		docker run hello-world

7. 配置docker开机自启动

		systemctl enable docker.service

卸载 
---

1. 列出安装的软件包

		yum list installed | grep docker

2. 移除软件包

		yum -y remove docker-engine.x86_64

上面的命令不会删除镜像、容器，卷组和用户自配置文件。

3. 删除所有镜像、容器和组

		rm -rf /var/lib/docker