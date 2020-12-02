# 最大程度的生成树（使用 Kruskal 算法）

> 原文： [https://www.geeksforgeeks.org/spanning-tree-with-maximum-degree-using-kruskals-algorithm/](https://www.geeksforgeeks.org/spanning-tree-with-maximum-degree-using-kruskals-algorithm/)

给定由`n`个顶点和`m`边组成的无向非加权连通图。 任务是找到此图的任何生成树，以使所有顶点上的最大度数最大可能。 打印输出边的顺序无关紧要，边也可以反面打印，即（u，v）也可以打印为（v，u）。

**示例**：

```
Input:
        1
       / \
      2   5
       \ /
        3
        |
        4
Output:
3 2
3 5
3 4
1 2
The maximum degree over all vertices 
is of vertex 3 which is 3 and is 
maximum possible.

Input:
        1
       /
      2 
     / \ 
    5   3
        |
        4
Output:
2 1
2 5
2 3
3 4

```

**先决条件**：[Kruskal 算法来查找最小生成树](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)

**方法**：可以使用 Kruskal 算法找到最小生成树来解决给定的问题。
我们在图中找到了度数最大的顶点。 首先，我们将执行与该顶点有关的所有边的合并，然后执行普通的 Kruskal 算法。 这为我们提供了最佳的生成树。

## 爪哇

```

// Java implementation of the approach 
import java.util.*; 
public class GFG { 

    // par and rank will store the parent 
    // and rank of particular node 
    // in the Union Find Algorithm 
    static int par[], rank[]; 

    // Find function of Union Find Algorithm 
    static int find(int x) 
    { 
        if (par[x] != x) 
            par[x] = find(par[x]); 
        return par[x]; 
    } 

    // Union function of Union Find Algorithm 
    static void union(int u, int v) 
    { 
        int x = find(u); 
        int y = find(v); 
        if (x == y) 
            return; 
        if (rank[x] > rank[y]) 
            par[y] = x; 
        else if (rank[x] < rank[y]) 
            par[x] = y; 
        else { 
            par[x] = y; 
            rank[y]++; 
        } 
    } 

    // Function to find the required spanning tree 
    static void findSpanningTree(int deg[], int n, 
                                 int m, ArrayList<Integer> g[]) 
    { 
        par = new int[n + 1]; 
        rank = new int[n + 1]; 

        // Initialising parent of a node 
        // by itself 
        for (int i = 1; i <= n; i++) 
            par[i] = i; 

        // Variable to store the node 
        // with maximum degree 
        int max = 1; 

        // Finding the node with maximum degree 
        for (int i = 2; i <= n; i++) 
            if (deg[i] > deg[max]) 
                max = i; 

        // Union of all edges incident 
        // on vertex with maximum degree 
        for (int v : g[max]) { 
            System.out.println(max + " " + v); 
            union(max, v); 
        } 

        // Carrying out normal Kruskal Algorithm 
        for (int u = 1; u <= n; u++) { 
            for (int v : g[u]) { 
                int x = find(u); 
                int y = find(v); 
                if (x == y) 
                    continue; 
                union(x, y); 
                System.out.println(u + " " + v); 
            } 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // Number of nodes 
        int n = 5; 

        // Number of edges 
        int m = 5; 

        // ArrayList to store the graph 
        ArrayList<Integer> g[] = new ArrayList[n + 1]; 
        for (int i = 1; i <= n; i++) 
            g[i] = new ArrayList<>(); 

        // Array to store the degree 
        // of each node in the graph 
        int deg[] = new int[n + 1]; 

        // Add edges and update degrees 
        g[1].add(2); 
        g[2].add(1); 
        deg[1]++; 
        deg[2]++; 
        g[1].add(5); 
        g[5].add(1); 
        deg[1]++; 
        deg[5]++; 
        g[2].add(3); 
        g[3].add(2); 
        deg[2]++; 
        deg[3]++; 
        g[5].add(3); 
        g[3].add(5); 
        deg[3]++; 
        deg[5]++; 
        g[3].add(4); 
        g[4].add(3); 
        deg[3]++; 
        deg[4]++; 

        findSpanningTree(deg, n, m, g); 
    } 
} 

```