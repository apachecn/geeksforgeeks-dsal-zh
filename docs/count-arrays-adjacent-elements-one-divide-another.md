# 所有相邻元素被一个元素除另一个元素的数组计数

> 原文:[https://www . geeksforgeeks . org/count-arrays-相邻-elements-one-divide-other/](https://www.geeksforgeeks.org/count-arrays-adjacent-elements-one-divide-another/)

给定两个正整数 **n** 和 **n** 。任务是找到大小为 n 的数组的数量，这些数组可以这样形成:

1.  每个元素都在[1，m]范围内
2.  所有相邻元素都是这样的，其中一个元素划分另一个元素，即元素 A <sub>i</sub> 划分 A <sub>i + 1</sub> 或元素 A <sub>i + 1</sub> 划分 A <sub>i + 2</sub> 。

**示例:**

```
Input : n = 3, m = 3.
Output : 17
{1,1,1}, {1,1,2}, {1,1,3}, {1,2,1}, 
{1,2,2}, {1,3,1}, {1,3,3}, {2,1,1},
{2,1,2}, {2,1,3}, {2,2,1}, {2,2,2},
{3,1,1}, {3,1,2}, {3,1,3}, {3,3,1}, 
{3,3,3} are possible arrays.

Input : n = 1, m = 10.
Output : 10 
```

我们试图在数组的每个索引处找到多个可能的值。首先，在索引 0 处，从 1 到 m 的所有值都是可能的。现在观察每个索引，我们可以达到它的倍数或因子。所以，预先计算并为所有元素存储它。因此，对于以整数 x 结束的每个位置 I，我们可以转到下一个位置 i + 1，数组以 x 的倍数或 x 的因子结束。此外，x 的倍数或 x 的因子必须小于 m

因此，我们定义了一个 2D 数组 dp[i][j]，它是大小为 I 的可能数组(可分的相邻元素)的数目，其中 j 是它的第一个索引元素。

```
1 <= i <= m, dp[1][m] = 1.
for 1 <= j <= m and 2 <= i <= n
  dp[i][j] = dp[i-1][j] + number of factor 
             of previous element less than m 
             + number of multiples of previous
             element less than m.
```

下面是该方法的实现:

## C++

```
// C++ program to count number of arrays
// of size n such that every element is
// in range [1, m] and adjacen are
// divisible
#include <bits/stdc++.h>
#define  MAX 1000
using namespace std;

int numofArray(int n, int m)
{
    int dp[MAX][MAX];

    // For storing factors.
    vector<int> di[MAX];

    // For storing multiples.
    vector<int> mu[MAX];

    memset(dp, 0, sizeof dp);
    memset(di, 0, sizeof di);
    memset(mu, 0, sizeof mu);

    // calculating the factors and multiples
    // of elements [1...m].
    for (int i = 1; i <= m; i++)
    {
        for (int j = 2*i; j <= m; j += i)
        {
            di[j].push_back(i);
            mu[i].push_back(j);
        }
        di[i].push_back(i);
    }

    // Initialising for size 1 array for
    // each i <= m.
    for (int i = 1; i <= m; i++)
        dp[1][i] = 1;

    // Calculating the number of array possible
    // of size i and starting with j.
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            dp[i][j] = 0;

            // For all previous possible values.
            // Adding number of factors.
            for (auto x:di[j])
                dp[i][j] += dp[i-1][x];

            // Adding number of multiple.
            for (auto x:mu[j])
                dp[i][j] += dp[i-1][x];
        }
    }

    // Calculating the total count of array
    // which start from [1...m].
    int ans = 0;
    for (int i = 1; i <= m; i++)
    {
        ans += dp[n][i];
        di[i].clear();
        mu[i].clear();
    }

    return ans;
}

// Driven Program
int main()
{
    int n = 3, m = 3;
    cout << numofArray(n, m) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of arrays
// of size n such that every element is
// in range [1, m] and adjacen are
// divisible
import java.util.*;

class GFG
{
static int MAX = 1000;

static int numofArray(int n, int m)
{
    int [][]dp = new int[MAX][MAX];

    // For storing factors.
    Vector<Integer> []di = new Vector[MAX];

    // For storing multiples.
    Vector<Integer> []mu = new Vector[MAX];

    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            dp[i][j] = 0;
        }
    }
    for(int i = 0; i < MAX; i++)
    {
        di[i] = new Vector<>();
        mu[i] = new Vector<>();
    }

    // calculating the factors and multiples
    // of elements [1...m].
    for (int i = 1; i <= m; i++)
    {
        for (int j = 2 * i; j <= m; j += i)
        {
            di[j].add(i);
            mu[i].add(j);
        }
        di[i].add(i);
    }

    // Initialising for size 1 array for
    // each i <= m.
    for (int i = 1; i <= m; i++)
        dp[1][i] = 1;

    // Calculating the number of array possible
    // of size i and starting with j.
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            dp[i][j] = 0;

            // For all previous possible values.
            // Adding number of factors.
            for (Integer x:di[j])
                dp[i][j] += dp[i - 1][x];

            // Adding number of multiple.
            for (Integer x:mu[j])
                dp[i][j] += dp[i - 1][x];
        }
    }

    // Calculating the total count of array
    // which start from [1...m].
    int ans = 0;
    for (int i = 1; i <= m; i++)
    {
        ans += dp[n][i];
        di[i].clear();
        mu[i].clear();
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3, m = 3;
    System.out.println(numofArray(n, m));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count the number of
# arrays of size n such that every element is
# in range [1, m] and adjacent are divisible

MAX = 1000

def numofArray(n, m):

    dp = [[0 for i in range(MAX)] for j in range(MAX)]

    # For storing factors.
    di = [[] for i in range(MAX)]

    # For storing multiples.
    mu = [[] for i in range(MAX)]

    # calculating the factors and multiples
    # of elements [1...m].
    for i in range(1, m+1):

        for j in range(2*i, m+1, i):

            di[j].append(i)
            mu[i].append(j)

        di[i].append(i)

    # Initialising for size 1 array for each i <= m.
    for i in range(1, m+1):
        dp[1][i] = 1

    # Calculating the number of array possible
    # of size i and starting with j.
    for i in range(2, n+1):

        for j in range(1, m+1):

            dp[i][j] = 0

            # For all previous possible values.
            # Adding number of factors.
            for x in di[j]:
                dp[i][j] += dp[i-1][x]

            # Adding number of multiple.
            for x in mu[j]:
                dp[i][j] += dp[i-1][x]

    # Calculating the total count of array
    # which start from [1...m].
    ans = 0
    for i in range(1, m+1):

        ans += dp[n][i]
        di[i].clear()
        mu[i].clear()

    return ans

# Driven Program
if __name__ == "__main__":

    n = m = 3
    print(numofArray(n, m))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count number of arrays
// of size n such that every element is
// in range [1, m] and adjacen are
// divisible
using System;
using System.Collections.Generic;                

class GFG
{
static int MAX = 1000;

static int numofArray(int n, int m)
{
    int [,]dp = new int[MAX, MAX];

    // For storing factors.
    List<int> []di = new List<int>[MAX];

    // For storing multiples.
    List<int> []mu = new List<int>[MAX];

    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            dp[i, j] = 0;
        }
    }
    for(int i = 0; i < MAX; i++)
    {
        di[i] = new List<int>();
        mu[i] = new List<int>();
    }

    // calculating the factors and multiples
    // of elements [1...m].
    for (int i = 1; i <= m; i++)
    {
        for (int j = 2 * i; j <= m; j += i)
        {
            di[j].Add(i);
            mu[i].Add(j);
        }
        di[i].Add(i);
    }

    // Initialising for size 1 array for
    // each i <= m.
    for (int i = 1; i <= m; i++)
        dp[1, i] = 1;

    // Calculating the number of array possible
    // of size i and starting with j.
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            dp[i, j] = 0;

            // For all previous possible values.
            // Adding number of factors.
            foreach (int x in di[j])
                dp[i, j] += dp[i - 1, x];

            // Adding number of multiple.
            foreach (int x in mu[j])
                dp[i, j] += dp[i - 1, x];
        }
    }

    // Calculating the total count of array
    // which start from [1...m].
    int ans = 0;
    for (int i = 1; i <= m; i++)
    {
        ans += dp[n, i];
        di[i].Clear();
        mu[i].Clear();
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3, m = 3;
    Console.WriteLine(numofArray(n, m));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to count number of arrays
// of size n such that every element is
// in range [1, m] and adjacen are
// divisible
let MAX = 1000;

function numofArray(n, m)
{
    let dp = new Array(MAX);

    // For storing factors.
    let di = new Array(MAX);

    // For storing multiples.
    let mu = new Array(MAX);

    for(let i = 0; i < MAX; i++)
    {
        dp[i] = new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            dp[i][j] = 0;
        }
    }
    for(let i = 0; i < MAX; i++)
    {
        di[i] = [];
        mu[i] = [];
    }

    // Calculating the factors and multiples
    // of elements [1...m].
    for(let i = 1; i <= m; i++)
    {
        for(let j = 2 * i; j <= m; j += i)
        {
            di[j].push(i);
            mu[i].push(j);
        }
        di[i].push(i);
    }

    // Initialising for size 1 array for
    // each i <= m.
    for(let i = 1; i <= m; i++)
        dp[1][i] = 1;

    // Calculating the number of array possible
    // of size i and starting with j.
    for(let i = 2; i <= n; i++)
    {
        for(let j = 1; j <= m; j++)
        {
            dp[i][j] = 0;

            // For all previous possible values.
            // Adding number of factors.
            for(let x = 0; x < di[j].length; x++)
                dp[i][j] += dp[i - 1][di[j][x]];

            // Adding number of multiple.
            for(let x = 0; x < mu[j].length; x++)
                dp[i][j] += dp[i - 1][mu[j][x]];
        }
    }

    // Calculating the total count of array
    // which start from [1...m].
    let ans = 0;
    for(let i = 1; i <= m; i++)
    {
        ans += dp[n][i];
        di[i] = [];
        mu[i] = [];
    }
    return ans;
}

// Driver Code
let n = 3, m = 3;

document.write(numofArray(n, m));

// This code is contributed by rag2127

</script>
```

**输出:**

```
17
```

**时间复杂度:** O(N*M)。

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。