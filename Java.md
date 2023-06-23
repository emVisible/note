

## 技巧

```
psvm： idea中快速生成main方法
con+shift+回车：自动生成回车
sout：自动生成打印
shitft + F6 ：重构
```



```
优先使用debug模式
con+d 复制一行并自动粘贴
```



```
查看源码的extends和implements信息，查看源码
```



# 第五章 String

- == 与 equals区别

  ```
  equals比较内容
  ==比较内存
  ```

  

  ```
  内存中拥有栈、常量池、堆
  
  栈存放类的引用
  常量池存放字符串常量
  堆存放通过new创建的对象
  ```

  

  <img src="C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230619233728609.png" alt="image-20230619233728609" style="zoom:50%;" />

- API

  ```
  new String // "" // 
  new StringBuilder(单线程效率比StringBuffer高)
  new StringBuffer (线程安全, 适用于多线程)
  
  ```

  

# 第六章

list和set都实现了collection接口，故使用比较类似



## List

### 定义

- ArrayList

  ```
  声明： 
  	ArrayList<> Arr = new ArrayList<>();
  基础操作：
      增:add(value) / add(index,  value)
      删:remove(value) / remove(index) & 返回删除对象
      改:set(index, newValue)
      查:get(index)
  API:
  	~.size() 长度
  ```

  ```
  底层基于数组实现
  添加了其它的方法，使用起来更加方便
  适合高频读取的情况：
  	访问快
  	插入慢
  
  ```

- LinkedList

  ```
  声明：
  	LinkedList<> Arr = new LinkedList<String>();
  基础操作同上
  ```

  ```
  底层基于（双端）链表实现
  适合高频插入的情况：
  	访问慢
  	插入快
  ```

### 遍历

- #### for循环遍历

  ```
  for (Type item: Arr){}
  例：
  for (String item: arr){
              System.out.println(item);
          }
  ```

- #### For Each 遍历

  ```
  Arr.forEach(item->{})
  
  Arr.forEach(System.out::println)
  
  例：
  arr.forEach(System.out::println);
  ```

  

- #### 迭代器遍历

  ```
  arr.iterator() // 每提取一个元素，指针向后移动一步
  
  例：
  Iterator<String> itr = arr.iterator();
          while (itr.hasNext()){
              System.out.println(itr.next());
          }
  ```

---

## Set

- set是乱序存储的
- 不可重复

> Set集合如何保证数据唯一性？
>
> 1、判断数据的hashCode是否存在
>
> 2、若存在，调用equals进行值的比较
>
> 3、两者若都存在，则认定数据唯一
>
> java中不同的类可能拥有不同的hashCode生成方式，比如Objecrt类是 public native int hashCode(){} 实际上是调用C++的代码生成的整数；而String的hashCode则是根据运算规则进行计算进行生成。

![image-20230505161433751](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230505161433751.png)

### 定义

- HashSet

  ```
  HashSet<String> set = new HashSet<String>();
  ```

  

  ```
  ~.size()
  ~.countains() 结合中是否包含元素
  ```

  案例：

  ```
  
  ```

  

- TreeSet