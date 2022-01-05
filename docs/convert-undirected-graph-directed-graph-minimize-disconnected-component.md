# 最小化弱连接节点的数量

> 原文:[https://www . geesforgeks . org/convert-无向图-有向图-最小化-断开组件/](https://www.geeksforgeeks.org/convert-undirected-graph-directed-graph-minimize-disconnected-component/)

给定一个**无向图**，任务是在将这个图转换成有向图后，找到最小数量的弱连接节点。

**弱连接节点:**具有 0 度(输入边数)的节点。

**先决条件:**T2【BFS 穿越

**示例:**

```
Input : 4 4 
        0 1
        1 2
        2 3
        3 0
Output : 0 disconnected components

Input : 6 5
       1 2
       2 3
       4 5
       4 6
       5 6
Output : 1 disconnected components
```

**说明:**

![](img/572e0755074ba6b76bf2e20d022c7bdb.png)

**方法:**我们找到一个节点，它有助于在一次行走中遍历最大节点。为了覆盖所有可能的路径，为此使用了 [DFS 图遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)技术。

执行以上步骤来遍历图表。现在，再次遍历图，检查哪些节点有 0 个索引。

## C++

```
// C++ code to minimize the number
// of weakly connected nodes
#include <bits/stdc++.h>
using namespace std;

// Set of nodes which are traversed
// in each launch of the DFS
set<int> node;
vector<int> Graph[10001];

// Function traversing the graph using DFS
// approach and updating the set of nodes
void dfs(bool visit[], int src)
{
    visit[src] = true;
    node.insert(src);
    int len = Graph[src].size();
    for (int i = 0; i < len; i++)   
        if (!visit[Graph[src][i]])       
            dfs(visit, Graph[src][i]);
}

// building a undirected graph
void buildGraph(int x[], int y[], int len){

    for (int i = 0; i < len; i++)
    {
        int p = x[i];
        int q = y[i];
        Graph[p].push_back(q);
        Graph[q].push_back(p);
    }
}

// computes the minimum number of disconnected
// components when a bi-directed graph is
// converted to a undirected graph
int compute(int n)
{
    // Declaring and initializing
    // a visited array
    bool visit[n + 5];
    memset(visit, false, sizeof(visit));
    int number_of_nodes = 0;

    // We check if each node is
    // visited once or not
    for (int i = 0; i < n; i++)
    {
        // We only launch DFS from a
        // node iff it is unvisited.
        if (!visit[i]) {

            // Clearing the set of nodes
            // on every relaunch of DFS
            node.clear();

            // relaunching DFS from an
            // unvisited node.
            dfs(visit, i);

            // iterating over the node set to count the
            // number of nodes visited after making the
            // graph directed and storing it in the
            // variable count. If count / 2 == number
            // of nodes - 1, then increment count by 1.
            int count = 0;        
            for (auto it = node.begin(); it != node.end(); ++it)
                count += Graph[(*it)].size();

            count /= 2;       
            if (count == node.size() - 1)
               number_of_nodes++;
        }
    }
    return number_of_nodes;
}

//Driver function
int main()
{
    int n = 6,m = 4;
    int x[m + 5] = {1, 1, 4, 4};
    int y[m+5] = {2, 3, 5, 6};

    /*For given x and y above, graph is as below :
        1-----2         4------5
        |               |
        |               |
        |               |
        3               6

        // Note : This code will work for
        // connected graph also as :
        1-----2
        |     | \
        |     |  \
        |     |   \
        3-----4----5
    */

    // Building graph in the form of a adjacency list
    buildGraph(x, y, n);
    cout << compute(n) << " weakly connected nodes";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to minimize the number
// of weakly connected nodes
import java.util.*;
public class Main
{
    // Set of nodes which are traversed
    // in each launch of the DFS
    static HashSet<Integer> node = new HashSet<Integer>();
    static Vector<Vector<Integer>> Graph = new Vector<Vector<Integer>>();

    // Function traversing the graph using DFS
    // approach and updating the set of nodes
    static void dfs(boolean[] visit, int src)
    {
        visit[src] = true;
        node.add(src);
        int len = Graph.get(src).size();

        for(int i = 0; i < len; i++)  
            if (!visit[Graph.get(src).get(i)])      
                dfs(visit, Graph.get(src).get(i));
    }

    // Building a undirected graph
    static void buildGraph(int[] x, int[] y, int len)
    {
        for(int i = 0; i < len; i++)
        {
            int p = x[i];
            int q = y[i];
            Graph.get(p).add(q);
            Graph.get(q).add(p);
        }
    }

    // Computes the minimum number of disconnected
    // components when a bi-directed graph is
    // converted to a undirected graph
    static int compute(int n)
    {

        // Declaring and initializing
        // a visited array
        boolean[] visit = new boolean[n + 5];
        Arrays.fill(visit, false);

        int number_of_nodes = 0;

        // We check if each node is
        // visited once or not
        for(int i = 0; i < n; i++)
        {

            // We only launch DFS from a
            // node iff it is unvisited.
            if (!visit[i])
            {

                // Clearing the set of nodes
                // on every relaunch of DFS
                node.clear();

                // Relaunching DFS from an
                // unvisited node.
                dfs(visit, i);

                // Iterating over the node set to count the
                // number of nodes visited after making the
                // graph directed and storing it in the
                // variable count. If count / 2 == number
                // of nodes - 1, then increment count by 1.
                int count = 0;       
                for(int it : node)
                    count += Graph.get(it).size();

                count /= 2;

                if (count == node.size() - 1)
                   number_of_nodes++;
            }
        }
        return number_of_nodes;
    }

    public static void main(String[] args) {
        int n = 6;
        for(int i = 0; i < 10001; i++)
        {
            Graph.add(new Vector<Integer>());
        }
        int[] x = { 1, 1, 4, 4, 0, 0, 0, 0 };
        int[] y = { 2, 3, 5, 6, 0, 0, 0, 0 };

        /*For given x and y above, graph is as below :
            1-----2         4------5
            |               |
            |               |
            |               |
            3               6

            // Note : This code will work for
            // connected graph also as :
            1-----2
            |     | \
            |     |  \
            |     |   \
            3-----4----5
        */

        // Building graph in the form of a adjacency list
        buildGraph(x, y, n);
        System.out.print(compute(n) +
        " weakly connected nodes");
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 code to minimize the number
# of weakly connected nodes

# Set of nodes which are traversed
# in each launch of the DFS
node = set()
Graph = [[] for i in range(10001)]

# Function traversing the graph using DFS
# approach and updating the set of nodes
def dfs(visit, src):

    visit[src] = True
    node.add(src)
    llen = len(Graph[src])

    for i in range(llen):
        if (not visit[Graph[src][i]]):
            dfs(visit, Graph[src][i])

# Building a undirected graph
def buildGraph(x, y, llen):

    for i in range(llen):
        p = x[i]
        q = y[i]
        Graph[p].append(q)
        Graph[q].append(p)

# Computes the minimum number of disconnected
# components when a bi-directed graph is
# converted to a undirected graph
def compute(n):

    # Declaring and initializing
    # a visited array
    visit = [False for i in range(n + 5)]

    number_of_nodes = 0

    # We check if each node is
    # visited once or not
    for i in range(n):

        # We only launch DFS from a
        # node iff it is unvisited.
        if (not visit[i]):

            # Clearing the set of nodes
            # on every relaunch of DFS
            node.clear()

            # Relaunching DFS from an
            # unvisited node.
            dfs(visit, i)

            # Iterating over the node set to count the
            # number of nodes visited after making the
            # graph directed and storing it in the
            # variable count. If count / 2 == number
            # of nodes - 1, then increment count by 1.
            count = 0     

            for it in node:
                count += len(Graph[(it)])

            count //= 2

            if (count == len(node) - 1):
               number_of_nodes += 1

    return number_of_nodes

# Driver code
if __name__=='__main__':

    n = 6
    m = 4
    x = [ 1, 1, 4, 4, 0, 0, 0, 0, 0 ]
    y = [ 2, 3, 5, 6, 0, 0, 0, 0, 0 ]

    '''For given x and y above, graph is as below :
        1-----2         4------5
        |               |
        |               |
        |               |
        3               6

        # Note : This code will work for
        # connected graph also as :
        1-----2
        |     | \
        |     |  \
        |     |   \
        3-----4----5
    '''

    # Building graph in the form of a adjacency list
    buildGraph(x, y, n)

    print(str(compute(n)) +
          " weakly connected nodes")

# This code is contributed by rutvik_56
```

## C#

```
// C# code to minimize the number
// of weakly connected nodes
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Set of nodes which are traversed
// in each launch of the DFS
static HashSet<int> node = new HashSet<int>();
static List<int> []Graph = new List<int>[10001];

// Function traversing the graph using DFS
// approach and updating the set of nodes
static void dfs(bool []visit, int src)
{
    visit[src] = true;
    node.Add(src);
    int len = Graph[src].Count;

    for(int i = 0; i < len; i++)   
        if (!visit[Graph[src][i]])       
            dfs(visit, Graph[src][i]);
}

// Building a undirected graph
static void buildGraph(int []x, int []y, int len)
{
    for(int i = 0; i < len; i++)
    {
        int p = x[i];
        int q = y[i];
        Graph[p].Add(q);
        Graph[q].Add(p);
    }
}

// Computes the minimum number of disconnected
// components when a bi-directed graph is
// converted to a undirected graph
static int compute(int n)
{

    // Declaring and initializing
    // a visited array
    bool []visit = new bool[n + 5];
    Array.Fill(visit, false);

    int number_of_nodes = 0;

    // We check if each node is
    // visited once or not
    for(int i = 0; i < n; i++)
    {

        // We only launch DFS from a
        // node iff it is unvisited.
        if (!visit[i])
        {

            // Clearing the set of nodes
            // on every relaunch of DFS
            node.Clear();

            // Relaunching DFS from an
            // unvisited node.
            dfs(visit, i);

            // Iterating over the node set to count the
            // number of nodes visited after making the
            // graph directed and storing it in the
            // variable count. If count / 2 == number
            // of nodes - 1, then increment count by 1.
            int count = 0;        
            foreach(int it in node)
                count += Graph[(it)].Count;

            count /= 2;

            if (count == node.Count - 1)
               number_of_nodes++;
        }
    }
    return number_of_nodes;
}

// Driver Code
static void Main(string []args)
{
    int n = 6;
    for(int i = 0; i < 10001; i++)
    {
        Graph[i] = new List<int>();
    }
    int []x = { 1, 1, 4, 4, 0, 0, 0, 0 };
    int []y = { 2, 3, 5, 6, 0, 0, 0, 0 };

    /*For given x and y above, graph is as below :
        1-----2         4------5
        |               |
        |               |
        |               |
        3               6

        // Note : This code will work for
        // connected graph also as :
        1-----2
        |     | \
        |     |  \
        |     |   \
        3-----4----5
    */

    // Building graph in the form of a adjacency list
    buildGraph(x, y, n);
    Console.Write(compute(n) +
    " weakly connected nodes");
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>
    // Javascript code to minimize the number
    // of weakly connected nodes

    // Set of nodes which are traversed
    // in each launch of the DFS
    let node = new Set();
    let Graph = [];
    for(let i = 0; i < 10001; i++)
    {
        Graph.push([]);
    }

    // Function traversing the graph using DFS
    // approach and updating the set of nodes
    function dfs(visit, src)
    {
        visit[src] = true;
        node.add(src);
        let len = Graph[src].length;

        for(let i = 0; i < len; i++)  
            if (!visit[Graph[src][i]])      
                dfs(visit, Graph[src][i]);
    }

    // Building a undirected graph
    function buildGraph(x, y, len)
    {
        for(let i = 0; i < len; i++)
        {
            let p = x[i];
            let q = y[i];
            Graph[p].push(q);
            Graph[q].push(p);
        }
    }

    // Computes the minimum number of disconnected
    // components when a bi-directed graph is
    // converted to a undirected graph
    function compute(n)
    {

        // Declaring and initializing
        // a visited array
        let visit = new Array(n + 5);
        visit.fill(false);

        let number_of_nodes = 0;

        // We check if each node is
        // visited once or not
        for(let i = 0; i < n; i++)
        {

            // We only launch DFS from a
            // node iff it is unvisited.
            if (!visit[i])
            {

                // Clearing the set of nodes
                // on every relaunch of DFS
                node.clear();

                // Relaunching DFS from an
                // unvisited node.
                dfs(visit, i);

                // Iterating over the node set to count the
                // number of nodes visited after making the
                // graph directed and storing it in the
                // variable count. If count / 2 == number
                // of nodes - 1, then increment count by 1.
                let count = 0;    
                node.forEach (function(it) {
                  count += Graph[it].length;
                })

                count = parseInt(count / 2);

                if (count == node.size - 1)
                   number_of_nodes++;
            }
        }
        return number_of_nodes;
    }

    let n = 6;
    let x = [ 1, 1, 4, 4, 0, 0, 0, 0 ];
    let y = [ 2, 3, 5, 6, 0, 0, 0, 0 ];

    /*For given x and y above, graph is as below :
        1-----2         4------5
        |               |
        |               |
        |               |
        3               6

        // Note : This code will work for
        // connected graph also as :
        1-----2
        |     | \
        |     |  \
        |     |   \
        3-----4----5
    */

    // Building graph in the form of a adjacency list
    buildGraph(x, y, n);
    document.write(compute(n) +
    " weakly connected nodes");

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
2 weakly connected nodes
```