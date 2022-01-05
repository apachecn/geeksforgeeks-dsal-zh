# 从给定的逆矩阵中生成原始排列

> 原文:[https://www . geeksforgeeks . org/generate-origin-array-from-给定-array-of-inversion/](https://www.geeksforgeeks.org/generate-original-permutation-from-given-array-of-inversions/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **arr[i]** 表示左侧元素的数量大于原始排列中第 **i <sup>个</sup>** 元素的数量。任务是找到给定反转数组 **arr[]** 有效的**【1，N】**的原始排列。

**示例:**

> **输入:** arr[] = {0，1，1，0，3}
> **输出:** 4 1 3 5 2
> **解释:**
> 原排列为 ans[] = {4，1，3，5，2}
> ans[0] = 4。
> ans[1] = 1。由于{4}位于其左侧，超过 1，arr[1] = 1 有效。
> ans[2] = 3。由于{4}位于其左侧，超过 3，arr[2] = 1 有效。
> ans[3] = 5。由于左边没有超过 5 的元素，arr[3] = 0 有效。
> ans[4] = 2。由于{4，3，5}位于其左侧，超过 2，arr[4] = 3 有效。
> 
> **输入:** arr[] = {0，1，2}
> **输出:** 3 2 1

**天真方法:**最简单的方法是[生成 **N** 数的所有排列](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)，对于每个排列，检查其元素是否满足数组**arr【】**给出的逆。如果找到这样的排列，打印出来。

***时间复杂度:** O(N！)*
***辅助空间:** O(N)*

**高效方法:**优化上述方法，思路是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。按照以下步骤解决问题:

1.  构建一个大小为 **N** 的段树，并用值 **1** 初始化所有叶节点。
2.  [从右向左遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。例如，如果当前索引为**N–1**，即没有访问任何元素。因此， **arr[i]** 是元素的数量，应该大于必须在这个位置的元素。因此，这个元素的答案是段树中的**(N–arr[N–1])<sup>第</sup>** 个元素对应于那个元素。之后，将该元素标记为 **0** 以避免其再次计数。
3.  同样，对于从**(N–1)**到 **0** 的每个 **i** ，在段树中找到**(I+1–arr[I])<sup>第</sup>** 个元素。
4.  找到**arr【I】**的答案后，让它为 **temp** ，将其存储在某个数组**ans【】**中，并用 **0** 更新索引为 **temp** 的节点。
5.  最后，将答案数组 **ans[]** 按照与原排列相反的顺序打印出来。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
const int MAXX = 100;

// Declaring segment tree
int st[4 * MAXX];

// Function to initialize segment tree
// with leaves filled with ones
void build(int x, int lx, int rx)
{
    // Base Case
    if (rx - lx == 1) {
        st[x] = 1;
        return;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Build the left subtree
    build(x * 2 + 1, lx, m);

    // Build the right subtree
    build(x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1]
            + st[x * 2 + 2];

    return;
}

// Function to make index x to 0
// and then update segment tree
void update(int i, int x,
            int lx, int rx)
{
    // Base Case
    if (rx - lx == 1) {
        st[x] = 0;
        return;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Update Query
    if (i < m)
        update(i, x * 2 + 1, lx, m);
    else
        update(i, x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1]
            + st[x * 2 + 2];

    return;
}

// Function to find the Kth element
int getans(int x, int lx, int rx,
           int k, int n)
{
    // Base Condition
    if (rx - lx == 1) {
        if (st[x] == k)
            return lx;
        return n;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Check if kth one is in left subtree
    // or right subtree of current node
    if (st[x * 2 + 1] >= k)
        return getans(x * 2 + 1,
                      lx, m, k, n);
    else
        return getans(x * 2 + 2, m,
                      rx, k - st[x * 2 + 1],
                      n);
}

// Function to generate the original
// permutation
void getPermutation(int inv[], int n)
{
    // Build segment tree
    build(0, 0, n);

    // Stores the original permutation
    vector<int> ans;

    for (int i = n - 1; i >= 0; i--) {

        // Find kth one
        int temp = getans(0, 0, n,
                          st[0] - inv[i], n);

        // Answer for arr[i]
        ans.push_back(temp + 1);

        // Setting found value back to 0
        update(max(0, temp), 0, 0, n);
    }

    // Print the permutation
    for (int i = n - 1; i >= 0; i--)
        cout << ans[i] << " ";

    return;
}

// Driver Code
int main()
{
    // Given array
    int inv[] = { 0, 1, 1, 0, 3 };

    // Length of the given array
    int N = sizeof(inv) / sizeof(inv[0]);

    // Function Call
    getPermutation(inv, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int MAXX = 100;

// Declaring segment tree
static int []st = new int[4 * MAXX];

// Function to initialize segment tree
// with leaves filled with ones
static void build(int x, int lx, int rx)
{

    // Base Case
    if (rx - lx == 1)
    {
        st[x] = 1;
        return;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Build the left subtree
    build(x * 2 + 1, lx, m);

    // Build the right subtree
    build(x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2];

    return;
}

// Function to make index x to 0
// and then update segment tree
static void update(int i, int x,
                   int lx, int rx)
{

    // Base Case
    if (rx - lx == 1)
    {
        st[x] = 0;
        return;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Update Query
    if (i < m)
        update(i, x * 2 + 1, lx, m);
    else
        update(i, x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2];

    return;
}

// Function to find the Kth element
static int getans(int x, int lx, int rx,
                  int k, int n)
{

    // Base Condition
    if (rx - lx == 1)
    {
        if (st[x] == k)
            return lx;

        return n;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Check if kth one is in left subtree
    // or right subtree of current node
    if (st[x * 2 + 1] >= k)
        return getans(x * 2 + 1,
                      lx, m, k, n);
    else
        return getans(x * 2 + 2, m, rx,
               k - st[x * 2 + 1], n);
}

// Function to generate the original
// permutation
static void getPermutation(int inv[], int n)
{

    // Build segment tree
    build(0, 0, n);

    // Stores the original permutation
    Vector<Integer> ans = new Vector<Integer>();

    for(int i = n - 1; i >= 0; i--)
    {

        // Find kth one
        int temp = getans(0, 0, n,
                          st[0] - inv[i], n);

        // Answer for arr[i]
        ans.add(temp + 1);

        // Setting found value back to 0
        update(Math.max(0, temp), 0, 0, n);
    }

    // Print the permutation
    for(int i = n - 1; i >= 0; i--)
        System.out.print(ans.get(i) + " ");

    return;
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int inv[] = { 0, 1, 1, 0, 3 };

    // Length of the given array
    int N = inv.length;

    // Function Call
    getPermutation(inv, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAXX = 100

# Declaring segment tree
st = [0] * (4 * MAXX)

# Function to initialize segment tree
# with leaves filled with ones
def build(x, lx, rx):

    # Base Case
    if (rx - lx == 1):
        st[x] = 1
        return

    # Split into two halves
    m = (lx + rx) // 2

    # Build the left subtree
    build(x * 2 + 1, lx, m)

    # Build the right subtree
    build(x * 2 + 2, m, rx)

    # Combining both left and right
    # subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2]

    return

# Function to make index x to 0
# and then update segment tree
def update(i, x, lx, rx):

    # Base Case
    if (rx - lx == 1):
        st[x] = 0
        return

    # Split into two halves
    m = (lx + rx) // 2

    # Update Query
    if (i < m):
        update(i, x * 2 + 1, lx, m)
    else:
        update(i, x * 2 + 2, m, rx)

    # Combining both left and right
    # subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2]

    return

# Function to find the Kth element
def getans(x, lx, rx, k, n):

    # Base Condition
    if (rx - lx == 1):
        if (st[x] == k):
            return lx

        return n

    # Split into two halves
    m = (lx + rx) // 2

    # Check if kth one is in left subtree
    # or right subtree of current node
    if (st[x * 2 + 1] >= k):
        return getans(x * 2 + 1, lx, m, k, n)
    else:
        return getans(x * 2 + 2, m, rx,
               k - st[x * 2 + 1], n)

# Function to generate the original
# permutation
def getPermutation(inv, n):

    # Build segment tree
    build(0, 0, n)

    # Stores the original permutation
    ans = []

    for i in range(n - 1, -1, -1):

        # Find kth one
        temp = getans(0, 0, n, st[0] - inv[i], n)

        # Answer for arr[i]
        ans.append(temp + 1)

        # Setting found value back to 0
        update(max(0, temp), 0, 0, n)

    # Print the permutation
    for i in range(n - 1, -1, -1):
        print(ans[i], end = " ")

    return

# Driver Code
if __name__ == '__main__':

    # Given array
    inv = [ 0, 1, 1, 0, 3 ]

    # Length of the given array
    N = len(inv)

    # Function Call
    getPermutation(inv, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int MAXX = 100;

// Declaring segment tree
static int []st = new int[4 * MAXX];

// Function to initialize segment tree
// with leaves filled with ones
static void build(int x, int lx, int rx)
{

    // Base Case
    if (rx - lx == 1)
    {
        st[x] = 1;
        return;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Build the left subtree
    build(x * 2 + 1, lx, m);

    // Build the right subtree
    build(x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2];

    return;
}

// Function to make index x to 0
// and then update segment tree
static void update(int i, int x,
                   int lx, int rx)
{

    // Base Case
    if (rx - lx == 1)
    {
        st[x] = 0;
        return;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Update Query
    if (i < m)
        update(i, x * 2 + 1, lx, m);
    else
        update(i, x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2];

    return;
}

// Function to find the Kth element
static int getans(int x, int lx, int rx,
                  int k, int n)
{

    // Base Condition
    if (rx - lx == 1)
    {
        if (st[x] == k)
            return lx;

        return n;
    }

    // Split into two halves
    int m = (lx + rx) / 2;

    // Check if kth one is in left subtree
    // or right subtree of current node
    if (st[x * 2 + 1] >= k)
        return getans(x * 2 + 1,
                      lx, m, k, n);
    else
        return getans(x * 2 + 2, m, rx,
               k - st[x * 2 + 1], n);
}

// Function to generate the original
// permutation
static void getPermutation(int []inv, int n)
{

    // Build segment tree
    build(0, 0, n);

    // Stores the original permutation
    List<int> ans = new List<int>();

    for(int i = n - 1; i >= 0; i--)
    {

        // Find kth one
        int temp = getans(0, 0, n,
                          st[0] - inv[i], n);

        // Answer for arr[i]
        ans.Add(temp + 1);

        // Setting found value back to 0
        update(Math.Max(0, temp), 0, 0, n);
    }

    // Print the permutation
    for(int i = n - 1; i >= 0; i--)
        Console.Write(ans[i] + " ");

    return;
}

// Driver Code
public static void Main(String []args)
{

    // Given array
    int []inv = { 0, 1, 1, 0, 3 };

    // Length of the given array
    int N = inv.Length;

    // Function Call
    getPermutation(inv, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach
let MAXX = 100;

// Declaring segment tree
let st = new Array(4 * MAXX);

// Function to initialize segment tree
// with leaves filled with ones
function build(x, lx, rx)
{

    // Base Case
    if (rx - lx == 1)
    {
        st[x] = 1;
        return;
    }

    // Split into two halves
    let m = parseInt((lx + rx) / 2, 10);

    // Build the left subtree
    build(x * 2 + 1, lx, m);

    // Build the right subtree
    build(x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2];

    return;
}

// Function to make index x to 0
// and then update segment tree
function update(i, x, lx, rx)
{

    // Base Case
    if (rx - lx == 1)
    {
        st[x] = 0;
        return;
    }

    // Split into two halves
    let m = parseInt((lx + rx) / 2, 10);

    // Update Query
    if (i < m)
        update(i, x * 2 + 1, lx, m);
    else
        update(i, x * 2 + 2, m, rx);

    // Combining both left and right
    // subtree to parent node
    st[x] = st[x * 2 + 1] + st[x * 2 + 2];

    return;
}

// Function to find the Kth element
function getans(x, lx, rx, k, n)
{

    // Base Condition
    if (rx - lx == 1)
    {
        if (st[x] == k)
            return lx;

        return n;
    }

    // Split into two halves
    let m = parseInt((lx + rx) / 2, 10);

    // Check if kth one is in left subtree
    // or right subtree of current node
    if (st[x * 2 + 1] >= k)
        return getans(x * 2 + 1, lx, m, k, n);
    else
        return getans(x * 2 + 2, m, rx,
               k - st[x * 2 + 1], n);
}

// Function to generate the original
// permutation
function getPermutation(inv, n)
{

    // Build segment tree
    build(0, 0, n);

    // Stores the original permutation
    let ans = [];

    for(let i = n - 1; i >= 0; i--)
    {

        // Find kth one
        let temp = getans(0, 0, n,
                          st[0] - inv[i], n);

        // Answer for arr[i]
        ans.push(temp + 1);

        // Setting found value back to 0
        update(Math.max(0, temp), 0, 0, n);
    }

    // Print the permutation
    for(let i = n - 1; i >= 0; i--)
        document.write(ans[i] + " ");

    return;
}

// Driver code

// Given array
let inv = [ 0, 1, 1, 0, 3 ];

// Length of the given array
let N = inv.length;

// Function Call
getPermutation(inv, N);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
4 1 3 5 2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*