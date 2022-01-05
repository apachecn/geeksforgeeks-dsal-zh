# 数组范围查询，通过更新计算强大的数字

> 原文:[https://www . geesforgeks . org/array-range-query-to-count-power-numbers-with-updates/](https://www.geeksforgeeks.org/array-range-queries-to-count-powerful-numbers-with-updates/)

给定一个 N 个整数的数组，任务是对给定的数组执行以下两个操作:

> **查询(L，R)** :从 L 到 R 打印子阵中[强大数字](https://www.geeksforgeeks.org/powerful-number/)的个数
> T5】更新(I，x) :将索引 I 处的值更新为 x，即 arr[i] = x

如果一个数 N 的每一个质因数 p，p <sup>2</sup> 也对其进行除法运算，那么这个数 N 就被称为**强数**。
**先决条件:** [强力号](https://www.geeksforgeeks.org/powerful-number/)[段树](https://www.geeksforgeeks.org/segment-tree-efficient-implementation/)
**示例:**

> **输入:**
> arr = {1，12，3，8，17，9}
> 查询 1:查询(L = 1，R = 4)
> 查询 2:更新(i = 1，x = 9)
> 查询 3:查询(L = 1，R = 4)
> **输出:**
> 1
> 2
> **解释:**
> 查询 1:arr[1:4]范围内的强力数字为 8
> 查询 2:更新操作后 arr[1:4]范围内的强力数字是 9 和 8。

**方法:**
因为我们需要处理点更新和范围查询，所以我们将使用**段树**来解决这个问题。

1.  我们将预计算所有[强大的数字](http://till the maximum value that arri can take, say MAX)直到 arr[i]能取的最大值，比如 **MAX** 。
    该操作的时间复杂度为 **O(MAX * sqrt(MAX))**

2.  **构建段树:**
    *   使用分段树可以将问题简化为[子阵和。](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/) 
    *   现在我们可以构建一个段树，其中叶节点将表示 **1** (当一个数是一个强有力的数)或 **0** (当一个数不是一个强有力的数)。所有内部节点都将有其两个子节点的总和。

3.  **点更新:**
    *   要更新一个元素，我们需要查看元素所在的区间，并相应地在左边或右边的子元素上递归。如果要更新的元素是一个强大的数字，那么我们将叶更新为 1，否则为 0。

4.  **范围查询:**
    *   每当我们得到一个从 L 到 R 的查询，那么我们就可以在段树中查询 L 到 R 范围内的节点的和，这又代表了 L 到 R 范围内的强力数的个数

以下是上述方法的实现:

## C++

```
// C++ Program to find the number
// of Powerful numbers in subarray
// using segment tree
#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

// Size of segment tree = 2^{log(MAX)+1}
int tree[3 * MAX];
int arr[MAX];
bool powerful[MAX + 1];

// Function to check if the
// number is powerful
bool isPowerful(int n)
{
    // First divide the number
    // repeatedly by 2
    while (n % 2 == 0)
    {
        int power = 0;
        while (n % 2 == 0)
        {
            n /= 2;
            power++;
        }

        // If only 2^1 divides
        // n (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2 then
    // this loop will execute
    // repeat above process
    for (int factor = 3; factor
         <= sqrt(n); factor += 2)
    {
        // Find highest power of
        // "factor" that divides n
        int power = 0;
        while (n % factor == 0)
        {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now if it is not
    // a prime numenr. Since prime
    // numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to build the array
void BuildArray(int input[], int n)
{
    for (int i = 0; i < n; i++)
    {
        // Check if input[i] is
        // a Powerful number or not
        if (powerful[input[i]])
            arr[i] = 1;

        else
            arr[i] = 0;
    }
    return;

}

// A utility function to get the middle
// index from corner indexes.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/* A recursive function that constructs
 Segment Tree for array[ss..se].

si --> Index of current node in the
       segment tree. Initially 0 is
       passed as root is always
       at index 0.
ss & se --> Starting and ending indexes
            of the segment represented by
            current node, i.e., st[index]
*/
void constructSTUtil(int si, int ss,
                     int se)
{
    if (ss == se) {
        // If there is one element
        // in array
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the two
    // values in this node
    else {
        int mid = getMid(ss, se);

        constructSTUtil(2 * si + 1,
                        ss, mid);

        constructSTUtil(2 * si + 2,
                        mid + 1, se);

        tree[si] = tree[2 * si + 1]
                  + tree[2 * si + 2];
    }
}

/* A recursive function to update the
nodes which have the given index
in their range.

si --> Index of current node in the segment tree.
       Initially 0 is passed as root is always
       at index 0.
ss & se --> Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]

ind --> Index of array to be updated

val --> The new value to be updated

*/
void updateValueUtil(int si, int ss, int se,
                     int idx, int val)
{
    // Leaf node
    if (ss == se) {
        tree[si] = tree[si] - arr[idx] + val;
        arr[idx] = val;
    }
    else {
        int mid = getMid(ss, se);

        // If idx is in the left child,
        // recurse on the left child
        if (ss <= idx and idx <= mid)
            updateValueUtil(2 * si + 1, ss,
                            mid, idx, val);

        // If idx is in the right child,
        // recurse on the right child
        else
            updateValueUtil(2 * si + 2, mid + 1,
                            se, idx, val);

        // Internal node will have the sum
        // of both of its children
        tree[si] = tree[2 * si + 1]
                   + tree[2 * si + 2];
    }
}

/* A recursive function to get the number
of Powerful numbers in a given
range of array indexes

si --> Index of current node in the segment tree.
       Initially 0 is passed as root is always
       at index 0.
ss & se --> Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]
l & r --> Starting and ending indexes of
          query range

 */
int queryPowerfulUtil(int si, int ss, int se,
                      int l, int r)
{
    // If segment of this node is
    // outside the given range
    if (r < ss or se < l) {
        return 0;
    }
    // If segment of this node is a part
    // of given range, then return the
    // number of composites
    // in the segment
    if (l <= ss and se <= r) {
        return tree[si];
    }

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    int p1 = queryPowerfulUtil(2 * si + 1,
                               ss, mid, l,
                               r);
    int p2 = queryPowerfulUtil(2 * si + 2,
                               mid + 1,
                               se, l, r);
    return (p1 + p2);
}

void queryPowerful(int n, int l, int r)
{
    printf("Number of Powerful numbers between %d to %d = %d\n",
           l, r, queryPowerfulUtil(0, 0,
                                   n - 1,
                                   l, r));
}

void updateValue(int n, int ind, int val)
{
    // If val is a Powerful number
    // we will update 1 in tree
    if (powerful[val])
        updateValueUtil(0, 0, n - 1,
                        ind, 1);
    else
        updateValueUtil(0, 0, n - 1,
                        ind, 0);
}

void precomputePowerful()
{

    memset(powerful, false,
           sizeof(powerful));

    // Computing all Powerful
    // numbers till MAX
    for (int i = 1; i <= MAX; i++)
    {
        // If the number is
        // Powerful make
        // powerful[i] = true
        if (isPowerful(i))
            powerful[i] = true;
    }
}

// Driver Code
int main()
{
    // Precompute all the powerful
    // numbers till MAX
    precomputePowerful();

    // Input array
    int input[] = { 4, 5, 18, 27, 40, 144 };

    // Size of Input array
    int n = sizeof(input) / sizeof(input[0]);

    // Build the array.
    BuildArray(input, n);

    // Build segment tree from
    // given array
    constructSTUtil(0, 0, n - 1);

    // Query 1: Query(L = 0, R = 3)
    int l = 0, r = 3;
    queryPowerful(n, l, r);

    // Query 2: Update(i = 1, x = 9),
    // i.e Update input[i] to x
    int i = 1;
    int val = 9;
    updateValue(n, i, val);

    // Query 3: Query(L = 0, R = 3)
    queryPowerful(n, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of Powerful numbers in subarray
// using segment tree
import java.util.*;

class GFG{

static final int MAX = 100000;

// Size of segment tree = 2^{log(MAX)+1}
static int []tree = new int[3 * MAX];
static int []arr = new int[MAX];
static boolean []powerful = new boolean[MAX + 1];

// Function to check if the
// number is powerful
static boolean isPowerful(int n)
{

    // First divide the number
    // repeatedly by 2
    while (n % 2 == 0)
    {
        int power = 0;
        while (n % 2 == 0)
        {
            n /= 2;
            power++;
        }

        // If only 2^1 divides
        // n (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2 then
    // this loop will execute
    // repeat above process
    for(int factor = 3;
            factor <= Math.sqrt(n);
            factor += 2)
    {

        // Find highest power of
        // "factor" that divides n
        int power = 0;
        while (n % factor == 0)
        {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now if it is not
    // a prime numenr. Since prime
    // numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to build the array
static void BuildArray(int input[], int n)
{
    for(int i = 0; i < n; i++)
    {

        // Check if input[i] is
        // a Powerful number or not
        if (powerful[input[i]])
            arr[i] = 1;

        else
            arr[i] = 0;
    }
    return;
}

// A utility function to get the middle
// index from corner indexes.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/* A recursive function that constructs
Segment Tree for array[ss..se].

si -. Index of current node in the
    segment tree. Initially 0 is
    passed as root is always
    at index 0.
ss & se -. Starting and ending indexes
            of the segment represented by
            current node, i.e., st[index]
*/
static void constructSTUtil(int si, int ss,
                            int se)
{
    if (ss == se)
    {

        // If there is one element
        // in array
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the two
    // values in this node
    else
    {
        int mid = getMid(ss, se);

        constructSTUtil(2 * si + 1,
                        ss, mid);

        constructSTUtil(2 * si + 2,
                        mid + 1, se);

        tree[si] = tree[2 * si + 1] +
                   tree[2 * si + 2];
    }
}

/* A recursive function to update the
nodes which have the given index
in their range.

si -. Index of current node in the segment tree.
    Initially 0 is passed as root is always
    at index 0.
ss & se -. Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]

ind -. Index of array to be updated

val -. The new value to be updated

*/
static void updateValueUtil(int si, int ss, int se,
                            int idx, int val)
{

    // Leaf node
    if (ss == se)
    {
        tree[si] = tree[si] - arr[idx] + val;
        arr[idx] = val;
    }
    else
    {
        int mid = getMid(ss, se);

        // If idx is in the left child,
        // recurse on the left child
        if (ss <= idx && idx <= mid)
            updateValueUtil(2 * si + 1, ss,
                            mid, idx, val);

        // If idx is in the right child,
        // recurse on the right child
        else
            updateValueUtil(2 * si + 2, mid + 1,
                            se, idx, val);

        // Internal node will have the sum
        // of both of its children
        tree[si] = tree[2 * si + 1] +
                   tree[2 * si + 2];
    }
}

/* A recursive function to get the number
of Powerful numbers in a given
range of array indexes

si -. Index of current node in the segment tree.
    Initially 0 is passed as root is always
    at index 0.
ss & se -. Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]
l & r -. Starting and ending indexes of
        query range

*/
static int queryPowerfulUtil(int si, int ss,
                             int se, int l, int r)
{

    // If segment of this node is
    // outside the given range
    if (r < ss || se < l)
    {
        return 0;
    }

    // If segment of this node is a part
    // of given range, then return the
    // number of composites
    // in the segment
    if (l <= ss && se <= r)
    {
        return tree[si];
    }

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    int p1 = queryPowerfulUtil(2 * si + 1,
                               ss, mid, l,
                               r);
    int p2 = queryPowerfulUtil(2 * si + 2,
                                  mid + 1,
                                 se, l, r);
    return (p1 + p2);
}

static void queryPowerful(int n, int l, int r)
{
    System.out.printf("Number of Powerful numbers " +
                      "between %d to %d = %d\n", l, r,
                      queryPowerfulUtil(0, 0, n - 1,
                                        l, r));
}

static void updateValue(int n, int ind, int val)
{

    // If val is a Powerful number
    // we will update 1 in tree
    if (powerful[val])
        updateValueUtil(0, 0, n - 1,
                        ind, 1);
    else
        updateValueUtil(0, 0, n - 1,
                        ind, 0);
}

static void precomputePowerful()
{
    Arrays.fill(powerful, false);

    // Computing all Powerful
    // numbers till MAX
    for(int i = 1; i <= MAX; i++)
    {

        // If the number is
        // Powerful make
        // powerful[i] = true
        if (isPowerful(i))
            powerful[i] = true;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Precompute all the powerful
    // numbers till MAX
    precomputePowerful();

    // Input array
    int input[] = { 4, 5, 18, 27, 40, 144 };

    // Size of Input array
    int n = input.length;

    // Build the array.
    BuildArray(input, n);

    // Build segment tree from
    // given array
    constructSTUtil(0, 0, n - 1);

    // Query 1: Query(L = 0, R = 3)
    int l = 0, r = 3;
    queryPowerful(n, l, r);

    // Query 2: Update(i = 1, x = 9),
    // i.e Update input[i] to x
    int i = 1;
    int val = 9;
    updateValue(n, i, val);

    // Query 3: Query(L = 0, R = 3)
    queryPowerful(n, l, r);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to find the number
# of Powerful numbers in subarray
# using segment tree
import math
MAX = 100000

# Size of segment tree = 2^{log(MAX)+1}
tree = [0]*(3 * MAX)
arr = [0]*(MAX)
powerful = [False]*(MAX + 1)

# Function to check if the
# number is powerful
def isPowerful(n):

    # First divide the number
    # repeatedly by 2
    while (n % 2 == 0):
        power = 0
        while (n % 2 == 0):
            n = int(n / 2)
            power += 1

        # If only 2^1 divides
        # n (not higher powers),
        # then return false
        if (power == 1):
            return False

    # If n is not a power of 2 then
    # this loop will execute
    # repeat above process
    for factor in range(3, int(math.sqrt(n)) + 1, 2):

        # Find highest power of
        # "factor" that divides n
        power = 0
        while (n % factor == 0):
            n = int(n / factor)
            power += 1

        # If only factor^1 divides n
        # (not higher powers),
        # then return false
        if (power == 1):
            return False

    # n must be 1 now if it is not
    # a prime numenr. Since prime
    # numbers are not powerful,
    # we return false if n is not 1.
    return (n == 1)

# Function to build the array
def BuildArray(Input, n):
    for i in range(n):

        # Check if input[i] is
        # a Powerful number or not
        if (powerful[Input[i]]):
            arr[i] = 1
        else:
            arr[i] = 0
    return

# A utility function to get the middle
# index from corner indexes.
def getMid(s, e):
    return s + int((e - s) / 2)

""" A recursive function that constructs
Segment Tree for array[ss..se].

si -. Index of current node in the
    segment tree. Initially 0 is
    passed as root is always
    at index 0.
ss & se -. Starting and ending indexes
            of the segment represented by
            current node, i.e., st[index]
"""
def constructSTUtil(si, ss, se):
    if (ss == se):
        # If there is one element
        # in array
        tree[si] = arr[ss]
        return

    # If there are more than one elements,
    # then recur for left and right subtrees
    # and store the sum of the two
    # values in this node
    else:
        mid = getMid(ss, se)
        constructSTUtil(2 * si + 1, ss, mid)
        constructSTUtil(2 * si + 2, mid + 1, se)
        tree[si] = tree[2 * si + 1] + tree[2 * si + 2]

""" A recursive function to update the
nodes which have the given index
in their range.

si -. Index of current node in the segment tree.
    Initially 0 is passed as root is always
    at index 0.
ss & se -. Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]

ind -. Index of array to be updated

val -. The new value to be updated

"""
def updateValueUtil(si, ss, se, idx, val):
    # Leaf node
    if (ss == se):
        tree[si] = tree[si] - arr[idx] + val
        arr[idx] = val
    else:
        mid = getMid(ss, se)
        # If idx is in the left child,
        # recurse on the left child
        if (ss <= idx and idx <= mid):
            updateValueUtil(2 * si + 1, ss, mid, idx, val)

        # If idx is in the right child,
        # recurse on the right child
        else:
            updateValueUtil(2 * si + 2, mid + 1, se, idx, val)

        # Internal node will have the sum
        # of both of its children
        tree[si] = tree[2 * si + 1] + tree[2 * si + 2]

""" A recursive function to get the number
of Powerful numbers in a given
range of array indexes

si -. Index of current node in the segment tree.
    Initially 0 is passed as root is always
    at index 0.
ss & se -. Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]
l & r -. Starting and ending indexes of
        query range
"""
def queryPowerfulUtil(si, ss, se, l, r):

    # If segment of this node is
    # outside the given range
    if (r < ss or se < l):
        return 0

    # If segment of this node is a part
    # of given range, then return the
    # number of composites
    # in the segment
    if (l <= ss and se <= r):
        return tree[si]

    # If a part of this segment
    # overlaps with the given range
    mid = getMid(ss, se)
    p1 = queryPowerfulUtil(2 * si + 1, ss, mid, l, r)
    p2 = queryPowerfulUtil(2 * si + 2, mid + 1, se, l, r)
    return (p1 + p2)

def queryPowerful(n, l, r):
    print("Number of Powerful numbers between", l, "to", r, "=", queryPowerfulUtil(0, 0, n - 1, l, r))

def updateValue(n, ind, val):

    # If val is a Powerful number
    # we will update 1 in tree
    if (powerful[val]):
        updateValueUtil(0, 0, n - 1, ind, 1)
    else:
        updateValueUtil(0, 0, n - 1, ind, 0)

def precomputePowerful():
    for i in range(MAX + 1):
        powerful[i] = False

    # Computing all Powerful
    # numbers till MAX
    for i in range(1, MAX + 1):

        # If the number is
        # Powerful make
        # powerful[i] = true
        if (isPowerful(i)):
            powerful[i] = True

# Precompute all the powerful
# numbers till MAX
precomputePowerful()

# Input array
Input = [ 4, 5, 18, 27, 40, 144 ]

# Size of Input array
n = len(Input)

# Build the array.
BuildArray(Input, n)

# Build segment tree from
# given array
constructSTUtil(0, 0, n - 1)

# Query 1: Query(L = 0, R = 3)
l, r = 0, 3
queryPowerful(n, l, r)

# Query 2: Update(i = 1, x = 9),
# i.e Update input[i] to x
i = 1
val = 9
updateValue(n, i, val)

# Query 3: Query(L = 0, R = 3)
queryPowerful(n, l, r)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to find the number
// of Powerful numbers in subarray
// using segment tree
using System;
class GFG{

static readonly int MAX = 100000;

// Size of segment tree = 2^{log(MAX)+1}
static int []tree = new int[3 * MAX];
static int []arr = new int[MAX];
static bool []powerful = new bool[MAX + 1];

// Function to check if the
// number is powerful
static bool isPowerful(int n)
{

    // First divide the number
    // repeatedly by 2
    while (n % 2 == 0)
    {
        int power = 0;
        while (n % 2 == 0)
        {
            n /= 2;
            power++;
        }

        // If only 2^1 divides
        // n (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2 then
    // this loop will execute
    // repeat above process
    for(int factor = 3;
            factor <= Math.Sqrt(n);
            factor += 2)
    {

        // Find highest power of
        // "factor" that divides n
        int power = 0;
        while (n % factor == 0)
        {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n
        // (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now if it is not
    // a prime numenr. Since prime
    // numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Function to build the array
static void BuildArray(int []input, int n)
{
    for(int i = 0; i < n; i++)
    {

        // Check if input[i] is
        // a Powerful number or not
        if (powerful[input[i]])
            arr[i] = 1;

        else
            arr[i] = 0;
    }
    return;
}

// A utility function to get the middle
// index from corner indexes.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

/* A recursive function that constructs
Segment Tree for array[ss..se].

si -. Index of current node in the
    segment tree. Initially 0 is
    passed as root is always
    at index 0.
ss & se -. Starting and ending indexes
            of the segment represented by
            current node, i.e., st[index]
*/
static void constructSTUtil(int si, int ss,
                            int se)
{
    if (ss == se)
    {

        // If there is one element
        // in array
        tree[si] = arr[ss];
        return;
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the two
    // values in this node
    else
    {
        int mid = getMid(ss, se);

        constructSTUtil(2 * si + 1,
                        ss, mid);

        constructSTUtil(2 * si + 2,
                        mid + 1, se);

        tree[si] = tree[2 * si + 1] +
                   tree[2 * si + 2];
    }
}

/* A recursive function to update the
nodes which have the given index
in their range.

si -. Index of current node in the segment tree.
    Initially 0 is passed as root is always
    at index 0.
ss & se -. Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]

ind -. Index of array to be updated

val -. The new value to be updated

*/
static void updateValueUtil(int si, int ss, int se,
                            int idx, int val)
{

    // Leaf node
    if (ss == se)
    {
        tree[si] = tree[si] - arr[idx] + val;
        arr[idx] = val;
    }
    else
    {
        int mid = getMid(ss, se);

        // If idx is in the left child,
        // recurse on the left child
        if (ss <= idx && idx <= mid)
            updateValueUtil(2 * si + 1, ss,
                            mid, idx, val);

        // If idx is in the right child,
        // recurse on the right child
        else
            updateValueUtil(2 * si + 2, mid + 1,
                            se, idx, val);

        // Internal node will have the sum
        // of both of its children
        tree[si] = tree[2 * si + 1] +
                   tree[2 * si + 2];
    }
}

/* A recursive function to get the number
of Powerful numbers in a given
range of array indexes

si -. Index of current node in the segment tree.
    Initially 0 is passed as root is always
    at index 0.
ss & se -. Starting and ending indexes of the
            segment represented by current node,
            i.e., st[index]
l & r -. Starting and ending indexes of
        query range

*/
static int queryPowerfulUtil(int si, int ss,
                             int se, int l, int r)
{

    // If segment of this node is
    // outside the given range
    if (r < ss || se < l)
    {
        return 0;
    }

    // If segment of this node is a part
    // of given range, then return the
    // number of composites
    // in the segment
    if (l <= ss && se <= r)
    {
        return tree[si];
    }

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    int p1 = queryPowerfulUtil(2 * si + 1,
                               ss, mid, l,
                               r);
    int p2 = queryPowerfulUtil(2 * si + 2,
                                  mid + 1,
                                 se, l, r);
    return (p1 + p2);
}

static void queryPowerful(int n, int l, int r)
{
    Console.WriteLine("Number of Powerful numbers " +
                      "between " + l +" to "+r+" = "+
                      queryPowerfulUtil(0, 0, n - 1,
                                        l, r));
}

static void updateValue(int n, int ind, int val)
{

    // If val is a Powerful number
    // we will update 1 in tree
    if (powerful[val])
        updateValueUtil(0, 0, n - 1,
                        ind, 1);
    else
        updateValueUtil(0, 0, n - 1,
                        ind, 0);
}

static void precomputePowerful()
{

    for(int i = 0; i <= MAX; i++)
        powerful[i] = false;

    // Computing all Powerful
    // numbers till MAX
    for(int i = 1; i <= MAX; i++)
    {

        // If the number is
        // Powerful make
        // powerful[i] = true
        if (isPowerful(i))
            powerful[i] = true;
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Precompute all the powerful
    // numbers till MAX
    precomputePowerful();

    // Input array
    int []input = { 4, 5, 18, 27, 40, 144 };

    // Size of Input array
    int n = input.Length;

    // Build the array.
    BuildArray(input, n);

    // Build segment tree from
    // given array
    constructSTUtil(0, 0, n - 1);

    // Query 1: Query(L = 0, R = 3)
    int l = 0, r = 3;
    queryPowerful(n, l, r);

    // Query 2: Update(i = 1, x = 9),
    // i.e Update input[i] to x
    int i = 1;
    int val = 9;
    updateValue(n, i, val);

    // Query 3: Query(L = 0, R = 3)
    queryPowerful(n, l, r);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript program to find the number
    // of Powerful numbers in subarray
    // using segment tree

    let MAX = 100000;

    // Size of segment tree = 2^{log(MAX)+1}
    let tree = new Array(3 * MAX);
    let arr = new Array(MAX);
    let powerful = new Array(MAX + 1);

    // Function to check if the
    // number is powerful
    function isPowerful(n)
    {

        // First divide the number
        // repeatedly by 2
        while (n % 2 == 0)
        {
            let power = 0;
            while (n % 2 == 0)
            {
                n = parseInt(n / 2, 10);
                power++;
            }

            // If only 2^1 divides
            // n (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // If n is not a power of 2 then
        // this loop will execute
        // repeat above process
        for(let factor = 3;
                factor <= Math.sqrt(n);
                factor += 2)
        {

            // Find highest power of
            // "factor" that divides n
            let power = 0;
            while (n % factor == 0)
            {
                n = parseInt(n / factor, 10);
                power++;
            }

            // If only factor^1 divides n
            // (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // n must be 1 now if it is not
        // a prime numenr. Since prime
        // numbers are not powerful,
        // we return false if n is not 1.
        return (n == 1);
    }

    // Function to build the array
    function BuildArray(input, n)
    {
        for(let i = 0; i < n; i++)
        {

            // Check if input[i] is
            // a Powerful number or not
            if (powerful[input[i]])
                arr[i] = 1;

            else
                arr[i] = 0;
        }
        return;
    }

    // A utility function to get the middle
    // index from corner indexes.
    function getMid(s, e)
    {
        return s + parseInt((e - s) / 2, 10);
    }

    /* A recursive function that constructs
    Segment Tree for array[ss..se].

    si -. Index of current node in the
        segment tree. Initially 0 is
        passed as root is always
        at index 0.
    ss & se -. Starting and ending indexes
                of the segment represented by
                current node, i.e., st[index]
    */
    function constructSTUtil(si, ss, se)
    {
        if (ss == se)
        {

            // If there is one element
            // in array
            tree[si] = arr[ss];
            return;
        }

        // If there are more than one elements,
        // then recur for left and right subtrees
        // and store the sum of the two
        // values in this node
        else
        {
            let mid = getMid(ss, se);

            constructSTUtil(2 * si + 1,
                            ss, mid);

            constructSTUtil(2 * si + 2,
                            mid + 1, se);

            tree[si] = tree[2 * si + 1] +
                       tree[2 * si + 2];
        }
    }

    /* A recursive function to update the
    nodes which have the given index
    in their range.

    si -. Index of current node in the segment tree.
        Initially 0 is passed as root is always
        at index 0.
    ss & se -. Starting and ending indexes of the
                segment represented by current node,
                i.e., st[index]

    ind -. Index of array to be updated

    val -. The new value to be updated

    */
    function updateValueUtil(si, ss, se, idx, val)
    {

        // Leaf node
        if (ss == se)
        {
            tree[si] = tree[si] - arr[idx] + val;
            arr[idx] = val;
        }
        else
        {
            let mid = getMid(ss, se);

            // If idx is in the left child,
            // recurse on the left child
            if (ss <= idx && idx <= mid)
                updateValueUtil(2 * si + 1, ss,
                                mid, idx, val);

            // If idx is in the right child,
            // recurse on the right child
            else
                updateValueUtil(2 * si + 2, mid + 1,
                                se, idx, val);

            // Internal node will have the sum
            // of both of its children
            tree[si] = tree[2 * si + 1] +
                       tree[2 * si + 2];
        }
    }

    /* A recursive function to get the number
    of Powerful numbers in a given
    range of array indexes

    si -. Index of current node in the segment tree.
        Initially 0 is passed as root is always
        at index 0.
    ss & se -. Starting and ending indexes of the
                segment represented by current node,
                i.e., st[index]
    l & r -. Starting and ending indexes of
            query range

    */
    function queryPowerfulUtil(si, ss, se, l, r)
    {

        // If segment of this node is
        // outside the given range
        if (r < ss || se < l)
        {
            return 0;
        }

        // If segment of this node is a part
        // of given range, then return the
        // number of composites
        // in the segment
        if (l <= ss && se <= r)
        {
            return tree[si];
        }

        // If a part of this segment
        // overlaps with the given range
        let mid = getMid(ss, se);
        let p1 = queryPowerfulUtil(2 * si + 1,
                                   ss, mid, l,
                                   r);
        let p2 = queryPowerfulUtil(2 * si + 2,
                                      mid + 1,
                                     se, l, r);
        return (p1 + p2);
    }

    function queryPowerful(n, l, r)
    {
        document.write("Number of Powerful numbers " +
                          "between " + l +" to "+r+" = "+
                          queryPowerfulUtil(0, 0, n - 1,
                                            l, r) + "</br>");
    }

    function updateValue(n, ind, val)
    {

        // If val is a Powerful number
        // we will update 1 in tree
        if (powerful[val])
            updateValueUtil(0, 0, n - 1,
                            ind, 1);
        else
            updateValueUtil(0, 0, n - 1,
                            ind, 0);
    }

    function precomputePowerful()
    {

        for(let i = 0; i <= MAX; i++)
            powerful[i] = false;

        // Computing all Powerful
        // numbers till MAX
        for(let i = 1; i <= MAX; i++)
        {

            // If the number is
            // Powerful make
            // powerful[i] = true
            if (isPowerful(i))
                powerful[i] = true;
        }
    }

    // Precompute all the powerful
    // numbers till MAX
    precomputePowerful();

    // Input array
    let input = [ 4, 5, 18, 27, 40, 144 ];

    // Size of Input array
    let n = input.length;

    // Build the array.
    BuildArray(input, n);

    // Build segment tree from
    // given array
    constructSTUtil(0, 0, n - 1);

    // Query 1: Query(L = 0, R = 3)
    let l = 0, r = 3;
    queryPowerful(n, l, r);

    // Query 2: Update(i = 1, x = 9),
    // i.e Update input[i] to x
    let i = 1;
    let val = 9;
    updateValue(n, i, val);

    // Query 3: Query(L = 0, R = 3)
    queryPowerful(n, l, r);

</script>
```

**Output:** 

```
Number of Powerful numbers between 0 to 3 = 2
Number of Powerful numbers between 0 to 3 = 3
```

**时间复杂度:**每查询 0(logN)