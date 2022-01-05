# 段树中不使用惰性传播和点查询的范围更新

> 原文:[https://www . geesforgeks . org/range-update-不使用惰性传播和分段树中的点查询/](https://www.geeksforgeeks.org/range-update-without-using-lazy-propagation-and-point-query-in-a-segment-tree/)

给定一个由**N**T6】0s 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个由以下两种类型的查询组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** :

*   **1 L R X:** 将**【L，R】**范围内的所有元素增加 **X** 。
*   **2 X:** 在数组的第 X 个 索引处打印元素。

> **输入:** arr[] = { 0，0，0，0，0 }，Q[][] = { { 1，0，2，100 }，{ 2，1 }，{ 1，2，3，200 }，{ 2，2 }，{
> 4 } }
> T4】输出: 100 300 0
> **解释:**
> 查询 1:将[0，2]范围内的所有数组元素递增 100 将 arr[]修改为
> 查询 2:打印 arr[1](=100)
> 查询 3:将范围[2，3]中的所有数组元素增加 200 会将 arr[]修改为{ 100，100，300，200，0 }。
> 查询 4:打印 arr[2](=300)
> 查询 5:打印 arr[4](=0)
> 
> **输入:** arr[] = { 0，0 }，Q[][] = { { 1，0，1，100 }，{ 2，1 } }
> **输出:** 100

**方式:**思路是利用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)的概念进行 **2** 类型的查询，利用[差异数组](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)进行 **1** 类型的查询。按照以下步骤解决问题:

*   对于类型 **{ 1，L，R，X }** 的查询，使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)更新 **arr[L] += X** 和 **arr[R + 1] -= X** 。
*   对于类型为 **{ 2，X }** 的查询，使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)找到范围**【0，X】**内数组元素的[和，并打印得到的和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to update the array elements
// at idx pos, i.e arr[pos] += X
void update(int Tree[], int idx, int s,
            int e, int pos, int X)
{
    // If current node is a
    // leaf nodes
    if (s == e) {

        // Update Tree[idx]
        Tree[idx] += X;
    }

    else {

        // Divide segment tree into left
        // and right subtree
        int m = (s + e) / 2;

        // Check if pos lies in left subtree
        if (pos <= m) {

            // Search pos in left subtree
            update(Tree, 2 * idx, s, m, pos, X);
        }
        else {

            // Search pos in right subtree
            update(Tree, 2 * idx + 1, m + 1, e,
                   pos, X);
        }

        // Update Tree[idx]
        Tree[idx]
            = Tree[2 * idx] + Tree[2 * idx + 1];
    }
}

// Function to find the sum from
// elements in the range [0, X]
int sum(int Tree[], int idx, int s,
        int e, int ql, int qr)
{
    // Check if range[ql, qr] equals
    // to range [s, e]
    if (ql == s && qr == e)
        return Tree[idx];

    if (ql > qr)
        return 0;

    // Divide segment tree into
    // left substree and
    // right substree
    int m = (s + e) / 2;

    // Return sum of elements in the range[ql, qr]
    return sum(Tree, 2 * idx, s, m, ql, min(m, qr))
           + sum(Tree, 2 * idx + 1, m + 1, e,
                 max(ql, m + 1), qr);
}

// Function to find Xth element
// in the array
void getElement(int Tree[], int X, int N)
{
    // Print element at index x
    cout << "Element at " << X << " is "
         << sum(Tree, 1, 0, N - 1, 0, X) << endl;
}

// Function to update array elements
// in the range [L, R]
void range_Update(int Tree[], int L,
                  int R, int X, int N)
{

    // Update arr[l] += X
    update(Tree, 1, 0, N - 1, L, X);

    // Update arr[R + 1] += X
    if (R + 1 < N)
        update(Tree, 1, 0, N - 1, R + 1, -X);
}

// Drivers Code
int main()
{
    // Size of array
    int N = 5;

    int Tree[4 * N + 5] = { 0 };

    int arr[] = { 0, 0 };
    vector<vector<int> >
        Q = { { 1, 0, 1, 100 }, { 2, 1 } };

    int cntQuery = Q.size();
    for (int i = 0; i < cntQuery; i++) {

        if (Q[i][0] == 1) {

            range_Update(Tree, Q[i][1],
                         Q[i][2], Q[i][3], N);
        }
        else {

            getElement(Tree, Q[i][1], N);
        }
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to update the array elements
// at idx pos, i.e arr[pos] += X
static void update(int Tree[], int idx, int s,
            int e, int pos, int X)
{

    // If current node is a
    // leaf nodes
    if (s == e)
    {

        // Update Tree[idx]
        Tree[idx] += X;
    }

    else
    {

        // Divide segment tree into left
        // and right subtree
        int m = (s + e) / 2;

        // Check if pos lies in left subtree
        if (pos <= m)
        {

            // Search pos in left subtree
            update(Tree, 2 * idx, s, m, pos, X);
        }
        else
        {

            // Search pos in right subtree
            update(Tree, 2 * idx + 1, m + 1, e,
                   pos, X);
        }

        // Update Tree[idx]
        Tree[idx]
            = Tree[2 * idx] + Tree[2 * idx + 1];
    }
}

// Function to find the sum from
// elements in the range [0, X]
static int sum(int Tree[], int idx, int s,
        int e, int ql, int qr)
{

    // Check if range[ql, qr] equals
    // to range [s, e]
    if (ql == s && qr == e)
        return Tree[idx];

    if (ql > qr)
        return 0;

    // Divide segment tree into
    // left substree and
    // right substree
    int m = (s + e) / 2;

    // Return sum of elements in the range[ql, qr]
    return sum(Tree, 2 * idx, s, m, ql, Math.min(m, qr))
           + sum(Tree, 2 * idx + 1, m + 1, e,
                 Math.max(ql, m + 1), qr);
}

// Function to find Xth element
// in the array
static void getElement(int Tree[], int X, int N)
{

    // Print element at index x
    System.out.print("Element at " +  X+ " is "
         + sum(Tree, 1, 0, N - 1, 0, X) +"\n");
}

// Function to update array elements
// in the range [L, R]
static void range_Update(int Tree[], int L,
                  int R, int X, int N)
{

    // Update arr[l] += X
    update(Tree, 1, 0, N - 1, L, X);

    // Update arr[R + 1] += X
    if (R + 1 < N)
        update(Tree, 1, 0, N - 1, R + 1, -X);
}

// Drivers Code
public static void main(String[] args)
{

    // Size of array
    int N = 5;
    int Tree[] = new int[4 * N + 5];
    int arr[] = { 0, 0 };
    int[][]
        Q = { { 1, 0, 1, 100 }, { 2, 1 } };
    int cntQuery = Q.length;
    for (int i = 0; i < cntQuery; i++)
    {
        if (Q[i][0] == 1)
        {
            range_Update(Tree, Q[i][1],
                         Q[i][2], Q[i][3], N);
        }
        else
        {
            getElement(Tree, Q[i][1], N);
        }
    }
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to update the array elements
# at idx pos, i.e arr[pos] += X
def update(Tree, idx, s, e, pos, X):

    # If current node is a
    # leaf nodes
    if (s == e):

        # Update Tree[idx]
        Tree[idx] += X

    else:

        # Divide segment tree into left
        # and right subtree
        m = (s + e) // 2

        # Check if pos lies in left subtree
        if (pos <= m):

            # Search pos in left subtree
            update(Tree, 2 * idx, s, m, pos, X)
        else:

            # Search pos in right subtree
            update(Tree, 2 * idx + 1, m + 1, e,pos, X)

        # Update Tree[idx]
        Tree[idx] = Tree[2 * idx] + Tree[2 * idx + 1]

# Function to find the sum from
# elements in the range [0, X]
def sum(Tree, idx, s, e, ql, qr):

    # Check if range[ql, qr] equals
    # to range [s, e]
    if (ql == s and qr == e):
        return Tree[idx]

    if (ql > qr):
        return 0

    # Divide segment tree into
    # left substree and
    # right substree
    m = (s + e) // 2

    # Return sum of elements in the range[ql, qr]
    return sum(Tree, 2 * idx, s, m, ql, min(m, qr))+ sum(Tree, 2 * idx + 1, m + 1, e,max(ql, m + 1), qr)

# Function to find Xth element
# in the array
def getElement(Tree, X, N):

    # Prelement at index x
    print("Element at", X, "is ", sum(Tree, 1, 0, N - 1, 0, X))

# Function to update array elements
# in the range [L, R]
def range_Update(Tree, L, R, X, N):

    # Update arr[l] += X
    update(Tree, 1, 0, N - 1, L, X)

    # Update arr[R + 1] += X
    if (R + 1 < N):
        update(Tree, 1, 0, N - 1, R + 1, -X)

# Drivers Code
if __name__ == '__main__':

    # Size of array
    N = 5
    Tree = [0]*(4 * N + 5)
    arr = [0, 0]
    Q = [ [1, 0, 1, 100], [2, 1] ]
    cntQuery = len(Q)
    for i in range(cntQuery):
        if (Q[i][0] == 1):
            range_Update(Tree, Q[i][1], Q[i][2], Q[i][3], N)
        else:
            getElement(Tree, Q[i][1], N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Function to update the array elements
  // at idx pos, i.e arr[pos] += X
  static void update(int []Tree, int idx, int s,
                     int e, int pos, int X)
  {

    // If current node is a
    // leaf nodes
    if (s == e)
    {

      // Update Tree[idx]
      Tree[idx] += X;
    }

    else
    {

      // Divide segment tree into left
      // and right subtree
      int m = (s + e) / 2;

      // Check if pos lies in left subtree
      if (pos <= m)
      {

        // Search pos in left subtree
        update(Tree, 2 * idx, s, m, pos, X);
      }
      else
      {

        // Search pos in right subtree
        update(Tree, 2 * idx + 1, m + 1, e,
               pos, X);
      }

      // Update Tree[idx]
      Tree[idx]
        = Tree[2 * idx] + Tree[2 * idx + 1];
    }
  }

  // Function to find the sum from
  // elements in the range [0, X]
  static int sum(int []Tree, int idx, int s,
                 int e, int ql, int qr)
  {

    // Check if range[ql, qr] equals
    // to range [s, e]
    if (ql == s && qr == e)
      return Tree[idx];

    if (ql > qr)
      return 0;

    // Divide segment tree into
    // left substree and
    // right substree
    int m = (s + e) / 2;

    // Return sum of elements in the range[ql, qr]
    return sum(Tree, 2 * idx, s, m, ql, Math.Min(m, qr))
      + sum(Tree, 2 * idx + 1, m + 1, e,
            Math.Max(ql, m + 1), qr);
  }

  // Function to find Xth element
  // in the array
  static void getElement(int []Tree, int X, int N)
  {

    // Print element at index x
    Console.Write("Element at " +  X+ " is "
                  + sum(Tree, 1, 0, N - 1, 0, X) +"\n");
  }

  // Function to update array elements
  // in the range [L, R]
  static void range_Update(int []Tree, int L,
                           int R, int X, int N)
  {

    // Update arr[l] += X
    update(Tree, 1, 0, N - 1, L, X);

    // Update arr[R + 1] += X
    if (R + 1 < N)
      update(Tree, 1, 0, N - 1, R + 1, -X);
  }

  // Drivers Code
  public static void Main(String[] args)
  {

    // Size of array
    int N = 5;
    int []Tree = new int[4 * N + 5];
    int []arr = { 0, 0 };
    int[,]Q = { { 1, 0, 1, 100 }, { 2, 1, 0, 0 } };
    int cntQuery = Q.GetLength(0);
    for (int i = 0; i < cntQuery; i++)
    {
      if (Q[i, 0] == 1)
      {
        range_Update(Tree, Q[i, 1],
                     Q[i, 2], Q[i, 3], N);
      }
      else
      {
        getElement(Tree, Q[i, 1], N);
      }
    }
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to update the array elements
// at idx pos, i.e arr[pos] += X
function update(Tree, idx, s, e, pos, X)
{
    // If current node is a
    // leaf nodes
    if (s == e) {

        // Update Tree[idx]
        Tree[idx] += X;
    }

    else {

        // Divide segment tree into left
        // and right subtree
        var m = parseInt((s + e) / 2);

        // Check if pos lies in left subtree
        if (pos <= m) {

            // Search pos in left subtree
            update(Tree, 2 * idx, s, m, pos, X);
        }
        else {

            // Search pos in right subtree
            update(Tree, 2 * idx + 1, m + 1, e,
                   pos, X);
        }

        // Update Tree[idx]
        Tree[idx]
            = Tree[2 * idx] + Tree[2 * idx + 1];
    }
}

// Function to find the sum from
// elements in the range [0, X]
function sum(Tree, idx, s, e, ql, qr)
{
    // Check if range[ql, qr] equals
    // to range [s, e]
    if (ql == s && qr == e)
        return Tree[idx];

    if (ql > qr)
        return 0;

    // Divide segment tree into
    // left substree and
    // right substree
    var m =parseInt((s + e) / 2);

    // Return sum of elements in the range[ql, qr]
    return sum(Tree, 2 * idx, s, m, ql, Math.min(m, qr))
           + sum(Tree, 2 * idx + 1, m + 1, e,
                 Math.max(ql, m + 1), qr);
}

// Function to find Xth element
// in the array
function getElement(Tree, X, N)
{
    // Print element at index x
    document.write( "Element at " + X + " is "
         + sum(Tree, 1, 0, N - 1, 0, X) );
}

// Function to update array elements
// in the range [L, R]
function range_Update(Tree, L, R, X, N)
{

    // Update arr[l] += X
    update(Tree, 1, 0, N - 1, L, X);

    // Update arr[R + 1] += X
    if (R + 1 < N)
        update(Tree, 1, 0, N - 1, R + 1, -X);
}

// Drivers Code
// Size of array
var N = 5;
var Tree = Array(4 * N + 5).fill(0);
var arr = [ 0, 0 ];
var Q = [[ 1, 0, 1, 100 ], [ 2, 1 ]];
var cntQuery = Q.length;
for (var i = 0; i < cntQuery; i++) {
    if (Q[i][0] == 1) {
        range_Update(Tree, Q[i][1],
                     Q[i][2], Q[i][3], N);
    }
    else {
        getElement(Tree, Q[i][1], N);
    }
}

</script>
```

**Output:** 

```
Element at 1 is 100
```

***时间复杂度:**O(| Q | * log(N))*
***辅助空间:** O(N)*