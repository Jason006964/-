# 金融风控训练营Task02数据分析学习笔记
本学习笔记为阿里云天池龙珠计划Docker训练营的学习内容，学习链接为：
https://tianchi.aliyun.com/specials/activity/promotion/aicampfr?spm=5176.12901015.0.i12901015.419b525cZREgQM

## 一、学习知识点概要
* 数据总体了解                                              
* 缺失值和唯一值
* 数据类型
* 数据间相关关系
* 数据报告

## 二、学习内容
### 知识点
* TSV是用制表符（Tab,'\t'）作为字段值的分隔符；CSV是用半角逗号（','）作为字段值的分隔符；
* pandas:通过nrows参数，来设置读取文件的前多少行，nrows是一个大于等于0的整数。
### 数据总体了解
* 查看数据集的样本个数和原始特征维度
* 查看一下具体的列名
```
data_train.columns
```
* 查看数据类型
```
data_train.info()
```
* 查看数据集各个特征的一些基本统计量
```
data_train.describe()
```
### 缺失值和唯一值
* 需要查看缺失值、缺失特征和缺失率
* 对缺失值的可视化
```
missing = data_train.isnull().sum()/len(data_train)
missing = missing[missing > 0]
missing.sort_values(inplace=True)
missing.plot.bar()
```

### 数据类型
* 特征一般都是由类别型特征和数值型特征组成，数值型特征分为**连续型**和**离散型**。
* 特征分箱（数值型特征本是可以直接入模的，但往往风控人员要对其做分箱，转化为WOE编码进而做标准评分卡等操作。）：降低变量的复杂性，减少变量噪音对模型的影响，提高自变量和因变量的相关度。从而使模型更加稳定。
* **数值连续型变量分析**
```
f = pd.melt(data_train, value_vars=numerical_serial_fea)
g = sns.FacetGrid(f, col="variable",  col_wrap=2, sharex=False, sharey=False)
g = g.map(sns.distplot, "value")
```

### 数据报告
使用pandas_profiling模块

## 三、学习问题与解答
* 对nan缺失值可视化的作用：纵向了解哪些列存在 “nan”, 并可以把nan的个数打印，主要的目的在于查看某一列nan存在的个数是否真的很大，如果nan存在的过多，说明这一列对label的影响几乎不起作用了，可以考虑删掉。如果缺失值很小一般可以选择填充。
* 对特征的数值类型和对象类型分析以及特征量分布的可视化部分数据量有点多，代码也稍微有些复杂，有点容易让人混乱
* 对matplotlib比较陌生，所以代码看得有点累，必须要多抽时间看看文档
## 四、学习思考与总结
task02学习了对数据整体概况和一些变量的基本情况、相互关系等的分析，包括数据的可视化思想，
遇到了点python语法上的问题，也顺带复习了一下python，
而到目前为止的学习来说，感觉方法多而杂，知识体量大而乱，然后python的库的运用也不是特别的熟悉，所以依然是觉得有点迷茫，
当拿到题目和数据的时候可能仍然是会无从下手
