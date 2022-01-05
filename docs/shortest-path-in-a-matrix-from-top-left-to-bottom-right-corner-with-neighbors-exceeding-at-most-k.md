# 矩阵中从左上角到右下角的最短路径，邻居最多超过 K

> 原文:[https://www . geeksforgeeks . org/矩阵中最短路径从左上角到右下角-与邻居在一起-最多超过-k/](https://www.geeksforgeeks.org/shortest-path-in-a-matrix-from-top-left-to-bottom-right-corner-with-neighbors-exceeding-at-most-k/)

给定矩阵 **mat[][]** 和整数 **K，**的任务是在矩阵中从左上角到右下角找到[最短路径的长度，使得相邻节点之间的差异不超过 **K.**](https://www.geeksforgeeks.org/shortest-path-in-a-binary-maze/)

**示例:**

> **输入:**mat = {-1，0，4，3}，K = 4，src = {0，0}，dest = {2，3}
> { 6，5，7，8}，
> { 2，1，2，0}}
> **输出:** 7
> **解释:**相邻节点之间的差异不超过 K 的唯一最短路径是:-1 - > 0 - > 4 - > 7
> 
> **输入:**mat = {-1，0，4，3}、K = 5，src = {0，0}、dest = {2，3 }
> 【6，5，7，8}、
> 【2，1，2，0 })
> **输出:**

**方法:**给定的问题可以使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)来解决。这个想法是，如果相邻节点之间的差异超过 k，就停止探索路径。下面的步骤可以用来解决这个问题:

*   在源节点上应用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)，访问其值与当前节点值的绝对差值不大于 **K** 的邻居节点
*   布尔矩阵用于跟踪矩阵的访问单元
*   到达目的节点后，返回行进的距离。
*   如果无法到达目的节点，则返回-1

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;
class Node {
public:
    int dist, i, j, val;

    // Constructor
    Node(int x, int y, int d, int v)
    {
        i = x;
        j = y;
        dist = d;
        val = v;
    }
};

// Function to find the length of the
// shortest path with neighbor nodes
// value not exceeding K
int shortestPathLessThanK(vector<vector<int> > mat, int K,
                          int src[], int dest[])
{

    // Initialize a queue
    queue<Node*> q;

    // Add the source node
    // into the queue
    Node* Nw
        = new Node(src[0], src[1], 0, mat[src[0]][src[1]]);
    q.push(Nw);

    // Initialize rows and cols
    int N = mat.size(), M = mat[0].size();

    // Initialize a boolean matrix
    // to keep track of visisted cells
    bool visited[N][M];
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            visited[i][j] = false;
        }
    }

    // Initialize the directions
    int dir[4][2]
        = { { -1, 0 }, { 1, 0 }, { 0, 1 }, { 0, -1 } };

    // Apply BFS
    while (!q.empty()) {

        Node* curr = q.front();
        q.pop();

        // If cell is already visited
        if (visited[curr->i][curr->j])
            continue;

        // Mark current node as visited
        visited[curr->i][curr->j] = true;

        // Return the answer after
        // reaching the destination node
        if (curr->i == dest[0] && curr->j == dest[1])
            return curr->dist;

        // Explore neighbors
        for (int i = 0; i < 4; i++) {

            int x = dir[i][0] + curr->i,
                y = dir[i][1] + curr->j;

            // If out of bounds or already visited
            // or difference in neighbor nodes
            // values is greater than K
            if (x < 0 || y < 0 || x == N || y == M
                || visited[x][y]
                || abs(curr->val - mat[x][y]) > K)
                continue;

            // Add current cell into the queue
            Node* n
                = new Node(x, y, curr->dist + 1, mat[x][y]);
            q.push(n);
        }
    }

    // No path exists return -1
    return -1;
}

// Driver function
int main()
{

  // Initialize the matrix
    vector<vector<int> > mat = { { -1, 0, 4, 3 },
                                 { 6, 5, 7, 8 },
                                 { 2, 1, 2, 0 } };
    int K = 4;

    // Source node
    int src[] = { 0, 0 };

    // Destination node
    int dest[] = { 2, 3 };

    // Call the function
    // and print the answer
    cout << (shortestPathLessThanK(mat, K, src, dest));
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;
import java.lang.Math;

class GFG {

    static class Node {

        int dist, i, j, val;

        // Constructor
        public Node(int i, int j,
                    int dist, int val)
        {
            this.i = i;
            this.j = j;
            this.dist = dist;
            this.val = val;
        }
    }

    // Function to find the length of the
    // shortest path with neighbor nodes
    // value not exceeding K
    public static int shortestPathLessThanK(
        int[][] mat, int K, int[] src, int[] dest)
    {

        // Initialize a queue
        Queue<Node> q = new LinkedList<>();

        // Add the source node
        // into the queue
        q.add(new Node(src[0], src[1], 0,
                       mat[src[0]][src[1]]));

        // Initialize rows and cols
        int N = mat.length,
            M = mat[0].length;

        // Initialize a boolean matrix
        // to keep track of visisted cells
        boolean[][] visited = new boolean[N][M];

        // Initialize the directions
        int[][] dir = { { -1, 0 }, { 1, 0 },
                        { 0, 1 }, { 0, -1 } };

        // Apply BFS
        while (!q.isEmpty()) {

            Node curr = q.poll();

            // If cell is already visited
            if (visited[curr.i][curr.j])
                continue;

            // Mark current node as visited
            visited[curr.i][curr.j] = true;

            // Return the answer after
            // reaching the destination node
            if (curr.i == dest[0] && curr.j == dest[1])
                return curr.dist;

            // Explore neighbors
            for (int i = 0; i < 4; i++) {

                int x = dir[i][0] + curr.i,
                    y = dir[i][1] + curr.j;

                // If out of bounds or already visited
                // or difference in neighbor nodes
                // values is greater than K
                if (x < 0 || y < 0 || x == N
                    || y == M || visited[x][y]
                    || Math.abs(curr.val - mat[x][y]) > K)
                    continue;

                // Add current cell into the queue
                q.add(new Node(x, y, curr.dist + 1,
                               mat[x][y]));
            }
        }

        // No path exists return -1
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the matrix
        int[][] mat = { { -1, 0, 4, 3 },
                        { 6, 5, 7, 8 },
                        { 2, 1, 2, 0 } };
        int K = 4;

        // Source node
        int[] src = { 0, 0 };

        // Destination node
        int[] dest = { 2, 3 };

        // Call the function
        // and print the answer
        System.out.println(
            shortestPathLessThanK(mat, K, src, dest));
    }
}
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    class Node {

        public int dist, i, j, val;

        // Constructor
        public Node(int i, int j,
                    int dist, int val)
        {
            this.i = i;
            this.j = j;
            this.dist = dist;
            this.val = val;
        }
    }

    // Function to find the length of the
    // shortest path with neighbor nodes
    // value not exceeding K
    public static int shortestPathLessThanK(
        int[,] mat, int K, int[] src, int[] dest)
    {

        // Initialize a queue
        Queue<Node> q = new Queue<Node>();

        // Add the source node
        // into the queue
        q.Enqueue(new Node(src[0], src[1], 0,
                        mat[src[0],src[1]]));

        // Initialize rows and cols
        int N = mat.GetLength(0),
            M = mat.GetLength(1);

        // Initialize a bool matrix
        // to keep track of visisted cells
        bool[,] visited = new bool[N,M];

        // Initialize the directions
        int[,] dir = { { -1, 0 }, { 1, 0 },
                        { 0, 1 }, { 0, -1 } };

        // Apply BFS
        while (q.Count!=0) {

            Node curr = q.Peek();
            q.Dequeue();

            // If cell is already visited
            if (visited[curr.i,curr.j])
                continue;

            // Mark current node as visited
            visited[curr.i,curr.j] = true;

            // Return the answer after
            // reaching the destination node
            if (curr.i == dest[0] && curr.j == dest[1])
                return curr.dist;

            // Explore neighbors
            for (int i = 0; i < 4; i++) {

                int x = dir[i,0] + curr.i,
                    y = dir[i,1] + curr.j;

                // If out of bounds or already visited
                // or difference in neighbor nodes
                // values is greater than K
                if (x < 0 || y < 0 || x == N
                    || y == M || visited[x,y]
                    || Math.Abs(curr.val - mat[x,y]) > K)
                    continue;

                // Add current cell into the queue
                q.Enqueue(new Node(x, y, curr.dist + 1,
                               mat[x,y]));
            }
        }

        // No path exists return -1
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Initialize the matrix
        int[,] mat = { { -1, 0, 4, 3 },
                        { 6, 5, 7, 8 },
                        { 2, 1, 2, 0 } };
        int K = 4;

        // Source node
        int[] src = { 0, 0 };

        // Destination node
        int[] dest = { 2, 3 };

        // Call the function
        // and print the answer
        Console.WriteLine(
            shortestPathLessThanK(mat, K, src, dest));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code for the above approach
class Node {

  // Constructor
  constructor(x, y, d, v) {
    this.i = x;
    this.j = y;
    this.dist = d;
    this.val = v;
  }
};

// Function to find the length of the
// shortest path with neighbor nodes
// value not exceeding K
function shortestPathLessThanK(mat, K, src, dest) {

  // Initialize a queue
  let q = [];

  // Add the source node
  // into the queue
  let Nw = new Node(src[0], src[1], 0, mat[src[0]][src[1]]);
  q.unshift(Nw);

  // Initialize rows and cols
  let N = mat.length, M = mat[0].length;

  // Initialize a boolean matrix
  // to keep track of visisted cells
  let visited = new Array(N).fill(0).map(() => new Array(M).fill(0));
  for (let i = 0; i < N; i++) {
    for (let j = 0; j < M; j++) {
      visited[i][j] = false;
    }
  }

  // Initialize the directions
  let dir = [[-1, 0], [1, 0], [0, 1], [0, -1]];

  // Apply BFS
  while (q.length) {

    let curr = q[q.length - 1];
    q.pop();

    // If cell is already visited
    if (visited[curr.i][curr.j])
      continue;

    // Mark current node as visited
    visited[curr.i][curr.j] = true;

    // Return the answer after
    // reaching the destination node
    if (curr.i == dest[0] && curr.j == dest[1])
      return curr.dist;

    // Explore neighbors
    for (let i = 0; i < 4; i++) {

      let x = dir[i][0] + curr.i,
        y = dir[i][1] + curr.j;

      // If out of bounds or already visited
      // or difference in neighbor nodes
      // values is greater than K
      if (x < 0 || y < 0 || x == N || y == M
        || visited[x][y]
        || Math.abs(curr.val - mat[x][y]) > K)
        continue;

      // Add current cell into the queue
      let n
        = new Node(x, y, curr.dist + 1, mat[x][y]);
      q.unshift(n);
    }
  }

  // No path exists return -1
  return -1;
}

// Driver function

// Initialize the matrix
let mat = [[-1, 0, 4, 3], [6, 5, 7, 8], [2, 1, 2, 0]];
let K = 4;

// Source node
let src = [0, 0];

// Destination node
let dest = [2, 3];

// Call the function
// and print the answer
document.write(shortestPathLessThanK(mat, K, src, dest));

// This code is contributed by gfgking.
</script>
```

**Output**

```
7
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N * M)