# 检查两个整数的不同位数之和是否相等

> 原文:[https://www . geeksforgeeks . org/检查两个整数的不同位数之和是否相等/](https://www.geeksforgeeks.org/check-if-the-sum-of-distinct-digits-of-two-integers-are-equal/)

给定两个整数 **m** 和 **n** ，任务是找出两个数字的不同数字之和并打印**是**如果两个和相等，则打印**否**。
**举例:**

> **输入:** m = 2452，n = 9222
> **输出:**YES
> 2452 的不同位数之和为 11 (2 + 4 + 5)
> 而 9222 的不同位数之和为 11 (9 + 2)
> **输入:** m = 121，n = 3035
> **输出:** NO

**逼近:**求 **m** 和 **n** 的唯一位数之和，分别存入**sum**和 **sumN** 中。如果**sum = SumN**则打印**是**否则打印**否**。
以下是上述方法的实施:

## C++

```
// C++ program to check if the sum of distinct
// digits of two integers are equal

#include <iostream>
using namespace std;

    // Function to return the sum of
    // distinct digits of a number
     int distinctDigitSum(int n)
    {
        bool used[10];
        int sum = 0;
        while (n > 0) {

            // Take last digit
            int digit = n % 10;

            // If digit has not been used before
            if (!used[digit]) {

                // Set digit as used
                used[digit] = true;
                sum += digit;
            }

            // Remove last digit
            n = (int)n / 10;
        }

        return sum;
    }

    // Function to check whether the sum of
    // distinct digits of two numbers are equal
     string checkSum(int m, int n)
    {
        int sumM = distinctDigitSum(m);
        int sumN = distinctDigitSum(n);

        if (sumM != sumN)
            return "YES";
        return "NO";
    }

    // Driver code
    int main() {

        int m = 2452, n = 9222;
        cout << (checkSum(m, n));
        return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the sum of distinct
// digits of two integers are equal
public class HelloWorld {

    // Function to return the sum of
    // distinct digits of a number
    static int distinctDigitSum(int n)
    {
        boolean used[] = new boolean[10];
        int sum = 0;
        while (n > 0) {

            // Take last digit
            int digit = n % 10;

            // If digit has not been used before
            if (!used[digit]) {

                // Set digit as used
                used[digit] = true;
                sum += digit;
            }

            // Remove last digit
            n = n / 10;
        }

        return sum;
    }

    // Function to check whether the sum of
    // distinct digits of two numbers are equal
    static String checkSum(int m, int n)
    {
        int sumM = distinctDigitSum(m);
        int sumN = distinctDigitSum(n);

        if (sumM == sumN)
            return "YES";
        return "NO";
    }

    // Driver code
    public static void main(String[] args)
    {
        int m = 2452, n = 9222;
        System.out.println(checkSum(m, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if the sum of
# distinct digits of two integers are equal

# Function to return the sum of
# distinct digits of a number
def distinctDigitSum(n) :

    used = [False] * 10
    sum = 0
    while (n > 0) :

        # Take last digit
        digit = n % 10

        # If digit has not been used before
        if (not used[digit]) :

            # Set digit as used
            used[digit] = True
            sum += digit

        # Remove last digit
        n = n // 10

    return sum

# Function to check whether the sum of
# distinct digits of two numbers are equal
def checkSum(m, n) :

    sumM = distinctDigitSum(m)
    sumN = distinctDigitSum(n)

    if (sumM == sumN) :
        return "YES"
    return "NO"

# Driver code
if __name__ == "__main__" :

    m = 2452
    n = 9222

    print(checkSum(m, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to check if the sum of distinct
// digits of two integers are equal

// Function to return the sum of
// distinct digits of a number

using System;

public class GFG{
        static int distinctDigitSum(int n)
    {
        bool []used = new bool[10];
        int sum = 0;
        while (n > 0) {

            // Take last digit
            int digit = n % 10;

            // If digit has not been used before
            if (!used[digit]) {

                // Set digit as used
                used[digit] = true;
                sum += digit;
            }

            // Remove last digit
            n = n / 10;
        }

        return sum;
    }

    // Function to check whether the sum of
    // distinct digits of two numbers are equal
    static String checkSum(int m, int n)
    {
        int sumM = distinctDigitSum(m);
        int sumN = distinctDigitSum(n);

        if (sumM == sumN)
            return "YES";
        return "NO";
    }

    // Driver code
    static public void Main (){
        int m = 2452, n = 9222;
        Console.WriteLine(checkSum(m, n));
    }
//This code is contributed by akt_mit   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if the sum of distinct
// digits of two integers are equal

// Function to return the sum of
// distinct digits of a number
function distinctDigitSum($n)
{
    $used[10] = array();
    $sum = 0;
    while ($n > 0)
    {

        // Take last digit
        $digit = $n % 10;

        // If digit has not been used before
        if ($used > 0)
        {

            // Set digit as used
            $used[$digit] = true;
            $sum += $digit;
        }

        // Remove last digit
        $n = (int)$n / 10;
    }

    return $sum;
}

// Function to check whether the sum of
// distinct digits of two numbers are equal
function checkSum($m, $n)
{
    $sumM = distinctDigitSum($m);
    $sumN = distinctDigitSum($n);

    if ($sumM != $sumN)
        return "YES";
    return "NO";
}

// Driver code
$m = 2452;
$n = 9222;
echo (checkSum($m, $n));

// This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>
// javascript program to check if the sum of distinct
// digits of two integers are equal

    // Function to return the sum of
    // distinct digits of a number
    function distinctDigitSum(n)
    {
        var used = Array(10).fill(false);
        var sum = 0;
        while (n > 0)
        {

            // Take last digit
            var digit = n % 10;

            // If digit has not been used before
            if (!used[digit]) {

                // Set digit as used
                used[digit] = true;
                sum += digit;
            }

            // Remove last digit
            n = parseInt(n / 10);
        }

        return sum;
    }

    // Function to check whether the sum of
    // distinct digits of two numbers are equal
    function checkSum(m , n) {
        var sumM = distinctDigitSum(m);
        var sumN = distinctDigitSum(n);

        if (sumM == sumN)
            return "YES";
        return "NO";
    }

    // Driver code
        var m = 2452, n = 9222;
        document.write(checkSum(m, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
YES
```