# 从给定源到给定目的地的路径，在图中具有第 k 个最大权重

> 原文:[https://www . geesforgeks . org/路径-从给定源到给定目的地-具有-kth-最大图中权重/](https://www.geeksforgeeks.org/path-from-a-given-source-to-a-given-destination-having-kth-largest-weight-in-a-graph/)

给定一个由 **N** 节点和 **M** 边组成的[加权图](https://www.geeksforgeeks.org/graph-and-its-representations/)，一个**源**顶点，**目的地**顶点，以及一个整数 **K** ，任务是找到图中从**源**到**目的地**权重最大的路径。

**示例:**

> **输入:** N = 7，M = 8，源= 0，目的地= 6，K = 3，边[][] = {{0，1，10}，{1，2，10}，{2，3，10}，{0，3，40}，{3，4，2}，{4，5，3}，{5，6，3}，{4，6，8}，{2，5，5}}
> **输出:**0 1 2 3 4【6 重量= 38。
> 路径:0 - > 1 - > 2 - > 3 - > 6。重量= 40。
> 路径:0 - > 3 - > 4 - > 5 - > 6。重量= 48。
> 路径:0 - > 3 - > 4 - > 6。重量= 50。
> 3<sup>rd</sup>最大加权路径是权重为 40 的路径。因此，具有权重 40 的路径是输出。
> 
> **输入:** N = 2，M = 1，源= 0，目的地= 1，K = 1，边[][] = {{0 1 25}}，
> T3】输出: 0 1

**方法:**给定的问题可以通过[找到从给定源到目的地的所有路径](https://www.geeksforgeeks.org/find-paths-given-source-destination/)并使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)找到第 [K <sup>个最大的</sup>权重来解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)

*   [初始化邻接表，根据给定的](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)[边集**边[][]** 创建图形](https://www.geeksforgeeks.org/set-in-cpp-stl/)。
*   使用**优先级队列**初始化[最大堆](https://www.geeksforgeeks.org/binary-heap/)，比如说 **PQ** 作为大小为 **K** 的[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/)，以存储**路径权重**和**路径**作为从源到目的地的字符串。
*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **访问了[]** ，以标记一个顶点是否被访问。
*   遍历图到[找到从源到目的地](https://www.geeksforgeeks.org/find-paths-given-source-destination/)的所有路径。
*   创建一个实用类 Pair 作为 **psf** 和 **wsf** ，分别用于维护到目前为止获得的路径和权重。
*   在优先级队列中，执行以下操作:
    *   如果[队列](https://www.geeksforgeeks.org/queue-data-structure/)的元素少于 **K** 元素，[将该对添加到队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)中。
    *   否则，如果路径的当前权重大于队列前面的对的权重，则[移除前面的元素](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)，将新的对添加到队列中。
*   完成上述步骤后，优先级队列顶端的元素给出包含 **K <sup>第</sup>T5【最大权重路径】的对。因此，打印该路径。**

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

// Edge class represents a source,
// destination, weight of the edge
class Edge {

    // Source
    int src;

    // Destination
    int nbr;

    // Weight
    int wt;

    // Constructor to create an Edge
    Edge(int src, int nbr, int wt)
    {
        this.src = src;
        this.nbr = nbr;
        this.wt = wt;
    }
}

// Pair class
class Pair implements Comparable<Pair> {

    // Weight so far
    int wsf;

    // Path so far
    String psf;

    // Constructor to create a Pair
    Pair(int wsf, String psf)
    {
        this.wsf = wsf;
        this.psf = psf;
    }

    // Function to sort in increasing
    // order of weights
    public int compareTo(Pair o)
    {
        return this.wsf - o.wsf;
    }
}

class GFG {

    // Initializing the priority queue
    static PriorityQueue<Pair> pq
        = new PriorityQueue<>();

    // Function to find the path from src to
    // dest with Kth largest weight in the graph
    public static void kthLargest(
        ArrayList<Edge>[] graph,
        int src, int dest,
        boolean[] visited, int k,
        String psf, int wsf)
    {
        // Base Case: When the
        // destination has been reached
        if (src == dest) {

            // If pq has at most K elements
            if (pq.size() < k) {
                pq.add(new Pair(wsf, psf));
            }

            else if (wsf > pq.peek().wsf) {
                pq.remove();
                pq.add(new Pair(wsf, psf));
            }

            return;
        }

        // Mark the source node as visited
        visited[src] = true;

        // Iterating over all
        // the neighbours of src
        for (Edge e : graph[src]) {

            // If neighbour is not visited
            if (!visited[e.nbr]) {

                kthLargest(graph, e.nbr,
                           dest, visited,
                           k, psf + e.nbr,
                           wsf + e.wt);
            }
        }

        // Mark src as unvisited
        visited[src] = false;
    }

    // Function to add edges
    public static void addEdges(
        ArrayList<Edge>[] graph)
    {
        // Adding a bidirectional edge
        graph[0].add(new Edge(0, 1, 10));
        graph[1].add(new Edge(1, 0, 10));

        graph[1].add(new Edge(1, 2, 10));
        graph[2].add(new Edge(2, 1, 10));

        graph[2].add(new Edge(2, 3, 10));
        graph[3].add(new Edge(3, 2, 10));

        graph[0].add(new Edge(0, 3, 40));
        graph[3].add(new Edge(3, 0, 40));

        graph[3].add(new Edge(3, 4, 2));
        graph[4].add(new Edge(4, 3, 2));

        graph[4].add(new Edge(4, 5, 3));
        graph[5].add(new Edge(5, 4, 3));

        graph[5].add(new Edge(5, 6, 3));
        graph[6].add(new Edge(6, 5, 3));

        graph[4].add(new Edge(4, 6, 8));
        graph[6].add(new Edge(6, 4, 8));
    }

    // Utility function to find the
    // path with Kth largest weight
    public static void kthLargestPathUtil(
        int N, int M, int src,
        int dest, int k)
    {
        @SuppressWarnings("unchecked")

        // Arraylist to store edges
        ArrayList<Edge>[] graph
            = new ArrayList[2 * N];

        for (int i = 0; i < 2 * N; i++) {
            graph[i] = new ArrayList<>();
        }

        // Function to add edges
        addEdges(graph);

        // Stores if a vertex is visited or not
        boolean[] visited = new boolean[N];

        kthLargest(graph, src, dest,
                   visited, k, src + "",
                   0);

        // Stores the kth largest weighted path
        String path = pq.peek().psf;

        // Traversing path string
        for (int i = 0;
             i < path.length(); i++) {
            System.out.print(
                path.charAt(i) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // No of vertices and Edges
        int N = 7, M = 8;

        // Source vertex
        int src = 0;

        // Destination vertex
        int dest = 6;
        int k = 3;

        kthLargestPathUtil(N, M, src,
                           dest, k);
    }
}
```

***时间复杂度:** O(V + E)*
***辅助空间:** O(V)*