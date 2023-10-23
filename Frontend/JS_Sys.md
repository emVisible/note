# 类与模块化

面向对象本身是编程范式。

原生js通过# 

super相当于调用父类的constructor。通过super.xxx()也相当于一个实例进行函数调用

子类想调用父类的static属性，也必须继承后再调用自身对static属性

- new.target，显示当前调用者 && 继承者

- Object.getPrototypreOf
- Object.setPrototypeOf

![image-20230704162649653](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230704162649653.png)

对象创建方式

```
字面量

构造函数

Object.create()
```

对象变量作为key

```
let a = "name"
let b = "age"
const obj = {
	[a]:xxx,
	[b]:xxx
}
```

工厂模式

```
提高复用性
```

原型

> Q：为什么要有原型？
>
> A：如果没有原型，那么每一个对象在创建时都会申请一段内存地址，将其无穷化，性能开销是很大的。
>
> ​		通过原型，可以使内存开销降低

- ```
  实例化对象上，拥有__proto__原型，所以可以有这种写法：
  const person = new Person()
  console.log(person.constructor == Person) // true, 因为本质上 实例对象.__proto__ 和 构造函数.prototype是一个东西
  ```

  

![image-20230704213824923](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230704213824923.png)

- 对比工厂函数，原型 && 构造函数占用内存空间更少

  工厂函数

  - 性能开销更大
  - 内存空间更多
  - 没有提供原型
  - 无法区分构造出的对象是通过哪个工厂函数构建的

  ```
  工厂函数每次都要生成相关操作，申请更多的内存空间
    function Person(name: string, age: number, hobby: string): yPerson {
      const obj: yPerson = {
        name,
        age,
        hobby,
      };
      return obj;
    }
  ```


---

> 如何使用类语法糖将代码条理设计的更加清晰合理
>
> 1. 事前思考，分析需求及特征
> 2. 定义抽象基类，进行复用

- script标签的type=module时，是strict模式

---

# 设计模式

设计-设计原则-SOLID

- Single Responsibility Principle 单一职责
  一个类只有一个变化的原因，只负责自己的部分

- Open Closed Principle 开闭原则
  对扩展开放，对修改关闭

- Liskov Substitution Principle 里式替换原则

  子类可以替换父类

- Law of Demeter 迪米特法则 / The Least Knowledge Principle 最少知识原则
  一个对象尽可能孤立

- Interface Segregation Principle 接口隔离原则
  多个特定的客户端接口好过一个通用性总接口

- Dependence inversich Principle 依赖倒置原则]
  上层模块和细节依]]

```
一个类只做一件事
	类中只有类本身需要的属性与方法进行私有化。内部尽量少修改，对外开放。
子类能够代替父类的功能，达到相同的结果
组件、父子组件、父子函数之间玩，只跟直接相关的、类、组件、函数使用

```

vue-eventBus

- 总线模式

  ```
  $bus = new Vue()
  $bus.on() // 添加   相当于先长时间诱惑触发和实战
  $bus.emit("EventName", fn) // 触发
  ```


同步与异步

在js中是一种消息通知机制

- 同步与异步，针对的是任务

- 阻塞与非阻塞，针对的是事件循环调用栈

  ```
  这个说的是错的，同步就是等待程序调用结果，阻塞时会释放cpu和资源。
  
  同步非阻塞就是会等待结果但是线程不会被挂起，会继续占用资源。
  
  同步阻塞就是等待结果的时候，线程被挂起了，资源和cpu别释放了，等待信号唤醒
  
  异步就是发送方执行很多调用，不关心结果。
  
  处理方如果等待处理结果不去执行其他东西，异步阻塞
  
  处理方如果也不等待，就行执行其他的程序，就是异步非阻塞
  ```

```
Step1 回调
	回调地狱 函数作为参数嵌套；可读性差；可维护性差； 下层
```

```
#headerShow{
	min-width:none;
	min-height:none;
	
}
```

