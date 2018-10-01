#   关系抽取简介
## 1. 基本介绍
---
### 1.1 常用数据集
1. ACE 2005: 599 docs. 7 types
2. SemiEval 2010 Task8 Dataset :
    - 19 types
    - train data(8000)
    - test data(2717)
3. MYT+FreeBase通过Distant Supervised method 提取，里面会有噪音数据:
   - 53 types
   - train data:522611 sentences
   - test data:172448 sentences

### 1.2文章中常见的学习方法
* Fully Supervised Learning
* Distant Supervised Learning
* Joint Learning with entity and relation
* Tree Baed Methods

其中Fully Supervised 一般评测使用label完全准确的 SemiEval 2010 Task 8数据集;Distant Supervised使用MYT+FreeBase数据集。

## 2. Fully Supervised Learning
---

相关文献 :这一部分基本上是在SemiEval 2010 Task 8数据集上做关系分类的工作，是一个完全监督的任务

### 2.1.Simple CNN  Model

> Liu,(2013). Convolution neural network for relation extraction. 8347 LNALI(PART 2),231-242

**基本介绍**：这篇文章是第一次用CNN来做关系分类任务的，使用的CNN结构也十分简单，甚至没有Pooling层，输入层也没有用word Embedding,而是对synonym的embedding表示作为输入。具体的输入层结构如下：
![enter image description here](http://cdn.htliu.cn/blog/relation-extraction/1.jpg)
具体步骤如下：
* 首先构建synonym list,使用wordnet数据集，来找哪些词属于同义词，相当于利用同义词关系，聚成若干类，当然有可能会有某个词没有同义词，那他自己就是一个类别
* 假设synonym list一共有【Math Processing Error]个类别，每个词都属于其中一类，这样就可以对词做one-hot表示了
![enter image description here](http://cdn.htliu.cn/blog/relation-extraction/2.png)
* 使用一个Look-up Table转换为一个低维vector


输入层之后是卷积网络+一个普通的全连接层以及softmax分类，如下：![enter image description here](http://cdn.htliu.cn/blog/relation-extraction/3.jpg)

**实验**
数据集：ACE 2005数据集，这篇文章除了使用前面所说的Synonym之外,还用了该数据集提供的entity type/subtype 以及后续做了POS tagger的特征，都是先使用one-hot表示,然后用LookUp Table再转换为低维向量，然后所有的feature vector concat成最终的向量，作为CNN层的输入。在大类Type上的实验结果，相对于几个Baseline提升还是比较明显的
![enter image description here](http://cdn.htliu.cn/blog/relation-extraction/4.png)

**总结**
优点：
  * 引入CNN结构来做关系抽取，虽然本质上属于文本分类，但是属于一次尝试，效果还可以
  * 引入Synonym Embedding作为词的特征，这一点在后续一部分工作中也在使用，相当于引入额外信息

缺点：
  * CNN结构比较简单，没有Pooling层，可能受噪音比较明显，因为一个句子里面影响两个词关系的可能只有几个词
  * 仍然使用了一些Linguistic Feature比如POS Tagger， NER等，并没有完全做到end-to-end的关系抽取
  * 使用Synonym Embedding(随机初始化的LookUp Table)可以引入一部分额外信息，但是却完全忽略了word embedding的语义信息，这一块在后续的工作中都会加入pre-train的word embedding

### 2.2 CNN with Max Pooling and word embedding(Zeng 2004)
> Zeng,(2014).Relation Classification via conlolutional Deep Neural network. Coling,2335-2344

这篇是中科院刘康老师的一篇论文，使用了比较经典的CNN结构，包含Pooling层，以及设计了Position Features,后面会具体介绍，整体框架：
![enter image description here](http://cdn.htliu.cn/blog/relation-extraction/5.jpg)

* 第一步
* 之后
* 最后

先介绍相对简单的Lexical Feature,一共有5部分
* L1
* L2
* L3
* L4
* L5

**总结**
优点：
* 使用了
* 引入

缺点：
* 虽然
* 结构简单

### 2.3 CNN with multi-sized window kernels(Nguyen 2015)
### 2.4 CNN with Rank loss(Santos 2015)
### 2.5 RNN(Zhang 2015)
### 2.6 BiLSTM Attention(Zhou 2016)
### 2.7 Multi-level Attention CNN(Wang 2016)
### 2.8 Attention CNNs(Zhu 2017)

## 3.Distant Supervised Learning
---
**相关文献**
#### 3.1 Piecewise Convolutional Neural Networks
> Zeng(2015).Distant Supervised for Relation Extraction via Piecewise Convolutional Neural Networks.EMNLP 
