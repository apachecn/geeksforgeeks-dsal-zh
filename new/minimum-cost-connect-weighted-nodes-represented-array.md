# 连接表示为数组

的加权节点的最低成本

> 原文： [https://www.geeksforgeeks.org/minimum-cost-connect-weighted-nodes-represented-array/](https://www.geeksforgeeks.org/minimum-cost-connect-weighted-nodes-represented-array/)

给定一个由 N 个元素（节点）组成的数组，其中每个元素都是该节点的权重。连接两个节点将花费其权重的成本。您必须将每个节点与每个其他节点（直接或间接）连接。 所需的最低费用。

**示例**：

```
Input : a[] = {6, 2, 1, 5}
Output :  13
Explanation : 
Here, we connect the nodes as follows:
connect a[0] and a[2], cost = 6*1 = 6,
connect a[2] and a[1], cost = 1*2 = 2,
connect a[2] and a[3], cost = 1*5 = 5.
every node is reachable from every other node:
Total cost = 6+2+5 = 13.

Input  : a[] = {5, 10}
Output : 50
Explanation : connections:
connect a[0] and a[1], cost = 5*10 = 50,
Minimum cost = 50\. 

```

我们需要做一些观察，我们必须制作一个具有 N-1 条边的连通图。 由于输出将是两个数字的乘积之和，因此我们必须使该和方程中每个项的乘积最小。 我们该怎么做？ 显然，选择数组中的最小元素并将其彼此连接。 这样，我们可以从特定节点访问所有其他节点。

设最小元素= a [i]，（让它的索引为 0）

**最低费用**

![=a[i]*a[1]+a[i]*a[2]+....+a[i]*a[n-1], ](img/cf4a6cc09b9612449a78884c7a9e9ad8.png "Rendered by QuickLaTeX.com")

![a[i]*(a[1]+a[2]+....+a[n-1]);](img/25667a7fb5bdd7fc3d4a60498005f5f9.png "Rendered by QuickLaTeX.com")

因此，答案是最小元素与除最小元素外的所有元素之和的*乘积。*

## C++

```cpp

// cpp code for Minimum Cost Required to connect weighted nodes 
#include <bits/stdc++.h> 
using namespace std; 
int minimum_cost(int a[], int n) 
{ 
    int mn = INT_MAX; 
    int sum = 0; 
    for (int i = 0; i < n; i++) { 

        // To find the minimum element  
        mn = min(a[i], mn); 

        // sum of all the elements  
        sum += a[i];  
    } 

    return mn * (sum - mn); 
} 

// Driver code 
int main() 
{ 
    int a[] = { 4, 3, 2, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << minimum_cost(a, n) << endl; 
    return 0; 
} 

```