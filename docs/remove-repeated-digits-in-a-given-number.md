# 删除给定号码中重复的数字

> 原文:[https://www . geesforgeks . org/remove-给定号码中的重复数字/](https://www.geeksforgeeks.org/remove-repeated-digits-in-a-given-number/)

给定一个整数，从中删除连续重复的数字。
**例:**

```
Input: x = 12224
Output: 124

Input: x = 124422
Output: 1242

Input: x = 11332
Output: 132
```

我们需要处理 n 的所有数字，并删除连续的表示。我们可以通过重复用 10 除 n 并取 n%10 来遍历所有数字。

## C++

```
// C++ program to remove repeated digits
#include <iostream>
using namespace std;

long int removeRecur(long int n)
{
    // Store first digits as previous digit
    int prev_digit = n % 10;

    // Initialize power
    long int pow = 10;
    long int res = prev_digit;

    // Iterate through all digits of n, note that
    // the digits are processed from least significant
    // digit to most significant digit.
    while (n) {
        // Store current digit
        int curr_digit = n % 10;

        if (curr_digit != prev_digit) {
            // Add the current digit to the beginning
            // of result
            res += curr_digit * pow;

            // Update previous result and power
            prev_digit = curr_digit;
            pow *= 10;
        }

        // Remove last digit from n
        n = n / 10;
    }

    return res;
}

// Driver program
int main()
{
    long int n = 12224;
    cout << removeRecur(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove repeated digits
import java.io.*;

class GFG {

    static long removeRecur(long n)
    {

        // Store first digits as previous
        // digit
        long prev_digit = n % 10;

        // Initialize power
        long pow = 10;
        long res = prev_digit;

        // Iterate through all digits of n,
        // note that the digits are
        // processed from least significant
        // digit to most significant digit.
        while (n>0) {

            // Store current digit
            long curr_digit = n % 10;

            if (curr_digit != prev_digit)
            {
                // Add the current digit to
                // the beginning of result
                res += curr_digit * pow;

                // Update previous result
                // and power
                prev_digit = curr_digit;
                pow *= 10;
            }

            // Remove last digit from n
            n = n / 10;
        }

        return res;
    }

    // Driver program
    public static void main (String[] args)
    {
        long n = 12224;

        System.out.println(removeRecur(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to remove repeated digits

def removeRecur(n):

    # Store first digits as previous digit
    prev_digit = n % 10

    # Initialize power
    pow = 10
    res = prev_digit

    # Iterate through all digits of n, note
    # that the digits are processed from
    # least significant digit to most
    # significant digit.
    while (n):

        # Store current digit
        curr_digit = n % 10

        if (curr_digit != prev_digit):

            # Add the current digit to the
            # beginning of result
            res += curr_digit * pow

            # Update previous result and power
            prev_digit = curr_digit
            pow *= 10

        # Remove last digit from n
        n = int(n / 10)

    return res

# Driver Code
if __name__ == '__main__':
    n = 12224
    print(removeRecur(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to remove repeated digits
using System;

class GFG {

    static long removeRecur(long n)
    {

        // Store first digits as previous
        // digit
        long prev_digit = n % 10;

        // Initialize power
        long pow = 10;
        long res = prev_digit;

        // Iterate through all digits of n,
        // note that the digits are
        // processed from least significant
        // digit to most significant digit.
        while (n > 0) {

            // Store current digit
            long curr_digit = n % 10;

            if (curr_digit != prev_digit)
            {
                // Add the current digit to
                // the beginning of result
                res += curr_digit * pow;

                // Update previous result
                // and power
                prev_digit = curr_digit;
                pow *= 10;
            }

            // Remove last digit from n
            n = n / 10;
        }

        return res;
    }

    // Driver program
    public static void Main ()
    {
        long n = 12224;

        Console.WriteLine(removeRecur(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to remove
// repeated digits

function removeRecur($n)
{

    // Store first digits
    // as previous digit
    $prev_digit = $n % 10;

    // Initialize power
    $pow = 10;
    $res = $prev_digit;

    // Iterate through all digits
    // of n, note that the digits
    // are processed from least
    // significant digit to most
    // significant digit.
    while ($n)
    {

        // Store current digit
        $curr_digit = $n%10;

        if ($curr_digit != $prev_digit)
        {
            // Add the current digit
            // to the beginning of
            // result
            $res += $curr_digit * $pow;

            // Update previous result
            // and power
            $prev_digit = $curr_digit;
            $pow *= 10;
        }

        // Remove last digit
        // from n
        $n = $n / 10;
    }

    return $res;
}

    // Driver Code
    $n = 12224;
    echo removeRecur($n);

// This ocde is contributed by ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to
    // remove repeated digits

    function removeRecur(n)
    {

        // Store first digits as previous
        // digit
        let prev_digit = n % 10;

        // Initialize power
        let pow = 10;
        let res = prev_digit;

        // Iterate through all digits of n,
        // note that the digits are
        // processed from least significant
        // digit to most significant digit.
        while (n > 0) {

            // Store current digit
            let curr_digit = n % 10;

            if (curr_digit != prev_digit)
            {
                // Add the current digit to
                // the beginning of result
                res += curr_digit * pow;

                // Update previous result
                // and power
                prev_digit = curr_digit;
                pow *= 10;
            }

            // Remove last digit from n
            n = parseInt(n / 10, 10);
        }

        return res;
    }

    let n = 12224;

      document.write(removeRecur(n));

</script>
```

**输出:**

```
124
```

时间复杂度:O(log <sub>10</sub> n)

辅助空间:0(1)

本文由 Kartik 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息