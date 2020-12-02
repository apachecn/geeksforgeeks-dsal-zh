# 查找到达阵列末端的最小移动次数

> 原文： [https://www.geeksforgeeks.org/find-the-minimum-number-of-moves-to-reach-end-of-the-array/](https://www.geeksforgeeks.org/find-the-minimum-number-of-moves-to-reach-end-of-the-array/)

给定大小为 **N** 的数组 **arr []** ，其中每个元素都在 **[0，9]** 范围内。 任务是从第一个索引开始到达数组的最后一个索引。 从**第<sup>个</sup>** 索引，我们可以移至**（i – 1）<sup>第</sup>** ，**（i + 1）**或任何 **j <sup>第</sup>** 索引，其中 **j≠i** 和 **arr [j] = arr [i]** 。

**示例：**

> **输入：** arr [] = {1，2，3，4，1，5}
> **输出：** 2
> 从第 0 个位置开始 <sup>HTG7]索引指向第 4 <sup>个索引
> ，然后从第 4 <sup>个</sup>索引到第 5 <sup>个索引</sup>。</sup></sup>
> 
> **输入：** arr [] = {1、2、3、4、5、1}
> **输出：** 1

**方法：**从给定的数组构造图形，其中图形中的节点数将等于数组的大小。 图 **i** 的每个节点都将连接到**（i 1） <sup>th</sup>** 节点，**（i +1） <sup>th [HTG10</sup>** 节点和节点 **j** ，使得 **i≠j** 和 **arr [i] = arr [j]** 。 现在，答案将是所构建图形中从索引 **0** 到索引 **N – 1** 的路径中的最小边。
数组 arr [] = {1、2、3、4、1、5}的图形如下图所示：
![](img/c453163a63ad255b45929d9367b68afe.png)

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 
#define N 100005 

vector<int> gr[N]; 

// Function to add edge 
void add_edge(int u, int v) 
{ 
    gr[u].push_back(v); 
    gr[v].push_back(u); 
} 

// Function to return the minimum path 
// from 0th node to the (n - 1)th node 
int dijkstra(int n) 
{ 
    // To check whether an edge is visited or not 
    // and to keep distance of vertex from 0th index 
    int vis[n] = { 0 }, dist[n]; 

    for (int i = 0; i < n; i++) 
        dist[i] = INT_MAX; 

    // Make 0th index visited and distance is zero 
    vis[0] = 1; 
    dist[0] = 0; 

    // Take a queue and push first element 
    queue<int> q; 
    q.push(0); 

    // Continue this until all vertices are visited 
    while (!q.empty()) { 
        int x = q.front(); 

        // Remove the first element 
        q.pop(); 

        for (int i = 0; i < gr[x].size(); i++) { 

            // Check if a vertex is already visited or not 
            if (vis[gr[x][i]] == 1) 
                continue; 

            // Make vertex visited 
            vis[gr[x][i]] = 1; 

            // Store the number of moves to reach element 
            dist[gr[x][i]] = dist[x] + 1; 

            // Push the current vertex into the queue 
            q.push(gr[x][i]); 
        } 
    } 

    // Return the minimum number of 
    // moves to reach (n - 1)th index 
    return dist[n - 1]; 
} 

// Function to return the minimum number of moves 
// required to reach the end of the array 
int Min_Moves(int a[], int n) 
{ 

    // To store the positions of each element 
    vector<int> fre[10]; 
    for (int i = 0; i < n; i++) { 
        if (i != n - 1) 
            add_edge(i, i + 1); 

        fre[a[i]].push_back(i); 
    } 

    // Add edge between same elements 
    for (int i = 0; i < 10; i++) { 
        for (int j = 0; j < fre[i].size(); j++) { 
            for (int k = j + 1; k < fre[i].size(); k++) { 
                if (fre[i][j] + 1 != fre[i][k] 
                    and fre[i][j] - 1 != fre[i][k]) { 
                    add_edge(fre[i][j], fre[i][k]); 
                } 
            } 
        } 
    } 

    // Return the required minimum number of moves 
    return dijkstra(n); 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 2, 3, 4, 1, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    cout << Min_Moves(a, n); 

    return 0; 
} 

```