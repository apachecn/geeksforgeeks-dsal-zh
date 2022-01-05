# 数组范围查询，通过更新找到最大阿姆斯特朗数

> 原文:[https://www . geeksforgeeks . org/array-range-query-to-find-max-Armstrong-number-with-updates/](https://www.geeksforgeeks.org/array-range-queries-to-find-the-maximum-armstrong-number-with-updates/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是执行以下两个查询:

*   **最大值(开始，结束)**:从开始到结束打印子数组中元素的最大阿姆斯特朗数
*   **更新(I，x)** :将 x 添加到数组索引 **i** 引用的数组元素中，即:arr[i] = x

如果子阵列中没有阿姆斯特朗编号，打印 **-1** 。

**示例:**

> **输入:**arr =【192，113，535，7，19，111】
> 查询 1:最大值(start=1，end=3)
> 查询 2:更新(i=1，x=153)即 arr[1]=153
> **输出:**
> 给定范围内最大阿姆斯特朗数= 7
> 给定范围内更新最大阿姆斯特朗数= 153
> **解释:**[113，535，7]
> 因此，7 是给定范围内的最大阿姆斯特朗数。
> 在更新查询中，索引 1 处的值更新为 153，数组 arr 现在为[192，153，535，7，19，111]
> 在更新最大查询中，子数组[1…3]有 2 个阿姆斯特朗数 153 和 7，即。[153，535，7]
> 因此，153 是给定范围内的最大阿姆斯特朗数。

**简单解法:**
简单解法是从 l 到 r 运行一个循环，计算给定范围内元素的最大 Armstrong 个数。要更新一个值，只需执行 arr[i] = x。第一个操作需要 **O(N)** 时间，第二个操作需要 **O(1)** 时间。

**有效方法:**

*   一个有效的方法是建立一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，其中每个节点存储两个值(**值**和 **max_set_bits** ，并对其进行范围查询以找到最大阿姆斯特朗数。
*   如果我们深入研究一下，任何两个射程组合的最大阿姆斯特朗数要么是左侧的最大阿姆斯特朗数，要么是右侧的最大阿姆斯特朗数，以最大者为准。
*   **段树的表示:**
    1.  叶节点是给定数组的元素。
    2.  每个内部节点代表其所有子节点的最大阿姆斯特朗数，或者-1 表示该范围内不存在阿姆斯特朗数。
    3.  树的数组表示用于表示段树。对于索引 I 处的每个节点，左子节点位于索引 ***2*i+1*** ，右子节点位于 ***2*i+2*** ，父节点位于 ***(i-1)/2*** 。
*   **从给定数组构建段树:**
    1.  我们从片段 arr[0]开始。。。n-1]，并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们在段树节点中存储最大 Armstrong number 值或-1。构建的段树的所有层都将被完全填充，除了最后一层。此外，该树将是一个完整的二叉树，因为我们总是在每一层将片段分成两半。由于构造的树总是一棵有 n 片叶子的完全二叉树，因此会有 n-1 个内部节点。因此**总节点**将为**2 * n–1**。段树的高度为**原木 <sub>2</sub> n** 。由于树是用数组表示的，父索引和子索引之间的关系必须保持，因此为段树分配的内存大小将是**2 *(2<sup>ceil(log</sup><sub><sup>2</sup></sub><sup>n)</sup>)–1**。
    2.  n 位数的正整数被称为 n 阶阿姆斯特朗数(阶是位数)，如果

> abcd… =功率(a，n) +功率(b，n) +功率(c，n) +功率(d，n) + …。

*   为了检查阿姆斯特朗数字，想法是首先计数数字位数(或寻找顺序)。让位数为 n，对于输入数 x 中的每一个数字 r，计算 r <sup>n</sup> 。如果所有这些值的总和等于 n，则返回 true 否则返回 false。
*   然后，我们对段树进行范围查询，找出给定范围的最大阿姆斯特朗数，并输出相应的值。

以下是上述方法的实现:

## C++

```
// C++ code to implement above approach

#include <bits/stdc++.h>
using namespace std;

// A utility function to get the
// middle index of given range.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Function that return true
// if num is armstrong
// else return false
bool isArmstrong(int x)
{
    int n = to_string(x).size();
    int sum1 = 0;
    int temp = x;
    while (temp > 0) {
        int digit = temp % 10;
        sum1 += pow(digit, n);
        temp /= 10;
    }
    if (sum1 == x)
        return true;
    return false;
}

/*  A recursive function to get
    the sum of values in the
    given range of the array.
    The following are parameters
    for this function.

st -> Pointer to segment tree
node -> Index of current node in
        the segment tree .
ss & se -> Starting and ending indexes
           of the segment represented
           by current node,
           i.e., st[node]
l & r -> Starting and ending indexes
         of range query */
int MaxUtil(
    int* st, int ss, int se, int l,
    int r, int node)
{

    // If segment of this node is
    // completely part of given range,
    // then return the max of segment.
    if (l <= ss && r >= se)
        return st[node];

    // If segment of this node does not
    // belong to given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node is
    // partially the part of given
    // range
    int mid = getMid(ss, se);

    return max(
        MaxUtil(st, ss, mid,
                l, r, 2 * node + 1),
        MaxUtil(st, mid + 1, se,
                l, r, 2 * node + 2));
}

/* A recursive function to update
   the nodes which have the given
   the index in their range. The
   following are parameters st, ss
   and se are same as defined above
   index -> index of the element
   to be updated.*/

void updateValue(int arr[],
                 int* st,int ss,
                 int se, int index,
                 int value, int node) {

    if (index < ss || index > se) {
        cout << "Invalid Input" << endl;
        return;
    }

    if (ss == se) {
        // update value in array
        // and in segment tree
        arr[index] = value;

        if (isArmstrong(value))
            st[node] = value;
        else
            st[node] = -1;
    }
    else {
        int mid = getMid(ss, se);

        if (index >= ss && index <= mid)
            updateValue(arr, st, ss,
                        mid, index, value,
                        2 * node + 1);
        else
            updateValue(arr, st, mid + 1,
                        se, index, value,
                        2 * node + 2);

        st[node] = max(st[2 * node + 1],
                       st[2 * node + 2]);
    }
    return;
}

// Return max of elements in
// range from index
// l (query start) to r (query end).

int getMax(int* st, int n,
           int l, int r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1
        || l > r) {
        printf("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1,
                   l, r, 0);
}

// A recursive function that
// constructs Segment Tree for
// array[ss..se]. si is index of
// current node in segment tree st
int constructSTUtil(int arr[],
                    int ss, int se,
                    int* st, int si)
{
    // If there is one
    // element in array, store
    // it in current node of
    // segment tree and return
    if (ss == se) {
        if (isArmstrong(arr[ss]))
            st[si] = arr[ss];
        else
            st[si] = -1;
        return st[si];
    }

    // If there are more than
    // one elements, then
    // recur for left and right
    // subtrees and store the
    // max of values in this node

    int mid = getMid(ss, se);

    st[si] = max(constructSTUtil(
                     arr, ss, mid, st,
                     si * 2 + 1),
                 constructSTUtil(
                     arr, mid + 1, se,
                     st, si * 2 + 2));

    return st[si];
}

/* Function to construct a segment tree
   from given array. This function
   allocates memory for segment tree.*/

int* constructST(int arr[], int n)
{
    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size
        = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0,
                    n - 1, st, 0);

    // Return the constructed
    // segment tree
    return st;
}

// Driver code
int main()
{
    int arr[] = { 192, 113,
                  535, 7, 19, 111 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from
    // given array
    int* st = constructST(arr, n);

    // Print max of values in array
    // from index 1 to 3
    cout << "Maximum armstrong "
         << "number in given range = "
         << getMax(st, n, 1, 3) << endl;

    // Update: set arr[1] = 153 and update
    // corresponding segment tree nodes.
    updateValue(arr, st, 0,
                n - 1, 1, 153, 0);

    // Find max after the value is updated
    cout << "Updated Maximum armstrong "
         << "number in given range = "
         << getMax(st, n, 1, 3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement
// the above approach
import java.util.*;
class GFG{

// A utility function to get the
// middle index of given range.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Function that return true
// if num is armstrong
// else return false
static boolean isArmstrong(int x)
{
    int n = String.valueOf(x).length();
    int sum1 = 0;
    int temp = x;
    while (temp > 0)
    {
        int digit = temp % 10;
        sum1 += Math.pow(digit, n);
        temp /= 10;
    }
    if (sum1 == x)
        return true;
    return false;
}

/* A recursive function to get
the sum of values in the
given range of the array.
The following are parameters
for this function.
st.Pointer to segment tree
node.Index of current node in
the segment tree .
ss & se.Starting and ending indexes
of the segment represented
by current node, i.e., st[node]
l & r.Starting and ending indexes
of range query */
static int MaxUtil(int []st, int ss,
                   int se, int l,
                   int r, int node)
{
    // If segment of this node is
    // completely part of given range,
    // then return the max of segment.
    if (l <= ss && r >= se)
        return st[node];

    // If segment of this node does not
    // belong to given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node is
    // partially the part of given
    // range
    int mid = getMid(ss, se);

    return Math.max(MaxUtil(st, ss, mid,
                            l, r, 2 * node ),
                    MaxUtil(st, mid + 1,
                            se, l, r,
                            2 * node + 1));
}

/* A recursive function to update
the nodes which have the given
the index in their range. The
following are parameters st, ss
and se are same as defined above
index.index of the element
to be updated.*/
static void updateValue(int arr[],
                        int []st,int ss,
                        int se, int index,
                        int value, int node)
{
    if (index < ss || index > se)
    {
        System.out.print("Invalid Input" + "\n");
        return;
    }

    if (ss == se)
    {
        // update value in array
        // and in segment tree
        arr[index] = value;

        if (isArmstrong(value))
            st[node] = value;
        else
            st[node] = -1;
    }
    else
    {
        int mid = getMid(ss, se);

        if (index >= ss && index <= mid)
            updateValue(arr, st, ss,
                        mid, index,
                        value, 2 * node);
        else
            updateValue(arr, st, mid + 1,
                        se, index, value,
                        2 * node +1);

        st[node] = Math.max(st[2 * node + 1],
                            st[2 * node + 2]);
    }
    return;
}

// Return max of elements in
// range from index
// l (query start) to r (query end).
static int getMax(int []st, int n,
                  int l, int r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1 ||
        l > r)
    {
        System.out.printf("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1,
                       l, r, 0);
}

// A recursive function that
// constructs Segment Tree for
// array[ss..se]. si is index of
// current node in segment tree st
static int constructSTUtil(int arr[],
                           int ss, int se,
                           int []st, int si)
{
    // If there is one
    // element in array, store
    // it in current node of
    // segment tree and return
    if (ss == se)
    {
        if (isArmstrong(arr[ss]))
            st[si] = arr[ss];
        else
            st[si] = -1;
        return st[si];
    }

    // If there are more than
    // one elements, then
    // recur for left and right
    // subtrees and store the
    // max of values in this node

    int mid = getMid(ss, se);

    st[si] = Math.max(constructSTUtil(arr, ss,
                                      mid, st,
                                      si * 2 ),
                      constructSTUtil(arr, mid + 1,
                                      se, st,
                                      si * 2 + 1));

    return st[si];
}

/* Function to cona segment tree
from given array. This function
allocates memory for segment tree.*/
static int[] constructST(int arr[], int n)
{
    // Height of segment tree
    int x = (int)(Math.ceil(Math.log(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.pow(2, x) - 1;

    // Allocate memory
    int []st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0,
                     n - 1, st, 0);

    // Return the constructed
    // segment tree
    return st;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {192, 113,
                 535, 7, 19, 111};
    int n = arr.length;

    // Build segment tree from
    // given array
    int[] st = constructST(arr, n);

    // Print max of values in array
    // from index 1 to 3
    System.out.print("Maximum armstrong " +
                     "number in given range = " +
                      getMax(st, n, 1, 3) + "\n");

    // Update: set arr[1] = 153 and update
    // corresponding segment tree nodes.
    updateValue(arr, st, 0,
                n - 1, 1, 153, 0);

    // Find max after the value is updated
    System.out.print("Updated Maximum armstrong " +
                       "number in given range = " +
                       getMax(st, n, 1, 3) + "\n");

}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python code to implement above approach
import math

# A utility function to get the
# middle index of given range.
def getMid(s: int, e: int) -> int:
    return s + (e - s) // 2

# Function that return true
# if num is armstrong
# else return false
def isArmstrong(x: int) -> bool:
    n = len(str(x))
    sum1 = 0
    temp = x
    while (temp > 0):
        digit = temp % 10
        sum1 += pow(digit, n)
        temp //= 10

    if (sum1 == x):
        return True
    return False

'''  A recursive function to get
    the sum of values in the
    given range of the array.
    The following are parameters
    for this function.

st -> Pointer to segment tree
node -> Index of current node in
        the segment tree .
ss & se -> Starting and ending indexes
           of the segment represented
           by current node,
           i.e., st[node]
l & r -> Starting and ending indexes
         of range query '''
def MaxUtil(st, ss, se, l, r, node):

    # If segment of this node is
    # completely part of given range,
    # then return the max of segment.
    if (l <= ss and r >= se):
        return st[node]

    # If segment of this node does not
    # belong to given range
    if (se < l or ss > r):
        return -1

    # If segment of this node is
    # partially the part of given
    # range
    mid = getMid(ss, se)

    return max(MaxUtil(st, ss, mid, l, r, 2 * node + 1),
               MaxUtil(st, mid + 1, se, l, r, 2 * node + 2))

''' A recursive function to update
   the nodes which have the given
   the index in their range. The
   following are parameters st, ss
   and se are same as defined above
   index -> index of the element
   to be updated.'''
def updateValue(arr, st, ss, se, index, value, node):
    if (index < ss or index > se):
        print("Invalid Input")
        return
    if (ss == se):

        # update value in array
        # and in segment tree
        arr[index] = value
        if (isArmstrong(value)):
            st[node] = value
        else:
            st[node] = -1

    else:
        mid = getMid(ss, se)

        if (index >= ss and index <= mid):
            updateValue(arr, st, ss, mid, index, value, 2 * node + 1)
        else:
            updateValue(arr, st, mid + 1, se, index, value, 2 * node + 2)

        st[node] = max(st[2 * node + 1], st[2 * node + 2])
    return

# Return max of elements in
# range from index
# l (query start) to r (query end).
def getMax(st, n, l, r):

    # Check for erroneous input values
    if (l < 0 or r > n - 1 or l > r):
        print("Invalid Input")
        return -1
    return MaxUtil(st, 0, n - 1, l, r, 0)

# A recursive function that
# constructs Segment Tree for
# array[ss..se]. si is index of
# current node in segment tree st
def constructSTUtil(arr, ss, se, st, si):

    # If there is one
    # element in array, store
    # it in current node of
    # segment tree and return
    if (ss == se):
        if (isArmstrong(arr[ss])):
            st[si] = arr[ss]
        else:
            st[si] = -1
        return st[si]

    # If there are more than
    # one elements, then
    # recur for left and right
    # subtrees and store the
    # max of values in this node
    mid = getMid(ss, se)
    st[si] = max(constructSTUtil(arr, ss, mid, st, si * 2 + 1),
                 constructSTUtil(arr, mid + 1, se, st, si * 2 + 2))
    return st[si]

''' Function to construct a segment tree
   from given array. This function
   allocates memory for segment tree.'''
def constructST(arr, n):

    # Height of segment tree
    x = int(math.ceil(math.log2(n)))

    # Maximum size of segment tree
    max_size = 2 * int(math.pow(2, x)) - 1

    # Allocate memory
    st = [0 for _ in range(max_size)]

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0)

    # Return the constructed
    # segment tree
    return st

# Driver code
if __name__ == "__main__":

    arr = [192, 113, 535, 7, 19, 111]
    n = len(arr)

    # Build segment tree from
    # given array
    st = constructST(arr, n)

    # Print max of values in array
    # from index 1 to 3
    print("Maximum armstrong number in given range = {}".format(
        getMax(st, n, 1, 3)))

    # Update: set arr[1] = 153 and update
    # corresponding segment tree nodes.
    updateValue(arr, st, 0, n - 1, 1, 153, 0)

    # Find max after the value is updated
    print("Updated Maximum armstrong number in given range = {}".format(
        getMax(st, n, 1, 3)))

# This code is contributed by sanjeev2552
```

## C#

```
// C# code to implement
// the above approach
using System;
class GFG{

// A utility function to get the
// middle index of given range.
static int getMid(int s, int e)
{
  return s + (e - s) / 2;
}

// Function that return true
// if num is armstrong
// else return false
static bool isArmstrong(int x)
{
  int n = String.Join("", x).Length;
  int sum1 = 0;
  int temp = x;
  while (temp > 0)
  {
    int digit = temp % 10;
    sum1 += (int)Math.Pow(digit, n);
    temp /= 10;
  }
  if (sum1 == x)
    return true;
  return false;
}

/* A recursive function to get
the sum of values in the
given range of the array.
The following are parameters
for this function.
st.Pointer to segment tree
node.Index of current node in
the segment tree .
ss & se.Starting and ending indexes
of the segment represented
by current node, i.e., st[node]
l & r.Starting and ending indexes
of range query */
static int MaxUtil(int []st, int ss,
                   int se, int l,
                   int r, int node)
{
  // If segment of this node is
  // completely part of given range,
  // then return the max of segment.
  if (l <= ss && r >= se)
    return st[node];

  // If segment of this node does not
  // belong to given range
  if (se < l || ss > r)
    return -1;

  // If segment of this node is
  // partially the part of given
  // range
  int mid = getMid(ss, se);

  return Math.Max(MaxUtil(st, ss, mid,
                          l, r, 2 * node),
                  MaxUtil(st, mid + 1,
                          se, l, r,
                          2 * node + 1));
}

/* A recursive function to update
the nodes which have the given
the index in their range. The
following are parameters st, ss
and se are same as defined above
index.index of the element
to be updated.*/
static void updateValue(int []arr,
                        int []st, int ss,
                        int se, int index,
                        int value, int node)
{
  if (index < ss || index > se)
  {
    Console.Write("Invalid Input" + "\n");
    return;
  }

  if (ss == se)
  {
    // update value in array
    // and in segment tree
    arr[index] = value;

    if (isArmstrong(value))
      st[node] = value;
    else
      st[node] = -1;
  }
  else
  {
    int mid = getMid(ss, se);

    if (index >= ss && index <= mid)
      updateValue(arr, st, ss,
                  mid, index,
                  value, 2 * node);
    else
      updateValue(arr, st, mid + 1,
                  se, index, value,
                  2 * node + 1);

    st[node] = Math.Max(st[2 * node + 1],
                        st[2 * node + 2]);
  }
  return;
}

// Return max of elements in
// range from index
// l (query start) to r (query end).
static int getMax(int []st, int n,
                  int l, int r)
{
  // Check for erroneous input values
  if (l < 0 || r > n - 1 ||
      l > r)
  {
    Console.Write("Invalid Input");
    return -1;
  }

  return MaxUtil(st, 0, n - 1,
                 l, r, 0);
}

// A recursive function that
// constructs Segment Tree for
// array[ss..se]. si is index of
// current node in segment tree st
static int constructSTUtil(int []arr,
                           int ss, int se,
                           int []st, int si)
{
  // If there is one
  // element in array, store
  // it in current node of
  // segment tree and return
  if (ss == se)
  {
    if (isArmstrong(arr[ss]))
      st[si] = arr[ss];
    else
      st[si] = -1;
    return st[si];
  }

  // If there are more than
  // one elements, then
  // recur for left and right
  // subtrees and store the
  // max of values in this node
  int mid = getMid(ss, se);

  st[si] = Math.Max(constructSTUtil(arr, ss,
                                    mid, st,
                                    si * 2),
                    constructSTUtil(arr, mid + 1,
                                    se, st,
                                    si * 2 + 1));
  return st[si];
}

/* Function to cona segment tree
from given array. This function
allocates memory for segment tree.*/
static int[] constructST(int []arr, int n)
{
  // Height of segment tree
  int x = (int)(Math.Ceiling(Math.Log(n)));

  // Maximum size of segment tree
  int max_size = 2 * (int)Math.Pow(2, x) - 1;

  // Allocate memory
  int []st = new int[max_size];

  // Fill the allocated memory st
  constructSTUtil(arr, 0,
                  n - 1, st, 0);

  // Return the constructed
  // segment tree
  return st;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {192, 113,
               535, 7, 19, 111};
  int n = arr.Length;

  // Build segment tree from
  // given array
  int[] st = constructST(arr, n);

  // Print max of values in array
  // from index 1 to 3
  Console.Write("Maximum armstrong " +
                "number in given range = " +
                 getMax(st, n, 1, 3) + "\n");

  // Update: set arr[1] = 153 and update
  // corresponding segment tree nodes.
  updateValue(arr, st, 0,
              n - 1, 1, 153, 0);

  // Find max after the value is updated
  Console.Write("Updated Maximum armstrong " +
                "number in given range = " +
                 getMax(st, n, 1, 3) + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript code to implement
// the above approach

// A utility function to get the
// middle index of given range.
function getMid(s,e)
{
    return s + Math.floor((e - s) / 2);
}

// Function that return true
// if num is armstrong
// else return false
function isArmstrong(x)
{
    let n = (x).toString().length;
    let sum1 = 0;
    let temp = x;
    while (temp > 0)
    {
        let digit = temp % 10;
        sum1 += Math.pow(digit, n);
        temp = Math.floor(temp/10);
    }
    if (sum1 == x)
        return true;
    return false;
}

/* A recursive function to get
the sum of values in the
given range of the array.
The following are parameters
for this function.
st.Pointer to segment tree
node.Index of current node in
the segment tree .
ss & se.Starting and ending indexes
of the segment represented
by current node, i.e., st[node]
l & r.Starting and ending indexes
of range query */
function MaxUtil(st,ss,se,l,r,node)
{
    // If segment of this node is
    // completely part of given range,
    // then return the max of segment.
    if (l <= ss && r >= se)
        return st[node];

    // If segment of this node does not
    // belong to given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node is
    // partially the part of given
    // range
    let mid = getMid(ss, se);

    return Math.max(MaxUtil(st, ss, mid,
                            l, r, 2 * node ),
                    MaxUtil(st, mid + 1,
                            se, l, r,
                            2 * node + 1));
}

/* A recursive function to update
the nodes which have the given
the index in their range. The
following are parameters st, ss
and se are same as defined above
index.index of the element
to be updated.*/
function updateValue(arr,st,ss,se,index,value,node)
{
    if (index < ss || index > se)
    {
        document.write("Invalid Input" + "<br>");
        return;
    }

    if (ss == se)
    {
        // update value in array
        // and in segment tree
        arr[index] = value;

        if (isArmstrong(value))
            st[node] = value;
        else
            st[node] = -1;
    }
    else
    {
        let mid = getMid(ss, se);

        if (index >= ss && index <= mid)
            updateValue(arr, st, ss,
                        mid, index,
                        value, 2 * node);
        else
            updateValue(arr, st, mid + 1,
                        se, index, value,
                        2 * node +1);

        st[node] = Math.max(st[2 * node + 1],
                            st[2 * node + 2]);
    }
    return;
}

// Return max of elements in
// range from index
// l (query start) to r (query end).
function getMax(st,n,l,r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1 ||
        l > r)
    {
        document.write("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1,
                       l, r, 0);
}

// A recursive function that
// constructs Segment Tree for
// array[ss..se]. si is index of
// current node in segment tree st
function constructSTUtil(arr,ss,se,st,si)
{
    // If there is one
    // element in array, store
    // it in current node of
    // segment tree and return
    if (ss == se)
    {
        if (isArmstrong(arr[ss]))
            st[si] = arr[ss];
        else
            st[si] = -1;
        return st[si];
    }

    // If there are more than
    // one elements, then
    // recur for left and right
    // subtrees and store the
    // max of values in this node

    let mid = getMid(ss, se);

    st[si] = Math.max(constructSTUtil(arr, ss,
                                      mid, st,
                                      si * 2 ),
                      constructSTUtil(arr, mid + 1,
                                      se, st,
                                      si * 2 + 1));

    return st[si];
}

/* Function to cona segment tree
from given array. This function
allocates memory for segment tree.*/
function constructST(arr,n)
{
    // Height of segment tree
    let x = (Math.ceil(Math.log(n)));

    // Maximum size of segment tree
    let max_size = 2 * Math.pow(2, x) - 1;

    // Allocate memory
    let st = new Array(max_size);

    // Fill the allocated memory st
    constructSTUtil(arr, 0,
                     n - 1, st, 0);

    // Return the constructed
    // segment tree
    return st;
}

// Driver code
let arr=[192, 113,
                 535, 7, 19, 111];
let n = arr.length;

// Build segment tree from
// given array
let st = constructST(arr, n);

// Print max of values in array
// from index 1 to 3
document.write("Maximum armstrong " +
                 "number in given range = " +
                 getMax(st, n, 1, 3) + "<br>");

// Update: set arr[1] = 153 and update
// corresponding segment tree nodes.
updateValue(arr, st, 0,
            n - 1, 1, 153, 0);

// Find max after the value is updated
document.write("Updated Maximum armstrong " +
                 "number in given range = " +
                 getMax(st, n, 1, 3) + "<br>");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Maximum armstrong number in given range = 7 
Updated Maximum armstrong number in given range = 153
```

***时间复杂度:**每次查询更新的时间复杂度为 **O(log N)** ，构建段树的时间复杂度为 **O(N)***