# 所有子阵列最大值之和|分治

> 原文:[https://www . geesforgeks . org/所有子阵列的最大值之和-分治/](https://www.geeksforgeeks.org/sum-of-maximum-of-all-subarrays-divide-and-conquer/)

给定一个长度为 N 的数组 arr[]，任务是找出该数组中每个可能子数组的最大元素之和。
**例:**

```
Input : arr[] = {1, 3, 1, 7}
Output : 42
Max of all sub-arrays:
{1} - 1
{1, 3} - 3
{1, 3, 1} - 3
{1, 3, 1, 7} - 7
{3} - 3
{3, 1} - 3
{3, 1, 7} - 7 
{1} - 1
{1, 7} - 7
{7} - 7
1 + 3 + 3 + 7 + 3 + 3 + 7 + 1 + 7 + 7 = 42

Input : arr[] = {1, 1, 1, 1, 1}
Output : 15
```

在这篇[文章](https://www.geeksforgeeks.org/sum-of-maximum-elements-of-all-possible-sub-arrays-of-an-array/)中，我们已经讨论了使用堆栈解决这个问题的 O(N)方法。
**进场:**
在本文中，我们将学习如何使用**分治**来解决这个问题。
我们假设第 i <sup>个</sup>指数的元素是所有元素中最大的。对于任何包含索引“I”的子数组，“I”处的元素将始终是子数组中的最大值。
如果第 i <sup>个</sup>索引处的元素最大，我们可以有把握地说，第 I 个索引处的元素在(i+1)*(N-i)个子阵列中将最大。因此，它总贡献将是 arr[i]*(i+1)*(N-i)。现在，我们将数组分成两部分，(0，i-1)和(i+1，N-1)，并分别对它们应用相同的算法。
所以我们一般的递归关系是:

```
maxSumSubarray(arr, l, r) = arr[i]*(r-i+1)*(i-l+1) 
                            + maxSumSubarray(arr, l, i-1)
                            + maxSumSubarray(arr, i+1, r)
where i is index of maximum element in range [l, r].
```

现在，我们需要一种方法来高效地回答 rangeMax()查询。[段树](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)将是回答这个查询的有效方式。我们最多需要回答这个问题 N 次。因此，我们的分治算法的时间复杂度将为 O(Nlog(N))。
如果我们必须回答“所有子阵列的最小值之和”的问题，那么我们将使用段树来回答 rangeMin()查询。为此，您可以浏览文章[段树范围最小值](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)。
下面是实现代码:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
#define seg_max 51
using namespace std;

// Array to store segment tree.
// In first we will store the maximum
// of a range
// In second, we will store index of
// that range
pair<int, int> seg_tree[seg_max];

// Size of array declared global
// to maintain simplicity in code
int n;

// Function to build segment tree
pair<int, int> buildMaxTree(int l, int r, int i, int arr[])
{
    // Base case
    if (l == r) {
        seg_tree[i] = { arr[l], l };
        return seg_tree[i];
    }

    // Finding the maximum among left and right child
    seg_tree[i] = max(buildMaxTree(l, (l + r) / 2, 2 * i + 1, arr),
                      buildMaxTree((l + r) / 2 + 1, r, 2 * i + 2, arr));

    // Returning the maximum to parent
    return seg_tree[i];
}

// Function to perform range-max query in segment tree
pair<int, int> rangeMax(int l, int r, int arr[],
                        int i = 0, int sl = 0, int sr = n - 1)
{
    // Base cases
    if (sr < l || sl > r)
        return { INT_MIN, -1 };
    if (sl >= l and sr <= r)
        return seg_tree[i];

    // Finding the maximum among left and right child
    return max(rangeMax(l, r, arr, 2 * i + 1, sl, (sl + sr) / 2),
               rangeMax(l, r, arr, 2 * i + 2, (sl + sr) / 2 + 1, sr));
}

// Function to find maximum sum subarray
int maxSumSubarray(int arr[], int l = 0, int r = n - 1)
{
    // base case
    if (l > r)
        return 0;

    // range-max query to determine
    // largest in the range.
    pair<int, int> a = rangeMax(l, r, arr);

    // divide the array in two parts
    return a.first * (r - a.second + 1) * (a.second - l + 1)
           + maxSumSubarray(arr, l, a.second - 1)
           + maxSumSubarray(arr, a.second + 1, r);
}

// Driver Code
int main()
{
    // Input array
    int arr[] = { 1, 3, 1, 7 };

    // Size of array
    n = sizeof(arr) / sizeof(int);

    // Builind the segment-tree
    buildMaxTree(0, n - 1, 0, arr);

    cout << maxSumSubarray(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {
    static class pair {
        int first, second;

        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    static final int seg_max = 51;

    // Array to store segment tree.
    // In first we will store the maximum
    // of a range
    // In second, we will store index of
    // that range
    static pair[] seg_tree = new pair[seg_max];

    // Size of array declared global
    // to maintain simplicity in code
    static int n;

    // Function to build segment tree
    static pair buildMaxTree(int l, int r, int i, int arr[])
    {
        // Base case
        if (l == r) {
            seg_tree[i] = new pair(arr[l], l);
            return seg_tree[i];
        }

        // Finding the maximum among left and right child
        seg_tree[i] = max(buildMaxTree(l, (l + r) / 2, 2 * i + 1, arr),
                buildMaxTree((l + r) / 2 + 1, r, 2 * i + 2, arr));

        // Returning the maximum to parent
        return seg_tree[i];
    }

    // Function to perform range-max query in segment tree
    static pair rangeMax(int l, int r, int arr[],
                        int i, int sl, int sr)
    {
        // Base cases
        if (sr < l || sl > r)
            return new pair(Integer.MIN_VALUE, -1);
        if (sl >= l && sr <= r)
            return seg_tree[i];

        // Finding the maximum among left and right child
        return max(rangeMax(l, r, arr, 2 * i + 1, sl, (sl + sr) / 2),
                rangeMax(l, r, arr, 2 * i + 2, (sl + sr) / 2 + 1, sr));
    }

    static pair max(pair f, pair s) {
        if (f.first > s.first)
            return f;
        else
            return s;
    }

    // Function to find maximum sum subarray
    static int maxSumSubarray(int arr[], int l, int r)
    {
        // base case
        if (l > r)
            return 0;

        // range-max query to determine
        // largest in the range.
        pair a = rangeMax(l, r, arr, 0, 0, n - 1);

        // divide the array in two parts
        return a.first * (r - a.second + 1) * (a.second - l + 1)
                + maxSumSubarray(arr, l, a.second - 1)
                + maxSumSubarray(arr, a.second + 1, r);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input array
        int arr[] = { 1, 3, 1, 7 };

        // Size of array
        n = arr.length;

        // Builind the segment-tree
        buildMaxTree(0, n - 1, 0, arr);

        System.out.print(maxSumSubarray(arr, 0, n - 1));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys

seg_max = 51

# Array to store segment tree.
# In first we will store the maximum
# of a range
# In second, we will store index of
# that range
seg_tree = [[] for i in range(seg_max)]

# Function to build segment tree
def buildMaxTree(l, r, i, arr):
    global n, seg_tree, seg_max
    # Base case
    if l == r:
        seg_tree[i] = [arr[l], l]
        return seg_tree[i]

    # Finding the maximum among left and right child
    seg_tree[i] = max(buildMaxTree(l, int((l + r) / 2), 2 * i + 1, arr), buildMaxTree(int((l + r) / 2) + 1, r, 2 * i + 2, arr))

    # Returning the maximum to parent
    return seg_tree[i]

# Function to perform range-max query in segment tree
def rangeMax(l, r, arr, i, sl, sr):
    global n, seg_tree, seg_max

    # Base cases
    if sr < l or sl > r:
        return [-sys.maxsize, -1]
    if sl >= l and sr <= r:
        return seg_tree[i]

    # Finding the maximum among left and right child
    return max(rangeMax(l, r, arr, 2 * i + 1, sl, int((sl + sr) / 2)), rangeMax(l, r, arr, 2 * i + 2, int((sl + sr) / 2) + 1, sr))

def Max(f, s):
    if f[0] > s[0]:
        return f
    else:
        return s

# Function to find maximum sum subarray
def maxSumSubarray(arr, l, r):
    # base case
    if l > r:
        return 0

    # range-max query to determine
    # largest in the range.
    a = rangeMax(l, r, arr, 0, 0, n - 1)

    # divide the array in two parts
    return a[0] * (r - a[1] + 1) * (a[1] - l + 1) + maxSumSubarray(arr, l, a[1] - 1) + maxSumSubarray(arr, a[1] + 1, r)

# Input array
arr = [ 1, 3, 1, 7 ]

# Size of array
n = len(arr)

# Builind the segment-tree
buildMaxTree(0, n - 1, 0, arr)

print(maxSumSubarray(arr, 0, n - 1))

# This code is contributed by decode2207.
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {
    class pair {
        public int first, second;

        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    static readonly int seg_max = 51;

    // Array to store segment tree.
    // In first we will store the maximum
    // of a range
    // In second, we will store index of
    // that range
    static pair[] seg_tree = new pair[seg_max];

    // Size of array declared global
    // to maintain simplicity in code
    static int n;

    // Function to build segment tree
    static pair buildMaxTree(int l, int r, int i, int []arr)
    {
        // Base case
        if (l == r) {
            seg_tree[i] = new pair(arr[l], l);
            return seg_tree[i];
        }

        // Finding the maximum among left and right child
        seg_tree[i] = max(buildMaxTree(l, (l + r) / 2, 2 * i + 1, arr),
                buildMaxTree((l + r) / 2 + 1, r, 2 * i + 2, arr));

        // Returning the maximum to parent
        return seg_tree[i];
    }

    // Function to perform range-max query in segment tree
    static pair rangeMax(int l, int r, int []arr,
                        int i, int sl, int sr)
    {
        // Base cases
        if (sr < l || sl > r)
            return new pair(int.MinValue, -1);
        if (sl >= l && sr <= r)
            return seg_tree[i];

        // Finding the maximum among left and right child
        return max(rangeMax(l, r, arr, 2 * i + 1, sl, (sl + sr) / 2),
                rangeMax(l, r, arr, 2 * i + 2, (sl + sr) / 2 + 1, sr));
    }

    static pair max(pair f, pair s) {
        if (f.first > s.first)
            return f;
        else
            return s;
    }

    // Function to find maximum sum subarray
    static int maxSumSubarray(int []arr, int l, int r)
    {
        // base case
        if (l > r)
            return 0;

        // range-max query to determine
        // largest in the range.
        pair a = rangeMax(l, r, arr, 0, 0, n - 1);

        // divide the array in two parts
        return a.first * (r - a.second + 1) * (a.second - l + 1)
                + maxSumSubarray(arr, l, a.second - 1)
                + maxSumSubarray(arr, a.second + 1, r);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Input array
        int []arr = { 1, 3, 1, 7 };

        // Size of array
        n = arr.Length;

        // Builind the segment-tree
        buildMaxTree(0, n - 1, 0, arr);

        Console.Write(maxSumSubarray(arr, 0, n - 1));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

class pair
{
    constructor(first,second)
    {
        this.first = first;
            this.second = second;
    }
}

let seg_max = 51;

// Array to store segment tree.
    // In first we will store the maximum
    // of a range
    // In second, we will store index of
    // that range
let seg_tree = new Array(seg_max);

// Size of array declared global
    // to maintain simplicity in code
let n;

// Function to build segment tree
function buildMaxTree(l,r,i,arr)
{
     // Base case
        if (l == r) {
            seg_tree[i] = new pair(arr[l], l);
            return seg_tree[i];
        }

        // Finding the maximum among left and right child
        seg_tree[i] = max(buildMaxTree(l, Math.floor((l + r) / 2),
        2 * i + 1, arr), buildMaxTree(Math.floor((l + r) / 2) +
        1, r, 2 * i + 2, arr));

        // Returning the maximum to parent
        return seg_tree[i];
}

// Function to perform range-max query in segment tree
function rangeMax(l,r,arr,i,sl,sr)
{
    // Base cases
        if (sr < l || sl > r)
            return new pair(Number.MIN_VALUE, -1);
        if (sl >= l && sr <= r)
            return seg_tree[i];

        // Finding the maximum among left and right child
        return max(rangeMax(l, r, arr, 2 * i + 1, sl,
                   Math.floor((sl + sr) / 2)),
                rangeMax(l, r, arr, 2 * i + 2,
                Math.floor((sl + sr) / 2) + 1, sr));
}

function max(f,s)
{
    if (f.first > s.first)
            return f;
        else
            return s;
}

// Function to find maximum sum subarray
function maxSumSubarray(arr,l,r)
{
    // base case
        if (l > r)
            return 0;

        // range-max query to determine
        // largest in the range.
        let a = rangeMax(l, r, arr, 0, 0, n - 1);

        // divide the array in two parts
        return a.first * (r - a.second + 1) * (a.second - l + 1)
                + maxSumSubarray(arr, l, a.second - 1)
                + maxSumSubarray(arr, a.second + 1, r);
}

// Driver Code
// Input array
let arr = [ 1, 3, 1, 7 ];

// Size of array
n = arr.length;

// Builind the segment-tree
buildMaxTree(0, n - 1, 0, arr);

document.write(maxSumSubarray(arr, 0, n - 1));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
42
```

**时间复杂度** : O(Nlog(N))