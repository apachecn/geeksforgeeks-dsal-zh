# 不大于 N 的最大数字，所有数字都是奇数

> 原文:[https://www . geesforgeks . org/最大数字不大于 n 所有数字都是奇数/](https://www.geeksforgeeks.org/largest-number-not-greater-than-n-all-the-digits-of-which-are-odd/)

给定一个数字 *N* ，任务是找到不大于 *N* 的最大数字，它的所有数字都是*奇数*。
**示例:**

> **输入:** N = 23
> **输出:** 19
> 19 是小于 23 的最大数字，它有所有奇数位。
> **输入:** N = 7236
> **输出:** 7199

**天真逼近**:从 *N* 迭代到 *0* ，找到第一个所有数字都是奇数的数字。如果跳过偶数，这种方法仍然可以优化，因为每个偶数的右边都有一个偶数。
以下是上述方法的实现:

## C++

```
// CPP program to print the largest integer
// not greater than N with all odd digits
#include <bits/stdc++.h>
using namespace std;

// Function to check if all digits
// of a number are odd
bool allOddDigits(int n)
{
    // iterate for all digits
    while (n) {

        // if digit is even
        if ((n % 10) % 2 == 0)
            return false;
        n /= 10;
    }

    // all digits are odd
    return true;
}

// function to return the largest number
// with all digits odd
int largestNumber(int n)
{
    if (n % 2 == 0)
        n--;

    // iterate till we find a
    // number with all digits odd
    for (int i = n;; i -= 2)
        if (allOddDigits(i))
            return i;
}

// Driver Code
int main()
{
    int N = 23;
    cout << largestNumber(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the largest integer
// not greater than N with all odd digits

public class GFG{

        // Function to check if all digits
        // of a number are odd
        static boolean allOddDigits(int n)
        {
            // iterate for all digits
            while (n != 0) {

                // if digit is even
                if ((n % 10) % 2 == 0)
                    return false;
                n /= 10;
            }

            // all digits are odd
            return true;
        }

        // function to return the largest number
        // with all digits odd
        static int largestNumber(int n)
        {
            if (n % 2 == 0)
                n--;

            // iterate till we find a
            // number with all digits odd
            for (int i = n;; i -= 2)
                if (allOddDigits(i))
                    return i;
        }

     public static void main(String []args){

        int N = 23;
        System.out.println(largestNumber(N));

    }
    // This code is contributed by ANKITRAI1

}
```

## 蟒蛇 3

```
# Python 3 program to print the largest
# integer not greater than N with all
# odd digits

# Function to check if all digits
# of a number are odd
def allOddDigits(n):

    # iterate for all digits
    while (n):

        # if digit is even
        if ((n % 10) % 2 == 0):
            return False
        n = int(n / 10)

    # all digits are odd
    return True

# function to return the largest
# number with all digits odd
def largestNumber(n):
    if (n % 2 == 0):
        n -= 1

    # iterate till we find a
    # number with all digits odd
    i = n
    while(1):
        if (allOddDigits(i)):
            return i
        i -= 2

# Driver Code
if __name__ =='__main__':
    N = 23
    print(largestNumber(N))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to print the largest
// integer not greater than N with
// all odd digits
using System;

class GFG
{

// Function to check if all
// digits of a number are odd
static bool allOddDigits(int n)
{
    // iterate for all digits
    while (n != 0)
    {

        // if digit is even
        if ((n % 10) % 2 == 0)
            return false;
        n /= 10;
    }

    // all digits are odd
    return true;
}

// function to return the largest
// number with all digits odd
static int largestNumber(int n)
{
    if (n % 2 == 0)
        n--;

    // iterate till we find a
    // number with all digits odd
    for (int i = n;; i -= 2)
        if (allOddDigits(i))
            return i;
}

// Driver Code
public static void Main()
{
    int N = 23;

    Console.WriteLine(largestNumber(N));
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the largest integer
// not greater than N with all odd digits

// Function to check if all digits
// of a number are odd
function allOddDigits($n)
{
    // iterate for all digits
    while ($n > 1)
    {

        // if digit is even
        if (($n % 10) % 2 == 0)
            return false;
        $n = (int)$n / 10;
    }

    // all digits are odd
    return true;
}

// function to return the largest
// number with all digits odd
function largestNumber($n)
{
    if ($n % 2 == 0)
        $n--;

    // iterate till we find a
    // number with all digits odd
    for ($i = $n;; $i= ($i - 2))
        if (allOddDigits($i))
            return $i;
}

// Driver Code
$N = 23;
echo largestNumber($N);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to print the largest integer
// not greater than N with all odd digits

// Function to check if all digits
// of a number are odd
function allOddDigits(n)
{

    // iterate for all digits
    while (n != 0)
    {

        // if digit is even
        if ((n % 10) % 2 == 0)
            return false;
        n = parseInt(n / 10);
    }

    // all digits are odd
    return true;
}

// function to return the largest number
// with all digits odd
function largestNumber(n)
{
    if (parseInt(n % 2) == 0)
        n--;

    // iterate till we find a
    // number with all digits odd

    for (i = n; i > 0; i -= 2)
        if (allOddDigits(i))
            return i;
}

// Driver code
var N = 23;
document.write(largestNumber(N));

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
19
```