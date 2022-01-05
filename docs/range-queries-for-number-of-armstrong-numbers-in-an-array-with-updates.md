# 数组中阿姆斯特朗数的范围查询和更新

> 原文:[https://www . geeksforgeeks . org/range-query-for-number-of-Armstrong-numbers-in-a-array-in-a-updates/](https://www.geeksforgeeks.org/range-queries-for-number-of-armstrong-numbers-in-an-array-with-updates/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是执行以下两个查询:

*   **查询(开始、结束)**:自始至终打印子阵中阿姆斯特朗编号的个数
*   **更新(I，x)** :将 x 添加到数组索引 **i** 引用的数组元素中，即:arr[i] = x

**示例:**

> **输入:** arr = { 18，153，8，9，14，5}
> 查询 1:查询(开始= 0，结束= 4)
> 查询 2:更新(i = 3，x = 11)
> 查询 3:查询(开始= 0，结束= 4)
> **输出:** 3
> 2
> **解释**
> 在**查询 1** 、
> 18 -= 18
> 153->1 * 1 * 1+5 * 5+3 * 3 * 3 = 153
> 8->8 = 8
> 9->9 = 9
> 14->1 * 1+4 * 4！= 14
> 子阵列【0…4】具有 **3** 阿姆斯特朗编号，即。{18，153，8，9，14}
> 在**查询 2** 中，索引 3 处的值更新为 11，
> 数组 arr 现在为，{ 18，153，8，11，14，5}
> 在**查询 3** ，
> 18 - > 1*1 + 8*8！= 18
> 153->1 * 1 * 1+5 * 5+3 * 3 * 3 = 153
> 8->8 = 8
> 9->1 * 1+1 * 1！= 11
> 14 - > 1*1 + 4*4！= 14
> 子阵列[0…4]具有 **2** 阿姆斯特朗编号，即。{18，153，8，11，14}

**方法:**为了处理点更新和范围查询，一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)最适合这个目的。
n 位数的正整数被称为 n 阶阿姆斯壮数(阶是位数)。

> abcd… =功率(a，n) +功率(b，n) +功率(c，n) +功率(d，n) + …。

为了检查阿姆斯特朗数字，想法是首先计数数字位数(或寻找顺序)。让位数为 n，对于输入数 x 中的每个数字 r，如果所有这些值的总和等于 n，则计算 r^n.，然后将其设置为 1，否则设置为 0。

**构建段树:**

*   这个问题现在被简化为[子阵和使用分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)的问题。
*   现在，我们可以构建段树，其中叶节点表示为 0(如果它不是阿姆斯特朗数)或 1(如果它是阿姆斯特朗数)。
*   段树的内部节点等于其子节点的总和，因此一个节点代表从 L 到 R 范围内的总阿姆斯特朗数，范围[L，R]位于该节点及其下的子树之下。

**处理查询和点更新:**

*   每当我们从头到尾收到一个查询时，我们可以在段树中查询从开始到结束范围内的节点总数，这又表示从开始到结束范围内的阿姆斯特朗数的数量。

*   为了执行点更新并将索引 I 处的值更新为 x，我们检查以下情况:
    让 arr 的旧值 <sub>i</sub> 为 y，新值为 x
    1.  **情况 1:如果 x 和 y 都是阿姆斯特朗数**
        子阵中阿姆斯特朗数的计数不变，所以我们只更新数组，不修改段树
    2.  **情况 2:如果 x 和 y 都不是阿姆斯特朗数**
        子阵中阿姆斯特朗数的计数不变，所以我们只更新数组，不修改段树
    3.  **情况 3:如果 y 是阿姆斯特朗数，但 x 不是**
        子阵中阿姆斯特朗数的计数减少，因此我们更新数组并在每个范围内加-1。要更新的索引 I 是段树中的一部分
    4.  **情况 4:如果 y 不是阿姆斯特朗数，而 x 是阿姆斯特朗数**
        子阵中阿姆斯特朗数的计数增加，所以我们更新数组，每个范围加 1。要更新的索引 I 是段树中的一部分

下面是上述方法的实现:

## C++

```
// C++ program to find the number
// of Armstrong numbers in a
// subarray and performing updates

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

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

// A utility function to get the middle
// index from corner indexes.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Recursive function to get the number
// of Armstrong numbers in a given range
/* where
    st    --> Pointer to segment tree
    index --> Index of current node in the
              segment tree. Initially 0 is passed
              as root is always at index 0
    ss & se  --> Starting and ending indexes of
              the segment represented by current
              node, i.e., st[index]
    qs & qe  --> Starting and ending indexes
              of query range  
    */
int queryArmstrongUtil(int* st, int ss,
                       int se, int qs,
                       int qe, int index)
{
    // If segment of this node is a part
    // of given range, then return
    // the number of Armstrong numbers
    // in the segment
    if (qs <= ss && qe >= se)
        return st[index];

    // If segment of this node
    // is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return queryArmstrongUtil(
               st, ss, mid, qs,
               qe, 2 * index + 1)
           + queryArmstrongUtil(
                 st, mid + 1, se,
                 qs, qe, 2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range.
/* where
    st, si, ss and se are same as getSumUtil()
    i --> index of the element to be updated.
          This index is in input array.
   diff --> Value to be added to all nodes
          which have i in range
*/
void updateValueUtil(int* st, int ss,
                     int se, int i,
                     int diff, int si)
{
    // Base Case:
    // If the input index lies outside
    // the range of this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range
    // of this node, then update the value
    // of the node and its children
    st[si] = st[si] + diff;
    if (se != ss) {

        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i,
                        diff, 2 * si + 1);
        updateValueUtil(st, mid + 1, se,
                        i, diff, 2 * si + 2);
    }
}

// Function to update a value in the
// input array and segment tree.
// It uses updateValueUtil() to update
// the value in segment tree
void updateValue(int arr[], int* st,
                 int n, int i,
                 int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n - 1) {
        printf("Invalid Input");
        return;
    }

    int diff, oldValue;

    oldValue = arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Case 1: Old and new values
    // both are Armstrong numbers
    if (isArmstrong(oldValue)
        && isArmstrong(new_val))
        return;

    // Case 2: Old and new values
    // both not Armstrong numbers
    if (!isArmstrong(oldValue)
        && !isArmstrong(new_val))
        return;

    // Case 3: Old value was Armstrong,
    // new value is non Armstrong
    if (isArmstrong(oldValue) && !isArmstrong(new_val)) {
        diff = -1;
    }

    // Case 4: Old value was non Armstrong,
    // new_val is Armstrong
    if (!isArmstrong(oldValue)
        && !isArmstrong(new_val)) {
        diff = 1;
    }

    // Update the values of
    // nodes in segment tree
    updateValueUtil(
        st, 0, n - 1,
        i, diff, 0);
}

// Return number of Armstrong numbers
// in range from index qs (query start)
// to qe (query end).
// It mainly uses queryArmstrongUtil()
void queryArmstrong(int* st, int n,
                    int qs, int qe)
{
    int ArmstrongInRange
        = queryArmstrongUtil(st, 0, n - 1,
                             qs, qe, 0);

    cout << "Number of Armstrong numbers "
         << "in subarray from "
         << qs << " to "
         << qe << " = "
         << ArmstrongInRange << "\n";
}

// Recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node
// in segment tree st
int constructSTUtil(int arr[], int ss,
                    int se, int* st,
                    int si)
{
    // If there is one element in array,
    // check if it is Armstrong number
    // then store 1 in the segment tree
    // else store 0 and return
    if (ss == se) {

        // if arr[ss] is Armstrong number
        if (isArmstrong(arr[ss]))
            st[si] = 1;
        else
            st[si] = 0;

        return st[si];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the
    // two values in this node
    int mid = getMid(ss, se);
    st[si] = constructSTUtil(
                 arr, ss, mid, st,
                 si * 2 + 1)
             + constructSTUtil(
                   arr, mid + 1, se, st,
                   si * 2 + 2);
    return st[si];
}

// Function to construct a segment
// tree from given array.
// This function allocates memory
// for segment tree and
// calls constructSTUtil() to
// fill the allocated memory
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

// Driver Code
int main()
{

    int arr[] = { 18, 153, 8, 9, 14, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    int* st = constructST(arr, n);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    queryArmstrong(st, n, start, end);

    // Query 2: Update(i = 3, x = 11),
    // i.e Update a[i] to x
    int i = 3;
    int x = 11;
    updateValue(arr, st, n, i, x);

    // Print array after update
    cout << "Array after update: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << ", ";
    cout << endl;

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryArmstrong(st, n, start, end);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find the number
# of Armstrong numbers in a
# subarray and performing updates
import math

MAX = 1000

# Function that return true
# if num is armstrong
# else return false
def isArmstrong(x):

    n = len(str(x))
    sum1 = 0
    temp = x

    while temp > 0:
        digit = temp % 10
        sum1 += pow(digit, n)
        temp = temp // 10

    if sum1 == x:
        return True
    return False

# A utility function to get the middle
# index from corner indexes.
def getMid(s, e):

    return s + (e - s) // 2

# Recursive function to get the number
# of Armstrong numbers in a given range
# where
# st --> Pointer to segment tree
# index --> Index of current node in the
#             segment tree. Initially 0 is passed
#             as root is always at index 0
# ss & se --> Starting and ending indexes of
#             the segment represented by current
#             node, i.e., st[index]
# qs & qe --> Starting and ending indexes
#             of query range
def queryArmstrongUtil(st, ss, se, qs, qe, index):

    # If segment of this node is a part
    # of given range, then return
    # the number of Armstrong numbers
    # in the segment
    if qs <= ss and qe >= se:
        return st[index]

    # If segment of this node
    # is outside the given range
    if se < qs or ss > qe:
        return 0

    # If a part of this segment
    # overlaps with the given range
    mid = getMid(ss, se)

    return (queryArmstrongUtil(st, ss, mid, qs,
                               qe, 2 * index + 1) +
            queryArmstrongUtil(st, mid + 1, se, qs,
                               qe, 2 * index + 2))

# Recursive function to update
# the nodes which have the given
# index in their range.
# where
# st, si, ss and se are same as getSumUtil()
# i --> index of the element to be updated.
#         This index is in input array.
# diff --> Value to be added to all nodes
#         which have i in range
def updateValueUtil(st, ss, se, i, diff, si):

    # Base Case:
    # If the input index lies outside
    # the range of this segment
    if i < ss or i > se:
        return

    # If the input index is in range
    # of this node, then update the value
    # of the node and its children
    st[si] = st[si] + diff
    if se != ss:
        mid = getMid(ss, se)
        updateValueUtil(st, ss, mid, i,
                        diff, 2 * si + 1)
        updateValueUtil(st, mid + 1, se, i,
                        diff, 2 * si + 2)

# Function to update a value in the
# input array and segment tree.
# It uses updateValueUtil() to update
# the value in segment tree
def updateValue(arr, st, n, i, new_val):

    # Check for erroneous input index
    if i < 0 or i > n - 1:
        print('Invalid Input')
        return

    oldValue = arr[i]

    # Update the value in array
    arr[i] = new_val

    # Case 1: Old and new values
    # both are Armstrong numbers
    if (isArmstrong(oldValue) and
        isArmstrong(new_val)):
        return

    # Case 2: Old and new values
    # both not Armstrong numbers
    if (not isArmstrong(oldValue) and
        not isArmstrong(new_val)):
        return

    # Case 3: Old value was Armstrong,
    # new value is non Armstrong
    if (isArmstrong(oldValue) and (not
        isArmstrong(new_val))):
        diff = -1

    # Case 4: Old value was non Armstrong,
    # new_val is Armstrong
    if (not isArmstrong(oldValue) and
        not isArmstrong(new_val)):
        diff = 1

    # Update the values of
    # nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0)

# Return number of Armstrong numbers
# in range from index qs (query start)
# to qe (query end).
# It mainly uses queryArmstrongUtil()
def queryArmstrong(st, n, qs, qe):

    ArmstrongInRange = queryArmstrongUtil(st, 0, n - 1,
                                          qs, qe, 0)
    print("Number of Armstrong numbers in "
          "subarray from", qs, "to", qe, "=",
           ArmstrongInRange)

# Recursive function that constructs
# Segment Tree for array[ss..se].
# si is index of current node
# in segment tree st
def constructSTUtil(arr, ss, se, st, si):

    # If there is one element in array,
    # check if it is Armstrong number
    # then store 1 in the segment tree
    # else store 0 and return
    if ss == se:

        # If arr[ss] is Armstrong number
        if isArmstrong(arr[ss]):
            st[si] = 1
        else:
            st[si] = 0

        return st[si]

    # If there are more than one elements,
    # then recur for left and right subtrees
    # and store the sum of the
    # two values in this node
    mid = getMid(ss, se)
    st[si] = (constructSTUtil(arr, ss, mid,
                              st, si * 2 + 1) +
              constructSTUtil(arr, mid + 1, se,
                              st, si * 2 + 2))

    return st[si]

# Function to construct a segment
# tree from given array.
# This function allocates memory
# for segment tree and
# calls constructSTUtil() to
# fill the allocated memory
def constructST(arr, n):

    # Allocate memory for segment tree

    # Height of segment tree
    x = int(math.ceil(math.log2(n)))

    # Maximum size of segment tree
    max_size = 2 * int(pow(2, x)) - 1

    st = [-1] * max_size

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0)

    # Return the constructed segment tree
    return st

# Driver code
arr = [ 18, 153, 8, 9, 14, 5 ]
n = len(arr)

# Build segment tree from given array
st = constructST(arr, n)

# Query 1: Query(start = 0, end = 4)
start = 0
end = 4
queryArmstrong(st, n, start, end)

# Query 2: Update(i = 3, x = 11),
# i.e Update a[i] to x
i = 3
x = 11
updateValue(arr, st, n, i, x)

# Print array after update
print("Array after update:", end = " ")
for i in range(n):
    print(arr[i], end = ", ")

print()

# Query 3: Query(start = 0, end = 4)
start = 0
end = 4
queryArmstrong(st, n, start, end)

# This code is contributed by stutipathak31jan
```

## C#

```
// C# program to find the number
// of Armstrong numbers in a
// subarray and performing updates
using System;

class GFG{

public int MAX = 1000;

// Function that return true
// if num is armstrong
// else return false
static bool isArmstrong(int x)
{
    int n = x.ToString().Length;
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

// A utility function to get the middle
// index from corner indexes.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Recursive function to get the number
// of Armstrong numbers in a given range
/* where
    st    --> Pointer to segment tree
    index --> Index of current node in the
              segment tree. Initially 0 is passed
              as root is always at index 0
    ss & se  --> Starting and ending indexes of
              the segment represented by current
              node, i.e., st[index]
    qs & qe  --> Starting and ending indexes
              of query range
    */
static int queryArmstrongUtil(int[] st, int ss, int se,
                              int qs, int qe, int index)
{

    // If segment of this node is a part
    // of given range, then return
    // the number of Armstrong numbers
    // in the segment
    if (qs <= ss && qe >= se)
        return st[index];

    // If segment of this node
    // is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return queryArmstrongUtil(st, ss, mid, qs, qe,
                              2 * index + 1) +
           queryArmstrongUtil(st, mid + 1, se, qs, qe,
                              2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range.
/* where
    st, si, ss and se are same as getSumUtil()
    i --> index of the element to be updated.
          This index is in input array.
   diff --> Value to be added to all nodes
          which have i in range
*/
static void updateValueUtil(int[] st, int ss, int se,
                            int i, int diff, int si)
{

    // Base Case:
    // If the input index lies outside
    // the range of this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range
    // of this node, then update the value
    // of the node and its children
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

// Function to update a value in the
// input array and segment tree.
// It uses updateValueUtil() to update
// the value in segment tree
static void updateValue(int[] arr, int[] st, int n,
                        int i, int new_val)
{

    // Check for erroneous input index
    if (i < 0 || i > n - 1)
    {
        Console.Write("Invalid Input");
        return;
    }

    int diff = 0, oldValue = 0;

    oldValue = arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Case 1: Old and new values
    // both are Armstrong numbers
    if (isArmstrong(oldValue) &&
        isArmstrong(new_val))
        return;

    // Case 2: Old and new values
    // both not Armstrong numbers
    if (!isArmstrong(oldValue) &&
        !isArmstrong(new_val))
        return;

    // Case 3: Old value was Armstrong,
    // new value is non Armstrong
    if (isArmstrong(oldValue) &&
        !isArmstrong(new_val))
    {
        diff = -1;
    }

    // Case 4: Old value was non Armstrong,
    // new_val is Armstrong
    if (!isArmstrong(oldValue) &&
        !isArmstrong(new_val))
    {
        diff = 1;
    }

    // Update the values of
    // nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0);
}

// Return number of Armstrong numbers
// in range from index qs (query start)
// to qe (query end).
// It mainly uses queryArmstrongUtil()
static void queryArmstrong(int[] st, int n, int qs,
                           int qe)
{
    int ArmstrongInRange = queryArmstrongUtil(
        st, 0, n - 1, qs, qe, 0);

    Console.WriteLine("Number of Armstrong numbers " +
                      "in subarray from " + qs + " to " +
                      qe + " = " + ArmstrongInRange);
}

// Recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node
// in segment tree st
static int constructSTUtil(int[] arr, int ss, int se,
                           int[] st, int si)
{

    // If there is one element in array,
    // check if it is Armstrong number
    // then store 1 in the segment tree
    // else store 0 and return
    if (ss == se)
    {

        // If arr[ss] is Armstrong number
        if (isArmstrong(arr[ss]))
            st[si] = 1;
        else
            st[si] = 0;

        return st[si];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the
    // two values in this node
    int mid = getMid(ss, se);
    st[si] = constructSTUtil(arr, ss, mid,
                             st, si * 2 + 1) +
             constructSTUtil(arr, mid + 1, se,
                             st, si * 2 + 2);
    return st[si];
}

// Function to construct a segment
// tree from given array.
// This function allocates memory
// for segment tree and
// calls constructSTUtil() to
// fill the allocated memory
static int[] constructST(int[] arr, int n)
{

    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(Math.Ceiling(Math.Log(n, 2)));

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
    int[] arr = { 18, 153, 8, 9, 14, 5 };
    int n = arr.Length;

    // Build segment tree from given array
    int[] st = constructST(arr, n);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    queryArmstrong(st, n, start, end);

    // Query 2: Update(i = 3, x = 11),
    // i.e Update a[i] to x
    int i = 3;
    int x = 11;
    updateValue(arr, st, n, i, x);

    // Print array after update
    Console.Write("Array after update: ");
    for(int j = 0; j < n; j++)
        Console.Write(arr[j] + ", ");

    Console.WriteLine();

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryArmstrong(st, n, start, end);
}
}

// This code is contributed by ukasp
```

**Output:** 

```
Number of Armstrong numbers in subarray from 0 to 4 = 3
Array after update: 18, 153, 8, 11, 14, 5, 
Number of Armstrong numbers in subarray from 0 to 4 = 2
```

**时间复杂度:**每次查询更新的时间复杂度为 **O(log N)** ，构建段树的时间复杂度为 **O(N)**