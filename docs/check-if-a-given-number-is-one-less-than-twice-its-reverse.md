# 检查给定的数字是否比它的倒数少一倍

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数字少于其反转的两倍/](https://www.geeksforgeeks.org/check-if-a-given-number-is-one-less-than-twice-its-reverse/)

给定一个整数 **N，**任务是检查它是否是方程 **2 *逆(N)–1 = N**的解

**示例**:

> **输入:**N = 73
> T3】输出:是
> T6】解释:T8】2 *反向(N) = 2 * 37 = 74
> N + 1 = 73 + 1 = 74
> 
> **输入:**N = 83
> T3】输出:否

**天真法:**最简单的方法是找到给定数的[逆，检查其是否满足等式 **2 *逆(N) = N + 1** 并相应打印“是”或“否”。](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Iterative function to
// reverse digits of num
int rev(int num)
{
    int rev_num = 0;

    // Loop to extract all
    // digits of the number
    while (num > 0) {
        rev_num
            = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to check if N
// satisfies given equation
bool check(int n)
{
    return 2 * rev(n) == n + 1;
}

// Driver Code
int main()
{
    int n = 73;
    if (check(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;
class GFG{

// Iterative function to
// reverse digits of num
static int rev(int num)
{
  int rev_num = 0;

  // Loop to extract all
  // digits of the number
  while (num > 0)
  {
    rev_num = rev_num * 10 +
              num % 10;
    num = num / 10;
  }
  return rev_num;
}

// Function to check if N
// satisfies given equation
static boolean check(int n)
{
  return 2 * rev(n) == n + 1;
}

// Driver Code
public static void main(String[] args)
{
  int n = 73;
  if (check(n))
    System.out.print("Yes");
  else
    System.out.print("No");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Iterative function to
# reverse digits of num
def rev(num):

    rev_num = 0

    # Loop to extract all
    # digits of the number
    while (num > 0):
        rev_num = (rev_num * 10 +
                       num % 10)
        num = num // 10

    return rev_num

# Function to check if N
# satisfies given equation
def check(n):

    return (2 * rev(n) == n + 1)

# Driver Code
n = 73

if (check(n)):
    print("Yes")  
else:
    print("No")

# This code is contributed by code_hunt
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Iterative function to
// reverse digits of num
static int rev(int num)
{
    int rev_num = 0;

    // Loop to extract all
    // digits of the number
    while (num > 0)
    {
        rev_num = rev_num * 10 +
                      num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to check if N
// satisfies given equation
static bool check(int n)
{
    return 2 * rev(n) == n + 1;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 73;

    if (check(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program of the
// above approach

// Iterative function to
// reverse digits of num
function rev(num)
{
    var rev_num = 0;

    // Loop to extract all
    // digits of the number
    while (num > 0) {
        rev_num
            = rev_num * 10 + num % 10;
        num = parseInt(num / 10);
    }
    return rev_num;
}

// Function to check if N
// satisfies given equation
function check(n)
{
    return 2 * rev(n) == n + 1;
}

// Driver Code
var n = 73;
if (check(n))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**高效方法:**优化上述方法的关键观察是满足给定方程的数可以表示为:

> x = 8 * 10<sup>(n-1)</sup>–7

要检查一个数 X 是否满足上式，需要检查这个数(X + 7) / 8 是否为 10 的[次幂](https://www.geeksforgeeks.org/check-if-a-number-is-power-of-another-number/)。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check y is a power of x
bool isPower(int x, int y)
{
    // logarithm function to
    // calculate value
    int res1 = log(y) / log(x);
    double res2 = log(y) / log(x);

    // Compare to the result1 or
    // result2 both are equal
    return (res1 == res2);
}

// Function to check if N
// satisfies the equation
// 2 * reverse(n) = n + 1
bool check(int n)
{
    int x = (n + 7) / 8;
    if ((n + 7) % 8 == 0
        && isPower(10, x))
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int n = 73;
    if (check(n))
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
import java.io.*;
import java.util.*;

class GFG{

// Function to check y is a power of x
static boolean isPower(int x, int y)
{

    // logarithm function to
    // calculate value
    double res1 = Math.log(y) / Math.log(x);
    double res2 = Math.log(y) / Math.log(x);

    // Compare to the result1 or
    // result2 both are equal
    return (res1 == res2);
}

// Function to check if N
// satisfies the equation
// 2 * reverse(n) = n + 1
static boolean check(int n)
{
    int x = (n + 7) / 8;

    if ((n + 7) % 8 == 0 &&
        isPower(10, x))
        return true;
    else
        return false;
}

// Driver Code
public static void main (String[] args)
{
    int n = 73;

    if (check(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to check y is a power of x
def isPower(x, y):

    # logarithm function to
    # calculate value
    res1 = math.log(y) // math.log(x)
    res2 = math.log(y) // math.log(x)

    # Compare to the result1 or
    # result2 both are equal
    return (res1 == res2)

# Function to check if N
# satisfies the equation
# 2 * reverse(n) = n + 1
def check(n):

    x = (n + 7) // 8

    if ((n + 7) % 8 == 0 and
        isPower(10, x)):
        return True
    else:
        return False

# Driver Code
n = 73

if (check(n) != 0):
    print("Yes")
else:
    print("No")

# This code is contributed by code_hunt
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check y is a power of x
static bool isPower(int x, int y)
{

    // logarithm function to
    // calculate value
    double res1 = Math.Log(y) / Math.Log(x);
    double res2 = Math.Log(y) / Math.Log(x);

    // Compare to the result1 or
    // result2 both are equal
    return (res1 == res2);
}

// Function to check if N
// satisfies the equation
// 2 * reverse(n) = n + 1
static bool check(int n)
{
    int x = (n + 7) / 8;

    if ((n + 7) % 8 == 0 &&
        isPower(10, x))
        return true;
    else
        return false;
}

// Driver Code
static public void Main ()
{
    int n = 73;

    if (check(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to check y is a power of x
function isPower(x, y)
{

    // logarithm function to
    // calculate value
    let res1 = Math.log(y) / Math.log(x);
    let res2 = Math.log(y) / Math.log(x);

    // Compare to the result1 or
    // result2 both are equal
    return (res1 == res2);
}

// Function to check if N
// satisfies the equation
// 2 * reverse(n) = n + 1
function check(n)
{
    let x = (n + 7) / 8;

    if ((n + 7) % 8 == 0 &&
        isPower(10, x))
        return true;
    else
        return false;
}

// Driver code
  let n = 73;
  if (check(n) != 0)
    document.write("Yes");
  else
    document.write("No");

    // This code is contributed by splevel62.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*