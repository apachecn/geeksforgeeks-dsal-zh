# 求图中每条边相加后的最大组件尺寸

> 原文:[https://www . geeksforgeeks . org/find-将每个边添加到图形后的最大组件大小/](https://www.geeksforgeeks.org/find-the-maximum-component-size-after-addition-of-each-edge-to-the-graph/)

给定一个数组 **arr[][]** ，该数组包含一个图的边，用于构建一个带有 **N** 节点的无向图 **G** ，任务是在构建该图时，在添加每个边之后，找到图中最大的组件大小。

**示例:**

> **输入:** N = 4，arr[][] = {{1，2}，{3，4}，{2，3}}
> **输出:** 2 2 4
> **解释:**
> 最初，图中有 4 个单独的节点 1、2、3 和 4。
> 添加第一条边后:1–2，3，4 - >最大构件尺寸= 2
> 添加第二条边后:1–2，3–4->最大构件尺寸= 2
> 添加第三条边后:1–2–3–4->最大构件尺寸= 4
> 
> **输入:** N = 4，arr[][] = {{2，3}，{1，2}，{1，5}，{2，4}}
> **输出:** 2 3 4 5

**朴素方法:**这个问题的朴素方法是依次添加边，在每一步应用[深度优先搜索算法找到最大分量的大小。](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)

下面是上述方法的实现:

## C++

```
// C++ program to find the
// maximum comake_paironent size
// after addition of each
// edge to the graph
#include <bits/stdc++.h>

using namespace std;

// Function to perform
// Depth First Search
// on the given graph
int dfs(int u, int visited[],
        vector<int>* adj)
{
    // Mark visited
    visited[u] = 1;
    int size = 1;

    // Add each child's
    // comake_paironent size
    for (auto child : adj[u]) {
        if (!visited[child])
            size += dfs(child,
                        visited, adj);
    }
    return size;
}

// Function to find the maximum
// comake_paironent size
// after addition of each
// edge to the graph
void maxSize(vector<pair<int, int> > e,
             int n)
{
    // Graph in the adjacency
    // list format
    vector<int> adj[n];

    // Visited array
    int visited[n];

    vector<int> answer;

    // At each step, add a new
    // edge and apply dfs on all
    // the nodes to find the maximum
    // comake_paironent size
    for (auto edge : e) {

        // Add this edge to undirected graph
        adj[edge.first - 1].push_back(
            edge.second - 1);
        adj[edge.second - 1].push_back(
            edge.first - 1);

        // Mark all the nodes
        // as unvisited
        memset(visited, 0,
               sizeof(visited));

        int maxAns = 0;

        // Loop to perform DFS
        // and find the size
        // of the maximum comake_paironent
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                maxAns = max(maxAns,
                             dfs(i, visited, adj));
            }
        }
        answer.push_back(maxAns);
    }

    // Print the answer
    for (auto i : answer) {
        cout << i << " ";
    }
}

// Driver code
int main()
{
    int N = 4;
    vector<pair<int, int> > E;
    E.push_back(make_pair(1, 2));
    E.push_back(make_pair(3, 4));
    E.push_back(make_pair(2, 3));

    maxSize(E, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// comake_paironent size after
// addition of each edge to the graph
import java.util.*;

@SuppressWarnings("unchecked")
class GFG{

static class pair
{
    int Key, Value;

    pair(int Key, int Value)
    {
        this.Key = Key;
        this.Value = Value;
    }
}

// Function to perform Depth First
// Search on the given graph
static int dfs(int u, int []visited,
               ArrayList []adj)
{

    // Mark visited
    visited[u] = 1;
    int size = 1;

    // Add each child's
    // comake_paironent size
    for(int child : (ArrayList<Integer>)adj[u])
    {
        if (visited[child] == 0)
            size += dfs(child,
                        visited, adj);
    }
    return size;
}

// Function to find the maximum
// comake_paironent size after
// addition of each edge to the graph
static void maxSize(ArrayList e,
                    int n)
{

    // Graph in the adjacency
    // list format
    ArrayList []adj = new ArrayList[n];

    for(int i = 0; i < n; i++)
    {
        adj[i] = new ArrayList();
    }

    // Visited array
    int []visited = new int[n];

    ArrayList answer = new ArrayList();

    // At each step, add a new
    // edge and apply dfs on all
    // the nodes to find the maximum
    // comake_paironent size
    for(pair edge : (ArrayList<pair>)e)
    {

        // Add this edge to undirected graph
        adj[edge.Key - 1].add(
           edge.Value - 1);
        adj[edge.Value - 1].add(
              edge.Key - 1);

        // Mark all the nodes
        // as unvisited
        Arrays.fill(visited,0);

        int maxAns = 0;

        // Loop to perform DFS and find the
        // size of the maximum comake_paironent
        for(int i = 0; i < n; i++)
        {
            if (visited[i] == 0)
            {
                maxAns = Math.max(maxAns,
                              dfs(i, visited, adj));
            }
        }
        answer.add(maxAns);
    }

    // Print the answer
    for(int i : (ArrayList<Integer>) answer)
    {
        System.out.print(i + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    ArrayList E = new ArrayList();
    E.add(new pair(1, 2));
    E.add(new pair(3, 4));
    E.add(new pair(2, 3));

    maxSize(E, N);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum comake_paironent size
# after addition of each
# edge to the graph

# Function to perform
# Depth First Search
# on the given graph
def dfs(u, visited, adj):

    # Mark visited
    visited[u] = 1
    size = 1

    # Add each child's
    # comake_paironent size
    for child in adj[u]:
        if (visited[child] == 0):
            size += dfs(child, visited, adj)
    return size

# Function to find the maximum
# comake_paironent size
# after addition of each
# edge to the graph
def maxSize(e, n):

    # Graph in the adjacency
    # list format
    adj = []

    for i in range(n):
        adj.append([])

    # Visited array
    visited = [0]*(n)

    answer = []

    # At each step, add a new
    # edge and apply dfs on all
    # the nodes to find the maximum
    # comake_paironent size
    for edge in e:
        # Add this edge to undirected graph
        adj[edge[0] - 1].append(edge[1] - 1)
        adj[edge[1] - 1].append(edge[0] - 1)

        # Mark all the nodes
        # as unvisited
        visited = [0]*(n)

        maxAns = 0

        # Loop to perform DFS
        # and find the size
        # of the maximum comake_paironent
        for i in range(n):
            if (visited[i] == 0):
                maxAns = max(maxAns, dfs(i, visited, adj))
        answer.append(maxAns)

    # Print the answer
    for i in answer:
        print(i, "", end = "")

N = 4
E = []
E.append([1, 2])
E.append([3, 4])
E.append([2, 3])

maxSize(E, N)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to find the
// maximum comake_paironent size
// after addition of each
// edge to the graph
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to perform
// Depth First Search
// on the given graph
static int dfs(int u, int []visited,
               ArrayList []adj)
{

    // Mark visited
    visited[u] = 1;
    int size = 1;

    // Add each child's
    // comake_paironent size
    foreach (int child in adj[u])
    {
        if (visited[child] == 0)
            size += dfs(child,
                        visited, adj);
    }
    return size;
}

// Function to find the maximum
// comake_paironent size
// after addition of each
// edge to the graph
static void maxSize(ArrayList e,
                    int n)
{

    // Graph in the adjacency
    // list format
    ArrayList []adj = new ArrayList[n];

    for(int i = 0; i < n; i++)
    {
        adj[i] = new ArrayList();
    }

    // Visited array
    int []visited = new int[n];

    ArrayList answer = new ArrayList();

    // At each step, add a new
    // edge and apply dfs on all
    // the nodes to find the maximum
    // comake_paironent size
    foreach(KeyValuePair<int, int> edge in e)
    {

        // Add this edge to undirected graph
        adj[edge.Key - 1].Add(
           edge.Value - 1);
        adj[edge.Value - 1].Add(
              edge.Key - 1);

        // Mark all the nodes
        // as unvisited
        Array.Fill(visited,0);

        int maxAns = 0;

        // Loop to perform DFS
        // and find the size
        // of the maximum comake_paironent
        for(int i = 0; i < n; i++)
        {
            if (visited[i] == 0)
            {
                maxAns = Math.Max(maxAns,
                              dfs(i, visited, adj));
            }
        }
        answer.Add(maxAns);
    }

    // Print the answer
    foreach(int i in answer)
    {
        Console.Write(i + " ");
    }
}

// Driver code
public static void Main(string[] args)
{
    int N = 4;
    ArrayList E = new ArrayList();
    E.Add(new KeyValuePair<int, int>(1, 2));
    E.Add(new KeyValuePair<int, int>(3, 4));
    E.Add(new KeyValuePair<int, int>(2, 3));

    maxSize(E, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // maximum comake_paironent size
    // after addition of each
    // edge to the graph

    // Function to perform
    // Depth First Search
    // on the given graph
    function dfs(u, visited, adj)
    {

        // Mark visited
        visited[u] = 1;
        let size = 1;

        // Add each child's
        // comake_paironent size
        for(let child = 0; child < adj[u].length; child++)
        {
            if (visited[adj[u][child]] == 0)
            {
                size += dfs(adj[u][child], visited, adj);
            }
        }
        return size;
    }

    // Function to find the maximum
    // comake_paironent size
    // after addition of each
    // edge to the graph
    function maxSize(e, n)
    {
        // Graph in the adjacency
        // list format
        let adj = [];

        for(let i = 0; i < n; i++)
        {
            adj.push([]);
        }

        // Visited array
        let visited = new Array(n);
        visited.fill(0);

        let answer = [];

        // At each step, add a new
        // edge and apply dfs on all
        // the nodes to find the maximum
        // comake_paironent size
        for(let edge = 0; edge < e.length; edge++)
        {
            // Add this edge to undirected graph
            adj[e[edge][0] - 1].push(e[edge][1] - 1);
            adj[e[edge][1] - 1].push(e[edge][0] - 1);

            // Mark all the nodes
            // as unvisited
            visited.fill(0);

            let maxAns = 0;

            // Loop to perform DFS
            // and find the size
            // of the maximum comake_paironent
            for(let i = 0; i < n; i++)
            {
                if (visited[i] == 0)
                    maxAns = Math.max(maxAns, dfs(i, visited, adj));
            }
            answer.push(maxAns);
        }

        // Print the answer
        for(let i = 0; i < answer.length; i++)
        {
            document.write(answer[i] + " ");
        }
    }

    let N = 4;
    let E = [];
    E.push([1, 2]);
    E.push([3, 4]);
    E.push([2, 3]);

    maxSize(E, N);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2 2 4
```

**时间复杂度:** *O(|E| * N)*

**高效方法:**思路是利用[不相交集(秩和路径压缩并集)](https://www.geeksforgeeks.org/disjoint-set-data-structures/)的概念更高效地解决问题。

*   每个节点最初都是一个独立的集合。当添加边时，不相交的集合会合并在一起，形成更大的组件。在不相交集合实现中，我们将基于组件大小来建立排名系统，即当执行两个组件的合并时，较大组件的根将被视为合并操作后的最终根。
*   在每次边添加后找到最大尺寸分量的一种方法是遍历尺寸数组(尺寸[i]表示节点‘I’所属的分量的尺寸)，但是当图中的节点数量较高时，这是低效的。
*   更有效的方法是将所有根的组件大小存储在一些有序的数据结构中，如[集合](https://www.geeksforgeeks.org/hashing-set-1-introduction/)。
*   当两个组件合并时，我们所需要做的就是从集合中移除先前的组件大小，并添加组合的组件大小。所以在每一步，我们都能够找到对数复杂度中最大的分量大小。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the maximum
// component size after the addition of
// each edge to the graph

#include <bits/stdc++.h>

using namespace std;

// Variables for implementing DSU
int par[100005];
int size[100005];

// Root of the component of node i
int root(int i)
{
    if (par[i] == i)
        return i;

    // Finding the root and applying
    // path compression
    else
        return par[i] = root(par[i]);
}

// Function to merge two components
void merge(int a, int b)
{

    // Find the roots of both
    // the components
    int p = root(a);
    int q = root(b);

    // If both the nodes already belong
    // to the same component
    if (p == q)
        return;

    // Union by rank, the rank in
    // this case is the size of
    // the component.
    // Smaller size will be
    // merged into larger,
    // so the larger's root
    // will be the final root
    if (size[p] > size[q])
        swap(p, q);

    par[p] = q;
    size[q] += size[p];
}

// Function to find the
// maximum component size
// after the addition of
// each edge to the graph
void maxSize(vector<pair<int, int> > e, int n)
{

    // Initialising the disjoint set
    for (int i = 1; i < n + 1; i++) {

        // Each node is the root and
        // each component size is 1
        par[i] = i;
        size[i] = 1;
    }

    vector<int> answer;

    // A multiset is being used to store
    // the size of the components
    // because multiple components
    // can have same sizes
    multiset<int> compSizes;
    for (int i = 1; i <= n; i++)
        compSizes.insert(size[i]);

    // At each step; add a new edge,
    // merge the components
    // and find the max
    // sized component
    for (auto edge : e) {

        // Merge operation is required only when
        // both the nodes don't belong to the
        // same component
        if (root(edge.first) != root(edge.second)) {

            // Sizes of the components
            int size1 = size[root(edge.first)];
            int size2 = size[root(edge.second)];

            // Remove the previous component sizes
            compSizes.erase(compSizes.find(size1));
            compSizes.erase(compSizes.find(size2));

            // Perform the merge operation
            merge(edge.first, edge.second);

            // Insert the combined size
            compSizes.insert(size1 + size2);
        }

        // Maximum value in the multiset is
        // the max component size
        answer.push_back(*compSizes.rbegin());
    }

    // Printing the answer
    for (int i = 0; i < answer.size(); i++) {
        cout << answer[i] << " ";
    }
}

// Driver code
int main()
{
    int N = 4;
    vector<pair<int, int> > E;
    E.push_back(make_pair(1, 2));
    E.push_back(make_pair(3, 4));
    E.push_back(make_pair(2, 3));

    maxSize(E, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation to find the maximum
# component size after the addition of
# each edge to the graph

# Variables for implementing DSU
par=[-1]*100005
size=[-1]*100005

# Root of the component of node i
def root(i):
    if (par[i] == i):
        return i

    # Finding the root and applying
    # path compression
    par[i] = root(par[i])
    return par[i]

# Function to merge two components
def merge(a, b):

    # Find the roots of both
    # the components
    p = root(a)
    q = root(b)

    # If both the nodes already belong
    # to the same component
    if (p == q):
        return

    # Union by rank, the rank in
    # this case is the size of
    # the component.
    # Smaller size will be
    # merged into larger,
    # so the larger's root
    # will be the final root
    if (size[p] > size[q]):
        p,q=q,p

    par[p] = q
    size[q] += size[p]

# Function to find the
# maximum component size
# after the addition of
# each edge to the graph
def maxSize(e, n):

    # Initialising the disjoint set
    for i in range(1, n + 1):

        # Each node is the root and
        # each component size is 1
        par[i] = i
        size[i] = 1

    answer=[]

    # A multiset is being used to store
    # the size of the components
    # because multiple components
    # can have same sizes
    compSizes=dict()
    for i in range(1,n+1):
        compSizes[size[i]]=compSizes.get(size[i],0)+1

    # At each step add a new edge,
    # merge the components
    # and find the max
    # sized component
    for  edge in e:

        # Merge operation is required only when
        # both the nodes don't belong to the
        # same component
        if (root(edge[0]) != root(edge[1])) :

            # Sizes of the components
            size1 = size[root(edge[0])]
            size2 = size[root(edge[1])]

            # Remove the previous component sizes
            compSizes[size1]-=1
            if compSizes[size1]==0:
                del compSizes[size1]
            compSizes[size2]-=1
            if compSizes[size2]==0:
                del compSizes[size2]

            # Perform the merge operation
            merge(edge[0], edge[1])

            # Insert the combined size
            compSizes[size1 + size2]=compSizes.get(size1 + size2,0)+1

        # Maximum value in the multiset is
        # the max component size
        answer.append(max(compSizes.keys()))

    # Printing the answer
    for i in range(len(answer)) :
        print(answer[i],end=' ')

# Driver code
if __name__ == '__main__':
    N = 4
    E=[]
    E.append((1, 2))
    E.append((3, 4))
    E.append((2, 3))

    maxSize(E, N)
```

**Output:** 

```
2 2 4
```

**时间复杂度:***O(| E | * log(N))*
T5】辅助空间: O(N)