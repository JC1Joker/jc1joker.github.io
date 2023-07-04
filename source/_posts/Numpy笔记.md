---
title: Numpy笔记
date: 2023-06-29 10:09:04
tags:
- 数据分析
- Numpy
categories:
- Python
---
![](Numpy笔记/NumPy_logo_2020.png)
> MOOC课程，数据分析相关课程，Numpy笔记

<!--more-->
## 统计函数

|         函数         |                         说明                          |
| :------------------: | :---------------------------------------------------: |
|   sum(a,axis-None)   |  根据给定轴axis计算数组a相关元素之和，axis整数或元组  |
|  mean(a,axis-None)   | 根据给定轴axis计算数组a相关元素的期望，axis整数或元组 |
| average(a,axis=None) |      根据给定轴axis计算数组a相关元素的加权平均值      |
|   std(a,axis=None)   |        根据给定轴axis计算数组a相关元素的标准差        |
|   var(a,axis=None)   |         根据给定轴axis计算数组a县官元素的方差         |

## 随机函数

| 函数                    | 说明 |
| ----------------------- | ---- |
| np.random.rand()        |      |
| np.random.randn()       |      |
| np.random.randint()     |      |
| np.random.seed()        |      |
| np.random.shuffle()     |      |
| np.random.permutation() |      |
| np.random.choice()      |      |

## random梯度函数

| 函数           | 说明                                                 |
| -------------- | ---------------------------------------------------- |
| np.gradient(f) | 计算数组f中元素的梯度，当f为多维时，返回每个维度梯度 |

梯度：连续值之间的变化率，即斜率

XY坐标轴连续三个X坐标对应的Y轴值：a，b，c，其中，b的踢肚时：(c-a)/2

## 小结

数据存取与函数

- CSV文件
- np.loadtxt()
- np.savetxt()

多维数组存取

- a.tofile()
- np.fromfile()
- np.save()
- np.savez()
- np.load()

## 图像的数组表示

图像是一个三维数组，维度分别是高度、宽度和像素RGB值

示例代码：

```python
from PIL import Image
import numpy as np
im=np.array(Image.open("D:/"))
print(im.shape,im.dtype)
#输出(699,1012,3)uint8
```

## 图像的变换

读入图像后，获得像素RGB值，修改后保存为新的文件

```python
from PIL import Image
import numpy as np
im=np.array(Image.open("D:/"))
print(im.shape,im.dtype)

b=[255,255,255]-a #这是一个三维数组RGB的补值

im = Image.fromarray(b.astype('uint8'))
im.save('b.jpg')
#输出(699,1012,3)uint8
```

## 图像手绘风格

`梯度的重构`

> 利用像素之间的梯度值和虚拟深度值对图像进行重构，根据灰度变化来模拟人类视觉的明暗程度



```python
a= np.asarray(Image.open('ins.jpg').convert('L')).astype('float')

depth = 10.         #(0-100)预设深度值为10
grad = np.gradient(a)      #取图像灰度的梯度值，提取x和y方向的梯度值
grad_x , grad_y = grad      # 分别取横纵图相梯度值
grad_x = grad_x*depth/100.#根据深度调整x和y方向的梯度值
grad_y = grad_y*depth/100.
A = np.sqrt(grad_x**2 + grad_y**2 + 1.)

uni_x = grad_x/A
uni_y = grad_y/A
uni_z = 1./A

vec_e1 = np.pi/2.2                  #光源的俯视角度，弧度值
vec_az = np.pi/4.                   # 光源的方位角度，弧度值
dx = np.cos(vec_e1)*np.cos(vec_az) # 光源对x轴的影响 np.cos(vec_e1)为单位光线在地平面上的投影长度
dy = np.cos(vec_e1)*np.sin(vec_az) # 光源对y轴的影响
dz = np.sin(vec_e1)             #光源对z轴的影响

b = 255*(dx*uni_x + dy*uni_y + dz*uni_z)# 光源归一化
b = b.clip(0,255) #clip 截断，限制数组的上下界,减少像素溢出

im = Image.fromarray(b.astype('uint8'))  #重构图像
im.show()
# im.save('11.jpg')
```

光源效果：

根据灰度变化来模拟人类视觉的远近程度

# matplotlib.pyplot

## pyplot绘图区域

plt.subplot(nrows.ncols,lot_number)

## plot

plt.plot(x,y,format_string,**kwargs)

* x:X轴数据，列表或数组，可选

* y:Y轴数据，列表或数组

* format_string：控制曲线的格式字符串，可选，由颜色字符、风格字符和标记字符组成

  * 颜色字符对应英文首字母

  * 风格字符

  `-`实线

  `--`破折线

  `-.`点划线

  `:`虚线

  * 格式字符串

  `.`点标记

  `,`像素标记

  `o`实心圈标记

  `v`倒三角标记

  `^`上三角标记

  `>`右三角标记

  `<`左三角标记

  `1`下花三角标记

  `2`上花三角标记

  `3`左花三角标记

  `4`右花三角标记

  `s`实心方形标记

  `p`实心五角标记

  `*`星形标记

  `h`竖六边形标记

  `H`横六边形标记

  `+`十字标记

  `x`x标记

  `D`菱形标记

  `d`瘦菱形标记

  `|`垂直线标记

  

* **kwargs：第二组或更多（x,y,format_string）

  * color：控制颜色，color=‘green’
  * linestyle：线条风格，linestyle=‘dashed’
  * marker：标记风格，marker=’o‘
  * markerfacecolor：标记颜色，markerfacecolor=’blue‘
  * markersize：标记尺寸，markersize=20
  * ……

  

当绘制多条曲线时，各条曲线的x不能省略

### pyplot中文显示方法

- 方法一：需要**rcParams**修改字体实现

| 属性(单引号需加上) | 说明                                     |
| ------------------ | ---------------------------------------- |
| ‘font.family’      | 用于显示字体的名字                       |
| ’font.style‘       | 字体风格，正常’normal‘或 斜体’italic‘    |
| ’font.size‘        | 字体大小，整数字号或者’large‘、’x-small‘ |



- 方法二：在有中文输出的地方，增加一个属性：fontproperties

```python
plt.xlabel("横轴(值)",fontproperties='SimHei',fontsize=20)
plt.ylabel("grade",,fontproperties='SimHei',fontsize=20)
```

## pyplot的文本显示方法

| 函数           | 说明                   |
| -------------- | ---------------------- |
| plt.xlabel()   | 对x轴添加文本标签      |
| plt.ylabel()   | 对y轴添加文本标签      |
| plt.title()    | 对图形整体增加文本标签 |
| plt.text()     | 在任意位置增加文本     |
| plt.annotate() | 在图形中增加带箭头注释 |

> LaTeX语法 
>
> $正弦波实例 y = cos(2pix)$



```
import matplotlib.pyplot as plt
plt.annotate()
```

![image-20220504183915496](C:\Users\JC\AppData\Roaming\Typora\typora-user-images\image-20220504183915496.png)

plt.subplot2grid(GridSpec,CurSpec,colspan=1,rowspan=1)

理念：设定网格，选中网格，确定选中行列区域数量，编号从0开始

## GridSpec类

实行多种格子

## pyplot基础图表函数

| 函数                               | 说明                         |
| ---------------------------------- | ---------------------------- |
| plt.plot(x,y,fmt,...)              | 绘制一个坐标图               |
| plt.boxplot(data,notch,position)   | 绘制一个箱型图               |
| plt.bar(left,height,width,bottom)  | 绘制一个条形图               |
| plt.barh(width,bottom,left,height) | 绘制一个横向条形图           |
| plt.polar(theta,r)                 | 绘制极坐标图                 |
| plt.pie(data,explode)              | 绘制饼图                     |
| plt.psd(x.NFFT=256,pad_to,Fs)      | 绘制功率谱密度图             |
| plt.specgram(x.NFFT=256,pad_to,Fs) | 绘制谱图                     |
| plt.cohere(x,y,NFFT=256,Fs)        | 绘制x-y相关性函数            |
| plt.step(s,y,where)                | 绘制步阶图                   |
| plt.hist(x,bins,normed)            | 绘制直方图                   |
| plt.scatter(x,y)                   | 绘制散点图，其中x和y长度相同 |
| plt.contour(X,Y,Z,N)               | 绘制等值图                   |
| plt.vlines()                       | 绘制垂直图                   |
| plt.stem(x,y,linefmt,markerfmt)    | 绘制柴火图                   |
| plt.plot_date()                    | 绘制数据日期                 |

startangle=90 起始角度

bin:直方图的个数

normed：纵坐标出现元素的个数

