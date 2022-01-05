# 更新给定索引并在范围内找到 gcd 的查询

> 原文:[https://www . geeksforgeeks . org/查询-更新-给定-索引-查找-范围内 gcd/](https://www.geeksforgeeks.org/queries-to-update-a-given-index-and-find-gcd-in-range/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，并查询 **Q** 。查询有两种类型:

1.  通过 **X** 更新给定的索引**找到**。
2.  求索引范围**【L，R】**内元素的 gcd。

**例:**

> **输入:** arr[] = {1，3，6，9，9，11}
> 类型 2 查询:L = 1，R = 3
> 类型 1 查询:ind = 1，X = 10
> 类型 2 查询:L = 1，R = 3
> **输出:**
> 3
> 1
> **输入:** arr[] = {1，2，4，9，3}
> 类型 2 查询:L = 1，1 X = 7
> 类型 2 查询:L = 1，R = 2
> 类型 2 查询:L = 3，R = 4
> **输出:**
> 2
> 1
> 3

**方法:**使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)可以解决以下问题。段树可用于中等时间的预处理和查询。对于段树，预处理时间为 0(n)，GCD 查询的时间为 0(Logn)。存储段树所需的额外空间为 0(n)。
**段树的表示**

*   叶节点是输入数组的元素。
*   每个内部节点代表其下所有叶子的 GCD。

**树的数组表示用于表示段树，即对于索引 I 处的每个节点**

*   左边的孩子在索引 2*i+1
*   右边的孩子在 2*i+2，父母在楼层((i-1)/2)。

**从给定的数组构建段树**

*   以段 arr[0]开始。。。n-1]并继续分成两半。每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，对于每个这样的段，我们将 GCD 值存储在段树节点中。
*   构建的段树的所有层都将被完全填充，除了最后一层。此外，该树将是一个完整的二叉树(每个节点有 0 或两个子节点)，因为我们总是在每个级别将段分成两半。
*   由于构造的树总是有 n 片叶子的全二叉树，因此会有 n-1 个内部节点。因此，节点总数将为 2 * n–1。

像树构造和查询操作一样，更新也可以递归完成。我们得到了一个需要更新的索引。让 diff 成为要添加的值。我们从段树的根开始，将 diff 添加到在其范围内给定索引的所有节点。如果一个节点在其范围内没有给定的索引，我们不会对该节点进行任何更改。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A utility function to get the
// middle index from corner indexes
int getMid(int s, int e)
{
    return (s + (e - s) / 2);
}

// A recursive function to get the gcd of values in given range
// of the array. The following are parameters for this function

// st --> Pointer to segment tree
// si --> Index of current node in the segment tree. Initially
// 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the segment represented
// by current node, i.e., st[si]
// qs & qe --> Starting and ending indexes of query range
int getGcdUtil(int* st, int ss, int se, int qs, int qe, int si)
{
    // If segment of this node is a part of given range
    // then return the gcd of the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment overlaps with the given range
    int mid = getMid(ss, se);
    return __gcd(getGcdUtil(st, ss, mid, qs, qe, 2 * si + 1),
                 getGcdUtil(st, mid + 1, se, qs, qe, 2 * si + 2));
}

// A recursive function to update the nodes which have the given
// index in their range. The following are parameters
// st, si, ss and se are same as getSumUtil()
// i --> index of the element to be updated. This index is
// in the input array.
// diff --> Value to be added to all nodes which have i in range
void updateValueUtil(int* st, int ss, int se, int i, int diff, int si)
{
    // Base Case: If the input index lies outside the range of
    // this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of this node, then update
    // the value of the node and its children
    st[si] = st[si] + diff;
    if (se != ss) {
        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i, diff, 2 * si + 1);
        updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2);
    }
}

// The function to update a value in input array and segment tree.
// It uses updateValueUtil() to update the value in segment tree
void updateValue(int arr[], int* st, int n, int i, int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n - 1) {
        cout << "Invalid Input";
        return;
    }

    // Get the difference between new value and old value
    int diff = new_val - arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Update the values of nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0);
}

// Function to return the sum of elements in range
// from index qs (query start) to qe (query end)
// It mainly uses getSumUtil()
int getGcd(int* st, int n, int qs, int qe)
{

    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe) {
        cout << "Invalid Input";
        return -1;
    }

    return getGcdUtil(st, 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for array[ss..se].
// si is index of current node in segment tree st
int constructGcdUtil(int arr[], int ss, int se, int* st, int si)
{
    // If there is one element in array, store it in current node of
    // segment tree and return
    if (ss == se) {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one element then recur for left and
    // right subtrees and store the sum of values in this node
    int mid = getMid(ss, se);
    st[si] = __gcd(constructGcdUtil(arr, ss, mid, st, si * 2 + 1),
                   constructGcdUtil(arr, mid + 1, se, st, si * 2 + 2));
    return st[si];
}

// Function to construct segment tree from given array. This function
// allocates memory for segment tree and calls constructSTUtil() to
// fill the allocated memory
int* constructGcd(int arr[], int n)
{
    // Allocate memory for the segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* st = new int[max_size];

    // Fill the allocated memory st
    constructGcdUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 6, 9, 9, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    int* st = constructGcd(arr, n);

    // Print GCD of values in array from index 1 to 3
    cout << getGcd(st, n, 1, 3) << endl;

    // Update: set arr[1] = 10 and update corresponding
    // segment tree nodes
    updateValue(arr, st, n, 1, 10);

    // Find GCD after the value is updated
    cout << getGcd(st, n, 1, 3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// segment tree
static int st[];

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// A utility function to get the
// middle index from corner indexes
static int getMid(int s, int e)
{
    return (s + (e - s) / 2);
}

// A recursive function to get the gcd of values in given range
// of the array. The following are parameters for this function

// st --> Pointer to segment tree
// si --> Index of current node in the segment tree. Initially
// 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the segment represented
// by current node, i.e., st[si]
// qs & qe --> Starting and ending indexes of query range
static int getGcdUtil( int ss, int se, int qs, int qe, int si)
{
    // If segment of this node is a part of given range
    // then return the gcd of the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment overlaps with the given range
    int mid = getMid(ss, se);
    return __gcd(getGcdUtil( ss, mid, qs, qe, 2 * si + 1),
                getGcdUtil( mid + 1, se, qs, qe, 2 * si + 2));
}

// A recursive function to update the nodes which have the given
// index in their range. The following are parameters
// si, ss and se are same as getSumUtil()
// i --> index of the element to be updated. This index is
// in the input array.
// diff --> Value to be added to all nodes which have i in range
static void updateValueUtil( int ss, int se, int i, int diff, int si)
{
    // Base Case: If the input index lies outside the range of
    // this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of this node, then update
    // the value of the node and its children
    st[si] = st[si] + diff;
    if (se != ss) {
        int mid = getMid(ss, se);
        updateValueUtil( ss, mid, i, diff, 2 * si + 1);
        updateValueUtil( mid + 1, se, i, diff, 2 * si + 2);
    }
}

// The function to update a value in input array and segment tree.
// It uses updateValueUtil() to update the value in segment tree
static void updateValue(int arr[], int n, int i, int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n - 1)
    {
        System.out.println("Invalid Input");
        return;
    }

    // Get the difference between new value and old value
    int diff = new_val - arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Update the values of nodes in segment tree
    updateValueUtil( 0, n - 1, i, diff, 0);
}

// Function to return the sum of elements in range
// from index qs (query start) to qe (query end)
// It mainly uses getSumUtil()
static int getGcd( int n, int qs, int qe)
{

    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        System.out.println( "Invalid Input");
        return -1;
    }

    return getGcdUtil( 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for array[ss..se].
// si is index of current node in segment tree st
static int constructGcdUtil(int arr[], int ss, int se, int si)
{
    // If there is one element in array, store it in current node of
    // segment tree and return
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one element then recur for left and
    // right subtrees and store the sum of values in this node
    int mid = getMid(ss, se);
    st[si] = __gcd(constructGcdUtil(arr, ss, mid, si * 2 + 1),
                constructGcdUtil(arr, mid + 1, se, si * 2 + 2));
    return st[si];
}

// Function to construct segment tree from given array. This function
// allocates memory for segment tree and calls constructSTUtil() to
// fill the allocated memory
static void constructGcd(int arr[], int n)
{
    // Allocate memory for the segment tree

    // Height of segment tree
    int x = (int)(Math.ceil(Math.log(n)/Math.log(2)));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.pow(2, x) - 1;

    // Allocate memory
    st = new int[max_size];

    // Fill the allocated memory st
    constructGcdUtil(arr, 0, n - 1, 0);

}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 3, 6, 9, 9, 11 };
    int n = arr.length;

    // Build segment tree from given array
    constructGcd(arr, n);

    // Print GCD of values in array from index 1 to 3
    System.out.println( getGcd( n, 1, 3) );

    // Update: set arr[1] = 10 and update corresponding
    // segment tree nodes
    updateValue(arr, n, 1, 10);

    // Find GCD after the value is updated
    System.out.println( getGcd( n, 1, 3) );
}
}

// This code is constructed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

from math import gcd,ceil,log2,pow

# A utility function to get the
# middle index from corner indexes
def getMid(s, e):
    return (s + int((e - s) / 2))

# A recursive function to get the gcd of values in given range
# of the array. The following are parameters for this function

# st --> Pointer to segment tree
# si --> Index of current node in the segment tree. Initially
# 0 is passed as root is always at index 0
# ss & se --> Starting and ending indexes of the segment represented
# by current node, i.e., st[si]
# qs & qe --> Starting and ending indexes of query range
def getGcdUtil(st,ss,se,qs,qe,si):

    # If segment of this node is a part of given range
    # then return the gcd of the segment
    if (qs <= ss and qe >= se):
        return st[si]

    # If segment of this node is outside the given range
    if (se < qs or ss > qe):
        return 0

    # If a part of this segment overlaps with the given range
    mid = getMid(ss, se)
    return gcd(getGcdUtil(st, ss, mid, qs, qe, 2 * si + 1),
            getGcdUtil(st, mid + 1, se, qs, qe, 2 * si + 2))

# A recursive function to update the nodes which have the given
# index in their range. The following are parameters
# st, si, ss and se are same as getSumUtil()
# i --> index of the element to be updated. This index is
# in the input array.
# diff --> Value to be added to all nodes which have i in range
def updateValueUtil(st,ss,se,i,diff,si):

    # Base Case: If the input index lies outside the range of
    # this segment
    if (i < ss or i > se):
        return

    # If the input index is in range of this node, then update
    # the value of the node and its children
    st[si] = st[si] + diff
    if (se != ss):
        mid = getMid(ss, se)
        updateValueUtil(st, ss, mid, i, diff, 2 * si + 1)
        updateValueUtil(st, mid + 1, se, i, diff, 2 * si + 2)

# The function to update a value in input array and segment tree.
# It uses updateValueUtil() to update the value in segment tree
def updateValue(arr, st, n, i, new_val):

    # Check for erroneous input index
    if (i < 0 or i > n - 1):
        print("Invalid Input")
        return

    # Get the difference between new value and old value
    diff = new_val - arr[i]

    # Update the value in array
    arr[i] = new_val

    # Update the values of nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0)

# Function to return the sum of elements in range
# from index qs (query start) to qe (query end)
# It mainly uses getSumUtil()
def getGcd(st,n,qs,qe):

    # Check for erroneous input values
    if (qs < 0 or qe > n - 1 or qs > qe):
        cout << "Invalid Input"
        return -1

    return getGcdUtil(st, 0, n - 1, qs, qe, 0)

# A recursive function that constructs Segment Tree for array[ss..se].
# si is index of current node in segment tree st
def constructGcdUtil(arr, ss,se, st, si):

    # If there is one element in array, store it in current node of
    # segment tree and return
    if (ss == se):
        st[si] = arr[ss]
        return arr[ss]

    # If there are more than one element then recur for left and
    # right subtrees and store the sum of values in this node
    mid = getMid(ss, se)
    st[si] = gcd(constructGcdUtil(arr, ss, mid, st, si * 2 + 1),
                constructGcdUtil(arr, mid + 1, se, st, si * 2 + 2))
    return st[si]

# Function to construct segment tree from given array. This function
# allocates memory for segment tree and calls constructSTUtil() to
# fill the allocated memory
def constructGcd(arr, n):

    # Allocate memory for the segment tree

    # Height of segment tree
    x = int(ceil(log2(n)))

    # Maximum size of segment tree
    max_size = 2 * int(pow(2, x) - 1)

    # Allocate memory
    st = [0 for i in range(max_size)]

    # Fill the allocated memory st
    constructGcdUtil(arr, 0, n - 1, st, 0)

    # Return the constructed segment tree
    return st

# Driver code
if __name__ == '__main__':
    arr = [1, 3, 6, 9, 9, 11]
    n = len(arr)

    # Build segment tree from given array
    st = constructGcd(arr, n)

    # Print GCD of values in array from index 1 to 3
    print(getGcd(st, n, 1, 3))

    # Update: set arr[1] = 10 and update corresponding
    # segment tree nodes
    updateValue(arr, st, n, 1, 10)

    # Find GCD after the value is updated
    print(getGcd(st, n, 1, 3))

# This code is contributed by
# SURENDRA_GANGWAR
```

## C#

```
// C# implementation of the approach.
using System;

class GFG
{

// segment tree
static int []st;

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// A utility function to get the
// middle index from corner indexes
static int getMid(int s, int e)
{
    return (s + (e - s) / 2);
}

// A recursive function to get the gcd of values in given range
// of the array. The following are parameters for this function

// st --> Pointer to segment tree
// si --> Index of current node in the segment tree. Initially
// 0 is passed as root is always at index 0
// ss & se --> Starting and ending indexes of the segment represented
// by current node, i.e., st[si]
// qs & qe --> Starting and ending indexes of query range
static int getGcdUtil( int ss, int se, int qs, int qe, int si)
{
    // If segment of this node is a part of given range
    // then return the gcd of the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment overlaps with the given range
    int mid = getMid(ss, se);
    return __gcd(getGcdUtil( ss, mid, qs, qe, 2 * si + 1),
                getGcdUtil( mid + 1, se, qs, qe, 2 * si + 2));
}

// A recursive function to update the nodes which have the given
// index in their range. The following are parameters
// si, ss and se are same as getSumUtil()
// i --> index of the element to be updated. This index is
// in the input array.
// diff --> Value to be added to all nodes which have i in range
static void updateValueUtil( int ss, int se, int i, int diff, int si)
{
    // Base Case: If the input index lies outside the range of
    // this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range of this node, then update
    // the value of the node and its children
    st[si] = st[si] + diff;
    if (se != ss) {
        int mid = getMid(ss, se);
        updateValueUtil( ss, mid, i, diff, 2 * si + 1);
        updateValueUtil( mid + 1, se, i, diff, 2 * si + 2);
    }
}

// The function to update a value in input array and segment tree.
// It uses updateValueUtil() to update the value in segment tree
static void updateValue(int []arr, int n, int i, int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n - 1)
    {
        Console.WriteLine("Invalid Input");
        return;
    }

    // Get the difference between new value and old value
    int diff = new_val - arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Update the values of nodes in segment tree
    updateValueUtil( 0, n - 1, i, diff, 0);
}

// Function to return the sum of elements in range
// from index qs (query start) to qe (query end)
// It mainly uses getSumUtil()
static int getGcd( int n, int qs, int qe)
{

    // Check for erroneous input values
    if (qs < 0 || qe > n - 1 || qs > qe)
    {
        Console.WriteLine( "Invalid Input");
        return -1;
    }

    return getGcdUtil( 0, n - 1, qs, qe, 0);
}

// A recursive function that constructs Segment Tree for array[ss..se].
// si is index of current node in segment tree st
static int constructGcdUtil(int []arr, int ss, int se, int si)
{
    // If there is one element in array, store it in current node of
    // segment tree and return
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // If there are more than one element then recur for left and
    // right subtrees and store the sum of values in this node
    int mid = getMid(ss, se);
    st[si] = __gcd(constructGcdUtil(arr, ss, mid, si * 2 + 1),
                constructGcdUtil(arr, mid + 1, se, si * 2 + 2));
    return st[si];
}

// Function to construct segment tree from given array. This function
// allocates memory for segment tree and calls constructSTUtil() to
// fill the allocated memory
static void constructGcd(int []arr, int n)
{
    // Allocate memory for the segment tree

    // Height of segment tree
    int x = (int)(Math.Ceiling(Math.Log(n)/Math.Log(2)));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.Pow(2, x) - 1;

    // Allocate memory
    st = new int[max_size];

    // Fill the allocated memory st
    constructGcdUtil(arr, 0, n - 1, 0);

}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 3, 6, 9, 9, 11 };
    int n = arr.Length;

    // Build segment tree from given array
    constructGcd(arr, n);

    // Print GCD of values in array from index 1 to 3
    Console.WriteLine( getGcd( n, 1, 3) );

    // Update: set arr[1] = 10 and update corresponding
    // segment tree nodes
    updateValue(arr, n, 1, 10);

    // Find GCD after the value is updated
    Console.WriteLine( getGcd( n, 1, 3) );
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach     // segment tree
    var st;

    // Recursive function to return gcd of a and b
    function __gcd(a , b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);

    }

    // A utility function to get the
    // middle index from corner indexes
    function getMid(s , e) {
        return (s + parseInt((e - s) / 2));
    }

    // A recursive function to get the gcd of values in given range
    // of the array. The following are parameters for this function

    // st --> Pointer to segment tree
    // si --> Index of current node in the segment tree. Initially
    // 0 is passed as root is always at index 0
    // ss & se --> Starting and ending indexes of the segment represented
    // by current node, i.e., st[si]
    // qs & qe --> Starting and ending indexes of query range
    function getGcdUtil(ss , se , qs , qe , si) {
        // If segment of this node is a part of given range
        // then return the gcd of the segment
        if (qs <= ss && qe >= se)
            return st[si];

        // If segment of this node is outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment overlaps with the given range
        var mid = getMid(ss, se);
        return __gcd(getGcdUtil(ss, mid, qs, qe, 2 * si + 1), getGcdUtil(mid + 1, se, qs, qe, 2 * si + 2));
    }

    // A recursive function to update the nodes which have the given
    // index in their range. The following are parameters
    // si, ss and se are same as getSumUtil()
    // i --> index of the element to be updated. This index is
    // in the input array.
    // diff --> Value to be added to all nodes which have i in range
    function updateValueUtil(ss , se , i , diff , si) {
        // Base Case: If the input index lies outside the range of
        // this segment
        if (i < ss || i > se)
            return;

        // If the input index is in range of this node, then update
        // the value of the node and its children
        st[si] = st[si] + diff;
        if (se != ss) {
            var mid = getMid(ss, se);
            updateValueUtil(ss, mid, i, diff, 2 * si + 1);
            updateValueUtil(mid + 1, se, i, diff, 2 * si + 2);
        }
    }

    // The function to update a value in input array and segment tree.
    // It uses updateValueUtil() to update the value in segment tree
    function updateValue(arr , n , i , new_val) {
        // Check for erroneous input index
        if (i < 0 || i > n - 1) {
            document.write("Invalid Input");
            return;
        }

        // Get the difference between new value and old value
        var diff = new_val - arr[i];

        // Update the value in array
        arr[i] = new_val;

        // Update the values of nodes in segment tree
        updateValueUtil(0, n - 1, i, diff, 0);
    }

    // Function to return the sum of elements in range
    // from index qs (query start) to qe (query end)
    // It mainly uses getSumUtil()
    function getGcd(n , qs , qe) {

        // Check for erroneous input values
        if (qs < 0 || qe > n - 1 || qs > qe) {
            document.write("Invalid Input");
            return -1;
        }

        return getGcdUtil(0, n - 1, qs, qe, 0);
    }

    // A recursive function that constructs Segment Tree for array[ss..se].
    // si is index of current node in segment tree st
    function constructGcdUtil(arr , ss , se , si) {
        // If there is one element in array, store it in current node of
        // segment tree and return
        if (ss == se) {
            st[si] = arr[ss];
            return arr[ss];
        }

        // If there are more than one element then recur for left and
        // right subtrees and store the sum of values in this node
        var mid = getMid(ss, se);
        st[si] = __gcd(constructGcdUtil(arr, ss, mid, si * 2 + 1), constructGcdUtil(arr, mid + 1, se, si * 2 + 2));
        return st[si];
    }

    // Function to construct segment tree from given array. This function
    // allocates memory for segment tree and calls constructSTUtil() to
    // fill the allocated memory
    function constructGcd(arr , n) {
        // Allocate memory for the segment tree

        // Height of segment tree
        var x = parseInt( (Math.ceil(Math.log(n) / Math.log(2))));

        // Maximum size of segment tree
        var max_size = 2 * parseInt( Math.pow(2, x) - 1);

        // Allocate memory
        st = Array(max_size).fill(0);

        // Fill the allocated memory st
        constructGcdUtil(arr, 0, n - 1, 0);

    }

    // Driver code

        var arr = [ 1, 3, 6, 9, 9, 11 ];
        var n = arr.length;

        // Build segment tree from given array
        constructGcd(arr, n);

        // Print GCD of values in array from index 1 to 3
        document.write(getGcd(n, 1, 3)+"<br/>");

        // Update: set arr[1] = 10 and update corresponding
        // segment tree nodes
        updateValue(arr, n, 1, 10);

        // Find GCD after the value is updated
        document.write(getGcd(n, 1, 3));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
3
1
```