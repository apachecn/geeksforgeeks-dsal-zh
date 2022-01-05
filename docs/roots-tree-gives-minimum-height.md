# 给予最小高度的树根

> 原文:[https://www . geesforgeks . org/root-tree-given-mini-height/](https://www.geeksforgeeks.org/roots-tree-gives-minimum-height/)

给定一个无向图，它具有树的特征。可以选择任何节点作为根，任务是只找到那些最小化树高的节点。

**例:**
下图中所有节点都被一一做成根，我们可以看到当 3 和 4 都是根的时候，树的高度是最小的(2)所以{3，4}就是我们的答案。

![](img/a4fa1c478421fb2877dd07f35a19fd84.png)

我们可以通过首先考虑一维解来解决这个问题，即如果给定最长的图，那么如果总节点数为奇数，则高度最小的节点将是中间节点，或者如果总节点数为偶数，则为中间两个节点。这个解决方案可以通过以下方法实现——从路径的两端开始两个指针，每次移动一步，直到指针相遇或一步之外，在末端指针将在那些将最小化高度的节点上，因为我们已经均匀地划分了节点，所以高度将最小化。
同样的方法也可以应用于一般的树。从所有叶节点开始指针，每次向内移动一步，继续合并移动时重叠的指针，最后只有一个指针留在某个顶点上，或者两个指针留在一个距离之外。这些节点代表顶点的根，这将最小化树的高度。
所以我们可以只有一个根，或者最多有两个根，最小高度取决于树的结构，如上所述。对于实现，我们将不使用实际的指针，而是遵循类似 BFS 的方法，在开始时，所有的叶节点被推入队列，然后它们从树中被移除，下一个新的叶节点被推入队列，这个过程继续进行，直到我们的树中只有 1 或 2 个节点，这代表了结果。

## C++

```
//  C++ program to find root which gives minimum height to tree
#include <bits/stdc++.h>
using namespace std;

// This class represents a undirected graph using adjacency list
// representation
class Graph
{
public:
    int V; // No. of vertices

    // Pointer to an array containing adjacency lists
    list<int> *adj;

    // Vector which stores degree of all vertices
    vector<int> degree;

    Graph(int V);            // Constructor
    void addEdge(int v, int w);   // To add an edge

    // function to get roots which give minimum height
    vector<int> rootForMinimumHeight();
};

// Constructor of graph, initializes adjacency list and
// degree vector
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
    for (int i = 0; i < V; i++)
        degree.push_back(0);
}

// addEdge method adds vertex to adjacency list and increases
// degree by 1
void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);    // Add w to v’s list
    adj[w].push_back(v);    // Add v to w’s list
    degree[v]++;            // increment degree of v by 1
    degree[w]++;            // increment degree of w by 1
}

//  Method to return roots which gives minimum height to tree
vector<int> Graph::rootForMinimumHeight()
{
    queue<int> q;

    //  first enqueue all leaf nodes in queue
    for (int i = 0; i < V; i++)
        if (degree[i] == 1)
            q.push(i);

    //  loop until total vertex remains less than 2
    while (V > 2)
    {
        int popEle = q.size();
        V -= popEle;      // popEle number of vertices will be popped

        for (int i = 0; i < popEle; i++)
        {
            int t = q.front();
            q.pop();

            // for each neighbour, decrease its degree and
            // if it become leaf, insert into queue
            for (auto j = adj[t].begin(); j != adj[t].end(); j++)
            {
                degree[*j]--;
                if (degree[*j] == 1)
                    q.push(*j);
            }
        }
    }

    //  copying the result from queue to result vector
    vector<int> res;
    while (!q.empty())
    {
        res.push_back(q.front());
        q.pop();
    }
    return res;
}

//  Driver code
int main()
{
    Graph g(6);
    g.addEdge(0, 3);
    g.addEdge(1, 3);
    g.addEdge(2, 3);
    g.addEdge(4, 3);
    g.addEdge(5, 4);

      // Function Call
    vector<int> res = g.rootForMinimumHeight();
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
    cout << endl;
}
```

## 计算机编程语言

```
# Python program to find root which gives minimum
# height to tree

# This class represents a undirected graph using
# adjacency list representation

class Graph:

    # Constructor of graph, initialize adjacency list
    # and degree vector
    def __init__(self, V, addEdge, rootForMinimumHeight):
        self.V = V
        self.adj = dict((i, []) for i in range(V))
        self.degree = list()
        for i in range(V):
            self.degree.append(0)

        # The below lines allows us define methods outside
        # of class definition
        # Check http://bit.ly/2e5HfrW for better explanation
        Graph.addEdge = addEdge
        Graph.rootForMinimumHeight = rootForMinimumHeight

# addEdge method adds vertex to adjacency list and
# increases degree by 1
def addEdge(self, v, w):
    self.adj[v].append(w)  # Adds w to v's list
    self.adj[w].append(v)  # Adds v to w's list
    self.degree[v] += 1      # increment degree of v by 1
    self.degree[w] += 1      # increment degree of w by 1

# Method to return roots which gives minimum height to tree
def rootForMinimumHeight(self):

    from Queue import Queue
    q = Queue()

    # First enqueue all leaf nodes in queue
    for i in range(self.V):
        if self.degree[i] == 1:
            q.put(i)

    # loop until total vertex remains less than 2
    while(self.V > 2):
        p = q.qsize()
        self.V -= p
        for i in range(p):
            t = q.get()

            # for each neighbour, decrease its degree and
            # if it become leaf, insert into queue
            for j in self.adj[t]:
                self.degree[j] -= 1
                if self.degree[j] == 1:
                    q.put(j)

    #  Copying the result from queue to result vector
    res = list()
    while(q.qsize() > 0):
        res.append(q.get())

    return res

# Driver code
g = Graph(6, addEdge, rootForMinimumHeight)
g.addEdge(0, 3)
g.addEdge(1, 3)
g.addEdge(2, 3)
g.addEdge(4, 3)
g.addEdge(5, 4)

# Function call
res = g.rootForMinimumHeight()
for i in res:
    print i,

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**Output**

```
3 4 
```

由于我们访问每个节点一次，解决方案的总**时间复杂度**为 O(n)。

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。