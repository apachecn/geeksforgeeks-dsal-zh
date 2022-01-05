# 给定无向图中所有顶点的连通分量中的最小顶点

> 原文:[https://www . geesforgeks . org/给定无向图中所有顶点的最小连通顶点分量/](https://www.geeksforgeeks.org/smallest-vertex-in-the-connected-components-of-all-the-vertices-in-given-undirect-graph/)

给定一个由 2 个 **N** 顶点和 **M** 边组成的[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/) **G(V，E)** ，任务是为范围**【1，N】**内的 **i** 的所有值找到顶点 **i** 的[连通分量](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)中的最小顶点。

**示例:**

> **输入:** N = 5，边[] = {{1，2}，{2，3}，{4，5}}
> **输出:**1 1 1 4
> 4**解释:**给定的图可以分为一组两个相连的组件，即{1，2，3}和{4，5}。
> 
> 1.  对于 i = 1，顶点 1 属于组件{1，2，3}。因此，集合中的最小顶点是 1。
> 2.  对于 i = 2，顶点 2 属于组件{1，2，3}。因此，集合中的最小顶点是 1。
> 3.  对于 i = 3，顶点 3 属于分量{1，2，3}。因此，集合中的最小顶点是 1。
> 4.  对于 i = 4，顶点 4 属于组件{4，5}。因此，集合中的最小顶点是 4。
> 5.  对于 i = 5，顶点 5 属于组件{4，5}。因此，集合中的最小顶点是 4。
> 
> **输入:** N = 6，边[] = {{1，3}，{2，4 } }
> T3】输出: 1 2 1 2 5 6

**方法:**借助[不相交集合并集](https://www.geeksforgeeks.org/disjoint-set-data-structures/)，可以高效地解决给定的问题。可以观察到，由一条边连接的顶点可以合并成同一个集合，并且[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)可以用于跟踪每个形成的集合的最小顶点。以下是要遵循的步骤:

*   使用本文[中讨论的方法](https://www.geeksforgeeks.org/disjoint-set-data-structures/)实现不相交集并集的 **find_set** 和 **union_set** 功能，其中 **find_set(x)** 返回包含 **x** 的集号， **union_set(x，y)** 将包含 **x** 的集与包含 **y** 的集合并。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **边[]** ，对于每个边 **(u，v)** ，将包含 **u** 的集合与包含 **v** 的集合合并。
*   创建一个[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **minVal** ，其中**minVal【x】**存储包含 **x** 作为元素的集合的最小顶点。
*   使用变量 **i** 迭代所有顶点，并为每个顶点将**minVal【find _ set(节点 I)】**的值设置为**minVal【find _ set(I)】**和 **i** 的最小值。
*   完成以上步骤后，对于每个顶点， **i** 在**【1，N】**范围内，打印**minVal【find _ set(I)】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int maxn = 100;

// Stores the parent and size of the
// set of the ith element
int parent[maxn], Size[maxn];

// Function to initialize the ith set
void make_set(int v)
{
    parent[v] = v;
    Size[v] = 1;
}

// Function to find set of ith vertex
int find_set(int v)
{
    // Base Case
    if (v == parent[v]) {
        return v;
    }

    // Recursive call to find set
    return parent[v] = find_set(
               parent[v]);
}

// Function to unite the set that includes
// a and the set that includes b
void union_sets(int a, int b)
{
    a = find_set(a);
    b = find_set(b);

    // If a and b are not from same set
    if (a != b) {
        if (Size[a] < Size[b])
            swap(a, b);
        parent[b] = a;
        Size[a] += Size[b];
    }
}

// Function to find the smallest vertex in
// the connected component of the ith
// vertex for all i in range [1, N]
void findMinVertex(
    int N, vector<pair<int, int> > edges)
{
    // Loop to initialize the ith set
    for (int i = 1; i <= N; i++) {
        make_set(i);
    }

    // Loop to unite all vertices connected
    // by edges into the same set
    for (int i = 0; i < edges.size(); i++) {
        union_sets(edges[i].first,
                   edges[i].second);
    }

    // Stores the minimum vertex value
    // for ith set
    unordered_map<int, int> minVal;

    // Loop to iterate over all vertices
    for (int i = 1; i <= N; i++) {

        // If current vertex does not exist
        // in minVal initialize it with i
        if (minVal[find_set(i)] == 0) {
            minVal[find_set(i)] = i;
        }

        // Update the minimum value of
        // the set having the ith vertex
        else {
            minVal[find_set(i)]
                = min(minVal[find_set(i)], i);
        }
    }

    // Loop to print required answer
    for (int i = 1; i <= N; i++) {
        cout << minVal[find_set(i)] << " ";
    }
}

// Driver Code
int main()
{
    int N = 6;
    vector<pair<int, int> > edges
        = { { 1, 3 }, { 2, 4 } };
    findMinVertex(N, edges);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

maxn = 100

# Stores the parent and size of the
# set of the ith element
parent = [0]*maxn
Size = [0]*maxn

# Function to initialize the ith set

def make_set(v):
    parent[v] = v
    Size[v] = 1

# Function to find set of ith vertex

def find_set(v):
    # Base Case
    if (v == parent[v]):
        return v

    # Recursive call to find set
    parent[v] = find_set(
        parent[v])
    return parent[v]

# Function to unite the set that includes
# a and the set that includes b

def union_sets(a, b):

    a = find_set(a)
    b = find_set(b)

    # If a and b are not from same set
    if (a != b):
        if (Size[a] < Size[b]):
            a, b = b, a
        parent[b] = a
        Size[a] += Size[b]

# Function to find the smallest vertex in
# the connected component of the ith
# vertex for all i in range [1, N]

def findMinVertex(
        N, edges):

    # Loop to initialize the ith set
    for i in range(1, N + 1):
        make_set(i)

    # Loop to unite all vertices connected
    # by edges into the same set
    for i in range(len(edges)):
        union_sets(edges[i][0],
                   edges[i][1])

    # Stores the minimum vertex value
    # for ith set
    minVal = {}

    # Loop to iterate over all vertices
    for i in range(1, N + 1):

        # If current vertex does not exist
        # in minVal initialize it with i
        if (find_set(i) not in minVal):
            minVal[find_set(i)] = i

        # Update the minimum value of
        # the set having the ith vertex
        else:
            minVal[find_set(i)] = min(minVal[find_set(i)], i)

    # Loop to print required answer
    for i in range(1, N + 1):
        print(minVal[find_set(i)], end=" ")

# Driver Code
if __name__ == "__main__":

    N = 6
    edges = [[1, 3], [2, 4]]
    findMinVertex(N, edges)

    # This code is contributed by ukasp.
```

**Output:** 

```
1 2 1 2 5 6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)