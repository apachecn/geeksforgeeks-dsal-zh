# 零和子集数

> 原文:[https://www . geesforgeks . org/零和子集数/](https://www.geeksforgeeks.org/number-of-subsets-with-zero-sum/)

给定一个由整数组成的数组“arr”，任务是找到子集的数量，使它们的和等于零。还应考虑空子集。

**示例:**

> **输入:** arr[] = {2，2，-4}
> **输出:** 2
> 所有可能的子集:
> {} = 0
> { 2 } = 2
> { 2 } = 2
> {-4 } =-4
> { 2，2} = 4
> {2，-4} = -2
> {2，-4} = -4
> {2，2，-4} = 0
> 自，{ }
> **输入:** arr[] = {1，1，1，1}
> **输出:** 1
> {}是
> 和为 0 的唯一可能子集，因此 ans 等于 1。

一种简单的**方法是递归生成所有可能的子集，并计算总和等于 0 的子集的数量。这种方法的时间复杂度将是 O(2^n).**

**更好的方法是使用[](https://www.geeksforgeeks.org/dynamic-programming/)**动态编程。
让我们假设我们所选择的所有元素的总和达到索引‘I-1’是‘S’。因此，从索引‘I’开始，我们必须找到和等于-S 的子数组{i，N-1}的子集数。
让我们定义 dp[i][S]。它表示“arr”的子阵列{i，N-1}的子集数，其和等于“-S”。
如果我们在第 I 个指数，我们有两个选择，即把它包括在总和中或者离开它。
因此，所需的递归关系变为****

> ****DP[I][s]= DP[I+1][s+arr[I]]+DP[I+1][s]****

****下面是上述方法的实现:****

## ****C++****

```
**#include <bits/stdc++.h>
#define maxSum 100
#define arrSize 51
using namespace std;

// variable to store
// states of dp
int dp[arrSize][maxSum];
bool visit[arrSize][maxSum];

// To find the number of subsets with sum equal to 0
// Since S can be negative, we will maxSum
// to it to make it positive
int SubsetCnt(int i, int s, int arr[], int n)
{
    // Base cases
    if (i == n) {
        if (s == 0)
            return 1;
        else
            return 0;
    }

    // Returns the value if a state is already solved
    if (visit[i][s + maxSum])
        return dp[i][s + maxSum];

    // If the state is not visited, then continue
    visit[i][s + maxSum] = 1;

    // Recurrence relation
    dp[i][s + maxSum] = SubsetCnt(i + 1, s + arr[i], arr, n)
                        + SubsetCnt(i + 1, s, arr, n);

    // Returning the value
    return dp[i][s + maxSum];
}

// Driver function
int main()
{
    int arr[] = { 2, 2, 2, -4, -4 };
    int n = sizeof(arr) / sizeof(int);

    cout << SubsetCnt(0, 0, arr, n);
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java implementation of above approach
class GFG
{

    static int maxSum = 100;
    static int arrSize = 51;

    // variable to store
    // states of dp
    static int[][] dp = new int[arrSize][maxSum];
    static boolean[][] visit = new boolean[arrSize][maxSum];

    // To find the number of subsets with sum equal to 0
    // Since S can be negative, we will maxSum
    // to it to make it positive
    static int SubsetCnt(int i, int s, int arr[], int n)
    {
        // Base cases
        if (i == n)
        {
            if (s == 0)
            {
                return 1;
            }
            else
            {
                return 0;
            }
        }

        // Returns the value if a state is already solved
        if (visit[i][s + arrSize])
        {
            return dp[i][s + arrSize];
        }

        // If the state is not visited, then continue
        visit[i][s + arrSize] = true;

        // Recurrence relation
        dp[i][s + arrSize] = SubsetCnt(i + 1, s + arr[i], arr, n)
                + SubsetCnt(i + 1, s, arr, n);

        // Returning the value
        return dp[i][s + arrSize];
    }

    // Driver function
    public static void main(String[] args)
    {
        int arr[] = {2, 2, 2, -4, -4};
        int n = arr.length;

        System.out.println(SubsetCnt(0, 0, arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */**
```

## ****蟒蛇 3****

```
**# Python3 implementation of above approach
import numpy as np

maxSum = 100
arrSize = 51

# variable to store
# states of dp
dp = np.zeros((arrSize, maxSum));
visit = np.zeros((arrSize, maxSum));

# To find the number of subsets
# with sum equal to 0.
# Since S can be negative,
# we will maxSum to it
# to make it positive
def SubsetCnt(i, s, arr, n) :

    # Base cases
    if (i == n) :
        if (s == 0) :
            return 1;
        else :
            return 0;

    # Returns the value
    # if a state is already solved
    if (visit[i][s + arrSize]) :
        return dp[i][s + arrSize];

    # If the state is not visited,
    # then continue
    visit[i][s + arrSize] = 1;

    # Recurrence relation
    dp[i][s + arrSize ] = (SubsetCnt(i + 1, s + arr[i], arr, n) +
                           SubsetCnt(i + 1, s, arr, n));

    # Returning the value
    return dp[i][s + arrSize];

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 2, 2, -4, -4 ];
    n = len(arr);

    print(SubsetCnt(0, 0, arr, n));

# This code is contributed by AnkitRai01**
```

## ****C#****

```
**// C# implementation of above approach
using System;

class GFG
{

    static int maxSum = 100;
    static int arrSize = 51;

    // variable to store
    // states of dp
    static int [,]dp = new int[arrSize, maxSum];
    static bool [,]visit = new bool[arrSize, maxSum];

    // To find the number of subsets with sum equal to 0
    // Since S can be negative, we will maxSum
    // to it to make it positive
    static int SubsetCnt(int i, int s, int []arr, int n)
    {
        // Base cases
        if (i == n)
        {
            if (s == 0)
            {
                return 1;
            }
            else
            {
                return 0;
            }
        }

        // Returns the value if a state is already solved
        if (visit[i, s + arrSize])
        {
            return dp[i, s + arrSize];
        }

        // If the state is not visited, then continue
        visit[i, s + arrSize] = true;

        // Recurrence relation
        dp[i, s + arrSize] = SubsetCnt(i + 1, s + arr[i], arr, n)
                + SubsetCnt(i + 1, s, arr, n);

        // Returning the value
        return dp[i,s + arrSize];
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, 2, 2, -4, -4};
        int n = arr.Length;

        Console.WriteLine(SubsetCnt(0, 0, arr, n));
    }
}

// This code contributed by anuj_67..**
```

## ****java 描述语言****

```
**<script>

var maxSum = 100
var arrSize = 51

// variable to store
// states of dp
var dp = Array.from(Array(arrSize), ()=> Array(maxSum));
var visit = Array.from(Array(arrSize), ()=> Array(maxSum));

// To find the number of subsets with sum equal to 0
// Since S can be negative, we will maxSum
// to it to make it positive
function SubsetCnt(i, s, arr, n)
{
    // Base cases
    if (i == n) {
        if (s == 0)
            return 1;
        else
            return 0;
    }

    // Returns the value if a state is already solved
    if (visit[i][s + maxSum])
        return dp[i][s + maxSum];

    // If the state is not visited, then continue
    visit[i][s + maxSum] = 1;

    // Recurrence relation
    dp[i][s + maxSum] = SubsetCnt(i + 1, s + arr[i], arr, n)
                        + SubsetCnt(i + 1, s, arr, n);

    // Returning the value
    return dp[i][s + maxSum];
}

// Driver function
var arr = [2, 2, 2, -4, -4];
var n = arr.length;
document.write( SubsetCnt(0, 0, arr, n));

</script>**
```

******Output:** 

```
7
```**** 

******时间复杂度:** O(n*S)，其中 n 是数组中元素的个数，S 是所有元素的和。****