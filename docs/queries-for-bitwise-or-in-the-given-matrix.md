# 查询给定矩阵中的位“或”运算

> 原文:[https://www . geeksforgeeks . org/查询给定矩阵中的位或运算/](https://www.geeksforgeeks.org/queries-for-bitwise-or-in-the-given-matrix/)

给定一个由非负整数组成的 **N * N** 矩阵**mat【】【】**和一些由子矩阵的左上角和右下角组成的查询，任务是找到每个查询中给定的子矩阵的所有元素的逐位或。
**例:**

> **输入:** mat[][] = {
> {1，2，3}，
> {4，5，6}，
> {7，8，9}}，
> q[] = {{1，1，1，1}，{1，2，2，2}}
> **输出:**
> 5
> 15
> 查询 1:子矩阵中只有元素为 5。
> 查询 2: 6 OR 9 = 15
> **输入:** mat[][] = {
> {12，23，13}，
> {41，15，46}，
> {75，82，123}}，
> q[] = {{0，0，2，2}，{1，1，2，1}}
> **输出:**
> 127【T22

**天真的方法:**遍历子矩阵，找到该范围内所有数字的逐位或。在最坏的情况下，每次查询将花费 0(n<sup>2</sup>)时间。
**高效方法:**如果我们将整数看作二进制数，我们可以很容易地看到，我们的答案的 **i <sup>第</sup>T10】位被设置的条件是子矩阵中至少一个整数的 **i <sup>第</sup>T14】位被设置。
所以，我们将计算每个位的前缀计数。我们将使用这个来寻找子矩阵中设置了 **i <sup>th</sup>** 位的整数个数。如果它是非零的，那么我们的答案的第 **i <sup>第</sup>** 位也将被设置。
为此，我们将创建一个 3d 数组， **prefix_count[][][]** ，其中 **prefix_count[i][x][y]** 将存储子矩阵所有元素的计数，左上角在 **{0，0}** 和右下角在 **{x，y}** 和 **i <sup>第</sup>** 位集。参考
[这篇](https://www.geeksforgeeks.org/submatrix-sum-queries/)文章了解矩阵情况下的前缀 _ 计数。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define bitscount 32
#define n 3
using namespace std;

// Array to store bit-wise
// prefix count
int prefix_count[bitscount][n][n];

// Function to find the prefix sum
void findPrefixCount(int arr[][n])
{

    // Loop for each bit
    for (int i = 0; i < bitscount; i++) {

        // Loop to find prefix-count
        // for each row
        for (int j = 0; j < n; j++) {
            prefix_count[i][j][0] = ((arr[j][0] >> i) & 1);
            for (int k = 1; k < n; k++) {
                prefix_count[i][j][k] = ((arr[j][k] >> i) & 1);
                prefix_count[i][j][k] += prefix_count[i][j][k - 1];
            }
        }
    }

    // Finding column-wise prefix
    // count
    for (int i = 0; i < bitscount; i++)
        for (int j = 1; j < n; j++)
            for (int k = 0; k < n; k++)
                prefix_count[i][j][k] += prefix_count[i][j - 1][k];
}

// Function to return the result for a query
int rangeOr(int x1, int y1, int x2, int y2)
{

    // To store the answer
    int ans = 0;

    // Loop for each bit
    for (int i = 0; i < bitscount; i++) {

        // To store the number of variables
        // with ith bit set
        int p;
        if (x1 == 0 and y1 == 0)
            p = prefix_count[i][x2][y2];
        else if (x1 == 0)
            p = prefix_count[i][x2][y2]
                - prefix_count[i][x2][y1 - 1];
        else if (y1 == 0)
            p = prefix_count[i][x2][y2]
                - prefix_count[i][x1 - 1][y2];
        else
            p = prefix_count[i][x2][y2]
                - prefix_count[i][x1 - 1][y2]
                - prefix_count[i][x2][y1 - 1]
                + prefix_count[i][x1 - 1][y1 - 1];

        // If count of variables with ith bit
        // set is greater than 0
        if (p != 0)
            ans = (ans | (1 << i));
    }

    return ans;
}

// Driver code
int main()
{
    int arr[][n] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };

    findPrefixCount(arr);

    int queries[][4] = { { 1, 1, 1, 1 }, { 1, 2, 2, 2 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    for (int i = 0; i < q; i++)
        cout << rangeOr(queries[i][0],
                        queries[i][1],
                        queries[i][2],
                        queries[i][3])
             << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    final static int bitscount = 32 ;
    final static int n = 3 ;

    // Array to store bit-wise
    // prefix count
    static int prefix_count[][][] = new int [bitscount][n][n];

    // Function to find the prefix sum
    static void findPrefixCount(int arr[][])
    {

        // Loop for each bit
        for (int i = 0; i < bitscount; i++)
        {

            // Loop to find prefix-count
            // for each row
            for (int j = 0; j < n; j++)
            {
                prefix_count[i][j][0] = ((arr[j][0] >> i) & 1);
                for (int k = 1; k < n; k++)
                {
                    prefix_count[i][j][k] = ((arr[j][k] >> i) & 1);
                    prefix_count[i][j][k] += prefix_count[i][j][k - 1];
                }
            }
        }

        // Finding column-wise prefix
        // count
        for (int i = 0; i < bitscount; i++)
            for (int j = 1; j < n; j++)
                for (int k = 0; k < n; k++)
                    prefix_count[i][j][k] += prefix_count[i][j - 1][k];
    }

    // Function to return the result for a query
    static int rangeOr(int x1, int y1, int x2, int y2)
    {

        // To store the answer
        int ans = 0;

        // Loop for each bit
        for (int i = 0; i < bitscount; i++)
        {

            // To store the number of variables
            // with ith bit set
            int p;
            if (x1 == 0 && y1 == 0)
                p = prefix_count[i][x2][y2];
            else if (x1 == 0)
                p = prefix_count[i][x2][y2]
                    - prefix_count[i][x2][y1 - 1];
            else if (y1 == 0)
                p = prefix_count[i][x2][y2]
                    - prefix_count[i][x1 - 1][y2];
            else
                p = prefix_count[i][x2][y2]
                    - prefix_count[i][x1 - 1][y2]
                    - prefix_count[i][x2][y1 - 1]
                    + prefix_count[i][x1 - 1][y1 - 1];

            // If count of variables with ith bit
            // set is greater than 0
            if (p != 0)
                ans = (ans | (1 << i));
        }

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[][] = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };

        findPrefixCount(arr);

        int queries[][] = { { 1, 1, 1, 1 }, { 1, 2, 2, 2 } };
        int q = queries.length;

        for (int i = 0; i < q; i++)
            System.out.println( rangeOr(queries[i][0],
                            queries[i][1],
                            queries[i][2],
                            queries[i][3]) );
    }
}

// This code is contributed by AnkitRai
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
bitscount = 32
n = 3
# Array to store bit-wise
# prefix count
prefix_count = [[[0 for i in range(n)] for j in range(n)] for k in range(bitscount)]

# Function to find the prefix sum
def findPrefixCount(arr):
    # Loop for each bit
    for i in range(bitscount):
        # Loop to find prefix-count
        # for each row
        for j in range(n):
            prefix_count[i][j][0] = ((arr[j][0] >> i) & 1)
            for k in range(1,n):
                prefix_count[i][j][k] = ((arr[j][k] >> i) & 1)
                prefix_count[i][j][k] += prefix_count[i][j][k - 1]

    # Finding column-wise prefix
    # count
    for i in range(bitscount):
        for j in range(1,n):
            for k in range(n):
                prefix_count[i][j][k] += prefix_count[i][j - 1][k]

# Function to return the result for a query
def rangeOr(x1, y1, x2, y2):
    # To store the answer
    ans = 0

    # Loop for each bit
    for i in range(bitscount):
        # To store the number of variables
        # with ith bit set
        if (x1 == 0 and y1 == 0):
            p = prefix_count[i][x2][y2]
        elif (x1 == 0):
            p = prefix_count[i][x2][y2] - prefix_count[i][x2][y1 - 1]
        elif (y1 == 0):
            p = prefix_count[i][x2][y2] - prefix_count[i][x1 - 1][y2]
        else:
            p = prefix_count[i][x2][y2] - prefix_count[i][x1 - 1][y2] - prefix_count[i][x2][y1 - 1] + prefix_count[i][x1 - 1][y1 - 1];

        # If count of variables with ith bit
        # set is greater than 0
        if (p != 0):
            ans = (ans | (1 << i))

    return ans

# Driver code
if __name__ == '__main__':
    arr =  [[1, 2, 3],
            [4, 5, 6],
            [7, 8, 9]]

    findPrefixCount(arr)
    queries = [[1, 1, 1, 1],
                        [1, 2, 2, 2]]
    q = len(queries)

    for i in range(q):
        print(rangeOr(queries[i][0],queries[i][1],queries[i][2],queries[i][3]))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int bitscount = 32 ;
    static int n = 3 ;

    // Array to store bit-wise
    // prefix count
    static int [,,]prefix_count = new int [bitscount,n,n];

    // Function to find the prefix sum
    static void findPrefixCount(int [,]arr)
    {

        // Loop for each bit
        for (int i = 0; i < bitscount; i++)
        {

            // Loop to find prefix-count
            // for each row
            for (int j = 0; j < n; j++)
            {
                prefix_count[i,j,0] = ((arr[j,0] >> i) & 1);
                for (int k = 1; k < n; k++)
                {
                    prefix_count[i, j, k] = ((arr[j, k] >> i) & 1);
                    prefix_count[i, j, k] += prefix_count[i, j, k - 1];
                }
            }
        }

        // Finding column-wise prefix
        // count
        for (int i = 0; i < bitscount; i++)
            for (int j = 1; j < n; j++)
                for (int k = 0; k < n; k++)
                    prefix_count[i, j, k] += prefix_count[i, j - 1, k];
    }

    // Function to return the result for a query
    static int rangeOr(int x1, int y1, int x2, int y2)
    {

        // To store the answer
        int ans = 0;

        // Loop for each bit
        for (int i = 0; i < bitscount; i++)
        {

            // To store the number of variables
            // with ith bit set
            int p;
            if (x1 == 0 && y1 == 0)
                p = prefix_count[i, x2, y2];
            else if (x1 == 0)
                p = prefix_count[i, x2, y2]
                    - prefix_count[i, x2, y1 - 1];
            else if (y1 == 0)
                p = prefix_count[i, x2, y2]
                    - prefix_count[i, x1 - 1, y2];
            else
                p = prefix_count[i, x2, y2]
                    - prefix_count[i, x1 - 1, y2]
                    - prefix_count[i, x2, y1 - 1]
                    + prefix_count[i, x1 - 1, y1 - 1];

            // If count of variables with ith bit
            // set is greater than 0
            if (p != 0)
                ans = (ans | (1 << i));
        }

        return ans;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int [,]arr = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };

        findPrefixCount(arr);

        int [,]queries = { { 1, 1, 1, 1 }, { 1, 2, 2, 2 } };
        int q = queries.GetLength(0);

        for (int i = 0; i < q; i++)
            Console.WriteLine( rangeOr(queries[i,0],
                            queries[i,1],
                            queries[i,2],
                            queries[i,3]) );
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const bitscount = 32;
const n = 3;

// Array to store bit-wise
// prefix count
let prefix_count = new Array(bitscount);
for (let i = 0; i < bitscount; i++) {
    prefix_count[i] = new Array(n);
    for (let j = 0; j < n; j++)
        prefix_count[i][j] = new Array(n);
}

// Function to find the prefix sum
function findPrefixCount(arr)
{

    // Loop for each bit
    for (let i = 0; i < bitscount; i++)
    {

        // Loop to find prefix-count
        // for each row
        for (let j = 0; j < n; j++) {
            prefix_count[i][j][0] =
            ((arr[j][0] >> i) & 1);
            for (let k = 1; k < n; k++)
            {
                prefix_count[i][j][k] =
                ((arr[j][k] >> i) & 1);
                prefix_count[i][j][k] +=
                prefix_count[i][j][k - 1];
            }
        }
    }

    // Finding column-wise prefix
    // count
    for (let i = 0; i < bitscount; i++)
        for (let j = 1; j < n; j++)
            for (let k = 0; k < n; k++)
                prefix_count[i][j][k] +=
                prefix_count[i][j - 1][k];
}

// Function to return the result for a query
function rangeOr(x1, y1, x2, y2)
{

    // To store the answer
    let ans = 0;

    // Loop for each bit
    for (let i = 0; i < bitscount; i++) {

        // To store the number of variables
        // with ith bit set
        let p;
        if (x1 == 0 && y1 == 0)
            p = prefix_count[i][x2][y2];
        else if (x1 == 0)
            p = prefix_count[i][x2][y2]
                - prefix_count[i][x2][y1 - 1];
        else if (y1 == 0)
            p = prefix_count[i][x2][y2]
                - prefix_count[i][x1 - 1][y2];
        else
            p = prefix_count[i][x2][y2]
                - prefix_count[i][x1 - 1][y2]
                - prefix_count[i][x2][y1 - 1]
                + prefix_count[i][x1 - 1][y1 - 1];

        // If count of variables with ith bit
        // set is greater than 0
        if (p != 0)
            ans = (ans | (1 << i));
    }

    return ans;
}

// Driver code
    let arr = [ [ 1, 2, 3 ],
                     [ 4, 5, 6 ],
                     [ 7, 8, 9 ] ];

    findPrefixCount(arr);

    let queries = [ [ 1, 1, 1, 1 ], [ 1, 2, 2, 2 ] ];
    let q = queries.length;

    for (let i = 0; i < q; i++)
        document.write(rangeOr(queries[i][0],
                        queries[i][1],
                        queries[i][2],
                        queries[i][3]) + "<br>");

</script>
```

**Output:** 

```
5
15
```

预计算的时间复杂度为 O(n <sup>2</sup> )，每个查询都可以在 O(1)中回答

辅助空间:O(n <sup>2</sup> )