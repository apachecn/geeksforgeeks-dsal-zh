# 求 K 个查询数组中所有唯一元素的和

> 原文:[https://www . geeksforgeeks . org/find-k 查询数组中所有唯一元素的总和/](https://www.geeksforgeeks.org/find-sum-of-all-unique-elements-in-the-array-for-k-queries/)

给定一个数组**arr【】**，其中最初所有元素都是 **0** 和另一个数组**Q【】【】**包含 **K** 查询，其中每个查询代表一个范围**【L，R】**，任务是将 **1** 添加到每个子阵列，其中每个子阵列由范围**【L，R】**定义，并返回所有**唯一**元素的总和。
**注意:**在 **Q[][]** 数组中使用基于一的索引来表示范围。
**例:**

> **输入:** arr[] = { 0，0，0，0，0，0 }，Q[][2] = {{1，3}，{4，6}，{3，4}，{3，3}}
> **输出:** 6
> **解释:**
> 最初数组为 arr[] = { 0，0，0，0，0，0 }。
> **查询 1:** arr[] = { 1，1，1，0，0，0 }。
> **查询 2:** arr[] = { 1，1，1，1，1，1 }。
> **查询 3:** arr[] = { 1，1，2，2，1，1 }。
> **查询 4:** arr[] = { 1，1，3，2，1，1 }。
> 因此独特的元素是{1，3，2}。因此总和= 1 + 3 + 2 = 6。
> **输入:** arr[] = { 0，0，0，0，0，0，0，0 }，Q[][2] = {{1，4}，{5，5}，{7，8}，{8，8}}
> **输出:** 3
> **解释:**
> 最初数组为 arr[] = { 0，0，0，0，0，0，0，0，0，{ 0 }。
> 处理完所有查询后，arr[] = { 1，1，1，1，1，0，1，2 }。
> 因此唯一的元素是{1，0，2}。因此总和= 1 + 0 + 2 = 3。

**方法:**思路是在 **L** 和 **R+1** 索引处分别递增 1 和递减 1 来处理每个查询。然后，计算数组的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，找到 Q 查询后的最终数组。正如[这篇](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)文章所解释的。最后，借助[散列图](https://www.geeksforgeeks.org/hashing-data-structure/)计算唯一元素的总和。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// sum of all unique elements of
// the array after Q queries

#include <bits/stdc++.h>

using namespace std;

// Function to find the sum of
// unique elements after Q Query
int uniqueSum(int A[], int R[][2],
            int N, int M)
{
    // Updating the array after
    // processing each query
    for (int i = 0; i < M; ++i) {

        int l = R[i][0], r = R[i][1] + 1;

        // Making it to 0-indexing
        l--;
        r--;
        A[l]++;

        if (r < N)
            A[r]--;
    }

    // Iterating over the array
    // to get the final array
    for (int i = 1; i < N; ++i) {
        A[i] += A[i - 1];
    }

    // Variable to store the sum
    int ans = 0;

    // Hash to maintain previously
    // occured elements
    unordered_set<int> s;

    // Loop to find the maximum sum
    for (int i = 0; i < N; ++i) {

        if (s.find(A[i]) == s.end())
            ans += A[i];

        s.insert(A[i]);
    }

    return ans;
}

// Driver code
int main()
{
    int A[] = { 0, 0, 0, 0, 0, 0 };
    int R[][2]
        = { { 1, 3 }, { 4, 6 },
            { 3, 4 }, { 3, 3 } };

    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(R) / sizeof(R[0]);

    cout << uniqueSum(A, R, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// sum of all unique elements of
// the array after Q queries

import java.util.*;

class GFG{

// Function to find the sum of
// unique elements after Q Query
static int uniqueSum(int A[], int R[][],
                     int N, int M)
{
    // Updating the array after
    // processing each query
    for (int i = 0; i < M; ++i)
    {
        int l = R[i][0], r = R[i][1] + 1;

        // Making it to 0-indexing
        l--;
        r--;
        A[l]++;

        if (r < N)
            A[r]--;
    }

    // Iterating over the array
    // to get the final array
    for (int i = 1; i < N; ++i)
    {
        A[i] += A[i - 1];
    }

    // Variable to store the sum
    int ans = 0;

    // Hash to maintain previously
    // occured elements
    HashSet<Integer> s = new HashSet<Integer>();

    // Loop to find the maximum sum
    for (int i = 0; i < N; ++i)
    {
        if (!s.contains(A[i]))
            ans += A[i];

        s.add(A[i]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 0, 0, 0, 0, 0, 0 };
    int R[][] = { { 1, 3 }, { 4, 6 },
                  { 3, 4 }, { 3, 3 } };
    int N = A.length;
    int M = R.length;
    System.out.print(uniqueSum(A, R, N, M));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python implementation to find the
# sum of all unique elements of
# the array after Q queries

# Function to find the sum of
# unique elements after Q Query
def uniqueSum(A, R, N, M) :

    # Updating the array after
    # processing each query
    for i in range(0, M) :

        l = R[i][0]
        r = R[i][1] + 1

        # Making it to 0-indexing
        l -= 1
        r -= 1
        A[l] += 1

        if (r < N) :
            A[r] -= 1

    # Iterating over the array
    # to get the final array
    for i in range(1, N) :
        A[i] += A[i - 1]

    # Variable to store the sum
    ans = 0

    # Hash to maintain previously
    # occured elements
    s = {chr}

    # Loop to find the maximum sum
    for i in range(0, N) :
        if (A[i] not in s) :
            ans += A[i]

        s.add(A[i])

    return ans

# Driver code
A = [ 0, 0, 0, 0, 0, 0 ]
R = [ [ 1, 3 ], [ 4, 6 ],
      [ 3, 4 ], [ 3, 3 ] ]
N = len(A)
M = len(R)

print(uniqueSum(A, R, N, M))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to find the
// sum of all unique elements of
// the array after Q queries
using System;
using System.Collections.Generic;

class GFG{

// Function to find the sum of
// unique elements after Q Query
static int uniqueSum(int []A, int [,]R,
                     int N, int M)
{

    // Updating the array after
    // processing each query
    for(int i = 0; i < M; ++i)
    {
       int l = R[i, 0], r = R[i, 1] + 1;

       // Making it to 0-indexing
       l--;
       r--;
       A[l]++;

       if (r < N)
           A[r]--;
    }

    // Iterating over the array
    // to get the readonly array
    for(int i = 1; i < N; ++i)
    {
       A[i] += A[i - 1];
    }

    // Variable to store the sum
    int ans = 0;

    // Hash to maintain previously
    // occured elements
    HashSet<int> s = new HashSet<int>();

    // Loop to find the maximum sum
    for(int i = 0; i < N; ++i)
    {
       if (!s.Contains(A[i]))
           ans += A[i];
       s.Add(A[i]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []A = { 0, 0, 0, 0, 0, 0 };
    int [,]R = { { 1, 3 }, { 4, 6 },
                 { 3, 4 }, { 3, 3 } };

    int N = A.Length;
    int M = R.GetLength(0);

    Console.Write(uniqueSum(A, R, N, M));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// sum of all unique elements of
// the array after Q queries

// Function to find the sum of
// unique elements after Q Query
function uniqueSum(A, R, N, M)
{

    // Updating the array after
    // processing each query
    for (let i = 0; i < M; ++i)
    {
        let l = R[i][0], r = R[i][1] + 1;

        // Making it to 0-indexing
        l--;
        r--;
        A[l]++;

        if (r < N)
            A[r]--;
    }

    // Iterating over the array
    // to get the final array
    for (let i = 1; i < N; ++i)
    {
        A[i] += A[i - 1];
    }

    // Variable to store the sum
    let ans = 0;

    // Hash to maintain previously
    // occured elements
    let s = new Set();

    // Loop to find the maximum sum
    for (let i = 0; i < N; ++i)
    {
        if (!s.has(A[i]))
            ans += A[i];

        s.add(A[i]);
    }
    return ans;
}

// Driver code
      let A = [ 0, 0, 0, 0, 0, 0 ];
    let R = [[ 1, 3 ], [ 4, 6 ],
                  [ 3, 4 ], [ 3, 3 ]];
    let N = A.length;
    let M = R.length;
    document.write(uniqueSum(A, R, N, M));

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
6
```

时间复杂度:O(M + N)

辅助空间:O(N)