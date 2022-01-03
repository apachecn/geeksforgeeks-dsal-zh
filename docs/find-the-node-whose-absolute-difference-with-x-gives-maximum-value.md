# 查找与 X 的绝对差给出最大值的节点

> 原文： [https://www.geeksforgeeks.org/find-the-node-whose-absolute-difference-with-x-gives-maximum-value/](https://www.geeksforgeeks.org/find-the-node-whose-absolute-difference-with-x-gives-maximum-value/)

给定一棵树，以及所有节点的权重和整数`x`，任务是找到一个节点`i`，使得 **| weight [i] – x |** 最大。

**示例**：

> **输入**：
> ![](img/107072b5f698ad7b63297c5c333d9375.png)
> x = 15
> **输出**：1
> 节点 1：| 5 – 15 | = 10
> 节点 2：| 10 – 15 | = 5
> 节点 3：| 11 -15 | = 4
> 节点 4：| 8 – 15 | = 7
> 节点 5：| 6 -15 | = 9

**方法**：在树上执行 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，并跟踪其加权绝对差与`x`给出最大值的节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

int maximum = INT_MIN, x, ans; 

vector<int> graph[100]; 
vector<int> weight(100); 

// Function to perform dfs to find 
// the maximum value 
void dfs(int node, int parent) 
{ 
    // If current value is more than 
    // the current maximum 
    if (maximum < abs(weight[node] - x)) { 
        maximum = abs(weight[node] - x); 
        ans = node; 
    } 
    for (int to : graph[node]) { 
        if (to == parent) 
            continue; 
        dfs(to, node); 
    } 
} 

// Driver code 
int main() 
{ 
    x = 15; 

    // Weights of the node 
    weight[1] = 5; 
    weight[2] = 10; 
    weight[3] = 11; 
    weight[4] = 8; 
    weight[5] = 6; 

    // Edges of the tree 
    graph[1].push_back(2); 
    graph[2].push_back(3); 
    graph[2].push_back(4); 
    graph[1].push_back(5); 

    dfs(1, 1); 

    cout << ans; 

    return 0; 
} 

```