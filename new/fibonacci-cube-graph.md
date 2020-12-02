# 斐波那契立方体图

> 原文： [https://www.geeksforgeeks.org/fibonacci-cube-graph/](https://www.geeksforgeeks.org/fibonacci-cube-graph/)

给出的输入是图 n 的顺序（连接到节点的最大边数），您必须在 n 阶的 Fibonacci 立方体图中找到顶点数。

**示例**：

```
Input : n = 3
Output : 5
Explanation : 
Fib(n + 2) = Fib(5) = 5

Input : n = 2
Output : 3

```

斐波那契立方体图类似于[超立方体图](https://www.geeksforgeeks.org/hypercube-graph/)，但顶点的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。 在斐波那契立方体图中，只有 1 个顶点的度为 n，其余所有度的度均小于 n。
阶 n 的斐波那契立方体图具有 F（n + 2）个顶点，其中 F（n）是第 n 个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，
斐波那契数列：1、1、2、3 ，5、8、13、21、34………………。

![](img/9f6afb7bdc0ed485a62f680367e03f48.png)

对于输入 n（作为图的顺序），在位置 n + 2 处找到相应的斐波那契数。
其中 F（n）= F（n – 1）+ F（n – 2）

**方法**：找到第（n + 2）个斐波那契数。

下面是上述方法的实现：

## C ++

```

// CPP code to find vertices in a fibonacci 
// cube graph of order n 
#include<iostream> 
using namespace std; 

// function to find fibonacci number 
int fib(int n) 
{ 
    if (n <= 1) 
        return n; 
    return fib(n - 1) + fib(n - 2); 
} 

// function for finding number of vertices  
// in fibonacci cube graph 
int findVertices (int n) 
{ 
    // return fibonacci number for f(n + 2)  
    return fib(n + 2); 
} 

// driver program 
int main() 
{ 
    // n is the order of the graph 
    int n = 3; 
    cout << findVertices(n); 
    return 0; 
} 

```