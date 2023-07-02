## JS高级

## V8引擎

- 搜索栏中输入网址发生的过程

  ```
  DNS解析 => 服务器IP地址 => 浏览器内核解析——V8引擎=> 以html为入口，遇到link则下载css文件，遇到script则下载js文件
  ```

  - 浏览器内核也称为**排版引擎（layout engine）、浏览器引擎（Browser engine）、页面渲染引擎（rendering engine）**

    ```
    layout engine
    		·浏览器内核有哪些？
    			Gecko								（早期被网景和火狐使用）
    			Trident								（微软开发，IE4-IE11使用；目前的Edge已经转向Blink）
    			Webkit（小程序架构）					（苹果基于KHTML开发，开源，用于Safari，谷歌之前也有用）
    				WebCore：负责解析、布局、渲染
    				JsCore：解析、执行JS代码
    			Blink								（Webkit的分支，谷歌开发，用于Chrome、Edge、Opera等）
    ```

  - JavaScript引擎

    ```
    js engine
    		·为什么需要js引擎？
    			js最后是被CPU执行，而js引擎就是作为桥梁
    		·Js引擎有哪些？
    			Spider Monkey		（Brendan Eich开发）
    			Chakra 				（微软，IE引擎）
    			JavaScriptCore		（苹果开发，也是小程序引擎）
    			V8					（谷歌开发）
    ```

    - V8引擎

      ```
      · C++编写、高性能
      · 可解析js、WebAssembly
      · 用于Chrome、Node
      · 多环境可运行（Win7、Mac10+、x64、IA-32、ARM、MIPS的Linux）
      · 可嵌入到任何C++程序
      ```

      ![image-20230607200741009](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230607200741009.png)

      ![image-20230607201136697](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230607201136697.png)

      ![image-20230607202013853](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230607202013853.png)

      ![image-20230607202241254](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230607202241254.png)

- 浏览器渲染页面的流程

  ```
  涉及到的概念：
  	1、HTML Parser
  	2、CSS Parser
  	3、DOM Tree
  	4、Style Rules
  	5、Attachment => Render Tree
  ```

  ![image-20230607191714739](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230607191714739.png)

## 内存管理

- 代码运行过程中需要内存分配。某些编程语言自动分配，某些手动分配。 

  ```
  手动管理内存分配，需要大量的内存管理操作
  	费时费力
  	要求高，易产生内存泄露
  ```

  

- 磁盘读取=>内存=>CPU执行

- 内存管理生命周期

  ```
  申请
  使用
  释放
  ```

- JS的垃圾回收机制（Garbage Collection, GC)

  ```
  对于不再使用的对象，js引擎会进行垃圾回收
  ```

  - 常见的GC算法

    - 引用计数

      ```
      当引用计数为0时，触发垃圾回收
      
      var obj = {name:"young"}				=>retain:3
      var obj2 = {name:"a",friend:obj}
      var obj3 = {name:"b",friend:obj}
      
      问题：产生循环引用，产生内存泄露
      var obj1 = {friend:obj2}
      var obj2 = {friend:obj1}
      ```

    - 标记清除

      ![image-20230608163117002](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230608163117002.png)

## 闭包

定义

- 函数和方法一把是一个东西。

  ```
  对象内部的函数称之为方法
  独立的函数称之为函数
  ```

- 在**词法解析**时，闭包就已经被确定。闭包只跟定义有关，跟调用无关

- 闭包又称为词法闭包 (lexical closure ) || 函数闭包(function closure)
  一个函数和对其周围状态（Lexical Environment）的引用捆绑在一起，这样的组合就是闭包

- 也就是说，闭包让你可以在一个内层函数中访问到外层函数的作用域

- 在js中，每当创建一个函数，闭包就会在函数创建是同时被创建出来

- 头等函数编程语言：函数是第一公民的编程语言

- 在js中，闭包是一个对象，存储两个东西 => 相当于符号的查找表

  - 函数
  - 关联的环境

- 闭包的自由变量在被捕捉时会被确定，即时脱离了捕捉的上下文它也照样可以运行

- 闭包的概念来自于Scheme（最早实现闭包的编程语言）

- 在js中

  ```
  广义上来讲，函数都是闭包
  狭义上来讲（更严格的角度上来讲)，函数访问了外部变量(有访问），它是一个闭包
  ```

内存泄露

- chrome中查看内存

  ```
  性能（performance）=> 勾选内存 => con+e 录制
  ```

  ![image-20230622091627817](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230622091627817.png)

- 内存泄露就是闭包导致部分内存无法被JS引擎进行GC解决方法就是将变量设置为null。

  ![image-20230611212726626](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230611212726626.png)

- V8引擎对其未用到的变量进行内存释放（优化）

## this

```
|-Section1
	|- VO对象
	|- 父级作用域
	|- this（动态）
|-Section2
	|- execute code body
```

