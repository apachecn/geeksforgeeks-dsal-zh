# 树上的扩展不交集集合并集

> 原文： [https://www.geeksforgeeks.org/extended-disjoint-set-union-on-trees/](https://www.geeksforgeeks.org/extended-disjoint-set-union-on-trees/)

**先决条件：** [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) ，[树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)， [DSU](https://www.geeksforgeeks.org/union-find/)

给定一棵树，其中有 **N** 个节点，从值 **1 到 N** 和 **E 个**边以及数组 **arr []** 表示与每个对象相关的数目 节点。 还向您提供 **Q** 查询，其中包含 2 个整数 **{V，F}** 。 对于每个查询，都有一个顶点为 **V** 的子树，任务是检查与该子树中每个节点关联的数字是否存在 **F** 。 如果是，则打印**是**，否则打印**是 False** 。

**示例：**

> **输入：** N = 8，E = {{1，2}，{1，3}，{2，4}，{2，5}，{5，8}，{5，6} ，{6，7}}，arr [] = {11，2，7，1，-3，-1，-1，-3}，Q = 3，查询[] = {{2，3}，{ 5，2}，{7，1}}
> **输出：**
> 假
> 是
> 是
> **说明：**
> 查询 1 ：在子树 2 中没有出现 3 次数字
> 查询 2：在子树 5 中出现了-1 和-3 2 次
> 查询 3：在子树 7 中出现了-1 次
> 
> **输入：** N = 11，E = {{1，2}，{1，3}，{2，4}，{2，5}，{4，9}，{4，8} ，{3，6}，{3，7}，{4，10}，{5，11}}，arr [] = {2，-1，-12，-1，6，14，7，-1 ，-2，13，12}，Q = 2，查询[] = {{2，2}，{4，2}}
> **输出：**
> 错误
> 是[
> **说明：**
> 查询 1：在子树 2 中没有正好出现 2 次数字
> 查询 2：子树 4 中-1 出现了两次

**天真的方法：**的想法是使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历遍历树，并计算与子树的每个顶点关联的数的频率 **V** 并存储 导致哈希图。 遍历后，我们只需要遍历哈希图以检查给定的频率数是否存在。

下面是上述方法的实现：

## 爪哇

```

// Java program for the above approach 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.Map; 

@SuppressWarnings("unchecked") 
public class Main { 

    // To store edges of tree 
    static ArrayList<Integer> adj[]; 

    // To store number associated 
    // with vertex 
    static int num[]; 

    // To store frequency of number 
    static HashMap<Integer, Integer> freq; 

    // Function to add edges in tree 
    static void add(int u, int v) 
    { 
        adj[u].add(v); 
        adj[v].add(u); 
    } 

    // Function returns boolean value 
    // representing is there any number 
    // present in subtree qv having 
    // frequency qc 
    static boolean query(int qv, int qc) 
    { 

        freq = new HashMap<>(); 

        // Start from root 
        int v = 1; 

        // DFS Call 
        if (qv == v) { 
            dfs(v, 0, true, qv); 
        } 
        else
            dfs(v, 0, false, qv); 

        // Check for frequency 
        for (int fq : freq.values()) { 
            if (fq == qc) 
                return true; 
        } 
        return false; 
    } 

    // Function to implement DFS 
    static void dfs(int v, int p, 
                    boolean isQV, int qv) 
    { 
        if (isQV) { 

            // If we are on subtree qv, 
            // then increment freq of 
            // num[v] in freq 
            freq.put(num[v], 
                     freq.getOrDefault(num[v], 0) + 1); 
        } 

        // Recursive DFS Call for 
        // adjacency list of node u 
        for (int u : adj[v]) { 
            if (p != u) { 
                if (qv == u) { 
                    dfs(u, v, true, qv); 
                } 
                else
                    dfs(u, v, isQV, qv); 
            } 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 

        // Given Nodes 
        int n = 8; 
        adj = new ArrayList[n + 1]; 
        for (int i = 1; i <= n; i++) 
            adj[i] = new ArrayList<>(); 

        // Given edges of tree 
        // (root=1) 
        add(1, 2); 
        add(1, 3); 
        add(2, 4); 
        add(2, 5); 
        add(5, 8); 
        add(5, 6); 
        add(6, 7); 

        // Number assigned to each vertex 
        num = new int[] { -1, 11, 2, 7, 1, -3, -1, -1, -3 }; 

        // Total number of queries 
        int q = 3; 

        // Function Call to find each query 
        System.out.println(query(2, 3)); 
        System.out.println(query(5, 2)); 
        System.out.println(query(7, 1)); 
    } 
} 

```

**Output:**

```
false
true
true

```

 ***时间复杂度：** *O（N * Q）*由于在每个查询中，都需要遍历树。
**辅助空间：** *O（N + E + Q）**

**有效方法：**的想法是对上述方法使用[扩展不相交集并集](https://www.geeksforgeeks.org/disjoint-set-data-structures/)：

1.  创建一个数组， **size []** 存储子树的大小。
2.  创建一个哈希图数组 **map []** ，即 map [V] [X] =子树 **V** 中总数为 **X** 的总顶点。
3.  通过调用 dfsSize（）使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历计算每个子树的大小。
4.  通过调用 dfs（V，p）使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历，计算 map [V]的值。
5.  在遍历中，要计算**映射[V]** ，请选择最大尺寸 **bigU** 除外的 **V** 的相邻顶点，除了父顶点 **p [** 。
6.  对于联接操作，将 map [bigU]的引用传递给 map [V]，即 **map [V] = map [bigU]** 。
7.  以及除父顶点 **p** 和 **bigU** 顶点之外的所有相邻顶点的[astn]合并图， **u** 至 **map [V]** 。
8.  现在，检查**映射[V]** 是否包含频率 F。 如果是，则打印**为真**，否则打印**为假**。

以下是有效方法的实现：

## 爪哇

```

// Java program for the above approach 
import java.awt.*; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.Map; 
import java.util.Map.Entry; 

@SuppressWarnings("unchecked") 
public class Main { 

    // To store edges 
    static ArrayList<Integer> adj[]; 

    // num[v] = number assigned 
    // to vertex v 
    static int num[]; 

    // map[v].get(c) = total vertices 
    // in subtree v having number c 
    static Map<Integer, Integer> map[]; 

    // size[v]=size of subtree v 
    static int size[]; 

    static HashMap<Point, Boolean> ans; 
    static ArrayList<Integer> qv[]; 

    // Function to add edges 
    static void add(int u, int v) 
    { 
        adj[u].add(v); 
        adj[v].add(u); 
    } 

    // Function to find subtree size 
    // of every vertex using dfsSize() 
    static void dfsSize(int v, int p) 
    { 
        size[v]++; 

        // Traverse dfsSize recursively 
        for (int u : adj[v]) { 
            if (p != u) { 
                dfsSize(u, v); 
                size[v] += size[u]; 
            } 
        } 
    } 

    // Function to implement DFS Traversal 
    static void dfs(int v, int p) 
    { 
        int mx = -1, bigU = -1; 

        // Find adjacent vertex with 
        // maximum size 
        for (int u : adj[v]) { 
            if (u != p) { 
                dfs(u, v); 
                if (size[u] > mx) { 
                    mx = size[u]; 
                    bigU = u; 
                } 
            } 
        } 

        if (bigU != -1) { 

            // Passing referencing 
            map[v] = map[bigU]; 
        } 
        else { 

            // If no adjacent vertex 
            // present initialize map[v] 
            map[v] = new HashMap<Integer, Integer>(); 
        } 

        // Update frequency of current number 
        map[v].put(num[v], 
                   map[v].getOrDefault(num[v], 0) + 1); 

        // Add all adjacent vertices 
        // maps to map[v] 
        for (int u : adj[v]) { 

            if (u != bigU && u != p) { 

                for (Entry<Integer, Integer> 
                         pair : map[u].entrySet()) { 
                    map[v].put( 
                        pair.getKey(), 
                        pair.getValue() 
                            + map[v] 
                                  .getOrDefault( 
                                      pair.getKey(), 0)); 
                } 
            } 
        } 

        // Store all queries related 
        // to vertex v 
        for (int freq : qv[v]) { 
            ans.put(new Point(v, freq), 
                    map[v].containsValue(freq)); 
        } 
    } 

    // Function to find answer for 
    // each queries 
    static void solveQuery(Point queries[], 
                           int N, int q) 
    { 
        // Add all queries to qv 
        // where i<qv[v].size() 
        qv = new ArrayList[N + 1]; 
        for (int i = 1; i <= N; i++) 
            qv[i] = new ArrayList<>(); 

        for (Point p : queries) { 
            qv[p.x].add(p.y); 
        } 

        // Get sizes of all subtrees 
        size = new int[N + 1]; 

        // calculate size[] 
        dfsSize(1, 0); 

        // Map will be used to store 
        // answers for current vertex 
        // on dfs 
        map = new HashMap[N + 1]; 

        // To store answer of queries 
        ans = new HashMap<>(); 

        // DFS Call 
        dfs(1, 0); 

        for (Point p : queries) { 

            // Print answer for each query 
            System.out.println(ans.get(p)); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int N = 8; 
        adj = new ArrayList[N + 1]; 
        for (int i = 1; i <= N; i++) 
            adj[i] = new ArrayList<>(); 

        // Given edges (root=1) 
        add(1, 2); 
        add(1, 3); 
        add(2, 4); 
        add(2, 5); 
        add(5, 8); 
        add(5, 6); 
        add(6, 7); 

        // Store number given to vertices 
        // set num[0]=-1 because 
        // there is no vertex 0 
        num 
            = new int[] { -1, 11, 2, 7, 1, 
                          -3, -1, -1, -3 }; 

        // Queries 
        int q = 3; 

        // To store queries 
        Point queries[] = new Point[q]; 

        // Given Queries 
        queries[0] = new Point(2, 3); 
        queries[1] = new Point(5, 2); 
        queries[2] = new Point(7, 1); 

        // Function Call 
        solveQuery(queries, N, q); 
    } 
} 

```