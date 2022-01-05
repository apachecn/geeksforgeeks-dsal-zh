# 计算没有特定数字的 n 位数

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-not-special-digits/](https://www.geeksforgeeks.org/count-n-digit-numbers-not-particular-digit/)

给我们两个整数 **n** 和 d，我们需要统计所有没有数字 d 的 n 位数。

**示例:**

```
Input : n = 2, d = 7
Output : 72
All two digit numbers that don't have
7 as digit are 10, 11, 12, 13, 14, 15,
16, 18, .....

Input : n = 3, d = 9
Output : 648

```

一个**简单的解决方案**是遍历所有的 d 位数。对于每个数字，检查它是否有 x 作为数字。

**有效方法**在该方法中，我们首先检查排除数字 d 是零还是非零。如果它是零，那么我们有 9 个数字(1 到 9)作为第一个数字，否则我们有 8 个数字(不包括 x 数字和 0)。那么对于所有其他数字，我们有 9 个选择，即 0 到 9(不包括 d 数字)。我们简单的调用 digitNumber 函数，用 n-1 个数字作为第一个数字，我们已经发现它可以是 8 或 9，然后简单的乘以它。对于其他数字，我们检查数字是奇数还是偶数，如果是奇数，我们用(n-1)/2 位数字调用 digitNumber 函数，并将其乘以 9，否则我们用 n/2 位数字调用 digitNumber 函数，并将它们存储在结果中并取结果平方。

插图:

```
Number from 1 to 7 excluding digit 9.
digits      multiple          number
1           8                   8
2           8*9                 72
3           8*9*9               648 
4           8*9*9*9             5832
5           8*9*9*9*9           52488
6           8*9*9*9*9*9         472392
7           8*9*9*9*9*9*9       4251528
```

如我们所见，在每一步中，我们都是数字的一半。假设我们有 7 位数字，我们用 6(7-1)位数字从 main 调用函数。当我们将数字减半时，我们留下了 3(6/2)个数字。因此，我们必须将 3 位数的结果与自身相乘，才能得到 6 位数的结果。同样，对于 3 位数，我们有奇数位，我们有奇数位。我们找到 1 ((3-1)/2)位的结果，找到结果的平方并乘以 9，因为我们找到 d-1 位的结果。

## C++

```
// C++ Implementation of above method
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Finding number of possible number with
// n digits excluding a particular digit
long long digitNumber(long long n) {

  // Checking if number of digits is zero
  if (n == 0)
    return 1;

  // Checking if number of digits is one
  if (n == 1)
    return 9;

  // Checking if number of digits is odd
  if (n % 2) {

    // Calling digitNumber function
    // with (digit-1)/2 digits
    long long temp = digitNumber((n - 1) / 2) % mod;
    return (9 * (temp * temp) % mod) % mod;
  } else {

    // Calling digitNumber function
    // with n/2 digits
    long long temp = digitNumber(n / 2) % mod;
    return (temp * temp) % mod;
  }
}

int countExcluding(int n, int d)
{
  // Calling digitNumber function
  // Checking if excluding digit is
  // zero or non-zero
  if (d == 0)
    return (9 * digitNumber(n - 1)) % mod;
  else
    return (8 * digitNumber(n - 1)) % mod;
}

// Driver function to run above program
int main() {

  // Initializing variables
  long long d = 9;
  int n = 3;
  cout << countExcluding(n, d) << endl;
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above method
import java.lang.*;

class GFG {

static final int mod = 1000000007;

// Finding number of possible number with
// n digits excluding a particular digit
static int digitNumber(long n) {

    // Checking if number of digits is zero
    if (n == 0)
    return 1;

    // Checking if number of digits is one
    if (n == 1)
    return 9;

    // Checking if number of digits is odd
    if (n % 2 != 0) {

    // Calling digitNumber function
    // with (digit-1)/2 digits
    int temp = digitNumber((n - 1) / 2) % mod;

    return (9 * (temp * temp) % mod) % mod;
    }
    else {

    // Calling digitNumber function
    // with n/2 digits
    int temp = digitNumber(n / 2) % mod;

    return (temp * temp) % mod;
    }
}

static int countExcluding(int n, int d) {

    // Calling digitNumber function
    // Checking if excluding digit is
    // zero or non-zero
    if (d == 0)
    return (9 * digitNumber(n - 1)) % mod;
    else
    return (8 * digitNumber(n - 1)) % mod;
}

// Driver function to run above program
public static void main(String[] args) {

    // Initializing variables
    int d = 9;
    int n = 3;
    System.out.println(countExcluding(n, d));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python Implementation
# of above method

mod=1000000007

# Finding number of
# possible number with
# n digits excluding
# a particular digit
def digitNumber(n):

    # Checking if number
    # of digits is zero
    if (n == 0):
        return 1

    # Checking if number
    # of digits is one
    if (n == 1):
        return 9

    # Checking if number
    # of digits is odd
    if (n % 2!=0):

        # Calling digitNumber function
        # with (digit-1)/2 digits
        temp = digitNumber((n - 1) // 2) % mod
        return (9 * (temp * temp) % mod) % mod
    else:

        # Calling digitNumber function
        # with n/2 digits
        temp = digitNumber(n // 2) % mod
        return (temp * temp) % mod

def countExcluding(n,d):

    # Calling digitNumber function
    # Checking if excluding digit is
    # zero or non-zero
    if (d == 0):
        return (9 * digitNumber(n - 1)) % mod
    else:
        return (8 * digitNumber(n - 1)) % mod

# Driver code

d = 9
n = 3
print(countExcluding(n, d))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Implementation of above method
using System;

class GFG {

    static int mod = 1000000007;

    // Finding number of possible number with
    // n digits excluding a particular digit
    static int digitNumber(long n) {

        // Checking if number of digits is zero
        if (n == 0)
            return 1;

        // Checking if number of digits is one
        if (n == 1)
            return 9;

        // Checking if number of digits is odd
        if (n % 2 != 0) {

            // Calling digitNumber function
            // with (digit-1)/2 digits
            int temp = digitNumber((n - 1) / 2) % mod;

            return (9 * (temp * temp) % mod) % mod;
        }
        else {

            // Calling digitNumber function
            // with n/2 digits
            int temp = digitNumber(n / 2) % mod;

            return (temp * temp) % mod;
        }
    }

    static int countExcluding(int n, int d) {

        // Calling digitNumber function
        // Checking if excluding digit is
        // zero or non-zero
        if (d == 0)
            return (9 * digitNumber(n - 1)) % mod;
        else
            return (8 * digitNumber(n - 1)) % mod;
    }

    // Driver function to run above program
    public static void Main() {

        // Initializing variables
        int d = 9;
        int n = 3;

        Console.WriteLine(countExcluding(n, d));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Implementation
// of above method

$mod = 1000000007;

// Finding number of
// possible number with
// n digits excluding
// a particular digit
function digitNumber($n)
{
    global $mod;

    // Checking if number
    // of digits is zero
    if ($n == 0)
        return 1;

    // Checking if number
    // of digits is one
    if ($n == 1)
        return 9;

    // Checking if number
    // of digits is odd
    if ($n % 2 != 0)
    {
        // Calling digitNumber
        // function with
        // (digit-1)/2 digits;
        $temp = digitNumber(($n -
                    1) / 2) % $mod;
        return (9 * ($temp * $temp) %
                     $mod) % $mod;
    }
    else
    {
        // Calling digitNumber
        // function with n/2 digits
        $temp = digitNumber($n /
                      2) % $mod;
        return ($temp *
                $temp) % $mod;
    }
}

function countExcluding($n, $d)
{
    global $mod;

    // Calling digitNumber
    // function Checking if
    // excluding digit is
    // zero or non-zero
    if ($d == 0)
        return (9 * digitNumber($n -
                         1)) % $mod;
    else
        return (8 * digitNumber($n -
                         1)) % $mod;
}    

// Driver code
$d = 9;
$n = 3;
print(countExcluding($n, $d));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript Implementation of above method

const mod = 1000000007;

// Finding number of possible number with
// n digits excluding a particular digit
function digitNumber(n) {

// Checking if number of digits is zero
if (n == 0)
    return 1;

// Checking if number of digits is one
if (n == 1)
    return 9;

// Checking if number of digits is odd
if (n % 2) {

    // Calling digitNumber function
    // with (digit-1)/2 digits
    let temp = digitNumber((n - 1) / 2) % mod;
    return (9 * (temp * temp) % mod) % mod;
} else {

    // Calling digitNumber function
    // with n/2 digits
    let temp = digitNumber(n / 2) % mod;
    return (temp * temp) % mod;
}
}

function countExcluding(n, d)
{
// Calling digitNumber function
// Checking if excluding digit is
// zero or non-zero
if (d == 0)
    return (9 * digitNumber(n - 1)) % mod;
else
    return (8 * digitNumber(n - 1)) % mod;
}

// Driver function to run above program

// Initializing variables
let d = 9;
let n = 3;
document.write(countExcluding(n, d) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
648
```

**时间复杂度:** O(log n)。