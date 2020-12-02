# 数组中的魔法指数

> 原文： [https://www.geeksforgeeks.org/magical-indices-array/](https://www.geeksforgeeks.org/magical-indices-array/)

给定整数数组 A。 如果 j =（i + A [i]）％n +1（假设基于 1 的索引），则认为 A 的索引 i 与索引 j 连接。 从索引 i 开始遍历数组，然后跳转到下一个连接的索引。 如果按所描述的顺序遍历数组，则再次访问索引 i，则索引 i 是一个神奇的索引。 计算数组中的魔术索引数。 假设数组 A 由非负整数组成。

**示例：**

```
Input : A = {1, 1, 1, 1}
Output : 4
Possible traversals:
1 -> 3 -> 1
2 -> 4 -> 2
3 -> 1 -> 3
4 -> 2 -> 4
Clearly all the indices are magical

Input : A = {0, 0, 0, 2}
Output : 2
Possible traversals:
1 -> 2 -> 3 -> 4 -> 3...
2 -> 3 -> 4 -> 3...
3 -> 4 -> 3
4 -> 3 ->4
Magical indices = 3, 4

```

**方法：**问题是要计算图中显示的所有循环中的节点数。 每个索引代表图的单个节点。 如问题陈述中所述，每个节点都有一个有向边。 此图具有特殊的属性：从任何顶点开始遍历时，始终会检测到一个循环。 此属性将有助于减少解决方案的时间复杂度。

阅读有关如何在有向图中检测周期的信息：[在有向图](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)中检测周期

让遍历从节点 i 开始。 节点 i 将被称为该遍历的父节点，并且该父节点将被分配给遍历期间访问的所有节点。 在遍历图形时，如果我们发现一个已经访问过的节点，并且该访问节点的父节点与遍历的父节点相同，则将检测到一个新的周期。 要计算此循环中的节点数，请从该节点启动另一个 dfs，直到不再访问同一节点为止。 对图的每个节点 i 重复此过程。 在最坏的情况下，每个节点最多将遍历 3 次。 因此，解决方案具有线性时间复杂度。

逐步算法为：

```
1\. For each node in the graph:
     if node i is not visited then:
       for every adjacent node j:
         if node j is not visited:
            par[j] = i
         else:
           if par[j]==i
             cycle detected
             count nodes in cycle
2\. return count       

```

**实施：**

## C ++

```

// C++ program to find number of magical  
// indices in the given array. 
#include <bits/stdc++.h> 
using namespace std; 

#define mp make_pair 
#define pb push_back 
#define mod 1000000007 

// Function to count number of magical indices. 
int solve(int A[], int n) 
{ 
    int i, cnt = 0, j; 

    // Array to store parent node of traversal. 
    int parent[n + 1]; 

    // Array to determine whether current node 
    // is already counted in the cycle. 
    int vis[n + 1]; 

    // Initialize the arrays. 
    memset(parent, -1, sizeof(parent)); 
    memset(vis, 0, sizeof(vis)); 

    for (i = 0; i < n; i++) { 
        j = i; 

        // Check if current node is already 
        // traversed or not. If node is not 
        // traversed yet then parent value 
        // will be -1\. 
        if (parent[j] == -1) { 

            // Traverse the graph until an 
            // already visited node is not 
            // found. 
            while (parent[j] == -1) { 
                parent[j] = i; 
                j = (j + A[j] + 1) % n; 
            } 

            // Check parent value to ensure 
            // a cycle is present. 
            if (parent[j] == i) { 

                // Count number of nodes in 
                // the cycle. 
                while (!vis[j]) { 
                    vis[j] = 1; 
                    cnt++; 
                    j = (j + A[j] + 1) % n; 
                } 
            } 
        } 
    } 

    return cnt; 
} 

int main() 
{ 
    int A[] = { 0, 0, 0, 2 }; 
    int n = sizeof(A) / sizeof(A[0]); 
    cout << solve(A, n); 
    return 0; 
} 

```