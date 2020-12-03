# 最小化弱连接节点的数量

> 原文： [https://www.geeksforgeeks.org/convert-undirected-graph-directed-graph-minimize-disconnected-component/](https://www.geeksforgeeks.org/convert-undirected-graph-directed-graph-minimize-disconnected-component/)

给定**无向图**，任务是在将该图转换为有向图之后，找到弱连接节点的最小数量。

**弱连接的节点**：节点的 in 度（传入边数）为 0。

**先决条件**：[BFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

例子 ：

```
Input : 4 4 
        0 1
        1 2
        2 3
        3 0
Output : 0 disconnected components

Input : 6 5
       1 2
       2 3
       4 5
       4 6
       5 6
Output : 1 disconnected components

```

**说明**：

![](img/572e0755074ba6b76bf2e20d022c7bdb.png)

**方法**：我们找到了一个节点，该节点可帮助一次遍历最大节点。 为了覆盖所有可能的路径，为此使用了 [DFS 图遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)技术。

执行上述步骤来遍历图形。 现在，再次遍历图并检查哪些节点的度数为 0。

```

// CPP code to minimize the number 
// of weakly connected nodes  
#include <bits/stdc++.h> 
using namespace std; 

// Set of nodes which are traversed 
// in each launch of the DFS 
set<int> node; 
vector<int> Graph[10001]; 

// Function traversing the graph using DFS 
// approach and updating the set of nodes 
void dfs(bool visit[], int src) 
{ 
    visit[src] = true; 
    node.insert(src); 
    int len = Graph[src].size(); 
    for (int i = 0; i < len; i++)     
        if (!visit[Graph[src][i]])         
            dfs(visit, Graph[src][i]); 
} 

// building a undirected graph 
void buildGraph(int x[], int y[], int len){ 

    for (int i = 0; i < len; i++) 
    { 
        int p = x[i]; 
        int q = y[i]; 
        Graph[p].push_back(q); 
        Graph[q].push_back(p); 
    } 
} 

// computes the minimum number of disconnected 
// components when a bi-directed graph is  
// converted to a undirected graph 
int compute(int n) 
{ 
    // Declaring and initializing 
    // a visited array 
    bool visit[n + 5]; 
    memset(visit, false, sizeof(visit)); 
    int number_of_nodes = 0; 

    // We check if each node is 
    // visited once or not 
    for (int i = 0; i < n; i++) 
    { 
        // We only launch DFS from a 
        // node iff it is unvisited. 
        if (!visit[i]) { 

            // Clearing the set of nodes 
            // on every relaunch of DFS 
            node.clear(); 

            // relaunching DFS from an 
            // unvisited node. 
            dfs(visit, i); 

            // iterating over the node set to count the 
            // number of nodes visited after making the 
            // graph directed and storing it in the 
            // variable count. If count / 2 == number 
            // of nodes - 1, then increment count by 1\. 
            int count = 0;          
            for (auto it = node.begin(); it != node.end(); ++it) 
                count += Graph[(*it)].size(); 

            count /= 2;         
            if (count == node.size() - 1) 
               number_of_nodes++; 
        } 
    } 
    return number_of_nodes; 
} 

//Driver function 
int main() 
{ 
    int n = 6,m = 4; 
    int x[m + 5] = {1, 1, 4, 4}; 
    int y[m+5] = {2, 3, 5, 6}; 

    /*For given x and y above, graph is as below : 
        1-----2         4------5 
        |               | 
        |               | 
        |               | 
        3               6 

        // Note : This code will work for  
        // connected graph also as : 
        1-----2 
        |     | \ 
        |     |  \ 
        |     |   \ 
        3-----4----5 
    */

    // Building graph in the form of a adjacency list 
    buildGraph(x, y, n); 
    cout << compute(n) << " weakly connected nodes"; 

    return 0; 
} 

```

**Output:**

```
2 weakly connected nodes

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。