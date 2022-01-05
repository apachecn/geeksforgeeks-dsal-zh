# τ–数学常数

> 原文:[https://www.geeksforgeeks.org/tau-mathematical-constant/](https://www.geeksforgeeks.org/tau-mathematical-constant/)

**什么是τ？**
常数在数值上等于**2 *π(2 倍π)**，数值约为 **6.28** 。这个比值等于 2*C/D，其中 C 是圆周，D 是圆的直径。
**τ的应用**

*   **有很多表达式**实际上需要**“2 *π”计算**，有τ等于这在很大程度上简化了它们，例如**圆的周长= 2 *π* r =τ* r**。
*   τ的概念可用于**角度测量**像弧度中的角度，表示为完整的“一圈”和 cos，三角函数中的正弦函数具有τ的周期。
*   这些概念对于**教授几何**非常有用，因为这将减少在许多应用中使用“pi”和“2*pi”的混乱，并有助于消除因子 2。
*   τ**通过消除因子 2 简化了欧拉恒等式**。
*   它在许多使用“2*pi”的地方很有用，如傅立叶变换、柯西积分公式等。

**对τ的批评**T2】

*   自从它**与扭矩、剪应力和时间的符号**相矛盾后，这个符号就受到了很多批评。
*   我们已经有了一个等于圆周率的“C/D”比，再有一个因子为 2 的圆比会造成选择上的混乱。
*   有一些**公式作为“π”**而不是τ的表达看起来更优雅，例如，圆的面积=π* r * r =(τ* r * r)/2，引入了额外的因子“1/2”。

**编码前景**
由于编程一直试图与数学进步相匹配，所以在最近的 python 3.6 的数学模块下，tau 的符号作为一个常数被引入。下面是它的插图。

## 蟒蛇 3

```
# Python code to demonstrate the working
# of tau

import math

# Printing the value of tau using 2*pi
print ("The value of tau (using 2*pi) is : ",end="")
print (math.pi*2)

# Printing the value of tau using in-built tau function
print ("The value of tau (using in-built tau) is : ",end="")
print (math.tau);
```

**输出:**

```
The value of tau (using 2*pi) is : 6.283185307179586
The value of tau (using in-built tau) is : 6.283185307179586
```

**注意:**由于不支持 Python 3.6，这段代码在 Geeksforgeeks IDE 上不起作用。
**参考:**http://math . wikia . com/wiki/Tau _(常量)
本文由 [**曼吉特·辛格**](https://auth.geeksforgeeks.org/profile.php?user=manjeet_04) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。