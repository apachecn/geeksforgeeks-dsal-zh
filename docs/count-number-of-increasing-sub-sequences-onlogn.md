# 计数增加的子序列数:O(NlogN)

> 原文:[https://www . geesforgeks . org/count-递增子序列数-onlogn/](https://www.geeksforgeeks.org/count-number-of-increasing-sub-sequences-onlogn/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找出给定数组中严格递增的子序列的数量。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 7
> 所有递增的子序列将为:
> 1){ 1 }
> 2){ 2 }
> 3){ 3 }
> 4){ 1，2}
> 5) {1，3}
> 6) {2，3}
> 7) {1，2，3}
> 这样，答案= 7

****进场:**一个 O(N <sup>2</sup> 进场已经在[这篇](https://www.geeksforgeeks.org/count-all-increasing-subsequences/)文章中讨论过了。这里，将讨论一种使用分段树数据结构的 O(NlogN)时间方法。
在前一篇文章中，使用的递归关系是:**

> **dp[i] = 1 +总和(dp[j])，其中 i<jarr></jarr>**

**由于整个子阵列 **arr[i+1…n-1]** 正在针对每个状态进行迭代，因此需要额外的 O(N)时间来求解。因此，复杂性是(N <sup>2</sup> )。
这个想法是为了避免为每个状态迭代 O(N)个额外的循环，并将其复杂度降低到 Log(N)。
**假设:**从每个索引‘I’开始严格递增的子序列的数量是已知的，其中 I 大于数字‘k’。
使用上述假设，从索引‘k’开始增加的子序列的数量可以在 log(N)时间中找到。
因此，必须找到所有大于“k”的指数“I”的总和。但是捕获是 arr[i]必须大于 arr[k]。要解决这个问题，可以采取以下措施:**

**1.对于数组的每个元素，其索引都是在数组被排序时找到的。示例–{ 7，8，1，9，4}这里，排名是:**

> **7-> 3
> 8->4
> 1->1
> 9->5
> 4->2**

**2.创建长度为“N”的段树来回答范围和查询。**

**3.在求解索引‘k’的同时回答查询，首先找到 **arr[k]** 的秩。假设排名是 **R** 。然后，在段树中，找到从索引**{ R }到 N-1}** 的范围和。**

**4.然后，段树点更新为**段-(R-1)等于 1 + segtree-query(R，N-1) + segtree-query(R-1，R-1)****

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 10000

// Segment tree array
int seg[3 * N];

// Function for point update in segment tree
int update(int in, int l, int r, int up_in, int val)
{
    // Base case
    if (r < up_in || l > up_in)
        return seg[in];

    // If l==r==up
    if (l == up_in and r == up_in)
        return seg[in] = val;

    // Mid element
    int m = (l + r) / 2;

    // Updating the segment tree
    return seg[in] = update(2 * in + 1, l, m, up_in, val)
                     + update(2 * in + 2, m + 1, r, up_in, val);
}

// Function for the range sum-query
int query(int in, int l, int r, int l1, int r1)
{
    // Base case
    if (l > r)
        return 0;
    if (r < l1 || l > r1)
        return 0;
    if (l1 <= l and r <= r1)
        return seg[in];

    // Mid element
    int m = (l + r) / 2;

    // Calling for the left and the right subtree
    return query(2 * in + 1, l, m, l1, r1)
           + query(2 * in + 2, m + 1, r, l1, r1);
}

// Function to return the count
int findCnt(int* arr, int n)
{
    // Copying array arr to sort it
    int brr[n];
    for (int i = 0; i < n; i++)
        brr[i] = arr[i];

    // Sorting array brr
    sort(brr, brr + n);

    // Map to store the rank of each element
    map<int, int> r;
    for (int i = 0; i < n; i++)
        r[brr[i]] = i + 1;

    // dp array
    int dp[n] = { 0 };

    // To store the final answer
    int ans = 0;

    // Updating the dp array
    for (int i = n - 1; i >= 0; i--) {

        // Rank of the element
        int rank = r[arr[i]];

        // Solving the dp-states using segment tree
        dp[i] = 1 + query(0, 0, n - 1, rank, n - 1);

        // Updating the final answer
        ans += dp[i];

        // Updating the segment tree
        update(0, 0, n - 1, rank - 1,
               dp[i] + query(0, 0, n - 1, rank - 1, rank - 1));
    }

    // Returning the final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 10, 9 };
    int n = sizeof(arr) / sizeof(int);

    cout << findCnt(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static final int N = 10000;

    // Segment tree array
    static int[] seg = new int[3 * N];

    // Function for point update in segment tree
    static int update(int in, int l, int r, int up_in, int val)
    {
        // Base case
        if (r < up_in || l > up_in)
            return seg[in];

        // If l==r==up
        if (l == up_in && r == up_in)
            return seg[in] = val;

        // Mid element
        int m = (l + r) / 2;

        // Updating the segment tree
        return seg[in] = update(2 * in + 1, l, m, up_in, val) +
                update(2 * in + 2, m + 1, r, up_in, val);
    }

    // Function for the range sum-query
    static int query(int in, int l, int r, int l1, int r1)
    {
        // Base case
        if (l > r)
            return 0;
        if (r < l1 || l > r1)
            return 0;
        if (l1 <= l && r <= r1)
            return seg[in];

        // Mid element
        int m = (l + r) / 2;

        // Calling for the left and the right subtree
        return query(2 * in + 1, l, m, l1, r1) +
                query(2 * in + 2, m + 1, r, l1, r1);
    }

    // Function to return the count
    static int findCnt(int[] arr, int n)
    {
        // Copying array arr to sort it
        int[] brr = new int[n];
        for (int i = 0; i < n; i++)
            brr[i] = arr[i];

        // Sorting array brr
        Arrays.sort(brr);

        // Map to store the rank of each element
        HashMap<Integer, Integer> r = new HashMap<Integer, Integer>();
        for (int i = 0; i < n; i++)
            r.put(brr[i], i + 1);

        // dp array
        int dp[] = new int[n];

        // To store the final answer
        int ans = 0;

        // Updating the dp array
        for (int i = n - 1; i >= 0; i--)
        {

            // Rank of the element
            int rank = r.get(arr[i]);

            // Solving the dp-states using segment tree
            dp[i] = 1 + query(0, 0, n - 1, rank, n - 1);

            // Updating the final answer
            ans += dp[i];

            // Updating the segment tree
            update(0, 0, n - 1, rank - 1, dp[i] +
                    query(0, 0, n - 1, rank - 1, rank - 1));
        }

        // Returning the final answer
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 10, 9 };
        int n = arr.length;

        System.out.print(findCnt(arr, n));

    }
}

// This code is contributed by PrinciRaj1992
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

N = 10000

# Segment tree array
seg = [0] * (3 * N)

# Function for point update in segment tree
def update(In, l, r, up_In, val):

    # Base case
    if (r < up_In or l > up_In):
        return seg[In]

    # If l==r==up
    if (l == up_In and r == up_In):
        seg[In] = val
        return val

    # Mid element
    m = (l + r) // 2

    # Updating the segment tree
    seg[In] = update(2 * In + 1, l, m, up_In, val) + update(2 * In + 2, m + 1, r, up_In, val)
    return seg[In]

# Function for the range sum-query
def query(In, l, r, l1, r1):

    # Base case
    if (l > r):
        return 0
    if (r < l1 or l > r1):
        return 0
    if (l1 <= l and r <= r1):
        return seg[In]

    # Mid element
    m = (l + r) // 2

    # CallIng for the left and the right subtree
    return query(2 * In + 1, l, m, l1, r1)+ query(2 * In + 2, m + 1, r, l1, r1)

# Function to return the count
def fIndCnt(arr, n):

    # Copying array arr to sort it
    brr = [0] * n
    for i in range(n):
        brr[i] = arr[i]

    # Sorting array brr
    brr = sorted(brr)

    # Map to store the rank of each element
    r = dict()
    for i in range(n):
        r[brr[i]] = i + 1

    # dp array
    dp = [0] * n

    # To store the final answer
    ans = 0

    # Updating the dp array
    for i in range(n - 1, -1, -1):

        # Rank of the element
        rank = r[arr[i]]

        # Solving the dp-states using segment tree
        dp[i] = 1 + query(0, 0, n - 1, rank, n - 1)

        # UpdatIng the final answer
        ans += dp[i]

        # Updating the segment tree
        update(0, 0, n - 1, rank - 1,dp[i] + query(0, 0, n - 1, rank - 1, rank - 1))

    # Returning the final answer
    return ans

# Driver code

arr = [1, 2, 10, 9]
n = len(arr)

print(fIndCnt(arr, n))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static readonly int N = 10000;

    // Segment tree array
    static int[] seg = new int[3 * N];

    // Function for point update In segment tree
    static int update(int In, int l, int r,
                        int up_in, int val)
    {
        // Base case
        if (r < up_in || l > up_in)
            return seg[In];

        // If l==r==up
        if (l == up_in && r == up_in)
            return seg[In] = val;

        // Mid element
        int m = (l + r) / 2;

        // Updating the segment tree
        return seg[In] = update(2 * In + 1, l, m, up_in, val) +
                update(2 * In + 2, m + 1, r, up_in, val);
    }

    // Function for the range sum-query
    static int query(int In, int l, int r, int l1, int r1)
    {
        // Base case
        if (l > r)
            return 0;
        if (r < l1 || l > r1)
            return 0;
        if (l1 <= l && r <= r1)
            return seg[In];

        // Mid element
        int m = (l + r) / 2;

        // Calling for the left and the right subtree
        return query(2 * In + 1, l, m, l1, r1) +
                query(2 * In + 2, m + 1, r, l1, r1);
    }

    // Function to return the count
    static int findCnt(int[] arr, int n)
    {
        // Copying array arr to sort it
        int[] brr = new int[n];
        for (int i = 0; i < n; i++)
            brr[i] = arr[i];

        // Sorting array brr
        Array.Sort(brr);

        // Map to store the rank of each element
        Dictionary<int, int> r = new Dictionary<int, int>();
        for (int i = 0; i < n; i++)
            r.Add(brr[i], i + 1);

        // dp array
        int []dp = new int[n];

        // To store the readonly answer
        int ans = 0;

        // Updating the dp array
        for (int i = n - 1; i >= 0; i--)
        {

            // Rank of the element
            int rank = r[arr[i]];

            // Solving the dp-states using segment tree
            dp[i] = 1 + query(0, 0, n - 1, rank, n - 1);

            // Updating the readonly answer
            ans += dp[i];

            // Updating the segment tree
            update(0, 0, n - 1, rank - 1, dp[i] +
                    query(0, 0, n - 1, rank - 1, rank - 1));
        }

        // Returning the readonly answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 10, 9 };
        int n = arr.Length;

        Console.Write(findCnt(arr, n));

    }
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

var N = 10000;

// Segment tree array
var seg = Array(3*N).fill(0);

// Function for point update inVal segment tree
function update(inVal, l, r, up_in, val)
{
    // Base case
    if (r < up_in || l > up_in)
        return seg[inVal];

    // If l==r==up
    if (l == up_in && r == up_in)
        return seg[inVal] = val;

    // Mid element
    var m = parseInt((l + r) / 2);

    // Updating the segment tree
    seg[inVal] = update(2 * inVal + 1, l, m, up_in, val)
                     + update(2 * inVal + 2, m + 1, r, up_in, val);
    return seg[inVal];
}

// Function for the range sum-query
function query(inVal, l, r, l1, r1)
{
    // Base case
    if (l > r)
        return 0;
    if (r < l1 || l > r1)
        return 0;
    if (l1 <= l && r <= r1)
        return seg[inVal];

    // Mid element
    var m = parseInt((l + r) / 2);

    // Calling for the left and the right subtree
    return query(2 * inVal + 1, l, m, l1, r1)
           + query(2 * inVal + 2, m + 1, r, l1, r1);
}

// Function to return the count
function findCnt(arr, n)
{
    // Copying array arr to sort it
    var brr = Array(n);
    for (var i = 0; i < n; i++)
        brr[i] = arr[i];

    // Sorting array brr
    brr.sort((a, b)=> a-b);

    // Map to store the rank of each element
    var r = new Map();
    for (var i = 0; i < n; i++)
        r[brr[i]] = i + 1;

    // dp array
    var dp = Array(n).fill(0);

    // To store the final answer
    var ans = 0;

    // Updating the dp array
    for (var i = n - 1; i >= 0; i--) {

        // Rank of the element
        var rank = r[arr[i]];

        // Solving the dp-states using segment tree
        dp[i] = 1 + query(0, 0, n - 1, rank, n - 1);

        // Updating the final answer
        ans += dp[i];

        // Updating the segment tree
        update(0, 0, n - 1, rank - 1,
               dp[i] + query(0, 0, n - 1, rank - 1, rank - 1));
    }

    // Returning the final answer
    return ans;
}

// Driver code
var arr = [1, 2, 10, 9 ];
var n = arr.length;
document.write( findCnt(arr, n));

</script>
```

****Output:** 

```
11
```**