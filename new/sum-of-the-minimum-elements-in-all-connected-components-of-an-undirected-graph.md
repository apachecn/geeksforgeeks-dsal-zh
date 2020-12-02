# 无向图

的所有连接组件中的最小元素的总和

> 原文： [https://www.geeksforgeeks.org/sum-of-the-minimum-elements-in-all-connected-components-of-an-undirected-graph/](https://www.geeksforgeeks.org/sum-of-the-minimum-elements-in-all-connected-components-of-an-undirected-graph/)

给定 N 个数字组成的数组 A，其中 A <sub>i</sub> 表示第（i + 1）<sup>个</sup>节点的值。 还给出了 M 对边，其中 u 和 v 表示通过边连接的节点。 任务是在给定无向图的所有连接组件中找到最小元素的总和。 如果一个节点与其他任何节点均无连接，则将其视为具有一个节点的组件。

**示例：**

> **输入：** a [] = {1、6、2、7、3、8、4、9、5、10} m = 5
> 1 2
> 3 4
> 5 6
> 7 8
> 9 10
> 
> **输出：** 15
> 连接的组件是：1-2、3-4、5-6、7-8 和 9-10
> 所有组件的总和：1 + 2 + 3 + 4 + 5 = 15
> 
> **输入：** a [] = {2，5，3，4，8} m = 2
> 1 4
> 4 5
> **输出：** 10
> ![](img/07a1bc34cb9958820d6c99c6bc7eff67.png)

**方法：**为无向图找到连接的组件是一件容易的事。 从每个未访问的顶点开始执行 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 或 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) ，将为我们提供连接的组件。 创建一个 **Visited []** 数组，该数组最初所有节点都标记为 False。 迭代所有节点，如果未访问该节点，则调用 **DFS（）**函数，以便将直接或间接连接到该节点的所有节点标记为已访问。 访问所有直接或间接连接的节点时，请存储所有节点的最小值。 创建一个变量 **sum** ，该变量存储所有这些连接的组件的最小值之和。 一旦访问了所有节点，*和*就可以解决问题。

下面是上述方法的实现：

```

// C++ program to find the sum 
// of the minimum elements in all 
// connected components of an undirected graph 
#include <bits/stdc++.h> 
using namespace std; 
const int N = 10000; 
vector<int> graph[N]; 

// Initially all nodes 
// marked as unvisited 
bool visited[N]; 

// DFS function that visits all 
// connected nodes from a given node 
void dfs(int node, int a[], int mini) 
{ 
    // Stores the minimum 
    mini = min(mini, a[node]); 

    // Marks node as visited 
    visited[node] = true; 

    // Traversed in all the connected nodes 
    for (int i : graph[node]) { 
        if (!visited[i]) 
            dfs(i, a, mini); 
    } 
} 

// Function to add the edges 
void addedge(int u, int v) 
{ 
    graph[u - 1].push_back(v - 1); 
    graph[v - 1].push_back(u - 1); 
} 

// Function that returns the sum of all minimums 
// of connected componenets of graph 
int minimumSumConnectedComponents(int a[], int n) 
{ 
    // Initially sum is 0 
    int sum = 0; 

    // Traverse for all nodes 
    for (int i = 0; i < n; i++) { 
        if (!visited[i]) { 
            int mini = a[i]; 
            dfs(i, a, mini); 
            sum += mini; 
        } 
    } 

    // Returns the answer 
    return sum; 
} 

// Driver Code 
int main() 
{ 
    int a[] = {1, 6, 2, 7, 3, 8, 4, 9, 5, 10}; 

    // Add edges 
    addedge(1, 2); 
    addedge(3, 4); 
    addedge(5, 6); 
    addedge(7, 8); 
    addedge(9, 10); 

    int n = sizeof(a) / sizeof(a[0]); 

    // Calling Function 
    cout << minimumSumConnectedComponents(a, n); 
    return 0; 
} 

```

**Output:**

```
15

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。