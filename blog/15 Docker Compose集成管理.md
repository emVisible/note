#  Docker Compose集成管理

---

我们知道，Docker推崇容器即服务，一个容器对应一个服务。而一个真正的应用程序需要多种服务共同组成，可以类比为一辆汽车需要多个核心部件组成。

而在软件开发的微服务化等趋势下，这就导致了通过Docker实现一个应用的服务需要比较多的容器。好比公司人多起来就需要进行部门管理一样，Docker的容器与容器之间的通讯、联络也随着容器数量规模的增大而复杂。

Docker Compose是Docker官方维护的独立软件，由Python编写，不隶属于Docker Engine中。Docker Compose就相当于一个主管(Director)的角色，对多个容器进行统一管理。

## 不同操作系统中的安装与使用

在Windows和Mac中，Docker Compose集成到了其专用的Docker软件中，通过docker-compose指令便可使用。

而在Linux中，我们需要手动安装。

```
方式1 通过curl安装
$ curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ chmod +x /usr/local/bin/docker-compose
```

```
方式2 通过pip安装
pip install docker-compose

* pip是Python的包管理工具
```

具体的使用需要三个步骤

1. 编写Dockerfile
2. 编写docker-compose.yml
3. 通过docker-compose 启动



## YMAL语法

在介绍docker-compose配置文件之前，我们先介绍一下YMAL基本语法。

YAML（YAML Ain't Markup Language）是一种针对数据序列化的格式，经常用来存储配置文件、传输数据、或者用于与编程语言交互。它的设计目标是让人类能够很容易地阅读和理解，同时也能被计算机很容易地解析和生成。

如果你对英文名感到疑惑，其实命名是为了强调这种语言以数据做为中心，而不是以标记语言为重点，而用反向缩略语重命名。

### 注释：以井号（#）开头的行表示注释，YAML会忽略这些行。

```
yamlCopy code
# 这是注释
```

### 键值对：使用冒号（:）来表示键值对。

```
yamlCopy code
key: value
```

### 列表：以短横线（-）开头，表示一个列表项。

```
yamlCopy code- item1
- item2
- item3
```

### 嵌套结构：可以嵌套使用键值对和列表。

```
yamlCopy codeparent:
  child1: value1
  child2:
    - item1
    - item2
```

### 多行文本：使用竖线（|）可以表示多行文本块，类似于使用换行符的字符串。也可以使用大于号（>）表示折叠的文本块，会将换行符转换为空格。

```
yamlCopy codedescription: |
  This is a multi-line
  description.
```

### 引用：可以使用&符号表示一个锚点（标签），使用*符号表示引用一个锚点。

```
yamlCopy codedefaults: &defaults
  key: value

specific: *defaults
```

## 配置

默认情况下，Docker Compose项目的默认配置名就是docker-compose.yml。

```
version:...
service:
	service1:
		...
	service2:
		...
	...
volumes:...
```

其中最为重要的是service，其表示服务集群配置。service下可以对服务进行水平扩展，对服务进行详细配置；也可以对其进行垂直扩展，增加其它服务。

## 启停

启动操作。默认会在当前文件夹内查找.yml文件作为配置文件，并结合当前目录名作为默认项目名。

```
$ docker-compose up 
```

```
$ docker-compose -f ./xxx/xxx.yml -p xxx up -d 
* -p定义项目名
  -f指定Docker Compose文件
  -d是detach的意思，前文中有所提及，指定服务运行于后台
```

停止操作。运行docker-compose down后会停止并删除所有容器以及相关配置。

```
$ docker-compose down
```

结合Docker的快速响应特性，使用Docker Compose我们可以在多套开发环境中进行快速切换和统一调度。

## 拉取

```
$ docker-compose pull xxx
```

## 其它指令

查看容器主进程的输出

```
$ docker-compose logs <定义的服务名称>
```

单独控制服务

```
$ docker-compose create/start/stop <定义的服务名称> 对单独服务进行创建 && 启动 && 停止
```

