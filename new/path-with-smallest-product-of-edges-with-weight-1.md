# 权重为> = 1

的边的乘积最小的路径

> 原文： [https://www.geeksforgeeks.org/path-with-smallest-product-of-edges-with-weight-1/](https://www.geeksforgeeks.org/path-with-smallest-product-of-edges-with-weight-1/)

给定一个有向图，其中有**个 N** 个节点和 **E 个**边缘，其中每个边缘的权重为 **> 1** ，还给出了源 **S** 和目的地 **D** 。 任务是找到从 **S** 到 **D** 的边的最小积的路径。 如果没有从 **S** 到 **D** 的路径，则打印 **-1** 。

**示例：**

> **输入：** N = 3，E = 3，边线= {{{{1，2}，5}，{{1，3}，9}，{{2，3}，1}}， S = 1，D = 3
> **输出：** 5
> 边乘积最小的路径为 1- > 2- > 3
> ，乘积为 5 * 1 = 5。
> 
> **输入：** N = 3，E = 3，边线= {{{{3，2}，5}，{{3，3}，9}，{{3，3}，1}}， S = 1，D = 3
> **输出：** -1

**方法：**这个想法是使用 [Dijkstra 的最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)并稍有变化。
可以按照以下步骤计算结果：

*   如果源等于目的地，则返回 **0** 。
*   使用 **S** 初始化其优先级队列 **pq** ，并将其权重设置为 **1** 和访问数组 **v []** 。
*   当 **pq** 不为空时：
    1.  从 **pq** 中弹出最上面的元素。 我们将其称为 **curr** ，其距离乘积称为 **dist** 。
    2.  如果**当前**已被访问，则继续。
    3.  如果**发生**等于 **D** ，则返回 **dist** 。
    4.  迭代与**相邻的所有节点 curr** 并压入 **pq** （next 和 dist + gr [nxt] .weight）
*   返回 **-1** 。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the smallest 
// product of edges 
double dijkstra(int s, int d, 
                vector<vector<pair<int, double> > > gr) 
{ 
    // If the source is equal 
    // to the destination 
    if (s == d) 
        return 0; 

    // Initialise the priority queue 
    set<pair<int, int> > pq; 
    pq.insert({ 1, s }); 

    // Visited array 
    bool v[gr.size()] = { 0 }; 

    // While the priority-queue 
    // is not empty 
    while (pq.size()) { 

        // Current node 
        int curr = pq.begin()->second; 

        // Current product of distance 
        int dist = pq.begin()->first; 

        // Popping the top-most element 
        pq.erase(pq.begin()); 

        // If already visited continue 
        if (v[curr]) 
            continue; 

        // Marking the node as visited 
        v[curr] = 1; 

        // If it is a destination node 
        if (curr == d) 
            return dist; 

        // Traversing the current node 
        for (auto it : gr[curr]) 
            pq.insert({ dist * it.second, it.first }); 
    } 

    // If no path exists 
    return -1; 
} 

// Driver code 
int main() 
{ 
    int n = 3; 

    // Graph as adjacency matrix 
    vector<vector<pair<int, double> > > gr(n + 1); 

    // Input edges 
    gr[1].push_back({ 3, 9 }); 
    gr[2].push_back({ 3, 1 }); 
    gr[1].push_back({ 2, 5 }); 

    // Source and destination 
    int s = 1, d = 3; 

    // Dijkstra 
    cout << dijkstra(s, d, gr); 

    return 0; 
} 

```