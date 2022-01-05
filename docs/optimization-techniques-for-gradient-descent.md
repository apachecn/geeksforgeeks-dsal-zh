# 梯度下降的优化技术

> 原文:[https://www . geesforgeks . org/优化-梯度下降技术/](https://www.geeksforgeeks.org/optimization-techniques-for-gradient-descent/)

梯度下降是一种迭代优化算法，用于寻找函数的最小值。总的思路是将参数初始化为随机值，然后在每次迭代中朝着“斜率”的方向小步前进。梯度下降在监督学习中被大量使用，以最小化误差函数并找到参数的最优值。

已经为梯度下降算法设计了各种扩展。下面讨论其中的一些:

*   **动量法**:该方法通过考虑梯度的指数加权平均值来加速梯度下降算法。使用平均值可以使算法更快地收敛到最小值，因为不常见方向的梯度被抵消了。动量法的伪代码如下。

    ```
    V = 0
    for each iteration i:
        compute dW
        V = β V + (1 - β) dW
        W = W - α V

    ```

    V 和 dW 分别类似于加速度和速度。α是学习率，β通常保持在 0.9。

*   **RMSProp** : RMSProp was put forward by Jeffrey Hinton of the University of Toronto. Intuition is the second moment when exponential weighted average method is applied to gradient (DW <sup>2</sup> ). The pseudo code is as follows:

    ```
    S = 0
    for each iteration i
        compute dW
        S = β S + (1 - β) dW2
        W = W - α dW⁄√S + ε

    ```

*   **亚当优化**:亚当优化算法结合了动量法和 RMSprop，以及偏差修正。这种方法的伪代码如下:

    ```
    V = 0
    S = 0
    for each iteration i
        compute dW
        V = β1 S + (1 - β1) dW
        S = β2 S + (1 - β2) dW2
        V = V⁄{1 - β<sub>1</sub><sup>i</sup>}
        S = S⁄{1 - β<sub>2</sub><sup>i</sup>}
        W = W - α V⁄√S + ε

    ```

    亚当的提出者金马和巴为超参数推荐了以下值。

    ```
    α = 0.001
    β1 = 0.9
    β2 = 0.999
    ε = 10-8

    ```