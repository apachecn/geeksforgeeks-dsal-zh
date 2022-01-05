# 宝藏与城市

> 原文:[https://www.geeksforgeeks.org/treasure-and-cities/](https://www.geeksforgeeks.org/treasure-and-cities/)

给定 n 个城市:x1，x2，… xn:每个都与 T[i](宝藏)和 C[i](颜色)相关联。你可以选择参观一个城市或跳过它。只允许向前移动。当您访问一个城市时，您会收到以下金额:

1.  A*T[i]如果到访城市的颜色与先前到访城市的颜色相同
2.  B*T[i]如果这是第一个参观过的城市，或者参观过的城市的颜色与以前参观过的城市的颜色不同。T[i]，A 和 B 的值可以是负数，而 C[i]的范围是 1 到 n

我们必须计算可能的最大利润。

**示例:**

```
Input :  A = -5, B = 7
Treasure = {4, 8, 2, 9}
color = {2, 2, 3, 2}
Output : 133
Visit city 2, 3 and 4\. Profit = 8*7+2*7+9*7 = 133

Input : A = 5, B = -7 
Treasure = {4, 8, 2, 9}
color = {2, 2, 3, 2}
Output: 57
Visit city 1, 2, 4\. Profit = (-7)*4+8*5+9*5 = 57
```

来源:[甲骨文面试体验集 61](https://www.geeksforgeeks.org/oracle-interview-experience-set-61-campus/) 。

这是标准 [0/1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题的变种。这个想法是要么参观一个城市，要么跳过它，返回两种情况下的最大值。

以下是上述问题的解决方案。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// k is current index and col is previous color.
int MaxProfit(int treasure[], int color[], int n,
              int k, int col, int A, int B)
{
    int sum = 0;

    if (k == n) // base case
        return 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city is equal
    // to prev visited city
    if (col == color[k])
        sum += max(A * treasure[k] +
                MaxProfit(treasure, color, n,
                       k + 1, color[k], A, B),
                MaxProfit(treasure, color, n,
                          k + 1, col, A, B));
    else
        sum += max(B * treasure[k] +                                         
                MaxProfit(treasure, color, n,
                       k + 1, color[k], A, B),
               MaxProfit(treasure, color, n,
                          k + 1, col, A, B));

    // return max of both options
    return sum;
}

int main()
{

    int A = -5, B = 7;
    int treasure[] = { 4, 8, 2, 9 };
    int color[] = { 2, 2, 6, 2 };
    int n = sizeof(color) / sizeof(color[0]);

    // Initially begin with color 0
    cout << MaxProfit(treasure, color, n, 0, 0, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// k is current index and col is previous color.
static int MaxProfit(int treasure[], int color[], int n,
            int k, int col, int A, int B)
{
    int sum = 0;

    if (k == n) // base case
        return 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city is equal
    // to prev visited city
    if (col == color[k])
        sum += Math.max(A * treasure[k] +
                MaxProfit(treasure, color, n,
                    k + 1, color[k], A, B),
                MaxProfit(treasure, color, n,
                        k + 1, col, A, B));
    else
        sum += Math.max(B * treasure[k] +                                        
                MaxProfit(treasure, color, n,
                    k + 1, color[k], A, B),
            MaxProfit(treasure, color, n,
                        k + 1, col, A, B));

    // return max of both options
    return sum;
}

public static void main(String[] args)
{

    int A = -5, B = 7;
    int treasure[] = { 4, 8, 2, 9 };
    int color[] = { 2, 2, 6, 2 };
    int n = color.length;

    // Initially begin with color 0
    System.out.print(MaxProfit(treasure, color, n, 0, 0, A, B));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# k is current index and col
# is previous color.
def MaxProfit(treasure, color, n,
                    k, col, A, B):
    sum = 0
    if k == n:
        return 0

    # we have two options either
    # visit current city or skip that

    # check if color of this city
    # is equal to prev visited city
    if col== color[k]:
        sum += max(A * treasure[k] +
                MaxProfit(treasure, color, n,
                       k + 1, color[k], A, B),
                MaxProfit(treasure, color, n,
                            k + 1, col, A, B))
    else:
        sum += max(B * treasure[k] +                                       
               MaxProfit(treasure, color, n,
                        k + 1, color[k], A, B),
               MaxProfit(treasure, color, n,
                           k + 1, col, A, B))

    # return max of both options
    return sum

# Driver Code
A = -5
B= 7
treasure = [4, 8, 2, 9]
color = [2, 2, 6, 2]
n = len(color)

# Initially begin with color 0
print( MaxProfit(treasure, color,
                 n, 0, 0, A, B))

# This code is contributed
# by Shrikant13
```

## C#

```
using System;

class GFG
{

// k is current index and col is previous color.
static int MaxProfit(int []treasure, int []color, int n,
            int k, int col, int A, int B)
{
    int sum = 0;

    if (k == n) // base case
        return 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city is equal
    // to prev visited city
    if (col == color[k])
        sum += Math.Max(A * treasure[k] +
                MaxProfit(treasure, color, n,
                    k + 1, color[k], A, B),
                MaxProfit(treasure, color, n,
                        k + 1, col, A, B));
    else
        sum += Math.Max(B * treasure[k] +                                        
                MaxProfit(treasure, color, n,
                    k + 1, color[k], A, B),
            MaxProfit(treasure, color, n,
                        k + 1, col, A, B));

    // return max of both options
    return sum;
}

// Driver code
public static void Main(String[] args)
{

    int A = -5, B = 7;
    int []treasure = { 4, 8, 2, 9 };
    int []color = { 2, 2, 6, 2 };
    int n = color.Length;

    // Initially begin with color 0
    Console.Write(MaxProfit(treasure, color, n, 0, 0, A, B));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// k is current index and col is previous color.
function MaxProfit(treasure,color,n,k,col,A,B)
{
    let sum = 0;

    if (k == n) // base case
        return 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city is equal
    // to prev visited city
    if (col == color[k])
        sum += Math.max(A * treasure[k] +
                MaxProfit(treasure, color, n,
                    k + 1, color[k], A, B),
                MaxProfit(treasure, color, n,
                        k + 1, col, A, B));
    else
        sum += Math.max(B * treasure[k] +                                       
                MaxProfit(treasure, color, n,
                    k + 1, color[k], A, B),
            MaxProfit(treasure, color, n,
                        k + 1, col, A, B));

    // return max of both options
    return sum;
}

let A = -5, B = 7;
let treasure = [ 4, 8, 2, 9 ];
let color = [ 2, 2, 6, 2 ];
let n = color.length;

// Initially begin with color 0
document.write(MaxProfit(treasure, color, n, 0, 0, A, B));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
133
```

由于子问题被再次评估，该问题具有**重叠子问题**属性。

以下是基于**动态编程**的实现。

## C++

```
// A memoization based program to find maximum
// treasure that can be collected.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1001;

int dp[MAX][MAX];

// k is current index and col is previous color.
int MaxProfit(int treasure[], int color[], int n,
              int k, int col, int A, int B)
{
    if (k == n) // base case
        return dp[k][col] = 0;

    if (dp[k][col] != -1)
        return dp[k][col];

    int sum = 0;

    // we have two options
    // either visit current city or skip that

    if (col == color[k]) // check if color of this city is equal to prev visited city
        sum += max(A * treasure[k] +
               MaxProfit(treasure, color, n, k + 1,
                                     color[k], A, B), 
               MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));
    else
        sum += max(B * treasure[k] +
                MaxProfit(treasure, color, n, k + 1,
                                   color[k], A, B),
                MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));

    // return max of both options
    return dp[k][col] = sum;
}

int main()
{
    int A = -5, B = 7;
    int treasure[] = { 4, 8, 2, 9 };
    int color[] = { 2, 2, 6, 2 };
    int n = sizeof(color) / sizeof(color[0]);
    memset(dp, -1, sizeof(dp));
    cout << MaxProfit(treasure, color, n, 0, 0, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A memoization based program to find maximum
// treasure that can be collected.
import java.util.*;

class GFG
{

static int MAX = 1001;

static int [][]dp = new int[MAX][MAX];

// k is current index and col is previous color.
static int MaxProfit(int treasure[], int color[], int n,
            int k, int col, int A, int B)
{
    if (k == n) // base case
        return dp[k][col] = 0;

    if (dp[k][col] != -1)
        return dp[k][col];

    int sum = 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city
    // is equal to prev visited city
    if (col == color[k])
        sum += Math.max(A * treasure[k] +
            MaxProfit(treasure, color, n, k + 1,
                                    color[k], A, B),
            MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));
    else
        sum += Math.max(B * treasure[k] +
                MaxProfit(treasure, color, n, k + 1,
                                color[k], A, B),
                MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));

    // return max of both options
    return dp[k][col] = sum;
}

// Driver code
public static void main(String[] args)
{
    int A = -5, B = 7;
    int treasure[] = { 4, 8, 2, 9 };
    int color[] = { 2, 2, 6, 2 };
    int n = color.length;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < MAX; j++)
            dp[i][j] = -1;
    System.out.print(MaxProfit(treasure, color, n, 0, 0, A, B));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A memoization based program to find maximum
# treasure that can be collected.
MAX = 1001

dp = [[-1 for i in range(MAX)] for i in range(MAX)]

# k is current index and col is previous color.
def MaxProfit(treasure, color, n,k, col, A, B):
    if (k == n):

        # base case
        dp[k][col] = 0
        return dp[k][col]
    if (dp[k][col] != -1):
        return dp[k][col]

    summ = 0

    # we have two options
    # either visit current city or skip that
    if (col == color[k]):

        # check if color of this city is equal to prev visited city
        summ += max(A * treasure[k] + MaxProfit(treasure,
                color, n, k + 1,color[k], A, B),
                MaxProfit(treasure, color, n, k + 1, col, A, B))
    else:
        summ += max(B * treasure[k] + MaxProfit(treasure,
                color, n, k + 1,color[k], A, B),
                MaxProfit(treasure, color, n, k + 1, col, A, B))
    dp[k][col] = summ

    # return max of both options
    return dp[k][col]

# Driver code
A = -5
B = 7
treasure = [ 4, 8, 2, 9 ]
color = [ 2, 2, 6, 2 ]
n = len(color)
print(MaxProfit(treasure, color, n, 0, 0, A, B))

# This code is contributed by shubhamsingh10
```

## C#

```
// A memoization based program to find maximum
// treasure that can be collected.
using System;

class GFG
{

static int MAX = 1001;

static int [,]dp = new int[MAX, MAX];

// k is current index and col is previous color.
static int MaxProfit(int []treasure, int []color, int n,
            int k, int col, int A, int B)
{
    if (k == n) // base case
        return dp[k, col] = 0;

    if (dp[k, col] != -1)
        return dp[k, col];

    int sum = 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city
    // is equal to prev visited city
    if (col == color[k])
        sum += Math.Max(A * treasure[k] +
            MaxProfit(treasure, color, n, k + 1,
                                    color[k], A, B),
            MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));
    else
        sum += Math.Max(B * treasure[k] +
                MaxProfit(treasure, color, n, k + 1,
                                color[k], A, B),
                MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));

    // return max of both options
    return dp[k, col] = sum;
}

// Driver code
public static void Main(String[] args)
{
    int A = -5, B = 7;
    int []treasure = { 4, 8, 2, 9 };
    int []color = { 2, 2, 6, 2 };
    int n = color.Length;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < MAX; j++)
            dp[i, j] = -1;
    Console.Write(MaxProfit(treasure, color, n, 0, 0, A, B));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// A memoization based program to find maximum
// treasure that can be collected.

let MAX = 1001;
let dp = new Array(MAX);

for(let i = 0; i < MAX; i++)
{
    dp[i] = new Array(MAX);
    for(let j = 0; j < MAX; j++)
        dp[i][j] = -1;
}

// k is current index and col is previous color.
function MaxProfit(treasure, color, n, k, col, A, B)
{
    if (k == n) // base case
        return dp[k][col] = 0;

    if (dp[k][col] != -1)
        return dp[k][col];

    let sum = 0;

    // we have two options
    // either visit current city or skip that

    // check if color of this city
    // is equal to prev visited city
    if (col == color[k])
        sum += Math.max(A * treasure[k] +
            MaxProfit(treasure, color, n, k + 1,
                                    color[k], A, B),
            MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));
    else
        sum += Math.max(B * treasure[k] +
                MaxProfit(treasure, color, n, k + 1,
                                color[k], A, B),
                MaxProfit(treasure, color, n, k + 1,
                                        col, A, B));

    // return max of both options
    return dp[k][col] = sum;
}

// Driver code
let A = -5, B = 7;
let treasure=[4, 8, 2, 9];
let color=[2, 2, 6, 2];
let n = color.length;
document.write(MaxProfit(treasure, color, n, 0, 0, A, B));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
133
```