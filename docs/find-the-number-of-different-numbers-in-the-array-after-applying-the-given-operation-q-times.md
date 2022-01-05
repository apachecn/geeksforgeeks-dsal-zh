# 应用给定的操作 q 次后求数组中不同数字的个数

> 原文:[https://www . geeksforgeeks . org/find-应用给定操作后数组中不同数字的数量-q-times/](https://www.geeksforgeeks.org/find-the-number-of-different-numbers-in-the-array-after-applying-the-given-operation-q-times/)

给定一个大小为 N 的数组，最初只由零组成。任务是应用给定的操作 q 次，找出数组中除零以外的不同数字的个数。
**操作格式:更新(l，r，x)::** 更新 a[i] = x 为所有(l < = i < = r)。

**示例:**

> **输入:** N = 5，Q = 3，
> 更新(1，3，1)
> 更新(0，1，2)
> 更新(3，3，3)
> T6】输出:3
> T9】说明:初始数组为{0，0，0，0，0}。
> 第一次应用操作后，数组变成{0，1，1，1，0}。
> 第二次操作后，数组变为
> {2，2，1，1，0}。第三次操作后，数组
> 变为{2，2，1，3，0}。所以，许多不同的数字除了零都是 3。
> 
> **输入:** N = 5，Q = 3，
> 更新(1，1，4)
> 更新(0，1，2)
> 更新(1，4，5)
> T6】输出: 2

**进场:**
每次操作建议范围更新，遂尝试使用[懒传播](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)更新阵位。在使用惰性传播应用操作 Q 次后，调用一个函数，该函数查找数组中不同数字的数量。这个函数使用 set 来查找不同数字的计数。
更新和查询操作类似于[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)中的操作，但有一些变化。每当在段树中执行更新查询时，与当前节点相关联的所有节点也被更新，而在惰性传播中，这些节点将仅在需要时被更新，即，我们创建大小等于给定数组的数组**惰性[]** ，其所有元素将被初始化为 **0** ，这意味着任何节点最初都没有更新，并且在**惰性[i]** 处的任何非零值指示节点 **i** 具有仅将被更新的未决更新

下面是上述方法的实现:

## C++

```
// CPP implementation for above approach
#include <bits/stdc++.h>
using namespace std;

#define N 100005

// To store the tree in lazy propagation
int lazy[4 * N];

// To store the different numbers
set<int> se;

// Function to update in the range [x, y) with given value
void update(int x, int y, int value, int id, int l, int r)
{
    // check out of bound
    if (x >= r or l >= y)
        return;

    // check for complete overlap
    if (x <= l && r <= y) {
        lazy[id] = value;
        return;
    }

    // find the mid number
    int mid = (l + r) / 2;

    // check for pending updates
    if (lazy[id])
        lazy[2 * id] = lazy[2 * id + 1] = lazy[id];

    // make lazy[id] = 0, so that it has no pending updates
    lazy[id] = 0;

    // call for two child nodes
    update(x, y, value, 2 * id, l, mid);
    update(x, y, value, 2 * id + 1, mid, r);
}

// Function to find non-zero integers in the range [l, r)
void query(int id, int l, int r)
{
    // if id contains positive number
    if (lazy[id]) {
        se.insert(lazy[id]);
        // There is no need to see the children,
        // because all the interval have same number
        return;
    }

    // check for out of bound
    if (r - l < 2)
        return;

    // find the middle number
    int mid = (l + r) / 2;

    // call for two child nodes
    query(2 * id, l, mid);
    query(2 * id + 1, mid, r);
}

// Driver code
int main()
{
    // size of the array and number of queries
    int n = 5, q = 3;

    // Update operation for l, r, x, id, 0, n
    update(1, 4, 1, 1, 0, n);
    update(0, 2, 2, 1, 0, n);
    update(3, 4, 3, 1, 0, n);

    // Query operation to get answer in the range [0, n-1]
    query(1, 0, n);

    // Print the count of non-zero elements
    cout << se.size() << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
import java.util.*;

class geeks
{

    static int N = 100005;

    // To store the tree in lazy propagation
    static int[] lazy = new int[4*N];

    // To store the different numbers
    static Set<Integer> se = new HashSet<Integer>();

    // Function to update in the range [x, y) with given value
    public static void update(int x, int y, int value,
                            int id, int l, int r)
    {

        // check out of bound
        if (x >= r || l >= y)
            return;

        // check for complete overlap
        if (x <= l && r <= y)
        {
            lazy[id] = value;
            return;
        }

        // find the mid number
        int mid = (l + r) / 2;

        // check for pending updates
        if (lazy[id] != 0)
            lazy[2 * id] = lazy[2 * id + 1] = lazy[id];

        // make lazy[id] = 0, so that it has no pending updates
        lazy[id] = 0;

        // call for two child nodes
        update(x, y, value, 2 * id, l, mid);
        update(x, y, value, 2 * id + 1, mid, r);
    }

    // Function to find non-zero integers in the range [l, r)
    public static void query(int id, int l, int r)
    {

        // if id contains positive number
        if (lazy[id] != 0)
        {
            se.add(lazy[id]);

            // There is no need to see the children,
            // because all the interval have same number
            return;
        }

        // check for out of bound
        if (r - l < 2)
            return;

        // find the middle number
        int mid = (l + r) / 2;

        // call for two child nodes
        query(2 * id, l, mid);
        query(2 * id + 1, mid, r);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // size of the array and number of queries
        int n = 5, q = 3;

        // Update operation for l, r, x, id, 0, n
        update(1, 4, 1, 1, 0, n);
        update(0, 2, 2, 1, 0, n);
        update(3, 4, 3, 1, 0, n);

        // Query operation to get answer in the range [0, n-1]
        query(1, 0, n);

        // Print the count of non-zero elements
        System.out.println(se.size());
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation for above approach
N = 100005

# To store the tree in lazy propagation
lazy = [0] * (4 * N);

# To store the different numbers
se = set()

# Function to update in the range [x, y)
# with given value
def update(x, y, value, id, l, r) :

    # check out of bound
    if (x >= r or l >= y):
        return;

    # check for complete overlap
    if (x <= l and r <= y) :
        lazy[id] = value;
        return;

    # find the mid number
    mid = (l + r) // 2;

    # check for pending updates
    if (lazy[id]) :
        lazy[2 * id] = lazy[2 * id + 1] = lazy[id];

    # make lazy[id] = 0,
    # so that it has no pending updates
    lazy[id] = 0;

    # call for two child nodes
    update(x, y, value, 2 * id, l, mid);
    update(x, y, value, 2 * id + 1, mid, r);

# Function to find non-zero integers
# in the range [l, r)
def query(id, l, r) :

    # if id contains positive number
    if (lazy[id]) :

        se.add(lazy[id]);

        # There is no need to see the children,
        # because all the interval have same number
        return;

    # check for out of bound
    if (r - l < 2) :
        return;

    # find the middle number
    mid = (l + r) // 2;

    # call for two child nodes
    query(2 * id, l, mid);
    query(2 * id + 1, mid, r);

# Driver code
if __name__ == "__main__" :

    # size of the array and number of queries
    n = 5; q = 3;

    # Update operation for l, r, x, id, 0, n
    update(1, 4, 1, 1, 0, n);
    update(0, 2, 2, 1, 0, n);
    update(3, 4, 3, 1, 0, n);

    # Query operation to get answer
    # in the range [0, n-1]
    query(1, 0, n);

    # Print the count of non-zero elements
    print(len(se));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation for above approach
using System;
using System.Collections.Generic;

public class geeks
{

    static int N = 100005;

    // To store the tree in lazy propagation
    static int[] lazy = new int[4*N];

    // To store the different numbers
    static HashSet<int> se = new HashSet<int>();

    // Function to update in the range [x, y) with given value
    public static void update(int x, int y, int value,
                            int id, int l, int r)
    {

        // check out of bound
        if (x >= r || l >= y)
            return;

        // check for complete overlap
        if (x <= l && r <= y)
        {
            lazy[id] = value;
            return;
        }

        // find the mid number
        int mid = (l + r) / 2;

        // check for pending updates
        if (lazy[id] != 0)
            lazy[2 * id] = lazy[2 * id + 1] = lazy[id];

        // make lazy[id] = 0, so that it has no pending updates
        lazy[id] = 0;

        // call for two child nodes
        update(x, y, value, 2 * id, l, mid);
        update(x, y, value, 2 * id + 1, mid, r);
    }

    // Function to find non-zero integers in the range [l, r)
    public static void query(int id, int l, int r)
    {

        // if id contains positive number
        if (lazy[id] != 0)
        {
            se.Add(lazy[id]);

            // There is no need to see the children,
            // because all the interval have same number
            return;
        }

        // check for out of bound
        if (r - l < 2)
            return;

        // find the middle number
        int mid = (l + r) / 2;

        // call for two child nodes
        query(2 * id, l, mid);
        query(2 * id + 1, mid, r);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // size of the array and number of queries
        int n = 5, q = 3;

        // Update operation for l, r, x, id, 0, n
        update(1, 4, 1, 1, 0, n);
        update(0, 2, 2, 1, 0, n);
        update(3, 4, 3, 1, 0, n);

        // Query operation to get answer in the range [0, n-1]
        query(1, 0, n);

        // Print the count of non-zero elements
        Console.WriteLine(se.Count);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation for above approach

var N = 100005;
// To store the tree in lazy propagation
var lazy = Array(4*N).fill(0);
// To store the different numbers
var se = new Set();
// Function to update in the range [x, y) with given value
function update(x, y, value, id, l, r)
{
    // check out of bound
    if (x >= r || l >= y)
        return;

    // check for complete overlap
    if (x <= l && r <= y)
    {
        lazy[id] = value;
        return;
    }

    // find the mid number
    var mid = parseInt((l + r) / 2);

    // check for pending updates
    if (lazy[id] != 0)
        lazy[2 * id] = lazy[2 * id + 1] = lazy[id];

    // make lazy[id] = 0, so that it has no pending updates
    lazy[id] = 0;

    // call for two child nodes
    update(x, y, value, 2 * id, l, mid);
    update(x, y, value, 2 * id + 1, mid, r);
}
// Function to find non-zero integers in the range [l, r)
function query(id, l, r)
{

    // if id contains positive number
    if (lazy[id] != 0)
    {
        se.add(lazy[id]);

        // There is no need to see the children,
        // because all the interval have same number
        return;
    }
    // check for out of bound
    if (r - l < 2)
        return;
    // find the middle number
    var mid = parseInt((l + r) / 2);
    // call for two child nodes
    query(2 * id, l, mid);
    query(2 * id + 1, mid, r);
}

// Driver Code
// size of the array and number of queries
var n = 5, q = 3;
// Update operation for l, r, x, id, 0, n
update(1, 4, 1, 1, 0, n);
update(0, 2, 2, 1, 0, n);
update(3, 4, 3, 1, 0, n);
// Query operation to get answer in the range [0, n-1]
query(1, 0, n);
// Print the count of non-zero elements
document.write(se.size);

</script>
```

**Output:** 

```
3
```