# 用其他数字替换一个数字的程序

> 原文:[https://www . geesforgeks . org/用其他替换一位数的程序/](https://www.geeksforgeeks.org/program-for-replacing-one-digit-with-other/)

给定一个数字 x 和两个数字 d1 和 d2，在 x 中用 d2 替换 D1。
**示例:**

```
Input : x = 645, d1 = 6, d2 = 5
Output : 545
We replace digit 6 with 5 in number 645.

Input  : x = 746, d1 = 7, d2 = 8
Output : 846
```

我们遍历 x 的所有数字。对于每个数字，我们检查它是否是 d1，并相应地更新结果。

## C++

```
// CPP program to replace a digit with other
// in a given number.
#include <bits/stdc++.h>
using namespace std;

int replaceDigit(int x, int d1, int d2)
{
    int result = 0, multiply = 1;

    while (x / 10 > 0)
    {

        // Take remainder of number starting from
        // the unit place digit
        int remainder = x % 10;

        // check whether it is equal to the digit
        // to be replaced.if yes then replace
        if (remainder == d1)
            result = result + d2 * multiply;

        else // else remain as such
            result = result + remainder * multiply;

        // Update and move forward from unit place
        // to hundred place and so on.
        multiply *= 10;
        x = x / 10; // update the value
    }

    // check whether it is equal to the digit
    // to be replaced.if yes then replace
    if (x == d1)
        result = result + d2 * multiply;

    else // else remain as such
        result = result + x * multiply;

    return result;
}

// Driver code
int main()
{
    int x = 645, d1 = 6, d2 = 5;
    cout << replaceDigit(x, d1, d2) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace a digit
// with other in a given number.
class GFG
{
    static int replaceDigit(int x, int d1, int d2)
    {
        int result = 0, multiply = 1;

        while (x / 10 > 0)
        {

            // Take remainder of number
            // starting from the unit
            // place digit
            int remainder = x % 10;

            // check whether it is equal
            // to the digit to be replaced.
            // if yes then replace
            if (remainder == d1)
                result = result + d2 * multiply;

            else // else remain as such
                result = result + remainder * multiply;

            // Update and move forward
            // from unit place to
            // hundred place and so on.
            multiply *= 10;
            x = x / 10; // update the value
        }

        // check whether it is equal to the digit
        // to be replaced.if yes then replace
        if (x == d1)
            result = result + d2 * multiply;

        else // else remain as such
            result = result + x * multiply;
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 645, d1 = 6, d2 = 5;
        System.out.println(replaceDigit(x, d1, d2));
    }
}

// This Code is Contributed by mits
```

## 蟒蛇 3

```
# Python3 program to replace
# a digit with other
# in a given number.

def replaceDigit(x, d1, d2):
    result = 0
    multiply = 1

    while (x // 10 > 0):

        # Take remainder of number
        # starting from the unit
        # place digit
        remainder = x % 10

        # check whether it is
        # equal to the digit
        # to be replaced.if yes
        # then replace
        if (remainder == d1):
            result = (result + d2 *
                      multiply)

        else:  # else remain as such
            result = (result + remainder *
                      multiply)

        # Update and move forward
        # from unit place to hundred
        # place and so on.
        multiply *= 10
        x = int(x / 10)  # update the value

    # check whether it is equal to the digit
    # to be replaced.if yes then replace
    if (x == d1):
        result = result + d2 * multiply

    else:  # else remain as such
        result = result + x * multiply
    return result

# Driver code
x = 645
d1 = 6
d2 = 5
print(replaceDigit(x, d1, d2))

# This Code is contributed
# by mits
```

## C#

```
// C# program to replace a digit
// with other in a given number
using System;
class GFG
{
    static int replaceDigit(int x, int d1, int d2)
    {
        int result = 0, multiply = 1;

        while (x / 10 > 0)
        {

            // Take remainder of number
            // starting from the unit
            // place digit
            int remainder = x % 10;

            // check whether it is equal
            // to the digit to be replaced.
            // if yes then replace
            if (remainder == d1)
                result = result + d2 * multiply;

            else // else remain as such
                result = result + remainder * multiply;

            // Update and move forward
            // from unit place to
            // hundred place and so on.
            multiply *= 10;
            x = x / 10; // update the value
        }

        // check whether it is equal to the digit
        // to be replaced.if yes then replace
        if (x == d1)
            result = result + d2 * multiply;

        else // else remain as such
            result = result + x * multiply;
        return result;
    }

    // Driver code
    public static void Main()
    {
        int x = 645, d1 = 6, d2 = 5;
        Console.WriteLine(replaceDigit(x, d1, d2));
    }
}

// This Code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace
// a digit with other
// in a given number.

function replaceDigit($x, $d1, $d2)
{
    $result = 0; $multiply = 1;

    while ($x / 10 > 0)
    {

        // Take remainder of number
        // starting from the unit
        // place digit
        $remainder = $x % 10;

        // check whether it is
        // equal to the digit
        // to be replaced.if yes
        // then replace
        if ($remainder == $d1)
            $result = $result + $d2 *
                           $multiply;

        else // else remain as such
            $result = $result + $remainder *
                                $multiply;    

        // Update and move forward
        // from unit place to hundred
        // place and so on.
        $multiply *= 10;
        $x = $x / 10; // update the value
    }

    // check whether it is equal to the digit
    // to be replaced.if yes then replace
    if ($x == $d1)
        $result = $result + $d2 * $multiply;

    else // else remain as such
        $result = $result + $x * $multiply;
    return $result;
}

// Driver code
$x = 645; $d1 = 6; $d2 = 5;
echo replaceDigit($x, $d1, $d2);

// This Code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
    // Javascript program to replace a digit
    // with other in a given number

    function replaceDigit(x, d1, d2)
    {
        let result = 0, multiply = 1;

        while (parseInt(x / 10, 10) > 0)
        {

            // Take remainder of number
            // starting from the unit
            // place digit
            let remainder = x % 10;

            // check whether it is equal
            // to the digit to be replaced.
            // if yes then replace
            if (remainder == d1)
                result = result + d2 * multiply;

            else // else remain as such
                result = result + remainder * multiply;

            // Update and move forward
            // from unit place to
            // hundred place and so on.
            multiply *= 10;
            x = parseInt(x / 10, 10); // update the value
        }

        // check whether it is equal to the digit
        // to be replaced.if yes then replace
        if (x == d1)
            result = result + d2 * multiply;

        else // else remain as such
            result = result + x * multiply;
        return result;
    }

    let x = 645, d1 = 6, d2 = 5;
      document.write(replaceDigit(x, d1, d2));

// This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
545
```