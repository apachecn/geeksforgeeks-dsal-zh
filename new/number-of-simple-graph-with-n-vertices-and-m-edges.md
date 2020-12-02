# 具有 N 个顶点和 M 个边的简单图的数量

> 原文： [https://www.geeksforgeeks.org/number-of-simple-graph-with-n-vertices-and-m-edges/](https://www.geeksforgeeks.org/number-of-simple-graph-with-n-vertices-and-m-edges/)

给定两个整数`N`和`M`，任务是计算可以用 **N 个顶点**和 **M 边绘制的简单无向图的数量[** 。 简单图是不包含多个边和自环的图。

**示例**：

> **输入**：N = 3，M = 1
> **输出**：3
> 这 3 个图分别是{1-2，3}，{2-3，1}， {1-3，2}。
> 
> **输入**：N = 5，M = 1
> **输出**：10

**方法**：`N`顶点从`1`到`N`编号。 由于没有自环或多个边，因此该边必须存在于两个不同的顶点之间。 因此，我们可以选择两个不同顶点的方式有 **<sup>N</sup> C <sub>2</sub>** ，它等于**（N *（N – 1））/ 2** 。 假设它为`P`。
现在`M`条边必须与这些顶点对一起使用，因此在`P`对之间选择`M`对顶点的方法有[ **<sup>P</sup> C <sub>M</sub>** 。
如果 **P < M** ，则答案将是`0`，因为多余的边缘不能独自留下。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the value of 
// Binomial Coefficient C(n, k) 
int binomialCoeff(int n, int k) 
{ 

    if (k > n) 
        return 0; 

    int res = 1; 

    // Since C(n, k) = C(n, n-k) 
    if (k > n - k) 
        k = n - k; 

    // Calculate the value of 
    // [n * (n - 1) *---* (n - k + 1)] / [k * (k - 1) * ... * 1] 
    for (int i = 0; i < k; ++i) { 
        res *= (n - i); 
        res /= (i + 1); 
    } 

    return res; 
} 

// Driver Code 
int main() 
{ 
    int N = 5, M = 1; 

    int P = (N * (N - 1)) / 2; 

    cout << binomialCoeff(P, M); 

    return 0; 
} 

```