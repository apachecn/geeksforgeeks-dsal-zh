# 检查一个数字在翻转颠倒、镜像翻转和镜像翻转颠倒中是否为质数

> 原文:[https://www . geesforgeks . org/check-如果一个数是质数-翻转-倒置-镜像-翻转-镜像-翻转-倒置/](https://www.geeksforgeeks.org/check-if-a-number-is-prime-in-flipped-upside-down-mirror-flipped-and-mirror-flipped-upside-down/)

给定一个整数 **N** ，任务是[检查 **N** 是否是给定数字的翻转向下、镜像翻转和镜像翻转向下形式中的质数](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/)。
**示例:**

> **输入:** N = 120121
> **输出:**是
> **解释:**
> 翻转过来的数字形式:
> 翻转过来的倒过来的–151051
> 镜像翻转过来的–121021
> 镜像翻转过来的–150151
> 由于 1510151 和 121021 都是质数，所以翻转过来的数字都是质数。
> 
> **输入:** N = 12
> **输出:**否
> **解释:**
> 翻转的数字形式:
> 翻转颠倒–15
> 镜像翻转–21
> 镜像翻转–51
> 所有翻转的数字都不是质数。

**方法:**按照以下步骤解决问题:

1.  由于数字 **N** 在翻转、镜像翻转和镜像翻转形式中必须是素数，因此它应该包含的唯一可能的数字是{0，1，2，5，8}。
2.  因此，问题简化为[检查数字是否为质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)以及是否仅由数字 **0、1、2、5** 和 **8** 组成。
3.  如果发现是真的，打印“**是**”。
4.  否则，打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N
// contains digits
// 0, 1, 2, 5, 8 only
bool checkDigits(int n)
{
    // Extract digits of N
    do {
        int r = n % 10;

        // Return false if any of
        // these digits are present
        if (r == 3 || r == 4 || r == 6
            || r == 7 || r == 9)
            return false;

        n /= 10;
    } while (n != 0);

    return true;
}

// Function to check if
// N is prime or not
bool isPrime(int n)
{
    if (n <= 1)
        return false;

    // Check for all factors
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to check if n is prime
// in all the desired forms
int isAllPrime(int n)
{
    return isPrime(n)
           && checkDigits(n);
}

// Driver Code
int main()
{
    int N = 101;

    if (isAllPrime(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to check if N
// contains digits
// 0, 1, 2, 5, 8 only
static boolean checkDigits(int n)
{
  // Extract digits of N
  do
  {
    int r = n % 10;

    // Return false if any of
    // these digits are present
    if (r == 3 || r == 4 ||
        r == 6 || r == 7 || r == 9)
      return false;

    n /= 10;
  } while (n != 0);

  return true;
}

// Function to check if
// N is prime or not
static boolean isPrime(int n)
{
  if (n <= 1)
    return false;

  // Check for all factors
  for (int i = 2; i * i <= n; i++)
  {
    if (n % i == 0)
      return false;
  }
  return true;
}

// Function to check if n is prime
// in all the desired forms
static boolean isAllPrime(int n)
{
  return isPrime(n) &&
         checkDigits(n);
}

// Driver Code
public static void main(String[] args)
{
  int N = 101;

  if (isAllPrime(N))
    System.out.print("Yes");
  else
    System.out.print("No");
}
}

// This code is  contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if N
# contains digits
# 0, 1, 2, 5, 8 only
def checkDigits(n):

    # Extract digits of N
    while True:
        r = n % 10

        # Return false if any of
        # these digits are present
        if (r == 3 or r == 4 or
            r == 6 or r == 7 or
            r == 9):
            return False

        n //= 10

        if n == 0:
            break

    return True

# Function to check if
# N is prime or not
def isPrime(n):

    if (n <= 1):
        return False

    # Check for all factors
    for i in range(2, n + 1):
        if i * i > n:
            break

        if (n % i == 0):
            return False

    return True

# Function to check if n is prime
# in all the desired forms
def isAllPrime(n):

    return isPrime(n) and checkDigits(n)

# Driver Code
if __name__ == '__main__':

    N = 101

    if (isAllPrime(N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if N
// contains digits
// 0, 1, 2, 5, 8 only
static bool checkDigits(int n)
{

  // Extract digits of N
  do
  {
    int r = n % 10;

    // Return false if any of
    // these digits are present
    if (r == 3 || r == 4 ||
        r == 6 || r == 7 ||
        r == 9)
      return false;

    n /= 10;
  } while (n != 0);

  return true;
}

// Function to check if
// N is prime or not
static bool isPrime(int n)
{
  if (n <= 1)
    return false;

  // Check for all factors
  for (int i = 2; i * i <= n; i++)
  {
    if (n % i == 0)
      return false;
  }
  return true;
}

// Function to check if n is prime
// in all the desired forms
static bool isAllPrime(int n)
{
  return isPrime(n) &&
         checkDigits(n);
}

// Driver Code
public static void Main(String[] args)
{
  int N = 101;

  if (isAllPrime(N))
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if N
// contains digits
// 0, 1, 2, 5, 8 only
function checkDigits(n)
{
    // Extract digits of N
    do {
        var r = n % 10;

        // Return false if any of
        // these digits are present
        if (r == 3 || r == 4 || r == 6
            || r == 7 || r == 9)
            return false;

        n = parseInt(n/10);
    } while (n != 0);

    return true;
}

// Function to check if
// N is prime or not
function isPrime(n)
{
    if (n <= 1)
        return false;

    // Check for all factors
    for (var i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Function to check if n is prime
// in all the desired forms
function isAllPrime(n)
{
    return isPrime(n)
           && checkDigits(n);
}

// Driver Code

var N = 101;
if (isAllPrime(N))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)