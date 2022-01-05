# 实现加博缩放算法的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-程序实现的 gabow-scaling-algorithm/](https://www.geeksforgeeks.org/java-program-to-implement-of-gabow-scaling-algorithm/)

加博算法是一种缩放算法，旨在通过最初仅考虑每个相关输入值的最高位(如边缘权重)来解决问题。然后，它通过查看两个最高位来细化初始解。它逐步查看越来越多的高阶位，在每次迭代中细化解，直到检查完所有位并计算出正确的解。

> 基本上，Gabow 的缩放算法是一种通过最初仅考虑每个输入值的最高位作为边缘权重来解决问题的缩放算法，然后它通过查看两个最高位来细化初始解，然后迭代地细化解，直到它访问了所有位(在图中)并计算出正确的解

**过程:**

1.  在中凯伊姆 *getSCComponents()* 拜占庭 conv *在*开头
    *   To name it. Initially, we used the list in java collection and
    *   To declare a graph, and then we apply [*DFS () method*](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)
2.  To find the strongly connected components. In the above methods, we have implemented a depth-first search method to consider every bit in the graph.
3.  In the main method, we take the number of vertices and edges, add them to the array list, and then print the getSCComponents () method to print out the strongly connected components of the given value in the figure.
4.  And print the output that does not represent the strongly connected components in the graph.

**算法:**

1.  仅使用权重的最高有效位的从 v0 到 v 的最小权重路径的权重是从 v0 到 v 的最小权重路径的权重的近似值。
2.  然后，递增地引入额外的权重位来改进我们对最小权重路径的近似。
3.  在每次迭代中，对于某些边(u，v)，我们将近似距离 u . dist-v . dist 的差值定义为跨(u，v)的电势。
4.  我们将边缘的成本定义为它在某次迭代中的精确权重加上它的潜力:
    *   li(u，v) = wi(u，v) + u 距离-v 距离。
5.  由于路径望远镜的总成本，这些成本保留了图中最小权重的路径。
6.  我们保证优势的成本总是非负的。
7.  我们可以在成本值图上反复寻找最小权重路径。

**示例:**

## Java

```
// Java Program to Implement Gabow Scaling Algorithm

// Importing input output classes
import java.io.*;
import java.util.*;

// Main Class
// Implementation of Gabow Scaling Algorithm
public class GFG {

    // Declaring variables

    // 1\. Number of vertices
    private int V;
    // 2\. Preorder number counter
    private int preCount;
    private int[] preorder;

    // 3\. To check if v is visited
    private boolean[] visited;

    // 4\. To check strong component containing v
    private boolean[] chk;

    // 5\. To store given graph
    private List<Integer>[] graph;

    // 6\. To store all Integer elements
    private List<List<Integer> > sccComp;
    private Stack<Integer> stack1;
    private Stack<Integer> stack2;

    // Method 1
    // To get all strongly connected components
    public List<List<Integer> >
        getSCComponents(List<Integer>[] graph)
    {
        V = graph.length;
        this.graph = graph;
        preorder = new int[V];
        chk = new boolean[V];
        visited = new boolean[V];
        stack1 = new Stack<Integer>();
        stack2 = new Stack<Integer>();
        sccComp = new ArrayList<>();

        for (int v = 0; v < V; v++)
            if (!visited[v])
                dfs(v);

        return sccComp;
    }

    // Method 2
    // Depth first search algorithm
    public void dfs(int v)
    {
        preorder[v] = preCount++;
        visited[v] = true;
        stack1.push(v);
        stack2.push(v);

        for (int w : graph[v]) {
            if (!visited[w])
                dfs(w);
            else if (!chk[w])
                while (preorder[stack2.peek()]
                       > preorder[w])
                    stack2.pop();
        }
        if (stack2.peek() == v) {
            stack2.pop();
            List<Integer> component
                = new ArrayList<Integer>();
            int w;
            do {
                w = stack1.pop();
                component.add(w);
                chk[w] = true;
            } while (w != v);
            sccComp.add(component);
        }
    }

    // Method 3
    // Main driver method
    public static void main(String[] args)
    {

        // Declaring and initializing variable to
        // number of vertices
        int V = 8;

        // Creating a graph
        @SuppressWarnings("unchecked")
        List<Integer>[] g = new List[V];
        for (int i = 0; i < V; i++)
            g[i] = new ArrayList<Integer>();

        // Accepting all edges
        int E = 14;

        // Custom integers inputs for all edges
        int[] x = new int[] { 0, 1, 2, 3, 3, 7, 2,
                              7, 5, 6, 1, 4, 4, 1 };
        int[] y = new int[] { 1, 2, 3, 2, 7, 3, 6,
                              6, 6, 5, 5, 5, 0, 4 };

        for (int i = 0; i < E; i++) {
            int x1 = x[i];
            int y1 = y[i];
            g[x1].add(y1);
        }

        // Creating an object of main class i the main()
        // method
        GFG gab = new GFG();

        // Display message only
        System.out.println(
            "\nStrongly Connected Components for given edges : ");

        // now, printing all the strongly connected
        // components
        List<List<Integer> > scComponents
            = gab.getSCComponents(g);
        System.out.println(scComponents);
    }
}
```

**输出**

```
Strongly Connected Components for give edges : 
[[5, 6], [7, 3, 2], [4, 1, 0]]
```