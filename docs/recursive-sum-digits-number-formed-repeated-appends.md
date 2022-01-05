# 重复追加形成的数字的数字递归和

> 原文:[https://www . geeksforgeeks . org/recursive-sum-digits-number-formed-repeated-appends/](https://www.geeksforgeeks.org/recursive-sum-digits-number-formed-repeated-appends/)

给定两个正数 **N** 和 **X** 。任务是求 N 次重复 X 次形成的数的位数之和，直到和变成个位数。

**示例:**

```
Input : N = 24, X = 3
Output : 9
Number formed after repeating 24 three time = 242424
Sum = 2 + 4 + 2 + 4 + 2 + 4
    = 18
Sum is not the single digit, so finding 
the sum of digits of 18,
1 + 8 = 9

Input : N = 4, X = 4
Output : 7
```

正如在[这篇](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)文章中所讨论的，如果数字是 9 的倍数，数字的递归和是 9，否则是 n % 9。由于可除性和模运算与乘法兼容，我们简单地找到单次出现的结果，用 x 乘结果，然后再次找到结果。

**这是如何工作的？**
让 N = 24，X = 3。
所以，sumUntilSingle(N) = 2 + 4 = 6。
6 乘以 3 = 18
sumUntilSingle(18) = 9。

下面是该方法的实现:

## C++

```
// C++ program to find Sum of digits of a
// number formed by repeating a number X number of
// times until sum become single digit.
#include <bits/stdc++.h>
using namespace std;

// return single digit sum of a number.
int digSum(int n)
{
    if (n == 0)
        return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Returns recursive sum of digits of a number
// formed by repeating a number X number of
// times until sum become single digit.
int repeatedNumberSum(int n, int x)
{
    int sum = x*digSum(n);
    return digSum(sum);
}

// Driver program
int main()
{
    int n = 24, x = 3;
    cout << repeatedNumberSum(n, x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum of digits of a
// number formed by repeating a number X number of
// times until sum become single digit.

class GFG {

    // return single digit sum of a number.
    static int digSum(int n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Returns recursive sum of digits of a number
    // formed by repeating a number X number of
    // times until sum become single digit.
    static int repeatedNumberSum(int n, int x)
    {
        int sum = x * digSum(n);
        return digSum(sum);
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 24, x = 3;
        System.out.println(repeatedNumberSum(n, x));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python program to find Sum of digits of a
# number formed by repeating a number X number
# of times until sum become single digit.

# Return single digit sum of a number
def digSum(n):
    if n == 0:
        return 0
    return (n % 9 == 0) and 9 or (n % 9)

# Returns recursive sum of digits of a number
# formed by repeating a number X number of
# times until sum become single digit.
def repeatedNumberSum(n, x):
    sum = x * digSum(n)
    return digSum(sum)

# Driver Code
n = 24; x = 3
print(repeatedNumberSum(n, x))

# This code is contributed by Ajit.
```

## C#

```
// C# program to find Sum of digits of a
// number formed by repeating a number X
// number of times until sum becomes
// single digit.
using System;

public class GFG
{    
    // return single digit sum of a number.
    static int digSum(int n)
    {
        if (n == 0)
            return 0;

        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Returns recursive sum of digits of a
    // number formed by repeating a number X
    // number of times until sum become
    // single digit.
    static int repeatedNumberSum(int n, int x)
    {
        int sum = x * digSum(n);
        return digSum(sum);
    }

    // driver program
    public static void Main ()
    {
        int n = 24, x = 3;
        Console.Write( repeatedNumberSum(n, x));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Sum
// of digits of a number
// formed by repeating a number
// X number of times until
// sum becomes single digit.

// return single digit
// sum of a number.
function digSum($n)
{
    if ($n == 0)
        return 0;
    return ($n % 9 == 0) ? 9 : ($n % 9);
}

// Returns recursive sum of
// digits of a number formed
// by repeating a number X
// number of times until sum
// become single digit.
function repeatedNumberSum( $n, $x)
{
    $sum = $x * digSum($n);
    return digSum($sum);
}

// Driver Code
$n = 24; $x = 3;
echo repeatedNumberSum($n, $x);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find Sum
// of digits of a number formed by
// repeating a number X number of
// times until sum becomes single digit.

// Return single digit
// sum of a number.
function digSum(n)
{
    if (n == 0)
        return 0;

    return (n % 9 == 0) ? 9 : (n % 9);
}

// Returns recursive sum of
// digits of a number formed
// by repeating a number X
// number of times until sum
// become single digit.
function repeatedNumberSum(n, x)
{
    sum = x * digSum(n);
    return digSum(sum);
}

// Driver Code
let n = 24;
let x = 3;

document.write(repeatedNumberSum(n, x));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
9
```