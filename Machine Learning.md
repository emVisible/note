# 人工智能

>  从经验中学习
>
> 从数据中的隐式模式中推断信息
>
> 对新事物进行标签推理

人工智能，机器学习，深度学习，数据科学之间的关系

```
AI > ML > DL
	^ ^ ^ ^ ^ ^ ^
	| | | | | | |
	Data Science
```

机器学习的应用

- 强规则性游戏——象棋 && 围棋
- 推荐算法——netflix && google 用于提高对用户偏好的准确度
- 药物侦测 && 字符识别——邮局
- 声音辅助系统——Siri
- 辅助驾驶
- 人脸识别系统——Facebook
- 癌症诊断

```
Alpha-beta剪枝

搜尋演算法
Alpha-beta剪枝是一种搜索算法，用以减少极小化极大算法搜索树的节点数。这是一种对抗性搜索算法，主要应用于机器游玩的二人游戏。当算法评估出某策略的后续走法比之前策略的还差时，就会停止计算该策略的后续发展。该算法和极小化极大算法所得结论相同，但剪去了不影响最终决定的分枝。
```

作出新的预测

- 元素
  - 训练集
  - 验证集
- 训练数据
- 推理引擎

机器学习的类别

1. 监督学习 与 非监督学习 supervised  & unsupervised
2. 聚类 与 分类

特征工程

- 核心是最大化信噪比，最大化携带信息最多的特征，最小化不是这样的特征

  - 测量哪些特征

  - 加权方法

- 从聚类的角度看待数据

  - 相同属性
  - 不同属性

- 特征 高匹配特征 权重计算

过度拟合

- 本不存在关联的元素之间，产生了某种映射关系
- 过多的特征容易产生过拟合，出现更大错误的机率 => 功能的选择十分重要

![image-20230727105746776](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230727105746776.png)

![image-20230727105750189](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230727105750189.png)

![image-20230727105753083](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230727105753083.png)

![image-20230727105755960](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230727105755960.png)

![image-20230727105759931](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230727105759931.png)

![image-20230727105803155](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230727105803155.png)