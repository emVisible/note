# Dockerfile及其使用

---

如果说启动一个容器好比盖了一层楼，那么Dockerfile的作用就相当于指导盖楼的蓝图。

在完整的测试，开发，部署的流程中，开发人员对环境搭配更为熟悉。而测试和运维往往需要根据开发人员提供的手册进行后续操作。

Dockerfile就好比指导Docker的手册，使其自动完成我们预先描述好的命令。

## 组成

Dockerfile由注释行和指令行组成，注释行通过#来标记

Dockerfile的指令分为五类

- 基础指令。用于镜像定义和基础操作
- 控制指令。用于镜像构建和过程描述。
- 引入指令。用于镜像内文件引入
- 执行指令。用于容器启动时执行的指令
- 配置指令。用于镜像和容器的相关配置

## 优点

Dockerfile同容器修改 && 镜像迁移相比

-  体积小
- 直观清晰的逻辑
- 更容易实现自动化部署
- 修改操作更加便捷

## 常见指令

### FROM

```
通过FROM指令指定基础镜像。基础镜像FROM在第一行。
FROM <image-name> [AS name]
FROM <image-name>[:tag] [AS name]
FROM <image-name>[@<digest>] [AS name]

当FROM指令多次出现，后续出现的指令都会合并到第一次引入的镜像中。
```

### RUN

```
向控制台发送命令。可以理解为RUN语句块内输入的命令就是向控制台内输入和执行的命令
命令语句以;作为结束标识，行末尾以\为结尾代表着换行
RUN <command>
RUN ["executable", "param1", "param2"]
```

### ENTRYPOINT && CMD

```
定义主进程启动命令。基于镜像的容器，在启动时会有PID为1的主程序。
ENTRYPOINT ["executable", "param1", "param2"]
ENTRYPOINT command param1 param2

CMD ["executable","param1","param2"]
CMD ["param1","param2"]
CMD command param1 param2
```

```
ENTRYPOINT主要针对对容器的初始化和参数声明，CMD用于真正定义主程序启动命令
在优先级上，ENTRYPOINT > CMD
```



### EXPOSE

```
暴露镜像网络端口。与容器创建时暴露端口不同，通过 EXPOSE 指令就可以为镜像指定要暴露的端口。
EXPOSE <port>/<protocol>

由通过expose暴露的镜像构建的容器，其也可通过--link被其它容器所链接
```

### VOLUME

```
指定基于此镜像的容器创建时自动建立数据卷。容器创建时需要-v指定数据卷，容易出现遗漏的问题。
VOLUME["/data"]
定义的目录在创建容器时会自动创建数据卷，不需要单独-v指定
```

### COPY && ADD

```
从宿主机的FS中导文件到镜像的FS中。
COPY [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] <src>... <dest>

COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]

两种方式使用格式相同。ADD 能够支持使用网络端的 URL 地址作为 src 源，并且在源文件被识别为压缩包时，自动进行解压，而 COPY 没有这两个能力。
```

## 构建

```
docker build -t xxx -f ./xxx/xxx.Dockerfile ./xxx
-t命名镜像名称
-f指定Dockerfile路径
最后的目录参数是指定构建的环境目录，后续操作继续这个目录进行
```

