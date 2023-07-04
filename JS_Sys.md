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

  