# 对给定树的权重以 X 为因子进行计数

> 原文： [https://www.geeksforgeeks.org/count-the-nodes-of-the-given-tree-whose-weight-has-x-as-a-factor/](https://www.geeksforgeeks.org/count-the-nodes-of-the-given-tree-whose-weight-has-x-as-a-factor/)

给定一棵树，以及所有节点的权重，任务是计算权重可被`x`整除的节点。

**示例**：

> **输入**：
> ![](img/c8d63a5a618701e1de407d9028376d6b.png)
> x = 5
> **输出**：2
> 只有节点 1 和 2 的权重可被 5 整除。

**方法**：在树上执行 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，对于每个节点，检查其权重是否可被 x 整除。 如果是，则增加计数。

**实施**：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

long ans = 0; 
int x; 
vector<int> graph[100]; 
vector<int> weight(100); 

// Function to perform dfs 
void dfs(int node, int parent) 
{ 

    // If weight of the current node 
    // is divisible by x 
    if (weight[node] % x == 0) 
        ans += 1; 

    for (int to : graph[node]) { 
        if (to == parent) 
            continue; 
        dfs(to, node); 
    } 
} 

// Driver code 
int main() 
{ 
    x = 5; 

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