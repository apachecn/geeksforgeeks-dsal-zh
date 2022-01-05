# 用 Java 实现类属图

> 原文:[https://www . geesforgeks . org/impering-generic-graph-in-Java/](https://www.geeksforgeeks.org/implementing-generic-graph-in-java/)

**先决条件:** [通用类](https://www.geeksforgeeks.org/generics-in-java/)

我们也可以用它们在 Java 中为[Graph](https://www.geeksforgeeks.org/graph-and-its-representations/)编码。图类是用 Java 中的[HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)实现的。正如我们所知，HashMap 包含一个键和值，我们将节点表示为图中值中的键和它们的邻接表。

**图解:**一个有 5 个顶点的无向未加权图。

![](img/30e8ea189197ba821470a315e1901675.png)

**邻接矩阵如下:**

![](img/bb131f35f3b5d91bbf0e21b108b63525.png)

**邻接表如下:**

![](img/367e2be9858f15556b5dc886d6fb46a6.png)

### 方法:

只是在 C++中不太可能，我们在泛型类创建中使用<>来指定参数类型。

**语法:**创建泛型类的对象

```
BaseType <Type> obj = new BaseType <Type>()
```

> **注意:**在参数类型中，我们不能使用像“int”、“char”或“double”这样的原语。

**例**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Graph
// with the help of Generics

import java.util.*;

class Graph<T> {

    // We use Hashmap to store the edges in the graph
    private Map<T, List<T> > map = new HashMap<>();

    // This function adds a new vertex to the graph
    public void addVertex(T s)
    {
        map.put(s, new LinkedList<T>());
    }

    // This function adds the edge
    // between source to destination
    public void addEdge(T source,
                        T destination,
                        boolean bidirectional)
    {

        if (!map.containsKey(source))
            addVertex(source);

        if (!map.containsKey(destination))
            addVertex(destination);

        map.get(source).add(destination);
        if (bidirectional == true) {
            map.get(destination).add(source);
        }
    }

    // This function gives the count of vertices
    public void getVertexCount()
    {
        System.out.println("The graph has "
                           + map.keySet().size()
                           + " vertex");
    }

    // This function gives the count of edges
    public void getEdgesCount(boolean bidirection)
    {
        int count = 0;
        for (T v : map.keySet()) {
            count += map.get(v).size();
        }
        if (bidirection == true) {
            count = count / 2;
        }
        System.out.println("The graph has "
                           + count
                           + " edges.");
    }

    // This function gives whether
    // a vertex is present or not.
    public void hasVertex(T s)
    {
        if (map.containsKey(s)) {
            System.out.println("The graph contains "
                               + s + " as a vertex.");
        }
        else {
            System.out.println("The graph does not contain "
                               + s + " as a vertex.");
        }
    }

    // This function gives whether an edge is present or not.
    public void hasEdge(T s, T d)
    {
        if (map.get(s).contains(d)) {
            System.out.println("The graph has an edge between "
                               + s + " and " + d + ".");
        }
        else {
            System.out.println("The graph has no edge between "
                               + s + " and " + d + ".");
        }
    }

    // Prints the adjancency list of each vertex.
    @Override
    public String toString()
    {
        StringBuilder builder = new StringBuilder();

        for (T v : map.keySet()) {
            builder.append(v.toString() + ": ");
            for (T w : map.get(v)) {
                builder.append(w.toString() + " ");
            }
            builder.append("\n");
        }

        return (builder.toString());
    }
}

// Driver Code
public class Main {

    public static void main(String args[])
    {

        // Object of graph is created.
        Graph<Integer> g = new Graph<Integer>();

        // edges are added.
        // Since the graph is bidirectional,
        // so boolean bidirectional is passed as true.
        g.addEdge(0, 1, true);
        g.addEdge(0, 4, true);
        g.addEdge(1, 2, true);
        g.addEdge(1, 3, true);
        g.addEdge(1, 4, true);
        g.addEdge(2, 3, true);
        g.addEdge(3, 4, true);

        // Printing the graph
        System.out.println("Graph:\n"
                           + g.toString());

        // Gives the no of vertices in the graph.
        g.getVertexCount();

        // Gives the no of edges in the graph.
        g.getEdgesCount(true);

        // Tells whether the edge is present or not.
        g.hasEdge(3, 4);

        // Tells whether vertex is present or not
        g.hasVertex(5);
    }
}
```

**Output:** 

```
Graph:
0: 1 4 
1: 0 2 3 4 
2: 1 3 
3: 1 2 4 
4: 0 1 3 

The graph has 5 vertex
The graph has 7 edges.
The graph has an edge between 3 and 4.
The graph does not contain 5 as a vertex.
```