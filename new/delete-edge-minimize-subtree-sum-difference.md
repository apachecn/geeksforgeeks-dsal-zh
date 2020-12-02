# 删除边缘以最小化子树总和差异

> 原文： [https://www.geeksforgeeks.org/delete-edge-minimize-subtree-sum-difference/](https://www.geeksforgeeks.org/delete-edge-minimize-subtree-sum-difference/)

给定一个无向树，其每个**节点都与权重**关联。 我们需要删除一条边，以使一个子树的权重之和与另一子树的权重之差最小。

**示例**：

```
 ![](img/55192133ad8702f9d33c722891d4cfe9.png)
In above tree, 
We have 6 choices for edge deletion,
edge 0-1,  subtree sum difference = 21 - 2 = 19
edge 0-2,  subtree sum difference = 14 - 9 = 5
edge 0-3,  subtree sum difference = 15 - 8 = 7
edge 2-4,  subtree sum difference = 20 - 3 = 17
edge 2-5,  subtree sum difference = 18 - 5 = 13
edge 3-6,  subtree sum difference = 21 - 2 = 19

```

我们可以使用 DFS 解决此问题。 一种**简单解决方案**是逐个删除每个边并检查子树总和差。 最后选择最少的一个。 这种方法需要二次的时间。 一种有效的**方法**可通过使用树的总和来计算两个子树的和，从而在线性时间内解决此问题。 我们可以通过从树的总和中减去一个子树的总和来获得另一棵树的总和，这样子树的总和差可以在 O（1）的每个节点上计算出来。 首先，我们计算完整树的权重，然后在每个节点上执行 DFS 时，计算其子树总和，通过使用这两个值，我们可以计算子树总和之差。
在下面的代码中，另一个数组子树用于将根于节点 i 的子树的总和存储在子树[i]中。 每次使用当前节点索引和父索引调用 DFS，以仅在每个节点上遍历子节点。
请参阅以下代码，以更好地理解。

## C++

```cpp

// C++ program to minimize subtree sum 
// difference by one edge deletion 
#include <bits/stdc++.h> 
using namespace std; 

/* DFS method to traverse through edges, 
   calculating subtree sum at each node and 
   updating the difference between subtrees */
void dfs(int u, int parent, int totalSum, 
        vector<int> edge[], int subtree[], int& res) 
{ 
    int sum = subtree[u]; 

    /*  loop for all neighbors except parent and 
        aggregate sum over all subtrees    */
    for (int i = 0; i < edge[u].size(); i++) 
    { 
        int v = edge[u][i]; 
        if (v != parent) 
        { 
            dfs(v, u, totalSum, edge, subtree, res); 
            sum += subtree[v]; 
        } 
    } 

    // store sum in current node's subtree index 
    subtree[u] = sum; 

    /*  at one side subtree sum is 'sum' and other side 
        subtree sum is 'totalSum - sum' so their difference 
        will  be totalSum - 2*sum, by which we'll update 
        res  */
    if (u != 0 && abs(totalSum - 2*sum) < res) 
        res = abs(totalSum - 2*sum); 
} 

//  Method returns minimum subtree sum difference 
int getMinSubtreeSumDifference(int vertex[], 
                     int edges[][2], int N) 
{ 
    int totalSum = 0; 
    int subtree[N]; 

    // Calculating total sum of tree and initializing 
    // subtree sum's by vertex values 
    for (int i = 0; i < N; i++) 
    { 
        subtree[i] = vertex[i]; 
        totalSum += vertex[i]; 
    } 

    //  filling edge data structure 
    vector<int> edge[N]; 
    for (int i = 0; i < N - 1; i++) 
    { 
        edge[edges[i][0]].push_back(edges[i][1]); 
        edge[edges[i][1]].push_back(edges[i][0]); 
    } 

    int res = INT_MAX; 

    // calling DFS method at node 0, with parent as -1 
    dfs(0, -1, totalSum, edge, subtree, res); 
    return res; 
} 

//  Driver code to test above methods 
int main() 
{ 
    int vertex[] = {4, 2, 1, 6, 3, 5, 2}; 
    int edges[][2] = {{0, 1}, {0, 2}, {0, 3}, 
                      {2, 4}, {2, 5}, {3, 6}}; 
    int N = sizeof(vertex) / sizeof(vertex[0]); 

    cout << getMinSubtreeSumDifference(vertex, edges, N); 
    return 0; 
} 

```