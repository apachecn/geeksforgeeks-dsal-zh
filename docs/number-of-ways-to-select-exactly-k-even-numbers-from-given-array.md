# 从给定数组中精确选择 K 个偶数的方法数

> 原文:[https://www . geeksforgeeks . org/从给定数组中精确选择 k 个偶数的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-select-exactly-k-even-numbers-from-given-array/)

给定一个由 n 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是找到从给定数组中精确选择 **K** 偶数的方法数。

**示例:**

> **输入:** arr[] = {1，2，3，4} k = 1
> **输出:** 2
> **解释:**
> 我们可以选择一个偶数的方式数是 2。
> 
> **输入:** arr[] = {61，65，99，26，57，68，23，2，32，30} k = 2
> **输出:** 10
> **说明:**
> 我们可以选择 2 偶数的方式数是 10。

**方法:**思路是应用组合学的规则。从给定的 **n 个对象**中选择 **r 个对象**，选择方式的总数由 **<sup>n</sup> C <sub>r</sub>** 给出。以下是步骤:

1.  计算给定数组中偶数元素的总数[(比如 **cnt** )。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)
2.  检查 **K 的值是否大于 cnt** ，则路数等于 0。
3.  否则，答案将是**<sup>n</sup>C<sub>k</sub>T5。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
long long f[12];

// Function for calculating factorial
void fact()
{
    // Factorial of n defined as:
    // n! = n * (n - 1) * ... * 1
    f[0] = f[1] = 1;

    for (int i = 2; i <= 10; i++)
        f[i] = i * 1LL * f[i - 1];
}

// Function to find the number of ways to
// select exactly K even numbers
// from the given array
void solve(int arr[], int n, int k)
{
    fact();

    // Count even numbers
    int even = 0;
    for (int i = 0; i < n; i++) {

        // Check if the current
        // number is even
        if (arr[i] % 2 == 0)
            even++;
    }

    // Check if the even numbers to be
    // chosen is greater than n. Then,
    // there is no way to pick it.
    if (k > even)
        cout << 0 << endl;

    else {
        // The number of ways will be nCk
        cout << f[even] / (f[k] * f[even - k]);
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof arr / sizeof arr[0];

    // Given count of even elements
    int k = 1;

    // Function Call
    solve(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static int []f = new int[12];

// Function for calculating factorial
static void fact()
{

    // Factorial of n defined as:
    // n! = n * (n - 1) * ... * 1
    f[0] = f[1] = 1;

    for(int i = 2; i <= 10; i++)
        f[i] = i * 1 * f[i - 1];
}

// Function to find the number of ways to
// select exactly K even numbers
// from the given array
static void solve(int arr[], int n, int k)
{
    fact();

    // Count even numbers
    int even = 0;
    for(int i = 0; i < n; i++)
    {

        // Check if the current
        // number is even
        if (arr[i] % 2 == 0)
            even++;
    }

    // Check if the even numbers to be
    // chosen is greater than n. Then,
    // there is no way to pick it.
    if (k > even)
        System.out.print(0 + "\n");

    else
    {
        // The number of ways will be nCk
        System.out.print(f[even] /
                        (f[k] * f[even - k]));
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;

    // Given count of even elements
    int k = 1;

    // Function call
    solve(arr, n, k);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
f = [0] * 12

# Function for calculating factorial
def fact():

    # Factorial of n defined as:
    # n! = n * (n - 1) * ... * 1
    f[0] = f[1] = 1

    for i in range(2, 11):
        f[i] = i * 1 * f[i - 1]

# Function to find the number of ways to
# select exactly K even numbers
# from the given array
def solve(arr, n, k):

    fact()

    # Count even numbers
    even = 0
    for i in range(n):

        # Check if the current
        # number is even
        if (arr[i] % 2 == 0):
            even += 1

    # Check if the even numbers to be
    # chosen is greater than n. Then,
    # there is no way to pick it.
    if (k > even):
        print(0)
    else:

        # The number of ways will be nCk
        print(f[even] // (f[k] * f[even - k]))

# Driver Code

# Given array arr[]
arr = [ 1, 2, 3, 4 ]

n = len(arr)

# Given count of even elements
k = 1

# Function call
solve(arr, n, k)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int []f = new int[12];

// Function for calculating factorial
static void fact()
{

    // Factorial of n defined as:
    // n! = n * (n - 1) * ... * 1
    f[0] = f[1] = 1;

    for(int i = 2; i <= 10; i++)
        f[i] = i * 1 * f[i - 1];
}

// Function to find the number of ways to
// select exactly K even numbers
// from the given array
static void solve(int []arr, int n, int k)
{
    fact();

    // Count even numbers
    int even = 0;
    for(int i = 0; i < n; i++)
    {

        // Check if the current
        // number is even
        if (arr[i] % 2 == 0)
            even++;
    }

    // Check if the even numbers to be
    // chosen is greater than n. Then,
    // there is no way to pick it.
    if (k > even)
        Console.Write(0 + "\n");

    else
    {
        // The number of ways will be nCk
        Console.Write(f[even] /
                        (f[k] * f[even - k]));
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 2, 3, 4 };
    int n = arr.Length;

    // Given count of even elements
    int k = 1;

    // Function call
    solve(arr, n, k);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for the above approach
var f = Array(12).fill(0);

// Function for calculating factorial
function fact()
{
    // Factorial of n defined as:
    // n! = n * (n - 1) * ... * 1
    f[0] = f[1] = 1;

    for (var i = 2; i <= 10; i++)
        f[i] = i * 1 * f[i - 1];
}

// Function to find the number of ways to
// select exactly K even numbers
// from the given array
function solve(arr, n, k)
{
    fact();

    // Count even numbers
    var even = 0;
    for (var i = 0; i < n; i++) {

        // Check if the current
        // number is even
        if (arr[i] % 2 == 0)
            even++;
    }

    // Check if the even numbers to be
    // chosen is greater than n. Then,
    // there is no way to pick it.
    if (k > even)
        document.write( 0 );

    else {
        // The number of ways will be nCk
        document.write( f[even] / (f[k] * f[even - k]));
    }
}

// Driver Code

// Given array arr[]
var arr = [ 1, 2, 3, 4 ];
var n = arr.length;

// Given count of even elements
var k = 1;

// Function Call
solve(arr, n, k);

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*