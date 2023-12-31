## Sentiment Analysis of Twitter Data for Predicting Stock Market Movements

### 摘要

预测股市活动。

社交网络代表了公众情感和观点。

尤其是推特。

基于推特表达出来的公共情绪的股票预测已经成为耐人寻味的研究领域。

以前的研究得出结论，聚合推特公共情绪和DJIA正相关。这项研究的主题是观察一个公司股票的涨跌和被在推上表达的对这个公司的观点有多相关。

从文本中理解作者的观点， 是情感分析的目标。

本文使用两个不同的文本表示，Word2vec 和N-gram，来分析推特公众情绪。本文中，我们在推文上使用情感分析和监督机器学习，并分析股市波动和推文情感的关联。

社交媒体上关于一个公司的正面新闻和推文肯定会鼓励人们投资于该公司的股票，因此该公司的股票价格会上升。本文最后表明，股票价格的涨跌与推文中的公众情绪之间存在着强烈的相关性。

### 介绍

### 相关工作

### 数据收集

2015.8.31-2016.8.25关于微软的推文，从twitter API 获取, 用正则表达式过滤。

twitter4j

推文

- 表达了特定的情感
- 包含有关微软的新闻
- 有关产品发布的推文

股票

- 2015.8.31-2016.8.25
- Yahoo！ 金融

### 数据预处理

- 股市不开放日：假设股票遵循凸函数趋势，简单近似填充
- 分词：根据空格和无关符号，划分成单词；去除表情符号等。每个推文形成一个单词列表。
- 去除stopwords：从单词列表中删除不表达任何感情的词。"a"、"is"、"the"、"with"
- 正则表达式删除字符 hashtag--> 去掉#； 提到某人，替换为USER；强烈感情cooooool --> cool.

### 情感分析

#### A 特征抽取

推文根据其所表达的情感被分类为积极、消极和中性

3216条：人工标注为1表示积极情感，0表示中性情感，2表示消极情感

剩下的用机器学习模型标注，模型从人工标注的推文中提取信息。

- N-gram。语料库包含了所有推文的N-gram。推文被分成N-gram, 模型特征是1 和 0 的字符串，1表示该N-gram存在于语料库中的推文中，0表示不存在。
- word2vec .推文中所有单词的300维向量之和作为特征提供给模型。

#### B 训练模型

以上从人工标注推文抽取的特征，输入随机森林模型，为未标注数据打标签。选择使用Word2vec表示训练的模型，因为它在大型数据集上具有可持续的意义和良好的性能。测试集准确率70.2%, 而人类对文本情感的一致程度70-79%，认为模型良好。

### 价格和情感的相关性分析

t天时间段内，统计推文中总积极，消极，和中性情感，作为分类器模型的特征，输出是下一天的标记值。

进行不同t的实验，t=3效果最好。

355个实例，每个实例3个属性，2:8划分 训练测试集。

#### 结果

#### A 情感分析结果

测试集准确率70.2%, 而人类对文本情感的一致程度70-79%，认为模型良好。

#### B 价格情感相关性结果

逻辑回归：69.01%

LibSVM: 71.82%

### 结论

贡献：情感分析器，判断文中存在的情感类型；推特上公众对公司的情绪确实或反映在公司股价上。

### 进一步工作

1. 仅考虑了推特数据，考虑加入stockwits、新闻数据
2. 情感分析器训练集太小。