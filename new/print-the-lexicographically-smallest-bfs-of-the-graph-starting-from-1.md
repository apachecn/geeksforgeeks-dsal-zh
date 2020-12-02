# 打印从 1 开始的图形在字典上最小的 BFS

> 原文： [https://www.geeksforgeeks.org/print-the-lexicographically-smallest-bfs-of-the-graph-starting-from-1/](https://www.geeksforgeeks.org/print-the-lexicographically-smallest-bfs-of-the-graph-starting-from-1/)

给定一个具有 **N** 个顶点和 **M** 边的连通图。 任务是从 1 开始打印该图的按字典顺序最小的 BFS 遍历。

**注意**：顶点的编号从 1 到 N。

**示例：**

```
Input: N = 5, M = 5 
       Edges: 
       1 4
       3 4
       5 4
       3 2
       1 5 
Output: 1 4 3 2 5 
Start from 1, go to 4, then to 3 and then to 2 and to 5\. 

Input: N = 3, M = 2 
       Edges: 
       1 2 
       1 3 
Output: 1 2 3 

```

**方法：**我们可以使用优先级队列（最小堆）代替简单的队列，而不必在图形上进行普通的 BFS 遍历。 当访问节点时，将其相邻节点添加到优先级队列中。 每次我们访问一个新节点时，它将是优先级队列中索引最小的节点。 每次访问时从 1 开始打印节点。

下面是上述方法的实现：

```

// C++ program to print the lexcicographically 
// smallest path starting from 1 

#include <bits/stdc++.h> 
using namespace std; 

// Function to print the smallest lexicographically 
// BFS path starting from 1 
void printLexoSmall(vector<int> adj[], int n) 
{ 
    // Visited array 
    bool vis[n + 1]; 
    memset(vis, 0, sizeof vis); 

    // Minimum Heap 
    priority_queue<int, vector<int>, greater<int> > Q; 

    // First one visited 
    vis[1] = true; 
    Q.push(1); 

    // Iterate till all nodes are visited 
    while (!Q.empty()) { 

        // Get the top element 
        int now = Q.top(); 

        // Pop the element 
        Q.pop(); 

        // Print the current node 
        cout << now << " "; 

        // Find adjacent nodes 
        for (auto p : adj[now]) { 

            // If not visited 
            if (!vis[p]) { 

                // Push 
                Q.push(p); 

                // Mark as visited 
                vis[p] = true; 
            } 
        } 
    } 
} 

// Function to insert edges in the graph 
void insertEdges(int u, int v, vector<int> adj[]) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// Driver Code 
int main() 
{ 
    int n = 5, m = 5; 
    vector<int> adj[n + 1]; 

    // Insert edges 
    insertEdges(1, 4, adj); 
    insertEdges(3, 4, adj); 
    insertEdges(5, 4, adj); 
    insertEdges(3, 2, adj); 
    insertEdges(1, 5, adj); 

    // Function call 
    printLexoSmall(adj, n); 

    return 0; 
} 

```

**Output:**

```
1 4 3 2 5

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。