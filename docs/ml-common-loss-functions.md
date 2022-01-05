# ML |常见损耗函数

> 原文:[https://www.geeksforgeeks.org/ml-common-loss-functions/](https://www.geeksforgeeks.org/ml-common-loss-functions/)

损失函数估计特定算法对所提供数据的建模程度。损失函数根据学习任务的类型分为两类–

*   **回归模型:**预测连续值。
*   **分类模型:**预测一组有限分类值的输出。

**回归损失:**T2】

*   **均方误差**
    又称**二次损失或**L2 损失。
    是预测值和实际观测值之间的平方差的平均值

<center>

(1) ![\begin{equation*} M S E=\frac{\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}}{n} \end{equation*}](img/6edc5cbc6013d1c21ecd4a045cce8315.png "Rendered by QuickLaTeX.com")

</center>

## 蟒蛇 3

```
import numpy as np

# Mean Squared Error

def mse( y, y_pred ) :

    return  np.sum( ( y - y_pred ) ** 2 ) / np.size( y )

```

```
where,
i        - ith training sample in a dataset
n        - number of training samples
y(i)     - Actual output of ith training sample
y-hat(i) - Predicted value of ith traing sample
```

*   **平均绝对误差**
    又称 **L1 损失**。
    是预测值与实际观测值绝对差的平均和。

<center>

(2) ![\begin{equation*} M A E=\frac{\sum_{i=1}^{n}\left|y_{i}-\hat{y}_{i}\right|}{n} \end{equation*}](img/08ba6245d8912bba9c133ee9a4b4727b.png "Rendered by QuickLaTeX.com")

</center>

## 蟒蛇 3

```
# Mean Absolute Error

def mae( y, y_pred ) :

    return np.sum( np.abs( y - y_pred ) ) / np.size( y )
```

*   **平均偏差误差**
    与**均方误差**相同。它不太准确，但可以得出模型是正偏差还是负偏差的结论。

<center>

(3) ![\begin{equation*} M B E=\frac{\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)}{n} \end{equation*}](img/f1b658098625a94355705288f9ae60ee.png "Rendered by QuickLaTeX.com")

</center>

## 蟒蛇 3

```
# Mean Bias Error

def mbe( y, y_pred ) :

    return np.sum( y - y_pred ) / np.size( y )
```

*   **胡贝尔损失**T2【又称**平滑平均绝对误差**。与均方误差相比，它对数据中的异常值不太敏感，并且在 0 处也是可微的。这是一个绝对误差，当误差很小时，它就变成了二次误差。

<center>

(4) ![\begin{equation*} \text { Loss }= \begin{cases}\frac{1}{2} *(x-y)^{2} & \text { if }(|x-y| \leq \delta) \\ \delta *|x-y|-\frac{1}{2} * \delta^{2} & \text { otherwise }\end{cases} \end{equation*}](img/2b0bf428b4fdd9619ed3ddf39ef4ea8f.png "Rendered by QuickLaTeX.com")

## 蟒蛇 3

```
def Huber( y, y_pred, delta ) :

    condition = np.abs( y - y_pred ) < delta 

    l =  np.where( condition, 0.5 * ( y - y_pred ) **2, delta * ( np.abs( y - y_pred ) - 0.5 * delta ) )

    return np.sum( l ) / np.size( y )
```

**分类损失:**

*   交叉熵**损失**
    又称**负对数似然**。它是常用的分类损失函数。交叉熵损失随着预测的概率偏离实际标签而进展。

## 蟒蛇 3

```
# Binary Loss

def cross_entropy( y, y_pred ) :

    return - np.sum( y * np.log( y_pred ) + ( 1 - y ) * np.log( 1 - y_pred ) ) / np.size( y )
```

<center>

(5) ![\begin{equation*} \text { CrossEntropyLoss }=-\left(y_{i} \log \left(\hat{y}_{i}\right)+\left(1-y_{i}\right) \log \left(1-\hat{y}_{i}\right)\right) \end{equation*}](img/6710b7b6e43084ce6d8e5503738715ac.png "Rendered by QuickLaTeX.com")

</center>

*   **铰链损失**T2【又称多级 **SVM 损失**。铰链损失用于最大边缘分类，特别是支持向量机。它是凸优化器中使用的凸函数。

<center>

(6) ![\begin{equation*} \text { SVMLoss }=\sum_{j \neq y_{i}} \max \left(0, s_{j}-s_{y_{i}}+1\right) \end{equation*}](img/b4a9fd24634959d57fa413b3217e1ad0.png "Rendered by QuickLaTeX.com")

</center>

## 蟒蛇 3

```
# Hinge Loss

def hinge( y, y_pred ) :

    l = 0

    size = np.size( y )

    for i in range( size ) :

        l = l + max( 0, 1 - y[i] * y_pred[i] )

    return l / size
```

</center>