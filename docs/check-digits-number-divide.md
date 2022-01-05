# 检查一个数字的所有数字是否都除了

> 原文:[https://www.geeksforgeeks.org/check-digits-number-divide/](https://www.geeksforgeeks.org/check-digits-number-divide/)

给定一个数 n，求 n 的所有数字是否都除。
示例:

```
Input : 128
Output : Yes
128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0.

Input : 130
Output : No
```

我们想测试每个数字是否非零，并对数字进行除法运算。比如用 128，我们要测试 d！= 0 && 128 % d == 0 表示 d = 1，2，8。为此，我们需要迭代数字的每个数字。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to check the number
// is divisible by all digits are not.
#include <bits/stdc++.h>
using namespace std;

// Function to check the divisibility
// of the number by its digit.
bool checkDivisibility(int n, int digit)
{
    // If the digit divides the number
    // then return true else return false.
    return (digit != 0 && n % digit == 0);
}

// Function to check if all digits
// of n divide it or not
bool allDigitsDivide(int n)
{
    int temp = n;
    while (temp > 0) {

        // Taking the digit of the
        // number into digit var.
        int digit = temp % 10;
        if (!(checkDivisibility(n, digit)))
            return false;

        temp /= 10;
    }
    return true;
}

// Driver function
int main()
{
    int n = 128;
    if (allDigitsDivide(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether
// number is divisible by all its digits.
import java.io.*;

class GFG {

    // Function to check the divisibility
    // of the number by its digit.
    static boolean checkDivisibility(int n, int digit)
    {
        // If the digit divides the number
        // then return  true else return false.
        return (digit != 0 && n % digit == 0);
    }

    // Function to check if all
    // digits of n divide it or not,
    static boolean allDigitsDivide(int n)
    {
        int temp = n;
        while (temp > 0) {

            // Taking the digit of the
            // number into var 'digit'.
            int digit = temp % 10;

            if ((checkDivisibility(n, digit)) == false)
                return false;

            temp /= 10;
        }
        return true;
    }

    // Driver function
    public static void main(String args[])
    {
        int n = 128;

        // function call to check
        // digits divisibility
        if (allDigitsDivide(n))
            System.out.println("Yes");

        else
            System.out.println("No");
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to
# check the number is
# divisible by all
# digits are not.

# Function to check
# the divisibility
# of the number by
# its digit.
def checkDivisibility(n, digit) :

    # If the digit divides the
    # number then return true
    # else return false.
    return (digit != 0 and n % digit == 0)

# Function to check if
# all digits of n divide
# it or not
def allDigitsDivide( n) :

    temp = n
    while (temp > 0) :

        # Taking the digit of
        # the number into digit
        # var.
        digit = temp % 10
        if ((checkDivisibility(n, digit)) == False) :
            return False

        temp = temp // 10

    return True

# Driver function
n = 128

if (allDigitsDivide(n)) :
    print("Yes")
else :
    print("No" )

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check whether
// number is divisible by all its digits.
using System;

class GFG {

    // Function to check the divisibility
    // of the number by its digit.
    static bool checkDivisibility(int n, int digit)
    {
        // If the digit divides the number
        // then return true else return false.
        return (digit != 0 && n % digit == 0);
    }

    // Function to check if all
    // digits of n divide it or not,
    static bool allDigitsDivide(int n)
    {
        int temp = n;
        while (temp > 0) {

            // Taking the digit of the
            // number into var 'digit'.
            int digit = temp % 10;

            if ((checkDivisibility(n, digit)) == false)
                return false;

            temp /= 10;
        }
        return true;
    }

    // Driver function
    public static void Main()
    {
        int n = 128;

        // function call to check
        // digits divisibility
        if (allDigitsDivide(n))
            Console.WriteLine("Yes");

        else
            Console.WriteLine("No");
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to check the number
// is divisible by all digits are not.

// Function to check the divisibility
// of the number by its digit.
function checkDivisibility($n, $digit)
{

    // If the digit divides the number
    // then return true else return false.
    return ($digit != 0 && $n % $digit == 0);
}

// Function to check if all digits
// of n divide it or not
function allDigitsDivide($n)
{
    $temp = $n;
    while ($temp > 0) {

        // Taking the digit of the
        // number into digit var.
        $digit = $temp % 10;

        if (!(checkDivisibility($n, $digit)))
            return false;

        $temp /= 10;
    }

    return true;
}

// Driver function

    $n = 128;
    if (allDigitsDivide($n))
        echo "Yes";
    else
        echo "No";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check the number
    // is divisible by all digits are not.

    // Function to check the divisibility
    // of the number by its digit.
    function checkDivisibility(n, digit)
    {

        // If the digit divides the number
        // then return true else return false.
        return (digit != 0 && n % digit == 0);
    }

    // Function to check if all digits
    // of n divide it or not
    function allDigitsDivide(n)
    {
        let temp = n;
        while (temp > 0)
        {

            // Taking the digit of the
            // number into digit var.
            let digit = temp % 10;
            if (!(checkDivisibility(n, digit)))
                return false;

            temp = parseInt(temp / 10, 10);
        }
        return true;
    }

    let n = 128;
    if (allDigitsDivide(n))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by divyeshrabadiya07.
</script>
```

输出:

```
Yes
```

**Python 中的替代实现**

## 蟒蛇 3

```
# Python 3 program to
# check the number is
# divisible by all
# digits are not.

# Function to check
# the divisibility
# of the number by
# its digit.
def checkDivisibility(n, digit) :

    # If the digit divides the
    # number then return true
    # else return false.
    return (digit != 0 and n % digit == 0)

# Function to check if
# all digits of n divide
# it or not
def allDigitsDivide( n) :
    nlist = map(int, set(str(n)))
    for digit in nlist :
        if  not (checkDivisibility(n, digit)) :
            return False
    return True

# Driver function
n = 128

print("Yes" if (allDigitsDivide(n)) else "No")
```