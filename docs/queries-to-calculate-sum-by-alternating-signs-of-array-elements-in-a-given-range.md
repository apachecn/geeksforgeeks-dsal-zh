# 通过给定范围内数组元素的交替符号计算总和的查询

> 原文:[https://www . geeksforgeeks . org/通过给定范围内的数组元素交替符号计算总和的查询/](https://www.geeksforgeeks.org/queries-to-calculate-sum-by-alternating-signs-of-array-elements-in-a-given-range/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个由以下两种类型的查询组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** :

*   **1x val:**update**arr【x]= val**。
*   **2 L R:** 求在**【L，R】**范围内有交替符号的数组元素的[和。](https://www.geeksforgeeks.org/sum-of-first-n-natural-numbers-with-alternate-signs)

**示例:**

> **输入:** arr[] = { 1，2，3，4 }，Q[][] = { { 2，0，3 }，{ 1，1，5 }，{ 2，1，2 } }
> **输出:**-2 2
> T6】解释:T8】查询 1:打印(arr[0]–arr[1]+arr[2]–arr[3])= 1–2+3–4 =-2
> 查询 2:将 arr[1]更新为 5
> 
> **输入:** arr[] = { 4，2，6，1，8，9，2}，Q = { { 2，1，4 }，{ 1，3，4 }，{ 2，0，3 } }
> **输出:** -11 5

**方法:**使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)可以解决问题。想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查数组元素的索引是否为负，然后将数组元素乘以 **-1** 。按照以下步骤解决问题:

*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，检查索引 **i** 是否为奇数。如果发现为真，则更新 **arr[i] = -Val** 。
*   对于类型 **1，X，Val** 的查询，检查 **X** 是否为偶数。如果发现为真，则使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)更新 **arr[X] = Val** 。
*   否则，使用线段树更新 **arr[X] = -Val** 。
*   对于 **2 L R:** 类型的查询，检查 **L** 是否为偶数。如果发现为真，则使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)打印范围**【L，R】**内的数组元素之和。
*   否则，用线段树求出**【L，R】**范围内的数组元素的[之和，并将所得之和乘以 **-1** 打印出来。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++  program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to build the segment tree
void build(int tree[], int arr[], int start,
           int end, int index)
{

    // If current node is a leaf node
    // of the segment tree
    if (start == end) {

        if (start % 2 == 0) {

            // Update tree[index]
            tree[index] = arr[start];
        }

        else {

            // Update tree[index]
            tree[index] = -arr[start];
        }
        return;
    }

    // Divide the segment tree
    int mid = start + (end - start) / 2;

    // Update on L segment tree
    build(tree, arr, start, mid,
          2 * index + 1);

    // Update on R segment tree
    build(tree, arr, mid + 1, end,
          2 * index + 2);

    // Find the sum from L subtree
    // and R subtree
    tree[index] = tree[2 * index + 1] + tree[2 * index + 2];
}

// Function to update elements at index pos
// by val in the segment tree
void update(int tree[], int index, int start,
            int end, int pos, int val)
{

    // If current node is a leaf node
    if (start == end) {

        // If current index is even
        if (start % 2 == 0) {

            // Update tree[index]
            tree[index] = val;
        }

        else {

            // Update tree[index]
            tree[index] = -val;
        }
        return;
    }

    // Divide the segment tree elements
    // into L and R subtree
    int mid = start + (end - start) / 2;

    // If element lies in L subtree
    if (mid >= pos) {

        update(tree, 2 * index + 1, start,
               mid, pos, val);
    }
    else {
        update(tree, 2 * index + 2, mid + 1,
               end, pos, val);
    }

    // Update tree[index]
    tree[index]
        = tree[2 * index + 1] + tree[2 * index + 2];
}

// Function to find the sum of array elements
// in the range [L, R]
int FindSum(int tree[], int start, int end,
            int L, int R, int index)
{

    // If start and end not lies in
    // the range [L, R]
    if (L > end || R < start) {
        return 0;
    }

    // If start and end comleately lies
    // in the range [L, R]
    if (L <= start && R >= end) {

        return tree[index];
    }
    int mid = start + (end - start) / 2;

    // Stores sum from left subtree
    int X = FindSum(tree, start, mid, L,
                    R, 2 * index + 1);

    // Stores sum from right subtree
    int Y = FindSum(tree, mid + 1, end, L,
                    R, 2 * index + 2);

    return X + Y;
}

int main()
{

    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int tree[4 * N + 5] = { 0 };
    build(tree, arr, 0, N - 1, 0);

    int Q[][3] = { { 2, 0, 3 }, { 1, 1, 5 }, { 2, 1, 2 } };

    int cntQuey = 3;
    for (int i = 0; i < cntQuey; i++) {

        if (Q[i][0] == 1) {

            update(tree, 0, 0, N - 1,
                   Q[i][1], Q[i][2]);
        }

        else {

            if (Q[i][1] % 2 == 0) {

                cout << FindSum(tree, 0, N - 1,
                                Q[i][1], Q[i][2], 0)
                     << " ";
            }
            else {

                cout << -FindSum(tree, 0, N - 1,
                                 Q[i][1], Q[i][2], 0)
                     << " ";
            }
        }
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to build the segment tree
static void build(int tree[], int arr[], int start,
           int end, int index)
{

    // If current node is a leaf node
    // of the segment tree
    if (start == end) {

        if (start % 2 == 0) {

            // Update tree[index]
            tree[index] = arr[start];
        }

        else {

            // Update tree[index]
            tree[index] = -arr[start];
        }
        return;
    }

    // Divide the segment tree
    int mid = start + (end - start) / 2;

    // Update on L segment tree
    build(tree, arr, start, mid,
          2 * index + 1);

    // Update on R segment tree
    build(tree, arr, mid + 1, end,
          2 * index + 2);

    // Find the sum from L subtree
    // and R subtree
    tree[index] = tree[2 * index + 1] + tree[2 * index + 2];
}

// Function to update elements at index pos
// by val in the segment tree
static void update(int tree[], int index, int start,
            int end, int pos, int val)
{

    // If current node is a leaf node
    if (start == end) {

        // If current index is even
        if (start % 2 == 0) {

            // Update tree[index]
            tree[index] = val;
        }

        else {

            // Update tree[index]
            tree[index] = -val;
        }
        return;
    }

    // Divide the segment tree elements
    // into L and R subtree
    int mid = start + (end - start) / 2;

    // If element lies in L subtree
    if (mid >= pos)
    {
        update(tree, 2 * index + 1, start,
               mid, pos, val);
    }
    else
    {
        update(tree, 2 * index + 2, mid + 1,
               end, pos, val);
    }

    // Update tree[index]
    tree[index]
        = tree[2 * index + 1] + tree[2 * index + 2];
}

// Function to find the sum of array elements
// in the range [L, R]
static int FindSum(int tree[], int start, int end,
            int L, int R, int index)
{

    // If start and end not lies in
    // the range [L, R]
    if (L > end || R < start)
    {
        return 0;
    }

    // If start and end comleately lies
    // in the range [L, R]
    if (L <= start && R >= end)
    {
        return tree[index];
    }
    int mid = start + (end - start) / 2;

    // Stores sum from left subtree
    int X = FindSum(tree, start, mid, L,
                    R, 2 * index + 1);

    // Stores sum from right subtree
    int Y = FindSum(tree, mid + 1, end, L,
                    R, 2 * index + 2);
    return X + Y;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;
    int tree[] = new int[4 * N + 5];
    Arrays.fill(tree, 0);
    build(tree, arr, 0, N - 1, 0);
    int Q[][] = { { 2, 0, 3 }, { 1, 1, 5 }, { 2, 1, 2 } };
    int cntQuey = 3;
    for (int i = 0; i < cntQuey; i++)
    {
        if (Q[i][0] == 1)
        {
            update(tree, 0, 0, N - 1,
                   Q[i][1], Q[i][2]);
        }
        else {
            if (Q[i][1] % 2 == 0)
            {
                System.out.print(FindSum(tree, 0, N - 1,
                                Q[i][1], Q[i][2], 0) + " ");
            }
            else
            {
                System.out.print(-FindSum(tree, 0, N - 1,
                                 Q[i][1], Q[i][2], 0)+ " ");
            }
        }
    }
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3  program to implement
# the above approach

# Function to build the segment tree
def build(tree, arr, start, end, index):

    # If current node is a leaf node
    # of the segment tree
    if (start == end):
        if (start % 2 == 0):

            # Update tree[index]
            tree[index] = arr[start]
        else:

            # Update tree[index]
            tree[index] = -arr[start]
        return

    # Divide the segment tree
    mid = start + (end - start) // 2

    # Update on L segment tree
    build(tree, arr, start, mid, 2 * index + 1)

    # Update on R segment tree
    build(tree, arr, mid + 1, end, 2 * index + 2)

    # Find the sum from L subtree
    # and R subtree
    tree[index] = tree[2 * index + 1] + tree[2 * index + 2]

# Function to update elements at index pos
# by val in the segment tree
def update(tree, index, start, end, pos, val):

    # If current node is a leaf node
    if (start == end):

        # If current index is even
        if (start % 2 == 0):

            # Update tree[index]
            tree[index] = val
        else:

            # Update tree[index]
            tree[index] = -val
        return

    # Divide the segment tree elements
    # into L and R subtree
    mid = start + (end - start) // 2

    # If element lies in L subtree
    if (mid >= pos):
        update(tree, 2 * index + 1, start, mid, pos, val)
    else:
        update(tree, 2 * index + 2, mid + 1, end, pos, val)

    # Update tree[index]
    tree[index] = tree[2 * index + 1] + tree[2 * index + 2]

# Function to find the sum of array elements
# in the range [L, R]
def FindSum(tree, start, end, L, R, index):

    # If start and end not lies in
    # the range [L, R]
    if (L > end or R < start):
        return 0

    #If start and end comleately lies
    #in the range [L, R]
    if (L <= start and R >= end):
        return tree[index]
    mid = start + (end - start) // 2

    # Stores sum from left subtree
    X = FindSum(tree, start, mid, L, R, 2 * index + 1)

    # Stores sum from right subtree
    Y = FindSum(tree, mid + 1, end, L, R, 2 * index + 2)

    return X + Y

  # Driver code
if __name__ == '__main__':

    arr = [1, 2, 3, 4]
    N = len(arr)
    tree = [0 for i in range(4 * N + 5)]
    build(tree, arr, 0, N - 1, 0)
    Q = [ [ 2, 0, 3 ], [ 1, 1, 5 ], [ 2, 1, 2 ] ]
    cntQuey = 3
    for i in range(cntQuey):
        if (Q[i][0] == 1):
            update(tree, 0, 0, N - 1, Q[i][1], Q[i][2])
        else:
            if (Q[i][1] % 2 == 0):
                print(FindSum(tree, 0, N - 1, Q[i][1], Q[i][2], 0),end=" ")
            else:
                print(-FindSum(tree, 0, N - 1, Q[i][1], Q[i][2], 0),end=" ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C#  program to implement
// the above approach
using System;
class GFG
{

    // Function to build the segment tree
    static void build(int[] tree, int[] arr, int start,
               int end, int index)
    {

        // If current node is a leaf node
        // of the segment tree
        if (start == end)
        {  
            if (start % 2 == 0)
            {

                // Update tree[index]
                tree[index] = arr[start];
            }

            else
            {

                // Update tree[index]
                tree[index] = -arr[start];
            }
            return;
        }

        // Divide the segment tree
        int mid = start + (end - start) / 2;

        // Update on L segment tree
        build(tree, arr, start, mid,
              2 * index + 1);

        // Update on R segment tree
        build(tree, arr, mid + 1, end,
              2 * index + 2);

        // Find the sum from L subtree
        // and R subtree
        tree[index] = tree[2 * index + 1] + tree[2 * index + 2];
    }

    // Function to update elements at index pos
    // by val in the segment tree
    static void update(int[] tree, int index, int start,
                int end, int pos, int val)
    {

        // If current node is a leaf node
        if (start == end)
        {

            // If current index is even
            if (start % 2 == 0)
            {

                // Update tree[index]
                tree[index] = val;
            }

            else
            {

                // Update tree[index]
                tree[index] = -val;
            }
            return;
        }

        // Divide the segment tree elements
        // into L and R subtree
        int mid = start + (end - start) / 2;

        // If element lies in L subtree
        if (mid >= pos)
        {

            update(tree, 2 * index + 1, start,
                   mid, pos, val);
        }
        else
        {
            update(tree, 2 * index + 2, mid + 1,
                   end, pos, val);
        }

        // Update tree[index]
        tree[index]
            = tree[2 * index + 1] + tree[2 * index + 2];
    }

    // Function to find the sum of array elements
    // in the range [L, R]
    static int FindSum(int[] tree, int start, int end,
                int L, int R, int index)
    {

        // If start and end not lies in
        // the range [L, R]
        if (L > end || R < start)
        {
            return 0;
        }

        // If start and end comleately lies
        // in the range [L, R]
        if (L <= start && R >= end)
        {

            return tree[index];
        }
        int mid = start + (end - start) / 2;

        // Stores sum from left subtree
        int X = FindSum(tree, start, mid, L,
                        R, 2 * index + 1);

        // Stores sum from right subtree
        int Y = FindSum(tree, mid + 1, end, L,
                        R, 2 * index + 2);

        return X + Y;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 2, 3, 4 };
    int N = arr.Length;
    int[] tree = new int[4 * N + 5];
    build(tree, arr, 0, N - 1, 0);

    int[,] Q = { { 2, 0, 3 }, { 1, 1, 5 }, { 2, 1, 2 } };

    int cntQuey = 3;
    for (int i = 0; i < cntQuey; i++)
    {
        if (Q[i, 0] == 1)
        {
            update(tree, 0, 0, N - 1,
                   Q[i, 1], Q[i, 2]);
        }

        else
        {
            if (Q[i, 1] % 2 == 0)
            {
                Console.Write(FindSum(tree, 0, N - 1,
                                      Q[i, 1], Q[i, 2], 0) + " ");
            }
            else
            {
                Console.Write(-FindSum(tree, 0, N - 1,
                                       Q[i, 1], Q[i, 2], 0) + " ");
            }
        }
    }
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript  program to implement
// the above approach

// Function to build the segment tree
function build(tree, arr, start, end, index)
{

    // If current node is a leaf node
    // of the segment tree
    if (start == end) {

        if (start % 2 == 0) {

            // Update tree[index]
            tree[index] = arr[start];
        }

        else {

            // Update tree[index]
            tree[index] = -arr[start];
        }
        return;
    }

    // Divide the segment tree
    var mid = start + parseInt((end - start) / 2);

    // Update on L segment tree
    build(tree, arr, start, mid,
          2 * index + 1);

    // Update on R segment tree
    build(tree, arr, mid + 1, end,
          2 * index + 2);

    // Find the sum from L subtree
    // and R subtree
    tree[index] = tree[2 * index + 1] + tree[2 * index + 2];
}

// Function to update elements at index pos
// by val in the segment tree
function update(tree, index, start, end, pos, val)
{

    // If current node is a leaf node
    if (start == end) {

        // If current index is even
        if (start % 2 == 0) {

            // Update tree[index]
            tree[index] = val;
        }

        else {

            // Update tree[index]
            tree[index] = -val;
        }
        return;
    }

    // Divide the segment tree elements
    // into L and R subtree
    var mid = start + parseInt((end - start) / 2);

    // If element lies in L subtree
    if (mid >= pos) {

        update(tree, 2 * index + 1, start,
               mid, pos, val);
    }
    else {
        update(tree, 2 * index + 2, mid + 1,
               end, pos, val);
    }

    // Update tree[index]
    tree[index]
        = tree[2 * index + 1] + tree[2 * index + 2];
}

// Function to find the sum of array elements
// in the range [L, R]
function FindSum(tree, start, end, L, R, index)
{

    // If start and end not lies in
    // the range [L, R]
    if (L > end || R < start) {
        return 0;
    }

    // If start and end comleately lies
    // in the range [L, R]
    if (L <= start && R >= end) {

        return tree[index];
    }
    var mid = start + parseInt((end - start) / 2);

    // Stores sum from left subtree
    var X = FindSum(tree, start, mid, L,
                    R, 2 * index + 1);

    // Stores sum from right subtree
    var Y = FindSum(tree, mid + 1, end, L,
                    R, 2 * index + 2);

    return X + Y;
}

var arr = [1, 2, 3, 4 ];
var N = arr.length;
var tree = Array(4*N+5).fill(0);
build(tree, arr, 0, N - 1, 0);
var Q = [ [ 2, 0, 3 ], [ 1, 1, 5 ], [ 2, 1, 2 ] ];
var cntQuey = 3;
for (var i = 0; i < cntQuey; i++) {
    if (Q[i][0] == 1) {
        update(tree, 0, 0, N - 1,
               Q[i][1], Q[i][2]);
    }
    else {
        if (Q[i][1] % 2 == 0) {
            document.write(FindSum(tree, 0, N - 1,
                            Q[i][1], Q[i][2], 0)
                 + " ");
        }
        else {
            document.write( -FindSum(tree, 0, N - 1,
                             Q[i][1], Q[i][2], 0)
                 + " ");
        }
    }
}

</script>
```

**Output:** 

```
-2 2
```

***时间复杂度:**O(| Q | * log(N))*
***辅助空间:** O(N)*