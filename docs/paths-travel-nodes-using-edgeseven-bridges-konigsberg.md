# 使用每条边穿过每个节点的路径(柯尼斯堡的七座桥)

> 原文:[https://www . geesforgeks . org/path-travel-nodes-use-edge seven-bridges-konigsberg/](https://www.geeksforgeeks.org/paths-travel-nodes-using-edgeseven-bridges-konigsberg/)

这些节点之间有 n 个节点和 m 个桥。使用每条边打印通过每个节点的可能路径(如果可能)，只通过每条边一次。

![](img/ed0ac67af5c2b609c4fece2759ea1fd1.png)

**示例:**

```
Input : [[0, 1, 0, 0, 1],
         [1, 0, 1, 1, 0],
         [0, 1, 0, 1, 0],
         [0, 1, 1, 0, 0],
         [1, 0, 0, 0, 0]]

Output : 5 -> 1 -> 2 -> 4 -> 3 -> 2

Input : [[0, 1, 0, 1, 1],
         [1, 0, 1, 0, 1],
         [0, 1, 0, 1, 1],
         [1, 1, 1, 0, 0],
         [1, 0, 1, 0, 0]]

Output : "No Solution"
```

它是图论中著名的问题之一，被称为“柯尼希斯堡七桥”问题。这个问题是由著名数学家莱昂哈德·欧拉在 1735 年解决的。这个问题也被认为是图论的开端。
当时的问题是:普鲁士的哥尼斯堡市周围有 7 座桥梁连接着 4 块土地。有没有什么方法可以从任何一片土地出发，穿过每一座桥一次，而且只穿过一次？请参见[这些维基百科图片](https://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg#/media/File:7_bridges.svg)了解更多信息。

欧拉首先引入图论来解决这个问题。他认为每一个陆地都是一个图的节点，中间的每一座桥都是一条边。现在他计算了在那个图中是否有[欧拉路径](https://www.geeksforgeeks.org/mathematics-euler-hamiltonian-paths/)。如果有欧拉路径，那么就有解决方案，否则就没有。
这里的问题，是 1735 年问题的广义版本。

下面是实现:

## C++

```
// A C++ program print Eulerian Trail in a
// given Eulerian or Semi-Eulerian Graph
#include <iostream>
#include <string.h>
#include <algorithm>
#include <list>
using namespace std;

// A class that represents an undirected graph
class Graph
{
// No. of vertices
    int V;

    // A dynamic array of adjacency lists
    list<int> *adj;
public:

    // Constructor and destructor
    Graph(int V)
    {
        this->V = V;
        adj = new list<int>[V];
    }
    ~Graph()
    {
        delete [] adj;
    }

    // functions to add and remove edge
    void addEdge(int u, int v)
    {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    void rmvEdge(int u, int v);

    // Methods to print Eulerian tour
    void printEulerTour();
    void printEulerUtil(int s);

    // This function returns count of vertices
    // reachable from v. It does DFS
    int DFSCount(int v, bool visited[]);

    // Utility function to check if edge u-v
    // is a valid next edge in Eulerian trail or circuit
    bool isValidNextEdge(int u, int v);
};

/* The main function that print Eulerian Trail.
It first finds an odd degree vertex (if there is any)
and then calls printEulerUtil() to print the path */
void Graph::printEulerTour()
{
    // Find a vertex with odd degree
    int u = 0;

    for (int i = 0; i < V; i++)
        if (adj[i].size() & 1)
        {
            u = i;
            break;
        }

    // Print tour starting from oddv
    printEulerUtil(u);
    cout << endl;
}

// Print Euler tour starting from vertex u
void Graph::printEulerUtil(int u)
{

    // Recur for all the vertices adjacent to
    // this vertex
    list<int>::iterator i;
    for (i = adj[u].begin(); i != adj[u].end(); ++i)
    {
        int v = *i;

        // If edge u-v is not removed and it's a a
        // valid next edge
        if (v != -1 && isValidNextEdge(u, v))
        {
            cout << u << "-" << v << " ";
            rmvEdge(u, v);
            printEulerUtil(v);
        }
    }
}

// The function to check if edge u-v can be considered
// as next edge in Euler Tout
bool Graph::isValidNextEdge(int u, int v)
{

    // The edge u-v is valid in one of the following
    // two cases:

    // 1) If v is the only adjacent vertex of u
    int count = 0; // To store count of adjacent vertices
    list<int>::iterator i;
    for (i = adj[u].begin(); i != adj[u].end(); ++i)
        if (*i != -1)
            count++;
    if (count == 1)
        return true;

    // 2) If there are multiple adjacents, then u-v
    //    is not a bridge
    // Do following steps to check if u-v is a bridge

    // 2.a) count of vertices reachable from u
    bool visited[V];
    memset(visited, false, V);
    int count1 = DFSCount(u, visited);

    // 2.b) Remove edge (u, v) and after removing
    // the edge, count vertices reachable from u
    rmvEdge(u, v);
    memset(visited, false, V);
    int count2 = DFSCount(u, visited);

    // 2.c) Add the edge back to the graph
    addEdge(u, v);

    // 2.d) If count1 is greater, then edge (u, v)
    // is a bridge
    return (count1 > count2)? false: true;
}

// This function removes edge u-v from graph.
// It removes the edge by replacing adjacent
// vertex value with -1.
void Graph::rmvEdge(int u, int v)
{
    // Find v in adjacency list of u and replace
    // it with -1
    list<int>::iterator iv = find(adj[u].begin(),
                                adj[u].end(), v);
    *iv = -1;

    // Find u in adjacency list of v and replace
    // it with -1
    list<int>::iterator iu = find(adj[v].begin(),
                                  adj[v].end(), u);
    *iu = -1;
}

// A DFS based function to count reachable
// vertices from v
int Graph::DFSCount(int v, bool visited[])
{
    // Mark the current node as visited
    visited[v] = true;
    int count = 1;

    // Recur for all vertices adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (*i != -1 && !visited[*i])
            count += DFSCount(*i, visited);

    return count;
}

// Driver program to test above function
int main()
{
    // Let us first create and test
    // graphs shown in above figure
    Graph g1(4);
    g1.addEdge(0, 1);
    g1.addEdge(0, 2);
    g1.addEdge(1, 2);
    g1.addEdge(2, 3);
    g1.printEulerTour();

    Graph g3(4);
    g3.addEdge(0, 1);
    g3.addEdge(1, 0);
    g3.addEdge(0, 2);
    g3.addEdge(2, 0);
    g3.addEdge(2, 3);
    g3.addEdge(3, 1);

    // comment out this line and you will see that
    // it gives TLE because there is no possible
    // output g3.addEdge(0, 3);
    g3.printEulerTour();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A java program print Eulerian Trail in a
// given Eulerian or Semi-Eulerian Graph
import java.util.*;

public class GFG{

    // A class that represents an undirected graph
    static class Graph
    {
        // No. of vertices
        int V;

        // A dynamic array of adjacency lists
        ArrayList<ArrayList<Integer>> adj;

        // Constructor
        Graph(int V)
        {
            this.V = V;
            adj = new ArrayList<ArrayList<Integer>>();

            for(int i=0; i<V; i++){
                adj.add(new ArrayList<Integer>());
            }
        }

        // functions to add and remove edge
        void addEdge(int u, int v)
        {
            adj.get(u).add(v);
            adj.get(v).add(u);
        }

        // This function removes edge u-v from graph.
        // It removes the edge by replacing adjacent
        // vertex value with -1.
        void rmvEdge(int u, int v)
        {
            // Find v in adjacency list of u and replace
            // it with -1
            int iv = find(adj.get(u), v);
            adj.get(u).set(iv, -1);

            // Find u in adjacency list of v and replace
            // it with -1
            int iu = find(adj.get(v), u);
            adj.get(v).set(iu, -1);
        }

        int find(ArrayList<Integer> al, int v){

            for(int i=0; i<al.size(); i++){
                if(al.get(i) == v){
                    return i;
                }
            }

            return -1;
        }

        // Methods to print Eulerian tour
        /* The main function that print Eulerian Trail.
        It first finds an odd degree vertex (if there is any)
        and then calls printEulerUtil() to print the path */
        void printEulerTour()
        {

            // Find a vertex with odd degree
            int u = 0;

            for (int i = 0; i < V; i++){
                if (adj.get(i).size() % 2 == 1)
                {
                    u = i;
                    break;
                }
            }

            // Print tour starting from oddv
            printEulerUtil(u);
            System.out.println();
        }

        // Print Euler tour starting from vertex u
        void printEulerUtil(int u)
        {

            // Recur for all the vertices adjacent to
            // this vertex
            for (int i = 0; i<adj.get(u).size(); ++i)
            {
                int v = adj.get(u).get(i);

                // If edge u-v is not removed and it's a a
                // valid next edge
                if (v != -1 && isValidNextEdge(u, v))
                {
                    System.out.print(u + "-" + v + " ");
                    rmvEdge(u, v);
                    printEulerUtil(v);
                }
            }
        }

        // This function returns count of vertices
        // reachable from v. It does DFS
        // A DFS based function to count reachable
        // vertices from v
        int DFSCount(int v, boolean visited[])
        {
            // Mark the current node as visited
            visited[v] = true;
            int count = 1;

            // Recur for all vertices adjacent to this vertex
            for (int i = 0; i<adj.get(v).size(); ++i){
                int u = adj.get(v).get(i);

                if (u != -1 && !visited[u]){
                    count += DFSCount(u, visited);
                }
            }

            return count;
        }

        // Utility function to check if edge u-v
        // is a valid next edge in Eulerian trail or circuit
        // The function to check if edge u-v can be considered
        // as next edge in Euler Tout
        boolean isValidNextEdge(int u, int v)
        {

            // The edge u-v is valid in one of the following
            // two cases:

            // 1) If v is the only adjacent vertex of u
            int count = 0; // To store count of adjacent vertices
            for (int i = 0; i<adj.get(u).size(); ++i)
                if (adj.get(u).get(i) != -1)
                    count++;
            if (count == 1)
                return true;

            // 2) If there are multiple adjacents, then u-v
            // is not a bridge
            // Do following steps to check if u-v is a bridge

            // 2.a) count of vertices reachable from u
            boolean visited[] = new boolean[V];
            Arrays.fill(visited, false);
            int count1 = DFSCount(u, visited);

            // 2.b) Remove edge (u, v) and after removing
            // the edge, count vertices reachable from u
            rmvEdge(u, v);
            Arrays.fill(visited, false);
            int count2 = DFSCount(u, visited);

            // 2.c) Add the edge back to the graph
            addEdge(u, v);

            // 2.d) If count1 is greater, then edge (u, v)
            // is a bridge
            return (count1 > count2)? false: true;
        }
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        // Let us first create and test
        // graphs shown in above figure
        Graph g1 = new Graph(4);
        g1.addEdge(0, 1);
        g1.addEdge(0, 2);
        g1.addEdge(1, 2);
        g1.addEdge(2, 3);
        g1.printEulerTour();

        Graph g3 = new Graph(4);
        g3.addEdge(0, 1);
        g3.addEdge(1, 0);
        g3.addEdge(0, 2);
        g3.addEdge(2, 0);
        g3.addEdge(2, 3);
        g3.addEdge(3, 1);

        // comment out this line and you will see that
        // it gives TLE because there is no possible
        // output g3.addEdge(0, 3);
        g3.printEulerTour();
    }
}

// This code is contributed by adityapande88.
```

**Output:** 

```
2-0  0-1  1-2  2-3  
1-0  0-2  2-3  3-1  1-0  0-2
```