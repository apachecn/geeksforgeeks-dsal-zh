# 检查 N 是否能被集合{A，B}

中的数字组成的数字整除

> 原文:[https://www . geesforgeks . org/check-if-n-n-是由集合 a-b 中的数字组成的可被数字整除的数/](https://www.geeksforgeeks.org/check-if-n-is-divisible-by-a-number-which-is-composed-of-the-digits-from-the-set-a-b/)

给定三个整数 **N** 、 **A** 和 **B** ，任务是找出 N 是否能被任何只包含 **A** 和 **B** 的数字整除。

**示例:**

> **输入:** N = 106，a = 3，b = 5
> **输出:**是
> 106 可被 53 整除
> 
> **输入:** N = 107，a = 3，b = 5
> **输出:**否

**方法 1(递归):**一个有效的解决方案是使用从数字 **a** 和 **b** 开始的递归函数，将包含 **a** 和 **b** 的所有数字作为它们的数字。如果函数调用是 **fun(x)** 那么递归调用为 **fun(x * 10 + a)** 和 **fun(x * 10 + b)** 。如果 **n** 可被任意数字整除，则打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program to find if number N is divisible by a
// number that contains only a and b as it's digits
#include <bits/stdc++.h>
using namespace std;

// Function to check whether n is divisible
// by a number whose digits are either a or b
bool isDivisibleRec(int x, int a, int b, int n)
{
    // base condition
    if (x > n)
        return false;

    if (n % x == 0)
        return true;

    // recursive call
    return (isDivisibleRec(x * 10 + a, a, b, n)
            || isDivisibleRec(x * 10 + b, a, b, n));
}

bool isDivisible(int a, int b, int n)
{
   // Check for all numbers beginning with 'a' or 'b'
   return isDivisibleRec(a, a, b, n) ||
          isDivisibleRec(b, a, b, n);
}

// Driver program
int main()
{
    int a = 3, b = 5, n = 53;

    if (isDivisible(a, b, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if number N is divisible by a
// number that contains only a and b as it's digits

import java.util.*;
class solution
{

// Function to check whether n is divisible
// by a number whose digits are either a or b
static boolean isDivisibleRec(int x, int a, int b, int n)
{
    // base condition
    if (x > n)
        return false;

    if (n % x == 0)
        return true;

    // recursive call
    return (isDivisibleRec(x * 10 + a, a, b, n)
            || isDivisibleRec(x * 10 + b, a, b, n));
}

static boolean isDivisible(int a, int b, int n)
{
// Check for all numbers beginning with 'a' or 'b'
return isDivisibleRec(a, a, b, n)
        ||isDivisibleRec(b, a, b, n);
}

// Driver program
public static void main(String args[])
{
    int a = 3, b = 5, n = 53;

    if (isDivisible(a, b, n))
        System.out.print("Yes");
    else
        System.out.print("No");

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find if number N
# is divisible by a number that contains
# only a and b as it's digits

# Function to check whether n is divisible
# by a number whose digits are either a or b
def isDivisibleRec(x, a, b, n):

    # base condition
    if (x > n):
        return False

    if (n % x == 0):
        return True

    # recursive call
    return (isDivisibleRec(x * 10 + a, a, b, n) or
            isDivisibleRec(x * 10 + b, a, b, n))

def isDivisible(a, b, n):

    # Check for all numbers beginning
    # with 'a' or 'b'
    return (isDivisibleRec(a, a, b, n) or
            isDivisibleRec(b, a, b, n))

# Driver Code
a = 3; b = 5; n = 53;

if (isDivisible(a, b, n)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to find if number N is
// divisible by a number that contains
// only a and b as it's digits
using System;

class GFG
{

// Function to check whether n is divisible
// by a number whose digits are either a or b
static bool isDivisibleRec(int x, int a,
                           int b, int n)
{
    // base condition
    if (x > n)
        return false;

    if (n % x == 0)
        return true;

    // recursive call
    return (isDivisibleRec(x * 10 + a, a, b, n) ||
            isDivisibleRec(x * 10 + b, a, b, n));
}

static bool isDivisible(int a, int b, int n)
{

// Check for all numbers beginning
// with 'a' or 'b'
return isDivisibleRec(a, a, b, n) ||
       isDivisibleRec(b, a, b, n);
}

// Driver Code
static public void Main ()
{
    int a = 3, b = 5, n = 53;

    if (isDivisible(a, b, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if number N is
// divisible by a number that contains
// only a and b as it's digits

// Function to check whether n is divisible
// by a number whose digits are either a or b
function isDivisibleRec($x, $a, $b, $n)
{
    // base condition
    if ($x > $n)
        return false;

    if ($n % $x == 0)
        return true;

    // recursive call
    return (isDivisibleRec($x * 10 + $a, $a, $b, $n) ||
            isDivisibleRec($x * 10 + $b, $a, $b, $n));
}

function isDivisible($a, $b, $n)
{

// Check for all numbers beginning
// with 'a' or 'b'
return isDivisibleRec($a, $a, $b, $n) ||
       isDivisibleRec($b, $a, $b, $n);
}

// Driver Code
$a = 3; $b = 5; $n = 53;

if (isDivisible($a, $b, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript program to find if number
// N is divisible by a number that
// contains only a and b as it's digits

// Function to check whether n is divisible
// by a number whose digits are either a or b
function isDivisibleRec(x, a, b, n)
{

    // Base condition
    if (x > n)
        return false;

    if (n % x == 0)
        return true;

    // Recursive call
    return(isDivisibleRec(x * 10 + a, a, b, n) ||
           isDivisibleRec(x * 10 + b, a, b, n));
}

function isDivisible(a, b, n)
{

    // Check for all numbers beginning
    // with 'a' or 'b'
    return isDivisibleRec(a, a, b, n) ||
           isDivisibleRec(b, a, b, n);
}

// Driver code
let a = 3, b = 5, n = 53;

if (isDivisible(a, b, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
Yes
```

**方法 2(基于队列):**想法是生成包含数字 a 和 b 的所有数字(小于 n)。对于每个数字，检查它是否除以 n。如何生成所有小于 n 的数字？我们用队列来做这个。最初，我们将“a”和“b”推到队列中。然后我们在队列前面小于 n 的时候运行一个循环。我们逐个弹出一个项目，对于每个弹出的项目 x，我们生成下一个数字 x*10 + a 和 x*10 + b，并将它们排队。该方法的时间复杂度为 O(n)
实施该方法请参考下面的帖子。
[小于 N 的二进制数字计数](https://www.geeksforgeeks.org/count-binary-digit-numbers-smaller-n/)