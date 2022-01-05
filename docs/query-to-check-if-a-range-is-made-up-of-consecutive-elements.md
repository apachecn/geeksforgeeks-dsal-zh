# 查询一个范围是否由连续的元素组成

> 原文:[https://www . geeksforgeeks . org/query-to-check-a-range-is-由连续元素组成/](https://www.geeksforgeeks.org/query-to-check-if-a-range-is-made-up-of-consecutive-elements/)

给定一个由 **n** 个非连续整数和 **Q** 个查询组成的数组，任务是检查对于给定的范围 **l** 和 **r** ，元素是否连续。
**举例:**

> **输入:** arr = { 2，4，3，7，6，1}，Q = { (1，3)，(3，5)，(5，6) }
> **输出:**是，否，否
> **解释:**数组元素来自(1，3) = {2，4，3}，(3，5) = {3，7，6}，(5，6) = {6，1}
> 所以答案是，否，否
> **输入**

**天真方法:**
范围 **l** 和 **r** 之间的子数组可以排序检查是否包含连续元素。
**时间复杂度:** O(q*n*log n)
其中 n 为数组大小，q 为查询次数。
**高效方法:**

1.  一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)可以用来得到一个范围内的最小值和最大值。
2.  如果一个子数组的最小元素是 x，最大元素是 y，那么我们可以说没有小于 x 大于 y 的元素，所以我们可以说 **x < =arr[i] < =y** 。
3.  由于没有重复的元素，因此可以得出结论，如果最大和最小元素+ 1 的差等于范围的长度(r-l+1)，则该范围由连续的元素组成。

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;

// Segment tree
int tree_min[1000001],
    tree_max[1000001];

// Functions to return
// minimum and maximum
int min(int a, int b)
{
    return a < b ? a : b;
}

int max(int a, int b)
{
    return a > b ? a : b;
}

// Segment tree for minimum element
void build_min(int array[], int node,
               int left, int right)
{
    // If left is equal to right
    if (left == right)
        tree_min[node] = array[left];

    else {
        // Divide the segment into equal halves
        build_min(array, 2 * node, left,
                  (left + right) / 2);

        build_min(array, 2 * node + 1,
                  (left + right) / 2 + 1, right);

        // Update the element as minimum
        // of the divided two subarrays
        tree_min[node] = min(tree_min[2 * node],
                             tree_min[2 * node + 1]);
    }
}

// Query to find a minimum
// in a given ranges
int query_min(int node, int c_l,
              int c_r, int l, int r)
{
    // Out of range
    if (c_l > r || c_r < l)
        return 1e9;

    // Within the range completely
    if (c_l >= l && c_r <= r)
        return tree_min[node];
    else
        // Divide the range into two halves
        // Query for each half
        // and return the minimum of two
        return min(query_min(2 * node, c_l,
                             (c_l + c_r) / 2, l, r),
                   query_min(2 * node + 1,
                             (c_l + c_r) / 2 + 1,
                             c_r, l, r));
}

// Segment tree for maximum element
void build_max(int array[], int node,
               int left, int right)
{
    // If left is equal to right
    if (left == right)
        tree_max[node] = array[left];

    else {
        // Divide the segment into equal halves
        build_max(array, 2 * node, left,
                  (left + right) / 2);

        build_max(array, 2 * node + 1,
                  (left + right) / 2 + 1, right);

        // Update the element as maximum
        // of the divided two subarrays
        tree_max[node] = max(tree_max[2 * node],
                             tree_max[2 * node + 1]);
    }
}

// Query to find maximum
// in a given ranges
int query_max(int node, int c_l,
              int c_r, int l, int r)
{
    // Out of range
    if (c_l > r || c_r < l)
        return -1;

    // Within the range completely
    if (c_l >= l && c_r <= r)
        return tree_max[node];
    else
        // Divide the range into two halves
        // and query for each half
        // and return the maximum of two
        return max(query_max(2 * node, c_l,
                             (c_l + c_r) / 2, l, r),
                   query_max(2 * node + 1,
                             (c_l + c_r) / 2 + 1,
                             c_r, l, r));
}

// Build the tree
void init(int array[], int n)
{
    build_min(array, 1, 0, n - 1);
    build_max(array, 1, 0, n - 1);
}

// Check if the given range is Consecutive
bool isConsecutive(int x, int y, int n)
{
    return ((query_max(1, 0, n - 1, x, y)
             - query_min(1, 0, n - 1, x, y))
            == (y - x));
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 3, 7, 6, 1 };
    int query[][2] = { { 1, 3 }, { 3, 5 }, { 5, 6 } };
    int n = sizeof(arr) / sizeof(int), q = 3;
    init(arr, n);

    for (int i = 0; i < q; i++) {
        int l, r;
        l = query[i][0];
        r = query[i][1];

        cout << (isConsecutive(l - 1, r - 1, n) ?
                           "Yes" : "No") << "\n";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

    // Segment tree
    static int[] tree_min = new int[1000001];
    static int[] tree_max = new int[1000001];

    // Functions to return
    // minimum and maximum
    static int min(int a, int b)
    {
        return a < b ? a : b;
    }

    static int max(int a, int b)
    {
        return a > b ? a : b;
    }

    // Segment tree for minimum element
    static void build_min(int array[], int node, int left, int right)
    {
        // If left is equal to right
        if (left == right)
            tree_min[node] = array[left];

        else
        {
            // Divide the segment into equal halves
            build_min(array, 2 * node, left, (left + right) / 2);

            build_min(array, 2 * node + 1,
                    (left + right) / 2 + 1, right);

            // Update the element as minimum
            // of the divided two subarrays
            tree_min[node] = Math.min(tree_min[2 * node],
                    tree_min[2 * node + 1]);
        }
    }

    // Query to find a minimum
    // in a given ranges
    static int query_min(int node, int c_l, int c_r, int l, int r)
    {
        // Out of range
        if (c_l > r || c_r < l)
            return (int) 1e9;

        // Within the range completely
        if (c_l >= l && c_r <= r)
            return tree_min[node];
        else
            // Divide the range into two halves
            // Query for each half
            // and return the minimum of two
            return min(query_min(2 * node, c_l, (c_l + c_r) / 2, l, r),
                    query_min(2 * node + 1, (c_l + c_r) / 2 + 1, c_r, l, r));
    }

    // Segment tree for maximum element
    static void build_max(int array[], int node, int left, int right)
    {
        // If left is equal to right
        if (left == right)
            tree_max[node] = array[left];

        else
        {
            // Divide the segment into equal halves
            build_max(array, 2 * node, left, (left + right) / 2);

            build_max(array, 2 * node + 1, (left + right) / 2 + 1, right);

            // Update the element as maximum
            // of the divided two subarrays
            tree_max[node] = Math.max(tree_max[2 * node],
                    tree_max[2 * node + 1]);
        }
    }

    // Query to find maximum
    // in a given ranges
    static int query_max(int node, int c_l, int c_r, int l, int r)
    {
        // Out of range
        if (c_l > r || c_r < l)
            return -1;

        // Within the range completely
        if (c_l >= l && c_r <= r)
            return tree_max[node];
        else
            // Divide the range into two halves
            // and query for each half
            // and return the maximum of two
            return Math.max(query_max(2 * node, c_l, (c_l + c_r) / 2, l, r),
                    query_max(2 * node + 1, (c_l + c_r) / 2 + 1, c_r, l, r));
    }

    // Build the tree
    static void init(int array[], int n)
    {
        build_min(array, 1, 0, n - 1);
        build_max(array, 1, 0, n - 1);
    }

    // Check if the given range is Consecutive
    static boolean isConsecutive(int x, int y, int n)
    {
        return ((query_max(1, 0, n - 1, x, y) -
                query_min(1, 0, n - 1, x, y)) == (y - x));
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 4, 3, 7, 6, 1 };
        int query[][] = { { 1, 3 }, { 3, 5 }, { 5, 6 } };
        int n = arr.length, q = 3;
        init(arr, n);

        for (int i = 0; i < q; i++)
        {
            int l, r;
            l = query[i][0];
            r = query[i][1];

            System.out.print((isConsecutive(l - 1, r - 1, n) ?
                    "Yes" : "No") + "\n");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python3 implementation of the above approach.

# Segment tree
tree_min = [0] * 1000001

tree_max = [0] * 1000001

# Segment tree for minimum element
def build_min(array, node,left, right):

    # If left is equal to right
    if (left == right):
        tree_min[node] = array[left]

    else :
        # Divide the segment into equal halves
        build_min(array, 2 * node, left,(left + right) // 2)

        build_min(array, 2 * node + 1,(left + right) // 2 + 1, right)

        # Update the element as minimum
        # of the divided two subarrays
        tree_min[node] = min(tree_min[2 * node], tree_min[2 * node + 1])

# Query to find a minimum
# in a given ranges
def query_min(node, c_l, c_r, l, r):

    # Out of range
    if (c_l > r or c_r < l):
        return 10**9

    # Within the range completely
    if (c_l >= l and c_r <= r):
        return tree_min[node]
    else:
        # Divide the range into two halves
        # Query for each half
        # and return the minimum of two
        return min(query_min(2 * node, c_l,(c_l + c_r) // 2, l, r),
                query_min(2 * node + 1, (c_l + c_r) // 2 + 1,c_r, l, r))

# Segment tree for maximum element
def build_max(array, node, left, right):

    # If left is equal to right
    if (left == right):
        tree_max[node] = array[left]

    else :
        # Divide the segment into equal halves
        build_max(array, 2 * node, left,(left + right) // 2)

        build_max(array, 2 * node + 1,(left + right) // 2 + 1, right)

        # Update the element as maximum
        # of the divided two subarrays
        tree_max[node] = max(tree_max[2 * node],tree_max[2 * node + 1])

# Query to find maximum
# in a given ranges
def query_max(node, c_l, c_r, l, r):

    # Out of range
    if (c_l > r or c_r < l):
        return -1

    # Within the range completely
    if (c_l >= l and c_r <= r):
        return tree_max[node]
    else:
        # Divide the range into two halves
        # and query for each half
        # and return the maximum of two
        return max(query_max(2 * node, c_l,(c_l + c_r) // 2, l, r),query_max(2 * node + 1,(c_l + c_r) // 2 + 1,c_r, l, r))

# Build the tree
def init(array, n):

    build_min(array, 1, 0, n - 1)
    build_max(array, 1, 0, n - 1)

# Check if the given range is Consecutive
def isConsecutive(x, y, n):

    return ((query_max(1, 0, n - 1, x, y) - query_min(1, 0, n - 1, x, y)) == (y - x))

# Driver code

arr = [2, 4, 3, 7, 6, 1]
query = [ [1, 3] , [3, 5 ], [5, 6] ]
n = len(arr)
q = 3
init(arr, n)

for i in range(q):
    l = query[i][0]
    r = query[i][1]

    if (isConsecutive(l - 1, r - 1, n) ):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

    // Segment tree
    static int[] tree_min = new int[1000001];
    static int[] tree_max = new int[1000001];

    // Functions to return
    // minimum and maximum
    static int min(int a, int b)
    {
        return a < b ? a : b;
    }

    static int max(int a, int b)
    {
        return a > b ? a : b;
    }

    // Segment tree for minimum element
    static void build_min(int []array, int node,
                           int left, int right)
    {
        // If left is equal to right
        if (left == right)
            tree_min[node] = array[left];

        else
        {
            // Divide the segment into equal halves
            build_min(array, 2 * node, left, (left + right) / 2);

            build_min(array, 2 * node + 1,
                    (left + right) / 2 + 1, right);

            // Update the element as minimum
            // of the divided two subarrays
            tree_min[node] = Math.Min(tree_min[2 * node],
                    tree_min[2 * node + 1]);
        }
    }

    // Query to find a minimum
    // in a given ranges
    static int query_min(int node, int c_l,
                        int c_r, int l, int r)
    {
        // Out of range
        if (c_l > r || c_r < l)
            return (int) 1e9;

        // Within the range completely
        if (c_l >= l && c_r <= r)
            return tree_min[node];
        else
            // Divide the range into two halves
            // Query for each half
            // and return the minimum of two
            return min(query_min(2 * node, c_l,
                        (c_l + c_r) / 2, l, r),
                        query_min(2 * node + 1,
                        (c_l + c_r) / 2 + 1, c_r, l, r));
    }

    // Segment tree for maximum element
    static void build_max(int []array, int node,
                           int left, int right)
    {
        // If left is equal to right
        if (left == right)
            tree_max[node] = array[left];

        else
        {
            // Divide the segment into equal halves
            build_max(array, 2 * node, left, (left + right) / 2);

            build_max(array, 2 * node + 1, (left + right) / 2 + 1, right);

            // Update the element as maximum
            // of the divided two subarrays
            tree_max[node] = Math.Max(tree_max[2 * node],
                    tree_max[2 * node + 1]);
        }
    }

    // Query to find maximum
    // in a given ranges
    static int query_max(int node, int c_l,
                        int c_r, int l, int r)
    {
        // Out of range
        if (c_l > r || c_r < l)
            return -1;

        // Within the range completely
        if (c_l >= l && c_r <= r)
            return tree_max[node];
        else
            // Divide the range into two halves
            // and query for each half
            // and return the maximum of two
            return Math.Max(query_max(2 * node, c_l,
                            (c_l + c_r) / 2, l, r),
                            query_max(2 * node + 1,
                            (c_l + c_r) / 2 + 1, c_r, l, r));
    }

    // Build the tree
    static void init(int []array, int n)
    {
        build_min(array, 1, 0, n - 1);
        build_max(array, 1, 0, n - 1);
    }

    // Check if the given range is Consecutive
    static bool isConsecutive(int x, int y, int n)
    {
        return ((query_max(1, 0, n - 1, x, y) -
                query_min(1, 0, n - 1, x, y)) == (y - x));
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 4, 3, 7, 6, 1};
        int [,]query = {{ 1, 3 }, { 3, 5 }, { 5, 6 }};
        int n = arr.Length, q = 3;
        init(arr, n);

        for (int i = 0; i < q; i++)
        {
            int l, r;
            l = query[i,0];
            r = query[i,1];

            Console.Write((isConsecutive(l - 1, r - 1, n) ?
                    "Yes" : "No") + "\n");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach.

// Segment tree
let  tree_min = new Array(1000001);
let tree_max = new Array(1000001);

// Functions to return
// minimum and maximum
function min(a,b)
{
    return a < b ? a : b;
}

function max(a,b)
{
    return a > b ? a : b;
}

// Segment tree for minimum element
function build_min(array,node,left,right)
{
    // If left is equal to right
        if (left == right)
            tree_min[node] = array[left];

        else
        {
            // Divide the segment into equal halves
            build_min(array, 2 * node, left,
            Math.floor((left + right) / 2));

            build_min(array, 2 * node + 1,
                    Math.floor((left + right) / 2) + 1, right);

            // Update the element as minimum
            // of the divided two subarrays
            tree_min[node] = Math.min(tree_min[2 * node],
                    tree_min[2 * node + 1]);
        }
}

// Query to find a minimum
// in a given ranges
function query_min(node,c_l,c_r,l,r)
{
    // Out of range
        if (c_l > r || c_r < l)
            return 1e9;

        // Within the range completely
        if (c_l >= l && c_r <= r)
            return tree_min[node];
        else
            // Divide the range into two halves
            // Query for each half
            // and return the minimum of two
            return min(query_min(2 * node, c_l,
            Math.floor((c_l + c_r) / 2), l, r),
            query_min(2 * node + 1,
            Math.floor((c_l + c_r) / 2) + 1, c_r, l, r));
}

// Segment tree for maximum element
function build_max(array,node,left,right)
{
    // If left is equal to right
        if (left == right)
            tree_max[node] = array[left];

        else
        {
            // Divide the segment into equal halves
            build_max(array, 2 * node, left,
            Math.floor((left + right) / 2));

            build_max(array, 2 * node + 1,
            Math.floor((left + right) / 2) + 1, right);

            // Update the element as maximum
            // of the divided two subarrays
            tree_max[node] = Math.max(tree_max[2 * node],
                    tree_max[2 * node + 1]);
        }
}

 // Query to find maximum
 // in a given ranges
function query_max(node,c_l,c_r,l,r)
{
    // Out of range
        if (c_l > r || c_r < l)
            return -1;

        // Within the range completely
        if (c_l >= l && c_r <= r)
            return tree_max[node];
        else
            // Divide the range into two halves
            // and query for each half
            // and return the maximum of two
            return Math.max(query_max(2 * node, c_l,
            Math.floor((c_l + c_r) / 2), l, r),
            query_max(2 * node + 1,
            Math.floor((c_l + c_r) / 2) + 1, c_r, l, r));
}

// Build the tree
function init(array,n)
{
    build_min(array, 1, 0, n - 1);
        build_max(array, 1, 0, n - 1);
}

// Check if the given range is Consecutive
function isConsecutive(x,y,n)
{
    return ((query_max(1, 0, n - 1, x, y) -
                query_min(1, 0, n - 1, x, y)) == (y - x));
}

// Driver code
let arr=[ 2, 4, 3, 7, 6, 1];
let query=[[ 1, 3 ], [ 3, 5 ], [ 5, 6 ] ];
let n = arr.length, q = 3;
init(arr, n);
for (let i = 0; i < q; i++)
        {
            let l, r;
            l = query[i][0];
            r = query[i][1];

            document.write((isConsecutive(l - 1, r - 1, n) ?
                    "Yes" : "No") + "<br>");
        }

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Yes
No
No
```

**时间复杂度:** O(Q*log(n))