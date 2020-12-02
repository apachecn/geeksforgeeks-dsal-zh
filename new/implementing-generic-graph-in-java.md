# 用 Java 实现通用图

> 原文： [https://www.geeksforgeeks.org/implementing-generic-graph-in-java/](https://www.geeksforgeeks.org/implementing-generic-graph-in-java/)

我们已经了解了 Java 中的[通用类](https://www.geeksforgeeks.org/generics-in-java/)。 我们还可以使用它们为 Java 中的[图进行编码。 Graph 类是使用 Java](https://www.geeksforgeeks.org/graph-and-its-representations/) 中的 [HashMap 实现的。 我们知道 HashMap 包含一个键和一个值，我们将节点表示为键，并在图中的值中表示其邻接表。](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)

**示例**：具有 5 个顶点的无向和无权图。
[![](img/30e8ea189197ba821470a315e1901675.png)](https://www.geeksforgeeks.org/graph-and-its-representations/)

**邻接矩阵**：
[![](img/bb131f35f3b5d91bbf0e21b108b63525.png)](https://www.geeksforgeeks.org/graph-and-its-representations/)

**邻接列表**：
[![](img/367e2be9858f15556b5dc886d6fb46a6.png)](https://www.geeksforgeeks.org/graph-and-its-representations/)

**方法**：
像 C ++一样，我们使用< >在通用类创建中指定参数类型。 为了创建通用类的对象，我们使用以下语法。

```
// To create an instance of generic class 
BaseType <Type> obj = new BaseType <Type>()

Note: In Parameter type, we cannot use primitives like 
      'int','char' or 'double'.

```

下面是上述方法的实现：

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

        // print the graph. 
        System.out.println("Graph:\n"
                           + g.toString()); 

        // gives the no of vertices in the graph. 
        g.getVertexCount(); 

        // gives the no of edges in the graph. 
        g.getEdgesCount(true); 

        // tells whether the edge is present or not. 
        g.hasEdge(3, 4); 

        // tells whether vertex is present or not 
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



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。