# 图着色|集合 2(贪婪算法)

> 原文:[https://www . geesforgeks . org/graph-coloring-set-2-greedy-algorithm/](https://www.geeksforgeeks.org/graph-coloring-set-2-greedy-algorithm/)

我们在前一篇文章中介绍了[图形着色和应用](http://www.geeksforgeeks.org/graph-coloring-applications/)。如前一篇文章中所讨论的，图着色被广泛使用。不幸的是，由于这个问题是一个已知的 [NP 完全问题](http://www.geeksforgeeks.org/np-completeness-set-1/)，所以没有有效的算法来用最少的颜色数给图着色。不过，有一些近似算法可以解决这个问题。下面是分配颜色的基本贪婪算法。它不保证使用最少的颜色，但它保证了颜色数量的上限。基本算法从不使用超过 d+1 种颜色，其中 d 是给定图中顶点的最大度数。

**基本贪婪着色算法:**

> **1。**用第一种颜色给第一个顶点上色。
> T3】2。对剩余的 V-1 顶点执行以下操作。
> ….. **a)** 考虑当前拾取的顶点，并使用
> 最低编号的颜色对其进行着色，该颜色尚未在与其相邻的任何先前
> 着色的顶点上使用。如果所有以前使用的颜色
> 都出现在与 v 相邻的顶点上，则为其指定一种新的颜色。

以下是上述贪婪算法的实现。

## C++

```
// A C++ program to implement greedy algorithm for graph coloring
#include <iostream>
#include <list>
using namespace std;

// A class that represents an undirected graph
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;    // A dynamic array of adjacency lists
public:
    // Constructor and destructor
    Graph(int V)   { this->V = V; adj = new list<int>[V]; }
    ~Graph()       { delete [] adj; }

    // function to add an edge to graph
    void addEdge(int v, int w);

    // Prints greedy coloring of the vertices
    void greedyColoring();
};

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
    adj[w].push_back(v);  // Note: the graph is undirected
}

// Assigns colors (starting from 0) to all vertices and prints
// the assignment of colors
void Graph::greedyColoring()
{
    int result[V];

    // Assign the first color to first vertex
    result[0]  = 0;

    // Initialize remaining V-1 vertices as unassigned
    for (int u = 1; u < V; u++)
        result[u] = -1;  // no color is assigned to u

    // A temporary array to store the available colors. True
    // value of available[cr] would mean that the color cr is
    // assigned to one of its adjacent vertices
    bool available[V];
    for (int cr = 0; cr < V; cr++)
        available[cr] = false;

    // Assign colors to remaining V-1 vertices
    for (int u = 1; u < V; u++)
    {
        // Process all adjacent vertices and flag their colors
        // as unavailable
        list<int>::iterator i;
        for (i = adj[u].begin(); i != adj[u].end(); ++i)
            if (result[*i] != -1)
                available[result[*i]] = true;

        // Find the first available color
        int cr;
        for (cr = 0; cr < V; cr++)
            if (available[cr] == false)
                break;

        result[u] = cr; // Assign the found color

        // Reset the values back to false for the next iteration
        for (i = adj[u].begin(); i != adj[u].end(); ++i)
            if (result[*i] != -1)
                available[result[*i]] = false;
    }

    // print the result
    for (int u = 0; u < V; u++)
        cout << "Vertex " << u << " --->  Color "
             << result[u] << endl;
}

// Driver program to test above function
int main()
{
    Graph g1(5);
    g1.addEdge(0, 1);
    g1.addEdge(0, 2);
    g1.addEdge(1, 2);
    g1.addEdge(1, 3);
    g1.addEdge(2, 3);
    g1.addEdge(3, 4);
    cout << "Coloring of graph 1 \n";
    g1.greedyColoring();

    Graph g2(5);
    g2.addEdge(0, 1);
    g2.addEdge(0, 2);
    g2.addEdge(1, 2);
    g2.addEdge(1, 4);
    g2.addEdge(2, 4);
    g2.addEdge(4, 3);
    cout << "\nColoring of graph 2 \n";
    g2.greedyColoring();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to implement greedy algorithm for graph coloring
import java.io.*;
import java.util.*;
import java.util.LinkedList;

// This class represents an undirected graph using adjacency list
class Graph
{
    private int V;   // No. of vertices
    private LinkedList<Integer> adj[]; //Adjacency List

    //Constructor
    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];
        for (int i=0; i<v; ++i)
            adj[i] = new LinkedList();
    }

    //Function to add an edge into the graph
    void addEdge(int v,int w)
    {
        adj[v].add(w);
        adj[w].add(v); //Graph is undirected
    }

    // Assigns colors (starting from 0) to all vertices and
    // prints the assignment of colors
    void greedyColoring()
    {
        int result[] = new int[V];

        // Initialize all vertices as unassigned
        Arrays.fill(result, -1);

        // Assign the first color to first vertex
        result[0]  = 0;

        // A temporary array to store the available colors. False
        // value of available[cr] would mean that the color cr is
        // assigned to one of its adjacent vertices
        boolean available[] = new boolean[V];

        // Initially, all colors are available
        Arrays.fill(available, true);

        // Assign colors to remaining V-1 vertices
        for (int u = 1; u < V; u++)
        {
            // Process all adjacent vertices and flag their colors
            // as unavailable
            Iterator<Integer> it = adj[u].iterator() ;
            while (it.hasNext())
            {
                int i = it.next();
                if (result[i] != -1)
                    available[result[i]] = false;
            }

            // Find the first available color
            int cr;
            for (cr = 0; cr < V; cr++){
                if (available[cr])
                    break;
            }

            result[u] = cr; // Assign the found color

            // Reset the values back to true for the next iteration
            Arrays.fill(available, true);
        }

        // print the result
        for (int u = 0; u < V; u++)
            System.out.println("Vertex " + u + " --->  Color "
                                + result[u]);
    }

    // Driver method
    public static void main(String args[])
    {
        Graph g1 = new Graph(5);
        g1.addEdge(0, 1);
        g1.addEdge(0, 2);
        g1.addEdge(1, 2);
        g1.addEdge(1, 3);
        g1.addEdge(2, 3);
        g1.addEdge(3, 4);
        System.out.println("Coloring of graph 1");
        g1.greedyColoring();

        System.out.println();
        Graph g2 = new Graph(5);
        g2.addEdge(0, 1);
        g2.addEdge(0, 2);
        g2.addEdge(1, 2);
        g2.addEdge(1, 4);
        g2.addEdge(2, 4);
        g2.addEdge(4, 3);
        System.out.println("Coloring of graph 2 ");
        g2.greedyColoring();
    }
}
// This code is contributed by Aakash Hasija
```

## 蟒蛇 3

```
# Python3 program to implement greedy
# algorithm for graph coloring

def addEdge(adj, v, w):

    adj[v].append(w)

    # Note: the graph is undirected
    adj[w].append(v) 
    return adj

# Assigns colors (starting from 0) to all
# vertices and prints the assignment of colors
def greedyColoring(adj, V):

    result = [-1] * V

    # Assign the first color to first vertex
    result[0] = 0;

    # A temporary array to store the available colors.
    # True value of available[cr] would mean that the
    # color cr is assigned to one of its adjacent vertices
    available = [False] * V

    # Assign colors to remaining V-1 vertices
    for u in range(1, V):

        # Process all adjacent vertices and
        # flag their colors as unavailable
        for i in adj[u]:
            if (result[i] != -1):
                available[result[i]] = True

        # Find the first available color
        cr = 0
        while cr < V:
            if (available[cr] == False):
                break

            cr += 1

        # Assign the found color
        result[u] = cr

        # Reset the values back to false
        # for the next iteration
        for i in adj[u]:
            if (result[i] != -1):
                available[result[i]] = False

    # Print the result
    for u in range(V):
        print("Vertex", u, " --->  Color", result[u])

# Driver Code
if __name__ == '__main__':

    g1 = [[] for i in range(5)]
    g1 = addEdge(g1, 0, 1)
    g1 = addEdge(g1, 0, 2)
    g1 = addEdge(g1, 1, 2)
    g1 = addEdge(g1, 1, 3)
    g1 = addEdge(g1, 2, 3)
    g1 = addEdge(g1, 3, 4)
    print("Coloring of graph 1 ")
    greedyColoring(g1, 5)

    g2 = [[] for i in range(5)]
    g2 = addEdge(g2, 0, 1)
    g2 = addEdge(g2, 0, 2)
    g2 = addEdge(g2, 1, 2)
    g2 = addEdge(g2, 1, 4)
    g2 = addEdge(g2, 2, 4)
    g2 = addEdge(g2, 4, 3)
    print("\nColoring of graph 2")
    greedyColoring(g2, 5)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program to implement greedy
// algorithm for graph coloring

// This class represents a directed graph
// using adjacency list representation
class Graph{

// Constructor
constructor(v)
{
    this.V = v;
    this.adj = new Array(v);

    for(let i = 0; i < v; ++i)
        this.adj[i] = [];

    this.Time = 0;
}

// Function to add an edge into the graph
addEdge(v,w)
{
    this.adj[v].push(w);

    // Graph is undirected
    this.adj[w].push(v);
}

// Assigns colors (starting from 0) to all
// vertices and prints the assignment of colors
greedyColoring()
{
    let result = new Array(this.V);

    // Initialize all vertices as unassigned
    for(let i = 0; i < this.V; i++)
        result[i] = -1;

    // Assign the first color to first vertex
    result[0]  = 0;

    // A temporary array to store the available
    // colors. False value of available[cr] would
    // mean that the color cr is assigned to one
    // of its adjacent vertices
    let available = new Array(this.V);

    // Initially, all colors are available
    for(let i = 0; i < this.V; i++)
        available[i] = true;

    // Assign colors to remaining V-1 vertices
    for(let u = 1; u < this.V; u++)
    {

        // Process all adjacent vertices and
        // flag their colors as unavailable
        for(let it of this.adj[u])
        {
            let i = it;
            if (result[i] != -1)
                available[result[i]] = false;
        }

        // Find the first available color
        let cr;
        for(cr = 0; cr < this.V; cr++)
        {
            if (available[cr])
                break;
        }

        // Assign the found color
        result[u] = cr;

        // Reset the values back to true
        // for the next iteration
        for(let i = 0; i < this.V; i++)
            available[i] = true;
    }

    // print the result
    for(let u = 0; u < this.V; u++)
        document.write("Vertex " + u + " --->  Color " +
                       result[u] + "<br>");
}
}   

// Driver code
let g1 = new Graph(5);
g1.addEdge(0, 1);
g1.addEdge(0, 2);
g1.addEdge(1, 2);
g1.addEdge(1, 3);
g1.addEdge(2, 3);
g1.addEdge(3, 4);
document.write("Coloring of graph 1<br>");
g1.greedyColoring();

document.write("<br>");
let g2 = new Graph(5);
g2.addEdge(0, 1);
g2.addEdge(0, 2);
g2.addEdge(1, 2);
g2.addEdge(1, 4);
g2.addEdge(2, 4);
g2.addEdge(4, 3);
document.write("Coloring of graph 2<br> ");
g2.greedyColoring();

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Coloring of graph 1
Vertex 0 --->  Color 0
Vertex 1 --->  Color 1
Vertex 2 --->  Color 2
Vertex 3 --->  Color 0
Vertex 4 --->  Color 1

Coloring of graph 2
Vertex 0 --->  Color 0
Vertex 1 --->  Color 1
Vertex 2 --->  Color 2
Vertex 3 --->  Color 0
Vertex 4 --->  Color 3
```

时间复杂度:最坏情况下的 O(V^2 + E)。

**基本算法分析**
上面的算法并不总是使用最小数量的颜色。此外，有时使用的颜色数量取决于顶点的处理顺序。例如，考虑以下两个图表。请注意，在右侧的图形中，顶点 3 和 4 被交换。如果我们考虑左图中的顶点 0，1，2，3，4，我们可以用 3 种颜色给图着色。但是如果我们考虑右图中的顶点 0，1，2，3，4，我们需要 4 种颜色。

![graph_coloring2](img/d93d336f44f59b7ee193450e26ff1b4e.png)

所以顶点的选取顺序很重要。许多人提出了不同的方法来找到比基本算法平均效果更好的排序。最常见的是[威尔士-鲍威尔算法](http://mrsleblancsmath.pbworks.com/w/file/fetch/46119304/vertex%20coloring%20algorithm.pdf)，它按照度数降序考虑顶点。

**基本算法如何保证 d+1 的上界？**
这里 d 是给定图中的最大度数。因为 d 是最大度数，所以一个顶点不能附着在 d 个以上的顶点上。当我们给一个顶点着色时，最多 d 种颜色可能已经被它的相邻顶点使用了。为了给这个顶点着色，我们需要选择相邻顶点不使用的最小编号颜色。如果颜色的编号是 1，2，…，那么这种最小数字的值必须在 1 到 d+1 之间(注意，d 数字已经被相邻顶点拾取)。
这也可以用归纳法证明。见[本](http://www.youtube.com/watch?v=h9wxtqoa1jY)视频讲座求证。
我们很快将讨论一些关于色数和图着色的有趣事实。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息