# 使用二分搜索法

找到给定精度的数字的平方根

> 原文:[https://www . geesforgeks . org/find-平方根-number-up-给定-precision-use-binary-search/](https://www.geeksforgeeks.org/find-square-root-number-upto-given-precision-using-binary-search/)

给定一个正数 n 和精度 p，用二分搜索法求小数点后 p 位数字的平方根。
**注:**先决条件:[二分搜索法](https://www.geeksforgeeks.org/binary-search/)T5】例:

```
Input : number = 50, precision = 3
Output : 7.071

Input : number = 10, precision = 4
Output : 3.1622
```

我们已经讨论了如何使用二分搜索法
**方法计算[平方根中平方根的整数值:](https://www.geeksforgeeks.org/square-root-of-an-integer/)**
**1)** 由于数字的平方根在范围 0 < =平方根< =数字，因此，初始化开始和结束为:开始= 0，结束=数字。
**2)** 将中间整数的平方与给定的数进行比较。如果等于这个数，求平方根。否则根据场景在左侧或右侧寻找相同的。
**【3)**一旦我们找到了一个整数部分，就开始计算小数部分。
**4)** 将*增量*变量初始化 0.1，迭代计算小数部分至 P 位。每次迭代，*增量*变为其前一值的 1/10。
**5)** 最后返回计算出的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation to find
// square root of given number
// upto given precision using
// binary search.
#include <bits/stdc++.h>
using namespace std;

// Function to find square root
// of given number upto given
// precision
float squareRoot(int number, int precision)
{
    int start = 0, end = number;
    int mid;

    // variable to store the answer
    float ans;

    // for computing integral part
    // of square root of number
    while (start <= end) {
        mid = (start + end) / 2;
        if (mid * mid == number) {
            ans = mid;
            break;
        }

        // incrementing start if integral
        // part lies on right side of the mid
        if (mid * mid < number) {
            start = mid + 1;
            ans = mid;
        }

        // decrementing end if integral part
        // lies on the left side of the mid
        else {
            end = mid - 1;
        }
    }

    // For computing the fractional part
    // of square root upto given precision
    float increment = 0.1;
    for (int i = 0; i < precision; i++) {
        while (ans * ans <= number) {
            ans += increment;
        }

        // loop terminates when ans * ans > number
        ans = ans - increment;
        increment = increment / 10;
    }
    return ans;
}

// Driver code
int main()
{
    // Function calling
    cout << squareRoot(50, 3) << endl;

    // Function calling
    cout << squareRoot(10, 4) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// square root of given number
// upto given precision using
// binary search.
import java.io.*;

class GFG {

    // Function to find square root
    // of given number upto given
    // precision
    static float squareRoot(int number, int precision)
    {
        int start = 0, end = number;
        int mid;

        // variable to store the answer
        double ans = 0.0;

        // for computing integral part
        // of square root of number
        while (start <= end) {
            mid = (start + end) / 2;

            if (mid * mid == number) {
                ans = mid;
                break;
            }

            // incrementing start if integral
            // part lies on right side of the mid
            if (mid * mid < number) {
                start = mid + 1;
                ans = mid;
            }

            // decrementing end if integral part
            // lies on the left side of the mid
            else {
                end = mid - 1;
            }
        }

        // For computing the fractional part
        // of square root upto given precision
        double increment = 0.1;
        for (int i = 0; i < precision; i++) {
            while (ans * ans <= number) {
                ans += increment;
            }

            // loop terminates when ans * ans > number
            ans = ans - increment;
            increment = increment / 10;
        }
        return (float)ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Function calling
        System.out.println(squareRoot(50, 3));

        // Function calling
        System.out.println(squareRoot(10, 4));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 implementation to find
# square root of given number
# upto given precision using
# binary search.

# Function to find square root of
# given number upto given precision

def squareRoot(number, precision):

    start = 0
    end, ans = number, 1

    # For computing integral part
    # of square root of number
    while (start <= end):
        mid = int((start + end) / 2)

        if (mid * mid == number):
            ans = mid
            break

        # incrementing start if integral
        # part lies on right side of the mid
        if (mid * mid < number):
            start = mid + 1
            ans = mid

        # decrementing end if integral part
        # lies on the left side of the mid
        else:
            end = mid - 1

    # For computing the fractional part
    # of square root upto given precision
    increment = 0.1
    for i in range(0, precision):
        while (ans * ans <= number):
            ans += increment

        # loop terminates when ans * ans > number
        ans = ans - increment
        increment = increment / 10

    return ans

# Driver code
print(round(squareRoot(50, 3), 4))
print(round(squareRoot(10, 4), 4))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# implementation to find
// square root of given number
// upto given precision using
// binary search.
using System;
class GFG {

    // Function to find square root
    // of given number upto given
    // precision
    static float squareRoot(int number, int precision)
    {
        int start = 0, end = number;
        int mid;

        // variable to store the answer
        double ans = 0.0;

        // for computing integral part
        // of square root of number
        while (start <= end) {
            mid = (start + end) / 2;

            if (mid * mid == number) {
                ans = mid;
                break;
            }

            // incrementing start if integral
            // part lies on right side of the mid
            if (mid * mid < number) {
                start = mid + 1;
                ans = mid;
            }

            // decrementing end if integral part
            // lies on the left side of the mid
            else {
                end = mid - 1;
            }
        }

        // For computing the fractional part
        // of square root upto given precision
        double increment = 0.1;
        for (int i = 0; i < precision; i++) {
            while (ans * ans <= number) {
                ans += increment;
            }

            // loop terminates when ans * ans > number
            ans = ans - increment;
            increment = increment / 10;
        }
        return (float)ans;
    }

    // Driver code
    public static void Main()
    {
        // Function calling
        Console.WriteLine(squareRoot(50, 3));

        // Function calling
        Console.WriteLine(squareRoot(10, 4));
    }
}

// This code is contributed by Sheharaz Sheikh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// square root of given number
// upto given precision using
// binary search.

// Function to find square root
// of given number upto given
// precision
function squareRoot($number, $precision)
{
    $start=0;
    $end=$number;
    $mid;

    // variable to store
    // the answer
    $ans;

    // for computing integral part
    // of square root of number
    while ($start <= $end)
    {
        $mid = ($start + $end) / 2;
        if ($mid * $mid == $number)
        {
            $ans = $mid;
            break;
        }

        // incrementing start if integral
        // part lies on right side of the mid
        if ($mid * $mid < $number)
        {
            $start = $mid + 1;
            $ans = $mid;
        }

        // decrementing end if integral part
        // lies on the left side of the mid
        else
        {
            $end = $mid - 1;
        }
    }

    // For computing the fractional part
    // of square root upto given precision
    $increment = 0.1;
    for ($i = 0; $i < $precision; $i++)
    {
        while ($ans * $ans <= $number)
        {
            $ans += $increment;
        }

        // loop terminates when
        // ans * ans > number
        $ans = $ans - $increment;
        $increment = $increment / 10;
    }
    return $ans;
}

    // Driver code
    // Function calling
    echo squareRoot(50, 3),"\n";

    // Function calling
    echo squareRoot(10, 4),"\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program implementation to find
// square root of given number
// upto given precision using
// binary search.

    // Function to find square root
    // of given number upto given
    // precision
    function squareRoot(number, precision)
    {
        let start = 0, end = number;
        let mid;

        // variable to store the answer
        let ans = 0.0;

        // for computing integral part
        // of square root of number
        while (start <= end)
        {
            mid = (start + end) / 2;

            if (mid * mid == number)
            {
                ans = mid;
                break;
            }

            // incrementing start if integral
            // part lies on right side of the mid
            if (mid * mid < number) {
                start = mid + 1;
                ans = mid;
            }

            // decrementing end if integral part
            // lies on the left side of the mid
            else {
                end = mid - 1;
            }
        }

        // For computing the fractional part
        // of square root upto given precision
        let increment = 0.1;
        for (let i = 0; i < precision; i++) {
            while (ans * ans <= number) {
                ans += increment;
            }

            // loop terminates when ans * ans > number
            ans = ans - increment;
            increment = increment / 10;
        }
        return ans;
    }

// Driver code

         // Function calling
        document.write(squareRoot(50, 3) + "<br/>");

        // Function calling
        document.write(squareRoot(10, 4) + "<br/>");

</script>
```

**输出:**

```
7.071
3.1622
```

**时间复杂度:**计算整数部分所需的时间为 O(log(number))且为常数，即=计算小数部分的精度。因此，整体时间复杂度为 O(log(数)+精度)，约等于 O(log(数))。