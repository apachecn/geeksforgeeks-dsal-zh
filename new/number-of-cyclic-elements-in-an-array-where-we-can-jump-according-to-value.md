# 我们可以根据值

跳转的数组中循环元素的数量

> 原文： [https://www.geeksforgeeks.org/number-of-cyclic-elements-in-an-array-where-we-can-jump-according-to-value/](https://www.geeksforgeeks.org/number-of-cyclic-elements-in-an-array-where-we-can-jump-according-to-value/)

给定 n 个整数的数组 arr []。 对于每个值 arr [i]，考虑周期中的数组元素，我们可以顺时针

移至 arr [i] +1。 我们需要计算数组中的循环元素。 如果一个元素是循环的，则从该元素开始并移至 arr [i] + 1 会导致相同的元素。

例子：

```
Input : arr[] = {1, 1, 1, 1}
Output : 4
All 4 elements are cyclic elements.
1 -> 3 -> 1
2 -> 4 -> 2
3 -> 1 -> 3
4 -> 2 -> 4

Input : arr[] = {3, 0, 0, 0}
Output : 1
There is one cyclic point 1,
1 -> 1
The path covered starting from 2 is
2 -> 3 -> 4 -> 1 -> 1.

The path covered starting from 3 is
2 -> 3 -> 4 -> 1 -> 1.

The path covered starting from 4 is
4 -> 1 -> 1

```

一种**简单解决方案**是一个接一个地检查所有元素。 我们从每个元素 arr [i]开始遵循简单路径，然后转到 arr [i] +1。如果返回到 arr [i]以外的其他访问元素，则不计算 arr [i]。 该解决方案的时间复杂度为`O(N^2)`

**有效解决方案**基于以下步骤。

1.  使用数组索引作为节点创建有向图。 我们从 i 到节点（arr [i] + 1）％n 添加一条边。

2.  创建图后，我们使用 Kosaraju 的算法

找到了所有[强连通组件。3）最后，我们返回了各个强连通组件中的节点总数。](https://www.geeksforgeeks.org/strongly-connected-components/)

```

// CPP program to count cyclic points 
// in an array using Kosaraju's Algorithm 
#include <bits/stdc++.h> 
using namespace std; 

// Most of the code is taken from below link 
// https://www.geeksforgeeks.org/strongly-connected-components/ 
class Graph { 
    int V; 
    list<int>* adj; 
    void fillOrder(int v, bool visited[], 
                      stack<int>& Stack); 
    int DFSUtil(int v, bool visited[]); 

public: 
    Graph(int V); 
    void addEdge(int v, int w); 
    int countSCCNodes(); 
    Graph getTranspose(); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

// Counts number of nodes reachable 
// from v 
int Graph::DFSUtil(int v, bool visited[]) 
{ 
    visited[v] = true; 
    int ans = 1; 
    list<int>::iterator i; 
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
        if (!visited[*i]) 
           ans += DFSUtil(*i, visited); 
    return ans; 
} 

Graph Graph::getTranspose() 
{ 
    Graph g(V); 
    for (int v = 0; v < V; v++) { 
        list<int>::iterator i; 
        for (i = adj[v].begin(); i != adj[v].end(); ++i) 
            g.adj[*i].push_back(v); 
    } 
    return g; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); 
} 

void Graph::fillOrder(int v, bool visited[], 
                           stack<int>& Stack) 
{ 
    visited[v] = true; 
    list<int>::iterator i; 
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
        if (!visited[*i]) 
            fillOrder(*i, visited, Stack); 
    Stack.push(v); 
} 

// This function mainly returns total count of  
// nodes in individual SCCs using Kosaraju's 
// algorithm. 
int Graph::countSCCNodes() 
{ 
    int res = 0; 
    stack<int> Stack; 
    bool* visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 
    for (int i = 0; i < V; i++) 
        if (visited[i] == false) 
            fillOrder(i, visited, Stack); 
    Graph gr = getTranspose(); 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 
    while (Stack.empty() == false) { 
        int v = Stack.top(); 
        Stack.pop(); 
        if (visited[v] == false) { 
            int ans = gr.DFSUtil(v, visited); 
            if (ans > 1) 
                res += ans; 
        } 
    } 
    return res; 
} 

// Returns count of cyclic elements in arr[] 
int countCyclic(int arr[], int n) 
{ 
    int  res = 0; 

    // Create a graph of array elements 
    Graph g(n + 1); 

    for (int i = 1; i <= n; i++) { 
        int x = arr[i-1]; 

        // If i + arr[i-1] jumps beyond last 
        // element, we take mod considering 
        // cyclic array 
        int v = (x + i) % n + 1; 

        // If there is a self loop, we 
        // increment count of cyclic points. 
        if (i == v) 
            res++; 

        g.addEdge(i, v); 
    } 

    // Add nodes of strongly connected components 
    // of size more than 1\. 
    res += g.countSCCNodes(); 

    return res; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 1, 1, 1}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << countCyclic(arr, n); 
    return 0; 
} 

```

输出：

```
4

```

时间复杂度：`O(N)`

辅助空间：`O(N)`注意，只有`O(N)`个边。

本文由 [**Mohak Agrawal**](https://auth.geeksforgeeks.org/profile.php?user=agrawalmohak99&list=practice) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

