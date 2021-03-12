---
title: LogisticRegression
date: 2020-03-05 15:26:52
tags: Machine Learning
mathjax: true
---
MLE:Maximum Likelihood Estimate
Cross Entropy Loss:交叉熵损失函数
MSE:Mean Square Error 均方误差
Convex：凸的
non-convex：非凸的
Conjugate gradient:共轭梯度
BFGS
L-BFGS
<!--more-->
## 公式
![formula](Formula.png)
## 梯度下降
![Gradient-Descent](Gradient-Descent.PNG)
这里Ag把学习率从线性的a换成了a/m，因为是常数所以没有影响。
## 推导
### cost function
![Cost-Function](Cost-Function0.PNG)

![Cost-Function](Cost-Function1.PNG)

![Cost-Function](Cost-Function2.PNG)
下面是从最大似然估计的角度得到的交叉熵损失函数的推导：
![MLE](MLE-Infer.jpg)
### 梯度更新
![infer](infer.PNG)
## One Vs All
![OneVsAll1.PNG](OneVsAll1.PNG)
![OneVsAll2.PNG](OneVsAll2.PNG)
$ h(\Theta)_i $相当于计算第i类的概率，自然是选择概率最大的归为那一类
## Advanced optimization
梯度下降的高级优化算法：
![AO](Advanced-Optimization.PNG)
