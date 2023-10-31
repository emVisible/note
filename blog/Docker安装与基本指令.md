# Docker运行环境与基本指令

---

由于Docker使用了大量Linux相关指令，其对Linux操作系统的支持度更高。

## 基本概念

### 系列

社区版( Community Edition )

- 针对开发者和小型团队
- 拥有基础功能

企业版( Enterprise Edition )

- 针对中大型项目
- 额外添加了插件、安全、容器 && 镜像等管理

稳定版 (Stable release)

预览版(Edge release)

版本号命名：根据发行日期

- 主要版本：xx.xx
- 次要版本：xx.xx.xx

### 环境依赖

![image-20231030150519835](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20231030150519835.png)

windows下

- 安装Docker Desktop
- 必须使用 Windows 10 Pro ( 专业版 )
- 必须使用 64 bit 版本的 Windows

Mac下

- 安装Docker for Mac
- Mac 硬件必须为 2010 年以后的型号
- 必须使用 macOS El Capitan 10.11 及以后的版本

其它

- virtualbox同docker有兼容性问题，安装docker需要卸载掉virtualbox
- 鲸鱼图标闪动表示其在进行环境配置和初始化，不再闪动后进入pending状态
- 

## 基本操作

### 启动

Linux下

```
直接启动Docker服务，不需要启动对应的dockerd程序
sudo systemctl start docker 
```

```
设置开机启动
sudo systemctl enable docker
```

Windows下

```
打开 Docker Desktop，将自动启动docker服务
```



### 配置镜像源

```
docker官方提供的国内镜像源
registry.docker-cn.com

配置daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```



### 命令

```
查看版本
docker version

查看详细信息
docker info

查看本地镜像
docker images

查看运行中的容器
docker ps -a

列出所有网络
docker network ls

列出所有数据卷
docker volume ls

========================================

运行docker容器
docker run <image_name>

停止运行中的容器
docker stop <container_ID>

========================================

构建docker镜像
docker build -t <images_name> <path>
```

