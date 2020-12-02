# 最低费用图表

> 原文： [https://www.geeksforgeeks.org/minimum-cost-graph/](https://www.geeksforgeeks.org/minimum-cost-graph/)

给定表示为**的二维平面上的 **N 个**节点（x <sub>i</sub> ，y <sub>i</sub> ）**。 如果节点之间的曼哈顿距离为 **1** ，则称这些节点已连接。 您可以连接两个未连接的节点，但要以它们之间的欧式距离为代价。 任务是连接图，以便每个节点都有一条从任何节点到其路径的路径，且成本最低。

**示例：**

> **输入：** N = 3，边缘[] [] = {{1，1}，{1，1}，{2，2}，{3，2}}
> **输出 ：** 1.41421
> 由于（2，2）和（2，3）已经连接。
> 因此，我们尝试将（1，1）与（2，2）
> 或（1，1）与（2，3）连接，但将（1，1）与（2，2）
> 连接 产生最小的成本。
> 
> **输入：** N = 3，edges [] [] = {{1，1}，{2，2}，{3，3}}
> **输出：** 2.82843

**方法：**蛮力方法是将每个节点与每个其他节点连接，类似地，将其他 **N** 个节点连接起来，但在最坏的情况下，时间复杂度将为 **N <sup>N</sup>** 。
另一种方法是找到具有欧几里得距离的每对顶点的成本，并且那些相连的对的成本为 **0** 。
在知道了每对的代价之后，我们将 [Kruskal 算法](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)应用于最小生成树，它将产生连接图的最小代价。 请注意，对于 Kruskal 算法，您必须具有[不交集集合联合（DSU）](https://www.geeksforgeeks.org/disjoint-set-data-structures/)的知识。

下面是上述方法的实现：

```

// C++ implentation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Max number of nodes given 
const int N = 500 + 10; 

// arr is the parent array 
// sz is the size of the 
// subtree in DSU 
int arr[N], sz[N]; 

// Function to initilize the parent 
// and size array for DSU 
void initialize() 
{ 
    for (int i = 1; i < N; ++i) { 
        arr[i] = i; 
        sz[i] = 1; 
    } 
} 

// Function to return the 
// parent of the node 
int root(int i) 
{ 
    while (arr[i] != i) 
        i = arr[i]; 
    return i; 
} 

// Function to perform the 
// merge operation 
void unin(int a, int b) 
{ 
    a = root(a); 
    b = root(b); 

    if (a != b) { 
        if (sz[a] < sz[b]) 
            swap(a, b); 

        sz[a] += sz[b]; 
        arr[b] = a; 
    } 
} 

// Function to return the minimum cost required 
double minCost(vector<pair<int, int> >& p) 
{ 

    // Number of points 
    int n = (int)p.size(); 

    // To store the cost of every possible pair 
    // as { cost, {to, from}}. 
    vector<pair<double, pair<int, int> > > cost; 

    // Calculating the cost of every possible pair 
    for (int i = 0; i < n; ++i) { 
        for (int j = 0; j < n; ++j) { 
            if (i != j) { 

                // Getting Manhattan distance 
                int x = abs(p[i].first - p[j].first) 
                        + abs(p[i].second - p[j].second); 

                // If the distance is 1 the cost is 0 
                // or already connected 
                if (x == 1) { 
                    cost.push_back({ 0, { i + 1, j + 1 } }); 
                    cost.push_back({ 0, { j + 1, i + 1 } }); 
                } 
                else { 

                    // Calculating the euclidean distance 
                    int a = p[i].first - p[j].first; 
                    int b = p[i].second - p[j].second; 
                    a *= a; 
                    b *= b; 
                    double d = sqrt(a + b); 
                    cost.push_back({ d, { i + 1, j + 1 } }); 
                    cost.push_back({ d, { j + 1, i + 1 } }); 
                } 
            } 
        } 
    } 

    // Krushkal Algorithm for Minimum 
    // spanning tree 
    sort(cost.begin(), cost.end()); 

    // To initialize the size and 
    // parent array 
    initialize(); 

    double ans = 0.00; 
    for (auto i : cost) { 
        double c = i.first; 
        int a = i.second.first; 
        int b = i.second.second; 

        // If the parents are different 
        if (root(a) != root(b)) { 
            unin(a, b); 
            ans += c; 
        } 
    } 

    return ans; 
} 

// Driver code 
int main() 
{ 

    // Vector pairs of points 
    vector<pair<int, int> > points = { 
        { 1, 1 }, 
        { 2, 2 }, 
        { 2, 3 } 
    }; 

    // Function calling and printing 
    // the answer 
    cout << minCost(points); 

    return 0; 
} 

```

**Output:**

```
1.41421

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。