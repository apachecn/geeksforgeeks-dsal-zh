# 使用二分查找法查找图的最小顶点覆盖大小

> 原文： [https://www.geeksforgeeks.org/finding-minimum-vertex-cover-graph-using-binary-search/](https://www.geeksforgeeks.org/finding-minimum-vertex-cover-graph-using-binary-search/)

无向图的[顶点覆盖](https://www.geeksforgeeks.org/vertex-cover-problem-set-1-introduction-approximate-algorithm-2/)是其顶点的子集，因此对于图的每个边缘（u，v），“ u”或“ v”都在顶点覆盖中。 图可能有很多顶点覆盖。

**问题**对于具有 V 个顶点和 m 个边的无向连接图，找到最小尺寸的顶点覆盖的大小，即具有最小基数的顶点覆盖的基数。

**示例**：

```
Input: V = 6, E = 6
             6
                /
           /
          1 -----5
         /|\
        3 | \
        \ |  \
          2   4
Output: Minimum vertex cover size = 2
Consider subset of vertices {1, 2}, every edge 
in above graph is either incident on vertex 1 
or 2\. Hence the minimum vertex cover = {1, 2}, 
the size of which is 2.

Input: V = 6, E = 7
           2 ---- 4 ---- 6
          /|      |
        1  |      |
          \|      |
           3 ---- 5
Output: Minimum vertex cover size = 3
Consider subset of vertices {2, 3, 4}, every
edge in above graph is either incident on 
vertex 2, 3 or 4\. Hence the minimum size of
a vertex cover can be 3.

```

**方法 1（朴素）**
我们可以使用以下算法在 O（E + V）时间中检查给定的顶点子集是否为顶点覆盖。

```
Generate all 2V subsets of vertices in graph and
do following for every subset.
  1\. edges_covered = 0
  2\. for each vertex in current subset
  3\.   for all edges emerging out of current vertex
  4\.      if the edge is not already marked visited
  5\.          mark the edge visited
  6\.          edges_covered++
  7\. if edges_covered is equal to total number edges
  8\.   return size of current subset

```

此解决方案的时间复杂度上限为 O（（E + V）* 2 <sup>V</sup> ）

**方法 2（二分查找）**
如果我们首先通过生成 <sup>V</sup> C <sub>V</sub> 子集，然后生成<sup>，则生成 2 个 <sup>V</sup> 子集 ] V</sup> C <sub>（V-1）</sub>子集，依此类推，直到 <sup>V</sup> C <sub>0</sub> 子集（2 <sup>V</sup> = HTG19] V C <sub>V</sub> + <sup>V</sup> C <sub>（V-1）</sub> +…+ <sup>V</sup> C <sub>1 [</sub> + <sup>V</sup> C <sub>0</sub> ）。 现在我们的目标是找到最小 k，以使 <sup>V</sup> C <sub>k</sub> 子集中的大小为“ k”的至少一个子集是一个顶点覆盖[我们知道如果最小尺寸的顶点覆盖 的大小为 k，则将存在所有大小大于 k 的顶点覆盖。 也就是说，将存在一个大小为 k + 1，k + 2，k + 3，…，n 的顶点覆盖。 ]

现在，让我们想象一个大小为 n 的布尔数组，并将其称为 isCover []。 因此，如果问题的答案； “是否存在大小为 x 的顶点覆盖？” 是的，我们在第 x 个位置放置一个“ 1”，否则放置“ 0”。

数组 isCover []将如下所示：

| 1 | 2 | 3 | . | . | . | 至 | . | . | . | ñ |
| 0 | 0 | 0 | . | . | . | 1 | . | . | . | 1 |

由于`k`之前没有索引将为'1'，并且`k`（包括两端）之后的每个索引都将为'1'，因此该数组已排序，因此可以进行二进制搜索。 HTG4] k 是答案。

因此，我们可以应用二进制搜索来查找覆盖所有边缘的最小尺寸的顶点集（此问题等同于在 isCover []中找到最后一个 1）。 现在的问题是如何生成给定大小的所有子集。 这个想法是使用 Gosper 的骇客。

**什么是 Gosper 的骇客？**
戈斯珀（Gosper）的骇客技巧是一种获得设置了相同位数的下一个数字的技术。 因此，我们从右开始设置前 x 位，并生成 x 位已设置的下一个数字，直到该数字小于 2 <sup>V</sup> 为止。 这样，我们可以生成设置了 x 位的所有 <sup>V</sup> Cx 号。

```

int set = (1 << k) - 1; 
int limit = (1 << V); 
while (set < limit)  
{ 
    // Do your stuff with current set 
    doStuff(set); 

    // Gosper's hack: 
    int c = set & -set; 
    int r = set + c; 
    set = (((r^set) >>> 2) / c) | r; 
} 

```

来源： [StackExchange](http://programmers.stackexchange.com/questions/67065/whats-your-favorite-bit-wise-technique)

我们使用闲聊的技巧来生成大小为 x（0 < x <= V), that is, to check whether we have a '1' or '0' at any index x in isCover[] array.

## C ++

```

// A C++ program to find size of minimum vertex 
// cover using Binary Search 
#include<bits/stdc++.h> 
#define maxn 25 

using namespace std; 

// Global array to store the graph 
// Note: since the array is global, all the 
// elements are 0 initially 
bool gr[maxn][maxn]; 

// Returns true if there is a possible subset 
// of size 'k' that can be a vertex cover 
bool isCover(int V, int k, int E) 
{ 
    // Set has first 'k' bits high initially 
    int set = (1 << k) - 1; 

    int limit = (1 << V); 

    // to mark the edges covered in each subset 
    // of size 'k' 
    bool vis[maxn][maxn]; 

    while (set < limit) 
    { 
        // Reset visited array for every subset 
        // of vertices 
        memset(vis, 0, sizeof vis); 

        // set counter for number of edges covered 
        // from this subset of vertices to zero 
        int cnt = 0; 

        // selected vertex cover is the indices 
        // where 'set' has its bit high 
        for (int j = 1, v = 1 ; j < limit ; j = j << 1, v++) 
        { 
            if (set & j) 
            { 
                // Mark all edges emerging out of this 
                // vertex visited 
                for (int k = 1 ; k <= V ; k++) 
                { 
                    if (gr[v][k] && !vis[v][k]) 
                    { 
                        vis[v][k] = 1; 
                        vis[k][v] = 1; 
                        cnt++; 
                    } 
                } 
            } 
        } 

        // If the current subset covers all the edges 
        if (cnt == E) 
            return true; 

        // Generate previous combination with k bits high 
        // set & -set = (1 << last bit high in set) 
        int c = set & -set; 
        int r = set + c; 
        set = (((r^set) >> 2) / c) | r; 
    } 
    return false; 
} 

// Returns answer to graph stored in gr[][] 
int findMinCover(int n, int m) 
{ 
    // Binary search the answer 
    int left = 1, right = n; 
    while (right > left) 
    { 
        int mid = (left + right) >> 1; 
        if (isCover(n, mid, m) == false) 
            left = mid + 1; 
        else
            right = mid; 
    } 

    // at the end of while loop both left and 
    // right will be equal,/ as when they are 
    // not, the while loop won't exit the minimum 
    // size vertex cover = left = right 
    return left; 
} 

// Inserts an edge in the graph 
void insertEdge(int u, int v) 
{ 
    gr[u][v] = 1; 
    gr[v][u] = 1;  // Undirected graph 
} 

// Driver code 
int main() 
{ 
    /* 
            6 
           / 
          1 ----- 5   vertex cover = {1, 2} 
         /|\ 
        3 | \ 
        \ |  \ 
          2   4   */
    int V = 6, E = 6; 
    insertEdge(1, 2); 
    insertEdge(2, 3); 
    insertEdge(1, 3); 
    insertEdge(1, 4); 
    insertEdge(1, 5); 
    insertEdge(1, 6); 
    cout << "Minimum size of a vertex cover = "
         << findMinCover(V, E) << endl; 

    // Let us create another graph 
    memset(gr, 0, sizeof gr); 
    /* 
           2 ---- 4 ---- 6 
          /|      | 
        1  |      |   vertex cover = {2, 3, 4} 
         \ |      | 
           3 ---- 5    */

    V = 6, E = 7; 
    insertEdge(1, 2); 
    insertEdge(1, 3); 
    insertEdge(2, 3); 
    insertEdge(2, 4); 
    insertEdge(3, 5); 
    insertEdge(4, 5); 
    insertEdge(4, 6); 
    cout << "Minimum size of a vertex cover = "
         << findMinCover(V, E) << endl; 

    return 0; 
} 

```