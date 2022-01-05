# 使用按位运算符

检查一个数是否能被 17 整除

> 原文:[https://www . geesforgeks . org/check-number-除数-17-使用按位运算符/](https://www.geeksforgeeks.org/check-number-divisible-17-using-bitwise-operators/)

给定一个数字 n，使用按位运算符检查它是否能被 17 整除。
示例:

```
Input : n = 34
Output : 34 is divisible by 17

Input :  n = 43
Output : 43 is not divisible by 17
```

一种简单的方法是，如果剩余值为 0，则由%运算符进行检查。
要使用**按位运算符**进行除法运算，我们必须用 2 的幂重写表达式。

```
n/17 = (16*n)/(17*16)
     = (17 - 1)*n/(17*16)
     = (n/16) - (n/(17*16))
```

我们可以用除法的一般规则把 n/16 改写成 floor(n/16) + (n%16)/16。

```
n/17 = floor(n/16) + (n%16)/16 - 
       (floor(n/16) + (n%16)/16)/17
     = floor(n/16) - (floor(n/16) - 
            17*(n%16)/16 + (n%16)/16)/17
     = floor(n/16) - (floor(n/16)-n%16)/17
```

这个方程的左手边是 n/17。只有当右边是整数时，它才是整数。根据定义，floor(n/16)是一个整数。因此，如果(floor(n/16)-n%16)/17 也是整数，那么整个左侧将是一个整数。
这意味着如果(地板(n/16)-n%16)能被 17 整除，则 n 能被 17 整除。
**(楼层(n/16)-n%16)** 可以按位写成**(int)(n>>4)–(int)(n&15)**其中 n > > 4 表示 n/16，n & 15 表示 n%16
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to check if a number is
// divisible by 17 or not using bitwise
// operator.
#include <bits/stdc++.h>
using namespace std;

// function to check recursively if the
// number is divisible by 17 or not
bool isDivisibleby17(int n)
{
    // if n=0 or n=17 then yes
    if (n == 0 || n == 17)
        return true;

    // if n is less then 17, not
    // divisible by 17
    if (n < 17)
        return false;

    // reducing the number by floor(n/16)
    // - n%16
    return isDivisibleby17((int)(n >> 4) - (int)(n & 15));
}

// driver code to check the above function
int main()
{
    int n = 35;
    if (isDivisibleby17(n))
        cout << n << " is divisible by 17";
    else
        cout << n << " is not divisible by 17";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// divisible by 17 or not using bitwise
// operator.
class GFG{

    // function to check recursively if the
    // number is divisible by 17 or not
    static boolean isDivisibleby17(int n)
    {

        // if n=0 or n=17 then yes
        if (n == 0 || n == 17)
            return true;

        // if n is less then 17, not
        // divisible by 17
        if (n < 17)
            return false;

        // reducing the number by
        // floor(n/16) - n%16
        return isDivisibleby17((int)(n >> 4)
                            - (int)(n & 15));
    }

    // driver function
    public static void main(String[] args)
    {
        int n = 35;
        if (isDivisibleby17(n) == true)
            System.out.printf
            ("%d is divisible by 17",n);
        else
            System.out.printf
            ("%d is not divisible by 17",n);
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to
# check if a number is
# divisible by 17 or
# not using bitwise
# operator.

# function to check recursively if the
# number is divisible by 17 or not
def isDivisibleby17(n):

    # if n=0 or n=17 then yes
    if (n == 0 or n == 17):
        return True

    # if n is less then 17, not
    # divisible by 17
    if (n < 17):
        return False

    # reducing the number by floor(n/16)
    # - n%16
    return isDivisibleby17((int)(n >> 4) - (int)(n & 15))

# driver code to check the above function
n = 35
if (isDivisibleby17(n)):
    print(n,"is divisible by 17")
else:
    print(n,"is not divisible by 17")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to check if a number is
// divisible by 17 or not using bitwise
// operator.
using System;

class GFG
{

    // function to check recursively if the
    // number is divisible by 17 or not
    static bool isDivisibleby17(int n)
    {

        // if n=0 or n=17 then yes
        if (n == 0 || n == 17)
            return true;

        // if n is less then 17, not
        // divisible by 17
        if (n < 17)
            return false;

        // reducing the number by
        // floor(n/16) - n%16
        return isDivisibleby17((int)(n >> 4)
                            - (int)(n & 15));
    }

    // Driver function
    public static void Main()
    {
        int n = 35;
        if (isDivisibleby17(n) == true)
            Console.WriteLine
            (n +"is divisible by 17");
        else
            Console.WriteLine
            ( n+ " is not divisible by 17");
    }
}

// This code is contributed by
// vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to check if a
// number is divisible by 17
// or not using bitwise
// operator.

// function to check recursively
// if the number is divisible
// by 17 or not
function isDivisibleby17($n)
{

    // if n=0 or n=17 then yes
    if ($n == 0 || $n == 17)
        return true;

    // if n is less then 17, not
    // divisible by 17
    if ($n < 17)
        return false;

    // reducing the number by floor(n/16)
    // - n%16
    return isDivisibleby17((int)($n >> 4) -
                            (int)($n & 15));
}

    // Driver Code
    $n = 35;
    if (isDivisibleby17($n))
        echo $n." is divisible by 17";
    else
        echo $n." is not divisible by 17";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if a number is
// divisible by 17 or not using bitwise
// operator.

// function to check recursively if the
// number is divisible by 17 or not
function isDivisibleby17(n)
{
    // if n=0 or n=17 then yes
    if (n == 0 || n == 17)
        return true;

    // if n is less then 17, not
    // divisible by 17
    if (n < 17)
        return false;

    // reducing the number by floor(n/16)
    // - n%16
    return isDivisibleby17(Math.floor(n >> 4) - Math.floor(n & 15));
}

// driver code to check the above function

    let n = 35;
    if (isDivisibleby17(n))
        document.write(n + " is divisible by 17");
    else
        document.write(n + " is not divisible by 17");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
35 is not divisible by 17
```