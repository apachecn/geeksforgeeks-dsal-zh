# 在 C ++中使用 STL 的 Kruskal 最小生成树

> 原文： [https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-using-stl-in-c/](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-using-stl-in-c/)

给定一个无向，连通和加权的图，请使用 Kruskal 算法找到图的`M`最小`S`平移`T`ree（MST）。

```
![](img/576b7bbdf820c1b3c849c6d34f16d7b4.png "Fig-1")

Input :   Graph as an array of edges
Output :  Edges of MST are 
          6 - 7
          2 - 8
          5 - 6
          0 - 1
          2 - 5
          2 - 3
          0 - 7
          3 - 4

          Weight of MST is 37

Note :  There are two possible MSTs, the other
        MST includes edge 1-2 in place of 0-7\. 

```

我们下面讨论了 Kruskal 的 MST 实现。

[贪心算法| 第 2 组（Kruskal 的最小生成树算法）](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/)

以下是使用 Kruskal 算法查找 MST 的步骤

1.  按重量的递减顺序对所有边缘进行排序。
2.  选择最小的边缘。 检查它是否与形成的生成树形成一个循环。 如果未形成循环，则包括该边。 否则，将其丢弃。
3.  重复步骤 2，直到生成树中有（V-1）个边。

以下是对我们使用 STL 实施 Kruskal 算法的一些关键点。

1.  Use a vector of edges which consist of all the edges in the graph and each item of a vector will contain 3 parameters: source, destination and the cost of an edge between the source and destination.

    ```
    		vector<pair<int, pair<int, int> > > edges;
    ```

    此处，在外部对（即<int>对）中，第一个元素对应于一条边的代价，而第二个元素本身就是一对，并包含两个边的顶点。</int>

2.  使用内置的 [std :: sort](https://www.geeksforgeeks.org/sort-c-stl/) 以非降序对边进行排序； 默认情况下，sort 函数以非降序排序。
3.  我们使用[联合查找算法](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)来检查当前边是否已添加到当前 MST 中，它是否构成了一个循环。 如果是，则将其丢弃，否则将其包含（联合）。

**伪代码**：

```
// Initialize result
mst_weight = 0

// Create V single item sets
for each vertex v
	parent[v] = v;
	rank[v] = 0;

Sort all edges into non decreasing 
order by weight w

for each (u, v) taken from the sorted list  E
    do if FIND-SET(u) != FIND-SET(v)
        print edge(u, v)
        mst_weight += weight of edge(u, v)
        UNION(u, v)

```

下面是上述算法的 C ++实现。

```

// C++ program for Kruskal's algorithm to find Minimum 
// Spanning Tree of a given connected, undirected and 
// weighted graph 
#include<bits/stdc++.h> 
using namespace std; 

// Creating shortcut for an integer pair 
typedef  pair<int, int> iPair; 

// Structure to represent a graph 
struct Graph 
{ 
    int V, E; 
    vector< pair<int, iPair> > edges; 

    // Constructor 
    Graph(int V, int E) 
    { 
        this->V = V; 
        this->E = E; 
    } 

    // Utility function to add an edge 
    void addEdge(int u, int v, int w) 
    { 
        edges.push_back({w, {u, v}}); 
    } 

    // Function to find MST using Kruskal's 
    // MST algorithm 
    int kruskalMST(); 
}; 

// To represent Disjoint Sets 
struct DisjointSets 
{ 
    int *parent, *rnk; 
    int n; 

    // Constructor. 
    DisjointSets(int n) 
    { 
        // Allocate memory 
        this->n = n; 
        parent = new int[n+1]; 
        rnk = new int[n+1]; 

        // Initially, all vertices are in 
        // different sets and have rank 0\. 
        for (int i = 0; i <= n; i++) 
        { 
            rnk[i] = 0; 

            //every element is parent of itself 
            parent[i] = i; 
        } 
    } 

    // Find the parent of a node 'u' 
    // Path Compression 
    int find(int u) 
    { 
        /* Make the parent of the nodes in the path 
           from u--> parent[u] point to parent[u] */
        if (u != parent[u]) 
            parent[u] = find(parent[u]); 
        return parent[u]; 
    } 

    // Union by rank 
    void merge(int x, int y) 
    { 
        x = find(x), y = find(y); 

        /* Make tree with smaller height 
           a subtree of the other tree  */
        if (rnk[x] > rnk[y]) 
            parent[y] = x; 
        else // If rnk[x] <= rnk[y] 
            parent[x] = y; 

        if (rnk[x] == rnk[y]) 
            rnk[y]++; 
    } 
}; 

 /* Functions returns weight of the MST*/ 

int Graph::kruskalMST() 
{ 
    int mst_wt = 0; // Initialize result 

    // Sort edges in increasing order on basis of cost 
    sort(edges.begin(), edges.end()); 

    // Create disjoint sets 
    DisjointSets ds(V); 

    // Iterate through all sorted edges 
    vector< pair<int, iPair> >::iterator it; 
    for (it=edges.begin(); it!=edges.end(); it++) 
    { 
        int u = it->second.first; 
        int v = it->second.second; 

        int set_u = ds.find(u); 
        int set_v = ds.find(v); 

        // Check if the selected edge is creating 
        // a cycle or not (Cycle is created if u 
        // and v belong to same set) 
        if (set_u != set_v) 
        { 
            // Current edge will be in the MST 
            // so print it 
            cout << u << " - " << v << endl; 

            // Update MST weight 
            mst_wt += it->first; 

            // Merge two sets 
            ds.merge(set_u, set_v); 
        } 
    } 

    return mst_wt; 
} 

// Driver program to test above functions 
int main() 
{ 
    /* Let us create above shown weighted 
       and unidrected graph */
    int V = 9, E = 14; 
    Graph g(V, E); 

    //  making above shown graph 
    g.addEdge(0, 1, 4); 
    g.addEdge(0, 7, 8); 
    g.addEdge(1, 2, 8); 
    g.addEdge(1, 7, 11); 
    g.addEdge(2, 3, 7); 
    g.addEdge(2, 8, 2); 
    g.addEdge(2, 5, 4); 
    g.addEdge(3, 4, 9); 
    g.addEdge(3, 5, 14); 
    g.addEdge(4, 5, 10); 
    g.addEdge(5, 6, 2); 
    g.addEdge(6, 7, 1); 
    g.addEdge(6, 8, 6); 
    g.addEdge(7, 8, 7); 

    cout << "Edges of MST are \n"; 
    int mst_wt = g.kruskalMST(); 

    cout << "\nWeight of MST is " << mst_wt; 

    return 0; 
} 

```

输出：

```
 Edges of MST are 
          6 - 7
          2 - 8
          5 - 6
          0 - 1
          2 - 5
          2 - 3
          0 - 7
          3 - 4

          Weight of MST is 37
```

**优化**：
上面的代码可以优化，以在所选边的数量变为 V-1 时停止 Kruskal 的主循环。 我们知道 MST 具有 V-1 边缘，并且在选择 V-1 边缘后没有点迭代。 我们没有添加此优化来使代码保持简单。

**参考**：
[Cormen Leiserson Rivest and Stein（CLRS）3 的算法简介](http://www.amazon.in/Introduction-Algorithms-Thomas-H-Cormen/dp/8120340078/ref=sr_1_1?ie=UTF8&qid=1459619144&sr=8-1&keywords=clrs)

时间复杂度和逐步说明已在[上一篇有关 Kruskal 算法的文章中进行了讨论。](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/)

本文由 **Chirag Agrawal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

