# 垂直或水平从(1，1)到(X，Y)的‘a’的最大数量的路径

> 原文:[https://www . geesforgeks . org/path-with-max-number-a-from-1-1-x-y-垂直或水平/](https://www.geeksforgeeks.org/paths-with-maximum-number-of-a-from-1-1-to-x-y-vertically-or-horizontally/)

给定一个由字符组成的 **N X N** 矩阵。还给出了 Q 查询，其中每个查询包含一个坐标(X，Y)。对于每个查询，通过垂直或水平移动找到从(1，1)到(X，Y)的所有路径，并选择其中具有最大数量![a     ](img/dad1f7e479eb136e5f42993179fc50ca.png "Rendered by QuickLaTeX.com")的路径。任务是沿着这条路径打印**非-a-字符**的数量。

**示例**:

```
Input: mat[][] = {{'a', 'b', 'a'}, 
                             {'a', 'c', 'd'}, 
                             {'b', 'a', 'b'}} 
            *Queries*: 
            X = 1, Y = 3
            X = 3, Y = 3
Output: 
1st query: 1
2nd query: 2

Query-1: There is only one path from (1, 1) to (1, 3)
i.e., "aba" and the number of characters 
which are not 'a' is 1\. 
Query-2: The path which has the maximum number of 'a'
in it is "aabab", hence non 'a' 
characters are 2\. 
```

该问题是[最小成本路径 Dp 问题](https://www.geeksforgeeks.org/min-cost-path-dp-6/)的变体。我们需要预先计算 DP[][]数组，然后答案将是 DP[X][Y]，因此每个查询都可以在 O(1)中回答。如果索引位置(1，1)字符不是“a”，则将 dp[1][1]值增加 1。然后简单地对行和列进行迭代，做一个[最小成本 DP](https://www.geeksforgeeks.org/min-cost-path-dp-6/) ，考虑‘a’为 1，非‘a’字符为 0。由于 DP[][]数组存储从(1，1)到任何索引(I，j)的最小开销路径，因此查询可以在 O(1)中得到回答。

下面是上述方法的实现:

## C++

```
// C++ program to find paths with maximum number
// of 'a' from (1, 1) to (X, Y) vertically
// or horizontally

#include <bits/stdc++.h>
using namespace std;

const int n = 3;
int dp[n][n];

// Function to answer queries
void answerQueries(pair<int, int> queries[], int q)
{
    // Iterate till query
    for (int i = 0; i < q; i++) {

        // Decrease to get 0-based indexing
        int x = queries[i].first;
        x--;
        int y = queries[i].second;
        y--;

        // Print answer
        cout << dp[x][y] << endl;
    }
}

// Function that pre-computes the dp array
void pre_compute(char a[][n])
{
    // Check fo the first character
    if (a[0][0] == 'a')
        dp[0][0] = 0;
    else
        dp[0][0] = 1;

    // Iterate in row and columns
    for (int row = 0; row < n; row++) {
        for (int col = 0; col < n; col++) {
            // If not first row or not first column
            if (row != 0 || col != 0)
                dp[row][col] = INT_MAX;

            // Not first row
            if (row != 0) {
                dp[row][col] = min(dp[row][col],
                                   dp[row - 1][col]);
            }

            // Not first column
            if (col != 0) {
                dp[row][col] = min(dp[row][col],
                                   dp[row][col - 1]);
            }

            // If it is not 'a' then increase by 1
            if (a[row][col] != 'a' && (row != 0 || col != 0))
                dp[row][col] += 1;
        }
    }
}

// Driver code
int main()
{
    // character N X N array
    char a[][3] = { { 'a', 'b', 'a' },
                    { 'a', 'c', 'd' },
                    { 'b', 'a', 'b' } };

    // queries
    pair<int, int> queries[] = { { 1, 3 }, { 3, 3 } };

    // number of queries
    int q = 2;

    // function call to pre-compute
    pre_compute(a);

    // function call to answer every query
    answerQueries(queries, q);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find paths with maximum number
// of 'a' from (1, 1) to (X, Y) vertically
// or horizontally
class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

static int n = 3;
static int [][]dp = new int[n][n];

// Function to answer queries
static void answerQueries(pair queries[], int q)
{
    // Iterate till query
    for (int i = 0; i < q; i++)
    {

        // Decrease to get 0-based indexing
        int x = queries[i].first;
        x--;
        int y = queries[i].second;
        y--;

        // Print answer
        System.out.println(dp[x][y]);
    }
}

// Function that pre-computes the dp array
static void pre_compute(char a[][])
{
    // Check fo the first character
    if (a[0][0] == 'a')
        dp[0][0] = 0;
    else
        dp[0][0] = 1;

    // Iterate in row and columns
    for (int row = 0; row < n; row++)
    {
        for (int col = 0; col < n; col++)
        {
            // If not first row or not first column
            if (row != 0 || col != 0)
                dp[row][col] = Integer.MAX_VALUE;

            // Not first row
            if (row != 0)
            {
                dp[row][col] = Math.min(dp[row][col],
                                        dp[row - 1][col]);
            }

            // Not first column
            if (col != 0)
            {
                dp[row][col] = Math.min(dp[row][col],
                                        dp[row][col - 1]);
            }

            // If it is not 'a' then increase by 1
            if (a[row][col] != 'a' && (row != 0 || col != 0))
                dp[row][col] += 1;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    // character N X N array
    char a[][] = {{ 'a', 'b', 'a' },
                  { 'a', 'c', 'd' },
                  { 'b', 'a', 'b' }};

    // queries
    pair queries[] = { new pair( 1, 3 ),
                       new pair(3, 3 ) };

    // number of queries
    int q = 2;

    // function call to pre-compute
    pre_compute(a);

    // function call to answer every query
    answerQueries(queries, q);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find paths with maximum number
# of 'a' from (1, 1) to (X, Y) vertically
# or horizontally
n = 3
dp = [[0 for i in range(n)]
         for j in range(n)]

# Function to answer queries
def answerQueries(queries, q):

    # Iterate till query
    for i in range(q):

        # Decrease to get 0-based indexing
        x = queries[i][0]
        x -= 1
        y = queries[i][1]
        y -= 1

        # Print answer
        print(dp[x][y])

# Function that pre-computes the dp array
def pre_compute(a):

    # Check for the first character
    if a[0][0] == 'a':
        dp[0][0] = 0
    else:
        dp[0][0] = 1

    # Iterate in row and columns
    for row in range(n):
        for col in range(n):

            # If not first row or not first column
            if (row != 0 or col != 0):
                dp[row][col] = 9999

            # Not first row
            if (row != 0):
                dp[row][col] = min(dp[row][col],
                                   dp[row - 1][col])

            # Not first column
            if (col != 0):
                dp[row][col] = min(dp[row][col],
                                   dp[row][col - 1])

            # If it is not 'a' then increase by 1
            if (a[row][col] != 'a' and (row != 0 or
                                        col != 0)):
                dp[row][col] += 1

# Driver code
if __name__ == '__main__':

    # Character N X N array
    a = [ ('a', 'b', 'a'),
          ('a', 'c', 'd'),
          ('b', 'a', 'b') ]

    # Queries
    queries = [ (1, 3), (3, 3) ]

    # Number of queries
    q = 2

    # Function call to pre-compute
    pre_compute(a)

    # function call to answer every query
    answerQueries(queries, q)

# This code is contributed by kirtishsurangalikar
```

## C#

```
// C# program to find paths with maximum number
// of 'a' from (1, 1) to (X, Y) vertically
// or horizontally
using System;

class GFG
{
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

static int n = 3;
static int [,]dp = new int[n, n];

// Function to answer queries
static void answerQueries(pair []queries, int q)
{
    // Iterate till query
    for (int i = 0; i < q; i++)
    {

        // Decrease to get 0-based indexing
        int x = queries[i].first;
        x--;
        int y = queries[i].second;
        y--;

        // Print answer
        Console.WriteLine(dp[x, y]);
    }
}

// Function that pre-computes the dp array
static void pre_compute(char [,]a)
{
    // Check fo the first character
    if (a[0, 0] == 'a')
        dp[0, 0] = 0;
    else
        dp[0, 0] = 1;

    // Iterate in row and columns
    for (int row = 0; row < n; row++)
    {
        for (int col = 0; col < n; col++)
        {
            // If not first row or not first column
            if (row != 0 || col != 0)
                dp[row, col] = int.MaxValue;

            // Not first row
            if (row != 0)
            {
                dp[row, col] = Math.Min(dp[row, col],
                                        dp[row - 1, col]);
            }

            // Not first column
            if (col != 0)
            {
                dp[row, col] = Math.Min(dp[row, col],
                                        dp[row, col - 1]);
            }

            // If it is not 'a' then increase by 1
            if (a[row, col] != 'a' &&
               (row != 0 || col != 0))
                dp[row, col] += 1;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    // character N X N array
    char [,]a = {{ 'a', 'b', 'a' },
                 { 'a', 'c', 'd' },
                 { 'b', 'a', 'b' }};

    // queries
    pair []queries = { new pair(1, 3),
                       new pair(3, 3) };

    // number of queries
    int q = 2;

    // function call to pre-compute
    pre_compute(a);

    // function call to answer every query
    answerQueries(queries, q);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find paths with maximum number
// of 'a' from (1, 1) to (X, Y) vertically
// or horizontally

class pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

let n = 3;

let dp=new Array(n);
for(let i=0;i<n;i++)
{
    dp[i]=new Array(n);
    for(let j=0;j<n;j++)
    {
        dp[i][j]=0;
    }
}

// Function to answer queries
function answerQueries(queries,q)
{
    // Iterate till query
    for (let i = 0; i < q; i++)
    {

        // Decrease to get 0-based indexing
        let x = queries[i].first;
        x--;
        let y = queries[i].second;
        y--;

        // Print answer
        document.write(dp[x][y]+"<br>");
    }
}

// Function that pre-computes the dp array
function pre_compute(a)
{
    // Check fo the first character
    if (a[0][0] == 'a')
        dp[0][0] = 0;
    else
        dp[0][0] = 1;

    // Iterate in row and columns
    for (let row = 0; row < n; row++)
    {
        for (let col = 0; col < n; col++)
        {
            // If not first row or not first column
            if (row != 0 || col != 0)
                dp[row][col] = Number.MAX_VALUE;

            // Not first row
            if (row != 0)
            {
                dp[row][col] = Math.min(dp[row][col],
                                        dp[row - 1][col]);
            }

            // Not first column
            if (col != 0)
            {
                dp[row][col] = Math.min(dp[row][col],
                                        dp[row][col - 1]);
            }

            // If it is not 'a' then increase by 1
            if (a[row][col] != 'a' && (row != 0 || col != 0))
                dp[row][col] += 1;
        }
    }
}

// Driver code
let a=[[ 'a', 'b', 'a' ],
                  [ 'a', 'c', 'd' ],
                  [ 'b', 'a', 'b' ]];
// queries
let queries = [ new pair( 1, 3 ),
new pair(3, 3 ) ];

// number of queries
let q = 2;

// function call to pre-compute
pre_compute(a);

// function call to answer every query
answerQueries(queries, q);

// This code is contributed by rag2127
</script>
```

**Output**

```
1
2
```

**时间复杂度** : O(N <sup>2</sup> )用于预计算，O(1)用于每个查询。
**辅助空间** : O(N <sup>2</sup> )