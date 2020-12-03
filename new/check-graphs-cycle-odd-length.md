# 检查图形是否具有奇数长度的循环

> 原文： [https://www.geeksforgeeks.org/check-graphs-cycle-odd-length/](https://www.geeksforgeeks.org/check-graphs-cycle-odd-length/)

给定一个图，任务是查找它是否具有奇数长度的循环。

![](img/85a6f37cb7a8268dc6e68835117f6c8f.png)

![](img/251fb6c0d2bad3d10300fbb9eea310c1.png)

这个想法基于一个重要的事实，即当且仅当图为 [Bipartite](https://www.geeksforgeeks.org/bipartite-graph/) 时，图**并不**包含奇数长度的循环，即它可以用两种颜色着色。

显然，如果一个图具有奇长的周期，那么它就不能是二分图。 在二部图中，有两组顶点，因此，一组中的任何顶点都不会与同一组的任何其他顶点相连。 对于奇数长度的循环，必须连接相同集合的两个顶点，这与 Bipartite 定义相矛盾。

让我们理解相反的情况，如果图没有奇数环，则它必须是二分图。 以下是从[中获得的归纳证明，来自](http://infohost.nmt.edu/~math/faculty/barefoot/Math321Spring98/BipartiteGraphsAndEvenCycles.html) [http://infohost.nmt.edu/~math/faculty/barefoot/Math321Spring98/BipartiteGraphsAndEvenCycles.html](http://infohost.nmt.edu/~math/faculty/barefoot/Math321Spring98/BipartiteGraphsAndEvenCycles.html)

* * *

假设（X，Y）是 *G* 的整数，并且让 *C = u <sub>1</sub>* ， *u <sub>2</sub>* 。 。 。 ， *u <sub>k</sub>* 是 *G* 的一个周期，其中 *u <sub>1</sub>* 在顶点集 X 中（缩写 *u <sub>1</sub>* ∈X）。 如果 *u <sub>1∈</sub>* X，则 *u <sub>2∈</sub>* 是。 。 。 通常， *u <sub>2j + 1∈</sub>* X 和 *u <sub>2i∈</sub>* Y。由于 C 是一个循环，因此 *u <sub>k∈</sub>* Y，因此对于某个正整数 *s， *k* = 2 *s* 。* 因此，周期 *C* 是偶数。

假设图 *G* 没有奇数周期。 将显示出这样的图是二部图。 证明是边数量的归纳。 对于具有最多一个边的图，该断言显然是正确的。 假设每个没有奇数循环且最多 *q* 个边的图都是二分图，并且让 *G* 是具有 *q* + 1 个边且没有奇数循环的图。 令 *e = uv* 为 *G* 的边，并考虑图 *H = G – uv。* 通过感应， *H* 具有二分（X，Y）。 如果 *e* 的一端在 *X* 中，另一端在 *Y* 中，则（ *X* ， *Y* ）为 *G* 的两部分。 因此，假设 *u* 和 *v* 在 *X* 中。 如果在 *H* 中的 *u* 和 *v* 之间存在 *P* 路径，则 *P* 的长度将 保持平衡 因此， *P + uv* 将是 *G* 的奇数周期。 因此， *u* 和 *v* 必须位于 *H* 的不同“件”或组件中。 因此，我们有：

![](img/eb5ef74b13f35148ed8489bfc06eccce.png)其中， *X = X1 & X2* 和 *Y = Y1 = Y2* 。 在这种情况下，很明显 *X1 = Y2，X2 = Y1 是 *G 的二等分。**

![](img/9088aaa6e243d2e6f0e31661bab3f80a.png)

因此，我们得出结论，每个没有奇数环的图都是二分图。 可以如下构造一个二等分：
（1）选择一个任意顶点 *x <sub>0</sub>* 并设置 *X <sub>0</sub>* = { *x <sub>0</sub>* }。
（2）令 *Y <sub>0</sub>* 为与 *x <sub>0</sub>* 相邻的所有顶点的集合，并重复步骤 3-4。
（3）假设 *X <sub>k</sub>* 为未选择的与 *Y <sub>k-1</sub>* 顶点相邻的顶点的集合 ]。
（4）令 *Y <sub>k</sub>* 为与 *X <sub>k-1</sub>* 顶点相邻的未选择顶点的集合 ]。
（5）如果选择了 *G* 的所有顶点，则
*X = X <sub>0</sub> ∪X <sub>1</sub> ∪X <sub>2</sub> ∪。 。 。* 和 *Y = Y <sub>0</sub> ∪Y <sub>1</sub> ∪Y <sub>2</sub> ∪。 。 。*

* * *

下面是检查图形是否具有奇数循环的代码。 该代码基本上检查图是否为 Bipartite。

## C++

```cpp

// C++ program to find out whether a given graph is 
// Bipartite or not 
#include <bits/stdc++.h> 
#define V 4 
using namespace std; 

// This function returns true if graph G[V][V] contains 
// odd cycle, else false 
bool containsOdd(int G[][V], int src) 
{ 
    // Create a color array to store colors assigned  
    // to all veritces. Vertex number is used as index  
    // in this array. The value '-1' of  colorArr[i]  
    // is used to indicate that no color is assigned to 
    // vertex 'i'.  The value 1 is used to indicate first  
    // color is assigned and value 0 indicates second  
    // color is assigned. 
    int colorArr[V]; 
    for (int i = 0; i < V; ++i) 
        colorArr[i] = -1; 

    // Assign first color to source 
    colorArr[src] = 1; 

    // Create a queue (FIFO) of vertex numbers and  
    // enqueue source vertex for BFS traversal 
    queue <int> q; 
    q.push(src); 

    // Run while there are vertices in queue (Similar to BFS) 
    while (!q.empty()) 
    { 
        // Dequeue a vertex from queue  
        int u = q.front(); 
        q.pop(); 

        // Return true if there is a self-loop  
        if (G[u][u] == 1) 
           return true;   

        // Find all non-colored adjacent vertices 
        for (int v = 0; v < V; ++v) 
        { 
            // An edge from u to v exists and destination 
            // v is not colored 
            if (G[u][v] && colorArr[v] == -1) 
            { 
                // Assign alternate color to this adjacent 
                // v of u 
                colorArr[v] = 1 - colorArr[u]; 
                q.push(v); 
            } 

            // An edge from u to v exists and destination 
            // v is colored with same color as u 
            else if (G[u][v] && colorArr[v] == colorArr[u]) 
                return true; 
        } 
    } 

    // If we reach here, then all adjacent  
    // vertices can be colored with alternate 
    // color 
    return false; 
} 

// Driver program to test above function 
int main() 
{ 
    int G[][V] = {{0, 1, 0, 1}, 
        {1, 0, 1, 0}, 
        {0, 1, 0, 1}, 
        {1, 0, 1, 0} 
    }; 

    containsOdd(G, 0) ? cout << "Yes" : cout << "No"; 
    return 0; 
} 

```