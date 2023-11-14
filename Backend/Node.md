# Node

---

> 阅读死月文章的知识记录

## 事件循环与异步IO

Js本身在V8的Browser runtime中有一套事件循环并发模型，而Node的事件循环机制由自己实现。

### libuv

libuv是跨平台的异步IO库，是Node事件循环的底层实现。

libuv 提供了事件循环、异步 I/O、定时器等功能，使 Node.js 能够在不同的操作系统上实现高性能的异步非阻塞操作。

### 事件循环与异步IO

事件循环是一个死循环，在循环中不断处理事件；而异步IO是事件循环的一种，是包含与被包含的关系；另外的方法还有任务调度等。

在事件循环中，整个过程可以看为一条直线，大部分时间阻塞在等待事件；而等待的过程中并不消耗CPU资源，而是等待底层的epoll得到事件，一旦有事件完成，就会通知epoll，进入下一步。libuv会一路调用到Js层，调用Js的callback。

```
fs.readFile(filename, (err, content) => {
  // 这里就是 callback
});
```

### tick

在Node的事件循环中，除了第一次启动由Node自身完成，其余都是通过kernel的epoll或者libuv的定时器等事件来触发执行。只有在触发后事件循环才会去处相应逻辑。其它的时间都阻塞在epoll的等待上。每次的触发称之为一个tick。

```
fs.readFile(filename, (err, content) => {
  fs.writeFile(filename, content, err => {
    // ...
  });

  setTimeout(() => {
    // ...
  }, 1000);
});
```

代码的执行过程如下，每一个圆都是一个tick。

![image-20231114103354754](C:\Users\16193\Desktop\note\_gallery\eventloop1.png)

### uv_async_t

在libuv中实现的用于线程安全地跨线程通信或在异步I/O完成后通知事件循环等场景。在Node中就是一个线程完成了一个任务后，通过uv_async_t通知主事件循环，也就是在下一个tick中主事件循环收到通知。

在vm模块中，使用了uv_async_t实现了对主事件循环本身的监视。vm在主事件循环中执行代码，而想要监视主事件循环，需要独立的线程管理，用于定时器超时时终止其运行。

```
在一个tick中，包含主线程和watchdog线程两个线程。

tick开始时会同时创建watch dogtimer、 watch dog event loop和主事件循环。主事件循环包括了Js死循环和watch dog解析。
    watch dog timer在创建时启动，创建意味着tick开始。
    watch dog timer到期意味着前半部分已经结束，tick进入了后半部分。
    此时后半部分会解析watch dog并通过uv_async_t通知给watch dog event loop使其自我结束线程，主事件循环会等待线程结束的通知。
    (为了线程安全，主循环也必须等待，不能直接kill掉watch dog线程)
	通知到来后，后半部分也就结束，整个tick结束。
```



## 引申知识

### 概念

#### 文件描述符

文件描述符（File Descriptor）是一种用于标识和访问已打开文件的抽象概念。文件描述符是一个非负整数，它是进程中打开文件的索引或句柄。每个进程在其打开的文件、套接字、管道等资源上都有一个唯一的文件描述符。

1. **非负整数**：文件描述符是一个非负整数。通常，0、1和2分别代表标准输入、标准输出和标准错误。
2. **进程级别**：文件描述符是进程级别的，每个进程都有独立的文件描述符表。这意味着一个进程可以打开相同的文件，但它们的文件描述符是不同的。
3. **通过系统调用进行创建和操作**：文件描述符是通过系统调用（如`open`、`socket`、`pipe`等）返回的。系统调用返回的文件描述符可以用于读取、写入、关闭等文件操作。
4. **标准文件描述符**：在UNIX系统中，通常有三个标准文件描述符：
   - 0（`STDIN_FILENO`）：标准输入
   - 1（`STDOUT_FILENO`）：标准输出
   - 2（`STDERR_FILENO`）：标准错误
5. **套接字和管道**：文件描述符不仅用于表示打开的文件，还用于表示套接字、管道等I/O资源。这使得在UNIX系统中，文件描述符成为一种通用的I/O抽象。

####  I/O 多路复用

在不同系统上的多路复用：Linux epoll, Mac kqueue, windows IOCP（网络请求: c-ares）

1. **平台差异**：`epoll`是Linux特有的，而`kqueue`是BSD系列系统中的特有机制。`IOCP`则是Windows特有的异步I/O机制。
2. **事件驱动模型**：`epoll`和`kqueue`都采用事件驱动的模型，而`IOCP`则是Windows的异步I/O机制，使用完成端口（Completion Port）来管理异步操作的完成。
3. **接口和用法**：由于是在不同的操作系统上实现，它们的接口和用法有所不同。程序需要根据目标操作系统选择相应的机制。

#### POSIX规范

POSIX（Portable Operating System Interface）规范用于定义操作系统接口相关规范。

### API

#### vm

vm(Virtual Machine)，提供代码运行的沙盒隔离环境，使得代码能在指定context中运行，不会影响到主程序的状态。

```
vm.createContext([sandbox])：
用于创建一个新的上下文对象，可选参数 sandbox 是一个对象，将在新的上下文中成为全局对象。

vm.runInContext(code, contextifiedSandbox[, options])：
在指定的上下文中执行 JavaScript 代码。
code 是要执行的 JavaScript 代码。
contextifiedSandbox 是一个通过 vm.createContext 创建的上下文对象。
options 是一个可选的选项对象，可以包括 filename（指定文件名）和 lineOffset（指定代码的行偏移量）等属性。

vm.runInNewContext(code[, sandbox][, options])：
在一个新的上下文中执行 JavaScript 代码。
code 是要执行的 JavaScript 代码。
sandbox 是一个可选的对象，将在新的上下文中成为全局对象。
options 是一个可选的选项对象，可以包括 filename（指定文件名）和 lineOffset（指定代码的行偏移量）等属性。

vm.runInThisContext(code[, options])：
在当前上下文中执行 JavaScript 代码。
code 是要执行的 JavaScript 代码。
options 是一个可选的选项对象，可以包括 filename（指定文件名）和 lineOffset（指定代码的行偏移量）等属性。
```

