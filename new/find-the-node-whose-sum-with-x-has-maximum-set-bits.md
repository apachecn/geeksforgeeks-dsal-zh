# 查找与 X 的总和具有最大设置位的节点

> 原文： [https://www.geeksforgeeks.org/find-the-node-whose-sum-with-x-has-maximum-set-bits/](https://www.geeksforgeeks.org/find-the-node-whose-sum-with-x-has-maximum-set-bits/)

给定一棵树，以及所有节点的权重和整数`x`，任务是找到一个节点`i`，使得 **weight [i] + x** 具有最大设置位。 如果两个或更多节点在添加`x`时具有相同的设置位计数，则找到一个最小值。

**示例**：

> **输入**：
> ![](img/107072b5f698ad7b63297c5c333d9375.png)
> x = 15
> **输出**：4
> 节点 1：setbits（5 + 15）= 2
> 节点 2：setbits（10 + 15）= 3
> 节点 3：setbits（11 + 15）= 3
> 节点 4：setbits（8 + 15）= 4
> 节点 5：setbits（6 + 15） = 3

**方法**：在树上执行 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，并跟踪其与`x`的总和具有最大设置位的节点。 如果两个或更多节点的设置位计数相等，则选择数量最少的一个。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

int maximum = INT_MIN, x, ans = INT_MAX; 

vector<int> graph[100]; 
vector<int> weight(100); 

// Function to perform dfs to find 
// the maximum set bits value 
void dfs(int node, int parent) 
{ 
    // If current set bits value is greater than 
    // the current maximum 
    int a = __builtin_popcount(weight[node] + x); 
    if (maximum < a) { 
        maximum = a; 
        ans = node; 
    } 

    // If count is equal to the maximum 
    // then choose the node with minimum value 
    else if (maximum == a) 
        ans = min(ans, node); 

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