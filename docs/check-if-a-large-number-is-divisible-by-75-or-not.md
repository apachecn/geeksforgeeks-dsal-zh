# 检查一个大数是否能被 75 整除

> 原文:[https://www . geeksforgeeks . org/check-如果一个大数字被 75 整除或不被整除/](https://www.geeksforgeeks.org/check-if-a-large-number-is-divisible-by-75-or-not/)

给定一个非常大的字符串形式的数字，任务是检查该数字是否能被 75 整除。
**例:**

```
Input: N = 175
Output: No 

Input: N = 100000000000000000754586672150
Output: Yes
```

**方法:**一个数只有被[3 整除](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)(如果数字之和被 3 整除)和[被 25 整除](https://www.geeksforgeeks.org/check-large-number-divisible-25-not/)(如果最后两位数字被 25 整除)两者都可以被 75 整除。
下面是检查给定数字是否能被 75 整除的实现。

## C++

```
// C++ implementation to check the number
// is divisible by 75 or not
#include <bits/stdc++.h>
using namespace std;

// check divisibleBy3
bool divisibleBy3(string number)
{
    // to store sum of Digit
    int sumOfDigit = 0;

    // traversing through each digit
    for (int i = 0; i < number.length(); i++)
        // summing up Digit
        sumOfDigit += number[i] - '0';

    // check if sumOfDigit is divisibleBy3
    if (sumOfDigit % 3 == 0)
        return true;

    return false;
}

// check divisibleBy25
bool divisibleBy25(string number)
{
    // if a single digit number
    if (number.length() < 2)
        return false;

    // length of the number
    int length = number.length();

    // taking the last two digit
    int lastTwo = (number[length - 2] - '0') * 10
                  + (number[length - 1] - '0');

    // checking if the lastTwo digit is divisibleBy25
    if (lastTwo % 25 == 0)
        return true;

    return false;
}

// Function to check divisibleBy75 or not
bool divisibleBy75(string number)
{

    // check if divisibleBy3 and divisibleBy25
    if (divisibleBy3(number) && divisibleBy25(number))
        return true;

    return false;
}

// Drivers code
int main()
{
    string number = "754586672150";

    // divisible
    bool divisible = divisibleBy75(number);

    // if divisibleBy75
    if (divisible)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check the number
// is divisible by 75 or not

import java.io.*;

class GFG {

// check divisibleBy3
static boolean divisibleBy3(String number)
{
    // to store sum of Digit
    int sumOfDigit = 0;

    // traversing through each digit
    for (int i = 0; i < number.length(); i++)
        // summing up Digit
        sumOfDigit += number.charAt(i) - '0';

    // check if sumOfDigit is divisibleBy3
    if (sumOfDigit % 3 == 0)
        return true;

    return false;
}

// check divisibleBy25
static  boolean divisibleBy25(String number)
{
    // if a single digit number
    if (number.length() < 2)
        return false;

    // length of the number
    int length = number.length();

    // taking the last two digit
    int lastTwo = (number.charAt(length - 2) - '0') * 10
                + (number.charAt(length - 1) - '0');

    // checking if the lastTwo digit is divisibleBy25
    if (lastTwo % 25 == 0)
        return true;

    return false;
}

// Function to check divisibleBy75 or not
static boolean divisibleBy75(String number)
{

    // check if divisibleBy3 and divisibleBy25
    if (divisibleBy3(number) && divisibleBy25(number))
        return true;

    return false;
}

// Drivers code

    public static void main (String[] args) {
    String number = "754586672150";

    // divisible
    boolean divisible = divisibleBy75(number);

    // if divisibleBy75
    if (divisible)
        System.out.println( "Yes");
    else
        System.out.println( "No");
    }
}
// This code is contributed
// by inder_verma..
```

## 蟒蛇 3

```
# Python 3 implementation to check the
# number is divisible by 75 or not

# check divisibleBy3
def divisibleBy3(number):

    # to store sum of Digit
    sumOfDigit = 0

    # traversing through each digit
    for i in range(0, len(number), 1):

        # summing up Digit
        sumOfDigit += ord(number[i]) - ord('0')

    # check if sumOfDigit is divisibleBy3
    if (sumOfDigit % 3 == 0):
        return True

    return False

# check divisibleBy25
def divisibleBy25(number):

    # if a single digit number
    if (len(number) < 2):
        return False

    # length of the number
    length = len(number)

    # taking the last two digit
    lastTwo = ((ord(number[length - 2]) -
                ord('0')) * 10 +
               (ord(number[length - 1]) - ord('0')))

    # checking if the lastTwo digit
    # is divisibleBy25
    if (lastTwo % 25 == 0):
        return True

    return False

# Function to check divisibleBy75 or not
def divisibleBy75(number):

    # check if divisibleBy3 and divisibleBy25
    if (divisibleBy3(number) and
        divisibleBy25(number)):
        return True

    return False

# Driver Code
if __name__ == '__main__':
    number = "754586672150"

    # divisible
    divisible = divisibleBy75(number)

    # if divisibleBy75
    if (divisible):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation to check the number
// is divisible by 75 or not
using System;

class GFG
{

// check divisibleBy3
static bool divisibleBy3(string number)
{
    // to store sum of Digit
    int sumOfDigit = 0;

    // traversing through each digit
    for (int i = 0; i < number.Length; i++)

        // summing up Digit
        sumOfDigit += number[i] - '0';

    // check if sumOfDigit is divisibleBy3
    if (sumOfDigit % 3 == 0)
        return true;

    return false;
}

// check divisibleBy25
static bool divisibleBy25(string number)
{
    // if a single digit number
    if (number.Length < 2)
        return false;

    // length of the number
    int length = number.Length;

    // taking the last two digit
    int lastTwo = (number[length - 2] - '0') * 10 +
                  (number[length - 1] - '0');

    // checking if the lastTwo digit
    // is divisibleBy25
    if (lastTwo % 25 == 0)
        return true;

    return false;
}

// Function to check divisibleBy75 or not
static bool divisibleBy75(string number)
{

    // check if divisibleBy3 and divisibleBy25
    if (divisibleBy3(number) && divisibleBy25(number))
        return true;

    return false;
}

// Driver Code
public static void Main ()
{
    string number = "754586672150";

    // divisible
    bool divisible = divisibleBy75(number);

    // if divisibleBy75
    if (divisible)
        Console.WriteLine( "Yes");
    else
        Console.WriteLine( "No");
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check the
// number is divisible by 75 or not

// check divisibleBy3
function divisibleBy3($number)
{
    // to store sum of Digit
    $sumOfDigit = 0;

    // traversing through each digit
    for ($i = 0;
         $i < strlen($number); $i++)
        // summing up Digit
        $sumOfDigit += $number[$i] - '0';

    // check if sumOfDigit is
    // divisibleBy3
    if ($sumOfDigit % 3 == 0)
        return true;

    return false;
}

// check divisibleBy25
function divisibleBy25($number)
{
    // if a single digit number
    if (strlen($number) < 2)
        return false;

    // length of the number
    $length = strlen($number);

    // taking the last two digit
    $lastTwo = ($number[$length - 2] - '0') * 10 +
               ($number[$length - 1] - '0');

    // checking if the lastTwo digit
    // is divisibleBy25
    if ($lastTwo % 25 == 0)
        return true;

    return false;
}

// Function to check divisibleBy75 or not
function divisibleBy75($number)
{

    // check if divisibleBy3 and
    // divisibleBy25
    if (divisibleBy3($number) &&
        divisibleBy25($number))
        return true;

    return false;
}

// Driver Code
$number = "754586672150";

// divisible
$divisible = divisibleBy75($number);

// if divisibleBy75
if ($divisible)
    echo "Yes";
else
    echo "No";

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to check the number
// is divisible by 75 or not

// check divisibleBy3
function divisibleBy3(number)
{
    // to store sum of Digit
    let sumOfDigit = 0;

    // traversing through each digit
    for (let i = 0; i < number.length; i++)
        // summing up Digit
        sumOfDigit += number[i] - '0';

    // check if sumOfDigit is divisibleBy3
    if (sumOfDigit % 3 == 0)
        return true;

    return false;
}

// check divisibleBy25
function divisibleBy25(number)
{
    // if a single digit number
    if (number.length < 2)
        return false;

    // length of the number
    let length = number.length;

    // taking the last two digit
    let lastTwo = (number[length - 2] - '0') * 10
                  + (number[length - 1] - '0');

    // checking if the lastTwo digit is divisibleBy25
    if (lastTwo % 25 == 0)
        return true;

    return false;
}

// Function to check divisibleBy75 or not
function divisibleBy75(number)
{

    // check if divisibleBy3 and divisibleBy25
    if (divisibleBy3(number) && divisibleBy25(number))
        return true;

    return false;
}

// Drivers code
    let number = "754586672150";

    // divisible
    let divisible = divisibleBy75(number);

    // if divisibleBy75
    if (divisible)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```