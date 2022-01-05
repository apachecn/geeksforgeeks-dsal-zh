# 在朋友图中形成的群组数量

> 原文:[https://www . geesforgeks . org/number-group-formed-graph-friends/](https://www.geeksforgeeks.org/number-groups-formed-graph-friends/)

给定 n 个朋友和他们的友谊关系，找出存在的团体总数。以及由每个现有团体的成员组成的新团体的方式数量。
如果没有给任何人任何关系，那么这个人就没有群体，并且单独形成一个群体。如果 a 是 b 的朋友，b 是 c 的朋友，那么 a b 和 c 组成一个小组。

**示例:**

```
Input : Number of people = 6 
        Relations : 1 - 2, 3 - 4 
                    and 5 - 6 
Output: Number of existing Groups = 3
        Number of new groups that can
        be formed = 8
Explanation: The existing groups are 
(1, 2), (3, 4), (5, 6). The new 8 groups 
that can be formed by considering a 
member of every group are (1, 3, 5), 
(1, 3, 6), (1, 4, 5), (1, 4, 6), (2, 
3, 5), (2, 3, 6), (2, 4, 5) and (2, 4,
6). 

Input:  Number of people = 4 
        Relations : 1 - 2 and 2 - 3 
Output: Number of existing Groups = 2
        Number of new groups that can
        be formed = 3
Explanation: The existing groups are 
(1, 2, 3) and (4). The new groups that 
can be formed by considering a member
of every group are (1, 4), (2, 4), (3, 4).
```

要计算组的数量，我们需要简单地计算给定无向图中的[个连通分量。使用](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/) [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 或 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 可以轻松计数连接的组件。由于这是一个无向图，深度优先搜索从每个朋友的未访问顶点开始的次数等于形成的组数。

计算我们组成新团体的方法的数量可以简单地用公式来完成，公式是(N1)*(N2)*…。(Nn)其中，Ni 为第 I 组人数。

## C++

```
// C++ program to count number of existing
// groups and number of new groups that can
// be formed.
#include <bits/stdc++.h>
using namespace std;

class Graph {
    int V; // No. of vertices

    // Pointer to an array containing
    // adjacency lists
    list<int>* adj;

    int countUtil(int v, bool visited[]);
public:
    Graph(int V); // Constructor

    // function to add an edge to graph
    void addRelation(int v, int w);
    void countGroups();
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

// Adds a relation as a two way edge of
// undirected graph.
void Graph::addRelation(int v, int w)
{
    // Since indexing is 0 based, reducing
    // edge numbers by 1.
    v--;
    w--;
    adj[v].push_back(w);
    adj[w].push_back(v);
}

// Returns count of not visited nodes reachable
// from v using DFS.
int Graph::countUtil(int v, bool visited[])
{
    int count = 1;
    visited[v] = true;
    for (auto i=adj[v].begin(); i!=adj[v].end(); ++i)
        if (!visited[*i])
            count = count + countUtil(*i, visited);
    return count;       
}

// A DFS based function to Count number of
// existing groups and number of new groups
// that can be formed using a member of
// every group.
void Graph::countGroups()
{
    // Mark all the vertices as not visited
    bool* visited = new bool[V];
    memset(visited, 0, V*sizeof(int));

    int existing_groups = 0, new_groups = 1;
    for (int i = 0; i < V; i++)
    {
        // If not in any group.
        if (visited[i] == false)
        {
            existing_groups++;

            // Number of new groups that
            // can be formed.
            new_groups = new_groups *
                     countUtil(i, visited);
        }
    }

    if (existing_groups == 1)
        new_groups = 0;

    cout << "No. of existing groups are "
         << existing_groups << endl;
    cout << "No. of new groups that can be"
            " formed are " << new_groups
         << endl;
}

// Driver code
int main()
{
    int n = 6;

    // Create a graph given in the above diagram
    Graph g(n); // total 6 people
    g.addRelation(1, 2); // 1 and 2 are friends
    g.addRelation(3, 4); // 3 and 4 are friends
    g.addRelation(5, 6); // 5 and 6 are friends

    g.countGroups();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// existing groups and number of
// new groups that can be formed.
import java.util.*;
import java.io.*;

class Graph{

// No. of vertices
private int V;

// Array  of lists for Adjacency
// List Representation
private LinkedList<Integer> adj[];

// Constructor
@SuppressWarnings("unchecked") Graph(int v)
{
    V = v;
    adj = new LinkedList[V];

    for(int i = 0; i < V; i++)
    {
        adj[i] = new LinkedList();
    }
}

// Adds a relation as a two way edge of
// undirected graph.
public void addRelation(int v, int w)
{

    // Since indexing is 0 based, reducing
    // edge numbers by 1.
    v--;
    w--;
    adj[v].add(w);
    adj[w].add(v);
}

// Returns count of not visited nodes
// reachable from v using DFS.
int countUtil(int v, boolean visited[])
{
    int count = 1;
    visited[v] = true;

    // Recur for all the vertices adjacent
    // to this vertex
    Iterator<Integer> i = adj[v].listIterator();
    while (i.hasNext())
    {
        int n = i.next();
        if (!visited[n])
            count = count + countUtil(n, visited);
    }
    return count;
}

// A DFS based function to Count number of
// existing groups and number of new groups
// that can be formed using a member of
// every group.
void countGroups()
{

    // Mark all the vertices as not
    // visited(set as false by default
    // in java)
    boolean visited[] = new boolean[V];
    int existing_groups = 0, new_groups = 1;

    for(int i = 0; i < V; i++)
    {

        // If not in any group.
        if (visited[i] == false)
        {
            existing_groups++;

            // Number of new groups that
            // can be formed.
            new_groups = new_groups *
                         countUtil(i, visited);
        }
    }

    if (existing_groups == 1)
        new_groups = 0;

    System.out.println("No. of existing groups are " +
                       existing_groups);
    System.out.println("No. of new groups that " +
                       "can be formed are " +
                       new_groups);
}

// Driver code
public static void main(String[] args)
{
    int n = 6;

    // Create a graph given in
    // the above diagram
    Graph g = new Graph(n); // total 6 people
    g.addRelation(1, 2); // 1 and 2 are friends
    g.addRelation(3, 4); // 3 and 4 are friends
    g.addRelation(5, 6); // 5 and 6 are friends

    g.countGroups();
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 program to count number of
# existing groups and number of new
# groups that can be formed.
class Graph:
    def __init__(self, V):
        self.V = V
        self.adj = [[] for i in range(V)]

    # Adds a relation as a two way
    # edge of undirected graph.
    def addRelation(self, v, w):

        # Since indexing is 0 based,
        # reducing edge numbers by 1.
        v -= 1
        w -= 1
        self.adj[v].append(w)
        self.adj[w].append(v)

    # Returns count of not visited
    # nodes reachable from v using DFS.
    def countUtil(self, v, visited):
        count = 1
        visited[v] = True
        i = 0
        while i != len(self.adj[v]):
            if (not visited[self.adj[v][i]]):
                count = count + self.countUtil(self.adj[v][i],
                                                      visited)
            i += 1
        return count

    # A DFS based function to Count number
    # of existing groups and number of new
    # groups that can be formed using a
    # member of every group.
    def countGroups(self):

        # Mark all the vertices as
        # not visited
        visited = [0] * self.V

        existing_groups = 0
        new_groups = 1
        for i in range(self.V):

            # If not in any group.
            if (visited[i] == False):
                existing_groups += 1

                # Number of new groups that
                # can be formed.
                new_groups = (new_groups *
                              self.countUtil(i, visited))

        if (existing_groups == 1):
            new_groups = 0

        print("No. of existing groups are",
                           existing_groups)
        print("No. of new groups that",
              "can be formed are", new_groups)

# Driver code
if __name__ == '__main__':

    n = 6

    # Create a graph given in the above diagram
    g = Graph(n) # total 6 people
    g.addRelation(1, 2) # 1 and 2 are friends
    g.addRelation(3, 4) # 3 and 4 are friends
    g.addRelation(5, 6) # 5 and 6 are friends

    g.countGroups()

# This code is contributed by PranchalK
```

**输出:**

```
No. of existing groups are 3
No. of new groups that can be formed are 8
```

**时间复杂度** : O(N + R)，其中 N 为人数，R 为关系数。

本文由 [**Raj**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。