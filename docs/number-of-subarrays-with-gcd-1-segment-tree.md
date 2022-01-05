# GCD = 1 的子阵数|段树

> 原文:[https://www . geesforgeks . org/子阵数量-带-gcd-1-段-树/](https://www.geeksforgeeks.org/number-of-subarrays-with-gcd-1-segment-tree/)

给定一个数组 **arr[]** ，任务是找出 GCD 等于 **1** 的子数组的个数。
**例:**

> **输入:** arr[] = {1，1，1}
> **输出:** 6
> 给定阵列的每个单个子阵列的 GCD
> 为 1，总共有 6 个子阵列。
> **输入:** arr[] = {2，2，2}
> **输出:** 0

**方法:**这个问题可以在 **O(NlogN)** 中使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)数据结构来解决。将要构建的段可以用来回答范围-gcd 查询。
现在来了解一下算法。使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决这个问题。在讨论算法之前，让我们先做一些观察。

*   假设 **G** 是子阵**arr【l…r】**的 GCD， **G1** 是子阵**arr【l+1…r】**的 GCD。 **G** 始终小于或等于 **G1** 。
*   假设给定的 **L1** 、 **R1** 是第一个使范围**【L，R】**的 GCD 为 **1** 的指标，那么对于任何大于或等于 **L1** 、 **R2** 的 **L2** 也将大于或等于 **R1** 。

经过以上观察，双指针技术完全有道理，即如果最小的 **R** 的长度
对于索引 **L** 是已知的，那么对于索引 **L + 1** ，搜索需要从 **R** 开始。
以下是上述方法的实施:

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

// Function to find the required count
int findCnt(int* arr, int n)
{
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    int i = 0, j = 0;

    // To store the final answer
    int ans = 0;

    // Looping
    while (i < n) {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n and query(0, n - 1, i, j, 0) != 1)
            j++;

        // Updating the final answer
        ans += (n - j);

        // Increment i
        i++;

        // Update j
        j = max(j, i);
    }

    // Returning the final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << findCnt(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
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
static int query(int l, int r, int l1,
                        int r1, int in)
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

// Function to find the required count
static int findCnt(int[] arr, int n)
{
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    int i = 0, j = 0;

    // To store the final answer
    int ans = 0;

    // Looping
    while (i < n)
    {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n && query(0, n - 1,
                                 i, j, 0) != 1)
            j++;

        // Updating the final answer
        ans += (n - j);

        // Increment i
        i++;

        // Update j
        j = Math.max(j, i);
    }

    // Returning the final answer
    return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 1, 1, 1 };
    int n = arr.length;

    System.out.println(findCnt(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import gcd

maxLen = 30;

# Array to store segment-tree
seg = [0] * (3 * maxLen);

# Function to build segment-tree to
# answer range GCD queries
def build(l, r, i, arr) :

    # Base-case
    if (l == r) :
        seg[i] = arr[l];
        return seg[i];

    # Mid element of the range
    mid = (l + r) // 2;

    # Merging the result of left and right sub-tree
    seg[i] = gcd(build(l, mid, 2 * i + 1, arr),
                 build(mid + 1, r, 2 * i + 2, arr));
    return seg[i];

# Function to perform range GCD queries
def query(l, r, l1, r1, i) :

    # Base-cases
    if (l1 <= l and r <= r1) :
        return seg[i];

    if (l > r1 or r < l1) :
        return 0;

    # Mid-element
    mid = (l + r) // 2;

    # Calling left and right child
    return gcd(query(l, mid, l1, r1, 2 * i + 1),
               query(mid + 1, r, l1, r1, 2 * i + 2));

# Function to find the required count
def findCnt(arr, n) :

    # Building the segment tree
    build(0, n - 1, 0, arr);

    # Two pointer variables
    i = 0; j = 0;

    # To store the final answer
    ans = 0;

    # Looping
    while (i < n) :

        # Incrementing j till we don't get
        # a gcd value of 1
        while (j < n and
               query(0, n - 1, i, j, 0) != 1) :
            j += 1;

        # Updating the final answer
        ans += (n - j);

        # Increment i
        i += 1;

        # Update j
        j = max(j, i);

    # Returning the final answer
    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 1, 1 ];
    n = len(arr);

    print(findCnt(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int maxLen = 30;

// Array to store segment-tree
static int []seg = new int[3 * maxLen];

// Function to build segment-tree to
// answer range GCD queries
static int build(int l, int r,
                 int iN, int[] arr)
{
    // Base-case
    if (l == r)
        return seg[iN] = arr[l];

    // Mid element of the range
    int mid = (l + r) / 2;

    // Merging the result of left and right sub-tree
    return seg[iN] = __gcd(build(l, mid, 2 * iN + 1, arr),
                           build(mid + 1, r, 2 * iN + 2, arr));
}

// Function to perform range GCD queries
static int query(int l, int r, int l1,
                        int r1, int iN)
{
    // Base-cases
    if (l1 <= l && r <= r1)
        return seg[iN];
    if (l > r1 || r < l1)
        return 0;

    // Mid-element
    int mid = (l + r) / 2;

    // Calling left and right child
    return __gcd(query(l, mid, l1, r1, 2 * iN + 1),
                 query(mid + 1, r, l1, r1, 2 * iN + 2));
}

// Function to find the required count
static int findCnt(int[] arr, int n)
{
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    int i = 0, j = 0;

    // To store the final answer
    int ans = 0;

    // Looping
    while (i < n)
    {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n && query(0, n - 1,
                               i, j, 0) != 1)
            j++;

        // Updating the final answer
        ans += (n - j);

        // Increment i
        i++;

        // Update j
        j = Math.Max(j, i);
    }

    // Returning the final answer
    return ans;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1, 1, 1 };
    int n = arr.Length;

    Console.WriteLine(findCnt(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let maxLen = 30;

// Array to store segment-tree
let seg = new Array(3 * maxLen);

// Function to build segment-tree to
// answer range GCD queries
function build(l, r, inn, arr) {
    // Base-case
    if (l == r)
        return seg[inn] = arr[l];

    // Mid element of the range
    let mid = Math.floor((l + r) / 2);

    // Merging the result of left and right sub-tree
    return seg[inn] = __gcd(build(l, mid, 2 * inn + 1, arr),
        build(mid + 1, r, 2 * inn + 2, arr));
}

// Function to perform range GCD queries
function query(l, r, l1, r1, inn) {
    // Base-cases
    if (l1 <= l && r <= r1)
        return seg[inn];
    if (l > r1 || r < l1)
        return 0;

    // Mid-element
    let mid = Math.floor((l + r) / 2);

    // Calling left and right child
    return __gcd(query(l, mid, l1, r1, 2 * inn + 1),
        query(mid + 1, r, l1, r1, 2 * inn + 2));
}

// Function to find the required count
function findCnt(arr, n) {
    // Building the segment tree
    build(0, n - 1, 0, arr);

    // Two pointer variables
    let i = 0, j = 0;

    // To store the final answer
    let ans = 0;

    // Looping
    while (i < n) {

        // Incrementing j till we don't get
        // a gcd value of 1
        while (j < n && query(0, n - 1,
            i, j, 0) != 1)
            j++;

        // Updating the final answer
        ans += (n - j);

        // Increment i
        i++;

        // Update j
        j = Math.max(j, i);
    }

    // Returning the final answer
    return ans;
}

function __gcd(a, b) {
    return b == 0 ? a : __gcd(b, a % b);
}

// Driver code

let arr = [1, 1, 1, 1];
let n = arr.length;

document.write(findCnt(arr, n));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
10
```