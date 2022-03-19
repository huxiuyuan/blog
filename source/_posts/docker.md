---
title: Docker
description: 'Docker介绍'
---

# Docker

> Docker是一个快速交付应用、运行应用的技术

项目部署的问题

大型项目组件较多，运行环境也较为复杂，部署时会遇到一些问题：

- 依赖关系复杂，容易出现兼容性问题
- 开发，测试，生产环境有差异

## Docker如何解决依赖的兼容性问题？

- Ubuntn和CentOS都是基于Liunx内核，只是系统应用不同，提供的函数库有差异

![image-20211224210226739](https://cdn.jsdelivr.net/gh/huxiuyuan/java-learn/202112242102916.png)

> - Docker将用户程序与所需要调用的系统(比如Ubuntn)函数库一起打包
> - Docker运行到不同操作系统时，直接基于打包的库函数，借助于操作系统的Linux内核来运行

Docker如何解决大型项目依赖关系复杂，不同组件依赖的兼容性问题？

- Docker允许开发中将应用、依赖、函数库、配置一起**打包**，形成可移植镜像
- Docker应用运行在容器中，使用沙箱机制，相互**隔离**

Docker如何解决开发、测试、生产环境有差异的问题？

- Docker镜像中包含完整运行环境，包括系统函数库，仅依赖系统的Linux内核，因此可以在任意Linux操作系统上运行

## Docker与虚拟机

![image-20211224211342994](https://cdn.jsdelivr.net/gh/huxiuyuan/java-learn/202112242113120.png)

Docker和虚拟机的差异：

> - docker是一个系统进程，虚拟机是在操作系统中的操作系统。
> - docker体积小、启动速度快、性能好；虚拟机体积大、启动速度慢、性能一般。

## 镜像和容器

> 镜像（image）：Docker将应用程序及其所需的依赖、函数库、环境、配置等文件打包在一起，成为镜像。
>
> 容器（Container）：镜像中的应用程序运行后形成的进程就是容器，只    是Docker会给容器做隔离，对外不可见

## Docker和DockerHub

- DockerHub：DockerHub是一个Docker镜像的托管平台。这样的平台称为Docker Registry。
- 国内也有类似于DockerHub的公开服务，比如网易云镜像服务、阿里云镜像服务

## Docker架构

- Docker是一个CS架构的程序，由两部分组成：

  1. 服务端（server）：Docker守护进程，负责处理Docker指令，管理镜像、容器等

  2. 客户端（client）：通过命令或RestAPI向Docker服务端发送指令。可以在本地或远程向服务端发送指令。

     ![image-20211224212532354](https://cdn.jsdelivr.net/gh/huxiuyuan/java-learn/202112242125466.png)

## Docker数据卷

- > 数据卷（volume）：是一个虚拟目录，指向宿主机文件系统中的某个目录

docker容器内部配置对外不可见，容器删除后配置随之删除，造成了

1. 不便于修改，要进入容器内部进行修改
2. 数据不可复用：在容器内的修改对外是不可见的。所有修改对新创建的容器不可复用
3. 升级维护困难：数据在容器内，如果要升级容器必然删除旧容器，所有数据都跟着删除了

![image-20211227150906606](https://cdn.jsdelivr.net/gh/huxiuyuan/java-learn/202112271509737.png)

- 数据卷的作用
  1. 将容器与数据分离，解耦合，方便操作容器内数据，保证数据安全

## 挂载数据卷

我们在创建容器时，可以通过 -v 参数来挂在一个数据卷到某个容器目录

![image-20211227151759434](https://cdn.jsdelivr.net/gh/huxiuyuan/java-learn/202112271517486.png)