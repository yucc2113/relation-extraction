# <center> 命名实体识别
### 常见数据集
- CoNLL 2003(https://www.clips.uantwerpen.be/conll2003/ner)
  * 包括1393篇英语新闻文章和909篇德语新闻文章。英语资料免费
  * 实体被标注为4中类型：LOC, ORG, PER, MISC(miscellaneous,其他)
- OntoNotes 5.0 /CoNNLL 2012(https://catalog.ldc.upenn.edu/ldc2013t19)
    * 该数据集有1745k英语、900k中文和300k阿拉伯语文本数据组成
    * 数据来源多种多样，有电话对话，新闻通讯社，广播新闻，广播对话和博客
    * 实体被标注为【PERSON】【ORGANIZATION】和【LOCATION】等18个类别，详见
- NLPBA 2014
- Enron Emails

### 标注方法
- IOB标注法
  * 是CoNLL 2003 采用的标注法
- BIOES
  * 是在IOB方法上扩展的标注方法。B表示实体的开始，I表示内部，O表示外部，E表示实体结束，S表示这个词自己就可以组成一个实体
  * 是目前最通用的命名实体标注方法
- Markup
  * 是OntoNotes使用的标注方法，思路比较简单,XML。用标签把实体框出来，然后在TYPE上，设置相应的类型
- 其他的标注方法，如IO,BMEWO等

### 模型
**1. NCRF++**
目前业界比较常用的模型是LSTM+CRF。在这类模型中，NCRF++算法，是目前最好的NER算法，发表在CONLLNG 2018上，论文见 : https://arxiv.org/abs/1806.04470。 NCRF++在论文报告其在CoNLL2003上能达到91.35的F1。
- 源码：https://github.com/jiesutd/NCRFpp
- NCRF++框架图
![NCRF++框架图](https://github.com/jiesutd/NCRFpp/raw/master/readme/architecture.png)
- 它支持BIO(注意BIO和IOB有点区别)和BIOES两种模式。因为CoNLL2003太过久远，一般将其转换到新的标注格式上来，转换方法见: https://github.com/jiesutd/NCRFpp/blob/master/utils/tagSchemaConverter.py
