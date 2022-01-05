# 多查询检查一个节点是否为叶节点

> 原文:[https://www . geesforgeks . org/check-一个节点是否是多查询的叶子节点/](https://www.geeksforgeeks.org/check-whether-a-node-is-leaf-node-or-not-for-multiple-queries/)

给定一棵树，其 **N** 个顶点从 **0** 到**N–1**编号，其中 **0** 是根节点。任务是检查一个节点是否是多个查询的叶节点。
**举例:**

```
Input:
       0
     /   \
   1      2
 /  \
3    4 
    /
  5
q[] = {0, 3, 4, 5}
Output:
No
Yes
No
Yes
From the graph, 2, 3 and 5 are the only leaf nodes.
```

**逼近:**存储数组中所有顶点的度数**度数[]** 。对于从 **A** 到 **B** 的每条边，**度【A】**和度【B】增加 **1** 。现在，不是根节点且度数为 1 的每个节点都是叶节点，所有其他节点都不是。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the degree of all the vertices
void init(int degree[], vector<pair<int, int> > edges, int n)
{
    // Initializing degree of all the vertices as 0
    for (int i = 0; i < n; i++) {
        degree[i] = 0;
    }

    // For each edge from A to B, degree[A] and degree[B]
    // are increased by 1
    for (int i = 0; i < edges.size(); i++) {
        degree[edges[i].first]++;
        degree[edges[i].second]++;
    }
}

// Function to perform the queries
void performQueries(vector<pair<int, int> > edges,
                    vector<int> q, int n)
{
    // To store the of degree
    // of all the vertices
    int degree[n];

    // Calculate the degree for all the vertices
    init(degree, edges, n);

    // For every query
    for (int i = 0; i < q.size(); i++) {

        int node = q[i];
        if (node == 0) {
            cout << "No\n";
            continue;
        }
        // If the current node has 1 degree
        if (degree[node] == 1)
            cout << "Yes\n";
        else
            cout << "No\n";
    }
}

// Driver code
int main()
{

    // Number of vertices
    int n = 6;

    // Edges of the tree
    vector<pair<int, int> > edges = {
        { 0, 1 }, { 0, 2 }, { 1, 3 }, { 1, 4 }, { 4, 5 }
    };

    // Queries
    vector<int> q = { 0, 3, 4, 5 };

    // Perform the queries
    performQueries(edges, q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to calculate the degree
// of all the vertices
static void init(int degree[],
                     pair[] edges, int n)
{
    // Initializing degree of
    // all the vertices as 0
    for (int i = 0; i < n; i++)
    {
        degree[i] = 0;
    }

    // For each edge from A to B,
    // degree[A] and degree[B]
    // are increased by 1
    for (int i = 0; i < edges.length; i++)
    {
        degree[edges[i].first]++;
        degree[edges[i].second]++;
    }
}

// Function to perform the queries
static void performQueries(pair [] edges,
                           int []q, int n)
{
    // To store the of degree
    // of all the vertices
    int []degree = new int[n];

    // Calculate the degree for all the vertices
    init(degree, edges, n);

    // For every query
    for (int i = 0; i < q.length; i++)
    {

        int node = q[i];
        if (node == 0)
        {
            System.out.println("No");
            continue;
        }

        // If the current node has 1 degree
        if (degree[node] == 1)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// Driver code
public static void main(String[] args)
{
    // Number of vertices
    int n = 6;

    // Edges of the tree
    pair[] edges = {new pair(0, 1),
                    new pair(0, 2),
                    new pair(1, 3),
                    new pair(1, 4),
                    new pair(4, 5)};

    // Queries
    int []q = { 0, 3, 4, 5 };

    // Perform the queries
    performQueries(edges, q, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to calculate the degree
# of all the vertices
def init(degree, edges, n) :

    # Initializing degree of
    # all the vertices as 0
    for i in range(n) :
        degree[i] = 0;

    # For each edge from A to B,
    # degree[A] and degree[B]
    # are increased by 1
    for i in range(len(edges)) :
        degree[edges[i][0]] += 1;
        degree[edges[i][1]] += 1;

# Function to perform the queries
def performQueries(edges, q, n) :

    # To store the of degree
    # of all the vertices
    degree = [0] * n;

    # Calculate the degree for all the vertices
    init(degree, edges, n);

    # For every query
    for i in range(len(q)) :

        node = q[i];
        if (node == 0) :
            print("No");
            continue;

        # If the current node has 1 degree
        if (degree[node] == 1) :
            print("Yes");
        else :
            print("No");

# Driver code
if __name__ == "__main__" :

    # Number of vertices
    n = 6;

    # Edges of the tree
    edges = [[ 0, 1 ], [ 0, 2 ],
             [ 1, 3 ], [ 1, 4 ],
             [ 4, 5 ]];

    # Queries
    q = [ 0, 3, 4, 5 ];

    # Perform the queries
    performQueries(edges, q, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to calculate the degree
// of all the vertices
static void init(int []degree,
                 pair[] edges, int n)
{
    // Initializing degree of
    // all the vertices as 0
    for (int i = 0; i < n; i++)
    {
        degree[i] = 0;
    }

    // For each edge from A to B,
    // degree[A] and degree[B]
    // are increased by 1
    for (int i = 0; i < edges.Length; i++)
    {
        degree[edges[i].first]++;
        degree[edges[i].second]++;
    }
}

// Function to perform the queries
static void performQueries(pair [] edges,
                            int []q, int n)
{
    // To store the of degree
    // of all the vertices
    int []degree = new int[n];

    // Calculate the degree for all the vertices
    init(degree, edges, n);

    // For every query
    for (int i = 0; i < q.Length; i++)
    {

        int node = q[i];
        if (node == 0)
        {
            Console.WriteLine("No");
            continue;
        }

        // If the current node has 1 degree
        if (degree[node] == 1)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// Driver code
public static void Main(String[] args)
{
    // Number of vertices
    int n = 6;

    // Edges of the tree
    pair[] edges = {new pair(0, 1),
                    new pair(0, 2),
                    new pair(1, 3),
                    new pair(1, 4),
                    new pair(4, 5)};

    // Queries
    int []q = { 0, 3, 4, 5 };

    // Perform the queries
    performQueries(edges, q, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to calculate the degree of all the vertices
function init(degree, edges, n)
{
    // Initializing degree of all the vertices as 0
    for (var i = 0; i < n; i++) {
        degree[i] = 0;
    }

    // For each edge from A to B, degree[A] and degree[B]
    // are increased by 1
    for (var i = 0; i < edges.length; i++) {
        degree[edges[i][0]]++;
        degree[edges[i][1]]++;
    }
}

// Function to perform the queries
function performQueries( edges, q, n)
{
    // To store the of degree
    // of all the vertices
    var degree = Array(n);

    // Calculate the degree for all the vertices
    init(degree, edges, n);

    // For every query
    for (var i = 0; i < q.length; i++) {

        var node = q[i];
        if (node == 0) {
            document.write( "No<br>");
            continue;
        }
        // If the current node has 1 degree
        if (degree[node] == 1)
            document.write( "Yes<br>");
        else
            document.write( "No<br>");
    }
}

// Driver code
// Number of vertices
var n = 6;
// Edges of the tree
var edges = [
    [ 0, 1 ], [ 0, 2 ], [ 1, 3 ], [ 1, 4 ], [ 4, 5 ]
];
// Queries
var q = [ 0, 3, 4, 5 ];
// Perform the queries
performQueries(edges, q, n);

</script>
```

**Output:** 

```
No
Yes
No
Yes
```

**时间复杂度:**O(n)
T3】辅助空间 : O(n)。