# 数组所有子集的子集之和| O(N)

> 原文:[https://www . geeksforgeeks . org/阵列上所有子集的子集总和/](https://www.geeksforgeeks.org/sum-of-subsets-of-all-the-subsets-of-an-array-on/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找出该数组所有子集的子集的总和。
**例:**

> **输入:** arr[] = {1，1}
> **输出:** 6
> 所有可能的子集:
> **a) {} : 0**
> 该子集
> 的所有可能子集将为{}，Sum = 0
> **b){1}:1**
> 该子集
> 的所有可能子集将为{}和{ 1 }， Sum = 0+1 = 1
> **c){1}:1**
> 该子集
> 的所有可能子集将为{}和{1}，Sum = 0 + 1 = 1
> **d) {1，1} : 4**
> 该子集
> 的所有可能子集将为{}、{1}、{1}和{ 1，1 }，Sum = 0+1+2 = 4
> 因此，ans = 0 + 1

**方法:**本文将讨论一种具有 **O(N)** 时间复杂度的方法来解决给定的问题。
关键是观察一个元素在所有子集中重复的次数。
把视野放大。众所周知，每个元素在子集和中会出现**2<sup>(N–1)</sup>**次。现在，让我们进一步放大视图，看看计数如何随子集大小而变化。
每个包含它的索引都有**<sup>N–1</sup>C<sub>K–1</sub>**大小子集 **K** 。
元素对尺寸子集 **K** 的贡献将等于其值的**2<sup>(K–1)</sup>**倍。因此，一个元素对所有长度子集 **K** 的总贡献将等于所有子集之间的**<sup>N–1</sup>C<sub>K–1</sub>* 2<sup>(K–1)</sup>**
总贡献将等于:

> <sup>N–1</sup>C<sub>N–1</sub>* 2<sup>(N–1)</sup>+<sup>N–1</sup>C<sub>N–2</sub>* 2<sup>(N–2</sup>+<sup>N–1</sup>C<sub>N–3</sub>* 2<sup>(N–3)</sup>+…+<sup>N–1</sup>C

现在，最终答案中每个元素的贡献是已知的。所以，把它乘以数组中所有元素的和，就会得到所需的答案。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define maxN 10

// To store factorial values
int fact[maxN];

// Function to return ncr
int ncr(int n, int r)
{
    return (fact[n] / fact[r]) / fact[n - r];
}

// Function to return the required sum
int findSum(int* arr, int n)
{
    // Initialising factorial
    fact[0] = 1;
    for (int i = 1; i < n; i++)
        fact[i] = i * fact[i - 1];

    // Multiplier
    int mul = 0;

    // Finding the value of multipler
    // according to the formula
    for (int i = 0; i <= n - 1; i++)
        mul += (int)pow(2, i) * ncr(n - 1, i);

    // To store the final answer
    int ans = 0;

    // Calculate the final answer
    for (int i = 0; i < n; i++)
        ans += mul * arr[i];

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << findSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int maxN = 10;

// To store factorial values
static int []fact = new int[maxN];

// Function to return ncr
static int ncr(int n, int r)
{
    return (fact[n] / fact[r]) / fact[n - r];
}

// Function to return the required sum
static int findSum(int[] arr, int n)
{
    // Initialising factorial
    fact[0] = 1;
    for (int i = 1; i < n; i++)
        fact[i] = i * fact[i - 1];

    // Multiplier
    int mul = 0;

    // Finding the value of multipler
    // according to the formula
    for (int i = 0; i <= n - 1; i++)
        mul += (int)Math.pow(2, i) * ncr(n - 1, i);

    // To store the final answer
    int ans = 0;

    // Calculate the final answer
    for (int i = 0; i < n; i++)
        ans += mul * arr[i];

    return ans;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 1 };
    int n = arr.length;

    System.out.println(findSum(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
maxN = 10

# To store factorial values
fact = [0]*maxN;

# Function to return ncr
def ncr(n, r) :

    return (fact[n] // fact[r]) // fact[n - r];

# Function to return the required sum
def findSum(arr, n) :

    # Initialising factorial
    fact[0] = 1;
    for i in range(1, n) :
        fact[i] = i * fact[i - 1];

    # Multiplier
    mul = 0;

    # Finding the value of multipler
    # according to the formula
    for i in range(n) :
        mul += (2 ** i) * ncr(n - 1, i);

    # To store the final answer
    ans = 0;

    # Calculate the final answer
    for i in range(n) :
        ans += mul * arr[i];

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1 ];
    n = len(arr);

    print(findSum(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int maxN = 10;

// To store factorial values
static int []fact = new int[maxN];

// Function to return ncr
static int ncr(int n, int r)
{
    return (fact[n] / fact[r]) / fact[n - r];
}

// Function to return the required sum
static int findSum(int[] arr, int n)
{
    // Initialising factorial
    fact[0] = 1;
    for (int i = 1; i < n; i++)
        fact[i] = i * fact[i - 1];

    // Multiplier
    int mul = 0;

    // Finding the value of multipler
    // according to the formula
    for (int i = 0; i <= n - 1; i++)
        mul += (int)Math.Pow(2, i) * ncr(n - 1, i);

    // To store the final answer
    int ans = 0;

    // Calculate the final answer
    for (int i = 0; i < n; i++)
        ans += mul * arr[i];

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1 };
    int n = arr.Length;

    Console.WriteLine(findSum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// To store factorial values
let fact = new Array(10);

// Function to return ncr
function ncr(n, r)
{
    return (fact[n] / fact[r]) / fact[n - r];
}

// Function to return the required sum
function findSum(arr, n)
{
    // Initialising factorial
    fact[0] = 1;
    for (let i = 1; i < n; i++)
        fact[i] = i * fact[i - 1];

    // Multiplier
    let mul = 0;

    // Finding the value of multipler
    // according to the formula
    for (let i = 0; i <= n - 1; i++)
        mul += Math.pow(2, i) * ncr(n - 1, i);

    // To store the final answer
    let ans = 0;

    // Calculate the final answer
    for (let i = 0; i < n; i++)
        ans += mul * arr[i];

    return ans;
}

// Driver code

    let arr = [ 1, 1 ];
    let n = arr.length;

    document.write(findSum(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
6
```