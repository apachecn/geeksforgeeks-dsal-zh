# 和可被 M 整除的子集数|集合 2

> 原文:[https://www . geesforgeks . org/sum 可被 m-set-2 整除的子集数/](https://www.geeksforgeeks.org/number-of-subsets-with-sum-divisible-by-m-set-2/)

给定一个由 **N** 个整数和一个整数 **M** 组成的数组 **arr[]** ，任务是找到非空子序列的数量，使得子序列的和可被 **M** 整除。

**示例:**

> **输入:** arr[] = {1，2，3}，M = 1
> **输出:** 7
> 该数组非空子集个数为 7。
> 由于 m = 1，m 将划分所有可能的子集。
> **输入:** arr[] = {1，2，3}，M = 2
> **输出:** 3

**方法:**时间复杂度为 **O(N * SUM)** 的基于动态规划的方法，其中 **N** 是数组的长度， **SUM** 是所有数组元素的和，该方法已在本文[中讨论过。
在本文中，将讨论对之前方法的改进。代替总和作为 DP 的状态之一，(总和% m)将被用作 DP 的状态之一，因为它是足够的。因此，时间复杂度归结为 O(m * N)。
复发关系:](https://www.geeksforgeeks.org/number-of-subsets-with-sum-divisible-by-m/)

> DP[I][curl]= DP[I+1][(curl+arr[I])% m]+DP[I+1][curl]

让我们现在定义状态， **dp[i][curr]** 简单地表示子阵列的子集数量 **arr[i…N-1]** ，使得**(其元素+ curr 之和)% m = 0** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define maxN 20
#define maxM 10

// To store the states of DP
int dp[maxN][maxM];
bool v[maxN][maxM];

// Function to find the required count
int findCnt(int* arr, int i, int curr, int n, int m)
{
    // Base case
    if (i == n) {
        if (curr == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][curr])
        return dp[i][curr];

    // Setting the state as solved
    v[i][curr] = 1;

    // Recurrence relation
    return dp[i][curr] = findCnt(arr, i + 1,
                                 curr, n, m)
                         + findCnt(arr, i + 1,
                                   (curr + arr[i]) % m,
                                   n, m);
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 3, 3 };
    int n = sizeof(arr) / sizeof(int);
    int m = 6;

    cout << findCnt(arr, 0, 0, n, m) - 1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int maxN = 20;
static int maxM = 10;

// To store the states of DP
static int [][]dp = new int[maxN][maxM];
static boolean [][]v = new boolean[maxN][maxM];

// Function to find the required count
static int findCnt(int[] arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        if (curr == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][curr])
        return dp[i][curr];

    // Setting the state as solved
    v[i][curr] = true;

    // Recurrence relation
    return dp[i][curr] = findCnt(arr, i + 1,
                                 curr, n, m) +
                         findCnt(arr, i + 1,
                                (curr + arr[i]) % m,
                                 n, m);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 3, 3, 3 };
    int n = arr.length;
    int m = 6;

    System.out.println(findCnt(arr, 0, 0, n, m) - 1);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
maxN = 20
maxM = 10

# To store the states of DP
dp = [[0 for i in range(maxN)]
         for i in range(maxM)]
v = [[0 for i in range(maxN)]
        for i in range(maxM)]

# Function to find the required count
def findCnt(arr, i, curr, n, m):

    # Base case
    if (i == n):
        if (curr == 0):
            return 1
        else:
            return 0

    # If the state has been solved before
    # return the value of the state
    if (v[i][curr]):
        return dp[i][curr]

    # Setting the state as solved
    v[i][curr] = 1

    # Recurrence relation
    dp[i][curr] = findCnt(arr, i + 1,
                          curr, n, m) + \
                  findCnt(arr, i + 1,
                         (curr + arr[i]) % m, n, m)
    return dp[i][curr]

# Driver code
arr = [3, 3, 3, 3]
n = len(arr)
m = 6

print(findCnt(arr, 0, 0, n, m) - 1)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int maxN = 20;
    static int maxM = 10;

    // To store the states of DP
    static int [,]dp = new int[maxN, maxM];
    static bool [,]v = new bool[maxN, maxM];

    // Function to find the required count
    static int findCnt(int[] arr, int i,
                       int curr, int n, int m)
    {
        // Base case
        if (i == n)
        {
            if (curr == 0)
                return 1;
            else
                return 0;
        }

        // If the state has been solved before
        // return the value of the state
        if (v[i, curr])
            return dp[i, curr];

        // Setting the state as solved
        v[i, curr] = true;

        // Recurrence relation
        return dp[i, curr] = findCnt(arr, i + 1,
                                     curr, n, m) +
                             findCnt(arr, i + 1,
                                    (curr + arr[i]) % m, n, m);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 3, 3, 3, 3 };
        int n = arr.Length;
        int m = 6;

        Console.WriteLine(findCnt(arr, 0, 0, n, m) - 1);
    }
}

// This code is contributed by kanugargng
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxN = 20
var maxM = 10

// To store the states of DP
var dp = Array.from(Array(maxN), () => Array(maxM));
var v = Array.from(Array(maxN), () => Array(maxM));

// Function to find the required count
function findCnt(arr, i, curr, n, m)
{
    // Base case
    if (i == n) {
        if (curr == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][curr])
        return dp[i][curr];

    // Setting the state as solved
    v[i][curr] = 1;

    // Recurrence relation
    dp[i][curr] = findCnt(arr, i + 1,
                                 curr, n, m)
                         + findCnt(arr, i + 1,
                                   (curr + arr[i]) % m,
                                   n, m);

    return dp[i][curr];
}

// Driver code
var arr = [3, 3, 3, 3];
var n = arr.length;
var m = 6;
document.write( findCnt(arr, 0, 0, n, m) - 1);

</script>
```

**Output:** 

```
7
```