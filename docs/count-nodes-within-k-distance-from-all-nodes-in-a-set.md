# 统计集合中所有节点的 K 距离内的节点

> 原文:[https://www . geesforgeks . org/count-nodes-in-k-distance-of-all-nodes-in-a-set/](https://www.geeksforgeeks.org/count-nodes-within-k-distance-from-all-nodes-in-a-set/)

给定一个有一些标记节点和一个正数 K 的无向树。我们需要打印所有这些节点的计数，这些节点与所有标记节点的距离小于 K，这意味着每个节点与所有标记节点的距离小于 K，应该在结果中计数。
**例:**

![](img/869b2c19f6bb0d69b1f321331e29212d.png)

```
In above tree we can see that node with index 
0, 2, 3, 5, 6, 7 have distances less than 3
from all the marked nodes.
so answer will be 6

```

我们可以使用广度优先搜索来解决这个问题。在这个问题中要观察的主要事情是，如果我们找到两个彼此距离最大的标记节点，考虑到所有标记节点对，那么如果一个节点与这两个节点的距离都小于 K，那么它与所有标记节点的距离将小于 K，因为这两个节点代表所有标记节点的极限，如果一个节点位于这个极限，那么它与所有标记节点的距离将小于 K，否则不是。
如上例，节点-1 和节点-4 是距离标记最远的节点，因此距离这两个节点小于 3 的节点也将距离节点 2 小于 3。现在我们可以从任意一个随机节点得到第一个远距离标记节点，我们可以从第一个标记节点得到另一个 bfs，在这个 bfs 中，我们还可以找到所有节点到第一个远距离标记节点的距离，为了找到所有节点到第二个远距离标记节点的距离，我们将再做一个 bfs， 因此在做了这三个 bfs 之后，我们可以从两个极端的标记节点获得所有节点的距离，可以将这两个节点与 K 进行比较，以知道哪些节点落在所有标记节点的 K 距离范围内。

## C++

```
//  C++ program to count nodes inside K distance
// range from marked nodes
#include <bits/stdc++.h>
using namespace std;

// Utility bfs method to fill distance vector and returns
// most distant marked node from node u
int bfsWithDistance(vector<int> g[], bool mark[], int u,
                                        vector<int>& dis)
{
    int lastMarked;
    queue<int> q;

    //  push node u in queue and initialize its distance as 0
    q.push(u);
    dis[u] = 0;

    //  loop untill all nodes are processed
    while (!q.empty())
    {
        u = q.front();      q.pop();
        //  if node is marked, update lastMarked variable
        if (mark[u])
            lastMarked = u;

        // loop over all neighbors of u and update their
        // distance before pushing in queue
        for (int i = 0; i < g[u].size(); i++)
        {
            int v = g[u][i];

            //  if not given value already
            if (dis[v] == -1)
            {
                dis[v] = dis[u] + 1;
                q.push(v);
            }
        }
    }
    //  return last updated marked value
    return lastMarked;
}

// method returns count of nodes which are in K-distance
// range from marked nodes
int nodesKDistanceFromMarked(int edges[][2], int V,
                             int marked[], int N, int K)
{
    //  vertices in a tree are one more than number of edges
    V = V + 1;
    vector<int> g[V];

    //  fill vector for graph
    int u, v;   
    for (int i = 0; i < (V - 1); i++)
    {
        u = edges[i][0];
        v = edges[i][1];

        g[u].push_back(v);
        g[v].push_back(u);
    }

    //  fill boolean array mark from marked array
    bool mark[V] = {false};
    for (int i = 0; i < N; i++)
        mark[marked[i]] = true;

    //  vectors to store distances
    vector<int> tmp(V, -1), dl(V, -1), dr(V, -1);

    //  first bfs(from any random node) to get one
    // distant marked node
    u = bfsWithDistance(g, mark, 0, tmp);

    /*  second bfs to get other distant marked node
        and also dl is filled with distances from first
        chosen marked node */
    v = bfsWithDistance(g, mark, u, dl);

    //  third bfs to fill dr by distances from second
    // chosen marked node
    bfsWithDistance(g, mark, v, dr);

    int res = 0;
    //  loop over all nodes
    for (int i = 0; i < V; i++)
    {
        // increase res by 1, if current node has distance
        // less than K from both extreme nodes
        if (dl[i] <= K && dr[i] <= K)
            res++;
    }
    return res;
}

// Driver code to test above methods
int main()
{
    int edges[][2] =
    {
        {1, 0}, {0, 3}, {0, 8}, {2, 3},
        {3, 5}, {3, 6}, {3, 7}, {4, 5},
        {5, 9}
    };
    int V = sizeof(edges) / sizeof(edges[0]);

    int marked[] = {1, 2, 4};
    int N = sizeof(marked) / sizeof(marked[0]);

    int K = 3;
    cout << nodesKDistanceFromMarked(edges, V, marked, N, K);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to count nodes inside
# K distance range from marked nodes
import queue

# Utility bfs method to fill distance
# vector and returns most distant
# marked node from node u
def bfsWithDistance(g, mark, u, dis):
    lastMarked = 0
    q = queue.Queue()

    # push node u in queue and initialize
    # its distance as 0
    q.put(u)
    dis[u] = 0

    # loop untill all nodes are processed
    while (not q.empty()):
        u = q.get()

        # if node is marked, update
        # lastMarked variable
        if (mark[u]):
            lastMarked = u

        # loop over all neighbors of u and
        # update their distance before
        # pushing in queue
        for i in range(len(g[u])):
            v = g[u][i]

            # if not given value already
            if (dis[v] == -1):
                dis[v] = dis[u] + 1
                q.put(v)

    # return last updated marked value
    return lastMarked

# method returns count of nodes which
# are in K-distance range from marked nodes
def nodesKDistanceFromMarked(edges, V, marked, N, K):

    # vertices in a tree are one
    # more than number of edges
    V = V + 1
    g = [[] for i in range(V)]

    # fill vector for graph
    u, v = 0, 0
    for i in range(V - 1):
        u = edges[i][0]
        v = edges[i][1]

        g[u].append(v)
        g[v].append(u)

    # fill boolean array mark from
    # marked array
    mark = [False] * V
    for i in range(N):
        mark[marked[i]] = True

    # vectors to store distances
    tmp = [-1] * V
    dl = [-1] * V
    dr = [-1] * V

    # first bfs(from any random node)
    # to get one distant marked node
    u = bfsWithDistance(g, mark, 0, tmp)

    # second bfs to get other distant
    # marked node and also dl is filled
    # with distances from first chosen
    # marked node
    u = bfsWithDistance(g, mark, u, dl)

    # third bfs to fill dr by distances
    # from second chosen marked node
    bfsWithDistance(g, mark, u, dr)

    res = 0

    # loop over all nodes
    for i in range(V):

        # increase res by 1, if current node
        # has distance less than K from both
        # extreme nodes
        if (dl[i] <= K and dr[i] <= K):
            res += 1
    return res

# Driver Code
if __name__ == '__main__':

    edges = [[1, 0], [0, 3], [0, 8],
             [2, 3], [3, 5], [3, 6],
             [3, 7], [4, 5], [5, 9]]
    V = len(edges)

    marked = [1, 2, 4]
    N = len(marked)

    K = 3
    print(nodesKDistanceFromMarked(edges, V,
                                   marked, N, K))

# This code is contributed by PranchalK
```

**输出:**

```
6

```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。