# 图片模型训练和使用的基本流程

1. 导入数据集

   ```
   需要完成的事情：
       确认训练数据集和测试数据集，均包括X与Y，X是训练输入，Y是训练结果
       (train_images, train_labels)
       (test_images, test_labels)
   
   	如需可视化展示，需要添加标签组，即构建一个Y的结果列表
   ```

2. 数据预处理

   ```
   浏览数据
   	确认训练集的图像数量与大小 （X）
   	确认训练集的标签数量与值（Y）
   	确认测试集的图像数量与大小（X）
   	确认测试集的标签数量与值（Y）
   预处理
   	检查图片像素值范围，并将其缩小至0-1之间，以馈送至神经	简易验证，确认是否正确（plt）
   ```

3. 构建模型

   ```
   设置层
   	展开层
   	全链接层
   设置编译模型
   	优化器 optimizer
   	缺失函数 loss
   	指标（用于监控训练和测试步骤）
   ```

4. 训练

   ```
   1. 馈送数据
   	model.fit(train_images, train_labels, epochs)
   2. 评估准确率
   	test_loss, testacc = model.evalueate(test_images, test_labels, verbose)
   3. 预测
   	附加Softmax层并进行预测。值为预测结果的数组。
   	np.argmax()输出最大置信度，并同测试集的原数据进行校验
   4. 验证结果
   
   *如有需要，通过plt包进行可视化操作
   ```

5. 使用(预测)

   ```
   附加softmax层
   ```

   ```
   <START> this film was just brilliant casting location scenery story direction everyone's really suited the part they played and you could just imagine being there robert <UNK> is an amazing actor and now the same being director <UNK> father came from the same scottish island as myself so i loved the fact there was a real connection with this film the witty remarks throughout the film were great it was just brilliant so much that i bought the film as soon as it was released for <UNK> and would recommend it to everyone to watch and the fly fishing was amazing really cried at the end it was so sad and you know what they say if you cry at a film it must have been good and this definitely was also <UNK> to the two little boy's that played the <UNK> of norman and paul they were just brilliant children are often left out of the <UNK> list i think because the stars that play them all grown up are such a big profile for the whole film but these children are amazing and should be praised for what they have done don't you think the whole story was so lovely because it was true and was someone's life after all that was shared with us all
   ```

   # 过拟合
   
   模型在训练数据上的表现 比 在以前从未见过的数据上的表现要更好。

---

# NLP Tutorial Python

> 地址：
>
> https://www.youtube.com/watch?v=R-AG4-qZs1A&list=PLeo1K3hjS3uuvuAXhYjV2lMEShq2UYSwX
>
> 特点：
> 	1. 直观
> 	1. 编码练习
> 	1. 端到段项目练习
> 	1. 真实行业现状以及使用

推荐的书

- Practical Natural Language Processing

- 其两位作者也是大佬，在油管有帐号

实际应用举例

1. Gmail 邮件过滤 => 短信过滤 => 信息特征提取 && 判断 && 过滤
2. 自然语言翻译。
3. 客服机器人。
4. 语音助手。Amazon、Alexa、Google Assistant
5. google搜索。使用BERT，提高结果精度
6. 新闻标题自动生成。 

---

免费可用预训练模型

- Fasttext
- Tensorflow Hub
- GPT3

开源系统

- spaCy
- Gensim
- NLTK
- scikit learn
- TensorFlow && PyTorch
- Hugging Face
- zoom
- Kaggle
- Stack Overflow

硬件资源（GPU）

- AWS
- Azure
- Google Cloud

学习资源

- Youtube
- Bootcamps
- uUdemy
- coursera
- towards data science

大型公司加持

- Google
  - TensorFlow
  - BERT
  - TPU
  - google home
  - google cloud
- AWS
  - Amazon SageMaker 
  - amazon echo dot

- Meta
  - PyTorch
  - fastText

---

> 很多NLP问题可以通过正则来解决
>
> 学习NLP之前，先学习正则，尽量简化问题
>
> 资源： regex101.com

用户机器人



信息提取