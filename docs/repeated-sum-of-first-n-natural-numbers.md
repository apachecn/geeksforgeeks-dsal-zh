# 前 N 个自然数的重复和

> 原文:[https://www . geesforgeks . org/repeated-sum-first-n-natural-numbers/](https://www.geeksforgeeks.org/repeated-sum-of-first-n-natural-numbers/)

给定两个整数 **N** 和 **K** ，任务是先求 **N** 自然数的和，然后更新 **N** 作为之前计算的和。重复这些步骤 **K** 次，最后打印 **N** 的值。
**示例:**

> **输入:** N = 2，K = 2
> **输出:** 6
> 运算 1: n =和(n) =和(2) = 1 + 2 = 3
> 运算 2: n =和(n) =和(3) = 1 + 2 + 3 = 6
> **输入:** N = 3，K = 2
> **输出:** 21

**逼近:**先用公式 **(N * (N + 1)) / 2** 求 **N** 自然数之和，然后用计算出的和更新 **N** 。精确重复这些步骤 **K** 次，打印 **N** 的最终值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the sum of
// the first n natural numbers
int sum(int n)
{
    int sum = (n * (n + 1)) / 2;
    return sum;
}

// Function to return the repeated sum
int repeatedSum(int n, int k)
{

    // Perform the operation exactly k times
    for (int i = 0; i < k; i++) {

        // Update n with the sum of
        // first n natural numbers
        n = sum(n);
    }

    return n;
}

// Driver code
int main()
{
    int n = 2, k = 2;

    cout << repeatedSum(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the sum of
    // the first n natural numbers
    static int sum(int n)
    {
        int sum = (n * (n + 1)) / 2;
        return sum;
    }

    // Function to return the repeated sum
    static int repeatedSum(int n, int k)
    {

        // Perform the operation exactly k times
        for (int i = 0; i < k; i++)
        {

            // Update n with the sum of
            // first n natural numbers
            n = sum(n);
        }
        return n;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2, k = 2;

        System.out.println(repeatedSum(n, k));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of
# the first n natural numbers
def sum(n):
    sum = (n * (n + 1)) // 2
    return sum

# Function to return the repeated sum
def repeatedSum(n, k):

    # Perform the operation exactly k times
    for i in range(k):

        # Update n with the sum of
        # first n natural numbers
        n = sum(n)

    return n

# Driver code
n = 2
k = 2

print(repeatedSum(n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the sum of
    // the first n natural numbers
    static int sum(int n)
    {
        int sum = (n * (n + 1)) / 2;
        return sum;
    }

    // Function to return the repeated sum
    static int repeatedSum(int n, int k)
    {

        // Perform the operation exactly k times
        for (int i = 0; i < k; i++)
        {

            // Update n with the sum of
            // first n natural numbers
            n = sum(n);
        }
        return n;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 2, k = 2;

        Console.WriteLine(repeatedSum(n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to return the sum of
// the first n natural numbers
    function sum(n) {
        var sum = (n * (n + 1)) / 2;
        return sum;
    }

    // Function to return the repeated sum
    function repeatedSum(n , k) {

        // Perform the operation exactly k times
        for (i = 0; i < k; i++) {

            // Update n with the sum of
            // first n natural numbers
            n = sum(n);
        }
        return n;
    }

    // Driver code

        var n = 2, k = 2;

        document.write(repeatedSum(n, k));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
6
```