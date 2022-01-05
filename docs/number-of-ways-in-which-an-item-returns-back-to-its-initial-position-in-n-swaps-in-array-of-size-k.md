# 在大小为 K 的数组中，一个项目在 N 次交换中返回其初始位置的方式数

> 原文:[https://www . geeksforgeeks . org/项目返回初始位置的方式数-n-交换大小数组-k/](https://www.geeksforgeeks.org/number-of-ways-in-which-an-item-returns-back-to-its-initial-position-in-n-swaps-in-array-of-size-k/)

给定两个数字 **K** 和 **N** ，任务是找到方法的数量，使得在位置 **i** 的项目在 **N** 步骤中返回到其在长度数组 **K** 中的初始位置，在每个步骤中，该项目可以与 K 中的任何其他项目交换

**示例:**

> **输入:** N = 2，K = 5
> **输出:** 4
> **解释:**
> 对于给定的 K，假设有 5 个位置 1、2、3、4、5。由于问题中给出的是项目位于某个初始位置 B，并且所有 B 的最终答案都是相同的，因此让我们假设项目在开始时位于位置 1。因此，在 2 个步骤中(N 值):
> 项目可以放置在位置 2，也可以再次放置在位置 1。
> 物品可以放在位置 3，也可以放在位置 1。
> 物品可以放在位置 4，也可以放在位置 1。
> 物品可以放在位置 5，也可以放在位置 1。
> 因此，共有 4 种方式。因此输出为 4。
> 
> **输入:** N = 5，K = 5
> T3】输出: 204

**方法:**解决这个问题的思路是使用[组合](https://www.geeksforgeeks.org/permutation-and-combination-gq/)的概念。这个想法是，在每一步，都有**K–1**的可能性将物品放在下一个地方。为了实现这一点，使用了一个数组 **F[]** ，其中 **F[i]** 表示将项目放置在“I”步位置 1 的方法数量。由于给定的项目不属于上一步所属的人，因此，每一步都要减去上一步的路数。因此，数组 F[]可以填充为:

```
F[i] = (K - 1)(i - 1) - F[i - 1]
```

最后，返回数组 F[]的最后一个元素。

以下是该方法的实施情况:

## C++

```
// C++ program to find the number of ways
// in which an item returns back to its
// initial position in N swaps
// in an array of size K

#include <bits/stdc++.h>
using namespace std;

#define mod 1000000007

// Function to calculate (x^y)%p in O(log y)
long long power(long x, long y)
{
    long p = mod;

    // Initialize result
    long res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0) {
        // If y is odd, multiply
        // x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        // y = y/2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function to return the number of ways
long long solve(int n, int k)
{
    // Base case
    if (n == 1)
        return 0LL;

    // Recursive case
    // F(n) = (k-1)^(n-1) - F(n-1).
    return (power((k - 1), n - 1) % mod
            - solve(n - 1, k) + mod)
           % mod;
}

// Drivers code
int main()
{
    int n = 4, k = 5;

    // Function calling
    cout << solve(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of ways
// in which an item returns back to its
// initial position in N swaps
// in an array of size K
class GFG{

static int mod = 1000000007;

// Function to calculate (x^y)%p in O(log y)
public static int power(int x, int y)
{
    int p = mod;

    // Initialize result
    int res = 1;

    // Update x if it is more than
    // or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        // y = y/2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function to return the number of ways
public static int solve(int n, int k)
{

    // Base case
    if (n == 1)
        return 0;

    // Recursive case
    // F(n) = (k-1)^(n-1) - F(n-1).
    return (power((k - 1), n - 1) % mod -
             solve(n - 1, k) + mod) % mod;
}

// Driver code
public static void main(String []args)
{
    int n = 4, k = 5;

    // Function calling
    System.out.println(solve(n, k));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the number of ways
# in which an item returns back to its
# initial position in N swaps
# in an array of size K

mod = 1000000007

# Function to calculate (x^y)%p in O(log y)
def power(x, y):

    p = mod

    # Initialize result
    res = 1

    # Update x if it is more than or
    # equal to p
    x = x % p

    while (y > 0) :
        # If y is odd, multiply
        # x with result
        if (y & 1) != 0 :
            res = (res * x) % p

        # y must be even now
        # y = y/2
        y = y >> 1
        x = (x * x) % p

    return res

# Function to return the number of ways
def solve(n, k):

    # Base case
    if (n == 1) :
        return 0

    # Recursive case
    # F(n) = (k-1)^(n-1) - F(n-1).
    return (power((k - 1), n - 1) % mod - solve(n - 1, k) + mod) % mod

n, k = 4, 5

# Function calling
print(solve(n, k))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the number of ways
// in which an item returns back to its
// initial position in N swaps
// in an array of size K
using System;
class GFG
{

  static int mod = 1000000007;

  // Function to calculate
  // (x^y)%p in O(log y)
  public static int power(int x,
                          int y)
  {
    int p = mod;

    // Initialize result
    int res = 1;

    // Update x if it
    // is more than
    // or equal to p
    x = x % p;

    while (y > 0)
    {
      // If y is odd, multiply
      // x with result
      if ((y & 1) != 0)
        res = (res * x) % p;

      // y must be even now
      // y = y/2
      y = y >> 1;
      x = (x * x) % p;
    }
    return res;
  }

  // Function to return
  // the number of ways
  public static int solve(int n,
                          int k)
  {
    // Base case
    if (n == 1)
      return 0;

    // Recursive case
    // F(n) = (k-1)^(n-1) - F(n-1).
    return (power((k - 1), n - 1) % mod -
            solve(n - 1, k) + mod) % mod;
  }

  // Driver code
  public static void Main(string []args)
  {
    int n = 4, k = 5;

    // Function calling
    Console.Write(solve(n, k));
  }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // Javascript program to find the number of ways
    // in which an item returns back to its
    // initial position in N swaps
    // in an array of size K

    let mod = 1000000007;

    // Function to calculate (x^y)%p in O(log y)
    function power(x, y)
    {
        let p = mod;

        // Initialize result
        let res = 1;

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0) {
            // If y is odd, multiply
            // x with result
            if ((y & 1) > 0)
                res = (res * x) % p;

            // y must be even now
            // y = y/2
            y = y >> 1;
            x = (x * x) % p;
        }
        return res;
    }

    // Function to return the number of ways
    function solve(n, k)
    {
        // Base case
        if (n == 1)
            return 0;

        // Recursive case
        // F(n) = (k-1)^(n-1) - F(n-1).
        return (power((k - 1), n - 1) % mod
                - solve(n - 1, k) + mod)
               % mod;
    }

    let n = 4, k = 5;

    // Function calling
    document.write(solve(n, k));

</script>
```

**Output:** 

```
52
```