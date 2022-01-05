# 给定 GCD 的最小子阵列

> 原文:[https://www . geesforgeks . org/minist-subarray-with-given-gcd/](https://www.geeksforgeeks.org/smallest-subarray-with-given-gcd/)

给定一个由 n 个数字和一个整数 k 组成的数组 arr[]，求 gcd 等于 k 的最小子数组的长度。
示例:

```
Input: arr[] = {6, 9, 7, 10, 12, 
                24, 36, 27}, 
           K = 3
Output: 2
Explanation: GCD of subarray {6,9} is 3.
GCD of subarray {24,36,27} is also 3,
but {6,9} is the smallest 
```

注:以下方法的时间复杂度分析假设数字是固定大小的，并且找到两个元素的 GCD 需要恒定的时间。

**方法 1**

求所有子阵的 gcd，用 gcd k 跟踪最小长度子阵，时间复杂度为每个子阵 O(n <sup>3</sup> )，O(n <sup>2</sup> )，求一个子阵的 GCD 为 O(n)。

**方法二**

使用基于分段树的方法找到所有子阵列的 GCD，这里讨论。该解决方案的时间复杂度为每个子阵列 O(n <sup>2</sup> logn)，O(n <sup>2</sup> )和 O(logn)，用于使用分段树寻找子阵列的 GCD。

**方法 3**

其思路是利用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)和二分搜索法实现时间复杂度 O(n (logn) <sup>2</sup> 。

1.  如果我们在数组中有任何等于“k”的数字，那么答案是 1，因为 k 的 GCD 是 k。返回 1。
2.  如果没有能被 k 整除的数，那么 GCD 就不存在。返回-1。
3.  如果上述情况都不成立，那么最小子阵的长度要么大于 1，要么不存在 GCD。在这种情况下，我们遵循以下步骤。
    *   构建段树，这样我们就可以使用这里讨论的方法快速找到任何子阵列的 GCD
    *   在建立段树之后，我们将每个索引视为起点，并对终点进行二分搜索法运算，使得这两点之间的子阵列具有 GCD k

以下是上述想法的实现。

## C++

```
// C++ Program to find GCD of a number in a given Range
// using segment Trees
#include <bits/stdc++.h>
using namespace std;

// To store segment tree
int *st;

// Function to find gcd of 2 numbers.
int gcd(int a, int b)
{
    if (a < b)
        swap(a, b);
    if (b==0)
        return a;
    return gcd(b, a%b);
}

/*  A recursive function to get gcd of given
    range of array indexes. The following are parameters for
    this function.

    st    --> Pointer to segment tree
    si --> Index of current node in the segment tree. Initially
               0 is passed as root is always at index 0
    ss & se  --> Starting and ending indexes of the segment
                 represented by current node, i.e., st[index]
    qs & qe  --> Starting and ending indexes of query range */
int findGcd(int ss, int se, int qs, int qe, int si)
{
    if (ss>qe || se < qs)
        return 0;
    if (qs<=ss && qe>=se)
        return st[si];
    int mid = ss+(se-ss)/2;
    return gcd(findGcd(ss, mid, qs, qe, si*2+1),
               findGcd(mid+1, se, qs, qe, si*2+2));
}

//Finding The gcd of given Range
int findRangeGcd(int ss, int se, int arr[], int n)
{
    if (ss<0 || se > n-1 || ss>se)
    {
        cout << "Invalid Arguments" << "\n";
        return -1;
    }
    return findGcd(0, n-1, ss, se, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st
int constructST(int arr[], int ss, int se, int si)
{
    if (ss==se)
    {
        st[si] = arr[ss];
        return st[si];
    }
    int mid = ss+(se-ss)/2;
    st[si] = gcd(constructST(arr, ss, mid, si*2+1),
                 constructST(arr, mid+1, se, si*2+2));
    return st[si];
}

/* Function to construct segment tree from given array.
   This function allocates memory for segment tree and
   calls constructSTUtil() to fill the allocated memory */
int *constructSegmentTree(int arr[], int n)
{
    int height = (int)(ceil(log2(n)));
    int size = 2*(int)pow(2, height)-1;
    st = new int[size];
    constructST(arr, 0, n-1, 0);
    return st;
}

// Returns size of smallest subarray of arr[0..n-1]
// with GCD equal to k.
int findSmallestSubarr(int arr[], int n, int k)
{
    // To check if a multiple of k exists.
    bool found = false;

    // Find if k or its multiple is present
    for (int i=0; i<n; i++)
    {
        // If k is present, then subarray size is 1.
        if (arr[i] == k)
            return 1;

        // Break the loop to indicate presence of a
        // multiple of k.
        if (arr[i] % k == 0)
            found = true;
    }

    // If there was no multiple of k in arr[], then
    // we can't get k as GCD.
    if (found == false)
        return -1;

    // If there is a multiple of k in arr[], build
    // segment tree from given array
    constructSegmentTree(arr, n);

    // Initialize result
    int res = n+1;

    // Now consider every element as starting point
    // and search for ending point using Binary Search
    for (int i=0; i<n-1; i++)
    {
        // a[i] cannot be a starting point, if it is
        // not a multiple of k.
        if (arr[i] % k != 0)
            continue;

        // Initialize indexes for binary search of closest
        // ending point to i with GCD of subarray as k.
        int low = i+1;
        int high = n-1;

        // Initialize closest ending point for i.
        int closest = 0;

        // Binary Search for closest ending point
        // with GCD equal to k.
        while (true)
        {
            // Find middle point and GCD of subarray
            // arr[i..mid]
            int mid = low + (high-low)/2;
            int gcd = findRangeGcd(i, mid, arr, n);

            // If GCD is more than k, look further
            if (gcd > k)
                low = mid;

            // If GCD is k, store this point and look for
            // a closer point
            else if (gcd == k)
            {
                high = mid;
                closest = mid;
            }

            // If GCD is less than, look closer
            else
                high = mid;

            // If termination condition reached, set
            // closest
            if (abs(high-low) <= 1)
            {
                if (findRangeGcd(i, low, arr, n) == k)
                    closest = low;
                else if (findRangeGcd(i, high, arr, n)==k)
                    closest = high;
                break;
            }
        }

        if (closest != 0)
            res = min(res, closest - i + 1);
    }

    // If res was not changed by loop, return -1,
    // else return its value.
    return (res == n+1) ? -1 : res;
}

// Driver program to test above functions
int main()
{
    int n = 8;
    int k = 3;
    int arr[] = {6, 9, 7, 10, 12, 24, 36, 27};
    cout << "Size of smallest sub-array with given"
         << " size is " << findSmallestSubarr(arr, n, k);
    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find GCD of a number in a given Range
// using segment Trees
class GFG 
{

// To store segment tree
static int []st;

// Function to find gcd of 2 numbers.
static int gcd(int a, int b)
{
    if (a < b)
        swap(a, b);
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

private static void swap(int x, int y) 
{
    int temp = x;
    x = y;
    y = temp;
} 
/* A recursive function to get gcd of given
    range of array indexes. The following are parameters for
    this function.

    st --> Pointer to segment tree
    si --> Index of current node in the segment tree. Initially
            0 is passed as root is always at index 0
    ss & se --> Starting and ending indexes of the segment
                represented by current node, i.e., st[index]
    qs & qe --> Starting and ending indexes of query range */
static int findGcd(int ss, int se, int qs, int qe, int si)
{
    if (ss > qe || se < qs)
        return 0;
    if (qs <= ss && qe >= se)
        return st[si];
    int mid = ss + (se - ss) / 2;
    return gcd(findGcd(ss, mid, qs, qe, si * 2 + 1),
            findGcd(mid + 1, se, qs, qe, si * 2 + 2));
}

// Finding The gcd of given Range
static int findRangeGcd(int ss, int se, int arr[], int n)
{
    if (ss < 0 || se > n-1 || ss > se)
    {
        System.out.println("Invalid Arguments");
        return -1;
    }
    return findGcd(0, n - 1, ss, se, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st
static int constructST(int arr[], int ss, int se, int si)
{
    if (ss == se)
    {
        st[si] = arr[ss];
        return st[si];
    }
    int mid = ss + (se - ss) / 2;
    st[si] = gcd(constructST(arr, ss, mid, si * 2 + 1),
                constructST(arr, mid+1, se, si * 2 + 2));
    return st[si];
}

/* Function to construct segment tree from given array.
This function allocates memory for segment tree and
calls constructSTUtil() to fill the allocated memory */
static int []constructSegmentTree(int arr[], int n)
{
    int height = (int)(Math.ceil(Math.log(n)));
    int size = 2*(int)Math.pow(2, height) - 1;
    st = new int[size];
    constructST(arr, 0, n - 1, 0);
    return st;
}

// Returns size of smallest subarray of arr[0..n-1]
// with GCD equal to k.
static int findSmallestSubarr(int arr[], int n, int k)
{
    // To check if a multiple of k exists.
    boolean found = false;

    // Find if k or its multiple is present
    for (int i = 0; i < n; i++)
    {
        // If k is present, then subarray size is 1.
        if (arr[i] == k)
            return 1;

        // Break the loop to indicate presence of a
        // multiple of k.
        if (arr[i] % k == 0)
            found = true;
    }

    // If there was no multiple of k in arr[], then
    // we can't get k as GCD.
    if (found == false)
        return -1;

    // If there is a multiple of k in arr[], build
    // segment tree from given array
    constructSegmentTree(arr, n);

    // Initialize result
    int res = n + 1;

    // Now consider every element as starting point
    // and search for ending point using Binary Search
    for (int i = 0; i < n - 1; i++)
    {
        // a[i] cannot be a starting point, if it is
        // not a multiple of k.
        if (arr[i] % k != 0)
            continue;

        // Initialize indexes for binary search of closest
        // ending point to i with GCD of subarray as k.
        int low = i + 1;
        int high = n - 1;

        // Initialize closest ending point for i.
        int closest = 0;

        // Binary Search for closest ending point
        // with GCD equal to k.
        while (true)
        {
            // Find middle point and GCD of subarray
            // arr[i..mid]
            int mid = low + (high-low)/2;
            int gcd = findRangeGcd(i, mid, arr, n);

            // If GCD is more than k, look further
            if (gcd > k)
                low = mid;

            // If GCD is k, store this point and look for
            // a closer point
            else if (gcd == k)
            {
                high = mid;
                closest = mid;
            }

            // If GCD is less than, look closer
            else
                high = mid;

            // If termination condition reached, set
            // closest
            if (Math.abs(high-low) <= 1)
            {
                if (findRangeGcd(i, low, arr, n) == k)
                    closest = low;
                else if (findRangeGcd(i, high, arr, n)==k)
                    closest = high;
                break;
            }
        }

        if (closest != 0)
            res = Math.min(res, closest - i + 1);
    }

    // If res was not changed by loop, return -1,
    // else return its value.
    return (res == n+1) ? -1 : res;
}

// Driver code
public static void main(String args[]) 
{
    int n = 8;
    int k = 3;
    int arr[] = {6, 9, 7, 10, 12, 24, 36, 27};
    System.out.println("Size of smallest sub-array with given"
        + " size is " + findSmallestSubarr(arr, n, k));
}
}

// This code is contributed by Rajput-Ji

```

## 蟒蛇 3

```
# Python Program to find GCD of a number in a given Range
# using segment Trees

# To store segment tree
st = []

# Function to find gcd of 2 numbers.
def gcd(a: int, b: int) -> int:
    if a < b:
        a, b = b, a
    if b == 0:
        return a
    return gcd(b, a % b)

# A recursive function to get gcd of given
# range of array indexes. The following are parameters for
# this function.

# st --> Pointer to segment tree
# si --> Index of current node in the segment tree. Initially
#             0 is passed as root is always at index 0
# ss & se --> Starting and ending indexes of the segment
#                 represented by current node, i.e., st[index]
# qs & qe --> Starting and ending indexes of query range
def findGcd(ss: int, se: int, qs: int, qe: int, si: int) -> int:
    if ss > qe or se < qs:
        return 0
    if qs <= ss and qe >= se:
        return st[si]
    mid = ss + (se - ss) // 2
    return gcd(findGcd(ss, mid, qs, qe, si * 2 + 1),
            findGcd(mid + 1, se, qs, qe, si * 2 + 2))

# Finding The gcd of given Range
def findRangeGcd(ss: int, se: int, arr: list, n: int) -> int:
    if ss < 0 or se > n - 1 or ss > se:
        print("invalid Arguments")
        return -1
    return findGcd(0, n - 1, ss, se, 0)

# A recursive function that constructs Segment Tree for
# array[ss..se]. si is index of current node in segment
# tree st
def constructST(arr: list, ss: int, se: int, si: int) -> int:
    if ss == se:
        st[si] = arr[ss]
        return st[si]
    mid = ss + (se - ss) // 2
    st[si] = gcd(constructST(arr, ss, mid, si * 2 + 1),
                constructST(arr, mid + 1, se, si * 2 + 2))
    return st[si]

# Function to construct segment tree from given array.
# This function allocates memory for segment tree and
# calls constructSTUtil() to fill the allocated memory
def constructSegmentTree(arr: list, n: int) -> list:
    global st
    from math import ceil, log2, pow

    height = int(ceil(log2(n)))
    size = 2 * int(pow(2, height)) - 1
    st = [0] * size
    constructST(arr, 0, n - 1, 0)
    return st

# Returns size of smallest subarray of arr[0..n-1]
# with GCD equal to k.
def findSmallestSubarr(arr: list, n: int, k: int) -> int:

    # To check if a multiple of k exists.
    found = False

    # Find if k or its multiple is present
    for i in range(n):

        # If k is present, then subarray size is 1.
        if arr[i] == k:
            return 1

        # Break the loop to indicate presence of a
        # multiple of k.
        if arr[i] % k == 0:
            found = True

    # If there was no multiple of k in arr[], then
    # we can't get k as GCD.
    if found == False:
        return -1

    # If there is a multiple of k in arr[], build
    # segment tree from given array
    constructSegmentTree(arr, n)

    # Initialize result
    res = n + 1

    # Now consider every element as starting point
    # and search for ending point using Binary Search
    for i in range(n - 1):

        # a[i] cannot be a starting point, if it is
        # not a multiple of k.
        if arr[i] % k != 0:
            continue

        # Initialize indexes for binary search of closest
        # ending point to i with GCD of subarray as k.
        low = i + 1
        high = n - 1

        # Initialize closest ending point for i.
        closest = 0

        # Binary Search for closest ending point
        # with GCD equal to k.
        while True:

            # Find middle point and GCD of subarray
            # arr[i..mid]
            mid = low + (high - low) // 2
            gcd = findRangeGcd(i, mid, arr, n)

            # If GCD is more than k, look further
            if gcd > k:
                low = mid

            # If GCD is k, store this point and look for
            # a closer point
            elif gcd == k:
                high = mid
                closest = mid

            # If GCD is less than, look closer
            else:
                high = mid

            # If termination condition reached, set
            # closest
            if abs(high - low) <= 1:
                if findRangeGcd(i, low, arr, n) == k:
                    closest = low
                elif findRangeGcd(i, high, arr, n) == k:
                    closest = high
                break
        if closest != 0:
            res = min(res, closest - i + 1)

    # If res was not changed by loop, return -1,
    # else return its value.
    return -1 if res == n + 1 else res

# Driver Code
if __name__ == "__main__":
    n = 8
    k = 3
    arr = [6, 9, 7, 10, 12, 24, 36, 27]
    print("Size of smallest sub-array with given size is",
        findSmallestSubarr(arr, n, k))

# This code is contributed by
# sanjeev2552

```

## C#

```
// C# Program to find GCD of a number in a given Range
// using segment Trees
using System;

class GFG 
{

// To store segment tree
static int []st;

// Function to find gcd of 2 numbers.
static int gcd(int a, int b)
{
    if (a < b)
        swap(a, b);
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

private static void swap(int x, int y) 
{
    int temp = x;
    x = y;
    y = temp;
}

/* A recursive function to get gcd of given
    range of array indexes. The following are parameters for
    this function.

    st --> Pointer to segment tree
    si --> Index of current node in the segment tree. Initially
            0 is passed as root is always at index 0
    ss & se --> Starting and ending indexes of the segment
                represented by current node, i.e., st[index]
    qs & qe --> Starting and ending indexes of query range */
static int findGcd(int ss, int se, int qs, int qe, int si)
{
    if (ss > qe || se < qs)
        return 0;
    if (qs <= ss && qe >= se)
        return st[si];
    int mid = ss + (se - ss) / 2;
    return gcd(findGcd(ss, mid, qs, qe, si * 2 + 1),
            findGcd(mid + 1, se, qs, qe, si * 2 + 2));
}

// Finding The gcd of given Range
static int findRangeGcd(int ss, int se, int []arr, int n)
{
    if (ss < 0 || se > n-1 || ss > se)
    {
        Console.WriteLine("Invalid Arguments");
        return -1;
    }
    return findGcd(0, n - 1, ss, se, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st
static int constructST(int []arr, int ss, int se, int si)
{
    if (ss == se)
    {
        st[si] = arr[ss];
        return st[si];
    }
    int mid = ss + (se - ss) / 2;
    st[si] = gcd(constructST(arr, ss, mid, si * 2 + 1),
                constructST(arr, mid+1, se, si * 2 + 2));
    return st[si];
}

/* Function to construct segment tree from given array.
This function allocates memory for segment tree and
calls constructSTUtil() to fill the allocated memory */
static int []constructSegmentTree(int []arr, int n)
{
    int height = (int)(Math.Ceiling(Math.Log(n)));
    int size = 2*(int)Math.Pow(2, height) - 1;
    st = new int[size];
    constructST(arr, 0, n - 1, 0);
    return st;
}

// Returns size of smallest subarray of arr[0..n-1]
// with GCD equal to k.
static int findSmallestSubarr(int []arr, int n, int k)
{
    // To check if a multiple of k exists.
    bool found = false;

    // Find if k or its multiple is present
    for (int i = 0; i < n; i++)
    {
        // If k is present, then subarray size is 1.
        if (arr[i] == k)
            return 1;

        // Break the loop to indicate presence of a
        // multiple of k.
        if (arr[i] % k == 0)
            found = true;
    }

    // If there was no multiple of k in arr[], then
    // we can't get k as GCD.
    if (found == false)
        return -1;

    // If there is a multiple of k in arr[], build
    // segment tree from given array
    constructSegmentTree(arr, n);

    // Initialize result
    int res = n + 1;

    // Now consider every element as starting point
    // and search for ending point using Binary Search
    for (int i = 0; i < n - 1; i++)
    {
        // a[i] cannot be a starting point, if it is
        // not a multiple of k.
        if (arr[i] % k != 0)
            continue;

        // Initialize indexes for binary search of closest
        // ending point to i with GCD of subarray as k.
        int low = i + 1;
        int high = n - 1;

        // Initialize closest ending point for i.
        int closest = 0;

        // Binary Search for closest ending point
        // with GCD equal to k.
        while (true)
        {
            // Find middle point and GCD of subarray
            // arr[i..mid]
            int mid = low + (high-low)/2;
            int gcd = findRangeGcd(i, mid, arr, n);

            // If GCD is more than k, look further
            if (gcd > k)
                low = mid;

            // If GCD is k, store this point and look for
            // a closer point
            else if (gcd == k)
            {
                high = mid;
                closest = mid;
            }

            // If GCD is less than, look closer
            else
                high = mid;

            // If termination condition reached, set
            // closest
            if (Math.Abs(high-low) <= 1)
            {
                if (findRangeGcd(i, low, arr, n) == k)
                    closest = low;
                else if (findRangeGcd(i, high, arr, n)==k)
                    closest = high;
                break;
            }
        }

        if (closest != 0)
            res = Math.Min(res, closest - i + 1);
    }

    // If res was not changed by loop, return -1,
    // else return its value.
    return (res == n+1) ? -1 : res;
}

// Driver code
public static void Main(String []args) 
{
    int n = 8;
    int k = 3;
    int []arr = {6, 9, 7, 10, 12, 24, 36, 27};
    Console.WriteLine("Size of smallest sub-array with given"
        + " size is " + findSmallestSubarr(arr, n, k));
}
}

/* This code is contributed by PrinciRaj1992 */

```

## java 描述语言

```
<script>

// Javascript Program to find GCD of a number in a given Range
// using segment Trees

// To store segment tree
var st = [];

// Function to find gcd of 2 numbers.
function gcd(a,  b)
{
    if (a < b)
        [a, b] = [b,a];
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

/* A recursive function to get gcd of given
    range of array indexes. The following are parameters for
    this function.

    st --> Pointer to segment tree
    si --> Index of current node in the segment tree. Initially
            0 is passed as root is always at index 0
    ss & se --> Starting and ending indexes of the segment
                represented by current node, i.e., st[index]
    qs & qe --> Starting and ending indexes of query range */
function findGcd(ss, se, qs, qe, si)
{
    if (ss > qe || se < qs)
        return 0;
    if (qs <= ss && qe >= se)
        return st[si];
    var mid = ss + parseInt((se - ss) / 2);
    return gcd(findGcd(ss, mid, qs, qe, si * 2 + 1),
            findGcd(mid + 1, se, qs, qe, si * 2 + 2));
}

// Finding The gcd of given Range
function findRangeGcd(ss, se, arr, n)
{
    if (ss < 0 || se > n-1 || ss > se)
    {
        document.write("Invalid Arguments");
        return -1;
    }
    return findGcd(0, n - 1, ss, se, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st
function constructST(arr, ss, se, si)
{
    if (ss == se)
    {
        st[si] = arr[ss];
        return st[si];
    }
    var mid = ss + parseInt((se - ss) / 2);
    st[si] = gcd(constructST(arr, ss, mid, si * 2 + 1),
                constructST(arr, mid+1, se, si * 2 + 2));
    return st[si];
}

/* Function to construct segment tree from given array.
This function allocates memory for segment tree and
calls constructSTUtil() to fill the allocated memory */
function constructSegmentTree(arr, n)
{
    var height = parseInt(Math.ceil(Math.log(n)));
    var size = 2*parseInt(Math.pow(2, height)) - 1;
    st = Array(size).fill(0);
    constructST(arr, 0, n - 1, 0);
    return st;
}

// Returns size of smallest subarray of arr[0..n-1]
// with GCD equal to k.
function findSmallestSubarr(arr, n, k)
{
    // To check if a multiple of k exists.
    var found = false;

    // Find if k or its multiple is present
    for (var i = 0; i < n; i++)
    {
        // If k is present, then subarray size is 1.
        if (arr[i] == k)
            return 1;

        // Break the loop to indicate presence of a
        // multiple of k.
        if (arr[i] % k == 0)
            found = true;
    }

    // If there was no multiple of k in arr[], then
    // we can't get k as GCD.
    if (found == false)
        return -1;

    // If there is a multiple of k in arr[], build
    // segment tree from given array
    constructSegmentTree(arr, n);

    // Initialize result
    var res = n + 1;

    // Now consider every element as starting point
    // and search for ending point using Binary Search
    for (var i = 0; i < n - 1; i++)
    {
        // a[i] cannot be a starting point, if it is
        // not a multiple of k.
        if (arr[i] % k != 0)
            continue;

        // Initialize indexes for binary search of closest
        // ending point to i with GCD of subarray as k.
        var low = i + 1;
        var high = n - 1;

        // Initialize closest ending point for i.
        var closest = 0;

        // Binary Search for closest ending point
        // with GCD equal to k.
        while (true)
        {
            // Find middle point and GCD of subarray
            // arr[i..mid]
            var mid = low + parseInt((high-low)/2);
            var gcd = findRangeGcd(i, mid, arr, n);

            // If GCD is more than k, look further
            if (gcd > k)
                low = mid;

            // If GCD is k, store this point and look for
            // a closer point
            else if (gcd == k)
            {
                high = mid;
                closest = mid;
            }

            // If GCD is less than, look closer
            else
                high = mid;

            // If termination condition reached, set
            // closest
            if (Math.abs(high-low) <= 1)
            {
                if (findRangeGcd(i, low, arr, n) == k)
                    closest = low;
                else if (findRangeGcd(i, high, arr, n)==k)
                    closest = high;
                break;
            }
        }

        if (closest != 0)
            res = Math.min(res, closest - i + 1);
    }

    // If res was not changed by loop, return -1,
    // else return its value.
    return (res == n+1) ? -1 : res;
}

// Driver code
var n = 8;
var k = 3;
var arr = [6, 9, 7, 10, 12, 24, 36, 27];
document.write("Size of smallest sub-array with given"
    + " size is " + findSmallestSubarr(arr, n, k));

// This code is contributed by itsok.
</script> 
```

**Output**

```
Size of smallest sub-array with given size is 2
```

**例:**

```
arr[] = {6, 9, 7, 10, 12, 24, 36, 27}, K = 3

// Initial value of minLen is equal to size 
// of array
minLen = 8 

No element is equal to k so result is either 
greater than 1 or doesn't exist. 
```

**第一指数**

*   子阵从 1 到 5 的 GCD 是 1。
*   GCD < k
*   子阵从 1 到 3 的 GCD 是 1。
*   GCD < k
*   子阵从 1 到 2 的 GCD 为 3
*   minLen =最小值(8.2)= 2

**第二指数**

*   从 2 到 5 的子阵列的 GCD 是 1
*   GCD < k
*   从 2 到 4 的子阵列的 GCD 是 1
*   GCD < k
*   子阵从 6 到 8 的 GCD 为 3
*   minLen =最小值(2.3)= 2。

**。**

**。**

**。**

**第六指数**

*   子阵从 6 到 7 的 GCD 是 12
*   GCD > k
*   子阵从 6 到 8 的 GCD 为 3
*   minLen =最小值(2.3)= 2

**时间复杂度:** O(n (logn) <sup>2</sup> 、O(n)用于遍历每个索引，O(logn)用于每个子阵列，O(logn)用于每个子阵列的 GCD。
本文由 **Nikhil Tekwani 供稿。**如果你喜欢 GeeksforGeeks，想投稿，也可以写一篇文章，把文章发到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息