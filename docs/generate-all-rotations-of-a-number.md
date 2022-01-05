# 生成一个数的所有旋转

> 原文:[https://www . geesforgeks . org/generate-all-rotations-of-a-number/](https://www.geeksforgeeks.org/generate-all-rotations-of-a-number/)

给定一个整数 **n** ，任务是生成所有可能的左移位数。左移数字是当数字的所有数字向左移动一个位置，并且第一个位置的数字移动到最后一个位置时生成的数字。
**例:**

> **输入:** n = 123
> **输出:** 231 312
> **输入:** n = 1445
> **输出:** 4451 4514 5144

**进场:**

*   假设 **n = 123** 。
*   将 **n** 乘以 **10** ，即 **n = n * 10 = 1230** 。
*   将第一个数字加到结果数字上，即 **1230 + 1 = 1231** 。
*   从结果数中减去**(第一位数字)* 10 <sup>k</sup>** ，其中 **k** 是原始数中的位数(在本例中，k = 3)。
*   **1231–1000 = 231**为原号码的左移号码。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of digits of n
int numberOfDigits(int n)
{
    int cnt = 0;
    while (n > 0) {
        cnt++;
        n /= 10;
    }
    return cnt;
}

// Function to print the left shift numbers
void cal(int num)
{
    int digits = numberOfDigits(num);
    int powTen = pow(10, digits - 1);

    for (int i = 0; i < digits - 1; i++) {

        int firstDigit = num / powTen;

        // Formula to calculate left shift
        // from previous number
        int left
            = ((num * 10) + firstDigit)
              - (firstDigit * powTen * 10);
        cout << left << " ";

        // Update the original number
        num = left;
    }
}

// Driver Code
int main()
{
    int num = 1445;
    cal(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of digits of n
static int numberOfDigits(int n)
{
    int cnt = 0;
    while (n > 0)
    {
        cnt++;
        n /= 10;
    }
    return cnt;
}

// Function to print the left shift numbers
static void cal(int num)
{
    int digits = numberOfDigits(num);
    int powTen = (int) Math.pow(10, digits - 1);

    for (int i = 0; i < digits - 1; i++)
    {
        int firstDigit = num / powTen;

        // Formula to calculate left shift
        // from previous number
        int left = ((num * 10) + firstDigit) -
                    (firstDigit * powTen * 10);

        System.out.print(left + " ");

        // Update the original number
        num = left;
    }
}

// Driver Code
public static void main(String[] args)
{
    int num = 1445;
    cal(num);
}
}

// This code is contributed by
// PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# function to return the count of digit of n
def numberofDigits(n):
    cnt = 0
    while n > 0:
        cnt += 1
        n //= 10
    return cnt

# function to print the left shift numbers
def cal(num):
    digit = numberofDigits(num)
    powTen = pow(10, digit - 1)

    for i in range(digit - 1):

        firstDigit = num // powTen

        # formula to calculate left shift
        # from previous number
        left = (num * 10 + firstDigit -
               (firstDigit * powTen * 10))
        print(left, end = " ")

        # Update the original number
        num = left

# Driver code
num = 1445
cal(num)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

public class GFG{

// Function to return the count of digits of n
static int numberOfDigits(int n)
{
    int cnt = 0;
    while (n > 0) {
        cnt++;
        n /= 10;
    }
    return cnt;
}

// Function to print the left shift numbers
static void cal(int num)
{
    int digits = numberOfDigits(num);
    int powTen = (int)Math.Pow(10, digits - 1);

    for (int i = 0; i < digits - 1; i++) {

        int firstDigit = num / powTen;

        // Formula to calculate left shift
        // from previous number
        int left
            = ((num * 10) + firstDigit)
            - (firstDigit * powTen * 10);
        Console.Write(left +  " ");

        // Update the original number
        num = left;
    }
}

// Driver Code
    static public void Main (){
        int num = 1445;
        cal(num);
    }
}

// This code is contributed by akt_mit....  
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of digits of n
function numberOfDigits($n)
{
    $cnt = 0;
    while ($n > 0)
    {
        $cnt++;
        $n = floor($n / 10);
    }
    return $cnt;
}

// Function to print the left shift numbers
function cal($num)
{
    $digits = numberOfDigits($num);
    $powTen = pow(10, $digits - 1);

    for ($i = 0; $i < $digits - 1; $i++)
    {

        $firstDigit = floor($num / $powTen);

        // Formula to calculate left shift
        // from previous number
        $left
            = (($num * 10) + $firstDigit) -
               ($firstDigit * $powTen * 10);

        echo $left, " ";

        // Update the original number
        $num = $left;
    }
}

// Driver Code
$num = 1445;
cal($num);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the count of digits of n
    function numberOfDigits(n)
    {
        let cnt = 0;
        while (n > 0) {
            cnt++;
            n = parseInt(n / 10, 10);
        }
        return cnt;
    }

    // Function to print the left shift numbers
    function cal(num)
    {
        let digits = numberOfDigits(num);
        let powTen = Math.pow(10, digits - 1);

        for (let i = 0; i < digits - 1; i++) {

            let firstDigit = parseInt(num / powTen, 10);

            // Formula to calculate left shift
            // from previous number
            let left = ((num * 10) + firstDigit)
                - (firstDigit * powTen * 10);
            document.write(left +  " ");

            // Update the original number
            num = left;
        }
    }

    let num = 1445;
    cal(num);

</script>
```

**Output:** 

```
4451 4514 5144
```