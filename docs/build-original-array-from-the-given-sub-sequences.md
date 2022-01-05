# 根据给定的子序列构建原始数组

> 原文:[https://www . geesforgeks . org/build-original-array-from-the-给定-sub-sequence/](https://www.geeksforgeeks.org/build-original-array-from-the-given-sub-sequences/)

给定整数 **N** 和整数数组的有效子序列，其中每个元素都是不同的，并且在范围**【0，N–1】**内，任务是找到原始数组。

**示例:**

> **输入:** N = 6，v[] = {
> {1，2，3}，
> {1，2}，
> {3，4}，
> {5，2}，
> {0，5，4}}
> **输出:** 0 1 5 2 3 4
> 
> **输入:** N = 10，v[] = {
> {9，1，2，8，3}，
> {6，1，2}，
> {9，6，3，4}，
> {5，2，7}，
> {0，9，5，4}}
> **输出:**0 9 6 5 1 8 7 3 4

**方法:**根据给定的子序列构建一个图。逐个选择每个子序列，并在子序列中的两个相邻元素之间添加一条边。建立图形后，对图形进行拓扑排序。
参见[拓扑排序](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)了解拓扑排序。这种拓扑排序是必需的数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to add edge to graph
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
}

// Function to calculate indegrees of all the vertices
void getindeg(vector<int> adj[], int V, vector<int>& indeg)
{
    // If there is an edge from i to x
    // then increment indegree of x
    for (int i = 0; i < V; i++) {
        for (auto x : adj[i]) {
            indeg[x]++;
        }
    }
}

// Function to perform topological sort
vector<int> topo(vector<int> adj[], int V, vector<int>& indeg)
{
    queue<int> q;

    // Push every node to the queue
    // which has no incoming edge
    for (int i = 0; i < V; i++) {
        if (indeg[i] == 0)
            q.push(i);
    }
    vector<int> res;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        res.push_back(u);

        // Since edge u is removed, update the indegrees
        // of all the nodes which had an incoming edge from u
        for (auto x : adj[u]) {
            indeg[x]--;
            if (indeg[x] == 0)
                q.push(x);
        }
    }
    return res;
}

// Function to generate the array
// from the given sub-sequences
vector<int> makearray(vector<vector<int> > v, int V)
{

    // Create the graph from the input sub-sequences
    vector<int> adj[V];
    for (int i = 0; i < v.size(); i++) {
        for (int j = 0; j < v[i].size() - 1; j++) {

            // Add edge between every two consecutive
            // elements of the given sub-sequences
            addEdge(adj, v[i][j], v[i][j + 1]);
        }
    }

    // Get the indegrees for all the vertices
    vector<int> indeg(V, 0);
    getindeg(adj, V, indeg);

    // Get the topological order of the created graph
    vector<int> res = topo(adj, V, indeg);
    return res;
}

// Driver code
int main()
{
    // Size of the required array
    int n = 10;

    // Given sub-sequences of the array
    vector<vector<int> > subseqs{ { 9, 1, 2, 8, 3 },
                                  { 6, 1, 2 },
                                  { 9, 6, 3, 4 },
                                  { 5, 2, 7 },
                                  { 0, 9, 5, 4 } };

    // Get the resultant array as vector
    vector<int> res = makearray(subseqs, n);

    // Printing the array
    for (auto x : res) {
        cout << x << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function to add edge to graph
static void addEdge(ArrayList<ArrayList<Integer>> adj,
                    int u, int v)
{
    adj.get(u).add(v);
}

// Function to calculate indegrees of all the vertices
static void getindeg(ArrayList<ArrayList<Integer>> adj,
                        int V, ArrayList<Integer> indeg)
{

    // If there is an edge from i to x
    // then increment indegree of x
    for(int i = 0; i < V; i++)
    {
        for(int x: adj.get(i))
        {
            indeg.set(x, indeg.get(x) + 1);
        }
    }
}

// Function to perform topological sort
static ArrayList<Integer> topo(ArrayList<ArrayList<Integer>> adj,
                                  int V, ArrayList<Integer> indeg)
{
    Queue<Integer> q = new LinkedList<>();

    // Push every node to the queue
    // which has no incoming edge
    for(int i = 0; i < V; i++)
    {
        if (indeg.get(i) == 0)
        {
            q.add(i);
        }
    }
    ArrayList<Integer> res = new ArrayList<Integer>();

    while (q.size() > 0)
    {
        int u = q.poll();
        res.add(u);

        // Since edge u is removed, update the
        // indegrees of all the nodes which had
        // an incoming edge from u
        for(int x: adj.get(u))
        {
            indeg.set(x, indeg.get(x) - 1);

            if (indeg.get(x) == 0)
            {
                q.add(x);
            }
        }
    }
    return res;
}

// Function to generate the array
// from the given sub-sequences
static ArrayList<Integer> makearray(
    ArrayList<ArrayList<Integer>> v, int V)
{

    // Create the graph from the
    // input sub-sequences
    ArrayList<
    ArrayList<Integer>> adj = new ArrayList<
                                  ArrayList<Integer>>();
    for(int i = 0; i < V; i++)
    {
        adj.add(new ArrayList<Integer>());
    }
    for(int i = 0; i < v.size(); i++)
    {
        for(int j = 0; j < v.get(i).size() - 1; j++)
        {

            // Add edge between every two consecutive
            // elements of the given sub-sequences
            addEdge(adj, v.get(i).get(j),
                         v.get(i).get(j + 1));
        }
    }

    // Get the indegrees for all the vertices
    ArrayList<Integer> indeg = new ArrayList<Integer>();
    for(int i = 0; i < V; i++)
    {
        indeg.add(0);
    }
    getindeg(adj, V, indeg);

    // Get the topological order of the created graph
    ArrayList<Integer> res = topo(adj, V, indeg);
    return res;
}

// Driver code
public static void main(String[] args)
{

    // Size of the required array
    int n = 10;

    // Given sub-sequences of the array
    ArrayList<
    ArrayList<Integer>> subseqs = new ArrayList<
                                      ArrayList<Integer>>();
    subseqs.add(new ArrayList<Integer>(
        Arrays.asList(9, 1, 2, 8, 3)));
    subseqs.add(new ArrayList<Integer>(
        Arrays.asList(6, 1, 2)));
    subseqs.add(new ArrayList<Integer>(
        Arrays.asList(9, 6, 3, 4)));
    subseqs.add(new ArrayList<Integer>(
        Arrays.asList(5, 2, 7)));
    subseqs.add(new ArrayList<Integer>(
        Arrays.asList(0, 9, 5, 4)));

    // Get the resultant array as vector
    ArrayList<Integer> res = makearray(subseqs, n);

    // Printing the array
    for(int x: res)
    {
        System.out.print(x + " ");
    }
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque
adj=[[] for i in range(100)]

# Function to add edge to graph
def addEdge(u, v):
    adj[u].append(v)

# Function to calculate indegrees of all the vertices
def getindeg(V,indeg):

    # If there is an edge from i to x
    # then increment indegree of x
    for i in range(V):
        for x in adj[i]:
            indeg[x] += 1

# Function to perform topological sort
def topo(V,indeg):
    q = deque()

    # Push every node to the queue
    # which has no incoming edge
    for i in range(V):
        if (indeg[i] == 0):
            q.appendleft(i)
    res=[]
    while (len(q) > 0):
        u = q.popleft()
        res.append(u)

        # Since edge u is removed, update the indegrees
        # of all the nodes which had an incoming edge from u
        for x in adj[u]:
            indeg[x]-=1
            if (indeg[x] == 0):
                q.appendleft(x)

    return res

# Function to generate the array
# from the given sub-sequences
def makearray(v, V):

    # Create the graph from the input sub-sequences
    for i in range(len(v)):
        for j in range(len(v[i])-1):

            # Add edge between every two consecutive
            # elements of the given sub-sequences
            addEdge(v[i][j], v[i][j + 1])

    # Get the indegrees for all the vertices
    indeg=[0 for i in range(V)]
    getindeg(V, indeg)

    # Get the topological order of the created graph
    res = topo(V, indeg)
    return res

# Driver code

# Size of the required array
n = 10

# Given sub-sequences of the array
subseqs=[ [ 9, 1, 2, 8, 3 ],
        [ 6, 1, 2 ],
        [ 9, 6, 3, 4 ],
        [ 5, 2, 7 ],
        [ 0, 9, 5, 4 ] ]

# Get the resultant array as vector
res = makearray(subseqs, n)

# Printing the array
for x in res:
    print(x,end=" ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to add edge to graph
static void addEdge(List<List<int>> adj, int u, int v)
{
    adj[u].Add(v);
}

// Function to calculate indegrees of
// all the vertices
static void getindeg(List<List<int>> adj, int V,
                          List<int> indeg)
{

    // If there is an edge from i to x
    // then increment indegree of x
    for(int i = 0; i < V; i++)
    {
        foreach(int x in adj[i])
        {
            indeg[x]++;
        }
    }
}

// Function to perform topological sort
static List<int> topo(List<List<int>> adj, int V,
                           List<int> indeg)
{
    Queue<int> q = new Queue<int>();

    // Push every node to the queue
    // which has no incoming edge
    for(int i = 0; i < V; i++)
    {
        if (indeg[i] == 0)
        {
            q.Enqueue(i);
        }
    }
    List<int> res = new List<int>();

    while (q.Count > 0)
    {
        int u = q.Dequeue();
        res.Add(u);

        // Since edge u is removed, update the
        // indegrees of all the nodes which had
        // an incoming edge from u
        foreach(int x in adj[u])
        {
            indeg[x]--;
            if (indeg[x] == 0)
            {
                q.Enqueue(x);
            }
        }
    }
    return res;
}

// Function to generate the array
// from the given sub-sequences
static List<int> makearray(List<List<int>> v, int V)
{

    // Create the graph from the
    // input sub-sequences
    List<List<int>> adj = new List<List<int>>();
    for(int i = 0; i < V; i++)
    {
        adj.Add(new List<int>());
    }
    for(int i = 0; i < v.Count; i++)
    {
        for(int j = 0; j < v[i].Count - 1; j++)
        {

            // Add edge between every two consecutive
            // elements of the given sub-sequences
            addEdge(adj, v[i][j], v[i][j+1]);
        }
    }

    // Get the indegrees for all the vertices
    List<int> indeg = new List<int>();
    for(int i = 0; i < V; i++)
    {
        indeg.Add(0);
    }
    getindeg(adj, V, indeg);

    // Get the topological order
    // of the created graph
    List<int> res = topo(adj, V, indeg);
    return res;
}

// Driver code
static public void Main()
{

    // Size of the required array
    int n = 10;

    // Given sub-sequences of the array
    List<List<int>> subseqs = new List<List<int>>();
    subseqs.Add(new List<int>(){9, 1, 2, 8, 3});
    subseqs.Add(new List<int>(){6, 1, 2});
    subseqs.Add(new List<int>(){9, 6, 3, 4});
    subseqs.Add(new List<int>(){5, 2, 7});
    subseqs.Add(new List<int>(){0, 9, 5, 4});

    // Get the resultant array as vector
    List<int> res = makearray(subseqs, n);

    // Printing the array
    foreach(int x in res)
    {
        Console.Write(x + " ");
    }
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to add edge to graph
function addEdge(adj, u, v)
{
    adj[u].push(v);
}

// Function to calculate indegrees of all the vertices
function getindeg(adj, V, indeg)
{
    // If there is an edge from i to x
    // then increment indegree of x
    for(let i = 0; i < V; i++)
    {
        for(let x = 0; x < adj[i].length; x++)
        {
            indeg[adj[i][x]] = indeg[adj[i][x]] + 1;
        }
    }
}

// Function to perform topological sort
function topo(adj, V, indeg)
{
    let q = [];

    // Push every node to the queue
    // which has no incoming edge
    for(let i = 0; i < V; i++)
    {
        if (indeg[i] == 0)
        {
            q.push(i);
        }
    }
    let res = [];

    while (q.length > 0)
    {
        let u = q.shift();
        res.push(u);

        // Since edge u is removed, update the
        // indegrees of all the nodes which had
        // an incoming edge from u
        for(let x = 0; x < adj[u].length; x++)
        {
            indeg[adj[u][x]] = indeg[adj[u][x]] - 1;

            if (indeg[adj[u][x]] == 0)
            {
                q.push(adj[u][x]);
            }
        }
    }
    return res;
}

// Function to generate the array
// from the given sub-sequences
function makearray(v,V)
{
    // Create the graph from the
    // input sub-sequences
    let adj = [];
    for(let i = 0; i < V; i++)
    {
        adj.push([]);
    }
    for(let i = 0; i < v.length; i++)
    {
        for(let j = 0; j < v[i].length - 1; j++)
        {

            // Add edge between every two consecutive
            // elements of the given sub-sequences
            addEdge(adj, v[i][j],
                         v[i][j+1]);
        }
    }

    // Get the indegrees for all the vertices
    let indeg = [];
    for(let i = 0; i < V; i++)
    {
        indeg.push(0);
    }
    getindeg(adj, V, indeg);

    // Get the topological order of the created graph
    let res = topo(adj, V, indeg);
    return res;
}

// Driver code
// Size of the required array
    let n = 10;

    // Given sub-sequences of the array
    let subseqs=[ [ 9, 1, 2, 8, 3 ],
        [ 6, 1, 2 ],
        [ 9, 6, 3, 4 ],
        [ 5, 2, 7 ],
        [ 0, 9, 5, 4 ] ];

    // Get the resultant array as vector
    let res = makearray(subseqs, n);

    // Printing the array
    for(let x = 0; x < res.length; x++)
    {
        document.write(res[x] + " ");
    }

// This code is contributed by patel2127
</script>
```

**Output:** 

```
0 9 6 5 1 2 8 7 3 4
```