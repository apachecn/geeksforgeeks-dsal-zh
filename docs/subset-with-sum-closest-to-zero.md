# 总和最接近零的子集

> 原文:[https://www . geesforgeks . org/sum 最接近零的子集/](https://www.geeksforgeeks.org/subset-with-sum-closest-to-zero/)

给定由整数组成的数组“arr”，任务是找到非空子集，使其和最接近于零，即零和和之间的绝对差最小。
**例:**

> **输入:** arr[] = {2，2，2，-4}
> **输出:**0
> arr[0]+arr[1]+arr[3]= 0
> 这就是答案为零的原因。
> **输入:** arr[] = {1，1，1，1}
> **输出:** 1

一种简单的**方法是递归生成所有可能的子集，找到和最接近于零的子集。这种方法的时间复杂度将是 O(2^n).
更好的方法是在 [**伪多项式时间复杂度**](https://www.geeksforgeeks.org/pseudo-polynomial-in-algorithms/) 中使用 [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) 。
让我们假设我们选择的所有元素的总和到索引“i-1”是“S”。所以，从索引‘I’开始，我们要找到一个和最接近-S 的子集。
我们先定义 dp[i][S]。它是指数组“arr”的子数组{i，N-1}的子集与最接近“-S”的和的和。
现在，我们可以将‘I’包含在当前总和中，也可以不包含。因此，我们有两条可能的道路要走。如果我们包括“I”，当前总和将更新为 S+arr[i]，我们将求解索引“i+1”，即 dp[i+1][S+arr[i]]，否则我们将直接求解索引“i+1”。因此，所需的递归关系将是。** 

> **DP[I][s]= ret close(arr[I]+DP[I][s+arr[I]]，dp[i+1][s]，-s)；
> 其中 RetClose(a，b，c)返回 a if |a-c| < |b-c|否则返回 b**

**以下是上述方法的实现:** 

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

#define arrSize 51
#define maxSum 201
#define MAX 100
#define inf 999999

// Variable to store states of dp
int dp[arrSize][maxSum];
bool visit[arrSize][maxSum];

// Function to return the number closer to integer s
int RetClose(int a, int b, int s)
{
    if (abs(a - s) < abs(b - s))
        return a;
    else
        return b;
}

// To find the sum closest to zero
// Since sum can be negative, we will add MAX
// to it to make it positive
int MinDiff(int i, int sum, int arr[], int n)
{

    // Base cases
    if (i == n)
        return 0;
    // Checks if a state is already solved
    if (visit[i][sum + MAX])
        return dp[i][sum + MAX];
    visit[i][sum + MAX] = 1;

    // Recurrence relation
    dp[i][sum + MAX] =  RetClose(arr[i] +
                        MinDiff(i + 1, sum + arr[i], arr, n),
                        MinDiff(i + 1, sum, arr, n), -1 * sum);

    // Returning the value
    return dp[i][sum + MAX];
}

// Function to calculate the closest sum value
void FindClose(int arr[],int n)
{
    int ans=inf;

    // Calculate the Closest value for every
    // subarray arr[i-1:n]
    for (int i = 1; i <= n; i++)
        ans = RetClose(arr[i - 1] +
                MinDiff(i, arr[i - 1], arr, n), ans, 0);

    cout<<ans<<endl;
}

// Driver function
int main()
{
    // Input array
    int arr[] = { 25, -9, -10, -4, -7, -33 };
    int n = sizeof(arr) / sizeof(int);

    FindClose(arr,n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program for above approach
import java.io.*;

class GFG
{

static int arrSize = 51;
static int maxSum = 201;
static int MAX = 100;
static int inf = 999999;

// Variable to store states of dp
static int dp[][] = new int [arrSize][maxSum];
static int visit[][] = new int [arrSize][maxSum];

// Function to return the number
// closer to integer s
static int RetClose(int a, int b, int s)
{
    if (Math.abs(a - s) < Math.abs(b - s))
        return a;
    else
        return b;
}

// To find the sum closest to zero
// Since sum can be negative, we will add MAX
// to it to make it positive
static int MinDiff(int i, int sum,
                   int arr[], int n)
{

    // Base cases
    if (i == n)
        return 0;

    // Checks if a state is already solved
    if (visit[i][sum + MAX] > 0 )
        return dp[i][sum + MAX];
    visit[i][sum + MAX] = 1;

    // Recurrence relation
    dp[i][sum + MAX] = RetClose(arr[i] +
                        MinDiff(i + 1, sum + arr[i], arr, n),
                        MinDiff(i + 1, sum, arr, n), -1 * sum);

    // Returning the value
    return dp[i][sum + MAX];
}

// Function to calculate the closest sum value
static void FindClose(int arr[], int n)
{
    int ans = inf;

    // Calculate the Closest value for every
    // subarray arr[i-1:n]
    for (int i = 1; i <= n; i++)
        ans = RetClose(arr[i - 1] +
            MinDiff(i, arr[i - 1],
                       arr, n), ans, 0);

        System.out.println(ans);
}

// Driver Code
public static void main (String[] args)
{

    // Input array
    int arr[] = { 25, -9, -10, -4, -7, -33 };
    int n = arr.length;

    FindClose(arr,n);
}
}

// This code is contributed by ajit_00023@
```

## **蟒蛇 3**

```
# Python3 Code for above implementation
import numpy as np

arrSize = 51
maxSum = 201
MAX = 100
inf = 999999

# Variable to store states of dp
dp = np.zeros((arrSize,maxSum));
visit = np.zeros((arrSize,maxSum));

# Function to return the number closer to integer s
def RetClose(a, b, s) :

    if (abs(a - s) < abs(b - s)) :
        return a;
    else :
        return b;

# To find the sum closest to zero
# Since sum can be negative, we will add MAX
# to it to make it positive
def MinDiff(i, sum, arr, n) :

    # Base cases
    if (i == n) :
        return 0;

    # Checks if a state is already solved
    if (visit[i][sum + MAX]) :
        return dp[i][sum + MAX];

    visit[i][sum + MAX] = 1;

    # Recurrence relation
    dp[i][sum + MAX] = RetClose(arr[i] +
                        MinDiff(i + 1, sum + arr[i], arr, n),
                        MinDiff(i + 1, sum, arr, n), -1 * sum);

    # Returning the value
    return dp[i][sum + MAX];

# Function to calculate the closest sum value
def FindClose(arr,n) :

    ans=inf;

    # Calculate the Closest value for every
    # subarray arr[i-1:n]
    for i in range(1, n + 1) :
        ans = RetClose(arr[i - 1] +
                MinDiff(i, arr[i - 1], arr, n), ans, 0);

    print(ans);

# Driver function
if __name__ == "__main__" :

    # Input array
    arr = [ 25, -9, -10, -4, -7, -33 ];
    n = len(arr);

    FindClose(arr,n);

    # This code is contributed by AnkitRai01
```

## **C#**

```
// C# Program for above approach
using System;

class GFG
{

static int arrSize = 51;
static int maxSum = 201;
static int MAX = 100;
static int inf = 999999;

// Variable to store states of dp
static int [,]dp = new int [arrSize,maxSum];
static int [,]visit = new int [arrSize,maxSum];

// Function to return the number
// closer to integer s
static int RetClose(int a, int b, int s)
{
    if (Math.Abs(a - s) < Math.Abs(b - s))
        return a;
    else
        return b;
}

// To find the sum closest to zero
// Since sum can be negative, we will add MAX
// to it to make it positive
static int MinDiff(int i, int sum,
                int []arr, int n)
{

    // Base cases
    if (i == n)
        return 0;

    // Checks if a state is already solved
    if (visit[i,sum + MAX] > 0 )
        return dp[i,sum + MAX];
    visit[i,sum + MAX] = 1;

    // Recurrence relation
    dp[i,sum + MAX] = RetClose(arr[i] +
                        MinDiff(i + 1, sum + arr[i], arr, n),
                        MinDiff(i + 1, sum, arr, n), -1 * sum);

    // Returning the value
    return dp[i,sum + MAX];
}

// Function to calculate the closest sum value
static void FindClose(int []arr, int n)
{
    int ans = inf;

    // Calculate the Closest value for every
    // subarray arr[i-1:n]
    for (int i = 1; i <= n; i++)
        ans = RetClose(arr[i - 1] +
            MinDiff(i, arr[i - 1],
                    arr, n), ans, 0);

        Console.WriteLine(ans);
}

// Driver Code
public static void Main ()
{

    // Input array
    int []arr = { 25, -9, -10, -4, -7, -33 };
    int n = arr.Length;

    FindClose(arr,n);
}
}

// This code is contributed by  anuj_67..
```

## **java 描述语言**

```
<script>
    // Javascript Program for above approach

    let arrSize = 51;
    let maxSum = 201;
    let MAX = 100;
    let inf = 999999;

    // Variable to store states of dp
    let dp = new Array(arrSize);
    let visit = new Array(arrSize);

    for(let i = 0; i < arrSize; i++)
    {
        dp[i] = new Array(maxSum);
        visit[i] = new Array(maxSum);
        for(let j = 0; j < maxSum; j++)
        {
            dp[i][j] = 0;
            visit[i][j] = 0;
        }
    }

    // Function to return the number
    // closer to integer s
    function RetClose(a, b, s)
    {
        if (Math.abs(a - s) < Math.abs(b - s))
            return a;
        else
            return b;
    }

    // To find the sum closest to zero
    // Since sum can be negative, we will add MAX
    // to it to make it positive
    function MinDiff(i, sum, arr, n)
    {

        // Base cases
        if (i == n)
            return 0;

        // Checks if a state is already solved
        if (visit[i][sum + MAX] > 0 )
            return dp[i][sum + MAX];
        visit[i][sum + MAX] = 1;

        // Recurrence relation
        dp[i][sum + MAX] = RetClose(arr[i] +
                            MinDiff(i + 1, sum + arr[i], arr, n),
                            MinDiff(i + 1, sum, arr, n), -1 * sum);

        // Returning the value
        return dp[i][sum + MAX];
    }

    // Function to calculate the closest sum value
    function FindClose(arr, n)
    {
        let ans = inf;

        // Calculate the Closest value for every
        // subarray arr[i-1:n]
        for (let i = 1; i <= n; i++)
            ans = RetClose(arr[i - 1] +
                MinDiff(i, arr[i - 1],
                           arr, n), ans, 0);

            document.write(ans);
    }

    // Input array
    let arr = [ 25, -9, -10, -4, -7, -33 ];
    let n = arr.length;

    FindClose(arr,n);

</script>
```

****Output:** 

```
-1
```** 

****时间复杂度** : O(N*S)，其中 N 是数组中元素的个数，S 是数组中所有个数的和。**