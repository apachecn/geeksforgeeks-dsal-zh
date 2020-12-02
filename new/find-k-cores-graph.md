# 查找无向图

的 k 核

> 原文： [https://www.geeksforgeeks.org/find-k-cores-graph/](https://www.geeksforgeeks.org/find-k-cores-graph/)

给定一个图 G 和一个整数 K，该图的 K 核是在小于 k 的所有度数顶点都被删除之后剩下的连接组件（来源 [Wiki](https://en.wikipedia.org/wiki/Degeneracy_%28graph_theory%29) ）

**示例**：

```
Input : Adjacency list representation of graph shown
        on left side of below diagram
Output: K-Cores : 
[2] -> 3 -> 4 -> 6
[3] -> 2 -> 4 -> 6 -> 7
[4] -> 2 -> 3 -> 6 -> 7
[6] -> 2 -> 3 -> 4 -> 7
[7] -> 3 -> 4 -> 6

```

![kcore](img/51df7bd05904ddd9ebbb4b03e8d2a10e.png)

**我们强烈建议您最小化浏览器，然后自己尝试。**
查找 k 核心图的标准算法是从输入图中删除度小于-“ K”的所有顶点。 我们必须小心，移除一个顶点会降低与其相邻的所有顶点的度数，因此相邻顶点的度数也可能会降到“ K”以下。 因此，我们可能也必须删除这些顶点。 直到/在图中没有任何顶点之前，此过程可能/可能不会进行。

为了实现上述算法，我们对输入图进行了修改后的 DFS，并删除了度数小于“ K”的所有顶点，然后更新了所有相邻顶点的度数，如果它们的度数低于“ K”，我们也将其删除。 。

以下是上述想法的实现。 请注意，以下程序仅打印 k 个核的顶点，但由于我们修改了邻接表，因此可以轻松扩展以打印完整的 k 个核。

## C++

```cpp

// C++ program to find K-Cores of a graph 
#include<bits/stdc++.h> 
using namespace std; 

// This class represents a undirected graph using adjacency 
// list representation 
class Graph 
{ 
    int V; // No. of vertices 

    // Pointer to an array containing adjacency lists 
    list<int> *adj; 
public: 
    Graph(int V); // Constructor 

    // function to add an edge to graph 
    void addEdge(int u, int v); 

    // A recursive function to print DFS starting from v 
    bool DFSUtil(int, vector<bool> &, vector<int> &, int k); 

    // prints k-Cores of given graph 
    void printKCores(int k); 
}; 

// A recursive function to print DFS starting from v. 
// It returns true if degree of v after processing is less 
// than k else false 
// It also updates degree of adjacent if degree of v 
// is less than k. And if degree of a processed adjacent 
// becomes less than k, then it reduces of degree of v also, 
bool Graph::DFSUtil(int v, vector<bool> &visited, 
                    vector<int> &vDegree, int k) 
{ 
    // Mark the current node as visited and print it 
    visited[v] = true; 

    // Recur for all the vertices adjacent to this vertex 
    list<int>::iterator i; 
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
    { 
        // degree of v is less than k, then degree of adjacent 
        // must be reduced 
        if (vDegree[v] < k) 
            vDegree[*i]--; 

        // If adjacent is not processed, process it 
        if (!visited[*i]) 
        { 
            // If degree of adjacent after processing becomes 
            // less than k, then reduce degree of v also. 
            if (DFSUtil(*i, visited, vDegree, k)) 
                vDegree[v]--; 
        } 
    } 

    // Return true if degree of v is less than k 
    return (vDegree[v] < k); 
} 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int u, int v) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// Prints k cores of an undirected graph 
void Graph::printKCores(int k) 
{ 
    // INITIALIZATION 
    // Mark all the vertices as not visited and not 
    // processed. 
    vector<bool> visited(V, false); 
    vector<bool> processed(V, false); 

    int mindeg = INT_MAX; 
    int startvertex; 

    // Store degrees of all vertices 
    vector<int> vDegree(V); 
    for (int i=0; i<V; i++) 
    { 
        vDegree[i] = adj[i].size(); 

        if (vDegree[i] < mindeg) 
        { 
            mindeg = vDegree[i]; 
            startvertex=i; 
        } 
    } 

    DFSUtil(startvertex, visited, vDegree, k); 

    // DFS traversal to update degrees of all 
    // vertices. 
    for (int i=0; i<V; i++) 
        if (visited[i] == false) 
            DFSUtil(i, visited, vDegree, k); 

    // PRINTING K CORES 
    cout << "K-Cores : \n"; 
    for (int v=0; v<V; v++) 
    { 
        // Only considering those vertices which have degree 
        // >= K after BFS 
        if (vDegree[v] >= k) 
        { 
            cout << "\n[" << v << "]"; 

            // Traverse adjacency list of v and print only 
            // those adjacent which have vDegree >= k after 
            // BFS. 
            list<int>::iterator itr; 
            for (itr = adj[v].begin(); itr != adj[v].end(); ++itr) 
                if (vDegree[*itr] >= k) 
                    cout << " -> " << *itr; 
        } 
    } 
} 

// Driver program to test methods of graph class 
int main() 
{ 
    // Create a graph given in the above diagram 
    int k = 3; 
    Graph g1(9); 
    g1.addEdge(0, 1); 
    g1.addEdge(0, 2); 
    g1.addEdge(1, 2); 
    g1.addEdge(1, 5); 
    g1.addEdge(2, 3); 
    g1.addEdge(2, 4); 
    g1.addEdge(2, 5); 
    g1.addEdge(2, 6); 
    g1.addEdge(3, 4); 
    g1.addEdge(3, 6); 
    g1.addEdge(3, 7); 
    g1.addEdge(4, 6); 
    g1.addEdge(4, 7); 
    g1.addEdge(5, 6); 
    g1.addEdge(5, 8); 
    g1.addEdge(6, 7); 
    g1.addEdge(6, 8); 
    g1.printKCores(k); 

    cout << endl << endl; 

    Graph g2(13); 
    g2.addEdge(0, 1); 
    g2.addEdge(0, 2); 
    g2.addEdge(0, 3); 
    g2.addEdge(1, 4); 
    g2.addEdge(1, 5); 
    g2.addEdge(1, 6); 
    g2.addEdge(2, 7); 
    g2.addEdge(2, 8); 
    g2.addEdge(2, 9); 
    g2.addEdge(3, 10); 
    g2.addEdge(3, 11); 
    g2.addEdge(3, 12); 
    g2.printKCores(k); 

    return 0; 
} 

```

## Java

```java

// Java program to find K-Cores of a graph 
import java.util.*; 

class GFG 
{ 

    // This class represents a undirected graph using adjacency 
    // list representation 
    static class Graph 
    { 
        int V; // No. of vertices 

        // Pointer to an array containing adjacency lists 
        Vector<Integer>[] adj; 

        @SuppressWarnings("unchecked") 
        Graph(int V) 
        { 
            this.V = V; 
            this.adj = new Vector[V]; 

            for (int i = 0; i < V; i++) 
                adj[i] = new Vector<>(); 
        } 

        // function to add an edge to graph 
        void addEdge(int u, int v) 
        { 
            this.adj[u].add(v); 
            this.adj[v].add(u); 
        } 

        // A recursive function to print DFS starting from v. 
        // It returns true if degree of v after processing is less 
        // than k else false 
        // It also updates degree of adjacent if degree of v 
        // is less than k. And if degree of a processed adjacent 
        // becomes less than k, then it reduces of degree of v also, 
        boolean DFSUtil(int v, boolean[] visited, int[] vDegree, int k) 
        { 

            // Mark the current node as visited and print it 
            visited[v] = true; 

            // Recur for all the vertices adjacent to this vertex 
            for (int i : adj[v]) 
            { 

                // degree of v is less than k, then degree of adjacent 
                // must be reduced 
                if (vDegree[v] < k) 
                    vDegree[i]--; 

                // If adjacent is not processed, process it 
                if (!visited[i]) 
                { 

                    // If degree of adjacent after processing becomes 
                    // less than k, then reduce degree of v also. 
                    if (DFSUtil(i, visited, vDegree, k)) 
                        vDegree[v]--; 
                } 
            } 

            // Return true if degree of v is less than k 
            return (vDegree[v] < k); 
        } 

        // Prints k cores of an undirected graph 
        void printKCores(int k) 
        { 

            // INITIALIZATION 
            // Mark all the vertices as not visited and not 
            // processed. 
            boolean[] visited = new boolean[V]; 
            boolean[] processed = new boolean[V]; 
            Arrays.fill(visited, false); 
            Arrays.fill(processed, false); 

            int mindeg = Integer.MAX_VALUE; 
            int startvertex = 0; 

            // Store degrees of all vertices 
            int[] vDegree = new int[V]; 
            for (int i = 0; i < V; i++) 
            { 
                vDegree[i] = adj[i].size(); 

                if (vDegree[i] < mindeg) 
                { 
                    mindeg = vDegree[i]; 
                    startvertex = i; 
                } 
            } 
            DFSUtil(startvertex, visited, vDegree, k); 

            // DFS traversal to update degrees of all 
            // vertices. 
            for (int i = 0; i < V; i++) 
                if (!visited[i]) 
                    DFSUtil(i, visited, vDegree, k); 

            // PRINTING K CORES 
            System.out.println("K-Cores : "); 
            for (int v = 0; v < V; v++) 
            { 

                // Only considering those vertices which have degree 
                // >= K after BFS 
                if (vDegree[v] >= k) 
                { 
                    System.out.printf("\n[%d]", v); 

                    // Traverse adjacency list of v and print only 
                    // those adjacent which have vDegree >= k after 
                    // BFS. 
                    for (int i : adj[v]) 
                        if (vDegree[i] >= k) 
                            System.out.printf(" -> %d", i); 
                } 
            } 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 

        // Create a graph given in the above diagram 
        int k = 3; 
        Graph g1 = new Graph(9); 
        g1.addEdge(0, 1); 
        g1.addEdge(0, 2); 
        g1.addEdge(1, 2); 
        g1.addEdge(1, 5); 
        g1.addEdge(2, 3); 
        g1.addEdge(2, 4); 
        g1.addEdge(2, 5); 
        g1.addEdge(2, 6); 
        g1.addEdge(3, 4); 
        g1.addEdge(3, 6); 
        g1.addEdge(3, 7); 
        g1.addEdge(4, 6); 
        g1.addEdge(4, 7); 
        g1.addEdge(5, 6); 
        g1.addEdge(5, 8); 
        g1.addEdge(6, 7); 
        g1.addEdge(6, 8); 
        g1.printKCores(k); 

        System.out.println(); 

        Graph g2 = new Graph(13); 
        g2.addEdge(0, 1); 
        g2.addEdge(0, 2); 
        g2.addEdge(0, 3); 
        g2.addEdge(1, 4); 
        g2.addEdge(1, 5); 
        g2.addEdge(1, 6); 
        g2.addEdge(2, 7); 
        g2.addEdge(2, 8); 
        g2.addEdge(2, 9); 
        g2.addEdge(3, 10); 
        g2.addEdge(3, 11); 
        g2.addEdge(3, 12); 
        g2.printKCores(k); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python

```py

# Python program to find K-Cores of a graph 
from collections import defaultdict 

# This class represents a undirected graph using adjacency 
# list representation 
class Graph: 

    def __init__(self,vertices): 
        self.V= vertices #No. of vertices 

        # default dictionary to store graph 
        self.graph= defaultdict(list) 

    # function to add an edge to undirected graph 
    def addEdge(self,u,v): 
        self.graph[u].append(v) 
        self.graph[v].append(u) 

    # A recursive function to call DFS starting from v. 
    # It returns true if vDegree of v after processing is less 
    # than k else false 
    # It also updates vDegree of adjacent if vDegree of v 
    # is less than k. And if vDegree of a processed adjacent 
    # becomes less than k, then it reduces of vDegree of v also, 
    def DFSUtil(self,v,visited,vDegree,k): 

        # Mark the current node as visited 
        visited[v] = True

        # Recur for all the vertices adjacent to this vertex 
        for i in self.graph[v]: 

            # vDegree of v is less than k, then vDegree of 
            # adjacent must be reduced 
            if vDegree[v] < k: 
                vDegree[i] = vDegree[i] - 1

            # If adjacent is not processed, process it 
            if visited[i]==False: 

                # If vDegree of adjacent after processing becomes 
                # less than k, then reduce vDegree of v also 
                if (self.DFSUtil(i,visited,vDegree,k)): 
                    vDegree[v]-=1

        # Return true if vDegree of v is less than k 
        return vDegree[v] < k 

    # Prints k cores of an undirected graph 
    def printKCores(self,k): 

        # INITIALIZATION 
        # Mark all the vertices as not visited 
        visited = [False]*self.V 

        # Store vDegrees of all vertices 
        vDegree = [0]*self.V 
        for i in self.graph: 
                vDegree[i]=len(self.graph[i]) 

        # choose any vertex as starting vertex 
        self.DFSUtil(0,visited,vDegree,k) 

        # DFS traversal to update vDegrees of all 
        # vertices,in case they are unconnected 
        for i in range(self.V): 
            if visited[i] ==False: 
                self.DFSUtil(i,k,vDegree,visited) 

        # PRINTING K CORES 
        print "\n K-cores: "
        for v in range(self.V): 

            # Only considering those vertices which have 
            # vDegree >= K after DFS 
            if vDegree[v] >= k: 
                print str("\n [ ") + str(v) + str(" ]"), 

                # Traverse adjacency list of v and print only 
                # those adjacent which have vvDegree >= k 
                # after DFS 
                for i in self.graph[v]: 
                    if vDegree[i] >= k: 
                        print "-> " + str(i), 

k = 3; 
g1 = Graph (9); 
g1.addEdge(0, 1) 
g1.addEdge(0, 2) 
g1.addEdge(1, 2) 
g1.addEdge(1, 5) 
g1.addEdge(2, 3) 
g1.addEdge(2, 4) 
g1.addEdge(2, 5) 
g1.addEdge(2, 6) 
g1.addEdge(3, 4) 
g1.addEdge(3, 6) 
g1.addEdge(3, 7) 
g1.addEdge(4, 6) 
g1.addEdge(4, 7) 
g1.addEdge(5, 6) 
g1.addEdge(5, 8) 
g1.addEdge(6, 7) 
g1.addEdge(6, 8) 
g1.printKCores(k) 

g2 = Graph(13); 
g2.addEdge(0, 1) 
g2.addEdge(0, 2) 
g2.addEdge(0, 3) 
g2.addEdge(1, 4) 
g2.addEdge(1, 5) 
g2.addEdge(1, 6) 
g2.addEdge(2, 7) 
g2.addEdge(2, 8) 
g2.addEdge(2, 9) 
g2.addEdge(3, 10) 
g2.addEdge(3, 11) 
g2.addEdge(3, 12) 
g2.printKCores(k) 

# This code is contributed by Neelam Yadav 

```

## C#

```cs

// C# program to find K-Cores of a graph
using System;
using System.Collections.Generic;

class GFG{

// This class represents a undirected 
// graph using adjacency list 
// representation
public class Graph
{

    // No. of vertices
    int V; 

    // Pointer to an array containing 
    // adjacency lists
    List<int>[] adj;

    public Graph(int V) 
    {
        this.V = V;
        this.adj = new List<int>[V];

        for(int i = 0; i < V; i++)
            adj[i] = new List<int>();
    }

    // Function to add an edge to graph
    public void addEdge(int u, int v)
    {
        this.adj[u].Add(v);
        this.adj[v].Add(u);
    }

    // A recursive function to print DFS 
    // starting from v. It returns true
    // if degree of v after processing 
    // is less than k else false
    // It also updates degree of adjacent
    // if degree of v is less than k. And
    // if degree of a processed adjacent
    // becomes less than k, then it reduces
    // of degree of v also,
    bool DFSUtil(int v, bool[] visited, 
                 int[] vDegree, int k)
    {

        // Mark the current node as 
        // visited and print it
        visited[v] = true;

        // Recur for all the vertices 
        // adjacent to this vertex
        foreach (int i in adj[v])
        {

            // Degree of v is less than k, 
            // then degree of adjacent
            // must be reduced
            if (vDegree[v] < k)
                vDegree[i]--;

            // If adjacent is not 
            // processed, process it
            if (!visited[i]) 
            {

                // If degree of adjacent after 
                // processing becomes less than
                // k, then reduce degree of v also.
                if (DFSUtil(i, visited, vDegree, k))
                    vDegree[v]--;
            }
        }

        // Return true if degree of
        // v is less than k
        return (vDegree[v] < k);
    }

    // Prints k cores of an undirected graph
    public void printKCores(int k)
    {

        // INITIALIZATION
        // Mark all the vertices as not
        // visited and not processed.
        bool[] visited = new bool[V];
        //bool[] processed = new bool[V];

        int mindeg = int.MaxValue;
        int startvertex = 0;

        // Store degrees of all vertices
        int[] vDegree = new int[V];

        for(int i = 0; i < V; i++) 
        {
            vDegree[i] = adj[i].Count;

            if (vDegree[i] < mindeg)
            {
                mindeg = vDegree[i];
                startvertex = i;
            }
        }
        DFSUtil(startvertex, visited, vDegree, k);

        // DFS traversal to update degrees of all
        // vertices.
        for(int i = 0; i < V; i++)
            if (!visited[i])
                DFSUtil(i, visited, vDegree, k);

        // PRINTING K CORES
        Console.WriteLine("K-Cores : ");

        for(int v = 0; v < V; v++) 
        {

            // Only considering those vertices 
            // which have degree >= K after BFS
            if (vDegree[v] >= k) 
            {
                Console.Write("\n " + v);

                // Traverse adjacency list of v 
                // and print only those adjacent
                // which have vDegree >= k after
                // BFS.
                foreach(int i in adj[v])
                    if (vDegree[i] >= k)
                        Console.Write(" -> " + i);
            }
        }
    }
}

// Driver Code
public static void Main(String[] args) 
{

    // Create a graph given in the 
    // above diagram
    int k = 3;

    Graph g1 = new Graph(9);
    g1.addEdge(0, 1);
    g1.addEdge(0, 2);
    g1.addEdge(1, 2);
    g1.addEdge(1, 5);
    g1.addEdge(2, 3);
    g1.addEdge(2, 4);
    g1.addEdge(2, 5);
    g1.addEdge(2, 6);
    g1.addEdge(3, 4);
    g1.addEdge(3, 6);
    g1.addEdge(3, 7);
    g1.addEdge(4, 6);
    g1.addEdge(4, 7);
    g1.addEdge(5, 6);
    g1.addEdge(5, 8);
    g1.addEdge(6, 7);
    g1.addEdge(6, 8);
    g1.printKCores(k);

    Console.WriteLine();

    Graph g2 = new Graph(13);
    g2.addEdge(0, 1);
    g2.addEdge(0, 2);
    g2.addEdge(0, 3);
    g2.addEdge(1, 4);
    g2.addEdge(1, 5);
    g2.addEdge(1, 6);
    g2.addEdge(2, 7);
    g2.addEdge(2, 8);
    g2.addEdge(2, 9);
    g2.addEdge(3, 10);
    g2.addEdge(3, 11);
    g2.addEdge(3, 12);

    g2.printKCores(k);
}
}

// This code is contributed by Princi Singh

```

**输出**：

```
K-Cores : 

[2] -> 3 -> 4 -> 6
[3] -> 2 -> 4 -> 6 -> 7
[4] -> 2 -> 3 -> 6 -> 7
[6] -> 2 -> 3 -> 4 -> 7
[7] -> 3 -> 4 -> 6

K-Cores : 

```

**上述解决方案的时间复杂度**为 O（V + E），其中 V 为顶点数，E 为边数。

**相关概念**：
简并性：图的简并性是最大值 k，因此图具有 k 核。 例如，上图显示的是 3 核，而没有 4 或更高的核。 因此，上图是 3 简并的。
图的简并性用于衡量图的稀疏程度。

**参考**：
[https://zh.wikipedia.org/wiki/Degeneracy_%28graph_theory%29](https://en.wikipedia.org/wiki/Degeneracy_%28graph_theory%29)
本文由 **Rachit Belwariar** 提供 。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

