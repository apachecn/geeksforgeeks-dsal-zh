# 给定指数范围内不等于 X 的最小指数

> 原文:[https://www . geesforgeks . org/给定范围内的最小索引不等于 x/](https://www.geeksforgeeks.org/smallest-index-in-given-range-of-indices-which-is-not-equal-to-x/)

给定一个大小为 **N** 的整数数组**arr【】**，以及 **{L，R，X}** 形式的 **Q** 查询，任务是从给定数组中找到 **L** 和 **R** 之间的最小索引，使得 **arr[i]！= X** 。如果数组中没有这样的索引，打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，2，1，1，3，5}，查询[][] = {{0，3，1}，{1，5，2}，{2，3，1}}
> **输出:** 1
> 2
> -1
> **说明:**
> 从 0 到 3 不包含 1 的第一个索引是 1
> 从 1 到 5 不包含 2 的第一个索引是 2
> All 因此，答案是-1。
> 
> **输入:** arr[] = { 1，2，3，2，1，1，3，5}，查询[][] = { { 1，4，2 }，{ 4，5，1 }，{ 2，3，1 }，{ 4，6，1 } }
> T3】输出: 2
> -1
> 2
> 6

**简单方法:**
为每个查询迭代范围**【L，R】**，并检查是否存在不包含 **X** 的索引。如果找到这样的索引，打印该索引。否则，打印 **-1** 。

***时间复杂度:** O (N * Q)*
***辅助空间:** O (1)*

**高效方法:**
对于每个数组元素，通过预计算和存储与当前元素不同的下一个元素的索引，可以进一步优化上述方法，这将每个查询的计算复杂度降低到 O(1)。
按照以下步骤解决问题:

1.  创建一个辅助数组 **nextpos[]** ，为每个数组元素存储与当前元素不同的下一个元素的索引。
2.  现在处理每个查询，首先检查索引 **L** 处的值是否不等于 **X** 。如果是，那么答案将是 **L** 。
3.  否则意味着 **arr[L] = X** 。在这种情况下，我们需要找到下一个与**arr【L】**值不同的指数。这可以从**下一步【L】**获得。
4.  如果**下一个【L】**小于等于 **R** ，则打印下一个【L】。
5.  如果以上两个条件都不满足，则答案为 **-1** 。

插图:

> arr[] = {1，2，1，1，3，5}，query[][] = {{0，3，1}，{1，5，2}，{2，3，1}}
> 对于给定的 arr[]，nextpos[]数组将是{1，2，4，4，5，6}
> 对于第一个查询:L = 0，R = 3，X = 1
> arr[0]= 1 = X
> next pos[0]= 1(<3)
> 因此
> 对于第二个查询:L = 1，R = 5，X = 2
> arr[1]= 2(= X)
> next pos[1]= 2(<5)
> 因此，答案是 2。
> 对于第三个查询:L = 2，R = 3，X = 1
> arr[2]= 1(= X)
> next pos[2]= 4(>R)
> 因此，答案为-1

下面是上述方法的实现:

## C++

```
// C++ Program to find the smallest
// index in the array in the range
// [L, R] which does not contain X

#include <bits/stdc++.h>
using namespace std;

// Precompute the index of next
// different element in the array
// for every array element
void precompute(int nextpos[], int arr[],
                int N)
{
    // Default value
    nextpos[N - 1] = N;

    for (int i = N - 2; i >= 0; i--) {

        // Compute nextpos[i] using
        // nextpos[i+1]
        if (arr[i] == arr[i + 1])
            nextpos[i] = nextpos[i + 1];
        else
            nextpos[i] = i + 1;
    }
}
// Function to return the smallest index
void findIndex(int query[][3], int arr[],
               int N, int Q)
{
    // nextpos[i] will store the next
    // position p where arr[p]!=arr[i]
    int nextpos[N];
    precompute(nextpos, arr, N);

    for (int i = 0; i < Q; i++) {
        int l, r, x;
        l = query[i][0];
        r = query[i][1];
        x = query[i][2];

        int ans = -1;

        // If X is not present at l
        if (arr[l] != x)
            ans = l;

        // Otherwise
        else {

            // Find the index which
            // stores a value different
            // from X
            int d = nextpos[l];

            // If that index is within
            // the range
            if (d <= r)
                ans = d;
        }
        cout << ans << "\n";
    }
}
// Driver Code
int main()
{
    int N, Q;
    N = 6;
    Q = 3;
    int arr[] = { 1, 2, 1, 1, 3, 5 };
    int query[Q][3] = { { 0, 3, 1 },
                        { 1, 5, 2 },
                        { 2, 3, 1 } };

    findIndex(query, arr, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// index in the array in the range
// [L, R] which does not contain X
class GFG{

// Precompute the index of next
// different element in the array
// for every array element
static void precompute(int nextpos[], int arr[],
                       int N)
{

    // Default value
    nextpos[N - 1] = N;

    for(int i = N - 2; i >= 0; i--)
    {

       // Compute nextpos[i] using
       // nextpos[i+1]
       if (arr[i] == arr[i + 1])
           nextpos[i] = nextpos[i + 1];
       else
           nextpos[i] = i + 1;
    }
}

// Function to return the smallest index
static void findIndex(int query[][], int arr[],
                      int N, int Q)
{

    // nextpos[i] will store the next
    // position p where arr[p]!=arr[i]
    int []nextpos = new int[N];
    precompute(nextpos, arr, N);

    for(int i = 0; i < Q; i++)
    {
       int l, r, x;
       l = query[i][0];
       r = query[i][1];
       x = query[i][2];

       int ans = -1;

       // If X is not present at l
       if (arr[l] != x)
           ans = l;

       // Otherwise
       else
       {

           // Find the index which
           // stores a value different
           // from X
           int d = nextpos[l];

           // If that index is within
           // the range
           if (d <= r)
               ans = d;
       }
       System.out.print(ans + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N, Q;
    N = 6;
    Q = 3;

    int arr[] = { 1, 2, 1, 1, 3, 5 };
    int query[][] = { { 0, 3, 1 },
                      { 1, 5, 2 },
                      { 2, 3, 1 } };

    findIndex(query, arr, N, Q);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# index in the array in the range
# [L, R] which does not contain X

# Precompute the index of next
# different element in the array
# for every array element

def precompute(nextpos, arr, N):

    # Default value
    nextpos[N - 1] = N

    for i in range(N - 2, -1, -1):

        # Compute nextpos[i] using
        # nextpos[i+1]
        if arr[i] == arr[i + 1]:
            nextpos[i] = nextpos[i + 1]
        else:
            nextpos[i] = i + 1

# Function to return the smallest index
def findIndex(query, arr, N, Q):

    # nextpos[i] will store the next
    # position p where arr[p]!=arr[i]
    nextpos = [0] * N
    precompute(nextpos, arr, N)

    for i in range(Q):
        l = query[i][0]
        r = query[i][1]
        x = query[i][2]

        ans = -1

        # If X is not present at l
        if arr[l] != x:
            ans = l

        # Otherwise
        else:

            # Find the index which
            # stores a value different
            # from X
            d = nextpos[l]

            # If that index is within
            # the range
            if d <= r:
                ans = d

        print(ans)

# Driver code     
N = 6
Q = 3
arr = [ 1, 2, 1, 1, 3, 5 ]
query = [ [ 0, 3, 1 ],
          [ 1, 5, 2 ],
          [ 2, 3, 1 ] ]

findIndex(query, arr, N, Q)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the smallest
// index in the array in the range
// [L, R] which does not contain X
using System;

class GFG{

// Precompute the index of next
// different element in the array
// for every array element
static void precompute(int []nextpos,
                       int []arr, int N)
{

    // Default value
    nextpos[N - 1] = N;

    for(int i = N - 2; i >= 0; i--)
    {

        // Compute nextpos[i] using
        // nextpos[i+1]
        if (arr[i] == arr[i + 1])
            nextpos[i] = nextpos[i + 1];
        else
            nextpos[i] = i + 1;
    }
}

// Function to return the smallest index
static void findIndex(int [,]query, int []arr,
                      int N, int Q)
{

    // nextpos[i] will store the next
    // position p where arr[p]!=arr[i]
    int []nextpos = new int[N];
    precompute(nextpos, arr, N);

    for(int i = 0; i < Q; i++)
    {
        int l, r, x;
        l = query[i, 0];
        r = query[i, 1];
        x = query[i, 2];

        int ans = -1;

        // If X is not present at l
        if (arr[l] != x)
            ans = l;

        // Otherwise
        else
        {

            // Find the index which
            // stores a value different
            // from X
            int d = nextpos[l];

            // If that index is within
            // the range
            if (d <= r)
                ans = d;
        }
        Console.Write(ans + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N, Q;
    N = 6;
    Q = 3;

    int []arr = { 1, 2, 1, 1, 3, 5 };
    int [,]query = { { 0, 3, 1 },
                     { 1, 5, 2 },
                     { 2, 3, 1 } };

    findIndex(query, arr, N, Q);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript Program to find the smallest
// index in the array in the range
// [L, R] which does not contain X

// Precompute the index of next
// different element in the array
// for every array element
function precompute(nextpos, arr, N)
{
    // Default value
    nextpos[N - 1] = N;

    for (var i = N - 2; i >= 0; i--) {

        // Compute nextpos[i] using
        // nextpos[i+1]
        if (arr[i] == arr[i + 1])
            nextpos[i] = nextpos[i + 1];
        else
            nextpos[i] = i + 1;
    }
}
// Function to return the smallest index
function findIndex(query, arr, N, Q)
{
    // nextpos[i] will store the next
    // position p where arr[p]!=arr[i]
    var nextpos = Array(N);
    precompute(nextpos, arr, N);

    for (var i = 0; i < Q; i++) {
        var l, r, x;
        l = query[i][0];
        r = query[i][1];
        x = query[i][2];

        var ans = -1;

        // If X is not present at l
        if (arr[l] != x)
            ans = l;

        // Otherwise
        else {

            // Find the index which
            // stores a value different
            // from X
            var d = nextpos[l];

            // If that index is within
            // the range
            if (d <= r)
                ans = d;
        }
        document.write( ans + "<br>");
    }
}
// Driver Code
var N, Q;
N = 6;
Q = 3;
var arr = [1, 2, 1, 1, 3, 5];
var query = [ [ 0, 3, 1 ],
                    [ 1, 5, 2 ],
                    [ 2, 3, 1 ] ];
findIndex(query, arr, N, Q);

</script>
```

**Output:** 

```
1
2
-1
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*