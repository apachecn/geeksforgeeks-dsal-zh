# 计算距集合

中所有节点 K 距离内的节点

> 原文： [https://www.geeksforgeeks.org/count-nodes-within-k-distance-from-all-nodes-in-a-set/](https://www.geeksforgeeks.org/count-nodes-within-k-distance-from-all-nodes-in-a-set/)

给定一个带有一些标记节点且正数为 K 的无向树，我们需要打印与所有标记节点之间的距离小于 K 的所有此类节点的计数，这意味着与所有标记节点之间的距离小于 K 的每个节点都应 被计入结果。
**示例：** [

![](img/869b2c19f6bb0d69b1f321331e29212d.png)

```
In above tree we can see that node with index 
0, 2, 3, 5, 6, 7 have distances less than 3
from all the marked nodes.
so answer will be 6

```

我们可以使用广度优先搜索解决此问题。 在这个问题中要观察的主要事情是，如果考虑所有成对的标记节点，找到两个彼此之间最大距离的标记节点，则如果一个节点与这两个节点的距离都小于 K，则它将是 与所有标记节点之间的距离小于 K，因为这两个节点代表所有标记节点的极限，如果一个节点位于此极限内，则它与所有标记节点之间的距离将小于 K。
如上面的示例，节点 1 和节点 4 是最远的标记节点，因此距这两个节点的距离小于 3 的节点也距节点 2 的距离也小于 3。 现在我们可以通过对任意随机节点进行 bfs 来获得第一个远距离标记节点，对第二个远距离标记节点可以通过对刚从第一个 bfs 中找到的标记节点进行另一个 bfs 来获得，在这个 bfs 中我们还可以找到所有节点的距离 从第一个远距离标记节点开始，并找到所有节点与第二个远距离标记节点的距离，我们将再做一次 bfs，因此在完成这三个 bfs 之后，我们可以获得从两个极端标记节点到所有节点的距离，可以与 K 进行比较以了解 哪些节点在所有标记节点的 K 距离范围内。

## C ++

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

## Python3

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

**输出：**

```
6

```

本文由 [**Utkarsh Trivedi**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

