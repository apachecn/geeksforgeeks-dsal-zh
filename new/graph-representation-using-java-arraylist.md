# 使用 Java ArrayList

的图形表示

> 原文： [https://www.geeksforgeeks.org/graph-representation-using-java-arraylist/](https://www.geeksforgeeks.org/graph-representation-using-java-arraylist/)

先决条件：[图及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)

在本文中，我们将讨论使用 Java 中的 ArrayList 的 Graph 的邻接表表示。

![](img/30e8ea189197ba821470a315e1901675.png "graph_representation1")

以下是上图的邻接列表表示。

![Adjacency List Representation of Graph](img/367e2be9858f15556b5dc886d6fb46a6.png "adjacency_list_representation")

这个想法是使用 ArrayLists 的 [ArrayList。](https://www.geeksforgeeks.org/arraylist-of-arraylist-in-java/)

```

// Java code to demonstrate Graph representation 
// using ArrayList in Java 
import java.util.*; 

class Test { 

    static void addEdge(ArrayList<ArrayList<Integer> > adj, 
                        int u, int v) 
    { 
        adj.get(u).add(v); 
        adj.get(v).add(u); 
    } 

    static void printAdjacencyList(ArrayList<ArrayList<Integer> > adj) 
    { 
        for (int i = 0; i < adj.size(); i++) { 
            System.out.println("Adjacency list of " + i); 
            for (int j = 0; j < adj.get(i).size(); j++) { 
                System.out.print(adj.get(i).get(j) + " "); 
            } 
            System.out.println(); 
        } 
    } 

    public static void main(String[] args) 
    { 
        // Creating a graph with 5 vertices 
        int V = 5; 
        ArrayList<ArrayList<Integer> > adj = new ArrayList<ArrayList<Integer> >(V); 
        for (int i = 0; i < V; i++) 
            adj.add(new ArrayList<Integer>()); 

        // Adding edges one by one. 
        addEdge(adj, 0, 1); 
        addEdge(adj, 0, 4); 
        addEdge(adj, 1, 2); 
        addEdge(adj, 1, 3); 
        addEdge(adj, 1, 4); 
        addEdge(adj, 2, 3); 
        addEdge(adj, 3, 4); 
        printAdjacencyList(adj); 
    } 
}

```

**Output:**

```
Adjacency list of 0
1 4 
Adjacency list of 1
0 2 3 4 
Adjacency list of 2
1 3 
Adjacency list of 3
1 2 4 
Adjacency list of 4
0 1 3

```

 **使用单独的 Graph 类的类似实现。

```

// Java code to demonstrate Graph representation 
// using ArrayList in Java 
import java.util.*; 

class Graph { 
    ArrayList<ArrayList<Integer> > adj; 
    int V; 
    Graph(int v) 
    { 
        V = v; 
        adj = new ArrayList<ArrayList<Integer> >(V); 
        for (int i = 0; i < V; i++) 
            adj.add(new ArrayList<Integer>()); 
    } 

    void addEdge(int u, int v) 
    { 
        adj.get(u).add(v); 
        adj.get(v).add(u); 
    } 

    void printAdjacencyList() 
    { 
        for (int i = 0; i < adj.size(); i++) { 
            System.out.println("Adjacency list of " + i); 
            for (int j = 0; j < adj.get(i).size(); j++) { 
                System.out.print(adj.get(i).get(j) + " "); 
            } 
            System.out.println(); 
        } 
    } 
} 

class Test { 

    public static void main(String[] args) 
    { 
        // Creating a graph with 5 vertices 
        int V = 5; 

        Graph g = new Graph(V); 

        // Adding edges one by one. 
        g.addEdge(0, 1); 
        g.addEdge(0, 4); 
        g.addEdge(1, 2); 
        g.addEdge(1, 3); 
        g.addEdge(1, 4); 
        g.addEdge(2, 3); 
        g.addEdge(3, 4); 
        g.printAdjacencyList(); 
    } 
}

```

**Output:**

```
Adjacency list of 0
1 4 
Adjacency list of 1
0 2 3 4 
Adjacency list of 2
1 3 
Adjacency list of 3
1 2 4 
Adjacency list of 4
0 1 3

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。**