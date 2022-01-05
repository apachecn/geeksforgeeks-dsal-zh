# 图中第 k 个最重的相邻节点，其中每个顶点都有权重

> 原文:[https://www . geesforgeks . org/kth-相邻节点-图-顶点-权重/](https://www.geeksforgeeks.org/kth-adjacent-node-graph-vertex-weight/)

给定一个正数 **k** 和一个从 0 到 N-1 的 **N** 节点的无向图，每个节点都有一个与之相关的权重。请注意，这不同于每个边都有权重的普通加权图。
对于每个节点，如果我们按照降序排列与其直接相连的节点(根据它们的权重)，那么在 **kth** 位置的节点数是多少。打印每个节点的第 k 个节点号(不是重量)，如果不存在，打印-1。
**示例:**

```
Input : N = 3, k = 2, wt[] = { 2, 4, 3 }.
edge 1: 0 2
edge 2: 0 1
edge 3: 1 2

Output : 2 0 0
Graph:
         0 (weight 2)
        / \
       /   \
      1-----2
(weight 4)  (weight 3)
For node 0, sorted (decreasing order) nodes
according to their weights are node 1(weight 4),
node 2(weight 3). The node at 2nd position for
node 0 is node 2.
For node 1, sorted (decreasing order) nodes 
according to their weight are node 2(weight 3), 
node 0(weight 2). The node at 2nd position for 
node 1 is node 0.
For node 2, sorted (decreasing order) nodes 
according to their weight are node 1(weight 4),
node 0(weight 2). The node at 2nd position for
node 2 is node 0.
```

其思想是根据相邻节点的权重对每个节点的邻接表进行排序。
首先，为所有节点创建邻接表。现在，对于每个节点，与其直接相连的所有节点都存储在一个列表中。在邻接表中，存储节点及其权重。
现在，对于每个节点，将与其直接相连的所有节点的权重进行逆序排序，然后打印出每个节点列表中第 k 个位置的节点号。
以下是本办法的实施情况:

## C++

```
// C++ program to find Kth node weight after s
// sorting of nodes directly connected to a node.
#include<bits/stdc++.h>
using namespace std;

// Print Kth node number for each node after sorting
// connected node according to their weight.
void printkthnode(vector< pair<int, int> > adj[],
                        int wt[], int n, int k)
{
    // Sort Adjacency List of all node on the basis
    // of its weight.
    for (int i = 0; i < n; i++)
      sort(adj[i].begin(), adj[i].end());

    // Printing Kth node for each node.
    for (int i = 0; i < n; i++)
    {
        if (adj[i].size() >= k)
          cout << adj[i][adj[i].size() - k].second;
        else
          cout << "-1";
    }
}

// Driven Program
int main()
{
    int n = 3, k = 2;
    int wt[] = { 2, 4, 3 };

    // Making adjacency list, storing the nodes
    // along with their weight.
    vector< pair<int, int> > adj[n+1];

    adj[0].push_back(make_pair(wt[2], 2));
    adj[2].push_back(make_pair(wt[0], 0));

    adj[0].push_back(make_pair(wt[1], 1));
    adj[1].push_back(make_pair(wt[0], 0));

    adj[1].push_back(make_pair(wt[2], 2));
    adj[2].push_back(make_pair(wt[1], 1));

    printkthnode(adj, wt, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Kth node weight after s
// sorting of nodes directly connected to a node.
import java.util.*;

class GFG
{
    // pair class
    static class pair
    {
        int first, second;

        pair(int a, int b)
        {
            first = a;
            second = b;
        }
    }

    // Print Kth node number for each node after sorting
    // connected node according to their weight.
    static void printkthnode(Vector<pair> adj[], int wt[], int n, int k)
    {
        // Sort Adjacency List of all node on the basis
        // of its weight.
        for (int i = 0; i < n; i++)
            Collections.sort(adj[i], new Comparator<pair>()
            {
                public int compare(pair p1, pair p2)
                {
                    return p1.first - p2.first;
                }
            });

        // Printing Kth node for each node.
        for (int i = 0; i < n; i++)
        {
            if (adj[i].size() >= k)
                System.out.print(adj[i].get(adj[i].size() -
                                            k).second + " ");
            else
                System.out.print("-1");
        }
    }

    // Driven Program
    public static void main(String[] args)
    {
        int n = 3, k = 2;
        int wt[] = { 2, 4, 3 };

        // Making adjacency list, storing the nodes
        // along with their weight.
        Vector<pair>[] adj = new Vector[n + 1];
        for (int i = 0; i < n + 1; i++)
            adj[i] = new Vector<pair>();

        adj[0].add(new pair(wt[2], 2));
        adj[2].add(new pair(wt[0], 0));

        adj[0].add(new pair(wt[1], 1));
        adj[1].add(new pair(wt[0], 0));

        adj[1].add(new pair(wt[2], 2));
        adj[2].add(new pair(wt[1], 1));

        printkthnode(adj, wt, n, k);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find Kth node
# weight after sorting of nodes
# directly connected to a node.

# PrKth node number for each node
# after sorting connected node
# according to their weight.
def printkthnode(adj, wt, n, k):

    # Sort Adjacency List of all
    # node on the basis of its weight.
    for i in range(n):
        adj[i].sort()

    # Printing Kth node for each node.
    for i in range(n):
        if (len(adj[i]) >= k):
            print(adj[i][len(adj[i]) -
                             k][1], end = " ")
        else:
            print("-1", end = " ")

# Driver Code
if __name__ == '__main__':

    n = 3
    k = 2
    wt = [2, 4, 3]

    # Making adjacency list, storing
    # the nodes along with their weight.
    adj = [[] for i in range(n + 1)]

    adj[0].append([wt[2], 2])
    adj[2].append([wt[0], 0])

    adj[0].append([wt[1], 1])
    adj[1].append([wt[0], 0])

    adj[1].append([wt[2], 2])
    adj[2].append([wt[1], 1])

    printkthnode(adj, wt, n, k)

# This code is contributed by PranchalK
```

**输出:**

```
2 0 0
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。