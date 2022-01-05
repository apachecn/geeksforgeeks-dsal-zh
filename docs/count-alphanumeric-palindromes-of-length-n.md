# 计数长度为 N 的字母数字回文

> 原文:[https://www . geesforgeks . org/count-字母数字-回文长度-n/](https://www.geeksforgeeks.org/count-alphanumeric-palindromes-of-length-n/)

给定一个正整数 **N** ，任务是找到长度为 **N** 的[字母数字](https://www.geeksforgeeks.org/how-to-check-string-is-alphanumeric-or-not-using-regular-expression/) [回文串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)的个数。由于这样的[字符串](https://www.geeksforgeeks.org/string-data-structure/)的计数会很大，所以打印答案[模 **10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 2
> **输出:** 62
> **说明:**有 26 个回文的形式{“AA”、“bb”、…、“ZZ”}，26 个回文的形式{“AA”、“BB”、…、“cc”}和 10 个回文的形式{“00”、“11”、…、“^ 99”}。因此，回文串的总数= 26 + 26 + 10 = 62。
> 
> **输入:**N = 3
> T3】输出: 3844

**天真方法:**最简单的方法是[生成所有可能的长度为 N 的字母数字字符串](https://www.geeksforgeeks.org/print-all-combinations-of-given-length/)，对于每个字符串，[检查它是否是回文](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)。因为在每个位置，总共可以放置 **62 个字符**。因此，有 **62 <sup>N</sup>** 种可能的字符串。

***时间复杂度:**O(N * 62<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是利用[回文](https://www.geeksforgeeks.org/tag/palindrome/)的属性。可以观察到，如果字符串的[长度为**甚至**，那么对于从 **0 到 N/2** 的每个索引 **i** ，索引 **i** 和**(N–1–I)**处的字符是相同的。因此，从 **0** 到 **N/ 2** 的每个位置都有 **62 <sup>N/2</sup>** 选项。同样，如果长度为奇数， **62 <sup>(N+1)/2</sup>** 选项也在。因此，可以说，对于某些 **N** 来说，存在着 **62 <sup>ceil(N/2)</sup>** 可能的](https://www.geeksforgeeks.org/find-length-of-a-string-in-python-4-ways/)[回文串](https://www.geeksforgeeks.org/string-palindrome/)。
按照以下步骤解决问题:

*   对于 **N** 的给定值，使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)计算**62<sup>ceil(N/2)</sup>mod 10<sup>9</sup>+7**。
*   打印**62<sup>ceil(N/2)</sup>mod 10<sup>9</sup>+7**作为所需答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// (x ^ y) mod p
int power(int x, int y,
          int p)
{
  // Initialize result
  int res = 1;

  // Update x if it is more
  // than or equal to p
  x = x % p;

  if (x == 0)
    return 0;

  while (y > 0)
  {
    // If y is odd, multiply
    // x with result
    if ((y & 1) == 1)
      res = (res * x) % p;

    // y must be even now
    y = y >> 1;
    x = (x * x) % p;
  }

  // Return the final
  // result
  return res;
}

// Driver Code
int main()
{   
  // Given N
  int N = 3;
  int flag, k, m;

  // Base Case
  if((N == 1) ||
     (N == 2))
    cout << 62;

  else
    m = 1000000000 + 7;

  // Check whether n
  // is even or odd
  if(N % 2 == 0)
  {
    k = N / 2;
    flag = true;
  }
  else
  {
    k = (N - 1) / 2;
    flag = false;
  }
  if(flag != 0)
  {      
    // Function Call
    int a = power(62,
                  k, m);
    cout << a;
  }
  else
  {
    // Function Call
    int a = power(62,
                  (k + 1), m);
    cout << a;
  }
}

// This code is contributed by sanjoy_62
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to calculate
// (x ^ y) mod p
static int power(int x,
                 int y, int p)
{
  // Initialize result
  int res = 1;

  // Update x if it is more
  // than or equal to p
  x = x % p;

  if (x == 0)
    return 0;

  while (y > 0)
  {
    // If y is odd, multiply
    // x with result
    if ((y & 1) == 1)
      res = (res * x) % p;

    // y must be even now
    y = y >> 1;
    x = (x * x) % p;
  }

  // Return the final
  // result
  return res;
}

// Driver Code
public static void main(String[] args)
{
  // Given N
  int N = 3;
  int flag, k, m =0;

  // Base Case
  if ((N == 1) || (N == 2))
    System.out.print(62);
  else
    m = 1000000000 + 7;

  // Check whether n
  // is even or odd
  if (N % 2 == 0)
  {
    k = N / 2;
    flag = 1;
  }
  else
  {
    k = (N - 1) / 2;
    flag = 0;
  }

  if (flag != 0)
  {
    // Function Call
    int a = power(62, k, m);
    System.out.print(a);
  }
  else
  {
    // Function Call
    int a = power(62, (k + 1), m);
    System.out.print(a);
  }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate (x ^ y) mod p
def power(x, y, p):

    # Initialize result
    res = 1

    # Update x if it is more
    # than or equal to p
    x = x % p

    if (x == 0):
        return 0

    while (y > 0):

        # If y is odd, multiply
        # x with result
        if ((y & 1) == 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1
        x = (x * x) % p

    # Return the final result
    return res

# Driver Code

# Given N
N = 3

# Base Case
if((N == 1) or (N == 2)):
    print(62)

else:

    m = (10**9)+7

    # Check whether n
    # is even or odd
    if(N % 2 == 0):
        k = N//2
        flag = True
    else:
        k = (N - 1)//2
        flag = False

    if(flag):

        # Function Call
        a = power(62, k, m)
        print(a)
    else:

        # Function Call
        a = power(62, (k + 1), m)
        print(a)
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to calculate
// (x ^ y) mod p
static int power(int x, int y,
                 int p)
{

  // Initialize result
  int res = 1;

  // Update x if it is more
  // than or equal to p
  x = x % p;

  if (x == 0)
    return 0;

  while (y > 0)
  {

    // If y is odd, multiply
    // x with result
    if ((y & 1) == 1)
      res = (res * x) % p;

    // y must be even now
    y = y >> 1;
    x = (x * x) % p;
  }

  // Return the final
  // result
  return res;
}

// Driver Code
public static void Main()
{

  // Given N
  int N = 3;
  int flag, k, m = 0;

  // Base Case
  if ((N == 1) || (N == 2))
    Console.Write(62);
  else
    m = 1000000000 + 7;

  // Check whether n
  // is even or odd
  if (N % 2 == 0)
  {
    k = N / 2;
    flag = 1;
  }
  else
  {
    k = (N - 1) / 2;
    flag = 0;
  }

  if (flag != 0)
  {
    // Function Call
    int a = power(62, k, m);
    Console.Write(a);
  }
  else
  {

    // Function Call
    int a = power(62, (k + 1), m);
    Console.Write(a);
  }
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate
// (x ^ y) mod p
function power(x, y, p)
{
  // Initialize result
  let res = 1;

  // Update x if it is more
  // than or equal to p
  x = x % p;

  if (x == 0)
    return 0;

  while (y > 0)
  {
    // If y is odd, multiply
    // x with result
    if ((y & 1) == 1)
      res = (res * x) % p;

    // y must be even now
    y = y >> 1;
    x = (x * x) % p;
  }

  // Return the final
  // result
  return res;
}
// Driver Code

      // Given N
  let N = 3;
  let flag, k, m =0;

  // Base Case
  if ((N == 1) || (N == 2))
    document.write(62);
  else
    m = 1000000000 + 7;

  // Check whether n
  // is even or odd
  if (N % 2 == 0)
  {
    k = N / 2;
    flag = 1;
  }
  else
  {
    k = (N - 1) / 2;
    flag = 0;
  }

  if (flag != 0)
  {
    // Function Call
    let a = power(62, k, m);
    document.write(a);
  }
  else
  {
    // Function Call
    let a = power(62, (k + 1), m);
    document.write(a);
  }

</script>
```

**Output:** 

```
3844
```

***时间复杂度:** O(log N)*
***辅助空间:** O(N)*