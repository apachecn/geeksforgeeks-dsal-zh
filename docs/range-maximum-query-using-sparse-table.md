# 使用稀疏表查询最大范围

> 原文:[https://www . geesforgeks . org/range-maximum-query-use-sparse-table/](https://www.geeksforgeeks.org/range-maximum-query-using-sparse-table/)

给定一个数组 **arr[]** ，任务是回答查询以找到索引范围 **arr[L…R]** 中所有元素的最大值。
**例:**

```
Input: arr[] = {6, 7, 4, 5, 1, 3}, q[][] = {{0, 5}, {3, 5}, {2, 4}}
Output:
7
5
5

Input: arr[] = {3, 34, 1}, q[][] = {{1, 2}}
Output:
34
```

**方法:**回答范围最小查询的类似问题已经在[这里](https://www.geeksforgeeks.org/sparse-table/)讨论过了。可以修改相同的方法来回答最大范围查询。下面是修改:

```
// Maximum of single element subarrays is same
// as the only element
lookup[i][0] = arr[i]

// If lookup[0][2] ≥  lookup[4][2], 
// then lookup[0][3] = lookup[0][2]
If lookup[i][j-1] ≥ lookup[i+2j-1-1][j-1]
   lookup[i][j] = lookup[i][j-1]

// If lookup[0][2] <  lookup[4][2], 
// then lookup[0][3] = lookup[4][2]
Else 
   lookup[i][j] = lookup[i+2j-1-1][j-1] 
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 500

// lookup[i][j] is going to store maximum
// value in arr[i..j]. Ideally lookup table
// size should not be fixed and should be
// determined using n Log n. It is kept
// constant to keep code simple.
int lookup[MAX][MAX];

// Fills lookup array lookup[][] in bottom up manner
void buildSparseTable(int arr[], int n)
{
    // Initialize M for the intervals with length 1
    for (int i = 0; i < n; i++)
        lookup[i][0] = arr[i];

    // Compute values from smaller to bigger intervals
    for (int j = 1; (1 << j) <= n; j++) {

        // Compute maximum value for all intervals with
        // size 2^j
        for (int i = 0; (i + (1 << j) - 1) < n; i++) {

            // For arr[2][10], we compare arr[lookup[0][7]]
            // and arr[lookup[3][10]]
            if (lookup[i][j - 1] > lookup[i + (1 << (j - 1))][j - 1])
                lookup[i][j] = lookup[i][j - 1];
            else
                lookup[i][j] = lookup[i + (1 << (j - 1))][j - 1];
        }
    }
}

// Returns maximum of arr[L..R]
int query(int L, int R)
{
    // Find highest power of 2 that is smaller
    // than or equal to count of elements in given
    // range
    // For [2, 10], j = 3
    int j = (int)log2(R - L + 1);

    // Compute maximum of last 2^j elements with first
    // 2^j elements in range
    // For [2, 10], we compare arr[lookup[0][3]] and
    // arr[lookup[3][3]]
    if (lookup[L][j] >= lookup[R - (1 << j) + 1][j])
        return lookup[L][j];

    else
        return lookup[R - (1 << j) + 1][j];
}

// Driver program
int main()
{
    int a[] = { 7, 2, 3, 0, 5, 10, 3, 12, 18 };
    int n = sizeof(a) / sizeof(a[0]);

    buildSparseTable(a, n);

    cout << query(0, 4) << endl;
    cout << query(4, 7) << endl;
    cout << query(7, 8) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    static final int MAX = 500;

    // lookup[i][j] is going to store maximum
    // value in arr[i..j]. Ideally lookup table
    // size should not be fixed and should be
    // determined using n Log n. It is kept
    // constant to keep code simple.
    static int lookup[][] = new int[MAX][MAX];

    // Fills lookup array lookup[][] in bottom up manner
    static void buildSparseTable(int arr[], int n)
    {
        // Initialize M for the intervals with length 1
        for (int i = 0; i < n; i++)
            lookup[i][0] = arr[i];

        // Compute values from smaller to bigger intervals
        for (int j = 1; (1 << j) <= n; j++) {

            // Compute maximum value for all intervals with
            // size 2^j
            for (int i = 0; (i + (1 << j) - 1) < n; i++) {

                // For arr[2][10], we compare arr[lookup[0][7]]
                // and arr[lookup[3][10]]
                if (lookup[i][j - 1] > lookup[i + (1 << (j - 1))][j - 1])
                    lookup[i][j] = lookup[i][j - 1];
                else
                    lookup[i][j] = lookup[i + (1 << (j - 1))][j - 1];
            }
        }
    }

    // Returns maximum of arr[L..R]
    static int query(int L, int R)
    {
        // Find highest power of 2 that is smaller
        // than or equal to count of elements in given
        // range
        // For [2, 10], j = 3
        int j = (int)Math.log(R - L + 1);

        // Compute maximum of last 2^j elements with first
        // 2^j elements in range
        // For [2, 10], we compare arr[lookup[0][3]] and
        // arr[lookup[3][3]]
        if (lookup[L][j] >= lookup[R - (1 << j) + 1][j])
            return lookup[L][j];

        else
            return lookup[R - (1 << j) + 1][j];
    }

    // Driver program
    public static void main(String args[])
    {
        int a[] = { 7, 2, 3, 0, 5, 10, 3, 12, 18 };
        int n = a.length;

        buildSparseTable(a, n);

        System.out.println(query(0, 4));
        System.out.println(query(4, 7));
        System.out.println(query(7, 8));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import log
MAX = 500

# lookup[i][j] is going to store maximum
# value in arr[i..j]. Ideally lookup table
# size should not be fixed and should be
# determined using n Log n. It is kept
# constant to keep code simple.
lookup = [[0 for i in range(MAX)]
             for i in range(MAX)]

# Fills lookup array lookup[][]
# in bottom up manner
def buildSparseTable(arr, n):

    # Initialize M for the intervals
    # with length 1
    for i in range(n):
        lookup[i][0] = arr[i]

    # Compute values from smaller
    # to bigger intervals
    i, j = 0, 1
    while (1 << j) <= n:

        # Compute maximum value for
        # all intervals with size 2^j
        while (i + (1 << j) - 1) < n:

            # For arr[2][10], we compare arr[lookup[0][7]]
            # and arr[lookup[3][10]]
            if (lookup[i][j - 1] >
                lookup[i + (1 << (j - 1))][j - 1]):
                lookup[i][j] = lookup[i][j - 1]
            else:
                lookup[i][j] = lookup[i + (1 << (j - 1))][j - 1]
            i += 1
        j += 1

# Returns maximum of arr[L..R]
def query(L, R):

    # Find highest power of 2 that is smaller
    # than or equal to count of elements in given
    # range
    # For [2, 10], j = 3
    j = int(log(R - L + 1))

    # Compute maximum of last 2^j elements with first
    # 2^j elements in range
    # For [2, 10], we compare arr[lookup[0][3]] and
    # arr[lookup[3][3]]
    if (lookup[L][j] >= lookup[R - (1 << j) + 1][j]):
        return lookup[L][j]

    else:
        return lookup[R - (1 << j) + 1][j]

# Driver Code
a = [7, 2, 3, 0, 5, 10, 3, 12, 18]
n = len(a)

buildSparseTable(a, n);

print(query(0, 4))
print(query(4, 7))
print(query(7, 8))

# This code is contributed by Mohit Kumar
```

## C#

```
// Java implementation of the approach
using System;
class GFG {

    static int MAX = 500;

    // lookup[i][j] is going to store maximum
    // value in arr[i..j]. Ideally lookup table
    // size should not be fixed and should be
    // determined using n Log n. It is kept
    // constant to keep code simple.
    static int[, ] lookup = new int[MAX, MAX];

    // Fills lookup array lookup[][] in bottom up manner
    static void buildSparseTable(int[] arr, int n)
    {
        // Initialize M for the intervals with length 1
        for (int i = 0; i < n; i++)
            lookup[i, 0] = arr[i];

        // Compute values from smaller to bigger intervals
        for (int j = 1; (1 << j) <= n; j++) {

            // Compute maximum value for all intervals with
            // size 2^j
            for (int i = 0; (i + (1 << j) - 1) < n; i++) {

                // For arr[2][10], we compare arr[lookup[0][7]]
                // and arr[lookup[3][10]]
                if (lookup[i, j - 1] > lookup[i + (1 << (j - 1)), j - 1])
                    lookup[i, j] = lookup[i, j - 1];
                else
                    lookup[i, j] = lookup[i + (1 << (j - 1)), j - 1];
            }
        }
    }

    // Returns maximum of arr[L..R]
    static int query(int L, int R)
    {
        // Find highest power of 2 that is smaller
        // than or equal to count of elements in given
        // range
        // For [2, 10], j = 3
        int j = (int)Math.Log(R - L + 1);

        // Compute maximum of last 2^j elements with first
        // 2^j elements in range
        // For [2, 10], we compare arr[lookup[0][3]] and
        // arr[lookup[3][3]]
        if (lookup[L, j] >= lookup[R - (1 << j) + 1, j])
            return lookup[L, j];

        else
            return lookup[R - (1 << j) + 1, j];
    }

    // Driver program
    public static void Main(String[] args)
    {
        int[] a = { 7, 2, 3, 0, 5, 10, 3, 12, 18 };
        int n = a.Length;

        buildSparseTable(a, n);

        Console.WriteLine(query(0, 4));
        Console.WriteLine(query(4, 7));
        Console.WriteLine(query(7, 8));
    }
}
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let MAX = 500;

// lookup[i][j] is going to store maximum
// value in arr[i..j]. Ideally lookup table
// size should not be fixed and should be
// determined using n Log n. It is kept
// constant to keep code simple.
let lookup = new Array();
for(let i = 0; i < MAX; i++)
{
    let temp = [];
    for(let j = 0; j < MAX; j++)
    {
        temp.push([])
    }
    lookup.push(temp)
}

// Fills lookup array lookup[][] in bottom up manner
function buildSparseTable(arr, n)
{

    // Initialize M for the letervals with length 1
    for (let i = 0; i < n; i++)
        lookup[i][0] = arr[i];

    // Compute values from smaller to bigger letervals
    for (let j = 1; (1 << j) <= n; j++) {

        // Compute maximum value for all letervals with
        // size 2^j
        for (let i = 0; (i + (1 << j) - 1) < n; i++) {

            // For arr[2][10], we compare arr[lookup[0][7]]
            // and arr[lookup[3][10]]
            if (lookup[i][j - 1] > lookup[i + (1 << (j - 1))][j - 1])
                lookup[i][j] = lookup[i][j - 1];
            else
                lookup[i][j] = lookup[i + (1 << (j - 1))][j - 1];
        }
    }
}

// Returns maximum of arr[L..R]
function query(L, R)
{

    // Find highest power of 2 that is smaller
    // than or equal to count of elements in given
    // range
    // For [2, 10], j = 3
    let j = Math.floor(Math.log2(R - L + 1));

    // Compute maximum of last 2^j elements with first
    // 2^j elements in range
    // For [2, 10], we compare arr[lookup[0][3]] and
    // arr[lookup[3][3]]
    if (lookup[L][j] >= lookup[R - (1 << j) + 1][j])
        return lookup[L][j];
    else
        return lookup[R - (1 << j) + 1][j];
}

// Driver program
    let a = [ 7, 2, 3, 0, 5, 10, 3, 12, 18 ];
    let n = a.length;

    buildSparseTable(a, n);

    document.write(query(0, 4) + "<br>");
    document.write(query(4, 7) + "<br>");
    document.write(query(7, 8) + "<br>");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
7
12
18
```

因此稀疏表方法支持 O(1)时间内的查询操作，具有 O(n Log n)预处理时间和 O(n Log n)空间。