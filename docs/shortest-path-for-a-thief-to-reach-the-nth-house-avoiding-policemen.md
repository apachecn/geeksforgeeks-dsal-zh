# 小偷躲避警察到达第 n 栋房屋的最短路径

> 原文:[https://www . geesforgeks . org/小偷到达第 n 个避屋警察的最短路径/](https://www.geeksforgeeks.org/shortest-path-for-a-thief-to-reach-the-nth-house-avoiding-policemen/)

给定一个[未加权图](https://www.geeksforgeeks.org/shortest-path-unweighted-graph/)和一个布尔[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[ ]** ，其中如果数组 **A[ ]** 的第 **i <sup>第</sup>T9】索引表示该节点是否可以被访问(*0*)(*1*)。任务是从**0**<sup>节点找到到达**(N–1)**<sup>第</sup>节点的最短路径。如果无法到达，打印 **-1** 。</sup>**

**示例:**

> **输入:** N = 5，A[] = {0，1，0，0，0}，Edges = {{0，1}，{0，2}，{1，4}，{2，3}，{3，4 } }
> T3】输出:3
> T6】说明:从 0 <sup>第</sup>栋到 4 <sup>第</sup>栋有两条路径
> 
> *   0 → 1 → 4
> *   0 →2 → 3 → 4
> 
> 因为有警察在第一<sup>家</sup>家，唯一可以选择的路就是第二条路。
> 
> **输入:** N = 4，A = {0，1，1，0}，边= {{0，1}，{0，2}，{1，3}，{2，3}}
> **输出:** -1

**方法:**这个问题类似于[在未加权图](https://www.geeksforgeeks.org/shortest-path-unweighted-graph/)中寻找最短路径。因此，使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 可以解决问题。

按照以下步骤解决问题:

*   初始化一个[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)，说**调整**来存储边。如果在节点 **a** 或节点 **b** 有警察，则必须排除边缘 **(a，b)** 。
*   初始化一个变量，**路径长度= 0。**
*   初始化[布尔数据类型](https://www.geeksforgeeks.org/bool-data-type-in-c/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**访问了**，以存储节点是否被访问。
*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)距离【0，1，…。，v-1]使得**距离【I】**存储顶点 **i** 到根顶点的距离
*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，并在其中推送节点 **0** 。此外，将节点 **0** 标记为已访问。
*   当[队列不为空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)且节点**N–1**未被访问时进行迭代，从队列中弹出[前元素，将所有从队列](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)的[前元素有边且未被访问的元素推入队列中，并将所有这些节点的距离增加 **1 + dist[q.top()]** 。](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)
*   如果节点**(N–1)**未被访问，则打印 **-1** 。
*   否则，打印**(N–1)**<sup>第</sup>节点到根节点的距离。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to create graph edges
// where node A and B can be visited
void createGraph(unordered_map<int, vector<int> >& adj,
                 int paths[][2], int A[], int N, int E)
{
    // Visit all the connections
    for (int i = 0; i < E; i++) {

        // If a policeman is at any point of
        // connection, leave that connection.
        // Insert the connect otherwise.
        if (!A[paths[i][0]] && !A[paths[i][1]]) {

            adj[paths[i][0]].push_back(paths[i][1]);
        }
    }
}

// Function to find the shortest path
int minPath(int paths[][2], int A[],
            int N, int E)
{
    // If police is at either at
    // the 1-st house or at N-th house
    if (A[0] == 1 || A[N - 1] == 1)

        // The thief cannot reach
        // the N-th house
        return -1;

    // Stores Edges of graph
    unordered_map<int, vector<int> > adj;

    // Function call to store connections
    createGraph(adj, paths, A, N, E);

    // Stores wheather node is
    // visited or not
    vector<int> visited(N, 0);

    // Stores distances
    // from the root node
    int dist[N];
    dist[0] = 0;

    queue<int> q;
    q.push(0);
    visited[0] = 1;

    // Visit all nodes that are
    // currently in the queue
    while (!q.empty()) {

        int temp = q.front();
        q.pop();

        for (auto x : adj[temp]) {

            // If current node is
            // not visited already
            if (!visited[x]) {

                q.push(x);
                visited[x] = 1;
                dist[x] = dist[temp] + 1;
            }
        }
    }

    if (!visited[N - 1])
        return -1;
    else
        return dist[N - 1];
}

// Driver Code
int main()
{
    // N : Number of houses
    // E: Number of edges
    int N = 5, E = 5;

    // Given positions
    int A[] = { 0, 1, 0, 0, 0 };

    // Given Paths
    int paths[][2] = { { 0, 1 },
                       { 0, 2 },
                       { 1, 4 },
                       { 2, 3 },
                       { 3, 4 } };

    // Function call
    cout << minPath(paths, A, N, E);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to create graph edges
    // where node A and B can be visited
    static void
    createGraph(HashMap<Integer, ArrayList<Integer> > adj,
                int paths[][], int A[], int N, int E)
    {
        // Visit all the connections
        for (int i = 0; i < E; i++) {

            // If a policeman is at any point of
            // connection, leave that connection.
            // Insert the connect otherwise.
            if (A[paths[i][0]] != 1
                && A[paths[i][1]] != 1) {
                ArrayList<Integer> list = adj.getOrDefault(
                    paths[i][0], new ArrayList<>());
                list.add(paths[i][1]);
                adj.put(paths[i][0], list);
            }
        }
    }

    // Function to find the shortest path
    static int minPath(int paths[][], int A[], int N, int E)
    {
        // If police is at either at
        // the 1-st house or at N-th house
        if (A[0] == 1 || A[N - 1] == 1)

            // The thief cannot reach
            // the N-th house
            return -1;

        // Stores Edges of graph
        HashMap<Integer, ArrayList<Integer> > adj
            = new HashMap<>();

        // Function call to store connections
        createGraph(adj, paths, A, N, E);

        // Stores wheather node is
        // visited or not
        boolean visited[] = new boolean[N];

        // Stores distances
        // from the root node
        int dist[] = new int[N];
        dist[0] = 0;

        ArrayDeque<Integer> q = new ArrayDeque<>();
        q.addLast(0);
        visited[0] = true;

        // Visit all nodes that are
        // currently in the queue
        while (!q.isEmpty()) {

            int temp = q.removeFirst();

            for (int x : adj.getOrDefault(
                     temp, new ArrayList<>())) {

                // If current node is
                // not visited already
                if (!visited[x]) {

                    q.addLast(x);
                    visited[x] = true;
                    dist[x] = dist[temp] + 1;
                }
            }
        }

        if (!visited[N - 1])
            return -1;
        else
            return dist[N - 1];
    }

    // Driver Code
    public static void main(String[] args)
    {

        // N : Number of houses
        // E: Number of edges
        int N = 5, E = 5;

        // Given positions
        int A[] = { 0, 1, 0, 0, 0 };

        // Given Paths
        int paths[][] = {
            { 0, 1 }, { 0, 2 }, { 1, 4 }, { 2, 3 }, { 3, 4 }
        };

        // Function call
        System.out.print(minPath(paths, A, N, E));
    }
}

// This code is contributed by Kingash.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

 // Stores Edges of graph
 var adj = new Map();

// Function to create graph edges
// where node A and B can be visited
function createGraph(paths, A, N, E)
{
    // Visit all the connections
    for (var i = 0; i < E; i++) {

        // If a policeman is at any point of
        // connection, leave that connection.
        // Insert the connect otherwise.
        if (!A[paths[i][0]] && !A[paths[i][1]]) {

            if(adj.has(paths[i][0]))
            {
                var tmp = adj.get(paths[i][0]);
                tmp.push(paths[i][1]);
                adj.set(paths[i][0], tmp);
            }
            else
            {
                var tmp = new Array();
                tmp.push(paths[i][1]);
                adj.set(paths[i][0], tmp);
            }
        }
    }
}

// Function to find the shortest path
function minPath(paths, A, N, E)
{
    // If police is at either at
    // the 1-st house or at N-th house
    if (A[0] == 1 || A[N - 1] == 1)

        // The thief cannot reach
        // the N-th house
        return -1;

    // Function call to store connections
    createGraph(paths, A, N, E);

    // Stores wheather node is
    // visited or not
    var visited = Array(N).fill(0);

    // Stores distances
    // from the root node
    var dist = Array(N).fill(0);
    dist[0] = 0;

    var q = [];
    q.push(0);
    visited[0] = 1;

    // Visit all nodes that are
    // currently in the queue
    while (q.length!=0) {

        var temp = q[0];
        q.pop();

        if(adj.has(temp))
        {
        for (var x of adj.get(temp)) {

            // If current node is
            // not visited already
            if (!visited[x]) {

                q.push(x);
                visited[x] = 1;
                dist[x] = dist[temp] + 1;
            }
        }
    }
    }

    if (!visited[N - 1])
        return -1;
    else
        return dist[N - 1];
}

// Driver Code
// N : Number of houses
// E: Number of edges
var N = 5, E = 5;

// Given positions
var A = [0, 1, 0, 0, 0 ];

// Given Paths
var paths = [ [ 0, 1 ],
                   [ 0, 2 ],
                   [ 1, 4 ],
                   [ 2, 3 ],
                   [ 3, 4 ] ];
// Function call
document.write(minPath(paths, A, N, E));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N+E)
T3】辅助空间: O (N + E)