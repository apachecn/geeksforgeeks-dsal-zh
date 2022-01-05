# 对具有单个设置位的给定范围内的数组元素进行计数的查询

> 原文:[https://www . geesforgeks . org/query-to-count-array-elements-from-a-给定范围-具有单个设置位-2/](https://www.geeksforgeeks.org/queries-to-count-array-elements-from-a-given-range-having-a-single-set-bit-2/)

给定一个由 **N** 个整数组成的 [<u>数组</u>](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个由以下两种类型的查询组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** :

*   **1 L R:** 打印只有一个设定位的范围**【L，R】**中的数字计数。
*   **2 X V:** 用 **V** 更新**X<sup>th</sup>T5】索引处的数组元素。**

**示例:**

> ***输入:** arr[] = { 12，11，16，2，32 }，Q[][] = { { 1，0，2 }，{ 2，4，24 }，{ 1，1，4 } }*
> ***输出:** 1 2*
> ***解释:***
> 
> *   *查询 1:打印索引[0，2]范围内只有一位的数组元素个数，即{16}。*
> *   *查询 2:设置 **arr[4] = 24** 。因此，arr[]数组修改为{12，11，16，24，5}。*
> *   *查询 3:打印索引[1，4]范围内只有一位的数组元素个数，即{16，32}。*
> 
> ***输入:** arr[] = { 2，1，101，11，4 }，Q[][] = { { 1，2，4 }，{ 2，4，12 }，{ 1，2，4 } }*
> ***输出:** 1 0*
> ***解释:***
> 
> *   *查询 1:打印索引[2，4]范围内只有一位的数组元素个数，即{4}。*
> *   *查询 2:设置 **arr[4] = 24** ，将数组修改为 arr[] = { 2，1，101，11，12}。*
> *   *查询 3:打印索引[2，4]范围内只有一位的数组元素的计数。但是给定范围的索引中没有一个数组元素只包含一个位。*

**简单方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的索引范围**【L，R】**对于每个查询和每个元素，检查它是否有精确的**一个设置位**。对于发现为真的每个数组元素，递增**计数**。在[遍历](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)整个范围后，打印**计数**的值。对于类型 2 的查询，只需 **arr[X] = V** 。
***时间复杂度:**O(N * Q * log(N))*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)进行优化。按照以下步骤解决问题:

*   定义一个函数，**检查(S)** 以检查整数是否只包含一个设置位。
*   初始化 3 个变量: **ss、se、**和 **si** 分别存储当前线段的起点、当前线段的终点和线段树中的当前节点值。
*   定义一个函数，比如说 **build_seg(ss，se，si)**来构建[一个段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)类似于[的求和段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，每个节点存储元素的计数，在其子树中只有一个位:
    *   如果 **ss == se，树[s[i]] =检查(arr[ss]** )
    *   否则，遍历左子树和右子树。
    *   现在，将当前节点更新为**树[si] =树[2 * si + 1]+树[2 * si + 2]。**
*   定义一个函数，比如**更新(ss，se，si，X，V)** ，指向更新数组中的一个值 **arr[]:**
    *   如果当前节点是叶节点，即 **ss == se** 则更新**树【si】= check(V)。**
    *   否则，搜索第 X <sup>个</sup>索引，即如果 **X ≤ (ss + se) / 2** ，则遍历左侧子树，即**更新(ss，mid，2 * si + 1，X，V)。**否则，遍历右子树即**更新(mid + 1，se，2 * si + 2，X，V)。**
    *   更新当前节点。
*   定义一个函数，比如说**查询(ss，se，si，L，R)** 来计算在范围**【L，R】:**中只有一位的数字
    *   检查当前线段**【L，R】**是否与**【ss，se】**不相交，然后返回 **0。**
    *   否则，如果**ss>= L****se≤R**则返回**树【si】**。
    *   如果以上条件都不满足，则返回**查询(ss，mid，L，R，2 * si+1)+查询(mid + 1，se，L，R，2 * si + 2)** 。
*   对于 **{ 1，L，R }** 类型的查询，打印**查询(0，N-1，0，L，R)。**
*   对于类型为 **{ 2，X，V }，**的查询，更新树中的值，**更新(0，N-1，0，X，V)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation
// for above approach

#include <bits/stdc++.h>
using namespace std;

// Check if N has only
// one set bit
bool check(int N)
{
    if (N == 0)
        return 0;
    return !(N & (N - 1));
}

// Function to build segment tree
void build_seg_tree(int ss, int se, int si,
                    int tree[], int arr[])
{
    // If se is leaf node
    if (ss == se) {

        // Update the node
        tree[si] = check(arr[ss]);
        return;
    }

    // Stores mid value of segment [ss, se]
    int mid = (ss + se) / 2;

    // Recursive call for left Subtree
    build_seg_tree(ss, mid,
                   2 * si + 1, tree, arr);

    // Recursive call for right Subtree
    build_seg_tree(mid + 1, se,
                   2 * si + 2, tree, arr);

    // Update the Current Node
    tree[si] = tree[2 * si + 1]
               + tree[2 * si + 2];
}

// Function to update a value at Xth index
void update(int ss, int se, int si,
            int X, int V, int tree[], int arr[])
{

    if (ss == se) {

        // If ss is equal to X
        if (ss == X) {

            // Update the Xth node
            arr[X] = V;

            // Update the tree
            tree[si] = check(V);
        }
        return;
    }

    // Stores the mid of segment [ss, se]
    int mid = (ss + se) / 2;

    if (X <= mid)
        update(ss, mid, 2 * si + 1,
               X, V, tree, arr);
    else
        update(mid + 1, se, 2 * si + 2,
               X, V, tree, arr);

    // Update current node
    tree[si] = tree[2 * si + 1]
               + tree[2 * si + 2];
}

// Count of numbers
// having one set bit
int query(int l, int r, int ss,
          int se, int si, int tree[])
{
    // If L > se or R < ss
    // Invalid Range
    if (r < ss || l > se)
        return 0;

    // If [ss, se] lies
    // inside the [L, R]
    if (l <= ss && r >= se)
        return tree[si];

    // Stores the mid of segment [ss, se]
    int mid = (ss + se) / 2;

    // Return the sum after recursively
    // traversing left and right subtree
    return query(l, r, ss,
                 mid, 2 * si + 1, tree)
           + query(l, r, mid + 1,
                   se, 2 * si + 2, tree);
}

// Function to solve queries
void Query(int arr[], int N,
           vector<vector<int> > Q)
{
    // Initialise Segment tree
    int tree[4 * N] = { 0 };

    // Build segment tree
    build_seg_tree(0, N - 1, 0, tree, arr);

    // Perform queries
    for (int i = 0; i < (int)Q.size(); i++) {
        if (Q[i][0] == 1)

            cout << query(Q[i][1], Q[i][2],
                          0, N - 1, 0, tree)
                 << " ";
        else
            update(0, N - 1, 0, Q[i][1], Q[i][2], tree,
                   arr);
    }
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 12, 11, 16, 2, 32 };
    vector<vector<int> > Q{ { 1, 0, 2 },
                            { 2, 4, 24 },
                            { 1, 1, 4 } };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to
    // solve queries
    Query(arr, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
class GFG {

  // Check if N has only
  // one set bit
  static int check(int N)
  {
    if (Integer.bitCount(N) == 1)
      return 1;
    else
      return 0;
  }

  // Function to build segment tree
  static void build_seg_tree(int ss, int se, int si,
                             int tree[], int arr[])
  {

    // If se is leaf node
    if (ss == se)
    {

      // Update the node
      tree[si] = check(arr[ss]);
      return;
    }

    // Stores mid value of segment [ss, se]
    int mid = (ss + se) / 2;

    // Recursive call for left Subtree
    build_seg_tree(ss, mid, 2 * si + 1, tree, arr);

    // Recursive call for right Subtree
    build_seg_tree(mid + 1, se, 2 * si + 2, tree, arr);

    // Update the Current Node
    tree[si] = tree[2 * si + 1] + tree[2 * si + 2];
  }

  // Function to update a value at Xth index
  static void update(int ss, int se, int si, int X, int V,
                     int tree[], int arr[])
  {

    if (ss == se)
    {

      // If ss is equal to X
      if (ss == X)
      {

        // Update the Xth node
        arr[X] = V;

        // Update the tree
        tree[si] = check(V);
      }
      return;
    }

    // Stores the mid of segment [ss, se]
    int mid = (ss + se) / 2;

    if (X <= mid)
      update(ss, mid, 2 * si + 1, X, V, tree, arr);
    else
      update(mid + 1, se, 2 * si + 2, X, V, tree,
             arr);

    // Update current node
    tree[si] = tree[2 * si + 1] + tree[2 * si + 2];
  }

  // Count of numbers
  // having one set bit
  static int query(int l, int r, int ss,
                   int se, int si,
                   int tree[])
  {
    // If L > se or R < ss
    // Invalid Range
    if (r < ss || l > se)
      return 0;

    // If [ss, se] lies
    // inside the [L, R]
    if (l <= ss && r >= se)
      return tree[si];

    // Stores the mid of segment [ss, se]
    int mid = (ss + se) / 2;

    // Return the sum after recursively
    // traversing left and right subtree
    return query(l, r, ss, mid, 2 * si + 1, tree)
      + query(l, r, mid + 1, se, 2 * si + 2, tree);
  }

  // Function to solve queries
  static void Query(int arr[], int N, int[][] Q)
  {
    // Initialise Segment tree
    int tree[] = new int[4 * N];

    // Build segment tree
    build_seg_tree(0, N - 1, 0, tree, arr);

    // Perform queries
    for (int i = 0; i < Q.length; i++) {
      if (Q[i][0] == 1)

        System.out.print(query(Q[i][1], Q[i][2], 0,
                               N - 1, 0, tree) + " ");
      else
        update(0, N - 1, 0, Q[i][1], Q[i][2], tree,
               arr);
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 12, 11, 16, 2, 32 };
    int[][] Q
      = { { 1, 0, 2 }, { 2, 4, 24 }, { 1, 1, 4 } };
    int N = arr.length;

    // Function call to
    // solve queries
    Query(arr, N, Q);
  }
}

// This code is contributed by hemanthsawarna1506.
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Check if N has only
# one set bit
def check(N) :

    if (N == 0):
        return 0
    return ((N & (N - 1)) == 0)

# Function to build segment tree
def build_seg_tree(ss, se, si, tree, arr) :

    # If se is leaf node
    if (ss == se) :

        # Update the node
        tree[si] = check(arr[ss])
        return

    # Stores mid value of segment [ss, se]
    mid = (ss + se) // 2

    # Recursive call for left Subtree
    build_seg_tree(ss, mid,
                   2 * si + 1, tree, arr)

    # Recursive call for right Subtree
    build_seg_tree(mid + 1, se,
                   2 * si + 2, tree, arr)

    # Update the Current Node
    tree[si] = tree[2 * si + 1] + tree[2 * si + 2]

# Function to update a value at Xth index
def update(ss, se, si, X, V, tree, arr) :
    if (ss == se) :

        # If ss is equal to X
        if (ss == X) :

            # Update the Xth node
            arr[X] = V

            # Update the tree
            tree[si] = check(V)   
        return

    # Stores the mid of segment [ss, se]
    mid = (ss + se) // 2

    if (X <= mid):
        update(ss, mid, 2 * si + 1,
               X, V, tree, arr)
    else :
        update(mid + 1, se, 2 * si + 2,
               X, V, tree, arr)

    # Update current node
    tree[si] = tree[2 * si + 1] + tree[2 * si + 2]

# Count of numbers
# having one set bit
def query(l, r, ss, se, si, tree) :

    # If L > se or R < ss
    # Invalid Range
    if (r < ss or l > se):
        return 0

    # If [ss, se] lies
    # inside the [L, R]
    if (l <= ss and r >= se):
        return tree[si]

    # Stores the mid of segment [ss, se]
    mid = (ss + se) // 2

    # Return the sum after recursively
    # traversing left and right subtree
    return (query(l, r, ss, mid, 2 * si + 1, tree) + query(l, r, mid + 1, se, 2 * si + 2, tree))

# Function to solve queries
def Query(arr, N, Q) :

    # Initialise Segment tree
    tree = [0] * (4 * N)

    # Build segment tree
    build_seg_tree(0, N - 1, 0, tree, arr)

    # Perform queries
    for i in range(len(Q)):
        if (Q[i][0] == 1):

            print(query(Q[i][1], Q[i][2],
                          0, N - 1, 0, tree), end = " ")
        else :
            update(0, N - 1, 0, Q[i][1], Q[i][2], tree, arr)

# Driver Code

# Input
arr = [ 12, 11, 16, 2, 32 ]
Q = [ [ 1, 0, 2 ], [ 2, 4, 24 ], [ 1, 1, 4 ]] 
N = len(arr)

# Function call to
# solve queries
Query(arr, N, Q)

# This code is contributed by code_hunt.
```

## C#

```
// C# implementation
// for above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Check if N has only
  // one set bit
  static int check(int N)
  {
    if (N == 0 || (N & (N - 1)) != 0)
      return 0;

    return 1;
  }

  // Function to build segment tree
  static void build_seg_tree(int ss, int se, int si,
                             int[] tree, int[] arr)
  {

    // If se is leaf node
    if (ss == se)
    {

      // Update the node
      tree[si] = check(arr[ss]);
      return;
    }

    // Stores mid value of segment [ss, se]
    int mid = (ss + se) / 2;

    // Recursive call for left Subtree
    build_seg_tree(ss, mid,
                   2 * si + 1, tree, arr);

    // Recursive call for right Subtree
    build_seg_tree(mid + 1, se,
                   2 * si + 2, tree, arr);

    // Update the Current Node
    tree[si] = tree[2 * si + 1]
      + tree[2 * si + 2];
  }

  // Function to update a value at Xth index
  static void update(int ss, int se, int si,
                     int X, int V, int[] tree, int[] arr)
  {

    if (ss == se)
    {

      // If ss is equal to X
      if (ss == X)
      {

        // Update the Xth node
        arr[X] = V;

        // Update the tree
        tree[si] = check(V);
      }
      return;
    }

    // Stores the mid of segment [ss, se]
    int mid = (ss + se) / 2;

    if (X <= mid)
      update(ss, mid, 2 * si + 1,
             X, V, tree, arr);
    else
      update(mid + 1, se, 2 * si + 2,
             X, V, tree, arr);

    // Update current node
    tree[si] = tree[2 * si + 1]
      + tree[2 * si + 2];
  }

  // Count of numbers
  // having one set bit
  static int query(int l, int r, int ss,
                   int se, int si, int[] tree)
  {

    // If L > se or R < ss
    // Invalid Range
    if (r < ss || l > se)
      return 0;

    // If [ss, se] lies
    // inside the [L, R]
    if (l <= ss && r >= se)
      return tree[si];

    // Stores the mid of segment [ss, se]
    int mid = (ss + se) / 2;

    // Return the sum after recursively
    // traversing left and right subtree
    return query(l, r, ss,
                 mid, 2 * si + 1, tree)
      + query(l, r, mid + 1,
              se, 2 * si + 2, tree);
  }

  // Function to solve queries
  static void Query(int[] arr, int N,
                    List<List<int> > Q)
  {

    // Initialise Segment tree
    int[] tree = new int[4 * N];

    // Build segment tree
    build_seg_tree(0, N - 1, 0, tree, arr);

    // Perform queries
    for (int i = 0; i < (int)Q.Count; i++)
    {
      if (Q[i][0] == 1)      
        Console.Write(query(Q[i][1], Q[i][2], 0, N - 1, 0, tree) + " ");
      else
        update(0, N - 1, 0, Q[i][1], Q[i][2], tree, arr);
    }
  } 

  // Driver code
  static void Main()
  {

    // Input
    int[] arr = { 12, 11, 16, 2, 32 };
    List<List<int> > Q = new List<List<int>>();
    Q.Add(new List<int>(new int[]{1, 0, 2}));
    Q.Add(new List<int>(new int[]{2, 4, 24}));
    Q.Add(new List<int>(new int[]{1, 1, 4}));
    int N = arr.Length;

    // Function call to
    // solve queries
    Query(arr, N, Q);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript implementation
// for above approach

// Check if N has only
// one set bit
function check( N)
{
    if (N == 0)
        return 0;
    return !(N & (N - 1));
}

// Function to build segment tree
function build_seg_tree( ss,  se,  si, tree, arr)
{
    // If se is leaf node
    if (ss == se) {

        // Update the node
        tree[si] = check(arr[ss]);
        return;
    }

    // Stores mid value of segment [ss, se]
    var mid = parseInt((ss + se) / 2);

    // Recursive call for left Subtree
    build_seg_tree(ss, mid, 2 * si + 1, tree, arr);

    // Recursive call for right Subtree
    build_seg_tree(mid + 1, se, 2 * si + 2, tree, arr);

    // Update the Current Node
    tree[si] = tree[2 * si + 1] + tree[2 * si + 2];
}

// Function to update a value at Xth index
function update(ss, se, si, X, V, tree,  arr)
{

    if (ss == se) {

        // If ss is equal to X
        if (ss == X) {

            // Update the Xth node
            arr[X] = V;

            // Update the tree
            tree[si] = check(V);
        }
        return;
    }

    // Stores the mid of segment [ss, se]
    var mid = parseInt((ss + se) / 2);

    if (X <= mid)
        update(ss, mid, 2 * si + 1, X, V, tree, arr);
    else
        update(mid + 1, se, 2 * si + 2, X, V, tree, arr);

    // Update current node
    tree[si] = tree[2 * si + 1] + tree[2 * si + 2];
}

// Count of numbers
// having one set bit
function query( l, r, ss, se, si, tree)
{
    // If L > se or R < ss
    // Invalid Range
    if (r < ss || l > se)
        return 0;

    // If [ss, se] lies
    // inside the [L, R]
    if (l <= ss && r >= se)
        return tree[si];

    // Stores the mid of segment [ss, se]
    var mid = parseInt((ss + se) / 2);

    // Return the sum after recursively
    // traversing left and right subtree
    return query(l, r, ss, mid, 2 * si + 1, tree)
           + query(l, r, mid + 1, se, 2 * si + 2, tree);
}

// Function to solve queries
function Query(arr, N, Q)
{
    // Initialise Segment tree
    var tree = new Array(4 * N);
    tree.fill( 0 );

    // Build segment tree
    build_seg_tree(0, N - 1, 0, tree, arr);

    // Perform queries
    for (var i = 0; i < Q.length; i++) {
        if (Q[i][0] == 1)

            document.write( query(Q[i][1], Q[i][2],
                          0, N - 1, 0, tree)
                 + " ");
        else
            update(0, N - 1, 0, Q[i][1], Q[i][2], tree,
                   arr);
    }
}

var arr = [ 12, 11, 16, 2, 32 ];
var Q = [ [1, 0, 2 ],
          [ 2, 4, 24],
          [ 1, 1, 4 ] ];
    var N = arr.length;

    // Function call to
    // solve queries
    Query(arr, N, Q);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1 2
```

***时间复杂度:**O(N * log(N)+Q * log(N))*
***辅助空间:** O(1)*