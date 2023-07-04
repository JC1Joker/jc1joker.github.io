---
title: conda的使用技巧
date: 2023-06-20 10:10:39
tags: 
- Shell
categories: 
- Python
---
![](conda的使用技巧/anaconda.png)
> anaconda的换源，创建环境

<!--more-->

# Win常用conda命令


## 1.查看当前环境下安装的工具

> pip list

或

> conda list



## 2.创建虚拟环境

> conda create --name[环境名称]

例

> conda create --name hacker



> `conda create -n 新的环境名 python=指定版本（2.7/3.6/3.7）` # 注意需要在base中运行，不能在虚拟环境中执行

即可创建一个名为hacker的虚拟环境

## 3.修改环境名称

> conda create --name newName（新环境名） --clone oldName（旧环境名）



## 4.删除环境

> conda remove --name oldName（旧环境名） --all 

## 5.查看虚拟环境

> conda env list
>
> conda info -e

其中带有*** **的表示当前所用的环境

## 6.切换环境

使用activate(激活)加上要切换的环境名称，即可切换

> conda activate[环境名称]

例

> conda activate learn 



## 7.退出虚拟环境

> conda deactivate



## 8.移除虚拟环境

> conda remove --name [环境] --all

例

> conda remove --name learn --all



## 9.包的安装

（无需进入环境）

> conda install [包名] -n [环境名]

## 10.包的更新

> conda update --all

## 11.包的删除

> conda remove [包名]

## 12.查看可以安装的python版本 

>  conda search --full-name python`

## 13.镜像源

### 查看当前conda源

> conda config --show

### 恢复默认源

> conda config --remove-key channels

### 中科大源

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
conda config --set show_channel_urls yes

### 清华源

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

###  腾讯云

```
conda config --add channels https://mirrors.cloud.tencent.com/anaconda/pkgs/free/
conda config --add channels https://mirrors.cloud.tencent.com/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

## 14清理conda缓存

```shell
conda clean -p     
conda clean -t      
conda clean -y -all 
 # 删除没有用的包 --packages
 # 删除tar打包 --tarballs
 # 删除所有的安装包及cache(索引缓存、锁定文件、未使用过的包和tar包)
```

## 15.pip国内源

阿里云 ：http://mirrors.aliyun.com/pypi/simple/
中国科技大学： https://pypi.mirrors.ustc.edu.cn/simple/
豆瓣(douban) ：http://pypi.douban.com/simple/
清华大学 ：https://pypi.tuna.tsinghua.edu.cn/simple/
中国科学技术大学： http://pypi.mirrors.ustc.edu.cn/simple/

```shell
# 使用豆瓣源安装
pip install opencv-python -i http://pypi.douban.com/simple 
# 报错说不信任该源，执行如下：
pip install opencv-python -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

## 16.修改python版本

```shell
#1.新建一个anaconda虚拟环境，指定Python版本
conda create -n envTest python=3.5
#2.直接将现有的anaconda中python更改为3.5
sudo conda install python=3.5
#3.下载并安装对应Python版本的anaconda，anaconda4.2->python3.5
#https://repo.continuum.io/archive/
```

## 17.打开交互界面

> anaconda-navigator

## 18.临时更换pip源

> pip install 库 -i http://pypi.douban.com/simple --trusted-host pypi.douban.com