# 最小子阵列，GCD 为 1 |段树

> 原文:[https://www . geesforgeks . org/minist-subarray-with-gcd-as-1-segment-tree/](https://www.geeksforgeeks.org/smallest-subarray-with-gcd-as-1-segment-tree/)

给定一个数组 **arr[]** ，任务是找到 GCD 等于 **1** 的最小子数组。如果没有这样的子阵列，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {2，6，3}
> **输出:** 3
> {2，6，3}是唯一 GCD = 1 的子阵列。
> 
> **输入:** arr[] = {2，2，2}
> **输出:** -1

**方法:**这个问题可以在 **O(NlogN)** 中使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)数据结构来解决。将要构建的段可以用来回答范围-gcd 查询。

现在让我们理解算法。使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决这个问题。在讨论算法之前，让我们先做一些观察。

*   假设 **G** 是子阵**arr【l…r】**的 GCD， **G1** 是子阵**arr【l+1…r】**的 GCD。 **G** 始终小于或等于 **G1** 。
*   假设给定的 **L1** 、 **R1** 是第一个指标，使得范围**【L，R】**的 GCD 为 **1** 比任何大于或等于**的**L2**L1**、 **R2** 也将大于或等于 **R1** 。

经过以上观察，双指针技术完全有道理，即如果对于索引 **L** 已知最小 **R** 的长度，那么对于索引 **L + 1** ，搜索需要从 **R** 开始。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define maxLen 30

// Array to store segment-tree
int seg[3 * maxLen];

// Function to build segment-tree to
// answer range GCD queries
int build(int l, int r, int in, int* arr)
{
    // Base-case
    if (l == r)
        return seg[in] = arr[l];

    // Mid element of the range
    int mid = (l + r) / 2;

    // Merging the result of left and right sub-tree
    return seg[in] = __gcd(build(l, mid, 2 * in + 1, arr),
                           build(mid + 1, r, 2 * in + 2, arr));
}

// Function to perform range GCD queries
int query(int l, int r, int l1, int r1, int in)
{
    // Base-cases
    if (l1 <= l and r <= r1)
        return seg[in];
    if (l > r1 or r < l1)
        return 0;

    // Mid-element
    int mid = (l + r) / 2;

    // Calling left and right child
    return __gcd(query(l, mid, l1, r1, 2 * in + 1),
                 query(mid + 1, r, l1, r1, 2 * in + 2));
}

// Function to find the required length
int findLen(int* arr, int n)
{
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    int i = 0, j = 0;

    // To store the final answer
    int ans = INT_MAX;

    // Looping
    while (i < n) {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n and query(0, n - 1, i, j, 0) != 1)
            j++;

        if (j == n)
            break;

        // Updating the final answer
        ans = min((j - i + 1), ans);

        // Incrementing i
        i++;

        // Updating j
        j = max(j, i);
    }

    // Returning the final answer
    if (ans == INT_MAX)
        return -1;
    else
        return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << findLen(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int maxLen = 30;

// Array to store segment-tree
static int []seg = new int[3 * maxLen];

// Function to build segment-tree to
// answer range GCD queries
static int build(int l, int r,
                 int in, int[] arr)
{
    // Base-case
    if (l == r)
        return seg[in] = arr[l];

    // Mid element of the range
    int mid = (l + r) / 2;

    // Merging the result of left and right sub-tree
    return seg[in] = __gcd(build(l, mid, 2 * in + 1, arr),
                           build(mid + 1, r, 2 * in + 2, arr));
}

// Function to perform range GCD queries
static int query(int l, int r,
                 int l1, int r1, int in)
{
    // Base-cases
    if (l1 <= l && r <= r1)
        return seg[in];
    if (l > r1 || r < l1)
        return 0;

    // Mid-element
    int mid = (l + r) / 2;

    // Calling left and right child
    return __gcd(query(l, mid, l1, r1, 2 * in + 1),
                 query(mid + 1, r, l1, r1, 2 * in + 2));
}

// Function to find the required length
static int findLen(int []arr, int n)
{
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    int i = 0, j = 0;

    // To store the final answer
    int ans = Integer.MAX_VALUE;

    // Looping
    while (i < n)
    {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n && query(0, n - 1,
                              i, j, 0) != 1)
            j++;

        if (j == n)
            break;

        // Updating the final answer
        ans = Math.min((j - i + 1), ans);

        // Incrementing i
        i++;

        // Updating j
        j = Math.max(j, i);
    }

    // Returning the final answer
    if (ans == Integer.MAX_VALUE)
        return -1;
    else
        return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 2, 2 };
    int n = arr.length;

    System.out.println(findLen(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

maxLen = 30

# Array to store segment-tree
seg = [0 for i in range(3 * maxLen)]

# Function to build segment-tree to
# answer range GCD queries
def build(l, r, inn, arr):

    # Base-case
    if (l == r):
        seg[inn] = arr[l]
        return seg[inn]

    # Mid element of the range
    mid = (l + r) // 2

    # Merging the result of
    # left and right sub-tree
    seg[inn] = __gcd(build(l, mid,
                           2 * inn + 1, arr),
                     build(mid + 1, r,
                           2 * inn + 2, arr))

    return seg[inn]

# Function to perform range GCD queries
def query(l, r, l1, r1, inn):

    # Base-cases
    if (l1 <= l and r <= r1):
        return seg[inn]
    if (l > r1 or r < l1):
        return 0

    # Mid-element
    mid = (l + r) // 2

    # Calling left and right child
    x=__gcd(query(l, mid, l1, r1,
                  2 * inn + 1),
            query(mid + 1, r, l1, r1,
                  2 * inn + 2))
    return x

# Function to find the required length
def findLen(arr, n):

    # Buildinng the segment tree
    build(0, n - 1, 0, arr)

    # Two pointer variables
    i = 0
    j = 0

    # To store the final answer
    ans = 10**9

    # Loopinng
    while (i < n):

        # Incrementing j till we
        # don't get a gcd value of 1
        while (j < n and query(0, n - 1,
                               i, j, 0) != 1):
            j += 1

        if (j == n):
            break;

        # Updating the final answer
        ans = minn((j - i + 1), ans)

        # Incrementing i
        i += 1

        # Updating j
        j = max(j, i)

    # Returning the final answer
    if (ans == 10**9):
        return -1
    else:
        return ans

# Driver code
arr = [2, 2, 2]
n = len(arr)

print(findLen(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int maxLen = 30;

    // Array to store segment-tree
    static int []seg = new int[3 * maxLen];

    // Function to build segment-tree to
    // answer range GCD queries
    static int build(int l, int r,
                     int ind, int[] arr)
    {
        // Base-case
        if (l == r)
            return seg[ind] = arr[l];

        // Mid element of the range
        int mid = (l + r) / 2;

        // Merging the result of left and right sub-tree
        return seg[ind] = __gcd(build(l, mid, 2 * ind + 1, arr),
                                build(mid + 1, r, 2 * ind + 2, arr));
    }

    // Function to perform range GCD queries
    static int query(int l, int r,
                     int l1, int r1, int ind)
    {
        // Base-cases
        if (l1 <= l && r <= r1)
            return seg[ind];
        if (l > r1 || r < l1)
            return 0;

        // Mid-element
        int mid = (l + r) / 2;

        // Calling left and right child
        return __gcd(query(l, mid, l1, r1, 2 * ind + 1),
                     query(mid + 1, r, l1, r1, 2 * ind + 2));
    }

    // Function to find the required length
    static int findLen(int []arr, int n)
    {
        // Building the segment tree
        build(0, n - 1, 0, arr);

        // Two pointer variables
        int i = 0, j = 0;

        // To store the final answer
        int ans = int.MaxValue;

        // Looping
        while (i < n)
        {

            // Incrementing j till we don't get
            // a gcd value of 1
            while (j < n && query(0, n - 1,
                                  i, j, 0) != 1)
                j++;

            if (j == n)
                break;

            // Updating the final answer
            ans = Math.Min((j - i + 1), ans);

            // Incrementing i
            i++;

            // Updating j
            j = Math.Max(j, i);
        }

        // Returning the final answer
        if (ans == int.MaxValue)
            return -1;
        else
            return ans;
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);    
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 2, 2 };
        int n = arr.Length;

        Console.WriteLine(findLen(arr, n));
    }
}

// This code is contributed by kanugargng
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let maxLen = 30;
// Array to store segment-tree
let seg = new Array(3 * maxLen);

// Function to build segment-tree to
// answer range GCD queries
function build(l,r,In,arr)
{
    // Base-case
    if (l == r)
        return seg[In] = arr[l];

    // Mid element of the range
    let mid = Math.floor((l + r) / 2);

    // Merging the result of left and right sub-tree
    return seg[In] = __gcd(build(l, mid, 2 * In + 1, arr),
                           build(mid + 1, r, 2 * In + 2, arr));
}

// Function to perform range GCD queries
function query(l,r,l1,r1,In)
{
    // Base-cases
    if (l1 <= l && r <= r1)
        return seg[In];
    if (l > r1 || r < l1)
        return 0;

    // Mid-element
    let mid = Math.floor((l + r) / 2);

    // Calling left and right child
    return __gcd(query(l, mid, l1, r1, 2 * In + 1),
                 query(mid + 1, r, l1, r1, 2 * In + 2));
}

// Function to find the required length
function findLen(arr,n)
{
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    let i = 0, j = 0;

    // To store the final answer
    let ans = Number.MAX_VALUE;

    // Looping
    while (i < n)
    {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n && query(0, n - 1,
                              i, j, 0) != 1)
            j++;

        if (j == n)
            break;

        // Updating the final answer
        ans = Math.min((j - i + 1), ans);

        // Incrementing i
        i++;

        // Updating j
        j = Math.max(j, i);
    }

    // Returning the final answer
    if (ans == Number.MAX_VALUE)
        return -1;
    else
        return ans;
}

function __gcd(a,b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
let arr=[2, 2, 2 ];
let n = arr.length;
document.write(findLen(arr, n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
-1
```