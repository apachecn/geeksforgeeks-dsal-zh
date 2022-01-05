# 正态方程多元线性回归模型

> 原文:[https://www . geesforgeks . org/多元线性回归-正态方程模型/](https://www.geeksforgeeks.org/multiple-linear-regression-model-with-normal-equation/)

**先决条件:**T2

考虑一个数据集，

<center>

<figure class="table">

| **区域(x <sub>1</sub> )** | **房间(x <sub>2</sub> )** | **年龄(x <sub>3</sub> )** | **价格(y)** |
| Twenty-three | three | eight | Six thousand five hundred and sixty-two |
| Fifteen | Two | seven | Four thousand five hundred and sixty-nine |
| Twenty-four | four | nine | Six thousand eight hundred and ninety-seven |
| Twenty-nine | five | four | Seven thousand five hundred and sixty-two |
| Thirty-one | seven | six | Eight thousand two hundred and thirty-four |
| Twenty-five | three | Ten | Seven thousand four hundred and eighty-five |

</figure>

</center>

#### 让我们考虑一下，

这里**面积、房间、年龄**为特征/自变量，**价格**为目标/因变量。众所周知，多元线性回归的**假设由下式给出:**

<center>![$h_{\theta}(x)=\theta_{0} x_{0}+\theta_{1} x_{1}+\theta_{2} x_{2}+\ldots+\theta_{n} x_{n}$](img/878f276129db011fb1a3f949b6a750bb.png "Rendered by QuickLaTeX.com")</center>

<center>![Parameters: $\theta=\left\{\theta_{0}, \theta_{1}, \theta_{2}, \ldots \theta_{n}\right\}$ \\ Features: $x=\left\{x_{0}, x_{1}, x_{2}, \ldots x_{n}\right\}$](img/7160f0319de9a25226bdd1a3eed5229f.png "Rendered by QuickLaTeX.com")</center>

其中，![$x_{0} = 1$](img/086add46b4792efd207c9fa7286fa6b3.png "Rendered by QuickLaTeX.com")

**注:**这里我们的目标是找到参数θ的最佳值。为了找到θ的最佳值，我们可以使用正规方程。因此，在找到θ值后，我们的线性假设或线性模型就可以预测新特性或输入的价格了。

**正态方程为:**

<center>![$\theta=\left(X^{T} X\right)^{-1} X^{\mathrm{T}} y$](img/536f99cb29878d07433ef9996929e3a8.png "Rendered by QuickLaTeX.com")</center>

**考虑到上面的数据集我们可以写，**

**X:** 大小为( *n x m* )的所有独立特征的数组，其中 *m* 是训练样本的总数， *n* 是特征的总数，包括(x <sub>0</sub> = 1)

**X<sup>T:</sup>T3】数组 X 的转置**

**y:** *y* 为目标/因变量的 1D 阵/列阵/向量，大小为 *m* ，其中 *m* 为训练样本总数。

对于上面的例子，我们可以写:

**X = [[ 1，23，3，8]，**

**【1，15，2，7】，**

**【1，24，4，9】，**

**【1，29，5，4】，**

**【1，31，7，6】，**

**[ 1，25，3，10]]**

**X <sup>T</sup> = [[ 1，1，1，1，1，1]，**

**【23、15、24、29、31、25】**

**【3、2、4、5、7、3】**

**【8、7、9、4、6、10】]**

**y= [6562，4569，6897，7562，8234，7485]**

### 代码:用正态方程实现线性回归模型

## 计算机编程语言

```
import numpy as np

class LinearRegression:
    def __init__(self):
        pass

    def __compute(self, x, y):
        try:
            '''
            # multiline code
            var = np.dot(x.T,x)
            var = np.linalg.inv(var)
            var = np.dot(var,x.T)
            var = np.dot(var,y)
            self.__thetas = var
            '''
            # one line code
            self.__thetas = np.dot(np.dot(np.linalg.inv(np.dot(x.T,x)),x.T),y)
        except Exception as e:
            raise e

    def fit(self, x, y):
        x = np.array(x)
        ones_ = np.ones(x.shape[0])
        x = np.c_[ones_,x]
        y = np.array(y)
        self.__compute(x,y)

    @property
    def coef_(self):
        return self.__thetas[0]

    @property
    def intercept_(self):
        return self.__thetas[1:]

    def predict(self, x):
        try:
            x = np.array(x)
            ones_ = np.ones(x.shape[0])
            x = np.c_[ones_,x]
            result = np.dot(x,self.__thetas)
            return result            
        except Exception as e:
            raise e

# testing of code...

# datasets
x_train = [[2,40],[5,15],[8,19],[7,25],[9,16]]
y_train = [194.4, 85.5, 107.1, 132.9, 94.8]
x_test = [[12,32],[2,40]]
y_test = []

# testing the model...
lr = LinearRegression()
lr.fit(x,y)
print(lr.coef_,lr.intercept_)
print(lr.predict(x_t))
```

#### 输出:

> 截距值= 305。3333333334813
> 
> 系数是=[236.85714286-4.76190476102 . 9047619]
> 
> 测试数据的实际值= [8234，7485]
> 
> 测试数据的预测值= [8232。7241.52380952]