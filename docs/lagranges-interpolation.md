# 拉格朗日插值

> 原文:[https://www.geeksforgeeks.org/lagranges-interpolation/](https://www.geeksforgeeks.org/lagranges-interpolation/)

**什么是插值？**
插值是在一组离散的已知数据点范围内寻找新数据点的方法(来源 [Wiki](https://en.wikipedia.org/wiki/Interpolation) )。换句话说，插值是一种估计数学函数值的技术，适用于自变量的任何中间值。
例如，在给定的表中，我们给出了 4 组离散数据点，用于未知函数 f(x) :

![\begin{array}{|c|c|c|c|c|} \hline \mathbf{i} & 1 & 2 & 3 & 4 \\ \hline \mathbf{x}_{\mathbf{i}} & 0 & 1 & 2 & 5 \\ \hline \mathbf{y}_{\mathbf{i}}=\mathbf{f}_{\mathbf{i}}(\mathbf{x}) & 2 & 3 & 12 & 147 \\ \hline \end{array}   ](img/aac811c7f7e08bd65a492f6ca268f95c.png "Rendered by QuickLaTeX.com")

**怎么找？**
这里我们可以应用拉格朗日插值公式得到我们的解。
拉格朗日插值公式:
如果，y = f(x)取值 y0，y1，…，yn 对应 x = x0，x1，…，xn，那么，

![f(x)=\frac{\left(x-x_{2}\right)\left(x-x_{3}\right) \ldots\left(x-x_{n}\right)}{\left(x_{1}-x_{2}\right)\left(x_{1}-x_{3}\right) \ldots\left(x_{1}-x_{n}\right)} y_{1}+\frac{\left(x-x_{1}\right)\left(x-x_{3}\right) \ldots\left(x-x_{n}\right)}{\left(x_{2}-x_{1}\right)\left(x_{2}-x_{3}\right) \ldots\left(x_{2}-x_{n}\right)} y_{2}+\ldots .+\frac{\left(x-x_{1}\right)\left(x-x_{2}\right) \ldots\left(x-x_{n}-1\right)}{\left(x_{n}-x_{1}\right)\left(x_{n}-x_{2}\right) \ldots\left(x_{n}-x_{n-1}\right)} y_{n}   ](img/53eb3978112cd85496c161ad86f5e6a8.png "Rendered by QuickLaTeX.com")
这种方法比牛顿法更受欢迎，因为它甚至适用于 x 的不等距值。
我们可以使用插值技术来找到一个中间数据点，比如 x = 3。

**拉格朗日插值的优点:**

*   这个公式用于计算函数值，即使参数的间距不相等。
*   这个公式用来求一个函数给定值对应的自变量 x 的值。

**拉格朗日插值的缺点:**

*   拉格朗日多项式中度数的变化涉及所有项的全新计算。
*   对于一个高次多项式，公式涉及大量的乘法运算，这使得过程相当缓慢。
*   在拉格朗日插值中，多项式的次数是从一开始就选择的。因此，很难找到适合于给定列表点集合的近似多项式的次数。

## C++

```
// C++ program for implementation of Lagrange's Interpolation
#include<bits/stdc++.h>
using namespace std;

// To represent a data point corresponding to x and y = f(x)
struct Data
{
    int x, y;
};

// function to interpolate the given data points using Lagrange's formula
// xi corresponds to the new data point whose value is to be obtained
// n represents the number of known data points
double interpolate(Data f[], int xi, int n)
{
    double result = 0; // Initialize result

    for (int i=0; i<n; i++)
    {
        // Compute individual terms of above formula
        double term = f[i].y;
        for (int j=0;j<n;j++)
        {
            if (j!=i)
                term = term*(xi - f[j].x)/double(f[i].x - f[j].x);
        }

        // Add current term to result
        result += term;
    }

    return result;
}

// driver function to check the program
int main()
{
    // creating an array of 4 known data points
    Data f[] = {{0,2}, {1,3}, {2,12}, {5,147}};

    // Using the interpolate function to obtain a data point
    // corresponding to x=3
    cout << "Value of f(3) is : " << interpolate(f, 3, 5);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation
// of Lagrange's Interpolation

import java.util.*;

class GFG
{

// To represent a data point
// corresponding to x and y = f(x)
static class Data
{
    int x, y;

    public Data(int x, int y)
    {
        super();
        this.x = x;
        this.y = y;
    }

};

// function to interpolate the given
// data points using Lagrange's formula
// xi corresponds to the new data point
// whose value is to be obtained n
// represents the number of known data points
static double interpolate(Data f[], int xi, int n)
{
    double result = 0; // Initialize result

    for (int i = 0; i < n; i++)
    {
        // Compute individual terms of above formula
        double term = f[i].y;
        for (int j = 0; j < n; j++)
        {
            if (j != i)
                term = term*(xi - f[j].x) / (f[i].x - f[j].x);
        }

        // Add current term to result
        result += term;
    }

    return result;
}

// Driver code
public static void main(String[] args)
{
    // creating an array of 4 known data points
    Data f[] = {new Data(0, 2), new Data(1, 3),
                new Data(2, 12), new Data(5, 147)};

    // Using the interpolate function to obtain
    // a data point corresponding to x=3
    System.out.print("Value of f(3) is : " +
                    (int)interpolate(f, 3, 4));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for implementation
# of Lagrange's Interpolation

# To represent a data point corresponding to x and y = f(x)
class Data:
    def __init__(self, x, y):
        self.x = x
        self.y = y

# function to interpolate the given data points
# using Lagrange's formula
# xi -> corresponds to the new data point
# whose value is to be obtained
# n -> represents the number of known data points
def interpolate(f: list, xi: int, n: int) -> float:

    # Initialize result
    result = 0.0
    for i in range(n):

        # Compute individual terms of above formula
        term = f[i].y
        for j in range(n):
            if j != i:
                term = term * (xi - f[j].x) / (f[i].x - f[j].x)

        # Add current term to result
        result += term

    return result

# Driver Code
if __name__ == "__main__":

    # creating an array of 4 known data points
    f = [Data(0, 2), Data(1, 3), Data(2, 12), Data(5, 147)]

    # Using the interpolate function to obtain a data point
    # corresponding to x=3
    print("Value of f(3) is :", interpolate(f, 3, 4))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for implementation
// of Lagrange's Interpolation
using System;

class GFG
{

// To represent a data point
// corresponding to x and y = f(x)
class Data
{
    public int x, y;
    public Data(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};

// function to interpolate the given
// data points using Lagrange's formula
// xi corresponds to the new data point
// whose value is to be obtained n
// represents the number of known data points
static double interpolate(Data []f,
                          int xi, int n)
{
    double result = 0; // Initialize result

    for (int i = 0; i < n; i++)
    {
        // Compute individual terms
        // of above formula
        double term = f[i].y;
        for (int j = 0; j < n; j++)
        {
            if (j != i)
                term = term * (xi - f[j].x) /
                          (f[i].x - f[j].x);
        }

        // Add current term to result
        result += term;
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{
    // creating an array of 4 known data points
    Data []f = {new Data(0, 2),
                new Data(1, 3),
                new Data(2, 12),
                new Data(5, 147)};

    // Using the interpolate function to obtain
    // a data point corresponding to x=3
    Console.Write("Value of f(3) is : " +
                  (int)interpolate(f, 3, 4));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program for implementation
// of Lagrange's Interpolation

// To represent a data point
// corresponding to x and y = f(x)
class Data
{
    constructor(x,y)
    {
        this.x=x;
        this.y=y;
    }
}

// function to interpolate the given
// data points using Lagrange's formula
// xi corresponds to the new data point
// whose value is to be obtained n
// represents the number of known data points
function interpolate(f,xi,n)
{
    let result = 0; // Initialize result

    for (let i = 0; i < n; i++)
    {
        // Compute individual terms of above formula
        let term = f[i].y;
        for (let j = 0; j < n; j++)
        {
            if (j != i)
                term = term*(xi - f[j].x) / (f[i].x - f[j].x);
        }

        // Add current term to result
        result += term;
    }

    return result;
}

// Driver code
 // creating an array of 4 known data points
let f=[new Data(0, 2), new Data(1, 3),
                new Data(2, 12), new Data(5, 147)];

// Using the interpolate function to obtain
    // a data point corresponding to x=3
document.write("Value of f(3) is : " +
                    interpolate(f, 3, 4));

// This code is contributed by rag2127
</script>
```

**输出:**

```
Value of f(3) is : 35
```

**复杂度:**
以上解的时间复杂度为 O(n <sup>2</sup> )，辅助空间为 O(1)。

**参考文献:**

*   [https://en.wikipedia.org/wiki/Lagrange_polynomial](https://en.wikipedia.org/wiki/Lagrange_polynomial)
    高等工程数学博士
*   [https://mat . iitm . AC . in/home/sryedida/public _ html/caimna/interpolation/lagrange . html](https://mat.iitm.ac.in/home/sryedida/public_html/caimna/interpolation/lagrange.html)

本文由[阿舒托什·库马尔](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。