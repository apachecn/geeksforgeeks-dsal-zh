# 所有树对之间的最小边重的乘积

> 原文:[https://www . geeksforgeeks . org/所有树对之间的最小边重乘积/](https://www.geeksforgeeks.org/product-of-minimum-edge-weight-between-all-pairs-of-a-tree/)

给定一棵有 N 个顶点和 N-1 条边的树。让我们定义一个函数 F(a，b)，它等于节点 a & b 之间路径中的最小边权重。任务是计算所有这样的 F(a，b)的乘积。这里 a&b 是无序对和 a！=b.
所以，基本上，我们需要找到:
的值

```
                           where 0<=i<j<=n-1.
```

在输入中，我们将被赋予 N 的值，然后 N-1 行跟随。每一行包含 3 个整数 u，v，w，表示节点 u 和 v 之间的边以及它的权重 w。因为乘积会很大，所以以 10^9+7.模输出它
**例:**

```
Input :
N = 4
1 2 1
1 3 3
4 3 2
Output : 12
Given tree is:
          1
      (1)/  \(3)
       2     3
              \(2)
               4
We will calculate the minimum edge weight between all the pairs:
F(1, 2) = 1         F(2, 3) = 1
F(1, 3) = 3         F(2, 4) = 1
F(1, 4) = 2         F(3, 4) = 2
Product of all F(i, j) = 1*3*2*1*1*2 = 12 mod (10^9 +7) =12

Input :
N = 5
1 2 1
1 3 3
4 3 2
1 5 4
Output :
288
```

如果我们仔细观察，那么我们将会看到，如果有一组节点的最小边权重为 W，并且如果我们在这个集合中添加一个节点，该节点通过权重为 W 的边与整个集合相连，这样 W <w then="" path="" formed="" between="" recently="" added="" node="" to="" all="" nodes="" present="" in="" the="" set="" will="" have="" minimum="" weight="" w.="">那么，这里我们可以应用[不相交-集合并](https://www.geeksforgeeks.org/disjoint-set-data-structures/)的概念来解决这个问题。
首先，按照权重递减对数据结构进行排序。最初将所有节点指定为一个集合。现在，当我们合并两个集合时，请执行以下操作:-</w> 

```
      Product=(present weight)^(size of set1*size of set2).                    
```

我们将对树的所有边乘以这个乘积值。
以下是上述方法的实现:

## C++

```
// C++ Implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007

// Function to return  (x^y) mod p
int power(int x, unsigned int y, int p)
{
    int res = 1;

    x = x % p;

    while (y > 0) {

        if (y & 1)
            res = (res * x) % p;
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Declaring size array globally
int size[300005];
int freq[300004];
vector<pair<int, pair<int, int> > > edges;

// Initializing DSU data structure
void initialize(int Arr[], int N)
{
    for (int i = 0; i < N; i++) {
        Arr[i] = i;
        size[i] = 1;
    }
}

// Function to find the root of ith
// node in the disjoint set
int root(int Arr[], int i)
{
    while (Arr[i] != i) {
        i = Arr[i];
    }
    return i;
}

// Weighted union using Path Compression
void weighted_union(int Arr[],
                    int size[], int A, int B)
{
    int root_A = root(Arr, A);
    int root_B = root(Arr, B);

    // size of set A is small than size of set B
    if (size[root_A] < size[root_B]) {
        Arr[root_A] = Arr[root_B];
        size[root_B] += size[root_A];
    }

    // size of set B is small than size of set A
    else {
        Arr[root_B] = Arr[root_A];
        size[root_A] += size[root_B];
    }
}

// Function to add an edge in the tree
void AddEdge(int a, int b, int w)
{
    edges.push_back({ w, { a, b } });
}

// Build the tree
void MakeTree()
{
    AddEdge(1, 2, 1);
    AddEdge(1, 3, 3);
    AddEdge(3, 4, 2);
}

// Function to return the required product
int MinProduct()
{
    int result = 1;

    // Sorting the edges with respect to its weight
    sort(edges.begin(), edges.end());

    // Start iterating in decreasing order of weight
    for (int i = edges.size() - 1; i >= 0; i--) {

        // Determine Current edge values
        int curr_weight = edges[i].first;
        int Node1 = edges[i].second.first;
        int Node2 = edges[i].second.second;

        // Calculate root of each node
        // and size of each set
        int Root1 = root(freq, Node1);
        int Set1_size = size[Root1];
        int Root2 = root(freq, Node2);
        int Set2_size = size[Root2];

        // Using the formula
        int prod = Set1_size * Set2_size;
        int Product = power(curr_weight, prod, mod);

        // Calculating final result
        result = ((result % mod) *
                             (Product % mod)) % mod;

        // Weighted union using Path Compression
        weighted_union(freq, size, Node1, Node2);
    }
    return result % mod;
}

// Driver code
int main()
{
    int n = 4;

    initialize(freq, n);

    MakeTree();

    cout << MinProduct();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above approach

import java.util.ArrayList;
import java.util.Collections;

public class Product {

    // to store first vertex, second vertex and weight of
    // the edge
    static class Edge implements Comparable<Edge> {
        int first, second, weight;
        Edge(int x, int y, int w)
        {
            this.first = x;
            this.second = y;
            this.weight = w;
        }

        @Override public int compareTo(Edge edge)
        {
            return this.weight - edge.weight;
        }
    }

    static int mod = 1000000007;

    // Function to return (x^y) mod p
    static int power(int x, int y, int p)
    {
        int res = 1;
        x = x % p;
        while (y > 0) {
            if ((y & 1) == 1)
                res = (res * x) % p;
            y = y >> 1;
            x = (x * x) % p;
        }
        return res;
    }

    // Declaring size array globally
    static int size[] = new int[300005];
    static int freq[] = new int[300004];
    static ArrayList<Edge> edges = new ArrayList<Edge>();

    // Initializing DSU data structure
    static void initialize(int Arr[], int N)
    {
        for (int i = 0; i < N; i++) {
            Arr[i] = i;
            size[i] = 1;
        }
    }

    // Function to find the root of ith
    // node in the disjoint set
    static int root(int Arr[], int i)
    {
        while (Arr[i] != i) {
            i = Arr[i];
        }
        return i;
    }

    // Weighted union using Path Compression
    static void weighted_union(int Arr[], int size[], int A,
                               int B)
    {
        int root_A = root(Arr, A);
        int root_B = root(Arr, B);

        // size of set A is small than size of set B
        if (size[root_A] < size[root_B]) {
            Arr[root_A] = Arr[root_B];
            size[root_B] += size[root_A];
        }

        // size of set B is small than size of set A
        else {
            Arr[root_B] = Arr[root_A];
            size[root_A] += size[root_B];
        }
    }

    // Function to add an edge in the tree
    static void AddEdge(int a, int b, int w)
    {
        edges.add(new Edge(a, b, w));
    }

    // Build the tree
    static void MakeTree()
    {
        AddEdge(1, 2, 1);
        AddEdge(1, 3, 3);
        AddEdge(3, 4, 2);
    }

    // Function to return the required product
    static int MinProduct()
    {
        int result = 1;

        // Sorting the edges with respect to its weight
        // ascending order
        Collections.sort(edges);

        // Start iterating in decreasing order of weight
        for (int i = edges.size() - 1; i >= 0; i--) {

            // Determine Current edge values
            int curr_weight = edges.get(i).weight;
            int Node1 = edges.get(i).first;
            int Node2 = edges.get(i).second;

            // Calculate root of each node
            // and size of each set
            int Root1 = root(freq, Node1);
            int Set1_size = size[Root1];
            int Root2 = root(freq, Node2);
            int Set2_size = size[Root2];

            // Using the formula
            int prod = Set1_size * Set2_size;
            int Product = power(curr_weight, prod, mod);

            // Calculating final result
            result
                = ((result % mod) * (Product % mod)) % mod;

            // Weighted union using Path Compression
            weighted_union(freq, size, Node1, Node2);
        }
        return result % mod;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        initialize(freq, n);
        MakeTree();
        System.out.println(MinProduct());
    }
}

// This code is contributed by jainlovely450
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 1000000007

# Function to return (x^y) mod p
def power(x: int, y: int, p: int) -> int:
    res = 1
    x %= p
    while y > 0:
        if y & 1:
            res = (res * x) % p
        y = y // 2
        x = (x * x) % p
    return res

# Declaring size array globally
size = [0] * 300005
freq = [0] * 300004
edges = []

# Initializing DSU data structure
def initialize(arr: list, N: int):
    for i in range(N):
        arr[i] = i
        size[i] = 1

# Function to find the root of ith
# node in the disjoint set
def root(arr: list, i: int) -> int:
    while arr[i] != i:
        i = arr[i]
    return i

# Weighted union using Path Compression
def weighted_union(arr: list, size: list, A: int, B: int):
    root_A = root(arr, A)
    root_B = root(arr, B)

    # size of set A is small than size of set B
    if size[root_A] < size[root_B]:
        arr[root_A] = arr[root_B]
        size[root_B] += size[root_A]

    # size of set B is small than size of set A
    else:
        arr[root_B] = arr[root_A]
        size[root_A] += size[root_B]

# Function to add an edge in the tree
def AddEdge(a: int, b: int, w: int):
    edges.append((w, (a, b)))

# Build the tree
def makeTree():
    AddEdge(1, 2, 1)
    AddEdge(1, 3, 3)
    AddEdge(3, 4, 2)

# Function to return the required product
def minProduct() -> int:
    result = 1

    # Sorting the edges with respect to its weight
    edges.sort(key = lambda a: a[0])

    # Start iterating in decreasing order of weight
    for i in range(len(edges) - 1, -1, -1):

        # Determine Current edge values
        curr_weight = edges[i][0]
        node1 = edges[i][1][0]
        node2 = edges[i][1][1]

        # Calculate root of each node
        # and size of each set
        root1 = root(freq, node1)
        set1_size = size[root1]
        root2 = root(freq, node2)
        set2_size = size[root2]

        # Using the formula
        prod = set1_size * set2_size
        product = power(curr_weight, prod, mod)

        # Calculating final result
        result = ((result % mod) * (product % mod)) % mod

        # Weighted union using Path Compression
        weighted_union(freq, size, node1, node2)

    return result % mod

# Driver Code
if __name__ == "__main__":

    # Number of nodes and edges
    n = 4
    initialize(freq, n)
    makeTree()
    print(minProduct())

# This code is contributed by
# sanjeev2552
```

**Output:** 

```
12
```

**时间复杂度:** O(N*logN)