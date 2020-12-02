# 在好友图表中形成的群组数量

> 原文： [https://www.geeksforgeeks.org/number-groups-formed-graph-friends/](https://www.geeksforgeeks.org/number-groups-formed-graph-friends/)

给定 n 个朋友和他们的友谊关系，找到存在的小组总数。 以及可以由每个现有组中的人组成的新组的方式数量。
如果未与任何人建立任何关系，则该人没有任何组，而是单独组成一个组。 如果 a 是 b 的朋友，b 是 c 的朋友，则 b 和 c 组成一个组。

**示例**：

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

Input:  Number of people = 6 
        Relations : 1 - 2 and 2 - 3 
Output: Number of existing Groups = 2
        Number of new groups that can
        be formed = 3
Explanation: The existing groups are 
(1, 2, 3) and (4). The new groups that 
can be formed by considering a member
of every group are (1, 4), (2, 4), (3, 4).

```

要计算组数，我们只需要计算给定无向图中的[个连接的组件。 使用](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/) [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 或 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 可以很容易地计算连接的组件。 由于这是无向图，因此对于每个朋友，从深度不限的顶点开始的深度优先搜索的次数等于形成的组数。

用简单的公式（N1）*（N2）* ....（Nn）来计算我们形成新群体的方式数量，其中 Ni 是第 i 个群体中的人数。

## C++

```cpp

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

## Java

```java

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

## Python3

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
        # reducing edge numbers by 1\. 
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

**输出**：

```
No. of existing groups are 3
No. of new groups that can be formed are 8

```

**时间复杂度**：O（N + R），其中 N 是人数，R 是关系数。

本文由 [**Raj**](https://www.facebook.com/raja.vikramaditya.7) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

