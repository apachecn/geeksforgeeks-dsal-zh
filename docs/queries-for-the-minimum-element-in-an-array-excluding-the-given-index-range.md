# 查询数组中的最小元素，不包括给定的索引范围

> 原文:[https://www . geesforgeks . org/查询数组中的最小元素-不包括给定的索引范围/](https://www.geeksforgeeks.org/queries-for-the-minimum-element-in-an-array-excluding-the-given-index-range/)

给定一个由 **N** 整数和 **Q** 查询组成的数组 **arr[]** ，其中每个查询由一个索引范围**【L，R】**组成。对于每个查询，任务是找到数组中的最小元素，不包括给定索引范围内的元素。

**示例:**

> **输入:** arr[] = {3，2，1，4，5}，Q[][] = {{1，2}，{2，3}}
> **输出:**
> 3
> 2
> 查询 1: min(arr[0]，arr[3..4]) = min(3，4，5) = 3
> 查询 2: min(arr[0..1]，arr[4]) = min(3，2，5) = 2
> 
> **输入:** arr[] = {1，2，3，4，5}，Q[][] = {{0，2}}
> **输出:**
> 4

**方法:**在多个查询的情况下，可以构建[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)来找到任何索引范围内的最小元素。现在，对于每个查询[L，R]，不包括该范围的最小元素将是 min(min(arr[0…L-1])，min(arr[R+1…N-1])

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A utility function to get minimum of two numbers
int minVal(int x, int y) { return (x < y) ? x : y; }

// A utility function to get the
// middle index from corner indexes.
int getMid(int s, int e) { return s + (e - s) / 2; }

/* A recursive function to get the
minimum value in a given range
of array indexes. The following
are parameters for this function.

    st --> Pointer to segment tree
    index --> Index of current node in the
        segment tree. Initially 0 is
        passed as root is always at index 0
    ss & se --> Starting and ending indexes
                of the segment represented
                by current node, i.e., st[index]
    qs & qe --> Starting and ending indexes of query range */
int RMQUtil(int* st, int ss, int se, int qs, int qe, int index)
{
    // If segment of this node is a part
    // of given range, then return
    // the min of the segment
    if (qs <= ss && qe >= se)
        return st[index];

    // If segment of this node
    // is outside the given range
    if (se < qs || ss > qe)
        return INT_MAX;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return minVal(RMQUtil(st, ss, mid, qs, qe, 2 * index + 1),
                  RMQUtil(st, mid + 1, se, qs, qe, 2 * index + 2));
}

// Return minimum of elements in range
// from index qs (query start) to
// qe (query end). It mainly uses RMQUtil()
int RMQ(int* st, int n, int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe) {
        cout << "Invalid Input";
        return -1;
    }

    return RMQUtil(st, 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node in segment tree st
int constructSTUtil(int arr[], int ss, int se,
                    int* st, int si)
{
    // If there is one element in array,
    // store it in current node of
    // segment tree and return
    if (ss == se) {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the minimum of two values in this node
    int mid = getMid(ss, se);
    st[si] = minVal(constructSTUtil(arr, ss, mid, st, si * 2 + 1),
                    constructSTUtil(arr, mid + 1, se, st, si * 2 + 2));
    return st[si];
}

/* Function to construct segment tree
from given array. This function allocates
memory for segment tree and calls constructSTUtil() to
fill the allocated memory */
int* constructST(int arr[], int n)
{
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    int* st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver program to test above functions
int main()
{
    int arr[] = { 3, 2, 1, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int queries[][2] = { { 1, 2 }, { 2, 3 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Build segment tree from given array
    int* st = constructST(arr, n);

    // Perform queries
    for (int i = 0; i < q; i++) {

        // Current index range to be exluded
        int L = queries[i][0];
        int R = queries[i][1];

        // Minimum in the left part
        int left = ((L - 1) < 0)
                       ? INT_MAX
                       : RMQ(st, n, 0, L - 1);

        // Minimum in the right part
        int right = ((R + 1) >= n)
                        ? INT_MAX
                        : RMQ(st, n, R + 1, n - 1);

        // Minimum in the array excluding the given range
        int minn = min(left, right);

        // Complete array has been excluded
        if (minn == INT_MAX)
            cout << -1 << endl;
        else
            cout << minn << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

    // A utility function to get minimum of two numbers
    static int minVal(int x, int y) {
        return (x < y) ? x : y;
    }

    // A utility function to get the
    // middle index from corner indexes.
    static int getMid(int s, int e) {
        return s + (e - s) / 2;
    }

    /*
    * A recursive function to get the minimum value in a given range of array
    * indexes. The following are parameters for this function.
    *
    * st --> Pointer to segment tree
    * index --> Index of current node in the
    *         segment tree. Initially 0 is passed as
    *         root is always at index 0
    * ss & se --> Starting and ending indexes
    *             of the segment represented
    *             by current node, i.e., st[index]
    * qs & qe --> Starting and ending indexes of query range
    */
    static int RMQUtil(int[] st, int ss, int se,
                        int qs, int qe, int index)
    {
        // If segment of this node is a part
        // of given range, then return
        // the min of the segment
        if (qs <= ss && qe >= se)
            return st[index];

        // If segment of this node
        // is outside the given range
        if (se < qs || ss > qe)
            return Integer.MAX_VALUE;

        // If a part of this segment
        // overlaps with the given range
        int mid = getMid(ss, se);
        return minVal(RMQUtil(st, ss, mid, qs, qe, 2 * index + 1),
                    RMQUtil(st, mid + 1, se, qs, qe, 2 * index + 2));
    }

    // Return minimum of elements in range
    // from index qs (query start) to
    // qe (query end). It mainly uses RMQUtil()
    static int RMQ(int[] st, int n, int qs, int qe)
    {

        // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe)
        {
            System.out.println("Invalid Input");
            return -1;
        }

        return RMQUtil(st, 0, n - 1, qs, qe, 0);
    }

    // A recursive function that constructs
    // Segment Tree for array[ss..se].
    // si is index of current node in segment tree st
    static int constructSTUtil(int arr[], int ss, int se,
                                int[] st, int si)
    {

        // If there is one element in array,
        // store it in current node of
        // segment tree and return
        if (ss == se) {
            st[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one elements,
        // then recur for left and right subtrees
        // and store the minimum of two values in this node
        int mid = getMid(ss, se);
        st[si] = minVal(constructSTUtil(arr, ss, mid, st, si * 2 + 1),
                constructSTUtil(arr, mid + 1, se, st, si * 2 + 2));
        return st[si];
    }

    /*
    * Function to construct segment tree
    * from given array. This function allocates
    * memory for segment tree and calls constructSTUtil() to
    * fill the allocated memory
    */
    static int[] constructST(int arr[], int n)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        int x = (int) (Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        int max_size = 2 * (int) Math.pow(2, x) - 1;

        int[] st = new int[max_size];

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0);

        // Return the constructed segment tree
        return st;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 2, 1, 4, 5 };
        int n = arr.length;

        int[][] queries = { { 1, 2 }, { 2, 3 } };
        int q = queries.length;

        // Build segment tree from given array
        int[] st = constructST(arr, n);

        // Perform queries
        for (int i = 0; i < q; i++)
        {

            // Current index range to be exluded
            int L = queries[i][0];
            int R = queries[i][1];

            // Minimum in the left part
            int left = ((L - 1) < 0) ? Integer.MAX_VALUE : RMQ(st, n, 0, L - 1);

            // Minimum in the right part
            int right = ((R + 1) >= n) ? Integer.MAX_VALUE : RMQ(st, n, R + 1, n - 1);

            // Minimum in the array excluding the given range
            int minn = Math.min(left, right);

            // Complete array has been excluded
            if (minn == Integer.MAX_VALUE)
                System.out.println(-1);
            else
                System.out.println(minn);
        }
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil,log,floor,sqrt

# A utility function to get minimum of two numbers
def minVal(x, y):
    return min(x, y)

# A utility function to get the
# middle index from corner indexes.
def getMid(s, e):
    return s + (e - s) // 2

""" A recursive function to get the
minimum value in a given range
of array indexes. The following
are parameters for this function.

    st --> Pointer to segment tree
    index --> Index of current node in the
        segment tree. Initially 0 is
        passed as root is always at index 0
    ss & se --> Starting and ending indexes
                of the segment represented
                by current node, i.e., st[index]
    qs & qe --> Starting and ending indexes of query range"""
def RMQUtil(st, ss, se, qs, qe, index):

    # If segment of this node is a part
    # of given range, then return
    # the min of the segment
    if (qs <= ss and qe >= se):
        return st[index]

    # If segment of this node
    # is outside the given range
    if (se < qs or ss > qe):
        return 10**9

    # If a part of this segment
    # overlaps with the given range
    mid = getMid(ss, se)
    return minVal(RMQUtil(st, ss, mid, qs, qe, 2 * index + 1),
                RMQUtil(st, mid + 1, se, qs, qe, 2 * index + 2))

# Return minimum of elements in range
# from index qs (query start) to
# qe (query end). It mainly uses RMQUtil()
def RMQ(st, n, qs, qe):

    # Check for erroneous input values
    if (qs < 0 or qe > n - 1 or qs > qe):
        print("Invalid Input")
        return -1

    return RMQUtil(st, 0, n - 1, qs, qe, 0)

# A recursive function that constructs
# Segment Tree for array[ss..se].
# si is index of current node in segment tree st
def constructSTUtil(arr, ss, se, st, si):

    # If there is one element in array,
    # store it in current node of
    # segment tree and return
    if (ss == se):
        st[si] = arr[ss]
        return arr[ss]

    # If there are more than one elements,
    # then recur for left and right subtrees
    # and store the minimum of two values in this node
    mid = getMid(ss, se)
    st[si] = minVal(constructSTUtil(arr, ss, mid, st, si * 2 + 1),
                constructSTUtil(arr, mid + 1, se, st, si * 2 + 2))
    return st[si]

""" Function to construct segment tree
from given array. This function allocates
memory for segment tree and calls constructSTUtil() to
fill the allocated memory"""
def constructST(arr, n):

    # Allocate memory for segment tree

    # Height of segment tree
    x = ceil(log(n, 2))

    # Maximum size of segment tree
    max_size = 2 * pow(2, x) - 1

    st = [0]*(max_size)

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0)

    # Return the constructed segment tree
    return st

# Driver program to test above functions
if __name__ == '__main__':
    arr = [3, 2, 1, 4, 5]
    n = len(arr)

    queries = [[1, 2], [2, 3]]
    q = len(queries)

    # Build segment tree from given array
    st = constructST(arr, n)

    # Perform queries
    for i in range(q):

        # Current index range to be exluded
        L = queries[i][0]
        R = queries[i][1]

        # Minimum in the left part
        if( (L - 1) < 0):
            left = 10**9
        else:
            left = RMQ(st, n, 0, L - 1)

        # Minimum in the right part
        if (R + 1) >= n:
            right = 10**9
        else:
            right = RMQ(st, n, R + 1, n - 1)

        # Minimum in the array excluding the given range
        minn = min(left, right)

        # Complete array has been excluded
        if (minn == 10**9):
            print(-1)
        else:
            print(minn)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// A utility function to get minimum
// of two numbers
static int minVal(int x, int y)
{
    return (x < y) ? x : y;
}

// A utility function to get the
// middle index from corner indexes.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/*
* A recursive function to get the minimum value
* in a given range of array indexes. The
* following are parameters for this function.
*
* st --> Pointer to segment tree
* index --> Index of current node in the
*         segment tree. Initially 0 is passed
*         as root is always at index 0
* ss & se --> Starting and ending indexes
*             of the segment represented
*             by current node, i.e., st[index]
* qs & qe --> Starting and ending indexes of
*             query range
*/
static int RMQUtil(int[] st, int ss, int se,
                     int qs, int qe, int index)
{

    // If segment of this node is a part
    // of given range, then return
    // the min of the segment
    if (qs <= ss && qe >= se)
        return st[index];

    // If segment of this node
    // is outside the given range
    if (se < qs || ss > qe)
        return Int32.MaxValue;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return minVal(RMQUtil(st, ss, mid, qs,
                          qe, 2 * index + 1),
                  RMQUtil(st, mid + 1, se, qs,
                          qe, 2 * index + 2));
}

// Return minimum of elements in range
// from index qs (query start) to
// qe (query end). It mainly uses RMQUtil()
static int RMQ(int[] st, int n, int qs, int qe)
{

    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        Console.Write("Invalid Input" + "\n");
        return -1;
    }

    return RMQUtil(st, 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node in segment tree st
static int constructSTUtil(int []arr, int ss, int se,
                           int[] st, int si)
{

    // If there is one element in array,
    // store it in current node of
    // segment tree and return
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the minimum of two values
    // in this node
    int mid = getMid(ss, se);
    st[si] = minVal(constructSTUtil(arr, ss, mid,
                                    st, si * 2 + 1),
                    constructSTUtil(arr, mid + 1, se,
                                    st, si * 2 + 2));
    return st[si];
}

/*
* Function to construct segment tree
* from given array. This function allocates
* memory for segment tree and calls
* constructSTUtil() to fill the allocated
* memory
*/
static int[] constructST(int []arr, int n)
{

    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(Math.Ceiling(Math.Log(n) /
                               Math.Log(2)));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.Pow(2, x) - 1;

    int[] st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 3, 2, 1, 4, 5 };
    int n = arr.Length;

    int[,] queries = { { 1, 2 }, { 2, 3 } };
    int q = queries.GetLength(0);

    // Build segment tree from given array
    int[] st = constructST(arr, n);

    // Perform queries
    for(int i = 0; i < q; i++)
    {

        // Current index range to be exluded
        int L = queries[i, 0];
        int R = queries[i, 1];

        // Minimum in the left part
        int left = ((L - 1) < 0) ? Int32.MaxValue :
                   RMQ(st, n, 0, L - 1);

        // Minimum in the right part
        int right = ((R + 1) >= n) ? Int32.MaxValue :
           RMQ(st, n, R + 1, n - 1);

        // Minimum in the array excluding
        // the given range
        int minn = Math.Min(left, right);

        // Complete array has been excluded
        if (minn == Int32.MaxValue)
            Console.Write(-1 + "\n");
        else
            Console.Write(minn + "\n");
    }
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// A utility function to get minimum of two numbers
function minVal(x,y)
{
    return (x < y) ? x : y;
}

// A utility function to get the
    // middle index from corner indexes.
function getMid(s,e)
{
    return s + Math.floor((e - s) / 2);
}

/*
    * A recursive function to get the minimum value in a given range of array
    * indexes. The following are parameters for this function.
    *
    * st --> Pointer to segment tree
    * index --> Index of current node in the
    *         segment tree. Initially 0 is passed as
    *         root is always at index 0
    * ss & se --> Starting and ending indexes
    *             of the segment represented
    *             by current node, i.e., st[index]
    * qs & qe --> Starting and ending indexes of query range
    */
function RMQUtil(st,ss,se,qs,qe,index)
{
    // If segment of this node is a part
        // of given range, then return
        // the min of the segment
        if (qs <= ss && qe >= se)
            return st[index];

        // If segment of this node
        // is outside the given range
        if (se < qs || ss > qe)
            return Number.MAX_VALUE;

        // If a part of this segment
        // overlaps with the given range
        let mid = getMid(ss, se);
        return minVal(RMQUtil(st, ss, mid, qs, qe, 2 * index + 1),
                    RMQUtil(st, mid + 1, se, qs, qe, 2 * index + 2));
}

// Return minimum of elements in range
    // from index qs (query start) to
    // qe (query end). It mainly uses RMQUtil()
function  RMQ(st,n,qs,qe)
{
    // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe)
        {
            document.write("Invalid Input<br>");
            return -1;
        }

        return RMQUtil(st, 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs
    // Segment Tree for array[ss..se].
    // si is index of current node in segment tree st
function constructSTUtil(arr,ss,se,st,si)
{
    // If there is one element in array,
        // store it in current node of
        // segment tree and return
        if (ss == se) {
            st[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one elements,
        // then recur for left and right subtrees
        // and store the minimum of two values in this node
        let mid = getMid(ss, se);
        st[si] = minVal(constructSTUtil(arr, ss, mid, st, si * 2 + 1),
                constructSTUtil(arr, mid + 1, se, st, si * 2 + 2));
        return st[si];
}

/*
    * Function to construct segment tree
    * from given array. This function allocates
    * memory for segment tree and calls constructSTUtil() to
    * fill the allocated memory
    */
function constructST(arr,n)
{
    // Allocate memory for segment tree

        // Height of segment tree
        let x = Math.floor (Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        let max_size = 2 * Math.floor( Math.pow(2, x)) - 1;

        let st = new Array(max_size);

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0);

        // Return the constructed segment tree
        return st;
}

// Driver Code
let arr=[3, 2, 1, 4, 5];
let n = arr.length;

let queries = [[ 1, 2 ], [ 2, 3 ]];
let q = queries.length;
// Build segment tree from given array
let st = constructST(arr, n);
// Perform queries
        for (let i = 0; i < q; i++)
        {

            // Current index range to be exluded
            let L = queries[i][0];
            let R = queries[i][1];

            // Minimum in the left part
            let left = ((L - 1) < 0) ? Number.MAX_VALUE : RMQ(st, n, 0, L - 1);

            // Minimum in the right part
            let right = ((R + 1) >= n) ? Number.MAX_VALUE : RMQ(st, n, R + 1, n - 1);

            // Minimum in the array excluding the given range
            let minn = Math.min(left, right);

            // Complete array has been excluded
            if (minn == Number.MAX_VALUE)
                document.write(-1);
            else
                document.write(minn+"<br>");
        }
// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
2
```