## Session

Session 服务端

Cookie 客户端

基于Session认证的问题

- 服务端开销增大——session保存在内存中
- 不便于分布式，扩展能力降低——只能从存储的服务器认证
- 易遭受CSRF——基于cookie识别用户，若cookie被截取，用户会遭受跨站请求攻击

基于Token的认证

- 便于扩展——不需要指定特定的机器

JsonWebToken（JWT）

- Header 头

  ```
  {
  	'typ':'jwt', // 声明类型
  	'alg':'HS256' // 一般使用HMAC SHA256声明
  }
  随后进行base64加密（可对称解密）
  ```

- Payload 载荷

  ```
  有效信息（一般不存储敏感信息）
  	标准声明
  	公共声明
  	私有声明
  ```

  ![image-20230702163435761](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702163435761.png)

  

- Signature 签名

  ![image-20230702163519726](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702163519726.png)

  ![image-20230702163641234](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702163641234.png)

  ![image-20230702163711491](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702163711491.png)

  ![image-20230702163754541](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702163754541.png)

  ![image-20230702163841530](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230702163841530.png)