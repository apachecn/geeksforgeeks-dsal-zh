# 使用图表

的不同组的计数

> 原文： [https://www.geeksforgeeks.org/count-of-different-groups-using-graph/](https://www.geeksforgeeks.org/count-of-different-groups-using-graph/)

给定具有`N`个节点的图，这些节点的值分别为`P`或`M`。 还给定 **K 个**整数对，作为**（x，y）**表示图形中的边，使得如果**将**连接到`b`并且`b`连接到`c`，然后`a`和`c`也将连接。

单个连接的组件称为组。 该组可以同时具有`P`和`M`值。 如果`P`的值大于`M`的值，则该组称为`P`，对`M`产生影响。 如果 **P 的**和 **M 的**的数目相等，则称为中性基团。 任务是找到受影响的`P`，受影响的`M`和**中性**组的数量。

**示例**：

> **输入**：节点[] = {P，M，P，M，P}，edges] [] = {
> {1，3}，
> {4，5}，
> {3，5}}
> **输出**：
> P = 1
> M = 1
> N = 0
> 将有两组索引
> {1，3，4，5}和{2}。
> 第一组受 P 影响，
> 第二组受 M 影响。
> 
> **输入**：节点[] = {P，M，P，M，P}，edges [] [] = {
> {1，3}，
> {4，5}} [
> **输出**：
> P = 1
> M = 2
> N = 0

**方法**：构造具有邻接表并从 **1 到 N** 循环并执行 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 并检查 P 和 M 计数的图形更为容易。 ]另一种方法是使用 [DSU](https://www.geeksforgeeks.org/disjoint-set-union-trees-set-1/) ，对其进行一些修改，即大小数组将是**对**，以便它既可以保持 **M 也可以是 P** 的计数。 在这种方法中，由于合并操作将负责连接的组件，因此无需构造图形。 请注意，您应该具有按大小/等级排列的 DSU 知识，以进行优化。

下面是上述方法的实现：

## CPP

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// To store the parents 
// of the current node 
vector<int> par; 

// To store the size of M and P 
vector<pair<int, int> > sz; 

// Function for initialization 
void init(vector<char>& nodes) 
{ 

    // Size of the graph 
    int n = (int)nodes.size(); 

    par.clear(); 
    sz.clear(); 
    par.resize(n + 1); 
    sz.resize(n + 1); 

    for (int i = 0; i <= n; ++i) { 
        par[i] = i; 

        if (i > 0) { 

            // If the node is P 
            if (nodes[i - 1] == 'P') 
                sz[i] = { 0, 1 }; 

            // If the node is M 
            else
                sz[i] = { 1, 0 }; 
        } 
    } 
} 

// To find the parent of 
// the current node 
int parent(int i) 
{ 
    while (par[i] != i) 
        i = par[i]; 
    return i; 
} 

// Merge funtion 
void unin(int a, int b) 
{ 
    a = parent(a); 
    b = parent(b); 

    if (a == b) 
        return; 

    // Total size by adding number of M and P 
    int sz_a = sz[a].first + sz[a].second; 
    int sz_b = sz[b].first + sz[b].second; 

    if (sz_a < sz_b) 
        swap(a, b); 

    par[b] = a; 
    sz[a].first += sz[b].first; 
    sz[a].second += sz[b].second; 
    return; 
} 

// Function to calculate the influenced value 
void influenced(vector<char>& nodes, 
                vector<pair<int, int> > connect) 
{ 

    // Number of nodes 
    int n = (int)nodes.size(); 

    // Initialization function 
    init(nodes); 

    // Size of the connected vector 
    int k = connect.size(); 

    // Performing union operation 
    for (int i = 0; i < k; ++i) { 
        unin(connect[i].first, connect[i].second); 
    } 

    // ne = Number of neutal groups 
    // ma = Number of M influenced groups 
    // pe = Number of P influenced groups 
    int ne = 0, ma = 0, pe = 0; 

    for (int i = 1; i <= n; ++i) { 
        int x = parent(i); 

        if (x == i) { 
            if (sz[i].first == sz[i].second) { 
                ne++; 
            } 
            else if (sz[i].first > sz[i].second) { 
                ma++; 
            } 
            else { 
                pe++; 
            } 
        } 
    } 

    cout << "P = " << pe << "\nM = "
         << ma << "\nN = " << ne << "\n"; 
} 

// Driver code 
int main() 
{ 

    // Nodes at each index ( 1 - base indexing ) 
    vector<char> nodes = { 'P', 'M', 'P', 'M', 'P' }; 

    // Connected Pairs 
    vector<pair<int, int> > connect = { 
        { 1, 3 }, 
        { 3, 5 }, 
        { 4, 5 } 
    }; 

    influenced(nodes, connect); 

    return 0; 
} 

```