---
title: Pandas笔记
date: 2023-06-07 11:56:19
categories: #分类 
- Python
tags: #标签
- 数据分析
- Pandas
---

> 中国大学MOOC,python数据分析相关课程笔记--pandas部分
<!--more-->
## pandas库
pd.Series()# pd.series是pandas中用于表示一维数据的数据结构

d.cumsum()计算前n项累加和

[^1]: axis = 0 代表对横轴操作，也就是第0轴；axis = 1 代表对纵轴操作，也就是第1轴；

## 理解

两个数据类型：Series，DataFrame

基于商促数据类型的各类操作

基本操作、运算操作、特征类操作、关联类操作

|                 Numpy                  |       Pandas       |
| :------------------------------------: | :----------------: |
|              基础数据类型              |    扩展数据类型    |
| 关注数据的结构表达(数据之间的维度表达) | 关注数据的应用表达 |
|           基于**维度**的运算           | 基于**索引**的运算 |

## series类型

由一组数据及与之相关的数据索引组成

index_0  data_a

index_1 data_b

- python 列表，index与列表元素个数一致
- 标量值，index表达Series类型的尺寸
- python字典，键值对中的“键”是索引，index从字典中进行选择操作
- ndarray，索引和数据都可以通过ndarray类型创建
- 其他函数，range()函数等



### 从ndarray类型创建

```python
import pandas as pd
import numpy as np
n = pd.Serise(np.arange(5))

输出：
0  0
1  1 
2  2 
3  3 
4  4 
```

## Series类型对齐操作

Series+Series

Series类型在运算中会自动对齐不同索引的数据

## name属性(.name)

Series对象和索引都可以有一个名字，存储在属性.name中

Series是一维带“标签”数组

Series基本操作类似ndarray和字典，根据索引对齐

DataFrame类型

二维ndarray对象

由一维ndarray、列表、字典、元组或series构成的字典

## 如何改变Series和DataFrame对象

增加或重排：重新索引

### 重新索引

.reindex()

.reindex(希望排列之后的index关系)能够改变或者重排Series和DataFrame索引

| 参数          | 说明                                            |
| ------------- | ----------------------------------------------- |
| index,columns | 新的行列自定义索引                              |
| fill_value    | 重新索引中，用于填充缺失位置的值                |
| method        | 填充方法，ffill当前值向前填充，bfill向后填充    |
| limit         | 最大填充量                                      |
| copy          | 默认True，生成新的对象，False时，新旧相等不复刻 |

## 索引类型

Series和DataFrame的索引时index类型

index对象是不可修改类型

常用方法

| 方法               | 说明                                   |
| ------------------ | -------------------------------------- |
| .append(idx)       | 连接另一个index对象，产生新的index对象 |
| .diff(idx)         | 计算差集，产生新的index对象            |
| .intersection(idx) | 计算交集                               |
| .union(idx)        | 计算并集                               |
| .delete(loc)       | 删除loc位置处的元素                    |
| .insert(loc.e)     | 在loc位置增加一个元素                  |

## 删除指定索引对象

.drop()能够删除Series和DataFrame指定行或列索引

## pandas数据运算

算数运算法则

算术运算根据行列索引，补齐后运算，运算默认产生浮点数

补齐时缺项填充NaN（空值）

二维和一维、一维和零维间的广播运算

采用+-*/符号进行的二元运算产生新的对象

| 方法            | 说明                     |
| --------------- | ------------------------ |
| .add(d,**argws) | 类型间加法运算，可选参数 |
| .sub(d,**argws) | 类型间减法运算，可选参数 |
| .mul(d,**argws) | 类型间乘法运算，可选参数 |
| .div(d,**argws) | 类型见除法运算，可选参数 |

## 比较运算法则

比较运算只能比较相同索引的元素，不进行补齐。

二维和一维、一维和零维间的广播运算

采用><>=<= == !=等符号进行的二元运算产生布尔对象

## 小结

Series = 索引+一维数据

DataFrame = 行列索引 + 二维数据

理解数据类型与索引的关系，操作索引即操作数据

像对待单一数据一样对待Series和DataFrame对象



## 数据排序

.sort_index()方法在指定轴上根据索引进行排序，默认升序

.sort_index(axis=0,ascending=True)

ascending=False降序

.sort_values()方法在指定轴上根据数值进行排序，默认升序

Serious.sort_values(axis=0,ascending=True)

DataFrame.sort_values(**by**,axis=0,ascending=True)

by:axis轴上的某个索引或索引列表

NaN统一放到排序末尾

## 基本的统计分析函数

适用Series和DataFrame类型

| 方法              | 说明                             |
| ----------------- | -------------------------------- |
| .sum()            | 计算数据的总和                   |
| .count()          | 非NaN值的数量                    |
| .mean() .median() | 计算数据的算术平均值、算数中位数 |
| .var() .std()     | 计算数据的方差、标准差           |
| .min() .max()     | 计算数据的最小值、最大值         |

统计汇总

| .describe | 针对0轴(各列)的统计汇总[^1] |
| --------- | --------------------------- |

累计统计分析函数

| 方法       | 说明                              |
| ---------- | --------------------------------- |
| .cumsum()  | 依次给出前1、2、……、n个数的和     |
| .cumprod() | 依次给出前1、2、……、n个数的积     |
| .cummax()  | 依次给出前1、2、……、n个数的最大值 |
| .cummin()  | 依次给出前1、2、……、n个数的最小值 |

滚动计算（窗口计算）

| 方法                    | 说明（跨行运算）                    |
| ----------------------- | ----------------------------------- |
| .rolling(w).sum()       | 依次计算相邻w个元素的和             |
| .rolling(w).mean()      | 依次计算相邻w个元素的算数平均值     |
| .rolling(w).var()       | 依次计算相邻w个元素的方差           |
| .rowing(w).std()        | 依次计算相邻w个元素的标准差         |
| .rowing(w).main().max() | 以此计算相邻w个元素的最小值和最大值 |

## 相关分析

两个事物，表示x和y，如何判断它们之间的存在相关性

**相关性**

- x增大，y增大，两个变量正相关
- x增大，y减小，两个变量负相关
- x增大，y无视，两个变量不相关

**协方差**

两个事物，表示x和y，如何判断它们之间的存在相关性









