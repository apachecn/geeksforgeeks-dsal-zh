# 绘制图形所需的最小颜色数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-colors-required-to-color-a-graph/](https://www.geeksforgeeks.org/minimum-number-of-colors-required-to-color-a-graph/)

给定一个具有`N`个顶点和`E`边的图。 边被指定为 **U []** 和 **V []** ，以便对于每个索引 i， **U [i]** 连接到 **V [i ]** 。 任务是找到给定图形着色所需的最小颜色数。

**范例**

> **输入**：N = 5，M = 6，U [] = {1，2，3，1，2，3}，V [] = {3，3，4，4，5，5 };
> **输出**：3
> **说明**：
> 对于上述图形节点，1、3 和 5 不能具有相同的颜色。 因此，计数为 3。

**方法**：
我们将保留两个数组**计数[]** 和**颜色[]** 。 数组 **count []** 将存储每个节点的边数，而 **colors []** 将存储每个节点的颜色。 将每个顶点的计数初始化为 0，将每个顶点的颜色初始化为 1。
**步骤**：

1.  为给定的一组边创建邻接表，并保留每个节点的边数
2.  遍历所有节点并将该节点插入没有边缘的队列`Q`中。
3.  当`Q`不为空时，请执行以下操作：
    *   从队列中弹出元素。
    *   对于连接到弹出节点的所有节点：
        1.  减少弹出节点的当前边沿计数。
        2.  如果当前颜色小于或等于其父级（弹出的节点）的颜色，则更新当前节点的颜色= 1 +弹出节点的颜色
        3.  如果 count 为零，则将该节点插入队列`Q`中。
4.  **colors []** 数组中的最大元素将给出给定图形着色所需的最小颜色数。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the minimum 
// number of colors needed to color 
// the graph 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count the minimum 
// number of color required 
void minimumColors(int N, int E, 
                   int U[], int V[]) 
{ 

    // Create array of vectors 
    // to make adjacency list 
    vector<int> adj[N]; 

    // Intialise colors array to 1 
    // and count array to 0 
    vector<int> count(N, 0); 
    vector<int> colors(N, 1); 

    // Create adjacency list of 
    // a graph 
    for (int i = 0; i < N; i++) { 
        adj[V[i] - 1].push_back(U[i] - 1); 
        count[U[i] - 1]++; 
    } 

    // Declare queue Q 
    queue<int> Q; 

    // Traverse count[] and insert 
    // in Q if count[i] = 0; 
    for (int i = 0; i < N; i++) { 
        if (count[i] == 0) { 
            Q.push(i); 
        } 
    } 

    // Traverse queue and update 
    // the count of colors 
    // adjacent node 
    while (!Q.empty()) { 
        int u = Q.front(); 
        Q.pop(); 

        // Traverse node u 
        for (auto x : adj[u]) { 
            count[x]--; 

            // If count[x] = 0 
            // insert in Q 
            if (count[x] == 0) { 
                Q.push(x); 
            } 

            // If colors of child 
            // node is less than 
            // parent node, update 
            // the count by 1 
            if (colors[x] <= colors[u]) { 
                colors[x] = 1 + colors[u]; 
            } 
        } 
    } 

    // Stores the minimumColors 
    // requires to color the graph. 
    int minColor = -1; 

    // Find the maximum of colors[] 
    for (int i = 0; i < N; i++) { 
        minColor = max(minColor, colors[i]); 
    } 

    // Print the minimum no. of 
    // colors required. 
    cout << minColor << endl; 
} 

// Driver function 
int main() 
{ 
    int N = 5, E = 6; 
    int U[] = { 1, 2, 3, 1, 2, 3 }; 
    int V[] = { 3, 3, 4, 4, 5, 5 }; 

    minimumColors(N, E, U, V); 
    return 0; 
} 

```