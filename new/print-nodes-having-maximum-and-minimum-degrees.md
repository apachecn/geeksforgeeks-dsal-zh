# 具有最大和最小度数的打印节点

> 原文： [https://www.geeksforgeeks.org/print-nodes-having-maximum-and-minimum-degrees/](https://www.geeksforgeeks.org/print-nodes-having-maximum-and-minimum-degrees/)

给定具有 **N** 个节点的无向​​图，任务是打印具有最小和最大度数的节点。

**示例：**

```
Input:
1-----2
|     |
3-----4
Output:
Nodes with maximum degree : 1 2 3 4 
Nodes with minimum degree : 1 2 3 4 
Every node has a degree of 2.

Input:
    1
   / \
  2   3
 /
4
Output:
Nodes with maximum degree : 1 2 
Nodes with minimum degree : 3 4 

```

**方法：**对于无向图，节点的度是入射到其上的边的数量，因此可以通过计算边列表中的频率来计算每个节点的度。 因此，该方法是使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)从边缘列表计算每个顶点的频率，并使用该映射查找具有最大和最小度数的节点。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print the nodes having 
// maximum and minimum degree 
void minMax(int edges[][2], int len, int n) 
{ 

    // Map to store the degrees of every node 
    map<int, int> m; 

    for (int i = 0; i < len; i++) { 

        // Storing the degree for each node 
        m[edges[i][0]]++; 
        m[edges[i][1]]++; 
    } 

    // maxi and mini variables to store 
    // the maximum and minimum degree 
    int maxi = 0; 
    int mini = n; 

    for (int i = 1; i <= n; i++) { 
        maxi = max(maxi, m[i]); 
        mini = min(mini, m[i]); 
    } 

    // Printing all the nodes with maximum degree 
    cout << "Nodes with maximum degree : "; 
    for (int i = 1; i <= n; i++) { 
        if (m[i] == maxi) 
            cout << i << " "; 
    } 
    cout << endl; 

    // Printing all the nodes with minimum degree 
    cout << "Nodes with minimum degree : "; 
    for (int i = 1; i <= n; i++) { 
        if (m[i] == mini) 
            cout << i << " "; 
    } 
} 

// Driver code 
int main() 
{ 

    // Count of nodes and edges 
    int n = 4, m = 6; 

    // The edge list 
    int edges[][2] = { { 1, 2 }, 
                       { 1, 3 }, 
                       { 1, 4 }, 
                       { 2, 3 }, 
                       { 2, 4 }, 
                       { 3, 4 } }; 

    minMax(edges, m, 4); 

    return 0; 
} 

```