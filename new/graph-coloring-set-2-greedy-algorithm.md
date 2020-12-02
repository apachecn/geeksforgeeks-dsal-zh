# 图形着色| 第 2 组（贪婪算法）

> 原文： [https://www.geeksforgeeks.org/graph-coloring-set-2-greedy-algorithm/](https://www.geeksforgeeks.org/graph-coloring-set-2-greedy-algorithm/)

我们在先前的文章中介绍了[图形着色和应用](http://www.geeksforgeeks.org/graph-coloring-applications/)。 如前一篇文章所述，图形着色已被广泛使用。 不幸的是，由于该问题是已知的 [NP 完全问题](http://www.geeksforgeeks.org/np-completeness-set-1/)，因此没有有效的算法可用于用最少的颜色数对图形进行着色。 虽然有解决该问题的近似算法。 以下是分配颜色的基本贪婪算法。 不保证使用最少的颜色，但可以保证颜色数量的上限。 基本算法永远不会使用超过 d + 1 种颜色，其中 d 是给定图中顶点的最大程度。

**基本贪婪着色算法**：

> **1\.** 用第一种颜色着色第一个顶点。
> **2\.** 对剩余的 V-1 顶点执行以下操作。
> ….. **a）**考虑当前拾取的顶点，并以
> 最低编号的颜色对其进行着色，该颜色尚未在与其相邻的任何
> 有色顶点上使用。 如果所有先前使用的颜色
> 出现在与 v 相邻的顶点上，请为其分配新的颜色。

以下是上述贪婪算法的 C ++和 Java 实现。

## C ++

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

## 爪哇

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

Output:

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

时间复杂度：最坏情况下为 O（V ^ 2 + E）。

**基本算法分析**
上面的算法并不总是使用最少的颜色。 同样，有时使用的颜色数量取决于处理顶点的顺序。 例如，考虑以下两个图形。 请注意，在右侧的图中，顶点 3 和 4 被交换。 如果我们考虑左图中的顶点 0、1、2、3、4，则可以使用 3 种颜色为图着色。 但是，如果我们考虑右图中的顶点 0、1、2、3、4，则需要 4 种颜色。

![graph_coloring2](img/d93d336f44f59b7ee193450e26ff1b4e.png)

因此，选取顶点的顺序很重要。 许多人提出了不同的方法来找到比平均算法更有效的排序。 最常见的是[威尔士-鲍威尔算法](http://mrsleblancsmath.pbworks.com/w/file/fetch/46119304/vertex%20coloring%20algorithm.pdf)，该算法按度的降序考虑顶点。

**基本算法如何保证 d + 1 的上限？**
此处 d 是给定图中的最大度数。 由于 d 是最大度数，所以一个顶点最多只能附加到 d 个顶点。 当我们着色一个顶点时，其相邻对象最多可能已经使用了 d 种颜色。 要为该顶点着色，我们需要选择相邻顶点不使用的最小编号的颜色。 如果将颜色编号为 1、2，....，则此类最小数字的值必须在 1 到 d + 1 之间（请注意，相邻顶点已经拾取了 d 个数字）。
这也可以通过归纳法证明。 有关证明，请参见此视频讲座的[。](http://www.youtube.com/watch?v=h9wxtqoa1jY)

我们将很快讨论一些有关色数和图形着色的有趣事实。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

