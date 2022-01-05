# 打印从给定源到目的地的所有路径

> 原文:[https://www . geesforgeks . org/find-path-given-source-destination/](https://www.geeksforgeeks.org/find-paths-given-source-destination/)

给定一个有向图、一个源顶点和一个目标顶点，打印从给定顶点到目标顶点的所有路径。
考虑以下有向图。让 s 为 2，d 为 3。从 2 到 3 有 3 种不同的路径。

[![allPaths](img/3bae321fd72c187df30b2e6e2e308f87.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/allPaths.png)

**进场:**

1.  其思想是对给定的有向图进行[深度优先遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。
2.  从源开始 DFS 遍历。
3.  继续将访问过的顶点存储在数组或哈希映射中，比如“路径[]”。
4.  如果到达目标顶点，打印路径[]的内容。
5.  重要的是将路径[]中的当前顶点也标记为已访问，这样遍历就不会循环进行。

以下是上述想法的实现。

## C++14

```
// C++ program to print all paths
// from a source to destination.
#include <iostream>
#include <list>
using namespace std;

// A directed graph using
// adjacency list representation
class Graph {
    int V; // No. of vertices in graph
    list<int>* adj; // Pointer to an array containing adjacency lists

    // A recursive function used by printAllPaths()
    void printAllPathsUtil(int, int, bool[], int[], int&);

public:
    Graph(int V); // Constructor
    void addEdge(int u, int v);
    void printAllPaths(int s, int d);
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int u, int v)
{
    adj[u].push_back(v); // Add v to u’s list.
}

// Prints all paths from 's' to 'd'
void Graph::printAllPaths(int s, int d)
{
    // Mark all the vertices as not visited
    bool* visited = new bool[V];

    // Create an array to store paths
    int* path = new int[V];
    int path_index = 0; // Initialize path[] as empty

    // Initialize all vertices as not visited
    for (int i = 0; i < V; i++)
        visited[i] = false;

    // Call the recursive helper function to print all paths
    printAllPathsUtil(s, d, visited, path, path_index);
}

// A recursive function to print all paths from 'u' to 'd'.
// visited[] keeps track of vertices in current path.
// path[] stores actual vertices and path_index is current
// index in path[]
void Graph::printAllPathsUtil(int u, int d, bool visited[],
                              int path[], int& path_index)
{
    // Mark the current node and store it in path[]
    visited[u] = true;
    path[path_index] = u;
    path_index++;

    // If current vertex is same as destination, then print
    // current path[]
    if (u == d) {
        for (int i = 0; i < path_index; i++)
            cout << path[i] << " ";
        cout << endl;
    }
    else // If current vertex is not destination
    {
        // Recur for all the vertices adjacent to current vertex
        list<int>::iterator i;
        for (i = adj[u].begin(); i != adj[u].end(); ++i)
            if (!visited[*i])
                printAllPathsUtil(*i, d, visited, path, path_index);
    }

    // Remove current vertex from path[] and mark it as unvisited
    path_index--;
    visited[u] = false;
}

// Driver program
int main()
{
    // Create a graph given in the above diagram
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(0, 3);
    g.addEdge(2, 0);
    g.addEdge(2, 1);
    g.addEdge(1, 3);

    int s = 2, d = 3;
    cout << "Following are all different paths from " << s << " to " << d << endl;
    g.printAllPaths(s, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to print all
// paths from a source to
// destination.
import java.util.ArrayList;
import java.util.List;

// A directed graph using
// adjacency list representation
public class Graph {

    // No. of vertices in graph
    private int v;

    // adjacency list
    private ArrayList<Integer>[] adjList;

    // Constructor
    public Graph(int vertices)
    {

        // initialise vertex count
        this.v = vertices;

        // initialise adjacency list
        initAdjList();
    }

    // utility method to initialise
    // adjacency list
    @SuppressWarnings("unchecked")
    private void initAdjList()
    {
        adjList = new ArrayList[v];

        for (int i = 0; i < v; i++) {
            adjList[i] = new ArrayList<>();
        }
    }

    // add edge from u to v
    public void addEdge(int u, int v)
    {
        // Add v to u's list.
        adjList[u].add(v);
    }

    // Prints all paths from
    // 's' to 'd'
    public void printAllPaths(int s, int d)
    {
        boolean[] isVisited = new boolean[v];
        ArrayList<Integer> pathList = new ArrayList<>();

        // add source to path[]
        pathList.add(s);

        // Call recursive utility
        printAllPathsUtil(s, d, isVisited, pathList);
    }

    // A recursive function to print
    // all paths from 'u' to 'd'.
    // isVisited[] keeps track of
    // vertices in current path.
    // localPathList<> stores actual
    // vertices in the current path
    private void printAllPathsUtil(Integer u, Integer d,
                                   boolean[] isVisited,
                                   List<Integer> localPathList)
    {

        if (u.equals(d)) {
            System.out.println(localPathList);
            // if match found then no need to traverse more till depth
            return;
        }

        // Mark the current node
        isVisited[u] = true;

        // Recur for all the vertices
        // adjacent to current vertex
        for (Integer i : adjList[u]) {
            if (!isVisited[i]) {
                // store current node
                // in path[]
                localPathList.add(i);
                printAllPathsUtil(i, d, isVisited, localPathList);

                // remove current node
                // in path[]
                localPathList.remove(i);
            }
        }

        // Mark the current node
        isVisited[u] = false;
    }

    // Driver program
    public static void main(String[] args)
    {
        // Create a sample graph
        Graph g = new Graph(4);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(0, 3);
        g.addEdge(2, 0);
        g.addEdge(2, 1);
        g.addEdge(1, 3);

        // arbitrary source
        int s = 2;

        // arbitrary destination
        int d = 3;

        System.out.println(
            "Following are all different paths from "
            + s + " to " + d);
        g.printAllPaths(s, d);
    }
}

// This code is contributed by Himanshu Shekhar.
```

## 计算机编程语言

```
# Python program to print all paths from a source to destination.

from collections import defaultdict

# This class represents a directed graph
# using adjacency list representation
class Graph:

    def __init__(self, vertices):
        # No. of vertices
        self.V = vertices

        # default dictionary to store graph
        self.graph = defaultdict(list)

    # function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)

    '''A recursive function to print all paths from 'u' to 'd'.
    visited[] keeps track of vertices in current path.
    path[] stores actual vertices and path_index is current
    index in path[]'''
    def printAllPathsUtil(self, u, d, visited, path):

        # Mark the current node as visited and store in path
        visited[u]= True
        path.append(u)

        # If current vertex is same as destination, then print
        # current path[]
        if u == d:
            print path
        else:
            # If current vertex is not destination
            # Recur for all the vertices adjacent to this vertex
            for i in self.graph[u]:
                if visited[i]== False:
                    self.printAllPathsUtil(i, d, visited, path)

        # Remove current vertex from path[] and mark it as unvisited
        path.pop()
        visited[u]= False

    # Prints all paths from 's' to 'd'
    def printAllPaths(self, s, d):

        # Mark all the vertices as not visited
        visited =[False]*(self.V)

        # Create an array to store paths
        path = []

        # Call the recursive helper function to print all paths
        self.printAllPathsUtil(s, d, visited, path)

# Create a graph given in the above diagram
g = Graph(4)
g.addEdge(0, 1)
g.addEdge(0, 2)
g.addEdge(0, 3)
g.addEdge(2, 0)
g.addEdge(2, 1)
g.addEdge(1, 3)

s = 2 ; d = 3
print ("Following are all different paths from % d to % d :" %(s, d))
g.printAllPaths(s, d)
# This code is contributed by Neelam Yadav
```

## C#

```
// C# program to print all
// paths from a source to
// destination.
using System;
using System.Collections.Generic;

// A directed graph using
// adjacency list representation
public class Graph {

    // No. of vertices in graph
    private int v;

    // adjacency list
    private List<int>[] adjList;

    // Constructor
    public Graph(int vertices)
    {

        // initialise vertex count
        this.v = vertices;

        // initialise adjacency list
        initAdjList();
    }

    // utility method to initialise
    // adjacency list
    private void initAdjList()
    {
        adjList = new List<int>[v];

        for (int i = 0; i < v; i++) {
            adjList[i] = new List<int>();
        }
    }

    // add edge from u to v
    public void addEdge(int u, int v)
    {
        // Add v to u's list.
        adjList[u].Add(v);
    }

    // Prints all paths from
    // 's' to 'd'
    public void printAllPaths(int s, int d)
    {
        bool[] isVisited = new bool[v];
        List<int> pathList = new List<int>();

        // add source to path[]
        pathList.Add(s);

        // Call recursive utility
        printAllPathsUtil(s, d, isVisited, pathList);
    }

    // A recursive function to print
    // all paths from 'u' to 'd'.
    // isVisited[] keeps track of
    // vertices in current path.
    // localPathList<> stores actual
    // vertices in the current path
    private void printAllPathsUtil(int u, int d,
                                   bool[] isVisited,
                                   List<int> localPathList)
    {

        if (u.Equals(d)) {
            Console.WriteLine(string.Join(" ", localPathList));
            // if match found then no need
            // to traverse more till depth
            return;
        }

        // Mark the current node
        isVisited[u] = true;

        // Recur for all the vertices
        // adjacent to current vertex
        foreach(int i in adjList[u])
        {
            if (!isVisited[i]) {
                // store current node
                // in path[]
                localPathList.Add(i);
                printAllPathsUtil(i, d, isVisited,
                                  localPathList);

                // remove current node
                // in path[]
                localPathList.Remove(i);
            }
        }

        // Mark the current node
        isVisited[u] = false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Create a sample graph
        Graph g = new Graph(4);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(0, 3);
        g.addEdge(2, 0);
        g.addEdge(2, 1);
        g.addEdge(1, 3);

        // arbitrary source
        int s = 2;

        // arbitrary destination
        int d = 3;

        Console.WriteLine("Following are all different"
                          + " paths from " + s + " to " + d);
        g.printAllPaths(s, d);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to print all
// paths from a source to
// destination.

let  v;

let adjList;

// A directed graph using
// adjacency list representation
function Graph(vertices)
{
    // initialise vertex count
        v = vertices;

        // initialise adjacency list
        initAdjList();
}

// utility method to initialise
    // adjacency list
function initAdjList()
{
    adjList = new Array(v);

        for (let i = 0; i < v; i++) {
            adjList[i] = [];
        }
}

// add edge from u to v
function addEdge(u,v)
{
    // Add v to u's list.
        adjList[u].push(v);
}

// Prints all paths from
    // 's' to 'd'
function printAllPaths(s,d)
{
     let isVisited = new Array(v);
     for(let i=0;i<v;i++)
         isVisited[i]=false;
        let pathList = [];

        // add source to path[]
        pathList.push(s);

        // Call recursive utility
        printAllPathsUtil(s, d, isVisited, pathList);
}

// A recursive function to print
    // all paths from 'u' to 'd'.
    // isVisited[] keeps track of
    // vertices in current path.
    // localPathList<> stores actual
    // vertices in the current path
function printAllPathsUtil(u,d,isVisited,localPathList)
{
    if (u == (d)) {
            document.write(localPathList+"<br>");
            // if match found then no need to
            // traverse more till depth
            return;
        }

        // Mark the current node
        isVisited[u] = true;

        // Recur for all the vertices
        // adjacent to current vertex
        for (let i=0;i< adjList[u].length;i++) {
            if (!isVisited[adjList[u][i]]) {
                // store current node
                // in path[]
                localPathList.push(adjList[u][i]);
                printAllPathsUtil(adjList[u][i], d,
                isVisited, localPathList);

                // remove current node
                // in path[]
                localPathList.splice(localPathList.indexOf
                (adjList[u][i]),1);
            }
        }

        // Mark the current node
        isVisited[u] = false;
}

 // Driver program
// Create a sample graph
Graph(4);
addEdge(0, 1);
addEdge(0, 2);
addEdge(0, 3);
addEdge(2, 0);
addEdge(2, 1);
addEdge(1, 3);

// arbitrary source
let s = 2;

// arbitrary destination
let d = 3;

document.write(
"Following are all different paths from "
+ s + " to " + d+"<Br>");
printAllPaths(s, d);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Following are all different paths from 2 to 3
2 0 1 3
2 0 3
2 1 3 
```

**复杂度分析:**

*   **时间复杂度:** O(V^V).
    时间复杂度为多项式。从每个顶点有 v 个顶点可以从当前顶点访问。
*   **辅助空间:** O(V^V).
    存储路径需要 V^V 空间。

本文由**希瓦姆·古普塔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。