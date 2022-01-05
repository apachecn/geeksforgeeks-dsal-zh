# 范围[L，R]

内所有奇数长度回文数之和

> 原文:[https://www . geeksforgeeks . org/所有奇数长度回文数字之和-范围内-l-r/](https://www.geeksforgeeks.org/sum-of-all-odd-length-palindromic-numbers-within-the-range-l-r/)

给定两个整数![L    ](img/d00da2568e7af08151680b804f1da153.png "Rendered by QuickLaTeX.com")和![R    ](img/e853f08293b438ccc8e11e7543ebcf37.png "Rendered by QuickLaTeX.com")，任务是找出**【L，R】**范围内所有回文数的和，这些回文数的长度为**奇数**。
**举例:**

> **输入:** L = 10，R = 130
> **输出:**333
> 101+111+121 = 333
> **输入:** L = 110，R = 1130
> **输出:** 49399

**方法:** [从![L    ](img/d00da2568e7af08151680b804f1da153.png "Rendered by QuickLaTeX.com")到![R    ](img/e853f08293b438ccc8e11e7543ebcf37.png "Rendered by QuickLaTeX.com")迭代](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个数字[检查是否是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)且长度为奇数。如果是，那么把它加到总数中。最后打印总和的值。
以下是上述方法的实施:

## C++

```
// C++ program to find the sum of all odd length
// palindromic numbers within the given range
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// the given number is a palindrome
bool isPalindrome(int num)
{
    int reverse_num = 0, remainder, temp;

    /* Here we are generating a new number (reverse_num)
     * by reversing the digits of original input number
     */
    temp = num;
    while (temp != 0) {
        remainder = temp % 10;
        reverse_num = reverse_num * 10 + remainder;
        temp /= 10;
    }

    /* If the original input number (num) is equal to
     * to its reverse (reverse_num) then its palindrome
     * else it is not.
     */
    if (reverse_num == num) {
        return true;
    }

    return false;
}

// Function that returns true if the
// given number is of odd length
bool isOddLength(int num)
{
    int count = 0;
    while (num > 0) {
        num /= 10;
        count++;
    }
    if (count % 2 != 0) {
        return true;
    }
    return false;
}

// Function to return the sum of all odd length
// palindromic numbers within the given range
long sumOfAllPalindrome(int L, int R)
{
    long sum = 0;
    if (L <= R)
        for (int i = L; i <= R; i++) {

            // if number is palindrome and of odd length
            if (isPalindrome(i) && isOddLength(i)) {
                sum += i;
            }
        }
    return sum;
}

// Driver code
int main()
{
    int L = 110, R = 1130;
    cout << " " <<  sumOfAllPalindrome(L, R) << endl;
}

// This code is contributed by shivanisinghs2110.
```

## C

```
// C program to find the sum of all odd length
// palindromic numbers within the given range
#include <stdbool.h>
#include <stdio.h>

// Function that returns true if
// the given number is a palindrome
bool isPalindrome(int num)
{
    int reverse_num = 0, remainder, temp;

    /* Here we are generating a new number (reverse_num)
     * by reversing the digits of original input number
     */
    temp = num;
    while (temp != 0) {
        remainder = temp % 10;
        reverse_num = reverse_num * 10 + remainder;
        temp /= 10;
    }

    /* If the original input number (num) is equal to
     * to its reverse (reverse_num) then its palindrome
     * else it is not.
     */
    if (reverse_num == num) {
        return true;
    }

    return false;
}

// Function that returns true if the
// given number is of odd length
bool isOddLength(int num)
{
    int count = 0;
    while (num > 0) {
        num /= 10;
        count++;
    }
    if (count % 2 != 0) {
        return true;
    }
    return false;
}

// Function to return the sum of all odd length
// palindromic numbers within the given range
long sumOfAllPalindrome(int L, int R)
{
    long sum = 0;
    if (L <= R)
        for (int i = L; i <= R; i++) {

            // if number is palindrome and of odd length
            if (isPalindrome(i) && isOddLength(i)) {
                sum += i;
            }
        }
    return sum;
}

// Driver code
int main()
{
    int L = 110, R = 1130;
    printf("%ld", sumOfAllPalindrome(L, R));
}
//this code is contributed by shivanisinghss2110
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all odd length
// palindromic numbers within the given range

class GFG {

    // Function that returns true if
    // the given number is a palindrome
    static boolean isPalindrome(int num)
    {
        int reverse_num = 0, remainder, temp;

        /* Here we are generating a new number (reverse_num)
    * by reversing the digits of original input number
         */
        temp = num;
        while (temp != 0) {
            remainder = temp % 10;
            reverse_num = reverse_num * 10 + remainder;
            temp /= 10;
        }

        /* If the original input number (num) is equal to
    * to its reverse (reverse_num) then its palindrome
    * else it is not.
         */
        if (reverse_num == num) {
            return true;
        }

        return false;
    }

    // Function that returns true if the
    // given number is of odd length
    static boolean isOddLength(int num)
    {
        int count = 0;
        while (num > 0) {
            num /= 10;
            count++;
        }
        if (count % 2 != 0) {
            return true;
        }
        return false;
    }

    // Function to return the sum of all odd length
    // palindromic numbers within the given range
    static long sumOfAllPalindrome(int L, int R)
    {
        long sum = 0;
        if (L <= R)
            for (int i = L; i <= R; i++) {

                // if number is palindrome and of odd length
                if (isPalindrome(i) && isOddLength(i)) {
                    sum += i;
                }
            }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int L = 110, R = 1130;
        System.out.println(sumOfAllPalindrome(L, R));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find the sum of
# all odd length palindromic numbers
# within the given range

# Function that returns true if
# the given number is a palindrome
def isPalindrome(num):
    reverse_num = 0

    # Here we are generating a new number
    # (reverse_num) by reversing the digits
    # of original input number
    temp = num
    while (temp != 0):
        remainder = temp % 10
        reverse_num = reverse_num * 10 + remainder
        temp = int(temp/10)

    # If the original input number (num) is
    # equal to its reverse (reverse_num) then
    # its palindrome else it is not.
    if (reverse_num == num):
        return True

    return False

# Function that returns true if the given
# number is of odd length
def isOddLength(num):
    count = 0
    while (num > 0):
        num = int (num / 10)
        count += 1

    if (count % 2 != 0):
        return True

    return False

# Function to return the sum of all odd length
# palindromic numbers within the given range
def sumOfAllPalindrome(L, R):
    sum = 0
    if (L <= R):
        for i in range(L, R + 1, 1):

            # if number is palindrome and of
            # odd length
            if (isPalindrome(i) and isOddLength(i)):
                sum += i

    return sum

# Driver code
if __name__ == '__main__':
    L = 110
    R = 1130
    print(sumOfAllPalindrome(L, R))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find the sum of all odd length
// palindromic numbers within the given range
using System;

public class GFG {

    // Function that returns true if
    // the given number is a palindrome
    static bool isPalindrome(int num)
    {
        int reverse_num = 0, remainder, temp;

        /* Here we are generating a new number (reverse_num)
    * by reversing the digits of original input number
        */
        temp = num;
        while (temp != 0) {
            remainder = temp % 10;
            reverse_num = reverse_num * 10 + remainder;
            temp /= 10;
        }

        /* If the original input number (num) is equal to
    * to its reverse (reverse_num) then its palindrome
    * else it is not.
        */
        if (reverse_num == num) {
            return true;
        }

        return false;
    }

    // Function that returns true if the
    // given number is of odd length
    static bool isOddLength(int num)
    {
        int count = 0;
        while (num > 0) {
            num /= 10;
            count++;
        }
        if (count % 2 != 0) {
            return true;
        }
        return false;
    }

    // Function to return the sum of all odd length
    // palindromic numbers within the given range
    static long sumOfAllPalindrome(int L, int R)
    {
        long sum = 0;
        if (L <= R)
            for (int i = L; i <= R; i++) {

                // if number is palindrome and of odd length
                if (isPalindrome(i) && isOddLength(i)) {
                    sum += i;
                }
            }
        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int L = 110, R = 1130;
        Console.WriteLine(sumOfAllPalindrome(L, R));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of x
// all odd length palindromic numbers
// within the given range

// Function that returns true if
// the given number is a palindrome
function isPalindrome($num)
{
    $reverse_num = 0;
    $remainder;
    $temp;

    // Here we are generating a new number
    // (reverse_num) by reversing the
    // digits of original input number
    $temp = $num;
    while ($temp != 0)
    {
        $remainder = $temp % 10;
        $reverse_num = $reverse_num * 10 +
                       $remainder;
        $temp = (int)($temp / 10);
    }

    // If the original input number (num) is
    // equal to its reverse (reverse_num)
    // then its palindrome else it is not.
    if ($reverse_num == $num)
    {
        return true;
    }

    return false;
}

// Function that returns true if the
// given number is of odd length
function isOddLength($num)
{
    $count = 0;
    while ($num > 0)
    {
        $num = (int)($num / 10);
        $count++;
    }
    if ($count % 2 != 0)
    {
        return true;
    }
    return false;
}

// Function to return the sum of
// all odd length palindromic numbers
// within the given range
function sumOfAllPalindrome($L, $R)
{
    $sum = 0;
    if ($L <= $R)
        for ($i = $L; $i <= $R; $i++)
        {

            // if number is palindrome and
            // of odd length
            if (isPalindrome($i) && isOddLength($i))
            {
                $sum += $i;
            }
        }
    return $sum;
}

// Driver code
$L = 110;
$R = 1130;
echo sumOfAllPalindrome($L, $R);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the sum of all odd length
// palindromic numbers within the given range

    // Function that returns true if
    // the given number is a palindrome
    function isPalindrome(num)
    {
        let reverse_num = 0, remainder, temp;

        /* Here we are generating a new number (reverse_num)
    * by reversing the digits of original input number
         */
        temp = num;
        while (temp != 0) {
            remainder = temp % 10;
            reverse_num = reverse_num * 10 + remainder;
            temp = Math.floor(temp/10);
        }

        /* If the original input number (num) is equal to
    * to its reverse (reverse_num) then its palindrome
    * else it is not.
         */
        if (reverse_num == num) {
            return true;
        }

        return false;
    }

    // Function that returns true if the
    // given number is of odd length
    function isOddLength(num)
    {
        let count = 0;
        while (num > 0) {
            num = Math.floor(num/10);
            count++;
        }
        if (count % 2 != 0) {
            return true;
        }
        return false;
    }

    // Function to return the sum of all odd length
    // palindromic numbers within the given range
    function sumOfAllPalindrome(L,R)
    {
        let sum = 0;
        if (L <= R)
            for (let i = L; i <= R; i++) {

                // if number is palindrome and of odd length
                if (isPalindrome(i) && isOddLength(i)) {
                    sum += i;
                }
            }
        return sum;
    }

    // Driver code
    let L = 110, R = 1130;
    document.write(sumOfAllPalindrome(L, R));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
49399
```