# 所有树对之间的最小边权重的乘积

> 原文： [https://www.geeksforgeeks.org/product-of-minimum-edge-weight-between-all-pairs-of-a-tree/](https://www.geeksforgeeks.org/product-of-minimum-edge-weight-between-all-pairs-of-a-tree/)

给定一棵具有 N 个顶点和 N-1 个边的树。 让我们定义一个函数 F（a，b），它等于节点 a 和 b 之间的路径中的最小边权重。 任务是计算所有此类 F（a，b）的乘积。 这里 a＆b 是无序对，而 a！= b。

因此，基本上，我们需要找到以下值：

```
                           where 0<=i<j<=n-1.

```

在输入中，我们将得到 N 的值，然后是 N-1 行。 每行包含 3 个整数 u，v，w，表示节点 u 和 v 之间的边，其权重为 w。 由于乘积将非常大，因此请以 10 ^ 9 + 7 为模输出。
**范例**：

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

如果我们仔细观察，就会发现如果有一组节点的最小边权重为 w，并且向该集中添加了一个节点，该节点通过权重 W 的边沿将节点与整个集连接起来，使得 W <w then="" path="" formed="" between="" recently="" added="" node="" to="" all="" nodes="" present="" in="" the="" set="" will="" have="" minimum="" weight="" w.="">因此，在这里我们可以应用[不交集并集](https://www.geeksforgeeks.org/disjoint-set-data-structures/)概念来解决该问题。
首先，根据递减的权重对数据结构进行排序。 最初将所有节点分配为一个集合。 现在，当我们合并两个集合时，请执行以下操作：</w>

```
      Product=(present weight)^(size of set1*size of set2).                    

```

我们将乘积乘以树的所有边。

下面是上述方法的实现：

## C++

```cpp

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

// Bulid the tree 
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

        // Determine Curret edge values 
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