# 段树中的惰性传播|集合 2

> 原文:[https://www . geesforgeks . org/lazy-段内传播-树集-2/](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree-set-2/)

给定一个大小为 **N** 的数组 **arr[]** 。有两种操作:

1.  更新(l，r，x):用值 x 递增 a[i] (l <= i <= r)。
2.  查询(l，r):在 l 到 r 的范围内找到数组中的最大值(两者都包括在内)。

**例:**

> **输入:** arr[] = {1，2，3，4，5}
> 更新(0，3，4)
> 查询(1，4)
> **输出:** 8
> 应用更新操作后
> 在给定范围内用给定值数组变为{5，6，7，8，5}。
> 则 1 至 4 范围内的最大值为 8。
> **输入:** arr[] = {1，2，3，4，5}
> 更新(0，0，10)
> 查询(0，4)
> **输出:** 11

**方法:**关于片段树中的懒惰繁殖的详细解释在[之前的](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)中进行了解释。问题中唯一需要改变的是在调用父节点查询时返回两个子节点之间的最大值。请参阅代码以获得更好的理解。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000

// Ideally, we should not use global variables and large
// constant-sized arrays, we have done it here for simplicity

// To store segment tree
int tree[MAX] = { 0 };

// To store pending updates
int lazy[MAX] = { 0 };

// si -> index of current node in segment tree
// ss and se -> Starting and ending indexes of
// elements for which current nodes stores sum
// us and ue -> starting and ending indexes of update query
// diff -> which we need to add in the range us to ue
void updateRangeUtil(int si, int ss, int se, int us,
                     int ue, int diff)
{
    // If lazy value is non-zero for current node of segment
    // tree, then there are some pending updates. So we need
    // to make sure that the pending updates are done before
    // making new updates. Because this value may be used by
    // parent after recursive calls (See last line of this
    // function)
    if (lazy[si] != 0) {
        // Make pending updates using value stored in lazy
        // nodes
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se) {
            // We can postpone updating children we don't
            // need their new values now.
            // Since we are not yet updating children of si,
            // we need to set lazy flags for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Set the lazy value for current node as 0 as it
        // has been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > ue || se < us)
        return;

    // Current segment is fully in range
    if (ss >= us && se <= ue) {
        // Add the difference to current node
        tree[si] += diff;

        // Same logic for checking leaf node or not
        if (ss != se) {
            // This is where we store values in lazy nodes,
            // rather than updating the segment tree itelf
            // Since we don't need these updated values now
            // we postpone updates by storing values in lazy[]
            lazy[si * 2 + 1] += diff;
            lazy[si * 2 + 2] += diff;
        }
        return;
    }

    // If not completely in range, but overlaps
    // recur for children
    int mid = (ss + se) / 2;
    updateRangeUtil(si * 2 + 1, ss, mid, us, ue, diff);
    updateRangeUtil(si * 2 + 2, mid + 1, se, us, ue, diff);

    // And use the result of children calls
    // to update this node
    tree[si] = max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to update a range of values in segment
// tree
// us and eu -> starting and ending indexes of update query
// ue -> ending index of update query
// diff -> which we need to add in the range us to ue
void updateRange(int n, int us, int ue, int diff)
{
    updateRangeUtil(0, 0, n - 1, us, ue, diff);
}

// A recursive function to get the max of values in given
// a range of the array. The following are the parameters
// for this function
// si --> Index of the current node in the segment tree
// Initially, 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the
// segment represented by current node
// i.e., tree[si]
// qs & qe --> Starting and ending indexes of query
// range
int getMaxUtil(int ss, int se, int qs, int qe, int si)
{

    // If lazy flag is set for current node of segment tree
    // then there are some pending updates. So we need to
    // make sure that the pending updates are done before
    // processing the sub sum query
    if (lazy[si] != 0) {

        // Make pending updates to this node. Note that this
        // node represents sum of elements in arr[ss..se] and
        // all these elements must be increased by lazy[si]
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se) {
            // Since we are not yet updating children os si,
            // we need to set lazy values for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Unset the lazy value for current node as it has
        // been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > qe || se < qs)
        return 0;

    // At this point, we are sure that pending lazy updates
    // are done for current node. So we can return value
    // (same as it was for a query in our previous post)

    // If this segment lies in range
    if (ss >= qs && se <= qe)
        return tree[si];

    // If a part of this segment overlaps with the given
    // range
    int mid = (ss + se) / 2;
    return max(getSumUtil(ss, mid, qs, qe, 2 * si + 1),
               getSumUtil(mid + 1, se, qs, qe, 2 * si + 2));
}

// Return max of elements in range from index qs (query
// start) to qe (query end). It mainly uses getSumUtil()
int getMax(int n, int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe) {
        printf("Invalid Input");
        return -1;
    }

    return getSumUtil(0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st.
void constructSTUtil(int arr[], int ss, int se, int si)
{
    // out of range as ss can never be greater than se
    if (ss > se)
        return;

    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se) {
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum
    // of values in this node
    int mid = (ss + se) / 2;
    constructSTUtil(arr, ss, mid, si * 2 + 1);
    constructSTUtil(arr, mid + 1, se, si * 2 + 2);

    tree[si] = max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to construct a segment tree from a given array
// This function allocates memory for segment tree and
// calls constructSTUtil() to fill the allocated memory
void constructST(int arr[], int n)
{
    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, 0);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    constructST(arr, n);

    // Add 4 to all nodes in index range [0, 3]
    updateRange(n, 0, 3, 4);

    // Print maximum element in index range [1, 4]
    cout << getSum(n, 1, 4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

static int MAX =1000;

// Ideally, we should not use global variables and large
// constant-sized arrays, we have done it here for simplicity

// To store segment tree
static int tree[] = new int[MAX];

// To store pending updates
static int lazy[] = new int[MAX];

// si -> index of current node in segment tree
// ss and se -> Starting and ending indexes of
// elements for which current nodes stores sum
// us and ue -> starting and ending indexes of update query
// diff -> which we need to add in the range us to ue
static void updateRangeUtil(int si, int ss, int se, int us,
                    int ue, int diff)
{
    // If lazy value is non-zero for current node of segment
    // tree, then there are some pending updates. So we need
    // to make sure that the pending updates are done before
    // making new updates. Because this value may be used by
    // parent after recursive calls (See last line of this
    // function)
    if (lazy[si] != 0)
    {
        // Make pending updates using value stored in lazy
        // nodes
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se)
        {
            // We can postpone updating children we don't
            // need their new values now.
            // Since we are not yet updating children of si,
            // we need to set lazy flags for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Set the lazy value for current node as 0 as it
        // has been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > ue || se < us)
        return;

    // Current segment is fully in range
    if (ss >= us && se <= ue)
    {
        // Add the difference to current node
        tree[si] += diff;

        // Same logic for checking leaf node or not
        if (ss != se)
        {
            // This is where we store values in lazy nodes,
            // rather than updating the segment tree itelf
            // Since we don't need these updated values now
            // we postpone updates by storing values in lazy[]
            lazy[si * 2 + 1] += diff;
            lazy[si * 2 + 2] += diff;
        }
        return;
    }

    // If not completely in range, but overlaps
    // recur for children
    int mid = (ss + se) / 2;
    updateRangeUtil(si * 2 + 1, ss, mid, us, ue, diff);
    updateRangeUtil(si * 2 + 2, mid + 1, se, us, ue, diff);

    // And use the result of children calls
    // to update this node
    tree[si] = Math.max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to update a range of values in segment
// tree
// us and eu -> starting and ending indexes of update query
// ue -> ending index of update query
// diff -> which we need to add in the range us to ue
static void updateRange(int n, int us, int ue, int diff)
{
    updateRangeUtil(0, 0, n - 1, us, ue, diff);
}

// A recursive function to get the sum of values in given
// a range of the array. The following are the parameters
// for this function
// si --> Index of the current node in the segment tree
// Initially, 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the
// segment represented by current node
// i.e., tree[si]
// qs & qe --> Starting and ending indexes of query
// range
static int getSumUtil(int ss, int se, int qs, int qe, int si)
{

    // If lazy flag is set for current node of segment tree
    // then there are some pending updates. So we need to
    // make sure that the pending updates are done before
    // processing the sub sum query
    if (lazy[si] != 0)
    {

        // Make pending updates to this node. Note that this
        // node represents sum of elements in arr[ss..se] and
        // all these elements must be increased by lazy[si]
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se)
        {
            // Since we are not yet updating children os si,
            // we need to set lazy values for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Unset the lazy value for current node as it has
        // been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > qe || se < qs)
        return 0;

    // At this point, we are sure that pending lazy updates
    // are done for current node. So we can return value
    // (same as it was for a query in our previous post)

    // If this segment lies in range
    if (ss >= qs && se <= qe)
        return tree[si];

    // If a part of this segment overlaps with the given
    // range
    int mid = (ss + se) / 2;
    return Math.max(getSumUtil(ss, mid, qs, qe, 2 * si + 1),
            getSumUtil(mid + 1, se, qs, qe, 2 * si + 2));
}

// Return sum of elements in range from index qs (query
// start) to qe (query end). It mainly uses getSumUtil()
static int getSum(int n, int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        System.out.print("Invalid Input");
        return -1;
    }

    return getSumUtil(0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st.
static void constructSTUtil(int arr[], int ss, int se, int si)
{
    // out of range as ss can never be greater than se
    if (ss > se)
        return;

    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se)
    {
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum
    // of values in this node
    int mid = (ss + se) / 2;
    constructSTUtil(arr, ss, mid, si * 2 + 1);
    constructSTUtil(arr, mid + 1, se, si * 2 + 2);

    tree[si] = Math.max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to construct a segment tree from a given array
// This function allocates memory for segment tree and
// calls constructSTUtil() to fill the allocated memory
static void constructST(int arr[], int n)
{
    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, 0);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;

    // Build segment tree from given array
    constructST(arr, n);

    // Add 4 to all nodes in index range [0, 3]
    updateRange(n, 0, 3, 4);

    // Print maximum element in index range [1, 4]
    System.out.println(getSum(n, 1, 4));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 1000

# Ideally, we should not use global variables
# and large constant-sized arrays,
# we have done it here for simplicity

# To store segment tree
tree = [0] * MAX;

# To store pending updates
lazy = [0] * MAX;

# si -> index of current node in segment tree
# ss and se -> Starting and ending indexes of
# elements for which current nodes stores sum
# us and ue -> starting and ending indexes of update query
# diff -> which we need to add in the range us to ue
def updateRangeUtil(si, ss, se, us, ue, diff) :

    # If lazy value is non-zero for current node
    # of segment tree, then there are some
    # pending updates. So we need to make sure that
    # the pending updates are done before making
    # new updates. Because this value may be used by
    # parent after recursive calls (See last line of this
    # function)
    if (lazy[si] != 0) :

        # Make pending updates using value
        # stored in lazy nodes
        tree[si] += lazy[si];

        # Checking if it is not leaf node because if
        # it is leaf node then we cannot go further
        if (ss != se) :

            # We can postpone updating children
            # we don't need their new values now.
            # Since we are not yet updating children of si,
            # we need to set lazy flags for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];

        # Set the lazy value for current node 
        # as 0 as it has been updated
        lazy[si] = 0;

    # Out of range
    if (ss > se or ss > ue or se < us) :
        return;

    # Current segment is fully in range
    if (ss >= us and se <= ue) :

        # Add the difference to current node
        tree[si] += diff;

        # Same logic for checking leaf node or not
        if (ss != se) :

            # This is where we store values in lazy nodes,
            # rather than updating the segment tree itelf
            # Since we don't need these updated values now
            # we postpone updates by storing values in lazy[]
            lazy[si * 2 + 1] += diff;
            lazy[si * 2 + 2] += diff;

        return;

    # If not completely in range, but overlaps
    # recur for children
    mid = (ss + se) // 2;
    updateRangeUtil(si * 2 + 1, ss,
                    mid, us, ue, diff);
    updateRangeUtil(si * 2 + 2, mid + 1,
                    se, us, ue, diff);

    # And use the result of children calls
    # to update this node
    tree[si] = max(tree[si * 2 + 1],
                   tree[si * 2 + 2]);

# Function to update a range of values
# in segment tree
# us and eu -> starting and ending
#              indexes of update query
# ue -> ending index of update query
# diff -> which we need to add in the range us to ue
def updateRange(n, us, ue, diff) :

    updateRangeUtil(0, 0, n - 1, us, ue, diff);

# A recursive function to get the sum of values
# in a given range of the array. The following
# are the parameters for this function
# si --> Index of the current node in the segment tree
# Initially, 0 is passed as root is always at index 0
# ss & se --> Starting and ending indexes of the
# segment represented by current node
# i.e., tree[si]
# qs & qe --> Starting and ending indexes of query
# range
def getSumUtil(ss, se, qs, qe, si) :

    # If lazy flag is set for current node
    # of segment tree then there are some
    # pending updates. So we need to make sure
    # that the pending updates are done before
    # processing the sub sum query
    if (lazy[si] != 0) :

        # Make pending updates to this node.
        # Note that this node represents sum of
        # elements in arr[ss..se] and all these
        # elements must be increased by lazy[si]
        tree[si] += lazy[si];

        # Checking if it is not leaf node because if
        # it is leaf node then we cannot go further
        if (ss != se) :

            # Since we are not yet updating children os si,
            # we need to set lazy values for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];

        # Unset the lazy value for current node
        # as it has been updated
        lazy[si] = 0;

    # Out of range
    if (ss > se or ss > qe or se < qs) :
        return 0;

    # At this point, we are sure that pending lazy updates
    # are done for current node. So we can return value
    # (same as it was for a query in our previous post)

    # If this segment lies in range
    if (ss >= qs and se <= qe) :
        return tree[si];

    # If a part of this segment overlaps
    # with the given range
    mid = (ss + se) // 2;
    return max(getSumUtil(ss, mid, qs, qe, 2 * si + 1),
               getSumUtil(mid + 1, se, qs, qe, 2 * si + 2));

# Return sum of elements in range from index qs (query
# start) to qe (query end). It mainly uses getSumUtil()
def getSum(n, qs, qe) :

    # Check for erroneous input values
    if (qs < 0 or qe > n - 1 or qs > qe) :
        print("Invalid Input", end = "");
        return -1;

    return getSumUtil(0, n - 1, qs, qe, 0);

# A recursive function that constructs
# Segment Tree for array[ss..se].
# si is index of current node in segment
# tree st.
def constructSTUtil(arr, ss, se, si) :

    # out of range as ss can never be
    # greater than se
    if (ss > se) :
        return;

    # If there is one element in array,
    # store it in current node of segment
    # tree and return
    if (ss == se) :
        tree[si] = arr[ss];
        return;

    # If there are more than one elements,
    # then recur for left and right subtrees
    # and store the sum of values in this node
    mid = (ss + se) // 2;
    constructSTUtil(arr, ss, mid, si * 2 + 1);
    constructSTUtil(arr, mid + 1, se, si * 2 + 2);

    tree[si] = max(tree[si * 2 + 1], tree[si * 2 + 2]);

# Function to construct a segment tree
# from a given array. This function allocates
# memory for segment tree and calls
# constructSTUtil() to fill the allocated memory
def constructST(arr, n) :

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, 0);

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];
    n = len(arr) ;

    # Build segment tree from given array
    constructST(arr, n);

    # Add 4 to all nodes in index range [0, 3]
    updateRange(n, 0, 3, 4);

    # Print maximum element in index range [1, 4]
    print(getSum(n, 1, 4));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX =1000;

// Ideally, we should not use global variables and large
// constant-sized arrays, we have done it here for simplicity

// To store segment tree
static int []tree = new int[MAX];

// To store pending updates
static int []lazy = new int[MAX];

// si -> index of current node in segment tree
// ss and se -> Starting and ending indexes of
// elements for which current nodes stores sum
// us and ue -> starting and ending indexes of update query
// diff -> which we need to add in the range us to ue
static void updateRangeUtil(int si, int ss, int se, int us,
                    int ue, int diff)
{
    // If lazy value is non-zero for current node of segment
    // tree, then there are some pending updates. So we need
    // to make sure that the pending updates are done before
    // making new updates. Because this value may be used by
    // parent after recursive calls (See last line of this
    // function)
    if (lazy[si] != 0)
    {
        // Make pending updates using value stored in lazy
        // nodes
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se)
        {
            // We can postpone updating children we don't
            // need their new values now.
            // Since we are not yet updating children of si,
            // we need to set lazy flags for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Set the lazy value for current node as 0 as it
        // has been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > ue || se < us)
        return;

    // Current segment is fully in range
    if (ss >= us && se <= ue)
    {
        // Add the difference to current node
        tree[si] += diff;

        // Same logic for checking leaf node or not
        if (ss != se)
        {
            // This is where we store values in lazy nodes,
            // rather than updating the segment tree itelf
            // Since we don't need these updated values now
            // we postpone updates by storing values in lazy[]
            lazy[si * 2 + 1] += diff;
            lazy[si * 2 + 2] += diff;
        }
        return;
    }

    // If not completely in range, but overlaps
    // recur for children
    int mid = (ss + se) / 2;
    updateRangeUtil(si * 2 + 1, ss, mid, us, ue, diff);
    updateRangeUtil(si * 2 + 2, mid + 1, se, us, ue, diff);

    // And use the result of children calls
    // to update this node
    tree[si] = Math.Max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to update a range of values in segment
// tree
// us and eu -> starting and ending indexes of update query
// ue -> ending index of update query
// diff -> which we need to add in the range us to ue
static void updateRange(int n, int us, int ue, int diff)
{
    updateRangeUtil(0, 0, n - 1, us, ue, diff);
}

// A recursive function to get the sum of values in given
// a range of the array. The following are the parameters
// for this function
// si --> Index of the current node in the segment tree
// Initially, 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the
// segment represented by current node
// i.e., tree[si]
// qs & qe --> Starting and ending indexes of query
// range
static int getSumUtil(int ss, int se, int qs, int qe, int si)
{

    // If lazy flag is set for current node of segment tree
    // then there are some pending updates. So we need to
    // make sure that the pending updates are done before
    // processing the sub sum query
    if (lazy[si] != 0)
    {

        // Make pending updates to this node. Note that this
        // node represents sum of elements in arr[ss..se] and
        // all these elements must be increased by lazy[si]
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se)
        {
            // Since we are not yet updating children os si,
            // we need to set lazy values for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Unset the lazy value for current node as it has
        // been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > qe || se < qs)
        return 0;

    // At this point, we are sure that pending lazy updates
    // are done for current node. So we can return value
    // (same as it was for a query in our previous post)

    // If this segment lies in range
    if (ss >= qs && se <= qe)
        return tree[si];

    // If a part of this segment overlaps with the given
    // range
    int mid = (ss + se) / 2;
    return Math.Max(getSumUtil(ss, mid, qs, qe, 2 * si + 1),
            getSumUtil(mid + 1, se, qs, qe, 2 * si + 2));
}

// Return sum of elements in range from index qs (query
// start) to qe (query end). It mainly uses getSumUtil()
static int getSum(int n, int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        Console.Write("Invalid Input");
        return -1;
    }

    return getSumUtil(0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st.
static void constructSTUtil(int []arr, int ss, int se, int si)
{
    // out of range as ss can never be greater than se
    if (ss > se)
        return;

    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se)
    {
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum
    // of values in this node
    int mid = (ss + se) / 2;
    constructSTUtil(arr, ss, mid, si * 2 + 1);
    constructSTUtil(arr, mid + 1, se, si * 2 + 2);

    tree[si] = Math.Max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to construct a segment tree from a given array
// This function allocates memory for segment tree and
// calls constructSTUtil() to fill the allocated memory
static void constructST(int []arr, int n)
{
    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, 0);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;

    // Build segment tree from given array
    constructST(arr, n);

    // Add 4 to all nodes in index range [0, 3]
    updateRange(n, 0, 3, 4);

    // Print maximum element in index range [1, 4]
    Console.WriteLine(getSum(n, 1, 4));
}
}
// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var MAX = 1000;

// Ideally, we should not use global variables and large
// constant-sized arrays, we have done it here for simplicity

// To store segment tree
var tree = Array(MAX).fill(0);

// To store pending updates
var lazy = Array(MAX).fill(0);

// si -> index of current node in segment tree
// ss and se -> Starting and ending indexes of
// elements for which current nodes stores sum
// us and ue -> starting and ending indexes of update query
// diff -> which we need to add in the range us to ue
function updateRangeUtil(si, ss, se, us, ue, diff)
{
    // If lazy value is non-zero for current node of segment
    // tree, then there are some pending updates. So we need
    // to make sure that the pending updates are done before
    // making new updates. Because this value may be used by
    // parent after recursive calls (See last line of this
    // function)
    if (lazy[si] != 0) {
        // Make pending updates using value stored in lazy
        // nodes
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se) {
            // We can postpone updating children we don't
            // need their new values now.
            // Since we are not yet updating children of si,
            // we need to set lazy flags for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Set the lazy value for current node as 0 as it
        // has been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > ue || se < us)
        return;

    // Current segment is fully in range
    if (ss >= us && se <= ue) {
        // Add the difference to current node
        tree[si] += diff;

        // Same logic for checking leaf node or not
        if (ss != se) {
            // This is where we store values in lazy nodes,
            // rather than updating the segment tree itelf
            // Since we don't need these updated values now
            // we postpone updates by storing values in lazy[]
            lazy[si * 2 + 1] += diff;
            lazy[si * 2 + 2] += diff;
        }
        return;
    }

    // If not completely in range, but overlaps
    // recur for children
    var mid = parseInt((ss + se) / 2);
    updateRangeUtil(si * 2 + 1, ss, mid, us, ue, diff);
    updateRangeUtil(si * 2 + 2, mid + 1, se, us, ue, diff);

    // And use the result of children calls
    // to update this node
    tree[si] = Math.max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to update a range of values in segment
// tree
// us and eu -> starting and ending indexes of update query
// ue -> ending index of update query
// diff -> which we need to add in the range us to ue
function updateRange( n, us, ue, diff)
{
    updateRangeUtil(0, 0, n - 1, us, ue, diff);
}

// A recursive function to get the max of values in given
// a range of the array. The following are the parameters
// for this function
// si --> Index of the current node in the segment tree
// Initially, 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the
// segment represented by current node
// i.e., tree[si]
// qs & qe --> Starting and ending indexes of query
// range
function getSumUtil(ss, se, qs, qe, si)
{

    // If lazy flag is set for current node of segment tree
    // then there are some pending updates. So we need to
    // make sure that the pending updates are done before
    // processing the sub sum query
    if (lazy[si] != 0) {

        // Make pending updates to this node. Note that this
        // node represents sum of elements in arr[ss..se] and
        // all these elements must be increased by lazy[si]
        tree[si] += lazy[si];

        // Checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se) {
            // Since we are not yet updating children os si,
            // we need to set lazy values for the children
            lazy[si * 2 + 1] += lazy[si];
            lazy[si * 2 + 2] += lazy[si];
        }

        // Unset the lazy value for current node as it has
        // been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > qe || se < qs)
        return 0;

    // At this point, we are sure that pending lazy updates
    // are done for current node. So we can return value
    // (same as it was for a query in our previous post)

    // If this segment lies in range
    if (ss >= qs && se <= qe)
        return tree[si];

    // If a part of this segment overlaps with the given
    // range
    var mid = (ss + se) / 2;
    return Math.max(getSumUtil(ss, mid, qs, qe, 2 * si + 1),
               getSumUtil(mid + 1, se, qs, qe, 2 * si + 2));
}

// Return max of elements in range from index qs (query
// start) to qe (query end). It mainly uses getSumUtil()
function getSum(n, qs, qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe) {
        document.write("Invalid Input");
        return -1;
    }

    return getSumUtil(0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for
// array[ss..se]. si is index of current node in segment
// tree st.
function constructSTUtil(arr, ss, se, si)
{
    // out of range as ss can never be greater than se
    if (ss > se)
        return;

    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se) {
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum
    // of values in this node
    var mid = parseInt((ss + se) / 2);
    constructSTUtil(arr, ss, mid, si * 2 + 1);
    constructSTUtil(arr, mid + 1, se, si * 2 + 2);

    tree[si] = Math.max(tree[si * 2 + 1], tree[si * 2 + 2]);
}

// Function to construct a segment tree from a given array
// This function allocates memory for segment tree and
// calls constructSTUtil() to fill the allocated memory
function constructST(arr, n)
{
    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, 0);
}

// Driver code
var arr = [1, 2, 3, 4, 5];
var n = arr.length;
// Build segment tree from given array
constructST(arr, n);
// Add 4 to all nodes in index range [0, 3]
updateRange(n, 0, 3, 4);
// Print maximum element in index range [1, 4]
document.write( getSum(n, 1, 4));

</script>
```

**Output:** 

```
8
```