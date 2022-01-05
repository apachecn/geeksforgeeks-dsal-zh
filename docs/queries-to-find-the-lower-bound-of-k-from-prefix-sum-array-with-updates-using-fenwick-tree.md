# 使用分威克树从前缀和数组中查找 K 的下界的查询

> 原文:[https://www . geeksforgeeks . org/query-to-find-k-from-prefix-sum-array-with-updates-use-fenwick-tree/](https://www.geeksforgeeks.org/queries-to-find-the-lower-bound-of-k-from-prefix-sum-array-with-updates-using-fenwick-tree/)

给定一个由非负整数组成的数组 **A[ ]** 和一个由以下两种类型的查询组成的矩阵 **Q[ ][ ]** :

*   【T1，l，val】:更新**a【l】**至**a【l]+val**。
*   **(2，K):** 在 **A[ ]** 的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)中找到 **K** 的[下界](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)。如果下限不存在，打印-1。

第二种类型的每个查询的任务是打印值 **K** 的**下界**的索引。

**示例:**

> **输入:** A[ ] = {1，2，3，5，8}，Q[ ][ ] = {{1，0，2}，{2，5}，{1，3，5 } }
> T3】输出:1
> T6】解释:T8】查询 1:将 A[0]更新为 A[0] + 2。现在 A[ ] = {3，2，3，5，8}
> 查询 2:前缀和数组{3，5，8，13，21}中 K = 5 的下界为 5，索引= 1。
> 查询 3:将 A[3]更新为 A[3] + 5。现在 A[ ] = {3，2，3，10，8}
> 
> **输入:** A[ ] = {4，1，12，8，20}，Q[ ] = {{2，50}，{1，3，12}，{2，50 } }
> T3】输出: -1

**天真方法:**
最简单的方法是首先构建给定数组 A[ ]，对于**类型 1** 的查询，更新值并重新计算前缀和。对于**类型 2** 的查询，在前缀和数组上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来查找**下限**。

***时间复杂度:**O(Q *(N * logn))*
***辅助空间:** O(N)*

**高效途径:**
以上途径可以优化[分威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)。使用此[数据结构](https://www.geeksforgeeks.org/data-structures/)，前缀和数组中的更新查询可以在对数时间内执行。
按照以下步骤解决问题:

*   使用芬威克树构造[前缀和数组。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
*   对于**类型 1** 的查询，当 **l > 0** 时，通过在 **l** 中添加[最低有效位](https://www.geeksforgeeks.org/print-kth-least-significant-bit-number/)将**值**添加到**A【l】**遍历父节点。
*   对于**类型 2** 的查询，在分支树上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)以获得下限。
*   每当出现大于 **K** 的前缀和**，**存储该**索引**，并遍历分支树的左侧部分。否则，现在遍历分威克树的右边部分，执行**二分搜索法**。
*   最后，打印所需的索引。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and return
// the sum of arr[0..index]
int getSum(int BITree[], int index)
{
    int ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0)
    {

        // Update the sum of current
        // element of BIT to ans
        ans += BITree[index];

        // Update index to that
        // of the parent node in
        // getSum() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Function to update the Binary Index
// Tree by replacing all ancestors of
// index by their respective sum with val
static void updateBIT(int BITree[], int n,
                      int index, int val)
{
    index = index + 1;

    // Traverse all ancestors
    // and sum with 'val'.
    while (index <= n)
    {

        // Add 'val' to current
        // node of BIT
        BITree[index] += val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Function to construct the Binary
// Indexed Tree for the given array
int* constructBITree(int arr[], int n)
{

    // Initialize the
    // Binary Indexed Tree
    int* BITree = new int[n + 1];

    for(int i = 0; i <= n; i++)
        BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for(int i = 0; i < n; i++)
        updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

// Function to obtain and return
// the index of lower_bound of k
int getLowerBound(int BITree[], int arr[],
                  int n, int k)
{
    int lb = -1;
    int l = 0, r = n - 1;

    while (l <= r)
    {
        int mid = l + (r - l) / 2;
        if (getSum(BITree, mid) >= k)
        {
            r = mid - 1;
            lb = mid;
        }
        else
            l = mid + 1;
    }
    return lb;
}

void performQueries(int A[], int n, int q[][3])
{

    // Store the Binary Indexed Tree
    int* BITree = constructBITree(A, n);

    // Solve each query in Q
    for(int i = 0;
            i < sizeof(q[0]) / sizeof(int);
            i++)
    {
        int id = q[i][0];

        if (id == 1)
        {
            int idx = q[i][1];
            int val = q[i][2];
            A[idx] += val;

            // Update the values of all
            // ancestors of idx
            updateBIT(BITree, n, idx, val);
        }
        else
        {
            int k = q[i][1];
            int lb = getLowerBound(BITree,
                                   A, n, k);
            cout << lb << endl;
        }
    }
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3, 5, 8 };

    int n = sizeof(A) / sizeof(int);

    int q[][3] = { { 1, 0, 2 },
                   { 2, 5, 0 },
                   { 1, 3, 5 } };

    performQueries(A, n, q);
}

// This code is contributed by jrishabh99
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.io.*;

class GFG {

    // Function to calculate and return
    // the sum of arr[0..index]
    static int getSum(int BITree[],
                      int index)
    {
        int ans = 0;
        index += 1;

        // Traverse ancestors
        // of BITree[index]
        while (index > 0) {

            // Update the sum of current
            // element of BIT to ans
            ans += BITree[index];

            // Update index to that
            // of the parent node in
            // getSum() view by
            // subtracting LSB(Least
            // Significant Bit)
            index -= index & (-index);
        }
        return ans;
    }

    // Function to update the Binary Index
    // Tree by replacing all ancestors of
    // index by their respective sum with val
    static void updateBIT(int BITree[],
                          int n, int index, int val)
    {
        index = index + 1;

        // Traverse all ancestors
        // and sum with 'val'.
        while (index <= n) {
            // Add 'val' to current
            // node of BIT
            BITree[index] += val;

            // Update index to that
            // of the parent node in
            // updateBit() view by
            // adding LSB(Least
            // Significant Bit)
            index += index & (-index);
        }
    }

    // Function to construct the Binary
    // Indexed Tree for the given array
    static int[] constructBITree(
        int arr[], int n)
    {
        // Initialize the
        // Binary Indexed Tree
        int[] BITree = new int[n + 1];

        for (int i = 0; i <= n; i++)
            BITree[i] = 0;

        // Store the actual values in
        // BITree[] using update()
        for (int i = 0; i < n; i++)
            updateBIT(BITree, n, i, arr[i]);

        return BITree;
    }

    // Function to obtain and return
    // the index of lower_bound of k
    static int getLowerBound(int BITree[],
                             int[] arr, int n, int k)
    {
        int lb = -1;
        int l = 0, r = n - 1;

        while (l <= r) {

            int mid = l + (r - l) / 2;
            if (getSum(BITree, mid) >= k) {
                r = mid - 1;
                lb = mid;
            }
            else
                l = mid + 1;
        }
        return lb;
    }

    static void performQueries(int A[], int n, int q[][])
    {

        // Store the Binary Indexed Tree
        int[] BITree = constructBITree(A, n);

        // Solve each query in Q
        for (int i = 0; i < q.length; i++) {
            int id = q[i][0];

            if (id == 1) {
                int idx = q[i][1];
                int val = q[i][2];
                A[idx] += val;

                // Update the values of all
                // ancestors of idx
                updateBIT(BITree, n, idx, val);
            }
            else {
                int k = q[i][1];
                int lb = getLowerBound(
                    BITree, A, n, k);
                System.out.println(lb);
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 1, 2, 3, 5, 8 };

        int n = A.length;

        int[][] q = { { 1, 0, 2 },
                      { 2, 5 },
                      { 1, 3, 5 } };

        performQueries(A, n, q);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate and return
# the sum of arr[0..index]
def getSum(BITree, index):

    ans = 0
    index += 1

    # Traverse ancestors
    # of BITree[index]
    while (index > 0):

        # Update the sum of current
        # element of BIT to ans
        ans += BITree[index]

        # Update index to that
        # of the parent node in
        # getSum() view by
        # subtracting LSB(Least
        # Significant Bit)
        index -= index & (-index)

    return ans

# Function to update the
# Binary Index Tree by
# replacing all ancestors
# of index by their respective
# sum with val
def updateBIT(BITree, n,
              index, val):

    index = index + 1

    # Traverse all ancestors
    # and sum with 'val'.
    while (index <= n):

        # Add 'val' to current
        # node of BIT
        BITree[index] += val

        # Update index to that
        # of the parent node in
        # updateBit() view by
        # adding LSB(Least
        # Significant Bit)
        index += index & (-index)

# Function to construct the Binary
# Indexed Tree for the given array
def constructBITree(arr, n):

    # Initialize the
    # Binary Indexed Tree
    BITree = [0] * (n + 1)

    for i in range(n + 1):
        BITree[i] = 0

    # Store the actual values in
    # BITree[] using update()
    for i in range(n):
        updateBIT(BITree, n, i, arr[i])

    return BITree

# Function to obtain and return
# the index of lower_bound of k
def getLowerBound(BITree, arr,
                  n,  k):

    lb = -1
    l = 0
    r = n - 1

    while (l <= r):
        mid = l + (r - l) // 2
        if (getSum(BITree,
                   mid) >= k):
            r = mid - 1
            lb = mid
        else:
            l = mid + 1

    return lb

def performQueries(A, n, q):

    # Store the Binary Indexed Tree
    BITree = constructBITree(A, n)

    # Solve each query in Q
    for i in range(len(q)):
        id = q[i][0]

        if (id == 1):
            idx = q[i][1]
            val = q[i][2]
            A[idx] += val

            # Update the values of all
            # ancestors of idx
            updateBIT(BITree, n,
                      idx, val)
        else:

            k = q[i][1]
            lb = getLowerBound(BITree,
                               A, n, k)
            print(lb)

# Driver Code
if __name__ == "__main__":

    A = [1, 2, 3, 5, 8]
    n = len(A)
    q = [[1, 0, 2],
         [2, 5, 0],
         [1, 3, 5]]
    performQueries(A, n, q)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate and return
// the sum of arr[0..index]
static int getSum(int []BITree,
                  int index)
{
    int ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0)
    {

        // Update the sum of current
        // element of BIT to ans
        ans += BITree[index];

        // Update index to that
        // of the parent node in
        // getSum() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Function to update the Binary Index
// Tree by replacing all ancestors of
// index by their respective sum with val
static void updateBIT(int []BITree,
                      int n, int index,
                      int val)
{
    index = index + 1;

    // Traverse all ancestors
    // and sum with 'val'.
    while (index <= n)
    {

        // Add 'val' to current
        // node of BIT
        BITree[index] += val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Function to construct the Binary
// Indexed Tree for the given array
static int[] constructBITree(int []arr,
                             int n)
{
    // Initialize the
    // Binary Indexed Tree
    int[] BITree = new int[n + 1];

    for(int i = 0; i <= n; i++)
        BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for(int i = 0; i < n; i++)
        updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

// Function to obtain and return
// the index of lower_bound of k
static int getLowerBound(int []BITree,
                         int[] arr, int n,
                         int k)
{
    int lb = -1;
    int l = 0, r = n - 1;

    while (l <= r)
    {
        int mid = l + (r - l) / 2;
        if (getSum(BITree, mid) >= k)
        {
            r = mid - 1;
            lb = mid;
        }
        else
            l = mid + 1;
    }
    return lb;
}

static void performQueries(int []A, int n,
                           int [,]q)
{

    // Store the Binary Indexed Tree
    int[] BITree = constructBITree(A, n);

    // Solve each query in Q
    for(int i = 0; i < q.GetLength(0); i++)
    {
        int id = q[i, 0];

        if (id == 1)
        {
            int idx = q[i, 1];
            int val = q[i, 2];
            A[idx] += val;

            // Update the values of all
            // ancestors of idx
            updateBIT(BITree, n, idx, val);
        }
        else
        {
            int k = q[i, 1];
            int lb = getLowerBound(BITree,
                                   A, n, k);
            Console.WriteLine(lb);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 1, 2, 3, 5, 8 };

    int n = A.Length;

    int [,]q = { { 1, 0, 2 },
                 { 2, 5, 0 },
                 { 1, 3, 5 } };

    performQueries(A, n, q);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to calculate and return
// the sum of arr[0..index]
function getSum(BITree, index) {
    let ans = 0;
    index += 1;

    // Traverse ancestors
    // of BITree[index]
    while (index > 0) {

        // Update the sum of current
        // element of BIT to ans
        ans += BITree[index];

        // Update index to that
        // of the parent node in
        // getSum() view by
        // subtracting LSB(Least
        // Significant Bit)
        index -= index & (-index);
    }
    return ans;
}

// Function to update the Binary Index
// Tree by replacing all ancestors of
// index by their respective sum with val
function updateBIT(BITree, n, index, val) {
    index = index + 1;

    // Traverse all ancestors
    // and sum with 'val'.
    while (index <= n) {

        // Add 'val' to current
        // node of BIT
        BITree[index] += val;

        // Update index to that
        // of the parent node in
        // updateBit() view by
        // adding LSB(Least
        // Significant Bit)
        index += index & (-index);
    }
}

// Function to construct the Binary
// Indexed Tree for the given array
function constructBITree(arr, n) {

    // Initialize the
    // Binary Indexed Tree
    let BITree = new Array(n + 1);

    for (let i = 0; i <= n; i++)
        BITree[i] = 0;

    // Store the actual values in
    // BITree[] using update()
    for (let i = 0; i < n; i++)
        updateBIT(BITree, n, i, arr[i]);

    return BITree;
}

// Function to obtain and return
// the index of lower_bound of k
function getLowerBound(BITree, arr, n, k) {
    let lb = -1;
    let l = 0, r = n - 1;

    while (l <= r) {
        let mid = Math.floor(l + (r - l) / 2);
        if (getSum(BITree, mid) >= k) {
            r = mid - 1;
            lb = mid;
        }
        else
            l = mid + 1;
    }
    return lb;
}

function performQueries(A, n, q) {

    // Store the Binary Indexed Tree
    let BITree = constructBITree(A, n);

    // Solve each query in Q
    for (let i = 0;
        i < q.length;
        i++) {
        let id = q[i][0];

        if (id == 1) {
            let idx = q[i][1];
            let val = q[i][2];
            A[idx] += val;

            // Update the values of all
            // ancestors of idx
            updateBIT(BITree, n, idx, val);
        }
        else {
            let k = q[i][1];
            let lb = getLowerBound(BITree,
                A, n, k);
            document.write(lb + "<br>");
        }
    }
}

// Driver Code

let A = [1, 2, 3, 5, 8];

let n = A.length;

let q = [[1, 0, 2],
        [2, 5, 0],
        [1, 3, 5]];

performQueries(A, n, q);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(Q *(logN)<sup>2</sup>)*
***辅助空间:** O(N)*