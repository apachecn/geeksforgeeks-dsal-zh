# 将 X 转换为 Y 所需的最少步骤，其中二进制矩阵表示可能的转换

> 原文： [https://www.geeksforgeeks.org/minimum-steps-required-to-convert-x-to-y-where-a-binary-matrix-represents-the-possible-conversions/](https://www.geeksforgeeks.org/minimum-steps-required-to-convert-x-to-y-where-a-binary-matrix-represents-the-possible-conversions/)

给定大小为 NxN 的二进制矩阵，其中 1 表示数字 i 可以转换为 j，而 0 表示数字不能转换为 j。 还给出了两个数字 X（

**示例：**

```
Input: 
{{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 1, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1}
{ 0, 0, 0, 1, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 1, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1}}

X = 2, Y = 3 
Output: 2 
Convert 2 -> 4 -> 3, which is the minimum way possible. 

Input:
{{ 0, 0, 0, 0}
{ 0, 0, 0, 1}
{ 0, 0, 0, 0}
{ 0, 1, 0, 0}}

X = 1, Y = 2
Output: -1 

```

**方法：**此问题是 [Floyd-warshall 算法](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)的变体，其中 i 和 j 之间有权重 1 的边，即 **mat [i] [j] == 1** ，否则它们没有边，我们可以像在 Floyd-Warshall 中一样将边指定为无穷大。 找到解矩阵，如果不是无限的，则返回 **dp [i] [j]** 。 如果它是无限的，则返回 **-1** ，这意味着它们之间没有路径。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the above approach 
#include <bits/stdc++.h> 
using namespace std; 
#define INF 99999 
#define size 10 

int findMinimumSteps(int mat[size][size], int x, int y, int n) 
{ 
    // dist[][] will be the output matrix that 
    // will finally have the shortest 
    // distances between every pair of numbers 
    int dist[n][n], i, j, k; 

    // Initially same as mat 
    for (i = 0; i < n; i++) { 
        for (j = 0; j < n; j++) { 
            if (mat[i][j] == 0) 
                dist[i][j] = INF; 
            else
                dist[i][j] = 1; 

            if (i == j) 
                dist[i][j] = 1; 
        } 
    } 

    // Add all numbers one by one to the set 
    // of intermediate numbers. Before start of  
    // an iteration, we have shortest distances  
    // between all pairs of numbers such that the  
    // shortest distances consider only the numbers  
    // in set {0, 1, 2, .. k-1} as intermediate numbers. 
    // After the end of an iteration, vertex no. k is  
    // added to the set of intermediate numbers and  
    // the set becomes {0, 1, 2, .. k} 
    for (k = 0; k < n; k++) { 

        // Pick all numbers as source one by one 
        for (i = 0; i < n; i++) { 

            // Pick all numbers as destination for the 
            // above picked source 
            for (j = 0; j < n; j++) { 

                // If number k is on the shortest path from 
                // i to j, then update the value of dist[i][j] 
                if (dist[i][k] + dist[k][j] < dist[i][j]) 
                    dist[i][j] = dist[i][k] + dist[k][j]; 
            } 
        } 
    } 

    // If no path 
    if (dist[x][y] < INF) 
        return dist[x][y]; 
    else
        return -1; 
} 

// Driver Code 
int main() 
{ 

    int mat[size][size] = { { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 }, 
                            { 0, 0, 0, 1, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 1, 0, 0, 0, 0, 0, 0, 0, 0 }, 
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 } }; 

    int x = 2, y = 3; 

    cout << findMinimumSteps(mat, x, y, size); 
} 

```