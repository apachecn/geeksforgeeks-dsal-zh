# 最大匹配的霍普克罗夫特-卡普算法|集合 2(实现)

> 原文:[https://www . geeksforgeeks . org/hopcroft-Karp-算法-最大匹配-集合-2-实现/](https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-2-implementation/)

我们强烈建议将以下帖子作为先决条件。
[最大匹配的 Hopcroft–Karp 算法|集合 1(简介)](https://www.geeksforgeeks.org/hopcroft-karp-algorithm-for-maximum-matching-set-1-introduction/)

在我们开始实施之前，很少有重要的事情需要注意。

1.  我们需要**找到一条增广路径**(一条在匹配边和不匹配边之间交替的路径，以自由顶点作为起点和终点)。
2.  一旦找到交替路径，我们需要**将找到的路径添加到现有的匹配**中。这里的添加路径是指，将该路径上先前匹配的边设为不匹配，将先前不匹配的边设为匹配。

这个想法是使用 BFS(广度优先搜索)来寻找扩充路径。因为 BFS 逐层遍历，所以它被用来将图分成匹配和不匹配边的层。添加一个虚拟顶点 NIL，它连接到左侧的所有顶点和右侧的所有顶点。以下数组用于查找扩充路径。到 NIL 的距离被初始化为 INF(无穷大)。如果我们从虚拟顶点开始，然后使用不同顶点的交替路径回到它，那么就有一个增广路径。

1.  pairU[]:大小为 m+1 的数组，其中 m 是二部图左侧的顶点数。如果 u 匹配，则在右侧存储 u 对，否则存储 NIL。
2.  pairV[]:大小为 n+1 的数组，其中 n 是二部图右侧的顶点数。如果 v 匹配，则 pairV[v]在左侧存储 v 对，否则存储 NIL。
3.  dist[]:大小为 m+1 的数组，其中 m 是二部图左侧的顶点数。如果 u 不匹配，dist[u]被初始化为 0，否则 INF(无穷大)。NIL 的 dist[]也被初始化为 INF

一旦找到扩充路径，深度优先搜索(DFS)被用于向当前匹配添加扩充路径。DFS 简单地遵循 BFS 设置的距离阵列。如果 v 在 BFS 的 u 旁边，它会填充 pairU[u]和 pairV[v]中的值。

下面是上面 Hopkroft 卡普算法的实现。

## C++14

```
// C++ implementation of Hopcroft Karp algorithm for
// maximum matching
#include<bits/stdc++.h>
using namespace std;
#define NIL 0
#define INF INT_MAX

// A class to represent Bipartite graph for Hopcroft
// Karp implementation
class BipGraph
{
    // m and n are number of vertices on left
    // and right sides of Bipartite Graph
    int m, n;

    // adj[u] stores adjacents of left side
    // vertex 'u'. The value of u ranges from 1 to m.
    // 0 is used for dummy vertex
    list<int> *adj;

    // These are basically pointers to arrays needed
    // for hopcroftKarp()
    int *pairU, *pairV, *dist;

public:
    BipGraph(int m, int n); // Constructor
    void addEdge(int u, int v); // To add edge

    // Returns true if there is an augmenting path
    bool bfs();

    // Adds augmenting path if there is one beginning
    // with u
    bool dfs(int u);

    // Returns size of maximum matching
    int hopcroftKarp();
};

// Returns size of maximum matching
int BipGraph::hopcroftKarp()
{
    // pairU[u] stores pair of u in matching where u
    // is a vertex on left side of Bipartite Graph.
    // If u doesn't have any pair, then pairU[u] is NIL
    pairU = new int[m+1];

    // pairV[v] stores pair of v in matching. If v
    // doesn't have any pair, then pairU[v] is NIL
    pairV = new int[n+1];

    // dist[u] stores distance of left side vertices
    // dist[u] is one more than dist[u'] if u is next
    // to u'in augmenting path
    dist = new int[m+1];

    // Initialize NIL as pair of all vertices
    for (int u=0; u<=m; u++)
        pairU[u] = NIL;
    for (int v=0; v<=n; v++)
        pairV[v] = NIL;

    // Initialize result
    int result = 0;

    // Keep updating the result while there is an
    // augmenting path.
    while (bfs())
    {
        // Find a free vertex
        for (int u=1; u<=m; u++)

            // If current vertex is free and there is
            // an augmenting path from current vertex
            if (pairU[u]==NIL && dfs(u))
                result++;
    }
    return result;
}

// Returns true if there is an augmenting path, else returns
// false
bool BipGraph::bfs()
{
    queue<int> Q; //an integer queue

    // First layer of vertices (set distance as 0)
    for (int u=1; u<=m; u++)
    {
        // If this is a free vertex, add it to queue
        if (pairU[u]==NIL)
        {
            // u is not matched
            dist[u] = 0;
            Q.push(u);
        }

        // Else set distance as infinite so that this vertex
        // is considered next time
        else dist[u] = INF;
    }

    // Initialize distance to NIL as infinite
    dist[NIL] = INF;

    // Q is going to contain vertices of left side only.
    while (!Q.empty())
    {
        // Dequeue a vertex
        int u = Q.front();
        Q.pop();

        // If this node is not NIL and can provide a shorter path to NIL
        if (dist[u] < dist[NIL])
        {
            // Get all adjacent vertices of the dequeued vertex u
            list<int>::iterator i;
            for (i=adj[u].begin(); i!=adj[u].end(); ++i)
            {
                int v = *i;

                // If pair of v is not considered so far
                // (v, pairV[V]) is not yet explored edge.
                if (dist[pairV[v]] == INF)
                {
                    // Consider the pair and add it to queue
                    dist[pairV[v]] = dist[u] + 1;
                    Q.push(pairV[v]);
                }
            }
        }
    }

    // If we could come back to NIL using alternating path of distinct
    // vertices then there is an augmenting path
    return (dist[NIL] != INF);
}

// Returns true if there is an augmenting path beginning with free vertex u
bool BipGraph::dfs(int u)
{
    if (u != NIL)
    {
        list<int>::iterator i;
        for (i=adj[u].begin(); i!=adj[u].end(); ++i)
        {
            // Adjacent to u
            int v = *i;

            // Follow the distances set by BFS
            if (dist[pairV[v]] == dist[u]+1)
            {
                // If dfs for pair of v also returns
                // true
                if (dfs(pairV[v]) == true)
                {
                    pairV[v] = u;
                    pairU[u] = v;
                    return true;
                }
            }
        }

        // If there is no augmenting path beginning with u.
        dist[u] = INF;
        return false;
    }
    return true;
}

// Constructor
BipGraph::BipGraph(int m, int n)
{
    this->m = m;
    this->n = n;
    adj = new list<int>[m+1];
}

// To add edge from u to v and v to u
void BipGraph::addEdge(int u, int v)
{
    adj[u].push_back(v); // Add u to v’s list.
}

// Driver Program
int main()
{
    BipGraph g(4, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 1);
    g.addEdge(3, 2);
    g.addEdge(4, 2);
    g.addEdge(4, 4);

    cout << "Size of maximum matching is " << g.hopcroftKarp();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of Hopcroft Karp
// algorithm for maximum matching
import java.util.ArrayList;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

class GFG{

static final int NIL = 0;
static final int INF = Integer.MAX_VALUE;

// A class to represent Bipartite graph
// for Hopcroft Karp implementation
static class BipGraph
{

    // m and n are number of vertices on left
    // and right sides of Bipartite Graph
    int m, n;

    // adj[u] stores adjacents of left side
    // vertex 'u'. The value of u ranges
    // from 1 to m. 0 is used for dummy vertex
    List<Integer>[] adj;

    // These are basically pointers to arrays
    // needed for hopcroftKarp()
    int[] pairU, pairV, dist;

    // Returns size of maximum matching
    int hopcroftKarp()
    {

        // pairU[u] stores pair of u in matching where u
        // is a vertex on left side of Bipartite Graph.
        // If u doesn't have any pair, then pairU[u] is NIL
        pairU = new int[m + 1];

        // pairV[v] stores pair of v in matching. If v
        // doesn't have any pair, then pairU[v] is NIL
        pairV = new int[n + 1];

        // dist[u] stores distance of left side vertices
        // dist[u] is one more than dist[u'] if u is next
        // to u'in augmenting path
        dist = new int[m + 1];

        // Initialize NIL as pair of all vertices
        Arrays.fill(pairU, NIL);
        Arrays.fill(pairV, NIL);

        // Initialize result
        int result = 0;

        // Keep updating the result while
        // there is an augmenting path.
        while (bfs())
        {

            // Find a free vertex
            for(int u = 1; u <= m; u++)

                // If current vertex is free and there is
                // an augmenting path from current vertex
                if (pairU[u] == NIL && dfs(u))
                    result++;
        }
        return result;
    }

    // Returns true if there is an augmenting
    // path, else returns false
    boolean bfs()
    {

        // An integer queue
        Queue<Integer> Q = new LinkedList<>();

        // First layer of vertices (set distance as 0)
        for(int u = 1; u <= m; u++)
        {

            // If this is a free vertex,
            // add it to queue
            if (pairU[u] == NIL)
            {

                // u is not matched
                dist[u] = 0;
                Q.add(u);
            }

            // Else set distance as infinite
            // so that this vertex is
            // considered next time
            else
                dist[u] = INF;
        }

        // Initialize distance to
        // NIL as infinite
        dist[NIL] = INF;

        // Q is going to contain vertices
        // of left side only.
        while (!Q.isEmpty())
        {

            // Dequeue a vertex
            int u = Q.poll();

            // If this node is not NIL and
            // can provide a shorter path to NIL
            if (dist[u] < dist[NIL])
            {

                // Get all adjacent vertices of
                // the dequeued vertex u
                for(int i : adj[u])
                {
                    int v = i;

                    // If pair of v is not considered
                    // so far (v, pairV[V]) is not yet
                    // explored edge.
                    if (dist[pairV[v]] == INF)
                    {

                        // Consider the pair and add
                        // it to queue
                        dist[pairV[v]] = dist[u] + 1;
                        Q.add(pairV[v]);
                    }
                }
            }
        }

        // If we could come back to NIL using
        // alternating path of distinct vertices
        // then there is an augmenting path
        return (dist[NIL] != INF);
    }

    // Returns true if there is an augmenting
    // path beginning with free vertex u
    boolean dfs(int u)
    {
        if (u != NIL)
        {
            for(int i : adj[u])
            {

                // Adjacent to u
                int v = i;

                // Follow the distances set by BFS
                if (dist[pairV[v]] == dist[u] + 1)
                {

                    // If dfs for pair of v also returns
                    // true
                    if (dfs(pairV[v]) == true)
                    {
                        pairV[v] = u;
                        pairU[u] = v;
                        return true;
                    }
                }
            }

            // If there is no augmenting path
            // beginning with u.
            dist[u] = INF;
            return false;
        }
        return true;
    }

    // Constructor
    @SuppressWarnings("unchecked")
    public BipGraph(int m, int n)
    {
        this.m = m;
        this.n = n;
        adj = new ArrayList[m + 1];
        Arrays.fill(adj, new ArrayList<>());
    }

    // To add edge from u to v and v to u
    void addEdge(int u, int v)
    {

        // Add u to v’s list.
        adj[u].add(v);
    }
}

// Driver code
public static void main(String[] args)
{

    BipGraph g = new BipGraph(4, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 1);
    g.addEdge(3, 2);
    g.addEdge(4, 2);
    g.addEdge(4, 4);

    System.out.println("Size of maximum matching is " +
                       g.hopcroftKarp());
}
}

// This code is contributed by sanjeev2552
```

**输出:**

```
Size of maximum matching is 4
```

以上实现主要采用了 [Hopcroft Karp 算法](https://en.wikipedia.org/wiki/Hopcroft%E2%80%93Karp_algorithm)Wiki 页面上提供的算法。
本文由**拉胡尔·古普塔**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息