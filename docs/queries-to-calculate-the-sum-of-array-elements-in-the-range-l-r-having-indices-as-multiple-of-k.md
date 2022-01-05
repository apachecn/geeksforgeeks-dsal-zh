# 查询以计算范围[L，R]中的数组元素的和，范围[L，R]的索引是 K 的倍数

> 原文:[https://www . geeksforgeeks . org/查询-计算范围内数组元素的和-l-r-具有作为 k 倍数的索引/](https://www.geeksforgeeks.org/queries-to-calculate-the-sum-of-array-elements-in-the-range-l-r-having-indices-as-multiple-of-k/)

给定一个由 **N** 整数组成的数组**arr【】**和一个由形式为 **(L，R，K)** 的查询组成的矩阵**Q【】【】**，每个查询的任务是计算范围**【L，R】**中的数组元素之和，这些数组元素出现在作为 **K** 和的倍数的索引(*基于 0 的索引*中

**示例:**

> **输入:** arr[]={1，2，3，4，5，6}，Q[][]={{2，5，2}，{0，5，1}}
> **输出:**
> 8
> 21
> **解释:**
> 查询 1:索引(2，4)是范围[2，5]中 K(= 2)的倍数。因此，要求 Sum = 3+5 = 8。
> 查询 2:由于所有指数都是 K 的倍数(= 1)，因此，范围[0，5] = 1 + 2 + 3 + 4 + 5 + 6 所需的总和= 21
> 
> **输入:** arr[]={4，3，5，1，9}，Q[][]={{1，4，1}，{3，4，3}}
> **输出:**
> 18
> 1

**方法:**使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[范围和查询](https://www.geeksforgeeks.org/range-sum-queries-without-updates/)技术可以解决这个问题。按照以下步骤解决问题:

1.  初始化一个大小为**prefixSum【】【】**的矩阵，使得**prefixSum【I】【j】**存储存在于从 **i** 到 **j <sup>th</sup> 索引的倍数的索引中的元素的总和。**
2.  遍历数组并预计算前缀和。
3.  遍历每个查询，打印**prefixSum[K][R]–prefixSum[K][L–1]**的结果。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Query
struct Node {
    int L;
    int R;
    int K;
};

// Function to calculate the sum of array
// elements at indices from range [L, R]
// which are multiples of K for each query
int kMultipleSum(int arr[], Node Query[],
                 int N, int Q)
{
    // Stores Prefix Sum
    int prefixSum[N + 1][N];

    // prefixSum[i][j] : Stores the sum from
    // indices [0, j] which are multiples of i
    for (int i = 1; i <= N; i++) {
        prefixSum[i][0] = arr[0];
        for (int j = 0; j < N; j++) {

            // If index j is a multiple of i
            if (j % i == 0) {

                // Compute prefix sum
                prefixSum[i][j]
                    = arr[j] + prefixSum[i][j - 1];
            }

            // Otherwise
            else {
                prefixSum[i][j]
                    = prefixSum[i][j - 1];
            }
        }
    }

    // Traverse each query
    for (int i = 0; i < Q; i++) {

        // Sum of all indices upto R which
        // are a multiple of K
        int last
            = prefixSum[Query[i].K][Query[i].R];
        int first;

        // Sum of all indices upto L - 1 which
        // are a multiple of K
        if (Query[i].L == 0) {
            first
                = prefixSum[Query[i].K][Query[i].L];
        }
        else {
            first
                = prefixSum[Query[i].K][Query[i].L - 1];
        }

        // Calculate the difference
        cout << last - first << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q = 2;
    Node Query[Q];
    Query[0].L = 2, Query[0].R = 5, Query[0].K = 2;
    Query[1].L = 3, Query[1].R = 5, Query[1].K = 5;
    kMultipleSum(arr, Query, N, Q);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure of a Query
static class Node
{
    int L;
    int R;
    int K;
};

// Function to calculate the sum of array
// elements at indices from range [L, R]
// which are multiples of K for each query
static void kMultipleSum(int arr[], Node Query[],
                         int N, int Q)
{

    // Stores Prefix Sum
    int prefixSum[][] = new int[N + 1][N];

    // prefixSum[i][j] : Stores the sum from
    // indices [0, j] which are multiples of i
    for(int i = 1; i <= N; i++)
    {
        prefixSum[i][0] = arr[0];
        for(int j = 0; j < N; j++)
        {

            // If index j is a multiple of i
            if (j % i == 0)
            {

                // Compute prefix sum
                if (j != 0)
                    prefixSum[i][j] = arr[j] +
                                prefixSum[i][j - 1];
            }

            // Otherwise
            else
            {
                prefixSum[i][j] = prefixSum[i][j - 1];
            }
        }
    }

    // Traverse each query
    for(int i = 0; i < Q; i++)
    {

        // Sum of all indices upto R which
        // are a multiple of K
        int last = prefixSum[Query[i].K][Query[i].R];
        int first;

        // Sum of all indices upto L - 1 which
        // are a multiple of K
        if (Query[i].L == 0)
        {
            first = prefixSum[Query[i].K][Query[i].L];
        }
        else
        {
            first = prefixSum[Query[i].K][Query[i].L - 1];
        }

        // Calculate the difference
        System.out.print(last - first + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = arr.length;
    int Q = 2;

    Node Query[] = new Node[Q];
    for(int i = 0; i < Q; i++)
        Query[i] = new Node();

    Query[0].L = 2;
    Query[0].R = 5;
    Query[0].K = 2;
    Query[1].L = 3;
    Query[1].R = 5;
    Query[1].K = 5;

    kMultipleSum(arr, Query, N, Q);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Structure of a Query
class Node
{
    public int L;
    public int R;
    public int K;
};

// Function to calculate the sum of array
// elements at indices from range [L, R]
// which are multiples of K for each query
static void kMultipleSum(int []arr, Node []Query,
                         int N, int Q)
{

    // Stores Prefix Sum
    int [,]prefixSum = new int[N + 1, N];

    // prefixSum[i,j] : Stores the sum from
    // indices [0, j] which are multiples of i
    for(int i = 1; i <= N; i++)
    {
        prefixSum[i, 0] = arr[0];
        for(int j = 0; j < N; j++)
        {

            // If index j is a multiple of i
            if (j % i == 0)
            {

                // Compute prefix sum
                if (j != 0)
                    prefixSum[i, j] = arr[j] +
                                prefixSum[i, j - 1];
            }

            // Otherwise
            else
            {
                prefixSum[i, j] = prefixSum[i, j - 1];
            }
        }
    }

    // Traverse each query
    for(int i = 0; i < Q; i++)
    {

        // Sum of all indices upto R which
        // are a multiple of K
        int last = prefixSum[Query[i].K,Query[i].R];
        int first;

        // Sum of all indices upto L - 1 which
        // are a multiple of K
        if (Query[i].L == 0)
        {
            first = prefixSum[Query[i].K,Query[i].L];
        }
        else
        {
            first = prefixSum[Query[i].K,Query[i].L - 1];
        }

        // Calculate the difference
        Console.Write(last - first + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6 };
    int N = arr.Length;
    int Q = 2;

    Node []Query = new Node[Q];
    for(int i = 0; i < Q; i++)
        Query[i] = new Node();

    Query[0].L = 2;
    Query[0].R = 5;
    Query[0].K = 2;
    Query[1].L = 3;
    Query[1].R = 5;
    Query[1].K = 5;

    kMultipleSum(arr, Query, N, Q);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
8
6
```

***时间复杂度:** O(N <sup>2</sup> + O(Q))，计算前缀和数组需要 O(N <sup>2</sup> )计算复杂度，每个查询需要 O(1)计算复杂度。*
***辅助空间:** O(N <sup>2</sup> )*