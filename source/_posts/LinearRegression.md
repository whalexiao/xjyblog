---
title: LinearRegression
date: 2020-03-05 09:28:44
tags: Machine Learning
mathjax: true
---
**Supervised Learning**  
Given the “right answer” for each example in the data.  
**Regression Problem**  
Predict real-valued output  
Gradient descent: 梯度下降
Feature Scaling：特征缩放
Learning Rate：学习率
Batch Gradient descent: Each step of gradient descent uses all the training examples.
<!-- more -->
## 1.公式
![Formula](Formula.PNG)   
## 2.最优化更新
梯度下降   
### 单变量
![Gradient-Descent](Gradient-Descent.PNG)  
对于含有i个参数的，$ \Theta_i $ 的更新法则和$ \Theta_1 $是一样的 
### 多变量
![Muti](Muti.PNG)
$ x^{(i)}_j $表示第i个样本的第j个特征，当j=0时候，xij=1   
这种方法叫做“Batch” Gradient Descent 
**“Batch”: Each step of gradient descent uses all the training examples.**
迭代停止可以通过计算每次目标函数的减小小于某个数，或者设置最大的迭代次数
## 3.推导
![Infer](infer.png)
下面是从最大似然估计的角度求得的损失函数
![MLE](MLE-Infer.PNG)
## 4.注意
### Feature Scaling
Ag表示使用特征缩放，让所有的特征大致位于一个范围可以使得梯度下降进行的更好，但是并未给出严格的数学证明，下面一张图大致能够解释原因：  
**进行缩放之后得到的函数，在进行预测时也需要带入缩放后的特征**
![Feature-Scaling](Feature-Scaling.PNG)
我的理解是：如果某一维度上取值较大时，在更新对应的参数$ \Theta $ 时，步长也较大，此时就会出现在大维度参数上震荡的情况，导致路线曲折地通往极值点。  
如果所有维度的取值范围相近，就不会出现震荡的情况，路线就会笔直地通往极值点。知乎上这篇文章说的比较详细 https://zhuanlan.zhihu.com/p/25234554  
特征缩放的方式还是有很多的，这里给出Ag举出的均值归一化  
- Mean normalization
    Replace $x_i$ with $x_i-\mu-i$ to make features have approximately zero mean (Do not apply to $x_0=1$ ).

### Learning Rate
- If a is too small: slow convergence.
- If a is too large: $ J(\Theta) $ may not decrease on every iteration; may not converge.
因为当学习率比较大的时候，在接近极小值时，因为步长比较大，会跳到极值点的另一侧，这时候倒数项也会变大，从而导致theta在两侧波动，最终发散。
![Learning-Rate](Learning-Rate.PNG)
<font size=6>**To choose a, try
...0.001,0.003,0.01,0.03,0.1,0.3...**</font>
## 5.多项式拟合
![Polynomial-Regression](Polynomial-Regression.PNG)
相当于是用了换元的思想，本质上还是Linear-Regression  
## 6.Normal Equation
因为线性回归比较简单，所以数学上可以解出来极值点。   
![Normal-Equation](Normal-Equation.PNG)
### 推导
![infer1](infer1.PNG)
![infer2](infer2.PNG)
![Compare](Compare.PNG)  
What if$X^TX$is non-invertible?  
- Redundant features (linearly dependent).(存在冗余，各个feature之间线性不独立)
- Too many features (Delete some features, or use regularization.)

