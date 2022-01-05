# 游戏的最佳策略|第 2 集

> 原文:[https://www . geesforgeks . org/a-game-set-2 的最优策略/](https://www.geeksforgeeks.org/optimal-strategy-for-a-game-set-2/)

问题陈述:考虑一排价值 v1 的 n 个硬币。。。vn，其中 n 是偶数。我们轮流和对手比赛。在每一回合中，玩家从该行中选择第一枚或最后一枚硬币，将其从该行中永久移除，并获得硬币的价值。确定如果我们先行动，我们肯定能赢的最大可能金额。
注意:对手和用户一样聪明。

让我们用几个例子来理解这个问题:
**1。** 5、3、7、10:用户收集最大值为 15(10 + 5)
**2。** 8、15、3、7:用户收集最大值为 22(7 + 15)

在每一步中选择最好的是否给出了最优解？
不是。在第二个例子中，游戏是这样结束的:

**1。**
……。用户选择 8。
……。对手选择 15。
……。用户选择 7。
……。对手选择 3。
用户采集的总值为 15(8 + 7)
**2。**
……。用户选择 7。
……。对手选择 8。
……。用户选择 15。
……。对手选择 3。
用户收集的总值为 22(7 + 15)
所以如果用户遵循第二种游戏状态，虽然第一招不是最好的，但可以收集最大值。

我们已经讨论了一种进行 4 次递归调用的方法。在这篇文章中，我们讨论了一种新的方法，它可以进行两次递归调用。
有两个选择:
**1。**用户选择价值 Vi 的第 I 枚硬币:对手选择(i+1)枚硬币或 jth 枚硬币。对手打算选择给用户留下最小价值的硬币。
即用户可以收集值 Vi+(Sum–Vi)–F(I+1，j，Sum–Vi)，其中 Sum 是从索引 I 到 j 的硬币的总和。表达式可以简化为 Sum–F(I+1，j，Sum–Vi)

![coinGame1](img/eaaec2c045cd5a6e4fcf301231528091.png)

**2。**用户选择价值 Vj 的第 j 枚硬币:对手要么选择第 I 枚硬币，要么选择(j-1)枚硬币。对手打算选择给用户留下最小价值的硬币。
即用户可以收集值 Vj+(Sum–Vj)–F(I，j-1，Sum–Vj)，其中 Sum 是从索引 I 到 j 的硬币总和。表达式可以简化为 Sum–F(I，j-1，Sum–Vj)

![coinGame2](img/f9d50e200f8f89802a80709b211e9e77.png)

以下是基于上述两个选择的递归解决方案。我们最多拿两个选择。

```
F(i, j)  represents the maximum value the user can collect from 
         i'th coin to j'th coin.
arr[]   represents the list of coins

    F(i, j)  = Max(Sum - F(i+1, j, Sum-arr[i]), 
                   Sum - F(i, j-1, Sum-arr[j])) 
Base Case
    F(i, j)  = max(arr[i], arr[j])  If j == i+1
```

**简单递归解**

## C++

```
// C++ program to find out maximum value from a
// given sequence of coins
#include <bits/stdc++.h>
using namespace std;

int oSRec(int arr[], int i, int j, int sum)
{
    if (j == i + 1)
        return max(arr[i], arr[j]);

    // For both of your choices, the opponent
    // gives you total sum minus maximum of
    // his value
    return max((sum - oSRec(arr, i + 1, j, sum - arr[i])),
               (sum - oSRec(arr, i, j - 1, sum - arr[j])));
}

// Returns optimal value possible that a player can
// collect from an array of coins of size n. Note
// than n must be even
int optimalStrategyOfGame(int* arr, int n)
{
    int sum = 0;
    sum = accumulate(arr, arr + n, sum);
    return oSRec(arr, 0, n - 1, sum);
}

// Driver program to test above function
int main()
{
    int arr1[] = { 8, 15, 3, 7 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    printf("%d\n", optimalStrategyOfGame(arr1, n));

    int arr2[] = { 2, 2, 2, 2 };
    n = sizeof(arr2) / sizeof(arr2[0]);
    printf("%d\n", optimalStrategyOfGame(arr2, n));

    int arr3[] = { 20, 30, 2, 2, 2, 10 };
    n = sizeof(arr3) / sizeof(arr3[0]);
    printf("%d\n", optimalStrategyOfGame(arr3, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out maximum value from a
// given sequence of coins
import java .io.*;

class GFG
{

    static int oSRec(int []arr, int i, int j, int sum)
    {
        if (j == i + 1)
            return Math.max(arr[i], arr[j]);

        // For both of your choices, the opponent
        // gives you total sum minus maximum of
        // his value
        return Math.max((sum - oSRec(arr, i + 1, j, sum - arr[i])),
                (sum - oSRec(arr, i, j - 1, sum - arr[j])));
    }

    // Returns optimal value possible that a player can
    // collect from an array of coins of size n. Note
    // than n must be even
    static int optimalStrategyOfGame(int[] arr, int n)
    {
        int sum = 0;
        for(int i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        return oSRec(arr, 0, n - 1, sum);
    }

    // Driver code
    static public void main (String[] args)
    {
        int []arr1 = { 8, 15, 3, 7 };
        int n = arr1.length;
        System.out.println(optimalStrategyOfGame(arr1, n));

        int []arr2 = { 2, 2, 2, 2 };
        n = arr2.length;
        System.out.println(optimalStrategyOfGame(arr2, n));

        int []arr3 = { 20, 30, 2, 2, 2, 10 };
        n = arr3.length ;
        System.out.println(optimalStrategyOfGame(arr3, n));
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# python3 program to find out maximum value from a
# given sequence of coins

def oSRec (arr, i, j, Sum):

    if (j == i + 1):
        return max(arr[i], arr[j])

    # For both of your choices, the opponent
    # gives you total Sum minus maximum of
    # his value
    return max((Sum - oSRec(arr, i + 1, j, Sum - arr[i])),
                (Sum - oSRec(arr, i, j - 1, Sum - arr[j])))

# Returns optimal value possible that a player can
# collect from an array of coins of size n. Note
# than n must be even
def optimalStrategyOfGame(arr, n):

    Sum = 0
    Sum = sum(arr)
    return oSRec(arr, 0, n - 1, Sum)

# Driver code

arr1= [ 8, 15, 3, 7]
n = len(arr1)
print(optimalStrategyOfGame(arr1, n))

arr2= [ 2, 2, 2, 2 ]
n = len(arr2)
print(optimalStrategyOfGame(arr2, n))

arr3= [ 20, 30, 2, 2, 2, 10 ]
n = len(arr3)
print(optimalStrategyOfGame(arr3, n))

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to find out maximum value from a
// given sequence of coins
using System;
class GFG
{
    static int oSRec(int []arr, int i,
                     int j, int sum)
    {
        if (j == i + 1)
            return Math.Max(arr[i], arr[j]);

        // For both of your choices, the opponent
        // gives you total sum minus maximum of
        // his value
        return Math.Max((sum - oSRec(arr, i + 1, j,
                                     sum - arr[i])),
                        (sum - oSRec(arr, i, j - 1,
                                     sum - arr[j])));
    }

    // Returns optimal value possible that a player can
    // collect from an array of coins of size n. Note
    // than n must be even
    static int optimalStrategyOfGame(int[] arr, int n)
    {
        int sum = 0;
        for(int i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        return oSRec(arr, 0, n - 1, sum);
    }

    // Driver code
    static public void Main ()
    {
        int []arr1 = { 8, 15, 3, 7 };
        int n = arr1.Length;
        Console.WriteLine(optimalStrategyOfGame(arr1, n));

        int []arr2 = { 2, 2, 2, 2 };
        n = arr2.Length;
        Console.WriteLine(optimalStrategyOfGame(arr2, n));

        int []arr3 = { 20, 30, 2, 2, 2, 10 };
        n = arr3.Length;
        Console.WriteLine(optimalStrategyOfGame(arr3, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to find out maximum value from a
    // given sequence of coins

    function oSRec(arr, i, j, sum)
    {
        if (j == i + 1)
            return Math.max(arr[i], arr[j]);

        // For both of your choices, the opponent
        // gives you total sum minus maximum of
        // his value
        return Math.max((sum - oSRec(arr, i + 1, j,
                                     sum - arr[i])),
                        (sum - oSRec(arr, i, j - 1,
                                     sum - arr[j])));
    }

    // Returns optimal value possible that a player can
    // collect from an array of coins of size n. Note
    // than n must be even
    function optimalStrategyOfGame(arr, n)
    {
        let sum = 0;
        for(let i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        return oSRec(arr, 0, n - 1, sum);
    }

    let arr1 = [ 8, 15, 3, 7 ];
    let n = arr1.length;
    document.write(optimalStrategyOfGame(arr1, n) + "</br>");

    let arr2 = [ 2, 2, 2, 2 ];
    n = arr2.length;
    document.write(optimalStrategyOfGame(arr2, n) + "</br>");

    let arr3 = [ 20, 30, 2, 2, 2, 10 ];
    n = arr3.length;
    document.write(optimalStrategyOfGame(arr3, n) + "</br>");

</script>
```

**Output:** 

```
22
4
42
```

**基于记忆的解决方案**

## C++

```
// C++ program to find out maximum value from a
// given sequence of coins
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

int memo[MAX][MAX];

int oSRec(int arr[], int i, int j, int sum)
{
    if (j == i + 1)
        return max(arr[i], arr[j]);

    if (memo[i][j] != -1)
        return memo[i][j];

    // For both of your choices, the opponent
    // gives you total sum minus maximum of
    // his value
    memo[i][j] = max((sum - oSRec(arr, i + 1, j, sum - arr[i])),
                     (sum - oSRec(arr, i, j - 1, sum - arr[j])));

    return memo[i][j];
}

// Returns optimal value possible that a player can
// collect from an array of coins of size n. Note
// than n must be even
int optimalStrategyOfGame(int* arr, int n)
{
    // Compute sum of elements
    int sum = 0;
    sum = accumulate(arr, arr + n, sum);

    // Initialize memoization table
    memset(memo, -1, sizeof(memo));

    return oSRec(arr, 0, n - 1, sum);
}

// Driver program to test above function
int main()
{
    int arr1[] = { 8, 15, 3, 7 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    printf("%d\n", optimalStrategyOfGame(arr1, n));

    int arr2[] = { 2, 2, 2, 2 };
    n = sizeof(arr2) / sizeof(arr2[0]);
    printf("%d\n", optimalStrategyOfGame(arr2, n));

    int arr3[] = { 20, 30, 2, 2, 2, 10 };
    n = sizeof(arr3) / sizeof(arr3[0]);
    printf("%d\n", optimalStrategyOfGame(arr3, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out maximum value from a
// given sequence of coins
import java.util.*;
class GFG{

static int MAX = 100;

static int [][]memo = new int[MAX][MAX];

static int oSRec(int arr[], int i,
                 int j, int sum)
{
    if (j == i + 1)
        return Math.max(arr[i], arr[j]);

    if (memo[i][j] != -1)
        return memo[i][j];

    // For both of your choices, the opponent
    // gives you total sum minus maximum of
    // his value
    memo[i][j] = Math.max((sum - oSRec(arr, i + 1, j,
                                       sum - arr[i])),
                           (sum - oSRec(arr, i, j - 1,
                                       sum - arr[j])));

    return memo[i][j];
}

static int accumulate(int[] arr,
                      int start, int end)
{
    int sum=0;
    for(int i= 0; i < arr.length; i++)
        sum += arr[i];
    return sum;
}

// Returns optimal value possible that a player can
// collect from an array of coins of size n. Note
// than n must be even
static int optimalStrategyOfGame(int []arr, int n)
{
    // Compute sum of elements
    int sum = 0;
    sum = accumulate(arr, 0, n);

    // Initialize memoization table
    for (int j = 0; j < MAX; j++)
    {
        for (int k = 0; k < MAX; k++)
            memo[j][k] = -1;
    }

    return oSRec(arr, 0, n - 1, sum);
}

// Driver Code
public static void main(String[] args)
{
    int arr1[] = { 8, 15, 3, 7 };
    int n = arr1.length;
    System.out.printf("%d\n",
               optimalStrategyOfGame(arr1, n));

    int arr2[] = { 2, 2, 2, 2 };
    n = arr2.length;
    System.out.printf("%d\n",
               optimalStrategyOfGame(arr2, n));

    int arr3[] = { 20, 30, 2, 2, 2, 10 };
    n = arr3.length;
    System.out.printf("%d\n",
               optimalStrategyOfGame(arr3, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to find out maximum value
# from a given sequence of coins
MAX = 100

memo = [[0 for i in range(MAX)]
           for j in range(MAX)]

def oSRec(arr, i, j, Sum):

    if (j == i + 1):
        return max(arr[i], arr[j])

    if (memo[i][j] != -1):
        return memo[i][j]

    # For both of your choices, the opponent
    # gives you total sum minus maximum of
    # his value
    memo[i][j] = max((Sum - oSRec(arr, i + 1, j,
                                     Sum - arr[i])),
                     (Sum - oSRec(arr, i, j - 1,
                                        Sum - arr[j])))

    return memo[i][j]

# Returns optimal value possible that a
# player can collect from an array of
# coins of size n. Note than n must
# be even
def optimalStrategyOfGame(arr, n):

    # Compute sum of elements
    Sum = 0
    Sum = sum(arr)

    # Initialize memoization table
    for j in range(MAX):
        for k in range(MAX):
            memo[j][k] = -1

    return oSRec(arr, 0, n - 1, Sum)

# Driver Code
arr1 = [ 8, 15, 3, 7 ]
n = len(arr1)
print(optimalStrategyOfGame(arr1, n))

arr2 = [ 2, 2, 2, 2 ]
n = len(arr2)
print(optimalStrategyOfGame(arr2, n))

arr3 = [ 20, 30, 2, 2, 2, 10 ]
n = len(arr3)
print(optimalStrategyOfGame(arr3, n))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find out maximum value from a
// given sequence of coins
using System;
class GFG{

  static int MAX = 100;

  static int[,] memo = new int[MAX, MAX];

  static int oSRec(int []arr, int i,
                   int j, int sum)
  {
    if (j == i + 1)
      return Math.Max(arr[i], arr[j]);

    if (memo[i, j] != -1)
      return memo[i, j];

    // For both of your choices, the opponent
    // gives you total sum minus maximum of
    // his value
    memo[i, j] = Math.Max((sum - oSRec(arr, i + 1, j,
                                       sum - arr[i])),
                          (sum - oSRec(arr, i, j - 1,
                                       sum - arr[j])));

    return memo[i,j];
  }

  static int accumulate(int[] arr, int start,
                        int end)
  {
    int sum = 0;
    for (int i = 0; i < arr.Length; i++)
      sum += arr[i];
    return sum;
  }

  // Returns optimal value possible that a player can
  // collect from an array of coins of size n. Note
  // than n must be even
  static int optimalStrategyOfGame(int[] arr, int n)
  {
    // Compute sum of elements
    int sum = 0;
    sum = accumulate(arr, 0, n);

    // Initialize memoization table
    for (int j = 0; j < MAX; j++)
    {
      for (int k = 0; k < MAX; k++)
        memo[j, k] = -1;
    }

    return oSRec(arr, 0, n - 1, sum);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr1 = { 8, 15, 3, 7 };
    int n = arr1.Length;
    Console.Write("{0}\n", optimalStrategyOfGame(arr1, n));

    int []arr2 = { 2, 2, 2, 2 };
    n = arr2.Length;
    Console.Write("{0}\n", optimalStrategyOfGame(arr2, n));

    int []arr3 = { 20, 30, 2, 2, 2, 10 };
    n = arr3.Length;
    Console.Write("{0}\n", optimalStrategyOfGame(arr3, n));
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program to find out maximum
// value from a given sequence of coins
let MAX = 100;
let memo = new Array(MAX);
for(let i = 0; i < MAX; i++)
{
    memo[i] = new Array(MAX);
    for(let j = 0; j < MAX; j++)
    {
        memo[i][j] = 0;
    }
}

function oSRec(arr, i, j, sum)
{
    if (j == i + 1)
        return Math.max(arr[i], arr[j]);

    if (memo[i][j] != -1)
        return memo[i][j];

    // For both of your choices, the opponent
    // gives you total sum minus maximum of
    // his value
    memo[i][j] = Math.max((sum - oSRec(arr, i + 1, j,
                                       sum - arr[i])),
                          (sum - oSRec(arr, i, j - 1,
                                       sum - arr[j])));

    return memo[i][j];
}

function accumulate(arr, start, end)
{
     let sum = 0;
    for(let i = 0; i < arr.length; i++)
        sum += arr[i];

    return sum;
}

// Returns optimal value possible that a player can
// collect from an array of coins of size n. Note
// than n must be even
function optimalStrategyOfGame(arr, n)
{

    // Compute sum of elements
    let sum = 0;
    sum = accumulate(arr, 0, n);

    // Initialize memoization table
    for(let j = 0; j < MAX; j++)
    {
        for(let k = 0; k < MAX; k++)
            memo[j][k] = -1;
    }
    return oSRec(arr, 0, n - 1, sum);
}

// Driver Code
let arr1 = [ 8, 15, 3, 7 ];
let n = arr1.length;
document.write(
    optimalStrategyOfGame(arr1, n) + "<br>");

let arr2 = [ 2, 2, 2, 2 ];
n = arr2.length;
document.write(
    optimalStrategyOfGame(arr2, n) + "<br>");

let arr3 = [ 20, 30, 2, 2, 2, 10 ];
n = arr3.length;
document.write(
    optimalStrategyOfGame(arr3, n) + "<br>");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
22
4
42
```

这种方法由 **Alind** 提出。