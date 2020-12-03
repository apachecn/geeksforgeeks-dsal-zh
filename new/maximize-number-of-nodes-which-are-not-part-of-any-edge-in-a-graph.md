# 最大化不属于图形

中任何边的节点的数量

> 原文： [https://www.geeksforgeeks.org/maximize-number-of-nodes-which-are-not-part-of-any-edge-in-a-graph/](https://www.geeksforgeeks.org/maximize-number-of-nodes-which-are-not-part-of-any-edge-in-a-graph/)

给定一个具有 n 个节点和 m 个边的图。 查找不属于任何边的节点的最大可能节点数（m 始终小于或等于完整图中的边数）。

**示例**：

```
Input: n = 3, m = 3
Output: Maximum Nodes Left Out: 0
Since it is a complete graph.

Input: n = 7, m = 6 
Output: Maximum Nodes Left Out: 3
We can construct a complete graph on 4 vertices using 6 edges.

```

**方法**：遍历所有 n，然后查看如果制作完整图，则在哪个节点上获得的多个边数大于 m，即为 K。答案为 **n-k** 。

*   可用于在 n 个节点上形成图的最大边数为 **n *（n – 1）/ 2** （完整图）。
*   然后找到最大 n 个数，它将使用 m 个或少于 m 个边来形成一个完整的图。
*   如果仍然留有边，则它将仅覆盖一个以上的节点，就好像它将覆盖一个以上的节点一样，这不是 n 的最大值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to illustrate above approach 
#include <bits/stdc++.h> 
#define ll long long int 
using namespace std; 

// Function to return number of nodes left out 
int answer(int n, int m) 
{ 
    int i; 
    for (i = 0; i <= n; i++) { 

        // Condition to terminate, when 
        // m edges are covered 
        if ((i * (i - 1)) >= 2 * m) 
            break; 
    } 

    return n - i; 
} 

// Driver Code 
int main() 
{ 
    int n = 7; 
    int m = 6; 
    cout << answer(n, m) << endl; 
} 

```