# 段树|集合 3(给定范围的异或)

> 原文:[https://www . geesforgeks . org/segment-tree-set-3-xor-给定-range/](https://www.geeksforgeeks.org/segment-tree-set-3-xor-given-range/)

我们有一个数组 arr[0。。。n-1]。有两种类型查询

1.  求从索引 l 到 r 的元素的异或，其中 0 <= l <= r <= n-1
2.  将数组中指定元素的值更改为新值 x。我们需要执行 arr[i] = x，其中 0 <= i <= n-1。

总共会有 q 个查询。

**输入约束**

```
 n <= 10^5, q <= 10^5
```

**解决方案 1**
一个简单的解决方案是运行一个从 l 到 r 的循环，并计算给定范围内元素的 xor。要更新一个值，只需执行 arr[i] = x。第一个操作需要 O(n)个时间，第二个操作需要 O(1)个时间。最差情况下，q 查询的时间复杂度为 o(n * q)
,这将花费 n ~ 10^5 和 q ~ 10^5.大量的时间因此，该解决方案将超过时间限制。

**解决方案 2**
另一个解决方案是在所有可能的范围内存储 xor，但是存在 O(n^2)可能的范围，因此对于 n ~ 10^5，它将超过空间复杂度，因此在不考虑时间复杂度的情况下，我们可以声明这个解决方案将不起作用。

**解决方案 3(段树)**
**先决条件** : [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
我们构建给定数组的段树，使得数组元素位于叶子处，内部节点存储覆盖在它们下面的叶子的 XOR。

## C++

```
// C++ program to show segment tree operations like construction,
// query and update
#include <iostream>
#include <math.h>
using namespace std;

// A utility function to get the middle index from corner indexes.
int getMid(int s, int e) {  return s + (e -s)/2;  }

/*  A recursive function to get the xor of values in given range
    of the array. The following are parameters for this function.

    st    --> Pointer to segment tree
    si    --> Index of current node in the segment tree. Initially
              0 is passed as root is always at index 0
    ss & se  --> Starting and ending indexes of the segment
                 represented by current node, i.e., st[si]
    qs & qe  --> Starting and ending indexes of query range */
int getXorUtil(int *st, int ss, int se, int qs, int qe, int si)
{
    // If segment of this node is a part of given range, then return
    // the xor of the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment overlaps with the given range
    int mid = getMid(ss, se);
    return getXorUtil(st, ss, mid, qs, qe, 2*si+1) ^
           getXorUtil(st, mid+1, se, qs, qe, 2*si+2);
}

/* A recursive function to update the nodes which have the given
   index in their range. The following are parameters
    st, si, ss and se are same as getXorUtil()
    i    --> index of the element to be updated. This index is
             in input array.
   diff --> Value to be added to all nodes which have i in range */
void updateValueUtil(int *st, int ss, int se, int i, int diff, int si)
{
    // Base Case: If the input index lies outside the range of
    // this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of this node, then update
    // the value of the node and its children
    st[si] = st[si] + diff;
    if (se != ss)
    {
        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i, diff, 2*si + 1);
        updateValueUtil(st, mid+1, se, i, diff, 2*si + 2);
    }
}

// The function to update a value in input array and segment tree.
// It uses updateValueUtil() to update the value in segment tree
void updateValue(int arr[], int *st, int n, int i, int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n-1)
    {
        cout <<"Invalid Input";
        return;
    }

    // Get the difference between new value and old value
    int diff = new_val - arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Update the values of nodes in segment tree
    updateValueUtil(st, 0, n-1, i, diff, 0);
}

// Return xor of elements in range from index qs (query start)
// to qe (query end).  It mainly uses getXorUtil()
int getXor(int *st, int n, int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n-1 || qs > qe)
    {
        cout <<"Invalid Input";
        return -1;
    }

    return getXorUtil(st, 0, n-1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for array[ss..se].
// si is index of current node in segment tree st
int constructSTUtil(int arr[], int ss, int se, int *st, int si)
{
    // If there is one element in array, store it in current node of
    // segment tree and return
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one elements, then recur for left and
    // right subtrees and store the xor of values in this node
    int mid = getMid(ss, se);
    st[si] =  constructSTUtil(arr, ss, mid, st, si*2+1) ^
              constructSTUtil(arr, mid+1, se, st, si*2+2);
    return st[si];
}

/* Function to construct segment tree from given array. This function
   allocates memory for segment tree and calls constructSTUtil() to
   fill the allocated memory */
int *constructST(int arr[], int n)
{
    // Allocate memory for segment tree

    //Height of segment tree
    int x = (int)(ceil(log2(n)));

    //Maximum size of segment tree
    int max_size = 2*(int)pow(2, x) - 1;

    // Allocate memory
    int *st =  (int *)malloc(sizeof(int)*max_size);

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n-1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver program to test above functions
int main()
{
    int arr[] = {1, 3, 5, 7, 9, 11};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Build segment tree from given array
    int *st = constructST(arr, n);

    // Print xor of values in array from index 1 to 3
    cout <<"Xor of values in given range = "<< getXor(st, n, 1, 3) << endl;

    // Update: set arr[1] = 10 and update corresponding
    // segment tree nodes
    updateValue(arr, st, n, 1, 10);

    // Find xor after the value is updated
    cout <<"Updated xor of values in given range = " << getXor(st, n, 1, 3) << endl;
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to show segment tree operations like construction,
// query and update
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// A utility function to get the middle index from corner indexes.
int getMid(int s, int e) {  return s + (e -s)/2;  }

/*  A recursive function to get the xor of values in given range
    of the array. The following are parameters for this function.

    st    --> Pointer to segment tree
    si    --> Index of current node in the segment tree. Initially
              0 is passed as root is always at index 0
    ss & se  --> Starting and ending indexes of the segment
                 represented by current node, i.e., st[si]
    qs & qe  --> Starting and ending indexes of query range */
int getXorUtil(int *st, int ss, int se, int qs, int qe, int si)
{
    // If segment of this node is a part of given range, then return
    // the xor of the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment overlaps with the given range
    int mid = getMid(ss, se);
    return getXorUtil(st, ss, mid, qs, qe, 2*si+1) ^
           getXorUtil(st, mid+1, se, qs, qe, 2*si+2);
}

/* A recursive function to update the nodes which have the given
   index in their range. The following are parameters
    st, si, ss and se are same as getXorUtil()
    i    --> index of the element to be updated. This index is
             in input array.
   diff --> Value to be added to all nodes which have i in range */
void updateValueUtil(int *st, int ss, int se, int i, int diff, int si)
{
    // Base Case: If the input index lies outside the range of
    // this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of this node, then update
    // the value of the node and its children
    st[si] = st[si] + diff;
    if (se != ss)
    {
        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i, diff, 2*si + 1);
        updateValueUtil(st, mid+1, se, i, diff, 2*si + 2);
    }
}

// The function to update a value in input array and segment tree.
// It uses updateValueUtil() to update the value in segment tree
void updateValue(int arr[], int *st, int n, int i, int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n-1)
    {
        printf("Invalid Input");
        return;
    }

    // Get the difference between new value and old value
    int diff = new_val - arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Update the values of nodes in segment tree
    updateValueUtil(st, 0, n-1, i, diff, 0);
}

// Return xor of elements in range from index qs (query start)
// to qe (query end).  It mainly uses getXorUtil()
int getXor(int *st, int n, int qs, int qe)
{
    // Check for erroneous input values
    if (qs < 0 || qe > n-1 || qs > qe)
    {
        printf("Invalid Input");
        return -1;
    }

    return getXorUtil(st, 0, n-1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for array[ss..se].
// si is index of current node in segment tree st
int constructSTUtil(int arr[], int ss, int se, int *st, int si)
{
    // If there is one element in array, store it in current node of
    // segment tree and return
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one elements, then recur for left and
    // right subtrees and store the xor of values in this node
    int mid = getMid(ss, se);
    st[si] =  constructSTUtil(arr, ss, mid, st, si*2+1) ^
              constructSTUtil(arr, mid+1, se, st, si*2+2);
    return st[si];
}

/* Function to construct segment tree from given array. This function
   allocates memory for segment tree and calls constructSTUtil() to
   fill the allocated memory */
int *constructST(int arr[], int n)
{
    // Allocate memory for segment tree

    //Height of segment tree
    int x = (int)(ceil(log2(n)));

    //Maximum size of segment tree
    int max_size = 2*(int)pow(2, x) - 1;

    // Allocate memory
    int *st =  (int *)malloc(sizeof(int)*max_size);

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n-1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver program to test above functions
int main()
{
    int arr[] = {1, 3, 5, 7, 9, 11};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Build segment tree from given array
    int *st = constructST(arr, n);

    // Print xor of values in array from index 1 to 3
    printf("Xor of values in given range = %d\n",
            getXor(st, n, 1, 3));

    // Update: set arr[1] = 10 and update corresponding
    // segment tree nodes
    updateValue(arr, st, n, 1, 10);

    // Find xor after the value is updated
    printf("Updated xor of values in given range = %d\n",
             getXor(st, n, 1, 3));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to show segment tree operations
// like construction, query and update
class GFG{

// A utility function to get the middle
// index from corner indexes.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/*
 * A recursive function to get the xor of values
 * in given range of the array.
 * The following are parameters for this function.
 *
 * st --> Pointer to segment tree
 * si --> Index of current node in the segment tree. Initially
 *        0 is passed as root is always at index 0
 * ss & se --> Starting and ending indexes of the segment
 *             represented by current node, i.e., st[si]
 * qs & qe --> Starting and ending indexes of query range
 */
static int getXorUtil(int[] st, int ss, int se,
                      int qs, int qe, int si)
{

    // If segment of this node is a part of
    // given range, then return the xor of
    // the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is
    // outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment overlaps
    // with the given range
    int mid = getMid(ss, se);
    return getXorUtil(st, ss, mid, qs,
                      qe, 2 * si + 1) ^
           getXorUtil(st, mid + 1, se, qs,
                      qe, 2 * si + 2);
}

/*
 * A recursive function to update the nodes which have the given
 * index in their range. The following are parameters
 * st, si, ss and se are same as getXorUtil()
 * i --> index of the element to be updated. This index is in
 *       input array.
 * diff --> Value to be added to all nodes which have i in range
 */
static void updateValueUtil(int[] st, int ss, int se,
                            int i, int diff, int si)
{

    // Base Case: If the input index lies outside the
    // range of this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of this node,
    // then update the value of the node and its children
    st[si] = st[si] + diff;
    if (se != ss)
    {
        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i, diff,
                         2 * si + 1);
        updateValueUtil(st, mid + 1, se, i, diff, 
                         2 * si + 2);
    }
}

// The function to update a value in input array
// and segment tree. It uses updateValueUtil()
// to update the value in segment tree
static void updateValue(int[] arr, int[] st, int n,
                        int i, int new_val)
{

    // Check for erroneous input index
    if (i < 0 || i > n - 1)
    {
        System.out.println("Invalid Input");
        return;
    }

    // Get the difference between new
    // value and old value
    int diff = new_val - arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Update the values of nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0);
}

// Return xor of elements in range from
// index qs (query start) to qe (query end).
// It mainly uses getXorUtil()
static int getXor(int[] st, int n, int qs, int qe)
{

    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        System.out.println("Invalid Input");
        return -1;
    }

    return getXorUtil(st, 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment
// Tree for array[ss..se]. si is index of current
// node in segment tree st
static int constructSTUtil(int arr[], int ss,
                           int se, int[] st, int si)
{

    // If there is one element in array, store
    // it in current node of segment tree and return
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the xor of values in this node
    int mid = getMid(ss, se);
    st[si] = constructSTUtil(arr, ss, mid, st,
                             si * 2 + 1) ^
             constructSTUtil(arr, mid + 1, se, st,
                             si * 2 + 2);
    return st[si];
}

/*
 * Function to construct segment tree from
 * given array. This function allocates memory
 * for segment tree and calls constructSTUtil()
 * to fill the allocated memory
 */
static int[] constructST(int arr[], int n)
{

    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(Math.ceil(Math.log(n) /
                            Math.log(2)));

    // Maximum size of segment tree
    int max_size = 2 * (int) Math.pow(2, x) - 1;

    // Allocate memory
    int[] st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 3, 5, 7, 9, 11 };
    int n = arr.length;

    // Build segment tree from given array
    int[] st = constructST(arr, n);

    // Print xor of values in array from index 1 to 3
    System.out.printf("Xor of values in given " +
                      "range = %d\n",
                      getXor(st, n, 1, 3));

    // Update: set arr[1] = 10 and update
    // corresponding segment tree nodes
    updateValue(arr, st, n, 1, 10);

    // Find xor after the value is updated
    System.out.printf("Updated xor of values in " +
                      "given range = %d\n",
                      getXor(st, n, 1, 3));
}
}

// This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>
    // Javascript program to show segment tree operations
    // like construction, query and update

    // A utility function to get the middle
    // index from corner indexes.
    function getMid(s, e)
    {
        return s + parseInt((e - s) / 2, 10);
    }

    function getXorUtil(st, ss, se, qs, qe, si)
    {

        // If segment of this node is a part of
        // given range, then return the xor of
        // the segment
        if (qs <= ss && qe >= se)
            return st[si];

        // If segment of this node is
        // outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment overlaps
        // with the given range
        let mid = getMid(ss, se);
        return getXorUtil(st, ss, mid, qs,
                          qe, 2 * si + 1) ^
               getXorUtil(st, mid + 1, se, qs,
                          qe, 2 * si + 2);
    }

    function updateValueUtil(st, ss, se, i, diff, si)
    {

        // Base Case: If the input index lies outside the
        // range of this segment
        if (i < ss || i > se)
            return;

        // If the input index is in range of this node,
        // then update the value of the node and its children
        st[si] = st[si] + diff;
        if (se != ss)
        {
            let mid = getMid(ss, se);
            updateValueUtil(st, ss, mid, i, diff,
                             2 * si + 1);
            updateValueUtil(st, mid + 1, se, i, diff,
                             2 * si + 2);
        }
    }

    // The function to update a value in input array
    // and segment tree. It uses updateValueUtil()
    // to update the value in segment tree
    function updateValue(arr, st, n, i, new_val)
    {

        // Check for erroneous input index
        if (i < 0 || i > n - 1)
        {
            document.write("Invalid Input");
            return;
        }

        // Get the difference between new
        // value and old value
        let diff = new_val - arr[i];

        // Update the value in array
        arr[i] = new_val;

        // Update the values of nodes in segment tree
        updateValueUtil(st, 0, n - 1, i, diff, 0);
    }

    // Return xor of elements in range from
    // index qs (query start) to qe (query end).
    // It mainly uses getXorUtil()
    function getXor(st, n, qs, qe)
    {

        // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe)
        {
            document.write("Invalid Input");
            return -1;
        }

        return getXorUtil(st, 0, n - 1, qs, qe, 0);
    }

    // A recursive function that constructs Segment
    // Tree for array[ss..se]. si is index of current
    // node in segment tree st
    function constructSTUtil(arr, ss, se, st, si)
    {

        // If there is one element in array, store
        // it in current node of segment tree and return
        if (ss == se)
        {
            st[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one elements,
        // then recur for left and right subtrees
        // and store the xor of values in this node
        let mid = getMid(ss, se);
        st[si] = constructSTUtil(arr, ss, mid, st,
                                 si * 2 + 1) ^
                 constructSTUtil(arr, mid + 1, se, st,
                                 si * 2 + 2);
        return st[si];
    }

    /*
     * Function to construct segment tree from
     * given array. This function allocates memory
     * for segment tree and calls constructSTUtil()
     * to fill the allocated memory
     */
    function constructST(arr, n)
    {

        // Allocate memory for segment tree

        // Height of segment tree
        let x = (Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        let max_size = 2 * parseInt(Math.pow(2, x), 10) - 1;

        // Allocate memory
        let st = new Array(max_size);
        st.fill(0);

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0);

        // Return the constructed segment tree
        return st;
    }

    let arr = [ 1, 3, 5, 7, 9, 11 ];
    let n = arr.length;

    // Build segment tree from given array
    let st = constructST(arr, n);

    // Print xor of values in array from index 1 to 3
    document.write("Xor of values in given " +
                      "range = " +
                      getXor(st, n, 1, 3) + "</br>");

    // Update: set arr[1] = 10 and update
    // corresponding segment tree nodes
    updateValue(arr, st, n, 1, 10);

    // Find xor after the value is updated
    document.write("Updated xor of values in " +
                      "given range = " +
                      getXor(st, n, 1, 3) + "</br>");

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Xor of values in given range = 1
Updated xor of values in given range = 8
```

**时空复杂度** :
树构造的时间复杂度为 O(n)。总共有 2n-1 个节点，每个节点的值在树构造中只计算一次。
查询的时间复杂度为 O(log n)。
更新的时间复杂度也是 O(log n)。
总时间复杂度为:O(n)为构造+ O(log n)为每个查询= O(n) + O(n * log n) = O(n * log n)

```
Time Complexity O(n * log n)
Auxiliary Space  O(n)
```

本文由 [**普拉蒂克·查哈尔**](https://pratik-chhajer.github.io/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。