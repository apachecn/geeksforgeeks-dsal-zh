# 给定范围内元素的异或运算，使用芬威克树进行更新

> 原文:[https://www . geeksforgeeks . org/给定范围内元素的 xor-with-updates-use-fenwick-tree/](https://www.geeksforgeeks.org/xor-of-elements-in-a-given-range-with-updates-using-fenwick-tree/)

给定整数数组**和由以下两种类型的查询组成的数组 **Q** :**

*   **(1，L，R)** :返回指数 **L** 和 **R** 之间存在的所有元素的异或。
*   **(2，I，val)** :将**A【I】**更新为**A【I】XOR val**。

任务是使用[分支树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)求解每个查询并打印第一类每个查询的异或。
**例:**

> **输入:** A[] = {2，1，1，3，2，3，4，5，6，7，8，9}
> Q = {{ 1，3，8}，{2，4，6}，{ 1，3，8}}
> **输出:**
> 3 到 8 范围内的元素异或为 5
> 3 到 8 范围内的元素异或为 3
> **说明:**
> 子阵{ 3，2，3
> 第二次查询后，arr[4]被 4 替换。
> 子阵{ 3，4，3，4，5，6 }的 Xor 为 3。
> **输入:** A[] = {2，1，1，3，2，3，4，5，6，7，8，9}
> Q = {{1，0，9}，{2，3，6}，{2，5，5}，{2，8，1}，{1，0，9}}
> **输出:**
> 0 到 9 范围内元素的异或为 0
> 0 到 9 范围内元素的异或为 0

**进场:**

*   对于类型 1 的查询，使用 getXor()返回范围**【1，R】**和范围**【1，L-1】**中元素的 Xor。
*   在 getXor()中，对于 **i** 从**索引**开始到其所有祖先直到 1，继续计算 **XOR** 和**bit REE【I】**。为了在 **getXor()** 视图中得到第 I 个索引的祖先，我们只需要通过**I = I–I&(-I)**从 I 中减去 LSB(最低有效位)。最后返回最终的异或值。
*   对于类型 2 的查询，将[索引]更新为**a[索引] ^值**。通过调用 **updateBIT()** ，更新 BITree[]中包含此元素的所有范围。
*   在 updateBIT()中，对于从**索引**开始直到 **N** 的每个 **i** ,将 BITree[i]更新为 BITree[i] ^ **val** 。为了在 **updateBit()** 视图中得到第 I 个索引的祖先，我们只需要通过 **i = i + i & (-i)** 从 I 中添加 LSB(最低有效位)。

下面是上述方法的实现:

## C++

```
// C++ Program to find XOR of
// elements in given range [L, R].

#include <bits/stdc++.h>
using namespace std;

// Returns XOR of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// XORs of array elements are stored
// in BITree[].
int getXOR(int BITree[], int index)
{
    int ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0) {

        // XOR current element
        // of BIT to ans
        ans ^= BITree[index];

        // Update index to that
        // of the parent node in
        // getXor() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Updates the Binary Index Tree by
// replacing all ancestors of index
// by their respective XOR with val
void updateBIT(int BITree[], int n,
               int index, int val)
{
    index = index + 1;

    // Traverse all ancestors
    // and XOR with 'val'.
    while (index <= n) {

        // XOR 'val' to current
        // node of BIT
        BITree[index] ^= val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Constructs and returns a Binary
// Indexed Tree for the given array
int* constructBITree(int arr[], int n)
{
    // Create and initialize
    // the Binary Indexed Tree
    int* BITree = new int[n + 1];
    for (int i = 1; i <= n; i++)
        BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for (int i = 0; i < n; i++)
        updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

int rangeXor(int BITree[], int l, int r)
{
    return getXOR(BITree, r)
           ^ getXOR(BITree, l - 1);
}

// Driver Code
int main()
{
    int A[] = { 2, 1, 1, 3, 2, 3,
                4, 5, 6, 7, 8, 9 };
    int n = sizeof(A) / sizeof(A[0]);

    vector<vector<int> > q
        = { { 1, 0, 9 },
            { 2, 3, 6 },
            { 2, 5, 5 },
            { 2, 8, 1 },
            { 1, 0, 9 } };

    // Create the Binary Indexed Tree
    int* BITree = constructBITree(A, n);

    // Solve each query in Q
    for (int i = 0; i < q.size(); i++) {
        int id = q[i][0];

        if (id == 1) {
            int L = q[i][1];
            int R = q[i][2];
            cout << "XOR of elements "
                 << "in given range is "
                 << rangeXor(BITree, L, R)
                 << "\n";
        }
        else {
            int idx = q[i][1];
            int val = q[i][2];
            A[idx] ^= val;

            // Update the values of all
            // ancestors of idx
            updateBIT(BITree, n, idx, val);
        }
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find XOR of
// elements in given range [L, R].
import java.util.*;

class GFG{

// Returns XOR of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// XORs of array elements are stored
// in BITree[].
static int getXOR(int BITree[], int index)
{
    int ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0)
    {

        // XOR current element
        // of BIT to ans
        ans ^= BITree[index];

        // Update index to that
        // of the parent node in
        // getXor() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Updates the Binary Index Tree by
// replacing all ancestors of index
// by their respective XOR with val
static void updateBIT(int BITree[], int n,
                      int index, int val)
{
    index = index + 1;

    // Traverse all ancestors
    // and XOR with 'val'.
    while (index <= n)
    {

        // XOR 'val' to current
        // node of BIT
        BITree[index] ^= val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Constructs and returns a Binary
// Indexed Tree for the given array
static int[] constructBITree(int arr[], int n)
{
    // Create and initialize
    // the Binary Indexed Tree
    int []BITree = new int[n + 1];
    for (int i = 1; i <= n; i++)
        BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for (int i = 0; i < n; i++)
        updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

static int rangeXor(int BITree[], int l, int r)
{
    return getXOR(BITree, r) ^
           getXOR(BITree, l - 1);
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 1, 1, 3, 2, 3,
                4, 5, 6, 7, 8, 9 };
    int n = A.length;

    int [][]q = { { 1, 0, 9 },
                  { 2, 3, 6 },
                  { 2, 5, 5 },
                  { 2, 8, 1 },
                  { 1, 0, 9 } };

    // Create the Binary Indexed Tree
    int []BITree = constructBITree(A, n);

    // Solve each query in Q
    for (int i = 0; i < q.length; i++)
    {
        int id = q[i][0];

        if (id == 1)
        {
            int L = q[i][1];
            int R = q[i][2];
            System.out.print("XOR of elements " +
                           "in given range is " +
                         rangeXor(BITree, L, R) + "\n");
        }
        else
        {
            int idx = q[i][1];
            int val = q[i][2];
            A[idx] ^= val;

            // Update the values of all
            // ancestors of idx
            updateBIT(BITree, n, idx, val);
        }
    }
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find XOR of
# elements in given range [L, R].

# Returns XOR of arr[0..index].
# This function assumes that the
# array is preprocessed and partial
# XORs of array elements are stored
# in BITree[].
def getXOR(BITree, index):

    ans = 0
    index += 1

    # Traverse ancestors
    # of BITree[index]
    while (index > 0):

        # XOR current element
        # of BIT to ans
        ans ^= BITree[index]

        # Update index to that
        # of the parent node in
        # getXor() view by
        # subtracting LSB(Least
        # Significant Bit)
        index -= index & (-index)

    return ans

# Updates the Binary Index Tree by
# replacing all ancestors of index
# by their respective XOR with val
def updateBIT(BITree, n, index, val):

    index = index + 1

    # Traverse all ancestors
    # and XOR with 'val'.
    while (index <= n):

        # XOR 'val' to current
        # node of BIT
        BITree[index] ^= val

        # Update index to that
        # of the parent node in
        # updateBit() view by
        # adding LSB(Least
        # Significant Bit)
        index += index & (-index)

# Constructs and returns a Binary
# Indexed Tree for the given array
def constructBITree(arr, n):

    # Create and initialize
    # the Binary Indexed Tree
    BITree = [0] * (n + 1)

    # Store the actual values in
    # BITree[] using update()
    for i in range(n):
        updateBIT(BITree, n, i, arr[i])

    return BITree

def rangeXor(BITree, l, r):

    return (getXOR(BITree, r) ^
            getXOR(BITree, l - 1))

# Driver Code
if __name__ == "__main__":

    A = [ 2, 1, 1, 3, 2, 3,
          4, 5, 6, 7, 8, 9 ]
    n = len(A)

    q = [ [ 1, 0, 9 ], [ 2, 3, 6 ],
          [ 2, 5, 5 ], [ 2, 8, 1 ],
          [ 1, 0, 9 ] ]

    # Create the Binary Indexed Tree
    BITree = constructBITree(A, n)

    # Solve each query in Q
    for i in range(len(q)):
        id = q[i][0]

        if (id == 1):
            L = q[i][1]
            R = q[i][2]
            print("XOR of elements in "
                  "given range is ",
                  rangeXor(BITree, L, R))
        else:
            idx = q[i][1]
            val = q[i][2]
            A[idx] ^= val

            # Update the values of all
            # ancestors of idx
            updateBIT(BITree, n, idx, val)

# This code is contributed by jana_sayantan
```

## C#

```
// C# program to find XOR of
// elements in given range [L, R].
using System;

class GFG{

// Returns XOR of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// XORs of array elements are stored
// in BITree[].
static int getXOR(int []BITree, int index)
{
    int ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0)
    {

        // XOR current element
        // of BIT to ans
        ans ^= BITree[index];

        // Update index to that
        // of the parent node in
        // getXor() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Updates the Binary Index Tree by
// replacing all ancestors of index
// by their respective XOR with val
static void updateBIT(int []BITree, int n,
                      int index, int val)
{
    index = index + 1;

    // Traverse all ancestors
    // and XOR with 'val'.
    while (index <= n)
    {

        // XOR 'val' to current
        // node of BIT
        BITree[index] ^= val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Constructs and returns a Binary
// Indexed Tree for the given array
static int[] constructBITree(int []arr,
                             int n)
{

    // Create and initialize
    // the Binary Indexed Tree
    int []BITree = new int[n + 1];
    for(int i = 1; i <= n; i++)
       BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for(int i = 0; i < n; i++)
       updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

static int rangeXor(int []BITree, int l,
                                  int r)
{
    return getXOR(BITree, r) ^
           getXOR(BITree, l - 1);
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 1, 1, 3, 2, 3,
                4, 5, 6, 7, 8, 9 };
    int n = A.Length;

    int [,]q = { { 1, 0, 9 },
                 { 2, 3, 6 },
                 { 2, 5, 5 },
                 { 2, 8, 1 },
                 { 1, 0, 9 } };

    // Create the Binary Indexed Tree
    int []BITree = constructBITree(A, n);

    // Solve each query in Q
    for(int i = 0; i < q.GetLength(0); i++)
    {
       int id = q[i, 0];

       if (id == 1)
       {
           int L = q[i, 1];
           int R = q[i, 2];
           Console.Write("XOR of elements " +
                       "in given range is " +
                     rangeXor(BITree, L, R) + "\n");
       }
       else
       {
           int idx = q[i, 1];
           int val = q[i, 2];
           A[idx] ^= val;

           // Update the values of
           // all ancestors of idx
           updateBIT(BITree, n, idx, val);
       }
    }
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript Program to find XOR of
// elements in given range [L, R].

// Returns XOR of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// XORs of array elements are stored
// in BITree[].
function getXOR(BITree, index)
{
    let ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0) {

        // XOR current element
        // of BIT to ans
        ans ^= BITree[index];

        // Update index to that
        // of the parent node in
        // getXor() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Updates the Binary Index Tree by
// replacing all ancestors of index
// by their respective XOR with val
function updateBIT(BITree, n, index, val)
{
    index = index + 1;

    // Traverse all ancestors
    // and XOR with 'val'.
    while (index <= n) {

        // XOR 'val' to current
        // node of BIT
        BITree[index] ^= val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Constructs and returns a Binary
// Indexed Tree for the given array
function constructBITree(arr, n)
{
    // Create and initialize
    // the Binary Indexed Tree
    let BITree = new Array(n + 1);
    for (let i = 1; i <= n; i++)
        BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for (let i = 0; i < n; i++)
        updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

function rangeXor(BITree, l, r)
{
    return getXOR(BITree, r)
           ^ getXOR(BITree, l - 1);
}

// Driver Code
    let A = [ 2, 1, 1, 3, 2, 3,
                4, 5, 6, 7, 8, 9 ];
    let n = A.length;

    let q
        = [ [ 1, 0, 9 ],
            [ 2, 3, 6 ],
            [ 2, 5, 5 ],
            [ 2, 8, 1 ],
            [ 1, 0, 9 ] ];

    // Create the Binary Indexed Tree
    let BITree = constructBITree(A, n);

    // Solve each query in Q
    for (let i = 0; i < q.length; i++) {
        let id = q[i][0];

        if (id == 1) {
            let L = q[i][1];
            let R = q[i][2];
            document.write("XOR of elements "
                 + "in given range is "
                 + rangeXor(BITree, L, R)
                 + "<br>");
        }
        else {
            let idx = q[i][1];
            let val = q[i][2];
            A[idx] ^= val;

            // Update the values of all
            // ancestors of idx
            updateBIT(BITree, n, idx, val);
        }
    }

</script>
```

**Output:** 

```
XOR of elements in given range is 0
XOR of elements in given range is 2
```

**getXor()的时间复杂度:***O(log N)*
T5】updateBIT()的时间复杂度: *O(log N)*
**整体时间复杂度:** O(M * log N)，其中 M 和 N 分别是给定数组的查询数量和大小。