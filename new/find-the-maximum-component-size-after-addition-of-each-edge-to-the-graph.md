# 在将每个边添加到图形

之后，找到最大组件尺寸

> 原文： [https://www.geeksforgeeks.org/find-the-maximum-component-size-after-addition-of-each-edge-to-the-graph/](https://www.geeksforgeeks.org/find-the-maximum-component-size-after-addition-of-each-edge-to-the-graph/)

给定一个数组 **arr [] []** ，该数组包含要用来构造具有`N`个节点的无向​​图`G`的图的边， 在构造图形时，在添加每个边后找到图形中的最大组件尺寸。
**范例**：

> **输入**：N = 4，arr [] [] = {{1，2}，{3，4}，{2，3}}
> **输出**：2 2 4
> **说明**：
> 最初，图形具有 4 个单独的节点 1、2、3 和 4。
> 添加第一个边后：1 – 2、3、4->最大组件大小= 2
> 添加第二个边缘后：1 – 2，3 – 4->最大组件大小= 2
> 添加第三个边缘后：1 – 2 – 3 – 4 ->最大组件大小= 4
> 
> **输入**：N = 4，arr [] [] = {{2，3}，{1，2}，{1，5}，{2，4}}
> **输出 **：2 3 4 5

**朴素方法**：针对此问题的朴素方法是依次添加边缘，并在每个步骤应用[深度优先搜索算法以找到最大分量的大小。](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)

下面是上述方法的实现：

## C++

```cpp

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

## C#

```cs

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

**Output:** 

```
2 2 4

```

**时间复杂度**：*O（| E | * N）*

**高效方法**：的想法是使用[不交集（按秩和路径压缩合并）](https://www.geeksforgeeks.org/disjoint-set-data-structures/)的概念来更有效地解决该问题。

*   每个节点最初在其内部都是不相交的集合。 随着边缘的添加，不相交的集合会合并在一起，形成更大的分量。 在不相交集合的实现中，我们将基于组件的大小来建立排名系统，即在执行两个组件的合并时，将较大的组件根作为合并操作之后的最终根。
*   在每次添加边后找到最大大小分量的一种方法是遍历大小数组（size [i]表示节点'i'所属的分量的大小），但这在图中的节点数较少时效率很低 高。
*   一种更有效的方法是将所有根的组件大小存储在某些有序的数据结构中，例如[集](https://www.geeksforgeeks.org/hashing-set-1-introduction/)。
*   当两个组件合并时，我们要做的就是从集合中删除以前的组件大小，然后添加组合的组件大小。 因此，在每一步中，我们都可以找到对数复杂度最大的组件。

下面是上述方法的实现：

## C++

```cpp

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
    // to the same compenent
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

            // Sizes of the compenents
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

**Output:** 

```
2 2 4

```

**时间复杂度**：*O（| E | * log（N））*

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。