# 求 N 的最小值，使得前 N 个自然数之和≥ X

> 原文:[https://www . geeksforgeeks . org/find-n 的最小值，即第一个 n 个自然数的和-is-x/](https://www.geeksforgeeks.org/find-the-smallest-value-of-n-such-that-sum-of-first-n-natural-numbers-is-x/)

给定一个正整数**X***(1≤X≤10<sup>6</sup>)*，任务是求最小值 **N** ，使得前 N 个自然数的[和为≥ **X** 。](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)

**示例:**

> **输入:** X = 14
> **输出:** 5
> **说明:**前 5 个自然数之和为 15，大于 X( = 14)。
> 
> *   1 + 2 = 3( < 14)
> *   1 + 2 + 3 = 6( < 14)
> *   1 + 2 + 3 + 4 = 10( < 15)
> *   1 + 2 + 3 + 4 + 5 = 15( > 14)
> 
> **输入:**X = 91
> T3】输出: 13

**天真方法:**解决这个问题最简单的方法是检查范围**【1，X】**中的每个值，并从该范围返回第一个值，对于该值，发现第一个 **N** 自然数的 s [um 为≥ **X** 。](https://www.geeksforgeeks.org/python-program-for-sum-of-squares-of-first-n-natural-numbers/)

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if sum of first
// N natural numbers is >= X
bool isGreaterEqual(int N, int X)
{
    return (N * 1LL * (N + 1) / 2) >= X;
}

// Finds minimum value of
// N such that sum of first
// N natural number >= X
int minimumPossible(int X)
{
    for (int i = 1; i <= X; i++) {

        // Check if sum of first i
        // natural number >= X
        if (isGreaterEqual(i, X))
            return i;
    }
}

// Driver Code
int main()
{
    // Input
    int X = 14;

    // Finds minimum value of
    // N such that sum of first
    // N natural number >= X
    cout << minimumPossible(X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
class GFG
{

  // Function to check if sum of first
  // N natural numbers is >= X
  static boolean isGreaterEqual(int N, int X)
  {
    return (N * (N + 1) / 2) >= X;
  }

  // Finds minimum value of
  // N such that sum of first
  // N natural number >= X
  static int minimumPossible(int X)
  {
    for (int i = 1; i <= X; i++)
    {

      // Check if sum of first i
      // natural number >= X
      if (isGreaterEqual(i, X))
        return i;
    }
    return 0;
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Input
    int X = 14;

    // Finds minimum value of
    // N such that sum of first
    // N natural number >= X
    System.out.print(minimumPossible(X));
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to check if sum of first
# N natural numbers is >= X
def isGreaterEqual(N, X):
    return (N * (N + 1) // 2) >= X

# Finds minimum value of
# N such that sum of first
# N natural number >= X
def minimumPossible(X):

    for i in range(1, X + 1):

        # Check if sum of first i
        # natural number >= X
        if (isGreaterEqual(i, X)):
            return i

# Driver Code
if __name__ == '__main__':

    # Input
    X = 14

    # Finds minimum value of
    # N such that sum of first
    # N natural number >= X
    print (minimumPossible(X))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program to implement
// the above approach
using System;
public class GFG
{

  // Function to check if sum of first
  // N natural numbers is >= X
  static bool isGreaterEqual(int N, int X)
  {
    return (N * (N + 1) / 2) >= X;
  }

  // Finds minimum value of
  // N such that sum of first
  // N natural number >= X
  static int minimumPossible(int X)
  {
    for (int i = 1; i <= X; i++)
    {

      // Check if sum of first i
      // natural number >= X
      if (isGreaterEqual(i, X))
        return i;
    }
    return 0;
  }

  // Driver Code
  static public void Main ()
  {

    // Input
    int X = 14;

    // Finds minimum value of
    // N such that sum of first
    // N natural number >= X
    Console.Write(minimumPossible(X));
  }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if sum of first
// N natural numbers is >= X
function isGreaterEqual(N, X)
{
    return parseInt((N * (N + 1)) / 2) >= X;
}

// Finds minimum value of
// N such that sum of first
// N natural number >= X
function minimumPossible(X)
{
    for(let i = 1; i <= X; i++)
    {

        // Check if sum of first i
        // natural number >= X
        if (isGreaterEqual(i, X))
            return i;
    }
}

// Driver Code

// Input
let X = 14;

// Finds minimum value of
// N such that sum of first
// N natural number >= X
document.write(minimumPossible(X));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**以下是上述方法的实现:

1.  想法是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决这个问题。
2.  初始化变量**低= 1，高= X** 并在此范围内执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。
3.  计算**mid = low+(high–low)/2**，检查第一个 mid 数之和是否大于等于 x。
4.  如果**总和≥ X** ，将其存储在变量 **res** 中，并将**设置为高=中 1**
5.  否则，将**设置为低=中+ 1**
6.  打印 **res，**这是所需答案。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check if sum of first
// N natural numbers is >= X
bool isGreaterEqual(int N, int X)
{
    return (N * 1LL * (N + 1) / 2) >= X;
}

// Finds minimum value of
// N such that sum of first
// N natural number >= X
int minimumPossible(int X)
{

    int low = 1, high = X, res = -1;

    // Binary Search
    while (low <= high) {
        int mid = low + (high - low) / 2;

        // Checks if sum of first 'mid' natural
        // numbers is greater than equal to X
        if (isGreaterEqual(mid, X)) {
            // Update res
            res = mid;
            // Update high
            high = mid - 1;
        }
        else
            // Update low
            low = mid + 1;
    }
    return res;
}

// Driver Code
int main()
{
    // Input
    int X = 14;

    // Finds minimum value of
    // N such that sum of first
    // N natural number >= X
    cout << minimumPossible(X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to check if sum of first
// N natural numbers is >= X
static boolean isGreaterEqual(int N, int X)
{
    return (N  * (N + 1) / 2) >= X;
}

// Finds minimum value of
// N such that sum of first
// N natural number >= X
static int minimumPossible(int X)
{
    int low = 1, high = X, res = -1;

    // Binary Search
    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        // Checks if sum of first 'mid' natural
        // numbers is greater than equal to X
        if (isGreaterEqual(mid, X))
        {

            // Update res
            res = mid;

            // Update high
            high = mid - 1;
        }
        else
            // Update low
            low = mid + 1;
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int X = 14;

    // Finds minimum value of
    // N such that sum of first
    // N natural number >= X
    System.out.print( minimumPossible(X));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Function to check if sum of first
# N natural numbers is >= X
def isGreaterEqual(N, X):
    return (N * (N + 1) // 2) >= X;

# Finds minimum value of
# N such that sum of first
# N natural number >= X
def minimumPossible(X):
  low = 1
  high = X
  res = -1;

  # Binary Search
  while (low <= high):
        mid = low + (high - low) // 2;

        # Checks if sum of first 'mid' natural
        # numbers is greater than equal to X
        if (isGreaterEqual(mid, X)):

            # Update res
            res = mid;

            # Update high
            high = mid - 1;

        else:
            # Update low
            low = mid + 1;

  return res

# Driver Code
if __name__ == "__main__":

    # Input
    X = 14;

    # Finds minimum value of
    # N such that sum of first
    # N natural number >= X
    print(minimumPossible(X));

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  // Function to check if sum of first
  // N natural numbers is >= X
  static bool isGreaterEqual(int N, int X)
  {
    return (N  * (N + 1) / 2) >= X;
  }

  // Finds minimum value of
  // N such that sum of first
  // N natural number >= X
  static int minimumPossible(int X)
  {
    int low = 1, high = X, res = -1;

    // Binary Search
    while (low <= high)
    {
      int mid = low + (high - low) / 2;

      // Checks if sum of first 'mid' natural
      // numbers is greater than equal to X
      if (isGreaterEqual(mid, X))
      {

        // Update res
        res = mid;

        // Update high
        high = mid - 1;
      }
      else
        // Update low
        low = mid + 1;
    }
    return res;
  }

  // Driver Code
  static public void Main()
  {
    // Input
    int X = 14;

    // Finds minimum value of
    // N such that sum of first
    // N natural number >= X
    Console.Write( minimumPossible(X));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Function to check if sum of first
// N natural numbers is >= X
function isGreaterEqual(N, X)
{
    return parseInt((N * (N + 1)) / 2) >= X;
}

// Finds minimum value of
// N such that sum of first
// N natural number >= X
function minimumPossible(X)
{

    let low = 1, high = X, res = -1;

    // Binary Search
    while (low <= high) {
        let mid = low + parseInt((high - low) / 2);

        // Checks if sum of first 'mid' natural
        // numbers is greater than equal to X
        if (isGreaterEqual(mid, X)) {
            // Update res
            res = mid;
            // Update high
            high = mid - 1;
        }
        else
            // Update low
            low = mid + 1;
    }
    return res;
}

// Driver Code
// Input
let X = 14;

// Finds minimum value of
// N such that sum of first
// N natural number >= X
document.write(minimumPossible(X));

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(log(X))*
***辅助空间:** O(1)*