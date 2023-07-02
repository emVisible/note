

## **技巧

```
psvm： idea中快速生成main方法
con+shift+回车：自动生成回车
sout：自动生成打印

```

- con+d 复制一行并自动粘贴

```
优先使用debug模式

```



```
查看源码的extends和implements信息，查看源码
```

## **快捷键

- 重命名 shift f6
- 运行  con shift f10



# 第五章 String

- 类别

  - 静态

    ```
    String
    ```

    

  - 动态

    ```
    StringBuilder
    ```

    

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
  
- StringBuilder

  ```
  高频操作字符串使用。
  	若使用String，因其不可变性会产生很多中间变量 以及 常量池有很多废弃数据
  不生成新的String常量。直接在堆中改变
  ```

  ![image-20230702091950319](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702091950319.png)

# 第六章

list和set都实现了collection接口，故使用比较类似

## List

### 类型

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

  - 实现双端队列和列表两个接口，基于链表
    - 写操作快
    - 读访问慢
  
  
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

简化版本的Map，只能存储单一数据

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

### 类型

- HashSet

  - 默认值为PRESENT

  - 乱序

  - 不重复

  - 以内存对象为标志，故会有业务逻辑同工具逻辑的冲突调整

  - 查找快
    - 通过散列值进行查找，是否已经有对象，定位与检索快

  - 哈希碰撞 && 重复
    - 通过hashCode与equals两个约束条件，实现去重的功能


  ```
  HashSet<String> set = new HashSet<String>();
  ```

  ```
  ~.size()
  ~.countains() 结合中是否包含元素
  ```

  ```
  若不自定义，默认采用顶层Object的hashCode和equals
  ```

  > 散列值
  >
  > ​		String h = "young";
  >
  > ​		int hash = (h.hashCode() )^(h>>>16) 

- LinkedHashSet

  - 逻辑有序
    - 在HashSet基础上增添before和after指针

- TreeSet

  - 有序
    - 基于红黑树实现

## Map

键值映射=>Entry对象=>存储

- 键值对的映射，保存映射关系 / KV
- K不可重复
- K/V可以是任意引用类型数据，一般为String

<img src="C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702112439075.png" alt="image-20230702112439075" style="zoom:80%;" />

### 类型

HashMap

- 对Key进行hash

- 无序存储
- K全局唯一