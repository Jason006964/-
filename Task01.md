# 天池龙珠训练营金融风控学习笔记

##  一、学习知识点概要

### 了解赛题
* 赛题概况
* 数据概况
* 预测指标
* 分析赛题

### 评分卡

## 二、学习内容
### 了解赛题
* 赛题概况：
背景为个人信贷问题，根据申请人的数据信息预测违约的可能性，以判断是否能通过此项贷款。属于分类问题。

employmentTitle 就业职称
purpose 借款人在贷款申请时的贷款用途类别
postCode 借款人在贷款申请中提供的邮政编码的前3位数字
title 借款人提供的贷款名称

数据脱敏：是指对某些敏感信息通过脱敏规则进行数据的变形

* 数据概况
  * 读取数据 :
```
# 方法一：直接下载到dsw本地，这样的好处是后面数据读取会快点，但是直接下载到本地会占用比较多的内存
# 下载测试数据集 41.33mb
!wget http://tianchi-media.oss-cn-beijing.aliyuncs.com/dragonball/FRC/data_set/testA.csv
# 下载训练数据集 166.77mb
!wget http://tianchi-media.oss-cn-beijing.aliyuncs.com/dragonball/FRC/data_set/train.csv
```

```
train = pd.read_csv('train.csv')
testA = pd.read_csv('testA.csv')
```
```
# 方法二：使用pandas直接读取链接数据，这样的好处是不占dsw内存，但是读取速度相对比较慢
train = pd.read_csv('http://tianchi-media.oss-cn-beijing.aliyuncs.com/dragonball/FRC/data_set/train.csv')
testA = pd.read_csv('http://tianchi-media.oss-cn-beijing.aliyuncs.com/dragonball/FRC/data_set/testA.csv')
```
```
print('Train data shape:',train.shape)
print('TestA data shape:',testA.shape)
train.head()
```
* 预测指标：
竞赛以AUC作为评价指标
  * AUC（Area Under Curve）被定义为 ROC曲线 下与坐标轴围成的面积(<=1)。
  * 由于ROC曲线一般都处于y=x这条直线的上方，所以AUC的取值范围在0.5和1之间。AUC越接近1.0，检测方法真实性越高;等于0.5时，则真实性最低，无应用价值。
  * ROC空间:将假正例率（FPR）定义为 X 轴，真正例率（TPR）定义为 Y 轴。
  * TPR：在所有实际为正例的样本中，被正确地判断为正例之比率。
  * FPR：在所有实际为负例的样本中，被错误地判断为正例之比率。

分类算法常见的评估指标：混淆矩阵、准确率、精确率(查准率)、召回率(查全率)

P-R曲线：描述精确率和召回率变化的曲线

---
金融风控预测类常见的评估指标: KS、ROC、AUC
   * KS：用于评估模型区分度。区分度越大，说模型的风险排序能力越强(但是也不是越大模型效果就越好，如果KS过大，模型可能存在异常，所以当KS值过高可能需要检查模型是否过拟合)。
   * K-S曲线将真正例率和假正例率都作为纵轴，横轴则由选定的阈值来充当。

* 分析赛题：
了解赛题流程

### 评分卡
评分卡是一张拥有分数刻度会让相应阈值的表，信用评分卡则是用于用户信用的一张刻度表。
```
def Score(prob,P0=600,PDO=20,badrate=None,goodrate=None):
    P0 = P0
    PDO = PDO
    theta0 = badrate/goodrate
    B = PDO/np.log(2)
    A = P0 + B*np.log(2*theta0)
    score = A-B*np.log(prob/(1-prob))
    return score
```

## 三、学习问题与解答
* 学习完task1后发现自己对numpy库的函数调用并不是很熟悉，后续要花点时间复习一下
* 此前还没接触过pandas，后续要花时间大概过一遍
* scikit-learn，没接触过，但很重要，也挺难的

## 四、学习思考与总结
赛题的理解有助于对竞赛全局的把握,通过Task1的学习后，我大概地熟悉了比赛流程，通过Task1的赛题例子也大概了解了对赛题的理解和分析过程，包括比赛的评价指标，评分体系，有没有类似的比赛可以参考借鉴等等，也了解了如何处理数据以及如何大概地通过数据和体型建立模型
