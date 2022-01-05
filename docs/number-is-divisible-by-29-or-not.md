# 数能不能被 29 整除

> 原文:[https://www . geesforgeks . org/number-is-by-29-or-not/](https://www.geeksforgeeks.org/number-is-divisible-by-29-or-not/)

给定一个大的数 n，找出这个数是否能被 29 整除。
**例:**

```
Input : 363927598
Output : No

Input : 292929002929
Output : Yes
```

> 检查一个数字是否能被 29 整除的一个快速方法是将最后一个数字的 3 倍加到剩余的数字上，并重复这个过程，直到数字变成 2 位数。如果得到的两位数能被 29 整除，则给定的数能被 29 整除。
> 数是 348，
> 最后一位数字的三倍+数的其余部分= 8*3 + 34 = 58
> 既然 58 能被 29 整除，那么 348 也能被 29 整除。

## C++

```
// CPP program to demonstrate above method
// to check divisibility by 29.
#include <iostream>
using namespace std;

// Returns true if n is divisible by 29
// else returns false.
bool isDivisible(long long int n)
{
    // add the lastdigit*3 to renaming
    // number until number comes only
    // 2 digit
    while (n / 100)
    {
        int last_digit = n % 10;
        n /= 10;
        n += last_digit * 3;
    }

    // return true if number is
    // divisible by 29 another
    return (n % 29 == 0);
}

// Driver Code
int main()
{
    long long int n = 348;
    if (isDivisible(n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate above method
// to check divisibility by 29.

import java.io.*;

class GFG {

    // Returns true if n is divisible by 29
    // else returns false.
    static boolean isDivisible(long n)
    {

        // add the lastdigit*3 to renaming
        // number until number comes only
        // 2 digit
        while (n / 100 > 0) {

            int last_digit = (int)n % 10;
            n /= 10;
            n += last_digit * 3;
        }

        // return true if number is
        // divisible by 29 another
        return (n % 29 == 0);
    }

    // Driver code
    public static void main(String[] args)
    {
        long n = 348;

        if (isDivisible(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to demonstrate above
# method to check divisibility by 29.

# Returns true if n is divisible
# by 29 else returns false.
def isDivisible(n):

    # add the lastdigit*3 to renaming
    # number until number comes only
    # 2 digit
    while (int(n / 100)) :
        last_digit = int(n % 10)
        n = int(n / 10)
        n += last_digit * 3

    # return true if number is
    # divisible by 29 another
    return (n % 29 == 0)

# Driver Code
n = 348

if(isDivisible(n) != 0):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to demonstrate above method
// to check divisibility by 29.
using System;
class GFG
{

    // Returns true if n is divisible by 29
    // else returns false.
    static bool isDivisible(long n)
    {

        // add the lastdigit*3 to renaming
        // number until number comes only
        // 2 digit
        while (n / 100 > 0)
        {

            int last_digit = (int)n % 10;
            n /= 10;
            n += last_digit * 3;
        }

        // return true if number is
        // divisible by 29 another
        return (n % 29 == 0);
    }

    // Driver code
    public static void Main()
    {
        long n = 348;

        if (isDivisible(n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to demonstrate
// above method to check
// divisibility by 29.

// Returns true if n is
// divisible by 29
// else returns false.
function isDivisible($n)
{
    // add the lastdigit*3 to
    // remaining number until
    // number becomes of only
    // 2 digit
    while (intval($n / 100))
    {
        $last_digit = $n % 10;
        $n = intval($n / 10);
        $n += $last_digit * 3;
    }

    // return true if number is
    // divisible by 29 another
    return ($n % 29 == 0);
}

// Driver Code
$n = 348;
if (isDivisible($n))
    echo "Yes";
else
    echo "No" ;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// Javascript program to demonstrate
// above method to check
// divisibility by 29.

// Returns true if n is
// divisible by 29
// else returns false.
function isDivisible(n)
{

    // add the lastdigit*3 to
    // remaining number until
    // number becomes of only
    // 2 digit
    while (parseInt(n / 100))
    {
        let last_digit = n % 10;
        n = parseInt(n / 10);
        n += last_digit * 3;
    }

    // return true if number is
    // divisible by 29 another
    return (n % 29 == 0);
}

// Driver Code
let n = 348;
if (isDivisible(n))
    document.write("Yes");
else
    document.write("No") ;

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output :** 

```
Yes
```