# 将幂律分布转换为线性图

> 原文:[https://www . geesforgeks . org/converting-power-law-distribution-to-a-linear-graph/](https://www.geeksforgeeks.org/converting-power-law-distribution-to-a-linear-graph/)

每当我们在 ML 项目上工作时，我们都必须处理数据集的高维度。这里有一个非常特殊的术语，即*维度诅咒*。虽然有很多方法可以解决这个问题，其中一个解决办法就是改变坐标系。从数据科学家的角度来看，这个解决方案有些有趣和新颖。
在进行模型训练时，我们试图消除假设的线性，以提高模型的准确性。但在本文中，我们试图理解如何轻松地可视化数据，并借助简单而创新的数学来理解它。

下面给出的是假设:

<center>![  f(x)=b x^{-a}  ](img/4823f7793f69bead61c66d6cc15c7acc.png "Rendered by QuickLaTeX.com")</center>

Power Law is a very important concept in statistics and gives information about two variables. And these two variables are relatively proportional to each other which means that the change in quantity of one variable will reflect the change in the quantity of other variables. One quantity varies as a power of another.
Now lets’s solve this equation with the help of natural logarithm (ln).
![](img/826822233ca330b7001b592865b656f7.png)

幂律图

<center>
![  y=b x^{-a}  ](img/691e633aa021b29c21edfa41ee755ff8.png "Rendered by QuickLaTeX.com")
![  \ln (y) = \ln \left(b x^{-a}\right)  ](img/a4624e840851da442b47622761b97e35.png "Rendered by QuickLaTeX.com")</center>

使用对数属性

<center>![  \ln y=\ln (b)-a \ln (x)  ](img/4b76547fbae2bd34f3bc9f69adc75b0d.png "Rendered by QuickLaTeX.com")
</center>

Now, lets assume ln(y) to be ![\widehat{y}](img/1632380de7503379617c8e7d650709bb.png "Rendered by QuickLaTeX.com") and ln(x) to be ![\widehat{x}](img/7a249d3f25b6d6f9671746ecced7da36.png "Rendered by QuickLaTeX.com"). Substituting the values in the the equation above and then we have the equation.

<center>![\hat{y}=-a \hat{x}+\ln (b)](img/5735572a77b2bd2da718969b60935e03.png "Rendered by QuickLaTeX.com")</center>

![](img/f175954d126fa4530ec0e3378a047556.png)

幂律图中的线性图

So now, it is very evident that the hypothesis is now been converted to a linear equation. And this will make our task easy to analyse how the parameters are affecting each other.