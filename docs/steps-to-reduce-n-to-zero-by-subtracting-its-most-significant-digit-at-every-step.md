# 通过在每一步减去其最高有效数字将 N 减少到零的步骤

> 原文:[https://www . geeksforgeeks . org/steps-to-reduce-n-to-zero-n-by-n-reduce-n-to-zero-n-reduce-n-to-zero-n-reduce-n-reduce-n-reduce-n-reduce-n-reduce-n-to-zero-n-reduce-n](https://www.geeksforgeeks.org/steps-to-reduce-n-to-zero-by-subtracting-its-most-significant-digit-at-every-step/)

给定一个数字![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")。通过在每一步中减去该数字的最高有效位(最左边的位)，将该数字减为零。任务是计算减少到零所需的步骤数。
**示例** :

```
Input: 14
Output: 6
Steps:
14 - 1 = 13
13 - 1 = 12
12 - 1 = 11
11 - 1 = 10
10 - 1 = 9
9 - 9 = 0

Input: 20  
Output: 12
Numbers after series of steps:
20, 18, 17, 16, 15, 14, 13, 12, 11, 10, 9, 0
```

**天真法**:天真法是将数字逐级减少第一位数字，求出步数，但如果提供一个大的数字，时间复杂度会很大。
**高效方法:**高效方法的主要思想是减少天真方法中的步骤数。我们可以跳过连续数字中前导数字相同的步骤，并对它们进行计数。跳过那些前导数字相同的数字的算法如下:

*   让数字是最后一个，倒数第二个数，然后减 1，因为具有相同前导数字和相同位数的最小数字会有相同数量的零。
*   根据最后/计数找到最后一个数字的第一个数字。
*   因此，具有相同前导号码的相同位数的最小数量将是**【第一个数字*(计数-1)】**
*   跳过的步数可以通过**【(倒数第二个数字)/第一个数字】**来实现。
*   因此最后一个数字将是**最后–(第一个*跳过)**

以下是上述方法的实现:

## C++

```
// C++ program to find the count of Steps to
// reduce N to zero by subtracting its most
// significant digit at every step

#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of digits in a number m
int countdig(int m)
{
    if (m == 0)
        return 0;
    else
        return 1 + countdig(m / 10);
}

// Function to count the number of
// steps to reach 0
int countSteps(int x)
{
    // count the total number of stesp
    int c = 0;
    int last = x;

    // iterate till we reach 0
    while (last) {

        // count the digits in last
        int digits = countdig(last);

        // decrease it by 1
        digits -= 1;

        // find the number on whose division,
        // we get the first digit
        int divisor = pow(10, digits);

        // first digit in last
        int first = last / divisor;

        // find the first number less than
        // last where the first digit changes
        int lastnumber = first * divisor;

        // find the number of numbers
        // with same first digit that are jumped
        int skipped = (last - lastnumber) / first;

        skipped += 1;

        // count the steps
        c += skipped;

        // the next number with a different
        // first digit
        last = last - (first * skipped);
    }

    return c;
}

// Driver code
int main()
{
    int n = 14;

    cout << countSteps(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of Steps to
// reduce N to zero by subtracting its most
// significant digit at every step

class GFG{
// Function to count the number
// of digits in a number m
static int countdig(int m)
{
    if (m == 0)
        return 0;
    else
        return 1 + countdig(m / 10);
}

// Function to count the number of
// steps to reach 0
static int countSteps(int x)
{
    // count the total number of stesp
    int c = 0;
    int last = x;

    // iterate till we reach 0
    while (last>0) {

        // count the digits in last
        int digits = countdig(last);

        // decrease it by 1
        digits -= 1;

        // find the number on whose division,
        // we get the first digit
        int divisor = (int)Math.pow(10, digits);

        // first digit in last
        int first = last / divisor;

        // find the first number less than
        // last where the first digit changes
        int lastnumber = first * divisor;

        // find the number of numbers
        // with same first digit that are jumped
        int skipped = (last - lastnumber) / first;

        skipped += 1;

        // count the steps
        c += skipped;

        // the next number with a different
        // first digit
        last = last - (first * skipped);
    }

    return c;
}

// Driver code
public static void main(String[] args)
{
    int n = 14;

    System.out.println(countSteps(n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find the
# count of Steps to reduce N to
# zero by subtracting its most
# significant digit at every step

# Function to count the number
# of digits in a number m
def countdig(m) :

    if (m == 0) :
        return 0
    else :
        return 1 + countdig(m // 10)

# Function to count the number
# of steps to reach 0
def countSteps(x) :

    # count the total number
    # of stesp
    c = 0
    last = x

    # iterate till we reach 0
    while (last) :

        # count the digits in last
        digits = countdig(last)

        # decrease it by 1
        digits -= 1

        # find the number on whose
        # division, we get the first digit
        divisor = pow(10, digits)

        # first digit in last
        first = last // divisor

        # find the first number less
        # than last where the first
        # digit changes
        lastnumber = first * divisor

        # find the number of numbers
        # with same first digit that
        # are jumped
        skipped = (last - lastnumber) // first

        skipped += 1

        # count the steps
        c += skipped

        # the next number with a different
        # first digit
        last = last - (first * skipped)

    return c

# Driver code
n = 14
print(countSteps(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find the count of Steps to
// reduce N to zero by subtracting its most
// significant digit at every step
using System;

class GFG{
// Function to count the number
// of digits in a number m
static int countdig(int m)
{
    if (m == 0)
        return 0;
    else
        return 1 + countdig(m / 10);
}

// Function to count the number of
// steps to reach 0
static int countSteps(int x)
{
    // count the total number of stesp
    int c = 0;
    int last = x;

    // iterate till we reach 0
    while (last>0) {

        // count the digits in last
        int digits = countdig(last);

        // decrease it by 1
        digits -= 1;

        // find the number on whose division,
        // we get the first digit
        int divisor = (int)Math.Pow(10, digits);

        // first digit in last
        int first = last / divisor;

        // find the first number less than
        // last where the first digit changes
        int lastnumber = first * divisor;

        // find the number of numbers
        // with same first digit that are jumped
        int skipped = (last - lastnumber) / first;

        skipped += 1;

        // count the steps
        c += skipped;

        // the next number with a different
        // first digit
        last = last - (first * skipped);
    }

    return c;
}

// Driver code
static void Main()
{
    int n = 14;

    Console.WriteLine(countSteps(n));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the count of Steps to
// reduce N to zero by subtracting its most
// significant digit at every step

// Function to count the number
// of digits in a number m
function countdig($m)
{
    if ($m == 0)
        return 0;
    else
        return 1 + countdig( (int)($m / 10));
}

// Function to count the number of
// steps to reach 0
function countSteps($x)
{
    // count the total number of stesp
    $c = 0;
    $last = $x;

    // iterate till we reach 0
    while ($last)
    {

        // count the digits in last
        $digits = countdig($last);

        // decrease it by 1
        $digits -= 1;

        // find the number on whose division,
        // we get the first digit
        $divisor = pow(10, $digits);

        // first digit in last
        $first =  (int)($last / $divisor);

        // find the first number less than
        // last where the first digit changes
        $lastnumber = $first * $divisor;

        // find the number of numbers
        // with same first digit that are jumped
        $skipped = ($last - $lastnumber) / $first;

        $skipped += 1;

        // count the steps
        $c += $skipped;

        // the next number with a different
        // first digit
        $last = $last - ($first * $skipped);
    }

    return $c;
}

// Driver code
$n = 14;

echo countSteps($n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// javascript program to find the count of Steps to
// reduce N to zero by subtracting its most
// significant digit at every step   
// Function to count the number
    // of digits in a number m
    function countdig(m) {
        if (m == 0)
            return 0;
        else
            return 1 + countdig(parseInt(m / 10));
    }

    // Function to count the number of
    // steps to reach 0
    function countSteps(x) {
        // count the total number of stesp
        var c =0;
        var last = x;

        // iterate till we reach 0
        while (last > 0) {

            // count the digits in last
            var digits = countdig(last);

            // decrease it by 1
            digits -= 1;

            // find the number on whose division,
            // we get the first digit
            var divisor = parseInt( Math.pow(10, digits));

            // first digit in last
            var first = parseInt(last / divisor);

            // find the first number less than
            // last where the first digit changes
            var lastnumber = first * divisor;

            // find the number of numbers
            // with same first digit that are jumped
            var skipped = parseInt((last - lastnumber) / first);

            skipped += 1;

            // count the steps
            c += skipped;

            // the next number with a different
            // first digit
            last = last - (first * skipped);
        }

        return c;
    }

    // Driver code

        var n = 14;

        document.write(countSteps(n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
6
```