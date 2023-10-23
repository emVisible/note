# Structured Query Language

## Before All

数据库是数据库管理系统的简称:

​		DBMS(database management system) 

现有的结构化查询语言适用于数据库

数据库分为关系型和非关系型数据库(NoSQL)

入门

- 获取
- 插入
- 更新
- 删除

初级

- 数据汇总
- 子查询编写复杂查询
- MySQL基本操作
- 视图
- 储存过程

高级

- 触发器
- 事件
- 事务
- 并发

进阶：

- 数据库设计
- 索引
- 安全
  - 用户账户
  - 权限分配

## Feature

---

- 语法大小写不敏感

- 大写SQL语句以区分

- 关系型数据库中都有一个主键列



---

## Trick

- 条件排序 --- where + order by 
- 分组筛选 --- group by + having
- 连接多个查询：
  - IN / NOT IN
  - = ANY
  - 

## Main

SQL管理：

​				放入git源码控制里



---

### Chapter 1  基础总结

- # 顺序
  
  - use				                 													                   选择数据库
  - select                                                                                                   选择列
    - distinct														               取消重复项
  - from                                                                                                     选择数据库下的表格
  - *JOIN / LEFT JOIN /RIGHT JOIN + clause
  - where                                                                                                   筛选
    - <>=    and   or   not   in   between and                   逻辑判断
    - like                                                                               模糊搜索
    - regexp                                                                         正则搜索
    - is null                                                                          空值判断
  - order by                                                                                               排序
    - order by xxx desc                                                      降序             
  - limit  a,b                                                                                              限制

```sql
USE sql_store;
SELECT * 
FROM customers
WHERE customer_id = 1		
ORDER BY first_name			
LIMIT 1,3;
/*空格和换行，提高可读性*/
```



- # 选择子句

  - select from 选择指定列：

    ```sql
    SELECT first_name,last_name,points,points+10
    FROM customers;
    ```

  - as:

    ```sql
    SELECT
    	first_name,
        last_name,
        points,
        points*10+100 as discount_factor
    FROM customers;
    -- 如果需要带上空格那就用单引号或者双引号： as "abc"    as 'abc'
    ```

    

  - **distinct:删除重复项**

    ```SQL
    SELECT DISTINCT
    	state
    FROM customers;
    ```

  - 选择子句可以为基本数学运算表达式


- # WHERE子句

  - 运算符

    ```
    >	>=
    <	<=
    =
    !=	<>
    ```
    
  - 日期默认描述方式
  
    ```sql
    YYYY-MM-DD
    
    ex:
        USE sql_store;
        SELECT * 
        FROM Customers
        WHERE birth_date > '1990-01-01';
    ```
  
- # 逻辑

  - and
  
  - or
  
  - not
  
    ```sql
    where not
    is not
    not in
    ```
  
  - in         sql中不可将str和bool整合，不过可以使用i
  
    - 多条件筛选使用IN 
  
    - ```sql
      where sq = 'a' or sq = 'b' or sq = 'c';
      等价于
      where sq in ('a','b','c')
      
      -- not in:
      -- where not in
      ```
  
  - between and
  
    - ```sql
      表示区间
      where quantity >= 1000 and quantitiy <= 4000
      等价于
      where quantity between 1000 and 3000
      ```
  
- # 搜索


  - 符号


    - %   任意字符


    - _     单个字符



  - like    模糊搜索


    - ```sql
      where last_name like 'b%';
      where phone like '%9'
      ​      
    ​      
    ​      --类似正则的%：
    ​      	--where name like '%b';
    ​      	--where name like '%b%';
    ​      	--where name like 'b%';
    ​      ```


​    
​          
​          - regexp
​    ​      
​    ​        - ```
​    ​          where last_name regexp 'filed';
​    ​          
​    ​          -- 其它的是正则语法^$|()[];
​    ​          	
​    ​          ```


  - is null

    - ```mysql
      select *
      from customers
      where phone is null
      
      select *
      from customers
      where phone is not null
      ```
      

- # 排序


  - MySQL 中，选择语句和排序优先度无关

  - order by

    ```mysql
    order by xxx  
    
    按选择的列顺序进行优先度划分：
    		select first_name,last_name
    		from customers
    		order by 1,2
    		-- 尽量少使用，因为数字固定为前两列，若发生顺序变化则列变化
    -- 降序：
    	-- order by xxx desc
    
    ```


- # 限制

  - limit

    ```mysql
    -- 数据分页
    -- page1: 1-4   page2: 5-8 page3: 9 - 12...
    select *
    from customers
    limit a,b
    -- a为偏移量，跳过a个数据的基础上取b个数据
    ```

    

---

### Chapter 2  单一检索

- # 内连接

  - join

    ```mysql
     -- inner join
     -- outer join
    ```

  - 别名

    ```mysql
    --类似c中宏定义
    select *
    from orders o
    join customers c
    	on o.customers_id = c.customer
    ```

    

- # 跨数据库连接

  - 非本数据库加前缀

- # 自连接

  - 可用于组织架构图    员工+上属
  
- # 多表连接

  ```mysql
  select *
  from orders o
  join customers c
  	on o.customers_id = c.custoer
  join payment p
  	on c.payment_method = p.payment_method_id
  ```

- # 多条件连接

  ```mysql
  join xxx 
  	on xxx = xxx
  	AND ooo = ooo
  	
  ```

  多条件连接时，往往是需要通过多个键来确定两张表的唯一数据

  ```mysql
  JOIN xxx
  	ON ooo = ooo AND
  		xxx = xxx
  ```

  

- # 显式连接与隐式链接

  ```mysql
  select *
  from xxx,ooo
  where xxx.xxx = ooo.ooo
  在MYSQL里等同于
  select *
  from xxx
  join ooo
  	on	xxx.xxx = ooo.ooo
  ```

---

### Chapter3 多表检索

- # 内连接与外连接

  - 内连接找需求

  - 外连接看大局

  - WHERE 要在JOIN之后

  - ## 外连接

    - 左连接	左边的记录被返回，无视结果(这里的左指的是：from 后边的数据)

      多表左外连接：

      ```mysql
      USE sql_store;
      SELECT 
      	o.order_date,
          o.order_id,
          c.first_name,
      	s.name AS shipeer,
          os.name AS status
      FROM orders o
      LEFT JOIN customers c
      	ON	c.customer_id = o.customer_id
      LEFT JOIN shippers s
      	ON s.shipper_id = o.shipper_id
      LEFT JOIN order_statuses os
      	ON os.order_status_id = o.status
      ORDER BY
      os.name
      ```

      自外连接：

      ```mysql
      USE sql_hr;
      SELECT 
      	e.employee_id,
      	e.first_name,
          m.first_name as Manager
      FROM employees e
      LEFT JOIN employees m
      	ON e.reports_to = m.employee_id
          
      ```

      

    - 右连接    右边的记录被返回(等同于内连接)(这里的右指的是：join后边的数据)

    

    

    

  - USING子句

    ```mysql
    JOIN连接的两张表，有相同的列（两张表的名字必须完全相同才可使用）
    
    SELECT 
    	o.order_Id
    	c.first_name
    FROM orders o
    JOIN customers c
    	-- ON o.cusotmer_id = c.customer_id
    	USING (customer_id)
    ```

    ```mysql
    USE sql_invocing;
    SELECT 
    	p.date,
        c.name AS client,
        p.amount,
        pm.name AS name
    FROM payments p
    LEFT JOIN clients c
    	USING(client_id)
    LEFT JOIN payment_methods pm
    	ON p.payment_method= pm.payment_method_id
    ```

  - 自然连接

    ```mysql
    Natural join
    数据库自动根据连接的表相同列进行选择，不建议使用，不易进行差错控制，一旦报错很难纠正
    
    USE xxx
    SELECT xxx
    FROM xxx
    NATURAL JOIN xxx
    ```

    

  - 交叉连接

    ```mysql
    cross join
    连接不同的表中的每一条记录，相当于穷举出所有组合方式 一般后边跟ORDER BY 排序
    显式：cross join
    隐式：from tableA,tableB
    
    显示：
    USE sql_store;
    SELECT 
    	s.name AS shipper,
        p.name As product
    FROM shippers s
    CROSS JOIN products p
    ORDER BY s.name
    
    隐式：
    USE sql_store;
    SELECT 
    	s.name AS shipper,
        p.name AS product
    FROM shippers s,products p
    ORDER BY s.name
    
    ```

    

  - UNION联合

    ```mysql
    合并多个查询的结果
    合并的查询必须返回相同数量的语句列
    
    SELECT clause A
    UNION
    SELECT clause B
    
    
    USE sql_store;
    SELECT
    	c.customer_id,
        c.first_name,
        c.points,
    	'Bronze' AS type
    FROM customers c
    WHERE c.points < 2000 
    UNION 
    SELECT 
    	c.customer_id,
        c.first_name,
        c.points,
    	'Silver' AS type
    FROM customers c
    WHERE c.points >= 2000 AND c.points < 3000
    UNION
    SELECT 
    	c.customer_id,
        c.first_name,
        c.points,
        'Golden' AS type
    FROM customers c
    WHERE c.points > 3000
    ```



---

### Chapter4 插入 更新 删除

- # 总览

  - 特殊设置的值

    - DEFAULT

    - NULL

    - 0

    

  - 插入

    - 接口：LAST_INSERT_ID()

    - INSERT INTO ...

      VALUES()

    - INSERT INTO

      /base-clause/

  - 创建

    - CREATE TABLE ... AS

      /base-clause/

      

- 列属性
  - PK：primary key 主键，唯一识别
  - NN：not null       非空，表示是否可以写空值
  - AI：auto increment  自动递增，对pk+1
  - default / expression 默认值

- 插入单行

  ```mysql
  INSERT INTO /table/
  VALUES (DEFAULT , 'cows2','cows3',NULL/DEFAULT)
  
  只对特定的几列插入
  INSET INTO customers (cow1,cow2,cow3,cow5)
  VLAUES (...)
  ```

- 插入多行

  ```mysql
  INSERT　INTO customers
  VALUES (),(),(),()
  
  例:
      USE sql_store;
      INSERT INTO products (name,quantity_in_stock,unit_price)
      VALUE (
          'Young',
          10,
          4.63
      ),
      (
          'Ze',
          20,
          1.56
      ),
      (
          'hang',
          30,
          6.68
      )
  ```

- 插入分层行

  ```mysql
  接口：LAST_INSERT_ID()
  INSERT INTO products
  VALUE (LAST_INSERT_ID(),xxx,xxx,xxx)
  ```

- 创建表

  ​		使用此方法复制表的时候，MYSQL会忽视PK及其AI属性，所以需要提供ID值

  ```
  CREATE TABLE xxx AS    (这里直接写表名，自动为str)
  /clause/        （查询子句）
  ```

- 插入子句+子查询 =>将一张表内的部分/所有数据插入到指定表中

  ```mysql
  INSERT INTO xxx
  SELECT XXX 
  FROM XXX
  WHERE xxx
  ORDER BY xxx
  LIMIT XXX
  ```

  例

  ```mysql
  USE sql_invoicing;
  CREATE TABLE invoices_archieved AS
  SELECT 
      i.invoice_Id,
  	i.number,
  	c.name AS client,
      i.invoice_total,
      i.payment_total,
      i.invoice_date,
      i.payment_date,
      i.due_date
  FROM invoices i
  LEFT JOIN clients c
  	USING(client_id)
  WHERE i.payment_date IS NOT NULL
  
  ```

- 更新

  ```mysql
  UPDATE xxx
  SET 
  	xxx = xxx,
      xxx = xxx，
      xxx = xxx
  WHERE xxx = xxx
  
  允许为空的列可以使用NULL值
  ```

  ```mysql
  选择子句：
  
  UPDATE xxx 
  SET 
  	xxx = xxx,
  	xxx = xxx
  WHERE xxx = 
              (
              SELECT xxx...
              WHERE xxx...)                  单一返回值时
              
  WHERE xxx in 
  			(SELECT xxx...
  			WHERE xxx...)					多返回值时
  ```

  - 先进行子句查询，确定查询的信息无误

    再进行更新

    ```sql
    USE sql_store;
    UPDATE orders
    SET 
    	orders.comments = 'Golden customer'
        WHERE orders.customer_id in (
    		SELECT customer_id
            FROM customers c
            WHERE c.points > 3000
        )
    ```

- 删除

  ```mysql
  删除全部：
  DELETE FROM xxx
  
  DELETE FROM xxx
  WHERE xxx...
  其它操作同更新，可使用子查询
  ```

  

- 恢复数据库
  - 执行初始化sql文件

---

### Chpater 5 聚合函数

- 汇总数据

  ​					★不包含非空值，需要包含非空值时，用*进行查询

  ​					★去重： distinct

  - MAX()
  - MIN()
  - AVG()
  - SUM()
  - COUNT(DISTINCT xxx)  求长度，相当于length

  ```mysql
  SELECT
  	'First half of 2019' AS date_range,
      SUM(invoice_total) AS total_sales,
      SUM(payment_total) AS total_payments,
      SUM(invoice_total - payment_total) AS what_we_expect
  FROM invoices i
  WHERE i.invoice_date 
  	BETWEEN '2019-01-01' AND'2019-06-30'
      
  UNION
  SELECT
  	'Second half of 2019' AS date_range,
      SUM(invoice_total) AS total_sales,
      SUM(payment_total) AS total_payments,
      SUM(invoice_total - payment_total) AS what_we_expect
  FROM invoices i
  WHERE i.invoice_date 
  	BETWEEN '2019-06-30' AND '2020-01-01'
  UNION
  SELECT
  	'Total' AS date_range,
      SUM(invoice_total) AS total_sales,
      SUM(payment_total) AS total_payments,
      SUM(invoice_total - payment_total) AS what_we_expect
  FROM invoices i
  WHERE i.invoice_date
  	BETWEEN '2019-01-01' AND '2019-12-31'
  ```

- 分组

  - GROUP-BY 利用一列数据按条件进行分组

  - 顺序

    ```mysql
    SELECT
    	聚合
    FROM
    WHERE
    ★GROUP BY
    ORDER BY ASC/DESC
    ```

    例

    ```mysql
    USE sql_invoicing;
    SELECT 
    	p.date,
        pm.name AS payment_method,
        p.amount AS total_payment
    FROM payments p
    JOIN payment_methods pm
    	ON pm.payment_method_id = p.payment_method
    ★GROUP BY p.date,payment_method
    ORDER BY p.date
    ```

- HAVING子句

  - HAVING之前的语句均为前提，在这些所有操作之后进行筛选。

  - 顺序必须在GROUPY-BY之后

    ```mysql
    SELECT 
    	c.customer_id,
        c.first_name,
        c.last_name,
        SUM(oi.quantity * oi.unit_price) AS summary
    FROM customers c
    JOIN orders o USING (customer_id)
    JOIN order_items oi
    WHERE state = 'VA'
    GROUP BY 
    	c.customer_id,
        c.first_name,
        c.last_name 
    HAVING summary > 100
    
    ```

- WITH ROLLUP运算符

  - 分类汇总

    ```mysql
    USE sql_invoicing;
    SELECT 
    	state,
        city,
    	i.client_id,
        SUM(i.invoice_total)AS totalPayment
    FROM invoices i
    JOIN clients c 
    	USING(client_id)
    GROUP BY 
    	state,
        city WITH ROLLUP
       
    ```

  - SUM+ROLLUP

    ```mysql
    SELECT 
    	pm.name AS payment_method ,
        SUM(p.amount) AS total
    FROM payments p
    JOIN payment_methods pm
    	ON p.payment_method = pm.payment_method_id
    GROUP BY pm.name WITH ROLLUP  --这里最好不使用别名
    ```

    

---

### Chapter 6 复杂查询

- 子查询

  - ```
    查一个查询返回的值
    SELECT *
    FROM products
    WHERE unit_price > (
    	SELECT unit_price
        from products
        WHERE product_id  = 3
    
    )
    
    例：
    USE sql_hr;
    SELECT *
    FROM employees e
    WHERE e.salary > (
    	SELECT AVG(salary)
        FROM employees
    )
    ```

- IN运算符

  - 某些选择的东西是否在另一张表里/ 不在另一张表里

  - ```
    USE sql_invoicing;
    SELECT *
    FROM clients c
    WHERE c.client_id  NOT IN(
    	SELECT DISTINCT client_id 
        FROM invoices
    )
    ```

- JOIN     VS    子查询

  - 根据表现和可读性进行取舍

    ```
    -- 使用子查询
    USE sql_store;
    SELECT
    	customer_id,
    	first_name,
        last_name
    FROM customers c
    WHERE customer_id IN (
    	SELECT o.customer_idt
        FROM order_items oi
        JOIN orders o
    		USING(order_id)
        WHERE product_id = 3
    )
    
    -- 使用JOIN：
    USE sql_store;
    SELECT DISTINCT
    	customer_id,
    	first_name,
        last_name
    FROM customers
    LEFT JOIN orders
    	USING(customer_id)
    LEFT JOIN order_items
    	USING(order_id)
    WHERE product_id = 3
    ```

- ALL关键词

  - ```
    将数据值与ALL()参数一一比对，返回结果符合假设的值
    ```

- ANY

  - = ANY   <=> IN

- 相关子查询

  - 子查询时间复杂度为n2 ， 对数据一一进行对比，不适用于超大规模数据查询

  - 子查询会返回值

  - ```
    USE sql_hr;
    SELECT 
    	first_name AS name,
        salary
    FROM employees e
    WHERE salary > (
    	SELECT AVG(salary)
        FROM employees
        WHERE e.office_id = office_id 
    )
    
    
    子查询逻辑：
    	查询所有员工的AVG  =>  查询同一部门的AVG
    	对每个对象进行子查询
    ```

- Exist

  - ```
    Exist返回boolean值
    表示查询是数据是否存在
    ```

    ```
    USE sql_store;
    SELECT *
    FROM products
    WHERE product_id NOT IN(
    	SELECT product_id
        FROM order_items
    )
    
    等价于
    
    USE sql_store;
    SELECT *
    FROM products p
    WHERE NOT EXISTS(
    	SELECT product_id
        FROM order_items
        WHERE p.product_id = product_id
    )
    ```

- SELECT子句中的子查询

  - ```
    SELECT 
    	invoice_id,
        invoice_total,
        (SELECT AVG(invoice_total) 
    		FROM invoices ) AS invoice_average,
    	invoice_total - (SELECT invoice_average)
    FROM invoices
    ```

  - 按列进行正交解耦

    ```
    USE sql_invoicing;
    SELECT 
    	client_id,
        name,
    	(SELECT SUM(invoice_total) 
    		FROM invoices
            WHERE c.client_id = client_id) AS total_sales,
    	(SELECT AVG(invoice_total) FROM invoices) AS average,
    	(SELECT total_sales) - (SELECT average) AS difference
    FROM clients c
    ```

- FROM子句中进行子查询

  - 只在简单的查询中直接使用FROM子查询

    ```
    SELECT *
    FROM (
        SELECT 
            client_id,
            name,
            (SELECT SUM(invoice_total) 
                FROM invoices
                WHERE c.client_id = client_id) AS total_sales,
            (SELECT AVG(invoice_total) FROM invoices) AS average,
            (SELECT total_sales) - (SELECT average) AS difference
        FROM clients c
    )
    ```

---

### Chapter 7 函数

- 数值函数

  - ROUND

    - 四舍五入

    - ```
      SELECT ROUND(xxx,x)  数字，精确到小数点几位
      ```

    - TRUNCATE

    - ```
      SElECT TRUNCATE(xxx,x)  数字，截取小数点后的几位
      ```

  - CEILING 

    - 向上取整

    - ```
      SELECT CEILING(xxx)   数字
      ```

  - FLOOR

    - 向下取整

    - ```
      SELECT FLOOR(xxx)  数字
      ```

  - ABS

    - ```
      SELECT ABS()
      ```

  - RAND

    - 范围： 0-1，浮点数

    - ```
      SELECT RAND()
      ```

- 字符串函数

  - LENGTH

  - UPPER

  - LOWER

  - TRIM

    - LTRIM

    - RTRIM

      

    - TRIM

      ```
      SELECT TRIM('    lksdjflkjas   ')    -- lksdjflkjas
      ```

      

  - LEFT(str,n)

    - str：字符串

    - n：从左开始截取的字符的数量

      ```
      SELECT LEFT('Young',3)   -- You
      ```

      

  - RIGHT(str,n)

    - str：字符串

    - n：从右开始截取的字符的数量

    - 返回截取的字符串

      ```
      SELECT RIGHT('Young',3)   -- ung
      ```

      

  - SUBSTRING(str,from.how many)

    - 类似于js里的splice

    - 从哪里开始截取，截取多少个

    - 返回截取的字符串

      ```
      SELECT SUBSTRING('young',3,2)  -- un
      ```

      

  - LOCATE(c,str)

    - 查找c在str里第一次出现的位置(按字符顺序即从1开始)

    - 如果没有查询到，返回0

      ```
      SELECT LOACTE('o','Young')   -- 2
      ```

      截取一串字符

      ```
      SELECT LOCATE('oung','Young')  -- 2
      ```

  - REPLACE(str,AimedStr,replaceStr)

    - 替换

      ```
      SELECT REPLACE('helloWorld','World','Young')
      ```

      

    

  - CONCAT(str1,str2)

    - 合并字符串，常用语连接姓名

      ```
      SELECT CONCAT(first_name,' ',last_name) AS fullName
      ```

- 日期函数

  - NOW()

    - 显示当前的日期+时间

  - CURDATE()

    - 返回日期

  - CURTIME()

    - 返回时间

  - 日期截取

    YEAR()

    - 截取年   YEAR()

      ```
      SELECT YEAR(NOW())  --2022
      ```

    - 截取月  MONTH()

      ```
      SELECT MONTH(NOW()) 
      ```

    - 截取日 DAY()

      ```
      SELECT DAY(NOW())   
      ```

    - 截取小时  HOUR()

      ```
      SELECT HOUR(NOW())    
      ```

    - 截取分钟  MINUTE()

      ```
      SELECT MINUTE(NOW())
      ```

    - 截取秒   SECOND()

      ```
      SELECT SECOND(NOW())
      ```

  - DAYNAME()<img src="C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221108144722364.png" alt="image-20221108144722364" style="zoom:33%;" />

  - EXTRACT()

    ```
    SELECT EXTRACT(DAY FROM NOW())
    ```

  - 灵活使用NOW()

    ```
    YEAR(NOW())
    DAY(NOW())
    MONTH(NOW())
    ```

  - 格式化时间&日期函数

    - DATE_FORMAT(NOW(),"%xxx")

      ```
      SELECT DATE_FORMAT(NOW(),"%y")		22
      SELECT DATE_FORMAT(NOW(),"%Y")		2022
      
      SELECT DATE_FORMAT(NOW(),"%m")		11
      SELECT DATE_FORMAT(NOW(),"%M") 		November
      
      SELECT DATE_FORMAT(NOW(),"%Y %M")    2022 November
      SELECT DATE_FORMAT(NOW(),"%M %d %Y") November 02 2022
      
      SELECT DATE_FORMAT(NOW(),"%H:%i %p")18:39 PM
      ```

    - 日期计算函数

    - DATE_ADD()

      ```sql
      DATE_ADD(NOW(),INTERVAL 1 DAY)  返回明天
      DATE_ADD(NOW(),INTERVAL 1 MONTH)
      DATE_ADD(NOW(),INTERVAL 1 YEAR)
      
      DATE_ADD(NOW(),INTERVAL -1 DAY)  返回昨天
      DATE_ADD(NOW(),INTERVAL -1 MONTH)
      DATE_ADD(NOW(),INTERVAL -1 YEAR)
      ```

    - DATEDIFF(A，B)

      ```
      DATEDIFF('2020-02-03','2020-02-05')  2 返回差值
      ```

    - TIME_TO_SEC(n)

      ```
      TIME_TO_SEC('09:00')  返回00:00 - 9:00 的秒数  32400
      
      
      使用TIME_TO_SEC()进行更加精确的时间计算
      TIME_TO_SEC('09:00') - TIME_TO_SEC('09:20')
      ```

- 其它函数

  - IFNULL(A,B)

    ```sql
    使用其它内容替换空值（单一替换）
    USE sql_store;
    SELECT 
        order_id,
    	IFNULL(shipper_id,'NO ASSIGN') AS shipper
    FROM orders
    ```

  - COALESCE

    ```sql
    使用其它内容替换空值（一组的待命数值）
    USE sql_store;
    SELECT 
        order_id,
    	COALESCE(shipper_id,comments,'NO ASSIGN') AS shipper
    FROM orders
    ```

  - 练习

    ```sql
    USE sql_store;
    SELECT 
    	CONCAT(first_name,' ',last_name) AS customer,
        IFNULL(phone,'Unknow')
    FROM customers
    
    Babara MacCaffrey	781-932-9754
    Ines Brushfield	804-427-9456
    Freddi Boagey	719-724-7869
    Ambur Roseburgh	407-231-8017
    Clemmie Betchley	Unknow
    Elka Twiddell	312-480-8498
    Ilene Dowson	615-641-4759
    Thacher Naseby	941-527-3977
    Romola Rumgay	559-181-3744
    Levy Mynett	404-246-3370
    ```

- IF函数

  ```sql
  SELECT 
  	order_id,
      order_date,
      IF(
  		YEAR(order_date) = YEAR(NOW()),
          'Active',
          'Archived') AS category
  FROM orders
  
  1	2019-01-30	Archived
  2	2018-08-02	Archived
  3	2017-12-01	Archived
  4	2017-01-22	Archived
  5	2017-08-25	Archived
  6	2018-11-18	Archived
  7	2018-09-22	Archived
  8	2018-06-08	Archived
  9	2017-07-05	Archived
  10	2018-04-22	Archived
  
  
  
  练习
  SELECT 
  	product_id pi,
      name,
      COUNT(*) AS orders,
      IF(COUNT(*) <= 1,'ONCE','MANY TIMES') AS frequency
  FROM products
  JOIN order_items
  USING(product_id)
  GROUP BY product_id,name
  ```

- CASE WHEN THEN函数

  ```sql
  SELECT
  	order_id,
      CASE 
  		WHEN YEAR(order_date) = YEAR(NOW()) THEN 'Active'
          WHEN YEAR(order_date) = YEAR(NOW()) - 1 THEN 'Last Year'
          WHEN YEAR(order_date) < YEAR(NOW()) -1 THEN 'Archived'
          ELSE 'Future'
  	END AS categroy
  FROM orders
  ```

  - ```
    练习
    SELECT 
    	CONCAT(first_name,' ',last_name) AS customer,
        points,
        CASE
    		WHEN points > 3000 THEN 'Gold'
            WHEN points BETWEEN 2000 AND 3000 THEN 'Silver'
    		ELSE 'Bronze'
    	END AS category
    FROM customers
    ORDER BY points DESC
       
    ```

    | Clemmie Betchley  | 3675 | Gold   |
    | ----------------- | ---- | ------ |
    | Elka Twiddell     | 3073 | Gold   |
    | Freddi Boagey     | 2967 | Silver |
    | Babara MacCaffrey | 2273 | Silver |
    | Ilene Dowson      | 1672 | Bronze |
    | Romola Rumgay     | 1486 | Bronze |
    | Ines Brushfield   | 947  | Bronze |
    | Levy Mynett       | 796  | Bronze |
    | Ambur Roseburgh   | 457  | Bronze |
    | Thacher Naseby    | 205  | Bronze |

---

### Chapter 8 视图

特点：

- 减少数据库设计改动的影响  
- 限制基础表访问
- 加强数据安全

作用：

- 当权限不够但还是需要去进行更新、修改的时候，使用视图
- 复用

视图相当于创建了一张价值更高的表

- 创建

  - 复用
  - 视图不存储数据，数据存储于表中
  - 提供是虚拟的表

  ```
  USE sql_invoicing;
  CREATE VIEW sales_by_client AS
  SELECT 
  	c.client_id,
      c.name,
      SUM(invoice_total) AS total_sales
  FROM clients c
  JOIN invoices i
  USING (client_id)
  GROUP BY client_id,name
  
  SELECT * FROM sql_invoicing.sales_by_client;
  ```

  | 1    | Vinte       | 802.89 |
  | ---- | ----------- | ------ |
  | 2    | Myworks     | 101.79 |
  | 3    | Yadel       | 705.90 |
  | 5    | Topiclounge | 980.02 |

  ```
  SELECT *
  FROM sales_by_client
  ```

  ```sql
  练习：
  USE sql_invoicing;
  CREATE VIEW clients_balance AS
  SELECT 
  	client_id,
      name,
      SUM(invoice_total - payment_total) AS balance
  FROM clients
  JOIN invoices
  USING(client_id)
  GROUP BY client_id,name
  ORDER BY balance DESC
  ```

  ★CREATE OR REPLACE 优化

  ```
  USE sql_invoicing;
  CREATE OR REPLACE VIEW clients_balance AS
  SELECT 
  	client_id,
      name,
      SUM(invoice_total - payment_total) AS balance
  FROM clients
  JOIN invoices
  USING(client_id)
  GROUP BY client_id,name
  ORDER BY balance DESC
  ```

  

- 删除

  ```
  DROP VIEW clients_balance
  ```

  ```
  USE sql_invoicing;
  CREATE OR REPLACE VIEW invoices_with_balance AS
  SELECT 
  	*,
      invoice_total - payment_total As balance
  FROM invoices
  WHERE (invoice_total - payment_total) > 0
  
  DELETE FROM invoices_with_balance...
  ```

- 注意

  - 当更新或者删除的时候MySQL会默认删除一些行

    ```
    在创建的时候加上语句：
    WITH CHECK OPTION
    ```

---

### Chapter 9 存储过程

运行在服务器上

优点

- 更快的运行速度
- 更加安全
- 更少的网络消耗

- 创建

  ```
  DELIMITER $$
  CREATE PROCEDURE xxx()
  BEGIN
  	/*here are body code  (in MySQ 每个句子整体结束都要有分号结束) */
  END$$
  DELIMITER ;
  ```

- 应用

  - 应用到整体

    ```
    DELIMITER $$
    	/*...*/
    $$
    DELIMITER ; nb
    ```

- 查询

  ``` 
  CALL xxx()
  ```

  

- 删除

  ```
  DROP PROCEDURE IF EXISTS xxx 
  ```

- 基本架构

  ```sql
  DROP PROCEDURE IF EXISTS xxx 
  
  DELIMITER $$
  CREATE PROCEDURE xxx()
  BEGIN
  	SELECT * FROM xxx;
  END$$
  
  DELIMITER ;
  
  
  将其基本架构放入文件夹单独管理
  ```

- 复用配置

  - 在MySQL上的stored procedure 设置全局配置

  - ![image-20221107141632681](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221107141632681.png)

    ```
    应用后，在当前位置生成新的procedure
    之后使用call查询即可
    ```

- 参数

  - 类似强类型语言的函数传参

    ```
    DROP PROCEDURE IF EXISTS query_by_state; 
    
    DELIMITER $$
    CREATE PROCEDURE query_by_state(pState char(2))
    BEGIN
    	SELECT * FROM xxx 
    	WHERE xxx = pState;
    END$$
    
    DELIMITER ;
    ```

- 默认参数

  ```
  DROP PROCEDURE IF EXISTS query_by_state; 
  
  DELIMITER $$
  CREATE PROCEDURE get_invoices_by_clients(pId int)
  BEGIN
  	IF pId IS NULL THEN
  		SET pId = 'xxx';
  	END IF;
  	SELECT * FROM clients
  	WHERE id = pId;
  END$$
  
  DELIMITER ;
  ```

- 参数验证

  ```
  CREATE PROCEDURE make_payment
  (
  	invoice_id INT,
      payment_amount DECIMAL(9,2),
      payment_date DATE
  )
  BEGIN
  	IF payment_total <= 0 THEN
  		SIGNAL SQLSTATE '22003'
  		SET MESSAGE_TEXT = 'Invalid payment amount';
  	UPDATE invoices i
      SET 
  		i.payment_total = payment_amount ,
          i.payment_date = payment_date
  	WHERE 
  		i.invoice_id = invoice_id;
  END
  ```

  

- 练习

  ```
  //prac1
  DELIMITER $$
  CREATE PROCEDURE get_invoices_with_balance()
  BEGIN
  	SELECT * 
      FROM invoices
      WHERE invoice_total - payment_total > 0;
  END$$
  DELIMITER ;
  
  //prac2
  DROP PROCEDURE IF EXISTS query_by_state; 
  
  DELIMITER $$
  CREATE PROCEDURE get_invoices_by_clients(pId int)
  BEGIN
  	SELECT * FROM clients
  	WHERE id = pId;
  END$$
  
  DELIMITER ;
  ```

  ---
  
  P73 

---

### Chapter 10 触发器

触发器在SQL查询前后执行

在SQL之后执行用于检查

- 通过触发器进行操作记录
- 通过触发器进行同步更新

- 创建

  ```
  DELIMITER $$
  CREATE TRIGGER payment_after_isnert
  	AFTER INSET ON payments
  	FOR EACH ROW
  
  BEGIN
  	UPDATE invoices
  	SET payment_total = payment_total + NEW.amount
  END
  
  $$
  DELIMITER;
  
  
  表命名遵循相应规范， 中间的before和after是行规
  
  练习
  DELIMITER $$
  CREATE TRIGGER payments_after_insert
  	AFTER DELETE ON payments
      FOR EACH ROW
      
  BEGIN 
  	UPDATE invoices
      SET payment_total = payment_total - OLD.amount
      WHERE invoice_id = OLD.invoices_id;
  END %%
  
  DELIMITER ;
  ```

- 查看

  ```sql 
  SHOW TRIGGERS
  
  模糊查询：
  	SHOW TRIGGER LIKE "XXX%"      			显示以XXX为名称开头的的trigger
  ```

- 删除

  ```sql
  DROP TRIGGER IF EXISTS xxx
  
  
  将删除和创建结合
  
  DROP TRIGGER IF EXISTS xxx
  ___创建
  ```

- 实际应用：审计

  ```sql
  DELIMITER $$
  DROP TRIGGER IF EXISTS payments_after_insert
  CREATE TRIGGER payments_after_insert
  	AFTER INSERT ON payments
      FOR EACH ROW
      
  BEGIN 
  	UPDATE invoices
      SET payment_total = payment_total + NEW.amount
      WHERE invoice_id = NEW.invoices_id;
      
      INSERT INTO payments_audit
      VALUES(NEW.client_id,NEW.date,NEW.amount,'Insert',NOW())
  END %%
  
  DELIMITER ;
  ```

- NEW:返回刚刚插入的行

  - NEW.xxx  快速获属性

- OLD 返回更新前的行以及数值

- LIKE xxx%



- 事件

  ```
  查看MYSQL所有系统变量SHOW VARIABLES LIKE 'event%'
  ```

  - 创建                               举例：删除超过一年的审计记录

    ```
    DELIMITER $$
    
    CREATE EVENT yearly_delete_stale_audit_rows
    ON SCHEDULE
    	-- AT '2019-05-01'
        EVERY 1 year starts '2019-01-01' ends '2029-01-01';
    DO BEGIN
    	DELETE FROM payment_audit
        WHERE action_date < now() - INTERVAL 1 year;
    
    END$$
    DELIMITER ;
    ```

  - 查看

    ```
    show events
    ```

  - 修改

    ```
    ALTER EVENT 
    -- same like create 
    ```

    

---

### Chapter 11 事务

- A C  I D
  - Atomicity            原子性
  - Consistency        一致性
  - Isolation              独立性
  - Durability            持久性

- 单个工作单元的一系列SQL语句
- 要么全部成功，要么全部失败
- 数据之间相互隔离

- 事务本身按顺序执行

- 事务创建

  ```
  START TRANSACTION
  
  
  COMMIT;
  
  或
  START TRANSACTION
  
  
  ROLLBACK;  显式取消语句执行
  
  ```

  

- 并发（concurrency）

  - 丢失更新   (后发生的操作覆盖了先发生的操作)

    ```
    多个事务更新相同数据
    &&
    没有上锁
    
    
    后边的操作会覆盖前边的操作
    
    
    解决方法：
    	使用锁
    ```

  - 脏读

    ```
    事务读取了未被提交的数据
    	给A权限然后撤销。
    	真正撤销前被B使用了权限，但此时已经撤销权限
    	也就是说得到了本没有的权限
    
    解决：建立隔离级别
    ```
    
  - 读取不一致的数据

    ```
    读取了两次相同的数据，但得到了不一样的结果
    ```
    
  - 幻读

    ```
    某一个命令在修改数据，其数据状态为空
    ```

- 锁

  - 使用事务运行，每行运行时会给当前行上锁，其它的程序并行的时候会进行异步等待

- 隔离

  - 隔离级别

  - ![image-20221205143157492](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221205143157492.png)

  - 隔离级别越高，性能开销越大（使用更多的锁）

  - 隔离级别越低，并发性能越高

    ```
    隔离级别可能会损害性能和可扩展性
    1、读取 && 已提交      只能读取已提交的程序
    2、可重复读
    ```

  - 系统默认

    ```
    SHOW VARIABLES LIKE 'transaction_isolation'
    
    --REPEATABLE-READ
    ```

  - 设置隔离级别

    ```
    SET TRANSACTION_ISOLATION LEVEL xxx
    
    为当前会话 || 之后所有的事务设定隔离级别
    SET SESSION TRANSACTION_ISOLATION LEVEL xxx
    
    SET GLOBAL TRANSACTION_ISOLATION LEVEL xxx
    ```

  - 四种级别

    - 等级1：读未提交
      - 可以读未提交的数据
      - READ UNCOMMITED
      - 会遇到所有并发问题
    - 等级2：读已提交
      - 可以读取已提交的数据
      - READ COMMITED
    - 等级3：可重复读取
      - REPEATABLE READ
      - 读取保持一致性
    - 等级4：序列化
      - SERIALIZABLE
  
  - 死锁
  
    - MYSQL的事件处理机制，当一条语句使用了数据库中某条数据时，将锁定其数据。若此时其它语句有使用到这条数据，将产生死锁，永远等待
    - 特点是两个不同的指令集以相反的顺序执行
    - 解决
      - 调整为相同的顺序
      - 简化程序事务，提高正交性
      - 错开运行时间
    - ![image-20221205153125425](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221205153125425.png)
  
    - ![image-20221205153143640](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221205153143640.png)







---

### Chapter12 数据类型



插入图片数据

- 数据库大小增加
- 弱化备份
- 性能问题
- 额外代码

字符串类：

```
char 
VARCHAR    65535   64kb  可被编入索引
TINYTEXT    255byte
TEXt        64kb
MEDIUMTEXT   16mb
LONGTEXT    4G 
```

数值类：

- 符号
- 补零

```
TINYINT            1byte   -128 127
UNSIGNED TINYINT            0-255            年龄

SMALLINT   
MEDIUMINT 
INT
BIGINT
```

浮点型：

```
DECIMAL(精度，位数)
DEC
NUMERIC
FIXED

货币等精准储存
FLOAT
DOUBLE
```

布尔型

```
TRUE 1
FLASE 0
```

枚举和集合 不建议使用

```ABAP
ENUM
SET
```

时间

```
TIME
DATE
TIMESTAMP  只能储存2038年之前
DATETIME
YEAR
```

二进制数据

```
TINYBLOB   255b
BLOB       65KB
MEDIUMBLOB 16MB
LONGBLOB    4g
```

JSON

```
创建：
	手动   '/字符内是json格式/'
	MYSQL内置函数：
		JSON_OBJECT()
		JSON_ARRAY()
		JSON_EXTRACT(列，路径)  如JSON_EXTRACT(xxx,$)  美元符号表示当前文档路径 
		
		JSON_SET()  更新现有或添加新属性
		JSON_REMOVE()
		UPDATE JSON_SET(
			properties,'$xxx.xxx'
		)
		
	列路径运算符
		xxx->$.xxx 返回值 || json对象
```

![image-20221211140359434](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221211140359434.png)

---

### Chapter 13 设计

- 数据建模是一个迭代的过程



- 理解和分析业务需求    --- 越是了解业务的问题，越是更好的找到解决方案
- 概念模型                       --- 业务的实体，事务，概念，以及之间的关系        人，事件，位置
- 构建数据库模型(逻辑模型)            ---存储数据
- 构建实体模型



设计细节

- VARCHAR(50) 用于 姓名，性别
- VARCHAR(255)用于邮箱
- DATETIME用于日期

- 核心
  - 概念    绘制概念图
  - 逻辑    标注数据类型
  - 实体    在DBMS中具体实现概念和逻辑



- 概念
  - EML  应用范围更广
  - ER  entity relation 实体关系图，用于数据建模
- 提高抽象层次的意义，是让双方理解，更多的是让对方理解

![image-20221211142855349](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20221211142855349.png)
