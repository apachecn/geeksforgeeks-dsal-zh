# 打印打标机序列中最大度的节点

> 原文： [https://www.geeksforgeeks.org/print-the-node-with-the-maximum-degree-in-the-prufer-sequence/](https://www.geeksforgeeks.org/print-the-node-with-the-maximum-degree-in-the-prufer-sequence/)

给定一棵树的 [Prufer 序列](https://www.geeksforgeeks.org/prufer-code-tree-creation/)，任务是在给出其 Prufer 序列的树中以最大程度打印该节点。 如果有很多节点的最大度数，则打印数量最少的节点。

**示例**：

```
Input: a[] = {4, 1, 3, 4} 
Output: 4
The tree is:
2----4----3----1----5
     |
     6 

Input: a[] = {1, 2, 2} 
Output: 2

```

**简单方法**是使用 Prufer 序列创建树，然后找到所有节点的度，然后在其中找到最大值。

**有效方法**：创建一个**度[]** 数组，其大小比 Prufer 序列的长度大 2，因为 prufer 序列的长度为 **N – 2**`N`是节点数。 首先，用`1`填充度数组。 对 Prufer 序列进行迭代，并增加度表中每个元素的频率。 该方法之所以有效，是因为 Prufer 序列中节点的频率比树中的度数小 1。 现在在度数数组中进行迭代，并找到频率最大的节点，这将是我们的答案。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the node with 
// the maximum degree in the tree 
// whose Prufer sequence is given 
int findMaxDegreeNode(int prufer[], int n) 
{ 
    int nodes = n + 2; 

    // Hash-table to mark the 
    // degree of every node 
    int degree[n + 2 + 1]; 

    // Initially let all the degrees be 1 
    for (int i = 1; i <= nodes; i++) 
        degree[i] = 1; 

    // Increase the count of the degree 
    for (int i = 0; i < n; i++) 
        degree[prufer[i]]++; 

    int maxDegree = 0; 
    int node = 0; 

    // Find the node with maximum degree 
    for (int i = 1; i <= nodes; i++) { 
        if (degree[i] > maxDegree) { 
            maxDegree = degree[i]; 
            node = i; 
        } 
    } 

    return node; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 2, 2 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << findMaxDegreeNode(a, n); 

    return 0; 
} 

```