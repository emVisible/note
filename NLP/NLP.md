

# *正则

> 很多NLP问题可以通过正则来解决
>
> 学习NLP之前，先学习正则，尽量简化问题，而不是把问题搞复杂

基础包：re

高级API包：regex

```
re.findall(regex, text)
```

---

## 原文档整理

A regular expression (or RE) specifies a set of strings that matches it.

- Unicode string(str)和8-bit
- 使用r string来表示raw data
- 调用API可以使用regex包
- 复杂的大型正则可以拆分为多个小型正则
- before a newline == end of the line selected

Grammar

```
. 默认不匹配newline. If the DOTALL flag has been specified, this matches any character including a newline.
$ searching for a single $ in 'foo\n' will find two (empty) matches: one just before the newline, and one at the end of the string.
```

Schema

- non-greedy 非贪婪模式

- Multiline 多行模式

- *+?默认为贪婪模式

  ```
  非贪婪模式
  *?
  +?
  ??
  ```

- {m,n}? 尽可能少的匹配，有m个就不匹配n个

- {m,n}+ 尽可能多的匹配，有n个就不匹配m个，非回溯匹配

Example

- ```
  a{4,}b
  ```



# NLP

> 参考教程地址：
>
> https://www.youtube.com/watch?v=R-AG4-qZs1A&list=PLeo1K3hjS3uuvuAXhYjV2lMEShq2UYSwX
>
> 特点：
>
>  	1. 直观
>  	 1. 编码练习
>  	 1. 端到段项目练习
>  	 1. 真实行业现状以及使用

## NLP的实际应用

核心：定向信息提取

1. Gmail 邮件过滤 => 短信过滤 => 信息特征提取 && 判断 && 过滤
2. 自然语言翻译。
3. 客服机器人。
4. 语音助手。Amazon、Alexa、Google Assistant
5. google搜索。使用BERT，提高结果精度
6. 新闻标题自动生成。 

---

## 索引

推荐书

- Practical Natural Language Processing

预训练模型

- Fasttext
- Tensorflow Hub
- GPT3

开源包

- spaCy
- Gensim
- NLTK
- scikit learn
- TensorFlow && PyTorch
- Hugging Face
- zoom
- Kaggle
- Stack Overflow

云服务

- AWS
- Azure
- Google Cloud

学习资源

- Youtube
- Bootcamps
- uUdemy
- coursera
- towards data science
- 正则： regex101.com

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

## 术语(Jargon)

### 基本概念

文档 Document

- 一段文本、一个段落、一篇新闻文章等等都从属于文档的概念

向量

- 本质上就是一堆数字。在Python中可以简单理解为list

拟合

- 模型拟合数据后，数据就是模型的corpus，也就是词汇库

训练-测试 分割(Train-Test Split)

- 将数据分为训练集和测试集

不平衡(Imbalance)

```
在机器学习中，不平衡问题（Imbalance Problem）指的是在训练数据中不同类别的样本数量差异很大的情况。通常情况下，一些类别的样本数量远远多于其他类别，导致模型在训练过程中更容易学到多数类别的特征，而对于少数类别的学习不足。这种不平衡可能会影响模型的性能，尤其是在处理二分类问题时。
```

分词 Token

分词器 Tokenizer

文本表示(Text Representation)

稀疏表示法(Sparse Representation)

- 0多但不重要，1少但重要

- 缺点
  - 浪费硬件资源
  - 不能准确转化语意(近义词)

稀疏矩阵(Sparse Matrix)

过拟合(Overfitting)

- 模型在训练数据上的表现 比 在以前从未见过的数据上的表现要更好，泛化能力过弱，只能比较好的处理见过的

词汇量问题(Out of Vocabulary, OOV)

- 文本转向量时，模型的词汇库中没有待转换的单个或者多个词汇

### 基本词 (Lemma)

```
eat 是 ate 的基本词
eat is ate's lemma
```

### 词性 POS (Part Of Speech)

```
名词					Noun
动词 					Verb
代词 					Pronoun
形容词				   Adjective
副词				    Adverb
感叹词				   Interjection
连词					Conjunction
介词(链接名词)		  Adposition |Preposition
```

### 命名实体识别(Named Entity Recognition, NER)

- 构建NER模型

  ```
  1 硬编码 + 手动添加
  2 基于规则的NER(spacy自带EntityRuler)
  	正则
  	自定义规则
  3 机器学习(CRF && BERT)
  ```

- label_ 

  ```
  Tesla Inc  |  ORG  |  Companies, agencies, institutions, etc.
  $45 billion  |  MONEY  |  Monetary values, including unit
  ```

  

### 停用词(STOP Words)

- 预处理阶段概念

- 常用的，同程序的正确率无关的词语，如

  ```
  to a from the had
  ```

- 停用词需要分场合和具体情况使用，如以下使用not为停用词会出现错误

  ```
  this is a good movie
  this is not a good movie
  ```

- 在Chat bot && QA && Language Translation等场合不适用

### 多元语法(N-Gram)

多元语法通过移动窗口(Moving window)使得原本单一词对应单一token变为多个词对应一个token。

词袋模型是N-Gram的特例(N = 1)、二元语法(Bi-Gram, N=2)、三元语法(Ti-Gram, N=3)

Gram模型基于文本中词语的组合，将连续的n个词语视为一个单元，构建了一个基于这些单元的统计模型



局限性

- 随着元数增加，模型稀疏性会提高
- 没有解决词汇量不足的问题



## NLP的一般流程

> 数据采集
>
> 数据清理
>
> 数据预处理
>
> 特征工程
>
> 模型构建
>
> 模型评估

大致流程可解释为：数据采集—分词—向量化—建模—

数据流：

​	文档==---预处理---==>后处理文本---==>词袋模型/计数向量化模型(词频计算)=>

### 数据采集(data acquisition)

采集原始数据

- 数据的质量奠定了大楼的根基，奠定了质量的上限

### 文本提取 && 文本清理(text extraction && text cleanup)

清理不需要的数据并改正错误数据

- 有效信息提取
- 对错误信息进行修复

### 预处理(pre-processing)

1. 分句(sentence tokenization / sentence segmentation)

   - 核心是创建句子过滤器(sentence filter && sentence tokenizer)，以处理和应对特殊语句和情况

2. 分词(word tokenization / tokenization)

   *词干分析使用NLTK, spacy不支持词干分析; spacy仅支持词形还原

   - 词干提取(Stemming)

     - 将同义词、不同语态和时态的相同的词映射到基本词（词包括基本词，比如loved=>love, eating=>eat）

       ```
       Use fixed rules such as remove able, ing etc. to derive a base word
       ```

   - 词形还原(Lemmatization)

     - 将同义词、不同语态和时态的相同的词映射到基本词（词不包括基本词，比如ate=>eat, ran=>run）

       ```
       Use knowledge of a language (a.k.a.linguistic knowledge)to derive a base word
       ```

---

> 计算机当然不会理解文本，所以需要转成数字的方式让计算机可以"理解"。这就是特征工程(feature engineering)。

---

### 特征工程(feature engineering) && 文本表示(Text Representation)

> 文本转向量

以适当的方式表示单词，从原始数据(文本)中提取特征，转换为数字向量。

特征工程的质量，相对于计算算法，会产生更大的能效。其地位实际上应该仅次于高质量的数据采集 && 处理。

将文本转为向量，成为向量空间模型(Vector space model)。

- *Label Encoding

  ```
  Create a vocabulary that need.
  ```

- *One Hot Encoding

  ```
  在拥有检测词库的前提下，对每一个token和词库进行一一比较。
  两条线确定一个点
  
  缺点：
  	不能准确的捕捉单词的语义 语义近似的单词没有近似的向量表示
  	硬件资源浪费
  	难以泛化 OOV(Out Of Vocabulary) 匹配的词汇量不足
  	长度不固定
  ```

- Bag of Words 词袋模型

  在 Bag of Words 模型中，文本被表示为一个包含单词频率的向量，其中每个单词都对应一个维度。其实现简单易懂、易于实现和计算效率高。

  模型假定文本中的含义来自于单词的出现频率，而忽略了单词的顺序和语法结构。不能有效捕捉上下文信息和语义关联。

  这意味着文本被看作一个“袋子”（即Bag），其中单词的出现顺序并不重要，只有单词的出现与否以及出现的频率对最终的表示起作用。

  会产生非常稀疏的高维向量，面对大规模文本语料库时，存储和计算开销较高。

  ```
  升级版本的独热编码，同样的拥有vocabulary，对检测的token进行了lemmatization，并以句子作为单位进行检测。
  
  模型训练的时候，训练的源数据往往并不长，NLP一般提取的是其少数关键词汇。
  
  通过计数向量化器，每个Source为独立的一个向量(这也符合词汇长度普遍不长的特点)，其会同vocabulary进行比较。
  ```

  ```
  词袋模型的构建流程
      构建词汇表：
          首先，从文本语料库中提取所有不同的单词，并将其作为词汇表的一部分。
          每个单词都对应一个唯一的标识符。
  
      计算单词频率：
          对于给定的文本文档，计算每个单词在文档中出现的次数。
  
      构建向量表示：
          根据词汇表中单词的顺序，将文档表示为一个向量，其中向量的每个元素对应一个单词在文档中出现的频率。
          这个向量被称为文档的 Bag of Words 表示。
  ```

  

- TF-IDF Vectorizer

- Word Embedding

---

### 模型构建(model building)

通过各类不同的手段，最终创建分类器(classifier

- Naive Bayes Classifier
- SVM
- Random Forest

### 模型评估(Evaluating)

Confusing Maxtrix

### ...下一步

循环(预处理=>特征工程=>模型构建=>模型评估)

- 对评估后得出的结果进行再应用，不断完善模型，

部署

监视 && 迭代

### 代码展示

```
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import classification_report
'''
    整体流程
      1. 数据采集。读取csv数据
      2. 文本提取。
          通过代码添加结果列
          手工分为数据集和测试集
      3. 预处理(跳过, 数据已经处理好)
      4. 特征工程。
          创建计数向量化器
          转化训练集数据为向量(fit_transform)
          转化测试集数据为向量(transform)
      5. 模型构建。
          创建分类器
          训练模型(fit)
      6. 模型预估。
          测试集预测&&报告
            将训练好的模型对测试集进行预测
            使用classification_report展示测试结果
          外部数据预测
            使用非训练&&测试数据的数据进行预测
'''

doc = pd.read_csv('./spam.csv')

doc['spam'] = doc['Category'].apply(lambda x: 1 if x == 'spam' else 0)
x_train, x_test, y_train, y_test = train_test_split(doc.Message, doc.spam, test_size=0.2)

count_vectorizor = CountVectorizer()
x_train_vector = count_vectorizor.fit_transform(x_train.values)
x_test_vector = count_vectorizor.transform(x_test)

model = MultinomialNB()
model.fit(x_train_vector, y_train)

y_test_predict = model.predict(x_test_vector)
classification_report(y_test ,y_test_predict)

useModel = [
    "I'm still looking for a car to buy. And have not gone 4the driving test yet.",
    "UpgrdCentre Orange customer, you may now claim your FREE CAMERA PHONE upgrade for your loyalty. Call now on 0207 153 9153. Offer ends 26th July. T&C's apply. Opt-out available"
]

result = model.predict(count_vectorizor.transform(useModel))
print(result)
```

## 常见问题

提取公司名称

```
通过构建词汇表
```



## spacy

> spacy   https://spacy.io



- 通过token.label_，筛选具体类别的事物（位置、人、日期...）
- 通过token.tag_
- 通过spacy.explain()，使
- 通过token.pos_

```
========================初始化========================
import spacy

模型加载
nlp = spacy.load("en_core_web_sm") # 加载预训练模型（需要提前下载）
nlp = spacy.blank("en")# 加载空模型（支持的语言均可传入）

获取doc
doc = nlp("...") # 传入文本对象

从文件获取text
import pandas as pd
df = pd.read_csv("")

# 获取前几项
df.head()

# 检查目标标签是否平衡
df.Category.value_counts()

# 文本处理
df['列名'].apply(lambda x: 1 if x == 'spam' else 0)


========================分词(Tokenization)========================

分词
token = doc[1] # 返回句子中对应位置的token
tokens = [token for token in doc]

获取词性，可提取不同词性的词
token.pos_
spacy.explain(token.pos_) # human-readable
# 获取计数统计
count = doc.count_by(spacy.attrs.POS)
for k,v in count.items():
	print(doc.vocab[k].text, v)
    NOUN 96
    VERB 27
    ADV 15
    ADP 39
    PROPN 16
    PUNCT 32
    DET 34
    PRON 4
    AUX 13
    CCONJ 10
    ADJ 23
    SPACE 7
    NUM 19
    PART 4
    SCONJ 8
    X 1

获取标签
token.tag_
spacy.explain(token.tag_)

词形还原
token.lemma_

命名体识别(Name Entity Recognize)
doc = nlp("Tesla Inc is going to acquire twitter for $45 billion")
for ent in doc.ents:
    print(ent.text, ent.label_) # 获取文本和标签
# 列出所有实体
nlp.pipe_labels['ner']

# NER渲染显示
from spacy import displacy
displacy.render(doc, style="ent")

# 自定义NER
from spacy.tokens import Span
doc = nlp("Tesla is going to acquire Twitter for $45 billion")
for ent in doc.ents:
    print(ent.text, " | ", ent.label_)
s1 = Span(doc, 0, 1, label="ORG")
s2 = Span(doc, 5, 6, label="ORG")

doc.set_ents([s1, s2], default="unmodified")
for ent in doc.ents:
    print(ent.text, " | ", ent.label_)

Tesla  |  ORG
Twitter  |  ORG
$45 billion  |  MONEY

获取指定格式
token.text # 返回字符

判断
token.is_alpha
token.like_num
token.is_currency # 特殊字符
token.i # 索引
token.is_punct # 标点
token.like_email


从句子中拆分词
    for sentence in doc.sents:
        for word in sentence:
            pass

读取文本
	with open("xxx.txt") as f:
    	text = f.readlines()
    text = " ".join(text)
    
自定义tokenizer # 对于gimme添加额外规则——拆分为gim和me两个单词
from spacy.symbols import ORTH
nlp = spacy.blank("en")
nlp.tokenizer.add_special_case("gimme", [
    {ORTH: "gim"},
    {ORTH: "me"},
])
doc = nlp("gimme double cheese extra large healthy pizza")
tokens = [token.text for token in doc]
# ['gim', 'me', 'double', 'cheese', 'extra', 'large', 'healthy', 'pizza']

========================分句(Sentence Tokenization / Segmentation)========================
# 分句前必须添加对应处理分句的pipeline
nlp.add_pipe('sentencizer')

分句
    for sentence in doc.sents:
        pass

========================管道（Pipeline）========================
获取预训练模型/加载的pipeline
nlp.pipeline

管道添加（基于blank pipeline）
source_nlp = spacy.load("en_core_web_sm")

nlp = spacy.blank("en")
nlp.add_pipe("ner", source=source_nlp)
nlp.pipe_names

========================词形还原Lemmatization========================
token.lemma_

# 自定义lemmatizer，处理特殊情况。指定：将Bro和Brah还原为Brother
nlp = spacy.load("en_core_web_sm")
ar = nlp.get_pipe('attribute_ruler')

ar.add([[{"TEXT":"Bro"}],[{"TEXT":"Brah"}]],{"LEMMA":"Brother"})

doc = nlp("Bro, you wanna go? Brah, don't say no! I am exhausted")
for token in doc:
    print(token.text, "|", token.lemma_)
# 将所有词拼起来，结果就是原句子的单词还原版
final_base_text = ' '.join(all_base_words)

========================停用词========================
import spacy
from spacy.lang.en.stop_words import STOP_WORDS
# 打印停用词
print(len(STOP_WORDS))
doc = "We just opened our wings,the flying part is coming soon"
nlp = spacy.load("en_core_web_sm")
doc = nlp(doc)

for token in doc:
    if token.is_stop:
        print(token)

```

<img src="C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20231029224517126.png" alt="image-20231029224517126" style="zoom:60%;" />

spacy案例

```
1结构化段落的URL
text='''
Look for data to help you address the question. Governments are good
sources because data from public research is often freely available. Good
places to start include http://www.data.gov/, and http://www.science.
gov/, and in the United Kingdom, http://data.gov.uk/.
Two of my favorite data sets are the General Social Survey at http://www3.norc.org/gss+website/, 
and the European Social Survey at http://www.europeansocialsurvey.org/.
'''

doc = nlp(text)
data_websites = [token.text for token in doc if token.like_url ] 

# ==============================


2句子中的货币量和单位
transactions = "Tony gave two $ to Peter, Bruce gave 500 € to Steve"
doc = nlp(transactions)
for token in doc:
    if token.like_num and doc[token.i+1].is_currency:
        print(token.text, doc[token.i+1].text)        
        
# ===============================
for k,v in count.items():
    print(doc.vocab[k].text, "|",v)
```



## NLTK

> NLTK

```
from nltk.tokenize import sent_tokenize, word_tokenize

import nltk

nltk.download('punkt')
分词
	sent_tokenize("...")
	word_tokenize("...")


==============词干提取=================
from nltk.stem import PorterStemmer
stemmer = PorterStemmer()
lst_words = ['running', 'painting', 'walking', 'dressing', 'likely', 'children', 'whom', 'good']
for word in lst_words:
	stemmer.stem(word)

```

## sklearn

使用 sklearn 库实现朴素贝叶斯文本分类器（Naive Bayes Classifier）进行垃圾邮件过滤

```
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import classification_report

# ====================特征工程=====================

# train_test分割, 使用20%数据作为测试集
X_train, X_test, y_train, y_test = train_test_split(df.Message, df.spam, test_size=0.2)

# 初始化一个 CountVectorizer 对象
v = CountVectorizer()

# 使用 CountVectorizer 对训练集文本数据进行向量化
X_train_cv = v.fit_transform(X_train.values)

# 将向量化后的训练集数据转换为 NumPy 数组形式
X_train_np = X_train_cv.toarray()

# ===================初始化模型=====================

# 初始化一个 MultinomialNB 朴素贝叶斯模型
model = MultinomialNB()

# ====================训练=========================

# 使用训练集数据进行模型训练
model.fit(X_train_cv, y_train)

# =====================测试=========================
# 对测试集数据进行向量化
X_test_cv = v.transform(X_test)

# 使用模型对测试集进行预测
y_pred = model.predict(X_test_cv)

# 打印分类报告
print(classification_report(y_test, y_pred))

# ====================应用=========================
# 对新的邮件数据进行分类
emails = [
    'Hey mohan, can we get together to watch footbal game tomorrow?',
    'Upto 20% discount on parking, exclusive offer just for you. Dont miss this reward!'
]

# 对新的邮件数据进行向量化
emails_count = v.transform(emails)

# 使用模型进行预测
model.predict(emails_count)

# ==============================================================================
# ============================基于管道实现========================================
# ==============================================================================
from sklearn.pipeline import Pipeline
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.naive_bayes import MultinomialNB

# 特征工程
X_train, X_test, y_train, y_test = train_test_split(df.Message, df.spam, test_size=0.2)

# 特征工程 && 建模
clf = Pipeline([
    ('vectorizer', CountVectorizer()),
    ('nb', MultinomialNB())
])

# 训练
clf.fit(X_train, y_train)

# 应用
y_pred = clf.predict(X_test)

print(classification_report(y_test, y_pred))
```

使用基于KNN的Pipeline

```
clf = Pipeline([
	('vectorizer', CountVectorizer()),
	('KNN', (KNeighborClassifier(n_neighbors=10, metric='euclidean')))
])
clf.fit(x_train, y_train)

y_pred = clf.predict(x_test)

classification.report(y_test, y_pred)
```

使用基于朴素贝叶斯的Pipeline

```
clf = Pipeline([
	('vectorizer', CountVectorizer()),
    ('Multi NB', MultinomialNB())   #using the Multinomial Naive Bayes classifier
])
clf.fit(x_train, y_train)

y_pred = clf.predict(x_test)

classification.report(y_test, y_pred)
```



## 具体任务

### 自动提取 / 标记类别

```
import pandas as pd
...
df.[column-name].value_counts()
```



### 读取JSON文件

```
import pandas as pd
df = pd.read_json("path.json")

df.shape
df.head()
```

### 列文本-数字映射 / 创建新列

```
target = {
	"CATEGORYA": 0,
	"CATEGORYB": 1,
	...
}
# 将平衡的数据的column-name列通过target映射表进行映射，结果设置到数据的new_column上
df_balanced['new_column'] = df_balanced.['column-name'].map(target)
```



### 处理不平衡问题  / raw data预处理

```
欠拟合—以最少数据为标准，丢弃除此之外的类别的多余数据
min_samples = 111
# 随机采样，random_state是随机状态变量，可以理解为种子
df_a = df[df.[column-name1] == "category-name"].sample(min_samples, random_state=20231113) 
df_b = df[df.[column-name2] == "category-name"].sample(min_samples, random_state=20231113) 
df_c = df[df.[column-name3] == "category-name"].sample(min_samples, random_state=20231113) 
df_d = df[df.[column-name4] == "category-name"].sample(min_samples, random_state=20231113) 
df_e = df[df.[column-name5] == "category-name"].sample(min_samples, random_state=20231113) 

# 平衡数据
df_balanced = df.concat([df_a, df_b, df_c, df_d], axis=0)
# 预处理raw data
import spacy
nlp = spacy.load("en_core_web_sm")
def preprocess(text):
    doc = nlp(text)
    filter_tokens = []
    for token in doc:
        if token.is_stop or token.is_punc:
            continue
        filter_tokens.append(token.lemma_)
    return " ".join(filter_tokens)
df_balanced['preprocess_column'] = df_balanced.text.apply(preprocess_func)
```

### 训练-测试分割

```
from sklearn.model_selection import train_test_split

x_train， x_test, y_train, y_test = train_test_split(
	df_balanced_text,
	df_balanced_category,
	test_size=0.2,
	random_state=20231113,
	stratify=df_balanced_category   # 在训练和测试的所有类别中创建相同数量的样本
)

# 打印的shape列与列之间相同
y_train.value_counts()
y_test.value_counts()
```

### 使用分类模型拟合数据(训练)

```
from sklearn.naive_bayes import MultinomialNB
from sklearn.pipeline import Pipeline
from sklearn.metrics import classification_report

# 创建分类器
clf = Pipeline([
	("vectorizer-bow", Vectorizer()),
	("Multi NB", MultinomialNB())
])
# 训练
clf.fit(x_train, y_train)

# 测试
y_pred = clf.predict(x_test)
classification_report(y_test, y_pred)
```



### 拆分基本词 

```
import spacy
nlp = spacy.load("en_core_web_sm")

# 定义词形还原的处理函数
def preprocess(text):
    doc = nlp(text)
    filter_tokens = []
    for token in doc:
        if token.is_stop or token.is_punc:
            continue
        filter_tokens.append(token.lemma_)
    return " ".join(filter_tokens)

# 使用处理函数遍历文档
doc = [preprocess(text) for text in corpus]
```

### 获取词汇表

```
from sklearn.feature_extraction.text import CountVectorizer
 
# 创建词袋模型, ngram_range用于设置词袋的多元词的组合
v = CountVectorizer(ngram_range=(1,1)) # default setting
# 拟合数据
v.fit(["xxx xxx xx x x xxx x"])
v.vocabulary_
```

### 文本转向量

```
from sklearn.feature_extraction.text import CountVectorizer
 
v = CountVectorizer(ngram_range=(1,1)) # default setting
v.transform(["..."]).toarray()
```



# CV

## 模型训练一般流程（图片）

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
