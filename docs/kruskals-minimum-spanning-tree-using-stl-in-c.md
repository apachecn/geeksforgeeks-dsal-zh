# c++中使用 STL 的 Kruskal 最小生成树

> 原文:[https://www . geesforgeks . org/kruskals-最小生成树-使用-stl-in-c/](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-using-stl-in-c/)

给定一个无向图、连通图和加权图，使用克鲁斯卡尔算法找到图的最小**M**T2 S 平移 **T** ree (MST)。

```
![Kruskal's Minimum Spanning Tree using STL in C++](img/576b7bbdf820c1b3c849c6d34f16d7b4.png "Fig-1")

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

我们已经在下面讨论了 Kruskal 的 MST 实现。

[贪婪算法|集合 2(克鲁斯卡尔最小生成树算法)](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/)

以下是使用克鲁斯卡尔算法寻找最小二乘的步骤

1.  按照权重的非递减顺序对所有边进行排序。
2.  选择最小的边。检查它是否与到目前为止形成的生成树形成一个循环。如果没有形成循环，包括这条边。否则，丢弃它。
3.  重复步骤#2，直到生成树中有(V-1)条边。

这里有一些关键点，将有助于我们使用 STL 实现克鲁斯卡尔算法。

1.  Use a vector of edges which consist of all the edges in the graph and each item of a vector will contain 3 parameters: source, destination and the cost of an edge between the source and destination.

    ```
            vector<pair<int, pair<int, int> > > edges;
    ```

    这里，在外部对(即对<int>>)中，第一个元素对应于边的成本，而第二个元素本身是一对，并且它包含边的两个顶点。</int>

2.  使用内置的[标准::排序](https://www.geeksforgeeks.org/sort-c-stl/)以非递减顺序对边进行排序；默认情况下，排序函数按非递减顺序排序。
3.  我们使用[联合查找算法](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)来检查当前边是否形成一个循环，如果它被添加到当前的 MST 中。如果是，丢弃它，否则包括它(联合)。

**伪码:**

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

下面是上述算法的 C++实现。

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
        // different sets and have rank 0.
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
       and undirected graph */
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

输出:

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

**优化:**
上述代码可以进行优化，当选择的边数变为 V-1 时，停止 Kruskal 的主循环。我们知道 MST 有 V-1 条边，选择 V-1 条边后没有点迭代。我们没有添加这种优化来保持代码简单。

**参考文献:**
[科曼·莱瑟森·瑞文斯特和斯坦(CLRS)算法导论 3](http://www.amazon.in/Introduction-Algorithms-Thomas-H-Cormen/dp/8120340078/ref=sr_1_1?ie=UTF8&qid=1459619144&sr=8-1&keywords=clrs)

时间复杂性和逐步说明在[之前关于克鲁斯卡尔算法的文章中讨论过。](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/)

本文由 **Chirag Agrawal** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论