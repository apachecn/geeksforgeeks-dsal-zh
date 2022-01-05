# 为边分配权重，使得最长路径的权重最小

> 原文:[https://www . geeksforgeeks . org/将权重分配给边，使得最长路径的权重最小化/](https://www.geeksforgeeks.org/assign-weights-to-edges-such-that-longest-path-in-terms-of-weights-is-minimized/)

给定一棵树的边和一个和 S。任务是给树的所有边分配权重，使得最长路径的权重最小，分配的权重总和应为 S，并打印最长路径的权重。
**注意:**边可以被赋予[0，S]范围内的任意权重，也可以是分数。
**示例:**

```
Input:      1
      /     |     \
     2      3      4
S = 3
Output: 2
All the edges can be assigned weights of 1, so 
the longest path will in terms of weight will be 
2--1--4 or 2--1--3 

Input:        1
            /
           2
        /      \ 
       3        4 
              /   \ 
            5      6 
S = 1 
Output: 0.50 
Assign the given below weights to edges. 
1--2: 0.25 
2--3: 0.25 
2--4: 0 
4--5: 0.25 
4--6: 0.25 

Hence the longest path in terms of weight is 1--2--3 
or 1--2--4--5 or 1--2--4--6\. 
```

**方法:**一个路径最多可以有两个叶节点的树的性质可以用来解决上述问题。因此，如果我们只给连接叶节点的边分配权重，而给其他边分配 0。那么连接到叶节点的每个边将被分配 s/(叶节点的数量)。由于一条路径最多可以包含两个叶节点，因此最长的路径将是***2 *(s/叶节点数)。***
以下是上述方法的实施:

## C++

```
// C++ program to assign weights to edges to
// minimize the longest path in terms of weight
#include <bits/stdc++.h>
using namespace std;

// Function to add edges
void addEdges(int u, int v, vector<int> adj[])
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function that assigns weights
// and returns the longest path
long double longestPath(vector<int> adj[],
                              int s, int n)
{
    int cnt = 0;
    for (int i = 1; i <= n; i++) {

        if (adj[i].size() == 1)
            cnt++;
    }

    long double ans =
       2.0 * (long double)(s / (long double)(cnt));
    return ans;
}

// Driver Code
int main()
{
    int n = 4;

    // Create an adjacency list
    // to store tree
    vector<int> adj[n + 1];

    // Add edges
    addEdges(1, 2, adj);
    addEdges(1, 3, adj);
    addEdges(1, 4, adj);

    // Given Sum
    int s = 3;

    // Function that prints the
    // longest path in terms of weights
    cout << longestPath(adj, s, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to assign weights to edges to
// minimize the longest path in terms of weight
import java.util.*;

class GFG
{

    // Function to add edges
    static void addEdges(int u, int v, Vector<Integer> adj[])
    {
        adj[u].add(v);
        adj[v].add(u);
    }

    // Function that assigns weights
    // and returns the longest path
    static double longestPath(Vector<Integer> adj[], int s, int n)
    {
        int cnt = 0;
        for (int i = 1; i <= n; i++)
        {

            if (adj[i].size() == 1)
                cnt++;
        }

        double ans = 2.0 * (double) (s / (double) (cnt));
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;

        // Create an adjacency list
        // to store tree
        Vector<Integer>[] adj = new Vector[n + 1];
        for (int i = 0; i < n + 1; i++)
            adj[i] = new Vector<Integer>();

        // Add edges
        addEdges(1, 2, adj);
        addEdges(1, 3, adj);
        addEdges(1, 4, adj);

        // Given Sum
        int s = 3;

        // Function that prints the
        // longest path in terms of weights
        System.out.print(longestPath(adj, s, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to assign weights to
# edges to minimize the longest path
# in terms of weight

# Function to add edges
def addEdges(u, v, adj):

    adj[u].append(v)
    adj[v].append(u)

# Function that assigns weights
# and returns the longest path
def longestPath(adj, s, n):

    cnt = 0
    for i in range(1, n + 1):

        if len(adj[i]) == 1:
            cnt += 1

    ans = 2 * (s / cnt)
    return ans

# Driver Code
if __name__ == "__main__":

    n = 4

    # Create an adjacency list
    # to store tree
    adj = [[] for i in range(n + 1)]

    # Add edges
    addEdges(1, 2, adj)
    addEdges(1, 3, adj)
    addEdges(1, 4, adj)

    # Given Sum
    s = 3

    # Function that prints the
    # longest path in terms of weights
    print(longestPath(adj, s, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to assign weights to edges to
// minimize the longest path in terms of weight
using System;
using System.Collections.Generic;

class GFG
{

    // Function to add edges
    static void addEdges(int u, int v, List<int> []adj)
    {
        adj[u].Add(v);
        adj[v].Add(u);
    }

    // Function that assigns weights
    // and returns the longest path
    static double longestPath(List<int> []adj, int s, int n)
    {
        int cnt = 0;
        for (int i = 1; i <= n; i++)
        {

            if (adj[i].Count == 1)
                cnt++;
        }

        double ans = 2.0 * (double) (s / (double) (cnt));
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;

        // Create an adjacency list
        // to store tree
        List<int>[] adj = new List<int>[n + 1];
        for (int i = 0; i < n + 1; i++)
            adj[i] = new List<int>();

        // Add edges
        addEdges(1, 2, adj);
        addEdges(1, 3, adj);
        addEdges(1, 4, adj);

        // Given Sum
        int s = 3;

        // Function that prints the
        // longest path in terms of weights
        Console.Write(longestPath(adj, s, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to assign weights to edges to
// minimize the longest path in terms of weight

// Function to add edges
function addEdges(u, v, adj)
{
    adj[u].push(v);
    adj[v].push(u);
}

// Function that assigns weights
// and returns the longest path
function longestPath(adj, s, n)
{
    var cnt = 0;
    for (var i = 1; i <= n; i++) {

        if (adj[i].length == 1)
            cnt++;
    }

    var ans =
       2.0 * (s / (cnt));
    return ans;
}

// Driver Code

var n = 4;
// Create an adjacency list
// to store tree
var adj = Array.from(Array(n+1), ()=>Array());
// Add edges
addEdges(1, 2, adj);
addEdges(1, 3, adj);
addEdges(1, 4, adj);
// Given Sum
var s = 3;
// Function that prints the
// longest path in terms of weights
document.write( longestPath(adj, s, n));

</script>
```

**Output:** 

```
2
```