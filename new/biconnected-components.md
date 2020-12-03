# 双向连接的组件

> 原文： [https://www.geeksforgeeks.org/biconnected-components/](https://www.geeksforgeeks.org/biconnected-components/)

[双向连接的组件](https://en.wikipedia.org/wiki/Biconnected_component)是最大的[双向连接的](https://en.wikipedia.org/wiki/Biconnected_graph) [子图](https://en.wikipedia.org/wiki/Glossary_of_graph_theory#Subgraphs)。

[双向图](https://en.wikipedia.org/wiki/Biconnected_graph)在此处已有讨论。 在本文中，我们将看到如何使用 John Hopcroft 和 Robert Tarjan 的算法在图形中查找[双向连接的组件](https://en.wikipedia.org/wiki/Biconnected_component)。

![Biconnected Components](img/2297f78330cce4c1ef0865e29a801210.png)

在上图中，以下是双向连接的组件：

*   4–2 3–4 3–1 2–3 1–2

*   8–9

*   8–5 7–8 5–7

*   6–0 5–6 1–5 0–1

*   10–11

该算法基于[强连接组件](https://www.geeksforgeeks.org/tarjan-algorithm-find-strongly-connected-components/)文章中讨论的 Disc 和低值。

想法是将访问的边沿存储在堆栈中，而 DFS 在图形上并继续寻找[铰接点](https://www.geeksforgeeks.org/articulation-points-or-cut-vertices-in-a-graph/)（在上图中突出显示）。 一旦找到[铰接点](https://www.geeksforgeeks.org/articulation-points-or-cut-vertices-in-a-graph/) u，从节点 u 开始进行 DFS 时访问的所有边将形成一个[双向连接的组件](https://en.wikipedia.org/wiki/Biconnected_component)。 当一个[连接的组件](https://en.wikipedia.org/wiki/Connected_component_%28graph_theory%29)的 DFS 完成时，堆栈中存在的所有边将形成一个双连接的组件。

如果图形中没有[铰接点](https://www.geeksforgeeks.org/articulation-points-or-cut-vertices-in-a-graph/)，则图形是双向连接的，因此将有一个双向连接的组件，即图形本身。

## C++

```cpp

// A C++ program to find biconnected components in a given undirected graph 
#include <iostream> 
#include <list> 
#include <stack> 
#define NIL -1 
using namespace std; 
int count = 0; 
class Edge { 
public: 
    int u; 
    int v; 
    Edge(int u, int v); 
}; 
Edge::Edge(int u, int v) 
{ 
    this->u = u; 
    this->v = v; 
} 

// A class that represents an directed graph 
class Graph { 
    int V; // No. of vertices 
    int E; // No. of edges 
    list<int>* adj; // A dynamic array of adjacency lists 

    // A Recursive DFS based function used by BCC() 
    void BCCUtil(int u, int disc[], int low[], 
                 list<Edge>* st, int parent[]); 

public: 
    Graph(int V); // Constructor 
    void addEdge(int v, int w); // function to add an edge to graph 
    void BCC(); // prints strongly connected components 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    this->E = 0; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); 
    E++; 
} 

// A recursive function that finds and prints strongly connected 
// components using DFS traversal 
// u --> The vertex to be visited next 
// disc[] --> Stores discovery times of visited vertices 
// low[] -- >> earliest visited vertex (the vertex with minimum 
// discovery time) that can be reached from subtree 
// rooted with current vertex 
// *st -- >> To store visited edges 
void Graph::BCCUtil(int u, int disc[], int low[], list<Edge>* st, 
                    int parent[]) 
{ 
    // A static variable is used for simplicity, we can avoid use 
    // of static variable by passing a pointer. 
    static int time = 0; 

    // Initialize discovery time and low value 
    disc[u] = low[u] = ++time; 
    int children = 0; 

    // Go through all vertices adjacent to this 
    list<int>::iterator i; 
    for (i = adj[u].begin(); i != adj[u].end(); ++i) { 
        int v = *i; // v is current adjacent of 'u' 

        // If v is not visited yet, then recur for it 
        if (disc[v] == -1) { 
            children++; 
            parent[v] = u; 
            // store the edge in stack 
            st->push_back(Edge(u, v)); 
            BCCUtil(v, disc, low, st, parent); 

            // Check if the subtree rooted with 'v' has a 
            // connection to one of the ancestors of 'u' 
            // Case 1 -- per Strongly Connected Components Article 
            low[u] = min(low[u], low[v]); 

            // If u is an articulation point, 
            // pop all edges from stack till u -- v 
            if ((disc[u] == 1 && children > 1) || (disc[u] > 1 && low[v] >= disc[u])) { 
                while (st->back().u != u || st->back().v != v) { 
                    cout << st->back().u << "--" << st->back().v << " "; 
                    st->pop_back(); 
                } 
                cout << st->back().u << "--" << st->back().v; 
                st->pop_back(); 
                cout << endl; 
                count++; 
            } 
        } 

        // Update low value of 'u' only of 'v' is still in stack 
        // (i.e. it's a back edge, not cross edge). 
        // Case 2 -- per Strongly Connected Components Article 
        else if (v != parent[u]) { 
            low[u] = min(low[u], disc[v]); 
            if (disc[v] < disc[u]) { 
                st->push_back(Edge(u, v)); 
            } 
        } 
    } 
} 

// The function to do DFS traversal. It uses BCCUtil() 
void Graph::BCC() 
{ 
    int* disc = new int[V]; 
    int* low = new int[V]; 
    int* parent = new int[V]; 
    list<Edge>* st = new list<Edge>[E]; 

    // Initialize disc and low, and parent arrays 
    for (int i = 0; i < V; i++) { 
        disc[i] = NIL; 
        low[i] = NIL; 
        parent[i] = NIL; 
    } 

    for (int i = 0; i < V; i++) { 
        if (disc[i] == NIL) 
            BCCUtil(i, disc, low, st, parent); 

        int j = 0; 
        // If stack is not empty, pop all edges from stack 
        while (st->size() > 0) { 
            j = 1; 
            cout << st->back().u << "--" << st->back().v << " "; 
            st->pop_back(); 
        } 
        if (j == 1) { 
            cout << endl; 
            count++; 
        } 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    Graph g(12); 
    g.addEdge(0, 1); 
    g.addEdge(1, 0); 
    g.addEdge(1, 2); 
    g.addEdge(2, 1); 
    g.addEdge(1, 3); 
    g.addEdge(3, 1); 
    g.addEdge(2, 3); 
    g.addEdge(3, 2); 
    g.addEdge(2, 4); 
    g.addEdge(4, 2); 
    g.addEdge(3, 4); 
    g.addEdge(4, 3); 
    g.addEdge(1, 5); 
    g.addEdge(5, 1); 
    g.addEdge(0, 6); 
    g.addEdge(6, 0); 
    g.addEdge(5, 6); 
    g.addEdge(6, 5); 
    g.addEdge(5, 7); 
    g.addEdge(7, 5); 
    g.addEdge(5, 8); 
    g.addEdge(8, 5); 
    g.addEdge(7, 8); 
    g.addEdge(8, 7); 
    g.addEdge(8, 9); 
    g.addEdge(9, 8); 
    g.addEdge(10, 11); 
    g.addEdge(11, 10); 
    g.BCC(); 
    cout << "Above are " << count << " biconnected components in graph"; 
    return 0; 
} 

```

## Java

```java

// A Java program to find biconnected components in a given 
// undirected graph 
import java.io.*; 
import java.util.*; 

// This class represents a directed graph using adjacency 
// list representation 
class Graph { 
    private int V, E; // No. of vertices & Edges respectively 
    private LinkedList<Integer> adj[]; // Adjacency List 

    // Count is number of biconnected components. time is 
    // used to find discovery times 
    static int count = 0, time = 0; 

    class Edge { 
        int u; 
        int v; 
        Edge(int u, int v) 
        { 
            this.u = u; 
            this.v = v; 
        } 
    }; 

    // Constructor 
    Graph(int v) 
    { 
        V = v; 
        E = 0; 
        adj = new LinkedList[v]; 
        for (int i = 0; i < v; ++i) 
            adj[i] = new LinkedList(); 
    } 

    // Function to add an edge into the graph 
    void addEdge(int v, int w) 
    { 
        adj[v].add(w); 
        E++; 
    } 

    // A recursive function that finds and prints strongly connected 
    // components using DFS traversal 
    // u --> The vertex to be visited next 
    // disc[] --> Stores discovery times of visited vertices 
    // low[] -- >> earliest visited vertex (the vertex with minimum 
    // discovery time) that can be reached from subtree 
    // rooted with current vertex 
    // *st -- >> To store visited edges 
    void BCCUtil(int u, int disc[], int low[], LinkedList<Edge> st, 
                 int parent[]) 
    { 

        // Initialize discovery time and low value 
        disc[u] = low[u] = ++time; 
        int children = 0; 

        // Go through all vertices adjacent to this 
        Iterator<Integer> it = adj[u].iterator(); 
        while (it.hasNext()) { 
            int v = it.next(); // v is current adjacent of 'u' 

            // If v is not visited yet, then recur for it 
            if (disc[v] == -1) { 
                children++; 
                parent[v] = u; 

                // store the edge in stack 
                st.add(new Edge(u, v)); 
                BCCUtil(v, disc, low, st, parent); 

                // Check if the subtree rooted with 'v' has a 
                // connection to one of the ancestors of 'u' 
                // Case 1 -- per Strongly Connected Components Article 
                if (low[u] > low[v]) 
                    low[u] = low[v]; 

                // If u is an articulation point, 
                // pop all edges from stack till u -- v 
                if ((disc[u] == 1 && children > 1) || (disc[u] > 1 && low[v] >= disc[u])) { 
                    while (st.getLast().u != u || st.getLast().v != v) { 
                        System.out.print(st.getLast().u + "--" + st.getLast().v + " "); 
                        st.removeLast(); 
                    } 
                    System.out.println(st.getLast().u + "--" + st.getLast().v + " "); 
                    st.removeLast(); 

                    count++; 
                } 
            } 

            // Update low value of 'u' only if 'v' is still in stack 
            // (i.e. it's a back edge, not cross edge). 
            // Case 2 -- per Strongly Connected Components Article 
            else if (v != parent[u] && disc[v] < disc[u] ) { 
                if (low[u] > disc[v]) 
                    low[u] = disc[v]; 

                st.add(new Edge(u, v)); 
            } 
        } 
    } 

    // The function to do DFS traversal. It uses BCCUtil() 
    void BCC() 
    { 
        int disc[] = new int[V]; 
        int low[] = new int[V]; 
        int parent[] = new int[V]; 
        LinkedList<Edge> st = new LinkedList<Edge>(); 

        // Initialize disc and low, and parent arrays 
        for (int i = 0; i < V; i++) { 
            disc[i] = -1; 
            low[i] = -1; 
            parent[i] = -1; 
        } 

        for (int i = 0; i < V; i++) { 
            if (disc[i] == -1) 
                BCCUtil(i, disc, low, st, parent); 

            int j = 0; 

            // If stack is not empty, pop all edges from stack 
            while (st.size() > 0) { 
                j = 1; 
                System.out.print(st.getLast().u + "--" + st.getLast().v + " "); 
                st.removeLast(); 
            } 
            if (j == 1) { 
                System.out.println(); 
                count++; 
            } 
        } 
    } 

    public static void main(String args[]) 
    { 
        Graph g = new Graph(12); 
        g.addEdge(0, 1); 
        g.addEdge(1, 0); 
        g.addEdge(1, 2); 
        g.addEdge(2, 1); 
        g.addEdge(1, 3); 
        g.addEdge(3, 1); 
        g.addEdge(2, 3); 
        g.addEdge(3, 2); 
        g.addEdge(2, 4); 
        g.addEdge(4, 2); 
        g.addEdge(3, 4); 
        g.addEdge(4, 3); 
        g.addEdge(1, 5); 
        g.addEdge(5, 1); 
        g.addEdge(0, 6); 
        g.addEdge(6, 0); 
        g.addEdge(5, 6); 
        g.addEdge(6, 5); 
        g.addEdge(5, 7); 
        g.addEdge(7, 5); 
        g.addEdge(5, 8); 
        g.addEdge(8, 5); 
        g.addEdge(7, 8); 
        g.addEdge(8, 7); 
        g.addEdge(8, 9); 
        g.addEdge(9, 8); 
        g.addEdge(10, 11); 
        g.addEdge(11, 10); 

        g.BCC(); 

        System.out.println("Above are " + g.count + " biconnected components in graph"); 
    } 
} 
// This code is contributed by Aakash Hasija 

```

## Python

```py

# Python program to find biconnected components in a given 
# undirected graph 
# Complexity : O(V + E) 

from collections import defaultdict 

# This class represents an directed graph  
# using adjacency list representation 
class Graph: 

    def __init__(self, vertices): 
        # No. of vertices 
        self.V = vertices  

        # default dictionary to store graph 
        self.graph = defaultdict(list) 

        # time is used to find discovery times 
        self.Time = 0 

        # Count is number of biconnected components 
        self.count = 0 

    # function to add an edge to graph 
    def addEdge(self, u, v): 
        self.graph[u].append(v)  
         self.graph[v].append(u) 

    '''A recursive function that finds and prints strongly connected 
    components using DFS traversal 
    u --> The vertex to be visited next 
    disc[] --> Stores discovery times of visited vertices 
    low[] -- >> earliest visited vertex (the vertex with minimum 
               discovery time) that can be reached from subtree 
               rooted with current vertex 
    st -- >> To store visited edges'''
    def BCCUtil(self, u, parent, low, disc, st): 

        # Count of children in current node  
        children = 0

        # Initialize discovery time and low value 
        disc[u] = self.Time 
        low[u] = self.Time 
        self.Time += 1

        # Recur for all the vertices adjacent to this vertex 
        for v in self.graph[u]: 
            # If v is not visited yet, then make it a child of u 
            # in DFS tree and recur for it 
            if disc[v] == -1 : 
                parent[v] = u 
                children += 1
                st.append((u, v)) # store the edge in stack 
                self.BCCUtil(v, parent, low, disc, st) 

                # Check if the subtree rooted with v has a connection to 
                # one of the ancestors of u 
                # Case 1 -- per Strongly Connected Components Article 
                low[u] = min(low[u], low[v]) 

                # If u is an articulation point, pop  
                # all edges from stack till (u, v) 
                if parent[u] == -1 and children > 1 or parent[u] != -1 and low[v] >= disc[u]: 
                    self.count += 1 # increment count 
                    w = -1
                    while w != (u, v): 
                        w = st.pop() 
                        print w, 
                    print"" 

            elif v != parent[u] and low[u] > disc[v]: 
                '''Update low value of 'u' only of 'v' is still in stack 
                (i.e. it's a back edge, not cross edge). 
                Case 2  
                -- per Strongly Connected Components Article'''

                low[u] = min(low [u], disc[v]) 

                st.append((u, v)) 

    # The function to do DFS traversal.  
    # It uses recursive BCCUtil() 
    def BCC(self): 

        # Initialize disc and low, and parent arrays 
        disc = [-1] * (self.V) 
        low = [-1] * (self.V) 
        parent = [-1] * (self.V) 
        st = [] 

        # Call the recursive helper function to  
        # find articulation points 
        # in DFS tree rooted with vertex 'i' 
        for i in range(self.V): 
            if disc[i] == -1: 
                self.BCCUtil(i, parent, low, disc, st) 

            # If stack is not empty, pop all edges from stack 
            if st: 
                self.count = self.count + 1

                while st: 
                    w = st.pop() 
                    print w, 
                print "" 

# Create a graph given in the above diagram 

g = Graph(12) 
g.addEdge(0, 1) 
g.addEdge(1, 2) 
g.addEdge(1, 3) 
g.addEdge(2, 3) 
g.addEdge(2, 4) 
g.addEdge(3, 4) 
g.addEdge(1, 5) 
g.addEdge(0, 6) 
g.addEdge(5, 6) 
g.addEdge(5, 7) 
g.addEdge(5, 8) 
g.addEdge(7, 8) 
g.addEdge(8, 9) 
g.addEdge(10, 11) 

g.BCC(); 
print ("Above are % d biconnected components in graph" %(g.count)); 

# This code is contributed by Neelam Yadav 

```

## C#

```cs

// A C# program to find biconnected components in a given  
// undirected graph  
using System; 
using System.Collections.Generic; 

// This class represents a directed graph using adjacency  
// list representation  
public class Graph  
{  
    private int V, E; // No. of vertices & Edges respectively  
    private List<int> []adj; // Adjacency List  

    // Count is number of biconnected components. time is  
    // used to find discovery times  
    int count = 0, time = 0;  

    class Edge  
    {  
        public int u;  
        public int v;  
        public Edge(int u, int v)  
        {  
            this.u = u;  
            this.v = v;  
        }  
    };  

    // Constructor  
    public Graph(int v)  
    {  
        V = v;  
        E = 0;  
        adj = new List<int>[v];  
        for (int i = 0; i < v; ++i)  
            adj[i] = new List<int>();  
    }  

    // Function to add an edge into the graph  
    void addEdge(int v, int w)  
    {  
        adj[v].Add(w);  
        E++;  
    }  

    // A recursive function that finds and prints strongly connected  
    // components using DFS traversal  
    // u --> The vertex to be visited next  
    // disc[] --> Stores discovery times of visited vertices  
    // low[] -- >> earliest visited vertex (the vertex with minimum  
    // discovery time) that can be reached from subtree  
    // rooted with current vertex  
    // *st -- >> To store visited edges  
    void BCCUtil(int u, int []disc, int []low, List<Edge> st,  
                int []parent)  
    {  

        // Initialize discovery time and low value  
        disc[u] = low[u] = ++time;  
        int children = 0;  

        // Go through all vertices adjacent to this  
        foreach(int it in adj[u]) 
        {  
            int v = it; // v is current adjacent of 'u'  

            // If v is not visited yet, then recur for it  
            if (disc[v] == -1)  
            {  
                children++;  
                parent[v] = u;  

                // store the edge in stack  
                st.Add(new Edge(u, v));  
                BCCUtil(v, disc, low, st, parent);  

                // Check if the subtree rooted with 'v' has a  
                // connection to one of the ancestors of 'u'  
                // Case 1 -- per Strongly Connected Components Article  
                if (low[u] > low[v])  
                    low[u] = low[v];  

                // If u is an articulation point,  
                // pop all edges from stack till u -- v  
                if ((disc[u] == 1 && children > 1) ||  
                    (disc[u] > 1 && low[v] >= disc[u]))  
                {  
                    while (st[st.Count-1].u != u ||  
                           st[st.Count-1].v != v)  
                    {  
                        Console.Write(st[st.Count - 1].u + "--" +  
                                      st[st.Count - 1].v + " ");  
                        st.RemoveAt(st.Count - 1);  
                    }  
                    Console.WriteLine(st[st.Count - 1].u + "--" + 
                                       st[st.Count - 1].v + " ");  
                    st.RemoveAt(st.Count - 1);  

                    count++;  
                }  
            }  

            // Update low value of 'u' only if 'v' is still in stack  
            // (i.e. it's a back edge, not cross edge).  
            // Case 2 -- per Strongly Connected Components Article  
            else if (v != parent[u] && disc[v] < disc[u] )  
            {  
                if (low[u] > disc[v])  
                    low[u] = disc[v];  

                st.Add(new Edge(u, v));  
            }  
        }  
    }  

    // The function to do DFS traversal. It uses BCCUtil()  
    void BCC()  
    {  
        int []disc = new int[V];  
        int []low = new int[V];  
        int []parent = new int[V];  
        List<Edge> st = new List<Edge>();  

        // Initialize disc and low, and parent arrays  
        for (int i = 0; i < V; i++)  
        {  
            disc[i] = -1;  
            low[i] = -1;  
            parent[i] = -1;  
        }  

        for (int i = 0; i < V; i++) 
        {  
            if (disc[i] == -1)  
                BCCUtil(i, disc, low, st, parent);  

            int j = 0;  

            // If stack is not empty, pop all edges from stack  
            while (st.Count > 0)  
            {  
                j = 1;  
                Console.Write(st[st.Count - 1].u + "--" +  
                            st[st.Count - 1].v + " ");  
                st.RemoveAt(st.Count - 1);  
            }  
            if (j == 1)  
            {  
                Console.WriteLine();  
                count++;  
            }  
        }  
    }  

    // Driver code 
    public static void Main(String []args)  
    {  
        Graph g = new Graph(12);  
        g.addEdge(0, 1);  
        g.addEdge(1, 0);  
        g.addEdge(1, 2);  
        g.addEdge(2, 1);  
        g.addEdge(1, 3);  
        g.addEdge(3, 1);  
        g.addEdge(2, 3);  
        g.addEdge(3, 2);  
        g.addEdge(2, 4);  
        g.addEdge(4, 2);  
        g.addEdge(3, 4);  
        g.addEdge(4, 3);  
        g.addEdge(1, 5);  
        g.addEdge(5, 1);  
        g.addEdge(0, 6);  
        g.addEdge(6, 0);  
        g.addEdge(5, 6);  
        g.addEdge(6, 5);  
        g.addEdge(5, 7);  
        g.addEdge(7, 5);  
        g.addEdge(5, 8);  
        g.addEdge(8, 5);  
        g.addEdge(7, 8);  
        g.addEdge(8, 7);  
        g.addEdge(8, 9);  
        g.addEdge(9, 8);  
        g.addEdge(10, 11);  
        g.addEdge(11, 10);  

        g.BCC();  

        Console.WriteLine("Above are " + g.count + 
                        " biconnected components in graph");  
    }  
} 

// This code is contributed by PrinciRaj1992 

```

输出：

```
4--2 3--4 3--1 2--3 1--2
8--9
8--5 7--8 5--7
6--0 5--6 1--5 0--1 
10--11
Above are 5 biconnected components in graph

```

本文由 **Anurag Singh** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

