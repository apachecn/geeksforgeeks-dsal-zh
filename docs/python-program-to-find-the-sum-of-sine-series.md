# Python 程序求正弦级数之和

> 原文:[https://www . geesforgeks . org/python-program-to-find-the-sum-of-sine-series/](https://www.geeksforgeeks.org/python-program-to-find-the-sum-of-sine-series/)

**先决条件:** [**数学**](https://www.geeksforgeeks.org/python-math-sin-function/)

给定 n 和 x，其中 n 是级数中的项数，x 是角度的度数。这里的任务是，编写一个程序来计算 x 的正弦级数之和。

**使用的配方:**

![sinx=x-(x3/3!)+(x5/5!)-(x7/7!)+…](img/63fadb0e0de4f78e62bcafaa3e23c657.png "Rendered by QuickLaTeX.com")

**示例:**

```
Input: n = 10
        x = 30
Output: sum of sine series is 0.5 

Input: n = 10
        x = 60
Output: sum of sine series is 0.87
```

**下面是计算正弦级数和的程序:**

## 蟒蛇 3

```
# Import Module
import math

# Create sine function
def sin( x, n):
    sine = 0
    for i in range(n):
        sign = (-1)**i
        pi = 22/7
        y = x*(pi/180)
        sine += ((y**(2.0*i+1))/math.factorial(2*i+1))*sign
    return sine

# driver nodes
# Enter value in degree in x
x = 10

# Enter number of terms
n = 90

# call sine function
print(round(sin(x,n),2))
```

**输出:**

```
0.17
```