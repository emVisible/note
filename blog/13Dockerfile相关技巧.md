# 13Dockerfile相关技巧

---

Dockerfile文件，本质上是一种configure文件。而在虚拟化这个应用背景下，configure更加侧重于对config的灵活调整以满足简洁高效的配置迁移。

下面介绍一些在Dockerfile中常用的指令，很多代码构建的核心概念基本相通，只是换了层皮。

## 

## 变量使用

结合Dockerfile往往以单文件的形式存在，设置变量的效果类似于全局变量这种概念，但并不相同。

我们主要介绍ARG和ENV两个命令

- ARG 只声明不赋值，值通过CMD指令传递
- ENV 声明并赋值，值通过语法Dockerfile指定

优先级

- ENV优先级永远大于ARG。其背后定义变量的原理都是通过$+变量名来进行声明。

使用频率

- ENV > ARG

### ARG

用于声明一个变量，变量只声明不赋值。

```
ARG <variable-name>
...
```

通过Dockerfile构建镜像，并通过--build-arg向配置文件宏定义的变量传入参数。每次传递一个参数都需要重复一次指令。

```
docker build --build-arg <variable-name1>=<variable-value1> 
			 --build-arg <variable-name2>=<variable-value2> 
			 ...
```

### ENV

用于声明一个变量并对其指定初始值。

其语法类似于C中的宏定义。

```
ENV <variable-name> <varibale-value>
```

## 命令合并 (RUN)

我们知道，Docker镜像是通过多层镜像层叠加组成的。

在Dockerfile中，我们经常看到的是

```
RUN xxxxx \
	xxxxxxxxxxxx\
	xxxxxxxx\
	xx\
	...
```

而不是

```
RUN xxxx
RUN xxxxxxxxxxxx
RUN xxxxxx
RUN xx
```

即便它们最后实现的效果是相同的，但就像i++和i+=1在底层实现不同一样，它们的运行效率是截然不同的。具体来说，在后者的运行过程中，Docker会根据上一条指令结果启动一个容器并在容器中运行内容，运行结果打包为镜像层并传递到下一条指令中；我们可以同Linux的管道符类比，上一个输出是下一个输入。

既然如此，那么上述后者的运行模式来说，优点是对程序员的心智负担相对更小，但在运行上会创建总共4个镜像层并分别拿取上一层的结果-运行指令-传递给下一层。

而第一种模式使用更为普遍，实际上也就很好理解了，它的命令只有一条，启动负担更小，效率更高。

这可以类比多种语言中文件的读写，前者就是Open-WriteAll-Close，后者就是Open-Write-Close循环。与文件读写不同的是，Dockerfile的configure本身职责单一，不需要考虑其它特殊情况，所以实际使用上我们使用单条换行的形式更多。



