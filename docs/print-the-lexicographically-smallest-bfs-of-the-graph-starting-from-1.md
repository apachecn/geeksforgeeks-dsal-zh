# 从 1

开始打印图表的字典最小 BFS

> 原文:[https://www . geeksforgeeks . org/print-the-the-字典最小-bfs-of-graph-from-1/](https://www.geeksforgeeks.org/print-the-lexicographically-smallest-bfs-of-the-graph-starting-from-1/)

给定一个有 **N** 个顶点和 **M** 条边的连通图。任务是打印从 1 开始的字典上最小的图的 BFS 遍历。
**注**:顶点从 1 到 n 编号
**例:**

```
Input: N = 5, M = 5 
       Edges: 
       1 4
       3 4
       5 4
       3 2
       1 5 
Output: 1 4 3 2 5 
Start from 1, go to 4, then to 3 and then to 2 and to 5\. 

Input: N = 3, M = 2 
       Edges: 
       1 2 
       1 3 
Output: 1 2 3 
```

**方法:**我们可以使用优先级队列(最小堆)代替简单的队列，而不是在图上进行正常的 BFS 遍历。当节点被访问时，将其相邻节点添加到优先级队列中。每次，我们访问一个新节点，它将是优先级队列中索引最小的节点。当我们每次从 1 开始访问节点时，打印节点。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print the lexcicographically
// smallest path starting from 1

#include <bits/stdc++.h>
using namespace std;

// Function to print the smallest lexicographically
// BFS path starting from 1
void printLexoSmall(vector<int> adj[], int n)
{
    // Visited array
    bool vis[n + 1];
    memset(vis, 0, sizeof vis);

    // Minimum Heap
    priority_queue<int, vector<int>, greater<int> > Q;

    // First one visited
    vis[1] = true;
    Q.push(1);

    // Iterate till all nodes are visited
    while (!Q.empty()) {

        // Get the top element
        int now = Q.top();

        // Pop the element
        Q.pop();

        // Print the current node
        cout << now << " ";

        // Find adjacent nodes
        for (auto p : adj[now]) {

            // If not visited
            if (!vis[p]) {

                // Push
                Q.push(p);

                // Mark as visited
                vis[p] = true;
            }
        }
    }
}

// Function to insert edges in the graph
void insertEdges(int u, int v, vector<int> adj[])
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Driver Code
int main()
{
    int n = 5, m = 5;
    vector<int> adj[n + 1];

    // Insert edges
    insertEdges(1, 4, adj);
    insertEdges(3, 4, adj);
    insertEdges(5, 4, adj);
    insertEdges(3, 2, adj);
    insertEdges(1, 5, adj);

    // Function call
    printLexoSmall(adj, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the lexcicographically
// smallest path starting from 1
import java.util.*;
public class GFG
{

  // Function to print the smallest lexicographically
  // BFS path starting from 1
  static void printLexoSmall(Vector<Vector<Integer>> adj, int n)
  {
    // Visited array
    boolean[] vis = new boolean[n + 1];

    // Minimum Heap
    Vector<Integer> Q = new Vector<Integer>();

    // First one visited
    vis[1] = true;
    Q.add(1);

    // Iterate till all nodes are visited
    while (Q.size() > 0) {

      // Get the top element
      int now = Q.get(0);

      // Pop the element
      Q.remove(0);

      // Print the current node
      System.out.print(now + " ");

      // Find adjacent nodes
      for(int p : adj.get(now)) {

        // If not visited
        if (!vis[p]) {

          // Push
          Q.add(p);
          Collections.sort(Q);

          // Mark as visited
          vis[p] = true;
        }
      }
    }
  }

  // Function to insert edges in the graph
  static void insertEdges(int u, int v, Vector<Vector<Integer>> adj)
  {
    adj.get(u).add(v);
    adj.get(v).add(u);
  }

  // Driver code
  public static void main(String[] args) {
    int n = 5;
    Vector<Vector<Integer>> adj = new Vector<Vector<Integer>>();    
    for(int i = 0; i < n + 1; i++)
    {
      adj.add(new Vector<Integer>());
    }

    // Insert edges
    insertEdges(1, 4, adj);
    insertEdges(3, 4, adj);
    insertEdges(5, 4, adj);
    insertEdges(3, 2, adj);
    insertEdges(1, 5, adj);

    // Function call
    printLexoSmall(adj, n);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python program to print the lexcicographically
# smallest path starting from 1

# Function to print the smallest lexicographically
# BFS path starting from 1
def printLexoSmall(adj, n):

    # Visited array
    vis = [False for i in range(n + 1)]

    # Minimum Heap
    Q = []

    # First one visited
    vis[1] = True;
    Q.append(1)

    # Iterate till all nodes are visited
    while(len(Q) != 0):

        # Get the top element
        now = Q[0]

        # Pop the element
        Q.pop(0)

        # Print the current node
        print(now, end = " ")

        # Find adjacent nodes
        for p in adj[now]:

            # If not visited
            if(not vis[p]):

                # Push
                Q.append(p)
                Q.sort()

                # Mark as visited
                vis[p] = True

# Function to insert edges in the graph
def insertEdges(u, v, adj):
    adj[u].append(v)
    adj[v].append(u)

# Driver code
n = 5
m = 5
adj = [[] for i in range(n + 1)]

# Insert edges
insertEdges(1, 4, adj)
insertEdges(3, 4, adj)
insertEdges(5, 4, adj)
insertEdges(3, 2, adj)
insertEdges(1, 5, adj)

# Function call
printLexoSmall(adj, n)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to print the lexcicographically
// smallest path starting from 1
using System;
using System.Collections.Generic;
class GFG {

    // Function to print the smallest lexicographically
    // BFS path starting from 1
    static void printLexoSmall(List<List<int>> adj, int n)
    {
        // Visited array
        bool[] vis = new bool[n + 1];

        // Minimum Heap
        List<int> Q = new List<int>();

        // First one visited
        vis[1] = true;
        Q.Add(1);

        // Iterate till all nodes are visited
        while (Q.Count > 0) {

            // Get the top element
            int now = Q[0];

            // Pop the element
            Q.RemoveAt(0);

            // Print the current node
            Console.Write(now + " ");

            // Find adjacent nodes
            foreach (int p in adj[now]) {

                // If not visited
                if (!vis[p]) {

                    // Push
                    Q.Add(p);
                    Q.Sort();

                    // Mark as visited
                    vis[p] = true;
                }
            }
        }
    }

    // Function to insert edges in the graph
    static void insertEdges(int u, int v, List<List<int>> adj)
    {
        adj[u].Add(v);
        adj[v].Add(u);
    }

  // Driver code
  static void Main()
  {
    int n = 5;
    List<List<int>> adj = new List<List<int>>();    
    for(int i = 0; i < n + 1; i++)
    {
        adj.Add(new List<int>());
    }

    // Insert edges
    insertEdges(1, 4, adj);
    insertEdges(3, 4, adj);
    insertEdges(5, 4, adj);
    insertEdges(3, 2, adj);
    insertEdges(1, 5, adj);

    // Function call
    printLexoSmall(adj, n);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// JavaScript program to print the lexcicographically
// smallest path starting from 1

// Function to print the smallest lexicographically
  // BFS path starting from 1
function printLexoSmall(adj,n)
{
    // Visited array
    let vis = new Array(n + 1);
     for(let i=0;i<n+1;i++)
    {
        vis[i]=false;
    }
    // Minimum Heap
    let Q = [];

    // First one visited
    vis[1] = true;
    Q.push(1);

    // Iterate till all nodes are visited
    while (Q.length > 0) {

      // Get the top element
      let now = Q[0];

      // Pop the element
      Q.shift();

      // Print the current node
      document.write(now + " ");

      // Find adjacent nodes
      for(let p=0;p< adj[now].length;p++) {

        // If not visited
        if (!vis[adj[now][p]]) {

          // Push
          Q.push(adj[now][p]);
          Q.sort(function(a,b){return a-b;});

          // Mark as visited
          vis[adj[now][p]] = true;
        }
      }
    }
}

// Function to insert edges in the graph
function insertEdges(u,v,adj)
{
    adj[u].push(v);
    adj[v].push(u);
}

n = 5;
let adj = [];
for(let i = 0; i < n + 1; i++)
{
    adj.push([]);
}

// Insert edges
insertEdges(1, 4, adj);
insertEdges(3, 4, adj);
insertEdges(5, 4, adj);
insertEdges(3, 2, adj);
insertEdges(1, 5, adj);

// Function call
printLexoSmall(adj, n);

// This code is contributed by ab2127

</script>
```

**Output:** 

```
1 4 3 2 5
```