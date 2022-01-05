# 在[L，R]

范围内对给定方程求值的查询

> 原文:[https://www . geesforgeks . org/query-to-evaluation-in-range-l-r/](https://www.geeksforgeeks.org/queries-to-evaluate-the-given-equation-in-a-range-l-r/)

给定一个由 **N** 整数和查询 **Q[][]** 组成的数组 **{L，R}** ，其中**0≤L<R≤N–1**，每个查询的任务是计算以下等式:

> **k<sub>l</sub>| k<sub>l+1</sub>|…| k<sub>r–1</sub>**
> 其中**k<sub>I</sub>=(arr[I]^ arr[I+1])|(arr[I]~ arr[I+1])**、
> **"~"** 代表二进制 **XNOR** 、
> **【^】**

**示例:**

> **输入:** arr[] = {5，2，3，0}，Q[][] = {{1，3}，{0，2}}
> **输出:**3 7
> T6】解释:t8】查询 1: L = 1，r = 3:k<sub>1</sub>=(2 ^ 3)|(2 ~ 3)=(3 | 2)= 3，K <sub>2</sub> = (3 ^ 0) | (3 ~ 0) =
> 因此，K<sub>1</sub>| K<sub>2</sub>=(3 | 3)= 3
> 查询 2: L = 0，R = 2 : K <sub>0</sub> = 7，K <sub>1</sub> = 3。
> 因此，K<sub>0</sub>| K<sub>1</sub>=(7 | 3)= 7
> 
> **输入:** arr[] = {4，0，1，2}，Q[][] = {{1，3}}
> **输出:** 3

**天真法:**解决这个问题最简单的方法就是遍历指数**【L，R–1】**，对于每个元素，计算**K<sub>I</sub>T7】，其中 **L ≤ i < R** 。**

***时间复杂度:** O(N * sizeof(Q))*

**高效方法**:优化上述方法，思路是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)或[稀疏表](https://www.geeksforgeeks.org/sparse-table/)。按照以下步骤解决问题:

*   需要进行以下观察:

> **异或**运算只设置那些在**arr<sub>I</sub>T5】或在**arr<sub>I+1</sub>**
> **XNOR**设置那些在两个 **a <sub>i</sub>** 和 **a <sub>i+1</sub>** 中设置或在两个中未设置的位。**

*   取这两个操作的**或**，将设置最高为 **max(MSB(arr <sub>i</sub> )、MSB(arr<sub>I+1</sub>)**中最大值的所有位。
*   因此，使用段树在给定的索引之间找到最大的数字，并将其所有位设置为 1，以获得所需的答案。
*   打印答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to obtain the
// middle index of the range
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/* Recursive function to get the sum of
   values in the given range from the array.
   The following are parameters for this
   function.

    st     -> Pointer to segment tree

    node     -> Index of current node in
                the segment tree

    ss & se -> Starting and ending indexes
               of the segment represented
               by current node, i.e., st[node]

    l & r -> Starting and ending indexes
             of range query */
int MaxUtil(int* st, int ss, int se, int l,
            int r, int node)
{
    // If the segment of this node lies
    // completely within the given range
    if (l <= ss && r >= se)

        // Return maximum in the segment
        return st[node];

    // If the segment of this node lies
    // outside the given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node lies
    // partially in the given range
    int mid = getMid(ss, se);

    return max(MaxUtil(st, ss, mid, l, r,
                       2 * node + 1),
               MaxUtil(st, mid + 1, se, l,
                       r, 2 * node + 2));
}

// Function to return the maximum in the
// range from [l, r]
int getMax(int* st, int n, int l, int r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1 || l > r) {
        printf("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1, l, r, 0);
}

// Function to construct Segment Tree
// for the subarray [ss..se]
int constructSTUtil(int arr[], int ss, int se,
                    int* st, int si)
{
    // For a single element
    if (ss == se) {
        st[si] = arr[ss];
        return arr[ss];
    }

    // Otherwise
    int mid = getMid(ss, se);

    // Recur for left subtree
    st[si] = max(constructSTUtil(arr, ss, mid, st,
                                 si * 2 + 1),

                 // Recur for right subtree
                 constructSTUtil(arr, mid + 1, se,
                                 st, si * 2 + 2));

    return st[si];
}

// Function to construct Segment Tree from
// the given array
int* constructST(int arr[], int n)
{
    // Height of Segment Tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of Segment Tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* st = new int[max_size];

    // Fill the allocated memory
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed Segment Tree
    return st;
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 3, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build the Segment Tree
    // from the given array
    int* st = constructST(arr, n);

    vector<vector<int> > Q = { { 1, 3 }, { 0, 2 } };
    for (int i = 0; i < Q.size(); i++) {

        int max = getMax(st, n, Q[i][0], Q[i][1]);
        int ok = 0;
        for (int i = 30; i >= 0; i--) {
            if ((max & (1 << i)) != 0)
                ok = 1;

            if (!ok)
                continue;

            max |= (1 << i);
        }

        cout << max << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to obtain the
// middle index of the range
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/* Recursive function to get the sum of
   values in the given range from the array.
   The following are parameters for this
   function.

    st    .Pointer to segment tree

    node    .Index of current node in
                the segment tree

    ss & se.Starting and ending indexes
               of the segment represented
               by current node, i.e., st[node]

    l & r.Starting and ending indexes
             of range query */
static int MaxUtil(int[] st, int ss,
                   int se, int l,
                   int r, int node)
{
    // If the segment of this node lies
    // completely within the given range
    if (l <= ss && r >= se)

        // Return maximum in the segment
        return st[node];

    // If the segment of this node lies
    // outside the given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node lies
    // partially in the given range
    int mid = getMid(ss, se);

    return Math.max(MaxUtil(st, ss, mid, l, r,
                                2 * node + 1),
                       MaxUtil(st, mid + 1, se, l,
                             r, 2 * node + 2));
}

// Function to return the maximum in the
// range from [l, r]
static int getMax(int []st, int n,
                  int l, int r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1 || l > r)
    {
        System.out.printf("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1, l, r, 0);
}

// Function to conSegment Tree
// for the subarray [ss..se]
static int constructSTUtil(int arr[], int ss,
                           int se, int[] st,
                           int si)
{
    // For a single element
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // Otherwise
    int mid = getMid(ss, se);

    // Recur for left subtree
    st[si] = Math.max(constructSTUtil(arr, ss, mid, st,
                                            si * 2 + 1),

                      // Recur for right subtree
                      constructSTUtil(arr, mid + 1, se,
                                       st, si * 2 + 2));

    return st[si];
}

// Function to conSegment Tree from
// the given array
static int[] constructST(int arr[], int n)
{
    // Height of Segment Tree
    int x = (int)(Math.ceil(Math.log(n)));

    // Maximum size of Segment Tree
    int max_size = 2 * (int)Math.pow(2, x) - 1;

    // Allocate memory
    int []st = new int[max_size];

    // Fill the allocated memory
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed Segment Tree
    return st;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 2, 3, 0 };
    int n = arr.length;

    // Build the Segment Tree
    // from the given array
    int []st = constructST(arr, n);

    int[][] Q = { { 1, 3 }, { 0, 2 } };
    for (int i = 0; i < Q.length; i++)
    {
        int max = getMax(st, n, Q[i][0], Q[i][1]);
        int ok = 0;
        for (int j = 30; j >= 0; j--)
        {
            if ((max & (1 << j)) != 0)
                ok = 1;

            if (ok<=0)
                continue;

            max |= (1 << j);
        }
        System.out.print(max+ " ");
    }
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to obtain the
# middle index of the range
def getMid(s, e):

    return (s + (e - s) // 2)

def MaxUtil(st, ss, se, l, r, node):

    # If the segment of this node lies
    # completely within the given range
    if (l <= ss and r >= se):

        # Return maximum in the segment
        return st[node]

    # If the segment of this node lies
    # outside the given range
    if (se < l or ss > r):
        return -1

    # If segment of this node lies
    # partially in the given range
    mid = getMid(ss, se)

    return max(MaxUtil(st, ss, mid, l,
                       r, 2 * node + 1),
               MaxUtil(st, mid + 1, se,
                       l, r, 2 * node + 2))

# Function to return the maximum
# in the range from [l, r]
def getMax(st, n, l, r):

    # Check for erroneous input values
    if (l < 0 or r > n - 1 or l > r):
        print("Invalid Input")
        return -1

    return MaxUtil(st, 0, n - 1, l, r, 0)

# Function to conSegment Tree
# for the subarray [ss..se]
def constructSTUtil(arr, ss, se, st, si):

    # For a single element
    if (ss == se):
        st[si] = arr[ss]
        return arr[ss]

    # Otherwise
    mid = getMid(ss, se)

    # Recur for left subtree
    st[si] = max(constructSTUtil(arr, ss, mid, st,
                                 si * 2 + 1),
                 constructSTUtil(arr, mid + 1, se,
                                 st, si * 2 + 2))
    return st[si]

# Function to conSegment Tree
# from the given array
def constructST(arr, n):

    # Height of Segment Tree
    x = (int)(math.ceil(math.log(n)))

    # Maximum size of Segment Tree
    max_size = 2 * (int)(pow(2, x)) - 1

    # Allocate memory
    st = [0] * max_size

    # Fill the allocated memory
    constructSTUtil(arr, 0, n - 1, st, 0)

    # Return the constructed Segment Tree
    return st

# Driver Code
arr = [ 5, 2, 3, 0 ]
n = len(arr)

# Build the Segment Tree
# from the given array
st = constructST(arr, n)

Q = [ [ 1, 3 ], [ 0, 2 ] ]
for i in range(len(Q)):
    Max = getMax(st, n, Q[i][0], Q[i][1])
    ok = 0

    for j in range(30, -1, -1):
        if ((Max & (1 << j)) != 0):
            ok = 1

        if (ok <= 0):
            continue

        Max |= (1 << j)

    print(Max, end = " ")

# This code is contributed by divyesh072019
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

    // Function to obtain the
    // middle index of the range
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    /* Recursive function to get the sum of
    values in the given range from the array.
    The following are parameters for this
    function:
    st--> Pointer to segment tree
    node--> Index of current node
    in segment tree
    ss & se--> Starting and ending indexes
    of the segment represented
    by current node, i.e., st[node]
    l & r--> Starting and ending indexes
    of range query */
    static int MaxUtil(int[] st, int ss, int se,
                       int l, int r, int node)
    {

        // If the segment of this node lies
        // completely within the given range
        if (l <= ss && r >= se)

            // Return maximum in the segment
            return st[node];

        // If the segment of this node lies
        // outside the given range
        if (se < l || ss > r)
            return -1;

        // If segment of this node lies
        // partially in the given range
        int mid = getMid(ss, se);

        return Math.Max(
            MaxUtil(st, ss, mid, l, r, 2 * node + 1),
            MaxUtil(st, mid + 1, se, l, r, 2 * node + 2));
    }

    // Function to return the maximum
    // in the range from [l, r]
    static int getMax(int[] st, int n, int l, int r)
    {
        // Check for erroneous input values
        if (l < 0 || r > n - 1 || l > r)
        {
            Console.Write("Invalid Input");
            return -1;
        }
        return MaxUtil(st, 0, n - 1, l, r, 0);
    }

    // Function to conSegment Tree
    // for the subarray [ss..se]
    static int constructSTUtil(int[] arr, int ss, int se,
                               int[] st, int si)
    {
        // For a single element
        if (ss == se)
        {
            st[si] = arr[ss];
            return arr[ss];
        }

        // Otherwise
        int mid = getMid(ss, se);

        // Recur for left subtree
        st[si] = Math.Max(
            constructSTUtil(arr, ss, mid, st,
                            si * 2 + 1),

            // Recur for right subtree
            constructSTUtil(arr, mid + 1, se, st,
                            si * 2 + 2));
        return st[si];
    }

    // Function to conSegment Tree
    // from the given array
    static int[] constructST(int[] arr, int n)
    {
        // Height of Segment Tree
        int x = (int)(Math.Ceiling(Math.Log(n)));

        // Maximum size of Segment Tree
        int max_size = 2 * (int)Math.Pow(2, x) - 1;

        // Allocate memory
        int[] st = new int[max_size];

        // Fill the allocated memory
        constructSTUtil(arr, 0, n - 1, st, 0);

        // Return the constructed Segment Tree
        return st;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = {5, 2, 3, 0};
        int n = arr.Length;

        // Build the Segment Tree
        // from the given array
        int[] st = constructST(arr, n);

        int[, ] Q = {{1, 3}, {0, 2}};
        for (int i = 0; i < Q.GetLength(0); i++) {
            int max = getMax(st, n, Q[i, 0], Q[i, 1]);
            int ok = 0;
            for (int j = 30; j >= 0; j--) {
                if ((max & (1 << j)) != 0)
                    ok = 1;

                if (ok <= 0)
                    continue;

                max |= (1 << j);
            }
            Console.Write(max + " ");
        }
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to obtain the
// middle index of the range
function getMid(s, e)
{
    return (s + Math.floor((e - s) / 2));
}

/* Recursive function to get the sum of
   values in the given range from the array.
   The following are parameters for this
   function.

    st    .Pointer to segment tree

    node    .Index of current node in
                the segment tree

    ss & se.Starting and ending indexes
               of the segment represented
               by current node, i.e., st[node]

    l & r.Starting and ending indexes
             of range query */
function MaxUtil(st, ss,
                   se, l,
                   r, node)
{
    // If the segment of this node lies
    // completely within the given range
    if (l <= ss && r >= se)

        // Return maximum in the segment
        return st[node];

    // If the segment of this node lies
    // outside the given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node lies
    // partially in the given range
    let mid = getMid(ss, se);

    return Math.max(MaxUtil(st, ss, mid, l, r,
                                2 * node + 1),
                       MaxUtil(st, mid + 1, se, l,
                             r, 2 * node + 2));
}

// Function to return the maximum in the
// range from [l, r]
function getMax(st, n, l, r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1 || l > r)
    {
        document.write("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1, l, r, 0);
}

// Function to conSegment Tree
// for the subarray [ss..se]
function constructSTUtil(arr, ss, se, st,
                           si)
{
    // For a single element
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // Otherwise
    let mid = getMid(ss, se);

    // Recur for left subtree
    st[si] = Math.max(constructSTUtil(arr, ss, mid, st,
                                            si * 2 + 1),

                      // Recur for right subtree
                      constructSTUtil(arr, mid + 1, se,
                                       st, si * 2 + 2));

    return st[si];
}

// Function to conSegment Tree from
// the given array
function constructST(arr, n)
{
    // Height of Segment Tree
    let x = (Math.ceil(Math.log(n)));

    // Maximum size of Segment Tree
    let max_size = 2 * Math.pow(2, x) - 1;

    // Allocate memory
    let st = Array.from({length: max_size}, (_, i) => 0);

    // Fill the allocated memory
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed Segment Tree
    return st;
}

// Driver Code

    let arr = [ 5, 2, 3, 0 ];
    let n = arr.length;

    // Build the Segment Tree
    // from the given array
    let st = constructST(arr, n);

    let Q = [[ 1, 3 ], [ 0, 2 ]];
    for (let i = 0; i < Q.length; i++)
    {
        let max = getMax(st, n, Q[i][0], Q[i][1]);
        let ok = 0;
        for (let j = 30; j >= 0; j--)
        {
            if ((max & (1 << j)) != 0)
                ok = 1;

            if (ok<=0)
                continue;

            max |= (1 << j);
        }
        document.write(max+ " ");
    }

</script>
```

**Output:** 

```
3 7
```

***时间复杂度:**O(N * log(sizeof(Q))*
**辅助空间:** O(N)