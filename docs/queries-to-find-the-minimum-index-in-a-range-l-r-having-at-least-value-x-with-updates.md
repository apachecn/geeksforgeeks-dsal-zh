# 通过更新来查找至少具有值 X 的范围[L，R]中的最小索引的查询

> 原文:[https://www . geesforgeks . org/query-to-find-a-range-l-r-with-updates-value-x/](https://www.geeksforgeeks.org/queries-to-find-the-minimum-index-in-a-range-l-r-having-at-least-value-x-with-updates/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由 **Q** 个查询组成的**查询数组**，类型为 **{X，L，R}** 以执行以下操作:

*   如果 **X** 的值为 **1** ，则将**X<sup>th</sup>T7】索引处的数组元素更新为 **L** 。**
*   否则，在**【L，R】**范围内找到最小指数 **j** ，使得**arr【j】≥X**。如果不存在这样的 **j** ，则打印**-1”**。

**示例:**

> **输入:** arr[] = {1，3，2，4，6}，查询[][] = {{2，0，4}，{1，2，5}，{4，0，4}，{0，0，4 } }
> T3】输出:1 2 0
> T6】解释:
> 查询 1:查找(2，0，4) = >第一个至少为 2 的元素为 3。所以，它的指数是 1。
> 查询 2:更新(2，5) = > arr[] = {1，3，5，4，6}。
> 查询 3:查找(4，0，4) = >第一个至少为 4 的元素为 5。所以，它的指数是 2。
> 查询 4:查找(0，0，4) = >第一个至少为 0 的元素为 1。所以，它的指数是 0。
> 
> **输入:** arr[] = {1}，query[][]= { { 2，0，0 } }；
> **输出:** 1 2 0
> **解释:**
> 查询 1:查找(2，0，0) = >无大于 2 的元素。因此，打印-1。

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)进行每个查询。对于**类型 1** 的查询，更新**A【X】**为 **L** 。对于**类型 2** 、[的查询，在**【L，R】**范围内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，找到满足条件的最小索引 **j** 。如果没有找到这样的索引，则打印**-1”**。
***时间复杂度:** O(N*Q)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，想法是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)以便高效地执行查询。按照以下步骤解决问题:

*   构建[线段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，其中每个节点将代表该节点范围内的[最大值。例如，对于任何给定的范围**【I，j】**，其对应的节点将包含该范围内的最大值。](https://www.geeksforgeeks.org/maximum-value-array-m-range-increment-operations/)
*   初始化一个变量，比如**和**。
*   现在，对于类型 2 的查询，如果当前范围不在范围**【L，R】**内，则遍历其左子树。
*   现在，在左子树中，如果最大值超过 **X** ，并且当前范围在**【L，R】**范围内，则转到该范围的**中点**，检查其值是否大于 **X** 。如果发现是真的，请访问它的左侧部分。否则，访问它的右边部分。
*   如果存在，将变量**和**更新为给定范围之间的最小索引。
*   继续上述步骤，直到范围的左边部分等于右边部分。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define maxN 100
using namespace std;

// Stores nodes value of the Tree
int Tree[4 * maxN];

// Function to build segment tree
void build(int arr[], int index,
           int s, int e)
{
    // Base Case
    if (s == e)
        Tree[index] = arr[s];

    else {
        // Find the value of mid
        int m = (s + e) / 2;

        // Update for left subtree
        build(arr, 2 * index, s, m);

        // Update for right subtree
        build(arr, 2 * index + 1,
              m + 1, e);

        // Update the value at the
        // current index
        Tree[index]
            = max(Tree[2 * index],
                  Tree[2 * index + 1]);
    }
}

// Function for finding the index
// of the first element at least x
int atleast_x(int index, int s, int e,
              int ql, int qr, int x)
{
    // If current range does
    // not lie in query range
    if (ql > e || qr < s)
        return -1;

    // If current range is inside
    // of query range
    if (s <= ql && e <= qr) {

        // Maximum value in this
        // range is less than x
        if (Tree[index] < x)
            return -1;

        // Finding index of first
        // value in this range
        while (s != e) {
            int m = (s + e) / 2;

            // Update the value of
            // the minimum index
            if (Tree[2 * index] >= x) {
                e = m;
                index = 2 * index;
            }
            else {
                s = m + 1;
                index = 2 * index + 1;
            }
        }
        return s;
    }

    // Find mid of the current range
    int m = (s + e) / 2;

    // Left subtree
    int val = atleast_x(2 * index, s,
                        m, ql, qr, x);

    if (val != -1)
        return val;

    // If it does not lie in
    // left subtree
    return atleast_x(2 * index + 1, m + 1,
                     e, ql, qr, x);
}

// Function for updating segment tree
void update(int index, int s, int e,
            int new_val, int pos)
{
    // Update the value, we
    // reached leaf node
    if (s == e)
        Tree[index] = new_val;

    else {

        // Find the mid
        int m = (s + e) / 2;

        if (pos <= m) {

            // If pos lies in the
            // left subtree
            update(2 * index, s, m,
                   new_val, pos);
        }
        else {

            // pos lies in the
            // right subtree
            update(2 * index + 1,
                   m + 1, e,
                   new_val, pos);
        }

        // Update the maximum value
        // in the range
        Tree[index]
            = max(Tree[2 * index],
                  Tree[2 * index + 1]);
    }
}

// Function to print the answer
// for the given queries
void printAnswer(int* arr, int n)
{
    // Build segment tree
    build(arr, 1, 0, n - 1);

    // Find index of first value
    // atleast 2 in range [0, n-1]
    cout << atleast_x(1, 0, n - 1,
                      0, n - 1, 2)
         << "\n";

    // Update value at index 2 to 5
    arr[2] = 5;
    update(1, 0, n - 1, 5, 2);

    // Find index of first value
    // atleast 4 in range [0, n-1]
    cout << atleast_x(1, 0, n - 1,
                      0, n - 1, 4)
         << "\n";

    // Find index of first value
    // atleast 0 in range [0, n-1]
    cout << atleast_x(1, 0, n - 1,
                      0, n - 1, 0)
         << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 2, 4, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printAnswer(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

static int maxN = 100;

// Stores nodes value of the Tree
static int Tree[] = new int[4 * maxN];

// Function to build segment tree
static void build(int arr[], int index,
           int s, int e)
{
    // Base Case
    if (s == e)
        Tree[index] = arr[s];

    else
    {

        // Find the value of mid
        int m = (s + e) / 2;

        // Update for left subtree
        build(arr, 2 * index, s, m);

        // Update for right subtree
        build(arr, 2 * index + 1,
              m + 1, e);

        // Update the value at the
        // current index
        Tree[index]
            = Math.max(Tree[2 * index],
                  Tree[2 * index + 1]);
    }
}

// Function for finding the index
// of the first element at least x
static int atleast_x(int index, int s, int e,
              int ql, int qr, int x)
{
    // If current range does
    // not lie in query range
    if (ql > e || qr < s)
        return -1;

    // If current range is inside
    // of query range
    if (s <= ql && e <= qr) {

        // Maximum value in this
        // range is less than x
        if (Tree[index] < x)
            return -1;

        // Finding index of first
        // value in this range
        while (s != e) {
            int m = (s + e) / 2;

            // Update the value of
            // the minimum index
            if (Tree[2 * index] >= x) {
                e = m;
                index = 2 * index;
            }
            else {
                s = m + 1;
                index = 2 * index + 1;
            }
        }
        return s;
    }

    // Find mid of the current range
    int m = (s + e) / 2;

    // Left subtree
    int val = atleast_x(2 * index, s,
                        m, ql, qr, x);
    if (val != -1)
        return val;

    // If it does not lie in
    // left subtree
    return atleast_x(2 * index + 1, m + 1,
                     e, ql, qr, x);
}

// Function for updating segment tree
static void update(int index, int s, int e,
            int new_val, int pos)
{

    // Update the value, we
    // reached leaf node
    if (s == e)
        Tree[index] = new_val;
    else
    {

        // Find the mid
        int m = (s + e) / 2;

        if (pos <= m)
        {

            // If pos lies in the
            // left subtree
            update(2 * index, s, m,
                   new_val, pos);
        }
        else
        {

            // pos lies in the
            // right subtree
            update(2 * index + 1,
                   m + 1, e,
                   new_val, pos);
        }

        // Update the maximum value
        // in the range
        Tree[index]
            = Math.max(Tree[2 * index],
                  Tree[2 * index + 1]);
    }
}

// Function to print the answer
// for the given queries
static void printAnswer(int[] arr, int n)
{

    // Build segment tree
    build(arr, 1, 0, n - 1);

    // Find index of first value
    // atleast 2 in range [0, n-1]
    System.out.println(atleast_x(1, 0, n - 1,
                      0, n - 1, 2));

    // Update value at index 2 to 5
    arr[2] = 5;
    update(1, 0, n - 1, 5, 2);

    // Find index of first value
    // atleast 4 in range [0, n-1]
    System.out.println(atleast_x(1, 0, n - 1,
                      0, n - 1, 4));

    // Find index of first value
    // atleast 0 in range [0, n-1]
    System.out.println(atleast_x(1, 0, n - 1,
                      0, n - 1, 0));
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 2, 4, 6 };
    int N = arr.length;

    // Function Call
    printAnswer(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
maxN = 100

# Stores nodes value of the Tree
Tree = [0 for i in range(4 * maxN)]

# Function to build segment tree
def build(arr, index, s, e):

    # Base Case
    global Tree
    global max
    if (s == e):
        Tree[index] = arr[s]
    else:

        # Find the value of mid
        m = (s + e) // 2

        # Update for left subtree
        build(arr, 2 * index, s, m)

        # Update for right subtree
        build(arr, 2 * index + 1, m + 1, e)

        # Update the value at the
        # current index
        Tree[index] = max(Tree[2 * index],
                          Tree[2 * index + 1])

# Function for finding the index
# of the first element at least x
def atleast_x(index, s,  e,  ql, qr, x):
    global Tree
    global max

    # If current range does
    # not lie in query range
    if (ql > e or qr < s):
        return -1

    # If current range is inside
    # of query range
    if (s <= ql and e <= qr):

        # Maximum value in this
        # range is less than x
        if (Tree[index] < x):
            return -1;

        # Finding index of first
        # value in this range
        while (s != e):
            m = (s + e) // 2

            # Update the value of
            # the minimum index
            if (Tree[2 * index] >= x):
                e = m
                index = 2 * index
            else:
                s = m + 1
                index = 2 * index + 1
        return s

    # Find mid of the current range
    m = (s + e) // 2

    # Left subtree
    val = atleast_x(2 * index, s, m, ql, qr, x)
    if (val != -1):
        return val

    # If it does not lie in
    # left subtree
    return atleast_x(2 * index + 1, m + 1,e, ql, qr, x)

# Function for updating segment tree
def update(index, s, e, new_val, pos):
    global Tree
    global max

    # Update the value, we
    # reached leaf node
    if (s == e):
        Tree[index] = new_val
    else:

        # Find the mid
        m = (s + e) // 2

        if (pos <= m):
            # If pos lies in the
            # left subtree
            update(2 * index, s, m,new_val, pos)
        else:
            # pos lies in the
            # right subtree
            update(2 * index + 1, m + 1, e, new_val, pos)

        # Update the maximum value
        # in the range
        Tree[index] = max(Tree[2 * index], Tree[2 * index + 1])

# Function to print the answer
# for the given queries
def printAnswer(arr, n):
    global Tree
    global max

    # Build segment tree
    build(arr, 1, 0, n - 1)

    # Find index of first value
    # atleast 2 in range [0, n-1]
    print(atleast_x(1, 0, n - 1, 0, n - 1, 2))

    # Update value at index 2 to 5
    arr[2] = 5
    update(1, 0, n - 1, 5, 2)

    # Find index of first value
    # atleast 4 in range [0, n-1]
    print(atleast_x(1, 0, n - 1, 0, n - 1, 4))

    # Find index of first value
    # atleast 0 in range [0, n-1]
    print(atleast_x(1, 0, n - 1, 0, n - 1, 0))

# Driver Code
if __name__ == '__main__':
    arr =  [1, 3, 2, 4, 6]
    N =  len(arr)

    # Function Call
    printAnswer(arr, N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

static int maxN = 100;

// Stores nodes value of the Tree
static int[] Tree = new int[4 * maxN];

// Function to build segment tree
static void build(int[] arr, int index,
           int s, int e)
{
    // Base Case
    if (s == e)
        Tree[index] = arr[s];

    else
    {

        // Find the value of mid
        int m = (s + e) / 2;

        // Update for left subtree
        build(arr, 2 * index, s, m);

        // Update for right subtree
        build(arr, 2 * index + 1,
              m + 1, e);

        // Update the value at the
        // current index
        Tree[index]
            = Math.Max(Tree[2 * index],
                  Tree[2 * index + 1]);
    }
}

// Function for finding the index
// of the first element at least x
static int atleast_x(int index, int s, int e,
              int ql, int qr, int x)
{
    // If current range does
    // not lie in query range
    if (ql > e || qr < s)
        return -1;

    // If current range is inside
    // of query range
    if (s <= ql && e <= qr) {

        // Maximum value in this
        // range is less than x
        if (Tree[index] < x)
            return -1;

        // Finding index of first
        // value in this range
        while (s != e) {
            int m = (s + e) / 2;

            // Update the value of
            // the minimum index
            if (Tree[2 * index] >= x) {
                e = m;
                index = 2 * index;
            }
            else {
                s = m + 1;
                index = 2 * index + 1;
            }
        }
        return s;
    }

    // Find mid of the current range
    int mm = (s + e) / 2;

    // Left subtree
    int val = atleast_x(2 * index, s,
                        mm, ql, qr, x);
    if (val != -1)
        return val;

    // If it does not lie in
    // left subtree
    return atleast_x(2 * index + 1, mm + 1,
                     e, ql, qr, x);
}

// Function for updating segment tree
static void update(int index, int s, int e,
            int new_val, int pos)
{

    // Update the value, we
    // reached leaf node
    if (s == e)
        Tree[index] = new_val;
    else
    {

        // Find the mid
        int m = (s + e) / 2;

        if (pos <= m)
        {

            // If pos lies in the
            // left subtree
            update(2 * index, s, m,
                   new_val, pos);
        }
        else
        {

            // pos lies in the
            // right subtree
            update(2 * index + 1,
                   m + 1, e,
                   new_val, pos);
        }

        // Update the maximum value
        // in the range
        Tree[index]
            = Math.Max(Tree[2 * index],
                  Tree[2 * index + 1]);
    }
}

// Function to print the answer
// for the given queries
static void printAnswer(int[] arr, int n)
{

    // Build segment tree
    build(arr, 1, 0, n - 1);

    // Find index of first value
    // atleast 2 in range [0, n-1]
    Console.WriteLine(atleast_x(1, 0, n - 1,
                      0, n - 1, 2));

    // Update value at index 2 to 5
    arr[2] = 5;
    update(1, 0, n - 1, 5, 2);

    // Find index of first value
    // atleast 4 in range [0, n-1]
    Console.WriteLine(atleast_x(1, 0, n - 1,
                      0, n - 1, 4));

    // Find index of first value
    // atleast 0 in range [0, n-1]
    Console.WriteLine(atleast_x(1, 0, n - 1,
                      0, n - 1, 0));
}

// Driver code
static void Main()
{
    int[] arr = { 1, 3, 2, 4, 6 };
    int N = arr.Length;

    // Function Call
    printAnswer(arr, N);

}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach
    let maxN = 100;

    // Stores nodes value of the Tree
    let Tree = new Array(4 * maxN);

    // Function to build segment tree
    function build(arr, index, s, e)
    {
        // Base Case
        if (s == e)
            Tree[index] = arr[s];

        else
        {

            // Find the value of mid
            let m = parseInt((s + e) / 2, 10);

            // Update for left subtree
            build(arr, 2 * index, s, m);

            // Update for right subtree
            build(arr, 2 * index + 1,
                  m + 1, e);

            // Update the value at the
            // current index
            Tree[index]
                = Math.max(Tree[2 * index],
                      Tree[2 * index + 1]);
        }
    }

    // Function for finding the index
    // of the first element at least x
    function atleast_x(index, s, e, ql, qr, x)
    {
        // If current range does
        // not lie in query range
        if (ql > e || qr < s)
            return -1;

        // If current range is inside
        // of query range
        if (s <= ql && e <= qr) {

            // Maximum value in this
            // range is less than x
            if (Tree[index] < x)
                return -1;

            // Finding index of first
            // value in this range
            while (s != e) {
                let m = parseInt((s + e) / 2, 10);

                // Update the value of
                // the minimum index
                if (Tree[2 * index] >= x) {
                    e = m;
                    index = 2 * index;
                }
                else {
                    s = m + 1;
                    index = 2 * index + 1;
                }
            }
            return s;
        }

        // Find mid of the current range
        let m = parseInt((s + e) / 2, 10);

        // Left subtree
        let val = atleast_x(2 * index, s,
                            m, ql, qr, x);
        if (val != -1)
            return val;

        // If it does not lie in
        // left subtree
        return atleast_x(2 * index + 1, m + 1,
                         e, ql, qr, x);
    }

    // Function for updating segment tree
    function update(index, s, e, new_val, pos)
    {

        // Update the value, we
        // reached leaf node
        if (s == e)
            Tree[index] = new_val;
        else
        {

            // Find the mid
            let m = parseInt((s + e) / 2, 10);

            if (pos <= m)
            {

                // If pos lies in the
                // left subtree
                update(2 * index, s, m,
                       new_val, pos);
            }
            else
            {

                // pos lies in the
                // right subtree
                update(2 * index + 1,
                       m + 1, e,
                       new_val, pos);
            }

            // Update the maximum value
            // in the range
            Tree[index]
                = Math.max(Tree[2 * index],
                      Tree[2 * index + 1]);
        }
    }

    // Function to print the answer
    // for the given queries
    function printAnswer(arr, n)
    {

        // Build segment tree
        build(arr, 1, 0, n - 1);

        // Find index of first value
        // atleast 2 in range [0, n-1]
        document.write(atleast_x(1, 0, n - 1, 0, n - 1, 2) + "</br>");

        // Update value at index 2 to 5
        arr[2] = 5;
        update(1, 0, n - 1, 5, 2);

        // Find index of first value
        // atleast 4 in range [0, n-1]
        document.write(atleast_x(1, 0, n - 1, 0, n - 1, 4) + "</br>");

        // Find index of first value
        // atleast 0 in range [0, n-1]
        document.write(atleast_x(1, 0, n - 1, 0, n - 1, 0) + "</br>");
    }

    let arr = [ 1, 3, 2, 4, 6 ];
    let N = arr.length;

    // Function Call
    printAnswer(arr, N);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
1
2
0
```

***时间复杂度:** O(Q*log N)*
***辅助空间:** O(N)*