# 使用 Java 数组列表的图形表示

> 原文:[https://www . geesforgeks . org/graph-presentation-use-Java-ArrayList/](https://www.geeksforgeeks.org/graph-representation-using-java-arraylist/)

先决条件:[图形及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)

在本文中，我们将讨论在 Java 中使用数组列表来表示图的邻接表。

![](img/30e8ea189197ba821470a315e1901675.png "graph_representation1")

下面是上图的邻接表表示。

![Adjacency List Representation of Graph](img/367e2be9858f15556b5dc886d6fb46a6.png "adjacency_list_representation")

想法是使用数组列表的[数组列表。](https://www.geeksforgeeks.org/arraylist-of-arraylist-in-java/)

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

**使用单独的图形类的类似实现。**

**T3】**

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