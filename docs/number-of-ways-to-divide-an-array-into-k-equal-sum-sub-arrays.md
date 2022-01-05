# 将一个数组划分为 K 个等和子数组的方式数

> 原文:[https://www . geeksforgeeks . org/将数组划分为 k 个等和子数组的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-divide-an-array-into-k-equal-sum-sub-arrays/)

给定一个整数 **K** 和一个由 **N** 个整数组成的数组**arr【】**，任务是找出将数组拆分成长度非零的 **K** 等份和子数组的方法。

**示例:**

> **输入:** arr[] = {0，0，0，0}，K = 3
> **输出:** 3
> 所有可能的方式为:
> {{0}、{0}、{0，0}}
> {{0}、{0，0}、{0}}
> {{0，0}、{0}、{0}}
> **输入:** arr[] = {1，-1，-1}，K = 0

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。下面是我们的算法:

1.  求数组所有元素的和，存储在变量 **SUM** 中。
    在进行第 2 步之前，让我们先了解一下 DP 的状态。
    为此，想象放条将阵列分成 **K** 等份。所以，我们总共要放**K–1**条。
    因此，我们的 dp 状态将包含 2 个术语。
    *   **I**–我们当前所在元素的索引。
    *   **CK**–我们已经插入的条数+ 1。
2.  调用递归函数**I = 0****CK = 1**，递归关系为:

> 情况 1:向上指数 I 之和等于((SUM)/k)* CK
> **DP[I][CK]= DP[I+1][CK]+DP[I+1][CK+1]**
> 情况 2:向上指数 I 之和不等于((SUM)/k)* CK
> **DP[I][CK]= DP[I+1][CK]**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define max_size 20
#define max_k 20
using namespace std;

// Array to store the states of DP
int dp[max_size][max_k];

// Array to check if a
// state has been solved before
bool v[max_size][max_k];

// To store the sum of
// the array elements
int sum = 0;

// Function to find the sum of
// all the array elements
void findSum(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        sum += arr[i];
}

// Function to return the number of ways
int cntWays(int arr[], int i, int ck,
            int k, int n, int curr_sum)
{
    // If sum is not divisible by k
    // answer will be zero
    if (sum % k != 0)
        return 0;
    if (i != n and ck == k + 1)
        return 0;

    // Base case
    if (i == n) {
        if (ck == k + 1)
            return 1;
        else
            return 0;
    }

    // To check if a state
    // has been solved before
    if (v[i][ck])
        return dp[i][ck];

    // Sum of all the numbers from the beginning
    // of the array
    curr_sum += arr[i];

    // Setting the current state as solved
    v[i][ck] = 1;

    // Recurrence relation
    dp[i][ck] = cntWays(arr, i + 1, ck, k, n, curr_sum);
    if (curr_sum == (sum / k) * ck)
        dp[i][ck] += cntWays(arr, i + 1, ck + 1, k, n, curr_sum);

    // Returning solved state
    return dp[i][ck];
}

// Driver code
int main()
{
    int arr[] = { 1, -1, 1, -1, 1, -1 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    // Function call to find the
    // sum of the array elements
    findSum(arr, n);

    // Print the number of ways
    cout << cntWays(arr, 0, 1, k, n, 0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int max_size= 20;
static int max_k =20;

// Array to store the states of DP
static int [][]dp = new int[max_size][max_k];

// Array to check if a
// state has been solved before
static boolean [][]v = new boolean[max_size][max_k];

// To store the sum of
// the array elements
static int sum = 0;

// Function to find the sum of
// all the array elements
static void findSum(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        sum += arr[i];
}

// Function to return the number of ways
static int cntWays(int arr[], int i, int ck,
            int k, int n, int curr_sum)
{
    // If sum is not divisible by k
    // answer will be zero
    if (sum % k != 0)
        return 0;
    if (i != n && ck == k + 1)
        return 0;

    // Base case
    if (i == n)
    {
        if (ck == k + 1)
            return 1;
        else
            return 0;
    }

    // To check if a state
    // has been solved before
    if (v[i][ck])
        return dp[i][ck];

    // Sum of all the numbers from the beginning
    // of the array
    curr_sum += arr[i];

    // Setting the current state as solved
    v[i][ck] = true;

    // Recurrence relation
    dp[i][ck] = cntWays(arr, i + 1, ck, k, n, curr_sum);
    if (curr_sum == (sum / k) * ck)
        dp[i][ck] += cntWays(arr, i + 1, ck + 1, k, n, curr_sum);

    // Returning solved state
    return dp[i][ck];
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, -1, 1, -1, 1, -1 };
    int n = arr.length;
    int k = 2;

    // Function call to find the
    // sum of the array elements
    findSum(arr, n);

    // Print the number of ways
    System.out.println(cntWays(arr, 0, 1, k, n, 0));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

max_size = 20
max_k = 20

# Array to store the states of DP
dp = np.zeros((max_size,max_k));

# Array to check if a
# state has been solved before
v = np.zeros((max_size,max_k));

# To store the sum of
# the array elements
sum = 0;

# Function to find the sum of
# all the array elements
def findSum(arr, n) :
    global sum
    for i in range(n) :
        sum += arr[i];

# Function to return the number of ways
def cntWays(arr, i, ck, k, n,  curr_sum) :

    # If sum is not divisible by k
    # answer will be zero
    if (sum % k != 0) :
        return 0;
    if (i != n and ck == k + 1) :
        return 0;

    # Base case
    if (i == n) :
        if (ck == k + 1) :
            return 1;
        else :
            return 0;

    # To check if a state
    # has been solved before
    if (v[i][ck]) :
        return dp[i][ck];

    # Sum of all the numbers from the beginning
    # of the array
    curr_sum += arr[i];

    # Setting the current state as solved
    v[i][ck] = 1;

    # Recurrence relation
    dp[i][ck] = cntWays(arr, i + 1, ck, k, n, curr_sum);
    if (curr_sum == (sum / k) * ck)  :
        dp[i][ck] += cntWays(arr, i + 1, ck + 1, k, n, curr_sum);

    # Returning solved state
    return dp[i][ck];

# Driver code
if __name__ == "__main__" :

    arr = [ 1, -1, 1, -1, 1, -1 ];
    n = len(arr);
    k = 2;

    # Function call to find the
    # sum of the array elements
    findSum(arr, n);

    # Print the number of ways
    print(cntWays(arr, 0, 1, k, n, 0));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;    

class GFG
{

static int max_size= 20;
static int max_k =20;

// Array to store the states of DP
static int [,]dp = new int[max_size, max_k];

// Array to check if a
// state has been solved before
static Boolean [,]v = new Boolean[max_size, max_k];

// To store the sum of
// the array elements
static int sum = 0;

// Function to find the sum of
// all the array elements
static void findSum(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        sum += arr[i];
}

// Function to return the number of ways
static int cntWays(int []arr, int i, int ck,
            int k, int n, int curr_sum)
{
    // If sum is not divisible by k
    // answer will be zero
    if (sum % k != 0)
        return 0;
    if (i != n && ck == k + 1)
        return 0;

    // Base case
    if (i == n)
    {
        if (ck == k + 1)
            return 1;
        else
            return 0;
    }

    // To check if a state
    // has been solved before
    if (v[i, ck])
        return dp[i, ck];

    // Sum of all the numbers from the beginning
    // of the array
    curr_sum += arr[i];

    // Setting the current state as solved
    v[i, ck] = true;

    // Recurrence relation
    dp[i,ck] = cntWays(arr, i + 1, ck, k, n, curr_sum);
    if (curr_sum == (sum / k) * ck)
        dp[i, ck] += cntWays(arr, i + 1, ck + 1, k, n, curr_sum);

    // Returning solved state
    return dp[i, ck];
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, -1, 1, -1, 1, -1 };
    int n = arr.Length;
    int k = 2;

    // Function call to find the
    // sum of the array elements
    findSum(arr, n);

    // Print the number of ways
    Console.WriteLine(cntWays(arr, 0, 1, k, n, 0));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var max_size = 20;
var max_k = 20

// Array to store the states of DP
var dp = Array.from(Array(max_size), ()=> Array(max_k));

// Array to check if a
// state has been solved before
var v = Array.from(Array(max_size), ()=> Array(max_k));

// To store the sum of
// the array elements
var sum = 0;

// Function to find the sum of
// all the array elements
function findSum(arr, n)
{
    for (var i = 0; i < n; i++)
        sum += arr[i];
}

// Function to return the number of ways
function cntWays(arr, i, ck, k, n, curr_sum)
{
    // If sum is not divisible by k
    // answer will be zero
    if (sum % k != 0)
        return 0;
    if (i != n && ck == k + 1)
        return 0;

    // Base case
    if (i == n) {
        if (ck == k + 1)
            return 1;
        else
            return 0;
    }

    // To check if a state
    // has been solved before
    if (v[i][ck])
        return dp[i][ck];

    // Sum of all the numbers from the beginning
    // of the array
    curr_sum += arr[i];

    // Setting the current state as solved
    v[i][ck] = 1;

    // Recurrence relation
    dp[i][ck] = cntWays(arr, i + 1, ck, k, n, curr_sum);
    if (curr_sum == (sum / k) * ck)
        dp[i][ck] += cntWays(arr, i + 1, ck + 1, k, n, curr_sum);

    // Returning solved state
    return dp[i][ck];
}

// Driver code
var arr = [1, -1, 1, -1, 1, -1];
var n = arr.length;
var k = 2;
// Function call to find the
// sum of the array elements
findSum(arr, n);
// Print the number of ways
document.write( cntWays(arr, 0, 1, k, n, 0));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n*k)