# 棋盘棋子范围及更新查询

> 原文:[https://www . geesforgeks . org/range-update-query-棋盘-棋子/](https://www.geeksforgeeks.org/range-update-query-chessboard-pieces/)

给定 N 个棋盘都是“白色”的，以及多个查询。有两种类型的查询:

1.  **更新:**给定范围[L，R]的指数。用 L 和 R 之间各自相反的颜色油漆所有的零件(即白色零件应涂黑色，黑色零件应涂白色)。
2.  **获取:**给定范围[L，R]的指数。找出 L 和 r 之间的黑块数量。

让我们用“0”代表“白色”作品，用“1”代表“黑色”作品。

**先决条件** : [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/) | [惰性繁殖](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)

**示例:**

```
Input : N = 4, Q = 5
        Get : L = 0, R = 3
        Update : L = 1, R = 2
        Get : L = 0, R = 1
        Update : L = 0, R = 3
        Get : L = 0, R = 3
Output : 0
         1
         2
```

**解释:**
查询 1 : A[] = { 0，0，0，0 }由于最初所有棋子都是白色的，因此黑色棋子的数量将为零。
查询 2 : A[] = { 0，1，1，0 }
查询 3:在[0，1] = 1
查询 4:将颜色更改为其在[0，3]中的相反颜色，A[] = { 1，0，0，1 }
查询 5:在[0，3]中的黑色件数= 2

**天真的做法:**
**更新(L，R) :** 从 L 到 R 迭代子阵，改变所有棋子的颜色(即 0 变 1，1 变 0)
**获取(L，R) :** 要获取黑色棋子的数量，只需统计[L，R]范围内的棋子数量即可。
无论是 update 还是 getBlackPieces()函数都会有 O(N)的时间复杂度。最坏情况下的时间复杂度为 O(Q * N)，其中 Q 为查询数，N 为棋盘棋子数。

**高效方法:**
解决这个问题的一个有效方法是使用**分段树**，这样可以降低更新的时间复杂度，并将 BlackPieces 函数设置为 O(LogN)。

**构建结构**:根据片的颜色，段树的每个叶节点将包含 0 或 1(即如果片是黑色的，节点将包含 1，否则为 0)。内部节点将包含其左子节点和右子节点的一个或多个黑色块的总和。因此，根节点将给出整个数组中黑色块的总数[0..N-1]

**更新结构:**点更新需要 O(Log(N))时间，但是当有范围更新时，使用**惰性传播**优化更新。下面是修改后的更新方法。

```
UpdateRange(ss, se)
1\. If current node's range lies completely in update query range.
...a) Value of current node becomes the difference of total count
      of black pieces in the subtree of current node and current
      value of node, i.e. tree[curNode] = (se - ss + 1) - tree[curNode]
...b) Provide the lazy value to its children by setting 
      lazy[2*curNode] = 1 - lazy[2*curNode]
      lazy[2*curNode + 1] = 1 - lazy[2*curNode + 1]

2\. If the current node's lazy value is not zero, first update
   it and provide lazy value to children.

3\. Partial Overlap of current node's range with query range
...a) Recurse for left and right child
...b) Combine the results of step (a)
```

**查询结构:**查询结构也会以和更新结构一样的方式发生一点变化，通过检查待更新并更新得到正确的查询输出。

**以下是上述方法的实施**

## C++

```
// C++ code for queries on chessboard
#include <bits/stdc++.h>

using namespace std;

// A utility function to get the
// middle index from corner indexes.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/*  A recursive function to get the
    sum of values in given range of
     the array. The following are
    parameters for this function.
    si --> Index of current node in
           the segment tree. Initially
           0 is passed as root is always
           at index 0
    ss & se  --> Starting and ending
                 indexes of the segment
                 represented by current
                 node, i.e., tree[si]
    qs & qe  --> Starting and ending
                 indexes of query range */
int getSumUtil(int* tree, int* lazy, int ss,
               int se, int qs, int qe, int si)
{
    // If lazy flag is set for current node
    // of segment tree, then there are some
    // pending updates. So we need to make
    // sure that the pending updates are done
    // before processing the sub sum query
    if (lazy[si] != 0)
    {
        // Make pending updates to this node.
        // Note that this node represents
        // sum of elements in arr[ss..se]
        tree[si] = (se - ss + 1) - tree[si];

        // checking if it is not leaf node
        // because if it is leaf node then
        // we cannot go further
        if (ss != se)
        {
            // Since we are not yet updating
            // children os si, we need to set
            // lazy values for the children
            lazy[si * 2 + 1] =
                 1 - lazy[si * 2 + 1];

            lazy[si * 2 + 2] =
                 1 - lazy[si * 2 + 2];
        }

        // unset the lazy value for current
        // node as it has been updated
        lazy[si] = 0;
    }

    // Out of range
    if (ss > se || ss > qe || se < qs)
        return 0;

    // At this point we are sure that pending
    //  lazy updates are done for current node.
    // So we can return value (same as it was
    // for query in our previous post)

    // If this segment lies in range
    if (ss >= qs && se <= qe)
        return tree[si];

    // If a part of this segment overlaps
    // with the given range
    int mid = (ss + se) / 2;
    return getSumUtil(tree, lazy, ss, mid,
                      qs, qe, 2 * si + 1) +
           getSumUtil(tree, lazy, mid + 1,
                      se, qs, qe, 2 * si + 2);
}

// Return sum of elements in range from index
// qs (query start) to qe (query end).  It
// mainly uses getSumUtil()
int getSum(int* tree, int* lazy, int n,
           int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        printf("Invalid Input");
        return -1;
    }

    return getSumUtil(tree, lazy, 0, n - 1,
                      qs, qe, 0);
}

/*  si -> index of current node in segment tree
    ss and se -> Starting and ending indexes of
                 elements for which current
                 nodes stores sum.
    us and ue -> starting and ending indexes
                 of update query */
void updateRangeUtil(int* tree, int* lazy, int si,
                     int ss, int se, int us, int ue)
{
    // If lazy value is non-zero for current node
    // of segment tree, then there are some
    // pending updates. So we need to make sure that
    //  the pending updates are done before making
    // new updates. Because this value may be used by
    // parent after recursive calls (See last line
    // of this function)
    if (lazy[si] != 0) {

        // Make pending updates using value stored
        // in lazy nodes
        tree[si] = (se - ss + 1) - tree[si];

        // checking if it is not leaf node because if
        // it is leaf node then we cannot go further
        if (ss != se)
        {
            // We can postpone updating children
            // we don't need their new values now.
            // Since we are not yet updating children
            // of si, we need to set lazy flags for
            // the children
            lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
            lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
        }

        // Set the lazy value for current node
        // as 0 as it has been updated
        lazy[si] = 0;
    }

    // out of range
    if (ss > se || ss > ue || se < us)
        return;

    // Current segment is fully in range
    if (ss >= us && se <= ue) {

        // Add the difference to current node
        tree[si] = (se - ss + 1) - tree[si];

        // same logic for checking leaf
        // node or not
        if (ss != se)
        {
            // This is where we store values in
            // lazy nodes, rather than updating
            //  the segment tree itelf. Since we
            // don't need these updated values now
            // we postpone updates by storing
            // values in lazy[]
            lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
            lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
        }
        return;
    }

    // If not completely in rang, but overlaps,
    // recur for children
    int mid = (ss + se) / 2;
    updateRangeUtil(tree, lazy, si * 2 + 1,
                    ss, mid, us, ue);
    updateRangeUtil(tree, lazy, si * 2 + 2,
                    mid + 1, se, us, ue);

    // And use the result of children calls
    // to update this node
    tree[si] = tree[si * 2 + 1] + tree[si * 2 + 2];
}

// Function to update a range of values
// in segment tree
/*  us and eu -> starting and ending indexes
    of update query ue  -> ending index
    of update query, diff -> which we need
    to add in the range us to ue */
void updateRange(int* tree, int* lazy,
                 int n, int us, int ue)
{
    updateRangeUtil(tree, lazy, 0, 0, n - 1, us, ue);
}

// A recursive function that constructs
// Segment Tree for array[ss..se]. si is
// index of current node in segment tree st
int constructSTUtil(int arr[], int ss, int se,
                    int* tree, int si)
{
    // If there is one element in array, store
    // it in current node of segment tree and return
    if (ss == se)
    {
        tree[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one elements, then
    // recur for left and right subtrees and
    // store the sum of values in this node
    int mid = getMid(ss, se);
    tree[si] = constructSTUtil(arr, ss, mid,
               tree, si * 2 + 1) +
               constructSTUtil(arr, mid + 1,
                       se, tree, si * 2 + 2);
    return tree[si];
}

/* Function to construct segment tree from
   given array. This function allocates
   memory for segment tree and calls
   constructSTUtil() to fill the
   allocated memory */
int* constructST(int arr[], int n)
{
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* tree = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, tree, 0);

    // Return the constructed segment tree
    return tree;
}

/* Function to construct lazy array for
   segment tree. This function allocates
   memory for lazy array  */
int* constructLazy(int arr[], int n)
{
    // Allocate memory for lazy array

    // Height of lazy array
    int x = (int)(ceil(log2(n)));

    // Maximum size of lazy array
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* lazy = new int[max_size];

    // Return the lazy array
    return lazy;
}

// Driver program to test above functions
int main()
{
    // Initialize the array to zero
    // since all pieces are white
    int arr[] = { 0, 0, 0, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    int* tree = constructST(arr, n);

    // Allocate memory for Lazy array
    int* lazy = constructLazy(arr, n);

    // Print number of black pieces
    // from index 0 to 3
    cout << "Black Pieces in given range = "
         << getSum(tree, lazy, n, 0, 3) << endl;

    // UpdateRange: Change color of pieces
    // from index 1 to 2
    updateRange(tree, lazy, n, 1, 2);

    // Print number of black pieces
    // from index 0 to 1
    cout << "Black Pieces in given range = "
         << getSum(tree, lazy, n, 0, 1) << endl;

    // UpdateRange: Change color of
    // pieces from index 0 to 3
    updateRange(tree, lazy, n, 0, 3);

    // Print number of black pieces
    // from index 0 to 3
    cout << "Black Pieces in given range = "
         << getSum(tree, lazy, n, 0, 3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG
{

    // A utility function to get the
    // middle index from corner indexes.
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    /*
    * A recursive function to get the sum of
    values in given range of the array.
    * The following are parameters for this function.
    * si --> Index of current node in
    *     the segment tree. Initially
    *     0 is passed as root is always
    *     at index 0
    * ss & se --> Starting and ending
    *             indexes of the segment
    *             represented by current
    *             node, i.e., tree[si]
    * qs & qe --> Starting and ending
    *             indexes of query range
    */
    static int getSumUtil(int[] tree, int[] lazy, int ss,
                       int se, int qs, int qe, int si)
    {

        // If lazy flag is set for current node
        // of segment tree, then there are some
        // pending updates. So we need to make
        // sure that the pending updates are done
        // before processing the sub sum query
        if (lazy[si] != 0)
        {

            // Make pending updates to this node.
            // Note that this node represents
            // sum of elements in arr[ss..se]
            tree[si] = (se - ss + 1) - tree[si];

            // checking if it is not leaf node
            // because if it is leaf node then
            // we cannot go further
            if (ss != se)
            {

                // Since we are not yet updating
                // children os si, we need to set
                // lazy values for the children
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];

                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }

            // unset the lazy value for current
            // node as it has been updated
            lazy[si] = 0;
        }

        // Out of range
        if (ss > se || ss > qe || se < qs)
            return 0;

        // At this point we are sure that pending
        // lazy updates are done for current node.
        // So we can return value (same as it was
        // for query in our previous post)

        // If this segment lies in range
        if (ss >= qs && se <= qe)
            return tree[si];

        // If a part of this segment overlaps
        // with the given range
        int mid = (ss + se) / 2;
        return getSumUtil(tree, lazy, ss, mid, qs, qe, 2 * si + 1)
                + getSumUtil(tree, lazy, mid + 1, se, qs, qe, 2 * si + 2);
    }

    // Return sum of elements in range from index
    // qs (query start) to qe (query end). It
    // mainly uses getSumUtil()
    static int getSum(int[] tree, int[] lazy, int n, int qs, int qe)
    {

        // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe)
        {
            System.out.println("Invalid Input");
            return -1;
        }

        return getSumUtil(tree, lazy, 0, n - 1, qs, qe, 0);
    }

    /*
    * si -> index of current node in segment tree
    * ss and se -> Starting and ending indexes of
    *             elements for which current
    *             nodes stores sum.
    * us and ue -> starting and ending indexes of
    *             update query
    */
    static void updateRangeUtil(int[] tree, int[] lazy, int si,
                                int ss, int se, int us, int ue)
    {

        // If lazy value is non-zero for current node
        // of segment tree, then there are some
        // pending updates. So we need to make sure that
        // the pending updates are done before making
        // new updates. Because this value may be used by
        // parent after recursive calls (See last line
        // of this function)
        if (lazy[si] != 0)
        {

            // Make pending updates using value stored
            // in lazy nodes
            tree[si] = (se - ss + 1) - tree[si];

            // checking if it is not leaf node because if
            // it is leaf node then we cannot go further
            if (ss != se)
            {

                // We can postpone updating children
                // we don't need their new values now.
                // Since we are not yet updating children
                // of si, we need to set lazy flags for
                // the children
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }

            // Set the lazy value for current node
            // as 0 as it has been updated
            lazy[si] = 0;
        }

        // out of range
        if (ss > se || ss > ue || se < us)
            return;

        // Current segment is fully in range
        if (ss >= us && se <= ue)
        {

            // Add the difference to current node
            tree[si] = (se - ss + 1) - tree[si];

            // same logic for checking leaf
            // node or not
            if (ss != se)
            {

                // This is where we store values in
                // lazy nodes, rather than updating
                // the segment tree itelf. Since we
                // don't need these updated values now
                // we postpone updates by storing
                // values in lazy[]
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }
            return;
        }

        // If not completely in rang, but overlaps,
        // recur for children
        int mid = (ss + se) / 2;
        updateRangeUtil(tree, lazy, si * 2 + 1, ss, mid, us, ue);
        updateRangeUtil(tree, lazy, si * 2 + 2, mid + 1, se, us, ue);

        // And use the result of children calls
        // to update this node
        tree[si] = tree[si * 2 + 1] + tree[si * 2 + 2];
    }

    // Function to update a range of values
    // in segment tree
    /*
    * us and eu -> starting and ending indexes
    *             of update query
    * ue -> ending index of update query
    * diff -> which we need to add in the range
    *         us to ue
    */
    static void updateRange(int[] tree, int[] lazy,
                            int n, int us, int ue)
    {
        updateRangeUtil(tree, lazy, 0, 0, n - 1, us, ue);
    }

    // A recursive function that constructs
    // Segment Tree for array[ss..se]. si is
    // index of current node in segment tree st
    static int constructSTUtil(int arr[], int ss,
                        int se, int[] tree, int si)
    {

        // If there is one element in array, store
        // it in current node of segment tree and return
        if (ss == se)
        {
            tree[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one elements, then
        // recur for left and right subtrees and
        // store the sum of values in this node
        int mid = getMid(ss, se);
        tree[si] = constructSTUtil(arr, ss, mid, tree, si * 2 + 1)
                + constructSTUtil(arr, mid + 1, se, tree, si * 2 + 2);
        return tree[si];
    }

    /*
    * Function to construct segment tree from
    given array. This function allocates memory
    for segment tree and calls constructSTUtil()
    to fill the allocated memory
    */
    static int[] constructST(int arr[], int n)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        int x = (int) Math.ceil(Math.log(n) / Math.log(2));

        // Maximum size of segment tree
        int max_size = 2 * (int) Math.pow(2, x) - 1;

        // Allocate memory
        int[] tree = new int[max_size];

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, tree, 0);

        // Return the constructed segment tree
        return tree;
    }

    /*
    * Function to construct lazy array
    for segment tree. This function allocates
    * memory for lazy array
    */
    static int[] constructLazy(int arr[], int n)
    {
        // Allocate memory for lazy array

        // Height of lazy array
        int x = (int) Math.ceil(Math.log(n) / Math.log(2));

        // Maximum size of lazy array
        int max_size = 2 * (int) Math.pow(2, x) - 1;

        // Allocate memory
        int[] lazy = new int[max_size];

        // Return the lazy array
        return lazy;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Initialize the array to zero
        // since all pieces are white
        int[] arr = {0, 0, 0, 0};
        int n = arr.length;

        // Build segment tree from given array
        int[] tree = constructST(arr, n);

        // Allocate memory for Lazy array
        int[] lazy = constructLazy(arr, n);

        // Print number of black pieces
        // from index 0 to 3
        System.out.println("Black Pieces in given range = " +
                                getSum(tree, lazy, n, 0, 3));

        // UpdateRange: Change color of pieces
        // from index 1 to 2
        updateRange(tree, lazy, n, 1, 2);

        // Print number of black pieces
        // from index 0 to 1
        System.out.println("Black Pieces in given range = " +
                                getSum(tree, lazy, n, 0, 1));

        // UpdateRange: Change color of
        // pieces from index 0 to 3
        updateRange(tree, lazy, n, 0, 3);

        // Print number of black pieces
        // from index 0 to 3
        System.out.println("Black Pieces in given range = " +
                                getSum(tree, lazy, n, 0, 3));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 code for queries on chessboard
import math

# A utility function to get the
# middle index from corner indexes.
def getMid(s, e):

    return s + int((e - s) / 2)

"""
* A recursive function to get the sum of
values in given range of the array.
* The following are parameters for this function.
* si --> Index of current node in
*     the segment tree. Initially
*     0 is passed as root is always
*     at index 0
* ss & se --> Starting and ending
*             indexes of the segment
*             represented by current
*             node, i.e., tree[si]
* qs & qe --> Starting and ending
*             indexes of query range
"""
def getSumUtil(tree, lazy, ss, se, qs, qe, si):

    # If lazy flag is set for current node
    # of segment tree, then there are some
    # pending updates. So we need to make
    # sure that the pending updates are done
    # before processing the sub sum query
    if (lazy[si] != 0):

        # Make pending updates to this node.
        # Note that this node represents
        # sum of elements in arr[ss..se]
        tree[si] = (se - ss + 1) - tree[si]

        # Checking if it is not leaf node
        # because if it is leaf node then
        # we cannot go further
        if (ss != se):

            # Since we are not yet updating
            # children os si, we need to set
            # lazy values for the children
            lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1]
            lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2]

        # unset the lazy value for current
        # node as it has been updated
        lazy[si] = 0

    # Out of range
    if (ss > se or ss > qe or se < qs):
        return 0

    # At this point we are sure that pending
    # lazy updates are done for current node.
    # So we can return value (same as it was
    # for query in our previous post)

    # If this segment lies in range
    if (ss >= qs and se <= qe):
        return tree[si]

    # If a part of this segment overlaps
    # with the given range
    mid = int((ss + se) / 2)
    return(getSumUtil(tree, lazy, ss, mid, qs,
                      qe, 2 * si + 1) +
           getSumUtil(tree, lazy, mid + 1, se,
                       qs, qe, 2 * si + 2))

# Return sum of elements in range from index
# qs (query start) to qe (query end). It
# mainly uses getSumUtil()
def getSum(tree, lazy, n, qs, qe):

    # Check for erroneous input values
    if (qs < 0 or qe > n - 1 or qs > qe):
        print("Invalid Input")
        return -1

    return getSumUtil(tree, lazy, 0, n - 1, qs, qe, 0)

"""
* si -> index of current node in segment tree
* ss and se -> Starting and ending indexes of
*             elements for which current
*             nodes stores sum.
* us and ue -> starting and ending indexes of
*             update query
"""
def updateRangeUtil(tree, lazy, si, ss, se, us, ue):

    # If lazy value is non-zero for current node
    # of segment tree, then there are some
    # pending updates. So we need to make sure that
    # the pending updates are done before making
    # new updates. Because this value may be used by
    # parent after recursive calls (See last line
    # of this function)
    if (lazy[si] != 0):

        # Make pending updates using value stored
        # in lazy nodes
        tree[si] = (se - ss + 1) - tree[si]

        # Checking if it is not leaf node because if
        # it is leaf node then we cannot go further
        if (ss != se):

            # We can postpone updating children
            # we don't need their new values now.
            # Since we are not yet updating children
            # of si, we need to set lazy flags for
            # the children
            lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1]
            lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2]

        # Set the lazy value for current node
        # as 0 as it has been updated
        lazy[si] = 0

    # Out of range
    if (ss > se or ss > ue or se < us):
        return

    # Current segment is fully in range
    if (ss >= us and se <= ue):

        # Add the difference to current node
        tree[si] = (se - ss + 1) - tree[si]

        # Same logic for checking leaf
        # node or not
        if (ss != se):

            # This is where we store values in
            # lazy nodes, rather than updating
            # the segment tree itelf. Since we
            # don't need these updated values now
            # we postpone updates by storing
            # values in lazy[]
            lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1]
            lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2]

        return

    # If not completely in rang, but overlaps,
    # recur for children
    mid = int((ss + se) / 2)
    updateRangeUtil(tree, lazy, si * 2 + 1,
                    ss, mid, us, ue)
    updateRangeUtil(tree, lazy, si * 2 + 2,
                    mid + 1, se, us, ue)

    # And use the result of children calls
    # to update this node
    tree[si] = tree[si * 2 + 1] + tree[si * 2 + 2]

# Function to update a range of values
# in segment tree
"""
* us and eu -> starting and ending indexes
*             of update query
* ue -> ending index of update query
* diff -> which we need to add in the range
*         us to ue
"""
def updateRange(tree, lazy, n, us, ue):

    updateRangeUtil(tree, lazy, 0, 0, n - 1, us, ue)

# A recursive function that constructs
# Segment Tree for array[ss..se]. si is
# index of current node in segment tree st
def constructSTUtil(arr, ss, se, tree, si):

    # If there is one element in array, store
    # it in current node of segment tree and return
    if (ss == se):

        tree[si] = arr[ss]
        return arr[ss]

    # If there are more than one elements, then
    # recur for left and right subtrees and
    # store the sum of values in this node
    mid = getMid(ss, se)
    tree[si] = (constructSTUtil(arr, ss, mid, tree,
                                si * 2 + 1) +
               constructSTUtil(arr, mid + 1, se, tree,
                               si * 2 + 2))

    return tree[si]

"""
* Function to construct segment tree from
given array. This function allocates memory
for segment tree and calls constructSTUtil()
to fill the allocated memory
"""
def constructST(arr, n):

    # Allocate memory for segment tree

    # Height of segment tree
    x = int(math.ceil(math.log(n) / math.log(2)))

    # Maximum size of segment tree
    max_size = 2 * int(math.pow(2, x)) - 1

    # Allocate memory
    tree = [0]*max_size

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, tree, 0)

    # Return the constructed segment tree
    return tree

"""
Function to construct lazy array
for segment tree. This function allocates
memory for lazy array
"""
def constructLazy(arr, n):

    # Allocate memory for lazy array

    # Height of lazy array
    x = int(math.ceil(math.log(n) / math.log(2)))

    # Maximum size of lazy array
    max_size = 2 * int(math.pow(2, x)) - 1

    # Allocate memory
    lazy = [0]*max_size

    # Return the lazy array
    return lazy

# Driver code

# Initialize the array to zero
# since all pieces are white
arr = [ 0, 0, 0, 0 ]
n = len(arr)

# Build segment tree from given array
tree = constructST(arr, n)

# Allocate memory for Lazy array
lazy = constructLazy(arr, n)

# Print number of black pieces
# from index 0 to 3
print("Black Pieces in given range =",
      getSum(tree, lazy, n, 0, 3))

# UpdateRange: Change color of pieces
# from index 1 to 2
updateRange(tree, lazy, n, 1, 2)

# Print number of black pieces
# from index 0 to 1
print("Black Pieces in given range =",
      getSum(tree, lazy, n, 0, 1))

# UpdateRange: Change color of
# pieces from index 0 to 3
updateRange(tree, lazy, n, 0, 3)

# Print number of black pieces
# from index 0 to 3
print("Black Pieces in given range =",
      getSum(tree, lazy, n, 0, 3))

# This code is contributed by suresh07
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // A utility function to get the
    // middle index from corner indexes.
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    /*
    * A recursive function to get the sum of
    values in given range of the array.
    * The following are parameters for this function.
    * si --> Index of current node in
    *     the segment tree. Initially
    *     0 is passed as root is always
    *     at index 0
    * ss & se --> Starting and ending
    *             indexes of the segment
    *             represented by current
    *             node, i.e., tree[si]
    * qs & qe --> Starting and ending
    *             indexes of query range
    */
    static int getSumUtil(int[] tree, int[] lazy, int ss,
                       int se, int qs, int qe, int si)
    {

        // If lazy flag is set for current node
        // of segment tree, then there are some
        // pending updates. So we need to make
        // sure that the pending updates are done
        // before processing the sub sum query
        if (lazy[si] != 0)
        {

            // Make pending updates to this node.
            // Note that this node represents
            // sum of elements in arr[ss..se]
            tree[si] = (se - ss + 1) - tree[si];

            // checking if it is not leaf node
            // because if it is leaf node then
            // we cannot go further
            if (ss != se)
            {

                // Since we are not yet updating
                // children os si, we need to set
                // lazy values for the children
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];

                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }

            // unset the lazy value for current
            // node as it has been updated
            lazy[si] = 0;
        }

        // Out of range
        if (ss > se || ss > qe || se < qs)
            return 0;

        // At this point we are sure that pending
        // lazy updates are done for current node.
        // So we can return value (same as it was
        // for query in our previous post)

        // If this segment lies in range
        if (ss >= qs && se <= qe)
            return tree[si];

        // If a part of this segment overlaps
        // with the given range
        int mid = (ss + se) / 2;
        return getSumUtil(tree, lazy, ss, mid, qs, qe, 2 * si + 1)
                + getSumUtil(tree, lazy, mid + 1, se, qs, qe, 2 * si + 2);
    }

    // Return sum of elements in range from index
    // qs (query start) to qe (query end). It
    // mainly uses getSumUtil()
    static int getSum(int[] tree, int[] lazy, int n, int qs, int qe)
    {

        // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe)
        {
            Console.WriteLine("Invalid Input");
            return -1;
        }

        return getSumUtil(tree, lazy, 0, n - 1, qs, qe, 0);
    }

    /*
    * si -> index of current node in segment tree
    * ss and se -> Starting and ending indexes of
    *             elements for which current
    *             nodes stores sum.
    * us and ue -> starting and ending indexes of
    *             update query
    */
    static void updateRangeUtil(int[] tree, int[] lazy, int si,
                                int ss, int se, int us, int ue)
    {

        // If lazy value is non-zero for current node
        // of segment tree, then there are some
        // pending updates. So we need to make sure that
        // the pending updates are done before making
        // new updates. Because this value may be used by
        // parent after recursive calls (See last line
        // of this function)
        if (lazy[si] != 0)
        {

            // Make pending updates using value stored
            // in lazy nodes
            tree[si] = (se - ss + 1) - tree[si];

            // checking if it is not leaf node because if
            // it is leaf node then we cannot go further
            if (ss != se)
            {

                // We can postpone updating children
                // we don't need their new values now.
                // Since we are not yet updating children
                // of si, we need to set lazy flags for
                // the children
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }

            // Set the lazy value for current node
            // as 0 as it has been updated
            lazy[si] = 0;
        }

        // out of range
        if (ss > se || ss > ue || se < us)
            return;

        // Current segment is fully in range
        if (ss >= us && se <= ue)
        {

            // Add the difference to current node
            tree[si] = (se - ss + 1) - tree[si];

            // same logic for checking leaf
            // node or not
            if (ss != se)
            {

                // This is where we store values in
                // lazy nodes, rather than updating
                // the segment tree itelf. Since we
                // don't need these updated values now
                // we postpone updates by storing
                // values in lazy[]
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }
            return;
        }

        // If not completely in rang, but overlaps,
        // recur for children
        int mid = (ss + se) / 2;
        updateRangeUtil(tree, lazy, si * 2 + 1, ss, mid, us, ue);
        updateRangeUtil(tree, lazy, si * 2 + 2, mid + 1, se, us, ue);

        // And use the result of children calls
        // to update this node
        tree[si] = tree[si * 2 + 1] + tree[si * 2 + 2];
    }

    // Function to update a range of values
    // in segment tree
    /*
    * us and eu -> starting and ending indexes
    *             of update query
    * ue -> ending index of update query
    * diff -> which we need to add in the range
    *         us to ue
    */
    static void updateRange(int[] tree, int[] lazy,
                            int n, int us, int ue)
    {
        updateRangeUtil(tree, lazy, 0, 0, n - 1, us, ue);
    }

    // A recursive function that constructs
    // Segment Tree for array[ss..se]. si is
    // index of current node in segment tree st
    static int constructSTUtil(int[] arr, int ss,
                        int se, int[] tree, int si)
    {

        // If there is one element in array, store
        // it in current node of segment tree and return
        if (ss == se)
        {
            tree[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one elements, then
        // recur for left and right subtrees and
        // store the sum of values in this node
        int mid = getMid(ss, se);
        tree[si] = constructSTUtil(arr, ss, mid, tree, si * 2 + 1)
                + constructSTUtil(arr, mid + 1, se, tree, si * 2 + 2);
        return tree[si];
    }

    /*
    * Function to construct segment tree from
    given array. This function allocates memory
    for segment tree and calls constructSTUtil()
    to fill the allocated memory
    */
    static int[] constructST(int[] arr, int n)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        int x = (int) Math.Ceiling(Math.Log(n) / Math.Log(2));

        // Maximum size of segment tree
        int max_size = 2 * (int) Math.Pow(2, x) - 1;

        // Allocate memory
        int[] tree = new int[max_size];

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, tree, 0);

        // Return the constructed segment tree
        return tree;
    }

    /*
    * Function to construct lazy array
    for segment tree. This function allocates
    * memory for lazy array
    */
    static int[] constructLazy(int[] arr, int n)
    {
        // Allocate memory for lazy array

        // Height of lazy array
        int x = (int) Math.Ceiling(Math.Log(n) / Math.Log(2));

        // Maximum size of lazy array
        int max_size = 2 * (int) Math.Pow(2, x) - 1;

        // Allocate memory
        int[] lazy = new int[max_size];

        // Return the lazy array
        return lazy;
    }

  static void Main() {
    // Initialize the array to zero
        // since all pieces are white
        int[] arr = {0, 0, 0, 0};
        int n = arr.Length;

        // Build segment tree from given array
        int[] tree = constructST(arr, n);

        // Allocate memory for Lazy array
        int[] lazy = constructLazy(arr, n);

        // Print number of black pieces
        // from index 0 to 3
        Console.WriteLine("Black Pieces in given range = " +
                                getSum(tree, lazy, n, 0, 3));

        // UpdateRange: Change color of pieces
        // from index 1 to 2
        updateRange(tree, lazy, n, 1, 2);

        // Print number of black pieces
        // from index 0 to 1
        Console.WriteLine("Black Pieces in given range = " +
                                getSum(tree, lazy, n, 0, 1));

        // UpdateRange: Change color of
        // pieces from index 0 to 3
        updateRange(tree, lazy, n, 0, 3);

        // Print number of black pieces
        // from index 0 to 3
        Console.WriteLine("Black Pieces in given range = " + getSum(tree, lazy, n, 0, 3));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // A utility function to get the
    // middle index from corner indexes.
    function getMid(s, e)
    {
        return s + parseInt((e - s) / 2, 10);
    }

    /*
    * A recursive function to get the sum of
    values in given range of the array.
    * The following are parameters for this function.
    * si --> Index of current node in
    *     the segment tree. Initially
    *     0 is passed as root is always
    *     at index 0
    * ss & se --> Starting and ending
    *             indexes of the segment
    *             represented by current
    *             node, i.e., tree[si]
    * qs & qe --> Starting and ending
    *             indexes of query range
    */
    function getSumUtil(tree, lazy, ss, se, qs, qe, si)
    {

        // If lazy flag is set for current node
        // of segment tree, then there are some
        // pending updates. So we need to make
        // sure that the pending updates are done
        // before processing the sub sum query
        if (lazy[si] != 0)
        {

            // Make pending updates to this node.
            // Note that this node represents
            // sum of elements in arr[ss..se]
            tree[si] = (se - ss + 1) - tree[si];

            // checking if it is not leaf node
            // because if it is leaf node then
            // we cannot go further
            if (ss != se)
            {

                // Since we are not yet updating
                // children os si, we need to set
                // lazy values for the children
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];

                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }

            // unset the lazy value for current
            // node as it has been updated
            lazy[si] = 0;
        }

        // Out of range
        if (ss > se || ss > qe || se < qs)
            return 0;

        // At this point we are sure that pending
        // lazy updates are done for current node.
        // So we can return value (same as it was
        // for query in our previous post)

        // If this segment lies in range
        if (ss >= qs && se <= qe)
            return tree[si];

        // If a part of this segment overlaps
        // with the given range
        let mid = parseInt((ss + se) / 2, 10);
        return getSumUtil(tree, lazy, ss, mid, qs, qe, 2 * si + 1)
                + getSumUtil(tree, lazy, mid + 1, se, qs, qe, 2 * si + 2);
    }

    // Return sum of elements in range from index
    // qs (query start) to qe (query end). It
    // mainly uses getSumUtil()
    function getSum(tree, lazy, n, qs, qe)
    {

        // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe)
        {
            document.write("Invalid Input");
            return -1;
        }

        return getSumUtil(tree, lazy, 0, n - 1, qs, qe, 0);
    }

    /*
    * si -> index of current node in segment tree
    * ss and se -> Starting and ending indexes of
    *             elements for which current
    *             nodes stores sum.
    * us and ue -> starting and ending indexes of
    *             update query
    */
    function updateRangeUtil(tree, lazy, si, ss, se, us, ue)
    {

        // If lazy value is non-zero for current node
        // of segment tree, then there are some
        // pending updates. So we need to make sure that
        // the pending updates are done before making
        // new updates. Because this value may be used by
        // parent after recursive calls (See last line
        // of this function)
        if (lazy[si] != 0)
        {

            // Make pending updates using value stored
            // in lazy nodes
            tree[si] = (se - ss + 1) - tree[si];

            // checking if it is not leaf node because if
            // it is leaf node then we cannot go further
            if (ss != se)
            {

                // We can postpone updating children
                // we don't need their new values now.
                // Since we are not yet updating children
                // of si, we need to set lazy flags for
                // the children
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }

            // Set the lazy value for current node
            // as 0 as it has been updated
            lazy[si] = 0;
        }

        // out of range
        if (ss > se || ss > ue || se < us)
            return;

        // Current segment is fully in range
        if (ss >= us && se <= ue)
        {

            // Add the difference to current node
            tree[si] = (se - ss + 1) - tree[si];

            // same logic for checking leaf
            // node or not
            if (ss != se)
            {

                // This is where we store values in
                // lazy nodes, rather than updating
                // the segment tree itelf. Since we
                // don't need these updated values now
                // we postpone updates by storing
                // values in lazy[]
                lazy[si * 2 + 1] = 1 - lazy[si * 2 + 1];
                lazy[si * 2 + 2] = 1 - lazy[si * 2 + 2];
            }
            return;
        }

        // If not completely in rang, but overlaps,
        // recur for children
        let mid = parseInt((ss + se) / 2, 10);
        updateRangeUtil(tree, lazy, si * 2 + 1, ss, mid, us, ue);
        updateRangeUtil(tree, lazy, si * 2 + 2, mid + 1, se, us, ue);

        // And use the result of children calls
        // to update this node
        tree[si] = tree[si * 2 + 1] + tree[si * 2 + 2];
    }

    // Function to update a range of values
    // in segment tree
    /*
    * us and eu -> starting and ending indexes
    *             of update query
    * ue -> ending index of update query
    * diff -> which we need to add in the range
    *         us to ue
    */
    function updateRange(tree, lazy, n, us, ue)
    {
        updateRangeUtil(tree, lazy, 0, 0, n - 1, us, ue);
    }

    // A recursive function that constructs
    // Segment Tree for array[ss..se]. si is
    // index of current node in segment tree st
    function constructSTUtil(arr, ss, se, tree, si)
    {

        // If there is one element in array, store
        // it in current node of segment tree and return
        if (ss == se)
        {
            tree[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one elements, then
        // recur for left and right subtrees and
        // store the sum of values in this node
        let mid = getMid(ss, se);
        tree[si] = constructSTUtil(arr, ss, mid, tree, si * 2 + 1)
                + constructSTUtil(arr, mid + 1, se, tree, si * 2 + 2);
        return tree[si];
    }

    /*
    * Function to construct segment tree from
    given array. This function allocates memory
    for segment tree and calls constructSTUtil()
    to fill the allocated memory
    */
    function constructST(arr, n)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        let x = parseInt(Math.ceil(Math.log(n) / Math.log(2)), 10);

        // Maximum size of segment tree
        let max_size = 2 * parseInt(Math.pow(2, x), 10) - 1;

        // Allocate memory
        let tree = new Array(max_size);
        tree.fill(0);

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, tree, 0);

        // Return the constructed segment tree
        return tree;
    }

    /*
    * Function to construct lazy array
    for segment tree. This function allocates
    * memory for lazy array
    */
    function constructLazy(arr, n)
    {
        // Allocate memory for lazy array

        // Height of lazy array
        let x = parseInt(Math.ceil(Math.log(n) / Math.log(2)), 10);

        // Maximum size of lazy array
        let max_size = 2 * parseInt(Math.pow(2, x), 10) - 1;

        // Allocate memory
        let lazy = new Array(max_size);
        lazy.fill(0);

        // Return the lazy array
        return lazy;
    }

    // Initialize the array to zero
    // since all pieces are white
    let arr = [0, 0, 0, 0];
    let n = arr.length;

    // Build segment tree from given array
    let tree = constructST(arr, n);

    // Allocate memory for Lazy array
    let lazy = constructLazy(arr, n);

    // Print number of black pieces
    // from index 0 to 3
    document.write("Black Pieces in given range = " +
                      getSum(tree, lazy, n, 0, 3) + "</br>");

    // UpdateRange: Change color of pieces
    // from index 1 to 2
    updateRange(tree, lazy, n, 1, 2);

    // Print number of black pieces
    // from index 0 to 1
    document.write("Black Pieces in given range = " +
                      getSum(tree, lazy, n, 0, 1) + "</br>");

    // UpdateRange: Change color of
    // pieces from index 0 to 3
    updateRange(tree, lazy, n, 0, 3);

    // Print number of black pieces
    // from index 0 to 3
    document.write("Black Pieces in given range = " + getSum(tree, lazy, n, 0, 3));

    // This code is contributed by divyeshrabadiy07.
</script>
```

**Output:** 

```
Black Pieces in given range = 0
Black Pieces in given range = 1
Black Pieces in given range = 2
```

**时间复杂度:**每次查询和每次更新将花费 **O(Log(N))** 时间，其中 N 为棋盘棋子数。因此，对于 Q 查询，最坏情况的复杂性将是 **(Q * Log(N))**