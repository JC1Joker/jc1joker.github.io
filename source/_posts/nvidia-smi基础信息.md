---
title: nvidia-smi基础信息
date: 2023-06-08 09:49:01
tags: 
- shell
categories: 
---

![](nvidia-smi基础信息/nvidia.png)

> nvidia-smi 查看当前GPU使用情况
<!--more-->
```
GPU：GPU 编号；

Name：GPU 型号； 

Persistence-M：持续模式的状态。持续模式虽然耗能大，但是在新的GPU应用启动时，花费的时间更少，这里显示的是off的状态；

Fan：风扇转速，从0到100%之间变动；

Temp：温度，单位是摄氏度； 

Perf：性能状态，从P0到P12，P0表示最大性能，P12表示状态最小性能（即 GPU 未工作时为P0，达到最大工作限度时为P12）。 

Pwr:Usage/Cap：能耗；

Memory Usage：显存使用率； 

Bus-Id：涉及GPU总线的东西  Disp.A：Display Active，表示GPU的显示是否初始化；

Volatile GPU-Util：浮动的GPU利用率；

Uncorr. ECC：Error Correcting Code，错误检查与纠正； 

Compute M：compute mode，计算模式

```

