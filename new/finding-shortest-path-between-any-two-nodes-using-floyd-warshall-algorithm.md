# 使用 Floyd Warshall 算法

查找任意两个节点之间的最短路径

> 原文： [https://www.geeksforgeeks.org/finding-shortest-path-between-any-two-nodes-using-floyd-warshall-algorithm/](https://www.geeksforgeeks.org/finding-shortest-path-between-any-two-nodes-using-floyd-warshall-algorithm/)

给定**图**以及两个节点`u`和`v`，任务是使用 [Floyd Warshall 算法](http://www.geeksforgeeks.org/dynamic-programming-set-16-floyd-warshall-algorithm/)打印 u 和 v 之间的最短路径 ]。

**示例**：

> **输入**：u = 1，v = 3
> 
> ![](img/d5ed1e28049e26e9af1d9f3d53692d97.png)
> 
> **输出**：1-> 2-> 3
> **说明**：
> 从 1 到 3 的最短路径是通过顶点 2，总成本为 3。
> 第一边缘为 1-> 2，成本为 2，第二边缘为 2-> 3，成本为 1。
> 
> **输入**：u = 0，v = 2
> 
> ![](img/d5ed1e28049e26e9af1d9f3d53692d97.png)
> 
> **输出**：0-> 1-> 2
> **说明**：
> 从 0 到 2 的最短路径是通过顶点 1，总成本= 5

**方法**：

*   这里的主要思想是使用 matrix（2D array），如果最短路径对任何一对节点都发生更改，它将跟踪下一个要指向的节点。 最初，两个节点 u 和 v 之间的最短路径是 v（即 u-> v 的直接边）。
*   Initialising the **Next** array

    > 如果路径存在于两个节点之间，则 **Next [u] [v] = v**
    > 否则我们设置 **Next [u] [v] = -1**

*   Modification in Floyd Warshall Algorithm

    > 在**内部，如果 Floyd Warshall 算法**的条件成立，我们将添加语句 Next [i] [j] = Next [i] [k]
    > （这意味着我们找到了 i，j 之间的最短路径 通过中间节点 k）。

    如果条件如下所示，这就是我们的

     **```
    if(dis[i][j] > dis[i][k] + dis[k][j])
    {
        dis[i][j] = dis[i][k] + dis[k][j];
        Next[i][j] = Next[i][k];    
    }

    ```** 
***   For constructing path using these nodes we’ll simply start looping through the node`u`while updating its value to next[u][v] until we reach node`v`.

    ```
    path = [u]
    while u != v:
        u = Next[u][v]
        path.append(u)

    ```** 

 **下面是上述方法的实现。

## C ++

```

// C++ program to find the shortest  
// path between any two nodes using  
// Floyd Warshall Algorithm.  
#include <bits/stdc++.h>  
using namespace std;  

#define MAXN 100  
// Infinite value for array  
const int INF = 1e7;  

int dis[MAXN][MAXN];  
int Next[MAXN][MAXN];  

// Initializing the distance and  
// Next array  
void initialise(int V,  
                vector<vector<int> >& graph)  
{  
    for (int i = 0; i < V; i++) {  
        for (int j = 0; j < V; j++) {  
            dis[i][j] = graph[i][j];  

            // No edge between node  
            // i and j  
            if (graph[i][j] == INF)  
                Next[i][j] = -1;  
            else
                Next[i][j] = j;  
        }  
    }  
}  

// Function construct the shotest  
// path between u and v  
vector<int> constructPath(int u,  
                        int v)  
{  
    // If there's no path between  
    // node u and v, simply return  
    // an empty array  
    if (Next[u][v] == -1)  
        return {};  

    // Storing the path in a vector  
    vector<int> path = { u };  
    while (u != v) {  
        u = Next[u][v];  
        path.push_back(u);  
    }  
    return path;  
}  

// Standard Floyd Warshall Algorithm  
// with little modification Now if we find  
// that dis[i][j] > dis[i][k] + dis[k][j]  
// then we modify next[i][j] = next[i][k]  
void floydWarshall(int V)  
{  
    for (int k = 0; k < V; k++) {  
        for (int i = 0; i < V; i++) {  
            for (int j = 0; j < V; j++) {  

                // We cannot travel through  
                // edge that doesn't exist  
                if (dis[i][k] == INF  
                    || dis[k][j] == INF)  
                    continue;  

                if (dis[i][j] > dis[i][k]  
                                    + dis[k][j]) {  
                    dis[i][j] = dis[i][k]  
                                + dis[k][j];  
                    Next[i][j] = Next[i][k];  
                }  
            }  
        }  
    }  
}  

// Print the shortest path  
void printPath(vector<int>& path)  
{  
    int n = path.size();  
    for (int i = 0; i < n - 1; i++)  
        cout << path[i] << " -> ";  
    cout << path[n - 1] << endl;  
}  

// Driver code  
int main()  
{  

    int V = 4;  
    vector<vector<int> > graph  
        = { { 0, 3, INF, 7 },  
            { 8, 0, 2, INF },  
            { 5, INF, 0, 1 },  
            { 2, INF, INF, 0 } };  

    // Function to initialise the  
    // distance and Next array  
    initialise(V, graph);  

    // Calling Floyd Warshall Algorithm,  
    // this will update the shortest  
    // distance as well as Next array  
    floydWarshall(V);  
    vector<int> path;  

    // Path from node 1 to 3  
    cout << "Shortest path from 1 to 3: ";  
    path = constructPath(1, 3);  
    printPath(path);  

    // Path from node 0 to 2  
    cout << "Shortest path from 0 to 2: ";  
    path = constructPath(0, 2);  
    printPath(path);  

    // path from node 3 to 2  
    cout << "Shortest path from 3 to 2: ";  
    path = constructPath(3, 2);  
    printPath(path);  

    return 0;  
}  

```**