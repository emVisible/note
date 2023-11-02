# Docker Desktop简介

---

Docker Desktop在windows中基于Hyper-V（windows）或HyperKit（Mac）并结合 Linux，以此为基础安装并运行Docker daemon。

Docker Desktop基于Hyper-V技术，是Docker Engine的超集。

除此之外，安装完Docker Desktop后，我们可以使用Docker相关CLI命令同docker进行交互，比如 docker version等，它们的实现机制并非是传统的IPC（Inter-Processing Communication）通信，而是之前文章中提到的REST API进行通信，利用的是Docker中的network机制。这里补充一些相关知识。

### 进程间通信  (IPC)

IPC指的是进程间通信，通常是在操作系统、软件中的进程之间实现数据交换，数据共享等机制。

IPC允许一台主机间不同的进程进行数据通信，它们可以是同一个程序内，也可以是不同的程序内。

### Hyper-V

Hyper-V是微软公司开发的一种基于硬件的虚拟化技术，它可以在物理计算机上创建和管理虚拟化的计算环境。

Hyper-V 在企业环境中被广泛用于服务器虚拟化，用于创建虚拟服务器和构建私有云基础架构。它还可以用于开发和测试环境中，以及构建虚拟化的开发和测试平台。Hyper-V 作为Windows操作系统的一部分，为企业提供了一种高性能、高可用性和可扩展性的虚拟化解决方案。

Hyper-V 核心功能如下：

1. 虚拟化：它允许用户在一台物理服务器上创建多个虚拟机，每个虚拟机都可以运行独立的操作系统和应用程序。
2. 管理工具：它提供了一系列管理工具，用于配置、监控和管理虚拟机，包括远程管理、动态迁移和自动化的管理功能。
3. 高可用性：通过故障转移集群（Failover Cluster）和动态内存（Dynamic Memory）等功能，提供了虚拟机的高可用性和灵活性。
4. 安全性：通过虚拟机和主机的隔离，可以帮助提高系统的安全性，并保护每个虚拟机上的数据和应用程序。
5. 兼容性：它支持多种操作系统，包括不同版本的Windows、Linux和其他常见操作系统，使其成为跨平台虚拟化解决方案的理想选择。

### 文件挂载

我们期望的效果是迅速且高效，那么文件挂载自然是直接挂载到宿主操作系统最为合宜。如果只从Docker内置的虚拟Linux中挂载，显然不是我们想要的。

Docker Desktop对于一整套流程进行了实现，我们只需要指定宿主机挂载目录即可：

```
	原生OS系统 => 虚拟Linux系统 => 容器

C:\\xxx\xxx  => /c/xxx/xxx => /volume/c/xxx
```

---

### Docker Desktop配置

右键小鲸鱼=>settings，进入配置。

相对重要的配置为Resources和Docker Engine两个方面

在Resources中，可以配置挂载位置、代理地址、资源占用、网络、WS(Windows Subsystem for Linux)集成

在Docker Engine中，可以配置镜像源、镜像仓库、Go Builder等信息；其对应的文件就是daemon.json，也就是Docker deamon的配置。

### 版本问题

上文提到，Docker基于WIndows的Hyper-V或Mac的HyperKit，而这两个虚拟化工具是在分别其较高版本推出的，也就不难理解为什么需要高版本支持。

针对较低版本使用Docker，官方推荐Docker Toolbox。Docker Toolbox是基于Oracle的virtualbox并加以封装，实质上是创建了一个虚拟的Linux系统，效果和Hyper-V / HyperKit本质上是一样的。而我们知道，Virtualbox同Docker是有兼容性问题的，不能较好的实现自动化操作。Docker为我们提供了Docker QuickStart Terminal，并且必须由它来操作Docker，而不能通过OS自带的Terminal来操作。

除此之外，文件系统的挂载也从半自动降级为手动。因为Docker Toolbox无法直接对virtualbox操作，所以我们需要手动在virtualbox的settings中进行挂载。



