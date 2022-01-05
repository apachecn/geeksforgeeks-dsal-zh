# 位数总和为 10 倍数的前 N 项

> 原文:[https://www . geesforgeks . org/first-n-terms-其数字总和是 10 的倍数/](https://www.geeksforgeeks.org/first-n-terms-whose-sum-of-digits-is-a-multiple-of-10/)

给定一个整数 **N** ，任务是打印第一个 **N** 项，其位数总和是 **10** 的倍数。该系列的前几个术语是 **19、28、37、46、55、……**
**示例:**

> **输入:** N = 5
> **输出:** 19 28 37 46 55
> **输入:** N = 10
> **输出:** 19 28 37 46 55 64 73 82 91 109

**方法:**可以观察到，要得到所需系列的 **N <sup>第</sup>T5】项，求 **N** 位数之和。如果总和已经是 **10** 的倍数，则在 **N** 的末尾追加数字 **0** ，否则在末尾追加最小可能数字，使得新的数字总和是 **10** 的倍数。** 

> 例如，要获得第**19**项，由于位数之和已经是第 **10** 的倍数，那么追加第 **0** 和第 **190** 就是该系列的第**19**项。
> 对于 **N = 5** ，可追加使位数之和为 **10** 倍数的最小位数为 **5** ， **55** 为该系列的 **5 <sup>第</sup>** 项。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

const int TEN = 10;

// Function to return the
// sum of digits of n
int digitSum(int n)
{
    int sum = 0;
    while (n > 0) {

        // Add last digit to the sum
        sum += n % TEN;

        // Remove last digit
        n /= TEN;
    }

    return sum;
}

// Function to return the nth term
// of the required series
int getNthTerm(int n)
{
    int sum = digitSum(n);

    // If sum of digit is already
    // a multiple of 10 then append 0
    if (sum % TEN == 0)
        return (n * TEN);

    // To store the minimum digit
    // that must be appended
    int extra = TEN - (sum % TEN);

    // Return n after appending
    // the required digit
    return ((n * TEN) + extra);
}

// Function to print the first n terms
// of the required series
void firstNTerms(int n)
{
    for (int i = 1; i <= n; i++)
        cout << getNthTerm(i) << " ";
}

// Driver code
int main()
{
    int n = 10;

    firstNTerms(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    final static int TEN = 10;

    // Function to return the
    // sum of digits of n
    static int digitSum(int n)
    {
        int sum = 0;
        while (n > 0)
        {

            // Add last digit to the sum
            sum += n % TEN;

            // Remove last digit
            n /= TEN;
        }
        return sum;
    }

    // Function to return the nth term
    // of the required series
    static int getNthTerm(int n)
    {
        int sum = digitSum(n);

        // If sum of digit is already
        // a multiple of 10 then append 0
        if (sum % TEN == 0)
            return (n * TEN);

        // To store the minimum digit
        // that must be appended
        int extra = TEN - (sum % TEN);

        // Return n after appending
        // the required digit
        return ((n * TEN) + extra);
    }

    // Function to print the first n terms
    // of the required series
    static void firstNTerms(int n)
    {
        for (int i = 1; i <= n; i++)
            System.out.print(getNthTerm(i) + " ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;

        firstNTerms(n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 code for above implementation
TEN = 10

# Function to return the
# sum of digits of n
def digitSum(n):
    sum = 0
    while (n > 0):

        # Add last digit to the sum
        sum += n % TEN

        # Remove last digit
        n //= TEN

    return sum

# Function to return the nth term
# of the required series
def getNthTerm(n):
    sum = digitSum(n)

    # If sum of digit is already
    # a multiple of 10 then append 0
    if (sum % TEN == 0):
        return (n * TEN)

    # To store the minimum digit
    # that must be appended
    extra = TEN - (sum % TEN)

    # Return n after appending
    # the required digit
    return ((n * TEN) + extra)

# Function to print the first n terms
# of the required series
def firstNTerms(n):
    for i in range(1, n + 1):
        print(getNthTerm(i), end = " ")

# Driver code
n = 10

firstNTerms(n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# Program to Find the Unique elements
// in linked lists
using System;

class GFG
{
    readonly static int TEN = 10;

    // Function to return the
    // sum of digits of n
    static int digitSum(int n)
    {
        int sum = 0;
        while (n > 0)
        {

            // Add last digit to the sum
            sum += n % TEN;

            // Remove last digit
            n /= TEN;
        }
        return sum;
    }

    // Function to return the nth term
    // of the required series
    static int getNthTerm(int n)
    {
        int sum = digitSum(n);

        // If sum of digit is already
        // a multiple of 10 then append 0
        if (sum % TEN == 0)
            return (n * TEN);

        // To store the minimum digit
        // that must be appended
        int extra = TEN - (sum % TEN);

        // Return n after appending
        // the required digit
        return ((n * TEN) + extra);
    }

    // Function to print the first n terms
    // of the required series
    static void firstNTerms(int n)
    {
        for (int i = 1; i <= n; i++)
            Console.Write(getNthTerm(i) + " ");
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 10;

        firstNTerms(n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

const TEN = 10;

// Function to return the
// sum of digits of n
function digitSum(n)
{
    let sum = 0;
    while (n > 0) {

        // Add last digit to the sum
        sum += n % TEN;

        // Remove last digit
        n = Math.floor(n / TEN);
    }

    return sum;
}

// Function to return the nth term
// of the required series
function getNthTerm(n)
{
    let sum = digitSum(n);

    // If sum of digit is already
    // a multiple of 10 then append 0
    if (sum % TEN == 0)
        return (n * TEN);

    // To store the minimum digit
    // that must be appended
    let extra = TEN - (sum % TEN);

    // Return n after appending
    // the required digit
    return ((n * TEN) + extra);
}

// Function to print the first n terms
// of the required series
function firstNTerms(n)
{
    for (let i = 1; i <= n; i++)
        document.write(getNthTerm(i) + " ");
}

// Driver code

    let n = 10;

    firstNTerms(n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
19 28 37 46 55 64 73 82 91 109
```