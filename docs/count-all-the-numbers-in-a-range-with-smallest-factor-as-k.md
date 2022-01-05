# 将系数最小的范围内的所有数字计算为 K

> 原文:[https://www . geeksforgeeks . org/count-所有范围内的数字，最小因子为 k/](https://www.geeksforgeeks.org/count-all-the-numbers-in-a-range-with-smallest-factor-as-k/)

给定从**‘a’**到**‘b’**的整数范围。我们的任务是计算区间**【a，b】**中不能被 2 和 k–1 之间的任何数整除但能被 **k** 整除的数的数量。
**注:**我们不必考虑除数等于 1。
**举例:**

```
Input : a = 12, b = 23, k = 3
Output : 2
Between [12, 23], 15 and 21 are the only number 
which are divisible k and not divisible by any 
number between 2 and k - 1.

Input : a = 1, b = 80, k = 7
Output : 3
```

**方法:**下面是解决这个问题的分步算法:

1.  一个数只能被 *k* 整除，不能被任何小于 *k* 的数整除，前提是 *k* 是一个质数。
2.  遍历从 *a* 到 *b* 的每个数字，检查该数字是否具有作为质数的最小因子 *k* 。
3.  在最小因子为素数 *k* 的范围内计算所有这样的数。

以下是上述方法的实现:

## C++

```
// C++ program to find the count of numbers in a range
// whose smallest factor is K

#include <bits/stdc++.h>
using namespace std;

// Function to check if k is a prime number or not
bool isPrime(int k)
{
    // Corner case
    if (k <= 1)
        return false;

    // Check from 2 to n-1
    for (int i = 2; i < k; i++)
        if (k % i == 0)
            return false;

    return true;
}

// Function to check if a number is not divisible
// by any number between 2 and K-1
int check(int num, int k)
{
    int flag = 1;

    // to check if the num is divisible by
    // any numbers between 2 and k - 1
    for (int i = 2; i < k; i++) {
        if (num % i == 0)
            flag = 0;
    }

    if (flag == 1) {
        // if not divisible by any number between
        // 2 and k - 1
        // but divisible by k
        if (num % k == 0)
            return 1;
        else
            return 0;
    }
    else
        return 0;
}

// Function to find count of numbers in range [a, b]
// with smallest factor as K
int findCount(int a, int b, int k)
{
    int count = 0;

    // a number can be divisible only by k and
    // not by any number less than k only
    // if k is a prime
    if (!isPrime(k))
        return 0;
    else {
        int ans;
        for (int i = a; i <= b; i++) {

            // to check if a number has
            // smallest factor as K
            ans = check(i, k);
            if (ans == 1)
                count++;
            else
                continue;
        }
    }

    return count;
}

// Driver code
int main()
{
    int a = 2020, b = 6300, k = 29;

    cout << findCount(a, b, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of numbers in a range
// whose smallest factor is K

public class GFG {

    // Function to check if k is a prime number or not
    static boolean isPrime(int k)
    {
        // Corner case
        if (k <= 1)
            return false;

        // Check from 2 to n-1
        for (int i = 2; i < k; i++)
            if (k % i == 0)
                return false;

        return true;
    }

    // Function to check if a number is not divisible
    // by any number between 2 and K-1
    static int check(int num, int k)
    {
        int flag = 1;

        // to check if the num is divisible by
        // any numbers between 2 and k - 1
        for (int i = 2; i < k; i++) {
            if (num % i == 0)
                flag = 0;
        }

        if (flag == 1) {
            // if not divisible by any number between
            // 2 and k - 1
            // but divisible by k
            if (num % k == 0)
                return 1;
            else
                return 0;
        }
        else
            return 0;
    }

    // Function to find count of numbers in range [a, b]
    // with smallest factor as K
    static int findCount(int a, int b, int k)
    {
        int count = 0;

        // a number can be divisible only by k and
        // not by any number less than k only
        // if k is a prime
        if (!isPrime(k))
            return 0;
        else {
            int ans;
            for (int i = a; i <= b; i++) {

                // to check if a number has
                // smallest factor as K
                ans = check(i, k);
                if (ans == 1)
                    count++;
                else
                    continue;
            }
        }

        return count;
    }

// Driver code
public static void main(String args[])
    {
         int a = 2020, b = 6300, k = 29;

            System.out.println(findCount(a, b, k));

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 program to find the count
# of numbers in a range whose smallest
# factor is K

# Function to check if k is
# a prime number or not
def isPrime( k):

    # Corner case
    if (k <= 1):
        return False

    # Check from 2 to n-1
    for i in range(2, k):
        if (k % i == 0):
            return false

    return True

# Function to check if a number
# is not divisible by any number
# between 2 and K-1
def check(num, k):
    flag = 1

    # to check if the num is divisible
    # by any numbers between 2 and k - 1
    for i in range(2, k) :
        if (num % i == 0):
            flag = 0

    if (flag == 1) :

        # if not divisible by any
        # number between 2 and k - 1
        # but divisible by k
        if (num % k == 0):
            return 1
        else:
            return 0
    else:
        return 0

# Function to find count of
# numbers in range [a, b]
# with smallest factor as K
def findCount(a, b, k):

    count = 0

    # a number can be divisible only
    # by k and not by any number
    # less than k only if k is a prime
    if (not isPrime(k)):
        return 0
    else :

        for i in range(a, b + 1) :

            # to check if a number has
            # smallest factor as K
            ans = check(i, k)
            if (ans == 1):
                count += 1
            else:
                continue

    return count

# Driver code
if __name__ == "__main__":
    a = 2020
    b = 6300
    k = 29

    print(findCount(a, b, k))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the count
// of numbers in a range whose
// smallest factor is K
using System;

class GFG
{

// Function to check if k is
// a prime number or not
static bool isPrime(int k)
{
    // Corner case
    if (k <= 1)
        return false;

    // Check from 2 to n-1
    for (int i = 2; i < k; i++)
        if (k % i == 0)
            return false;

    return true;
}

// Function to check if a number
// is not divisible by any number
// between 2 and K-1
static int check(int num, int k)
{
    int flag = 1;

    // to check if the num is divisible by
    // any numbers between 2 and k - 1
    for (int i = 2; i < k; i++)
    {
        if (num % i == 0)
            flag = 0;
    }

    if (flag == 1)
    {
        // if not divisible by any
        // number between 2 and k - 1
        // but divisible by k
        if (num % k == 0)
            return 1;
        else
            return 0;
    }
    else
        return 0;
}

// Function to find count of
// numbers in range [a, b]
// with smallest factor as K
static int findCount(int a, int b, int k)
{
    int count = 0;

    // a number can be divisible only
    // by k and not by any number less
    // than k only if k is a prime
    if (!isPrime(k))
        return 0;
    else
    {
        int ans;
        for (int i = a; i <= b; i++)
        {

            // to check if a number has
            // smallest factor as K
            ans = check(i, k);
            if (ans == 1)
                count++;
            else
                continue;
        }
    }

    return count;
}

// Driver code
public static void Main()
{
    int a = 2020, b = 6300, k = 29;

    Console.WriteLine(findCount(a, b, k));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the count
// of numbers in a range whose
// smallest factor is K

// Function to check if k is
// a prime number or not
function isPrime($k)
{
    // Corner case
    if ($k <= 1)
        return false;

    // Check from 2 to n-1
    for ($i = 2; $i < $k; $i++)
        if ($k % $i == 0)
            return false;

    return true;
}

// Function to check if a number
// is not divisible by any number
// between 2 and K-1
function check($num, $k)
{
    $flag = 1;

    // to check if the num is divisible
    // by any numbers between 2 and k - 1
    for ($i = 2; $i < $k; $i++)
    {
        if ($num % $i == 0)
            $flag = 0;
    }

    if ($flag == 1)
    {
        // if not divisible by any
        // number between 2 and k - 1
        // but divisible by k
        if ($num % $k == 0)
            return 1;
        else
            return 0;
    }
    else
        return 0;
}

// Function to find count of
// numbers in range [a, b]
// with smallest factor as K
function findCount($a, $b, $k)
{
    $count = 0;

    // a number can be divisible
    // only by k and not by any
    // number less than k only
    // if k is a prime
    if (!isPrime($k))
        return 0;
    else
    {
        for ($i = $a; $i <= $b; $i++)
        {

            // to check if a number has
            // smallest factor as K
            $ans = check($i, $k);
            if ($ans == 1)
                $count++;
            else
                continue;
        }
    }

    return $count;
}

// Driver code
$a = 2020;
$b = 6300;
$k = 29;

echo (findCount($a, $b, $k));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to find the count of numbers in a range
// whose smallest factor is K

    // Function to check if k is a prime number or not
    function isPrime(k)
    {
        // Corner case
        if (k <= 1)
            return false;

        // Check from 2 to n-1
        for (let i = 2; i < k; i++)
            if (k % i == 0)
                return false;

        return true;
    }

    // Function to check if a number is not divisible
    // by any number between 2 and K-1
    function check(num,k)
    {
        let flag = 1;

        // to check if the num is divisible by
        // any numbers between 2 and k - 1
        for (let i = 2; i < k; i++) {
            if (num % i == 0)
                flag = 0;
        }

        if (flag == 1) {
            // if not divisible by any number between
            // 2 and k - 1
            // but divisible by k
            if (num % k == 0)
                return 1;
            else
                return 0;
        }
        else
            return 0;
    }

    // Function to find count of numbers in range [a, b]
    // with smallest factor as K
    function findCount(a,b,k)
    {
        let count = 0;

        // a number can be divisible only by k and
        // not by any number less than k only
        // if k is a prime
        if (!isPrime(k))
            return 0;
        else {
            let ans;
            for (let i = a; i <= b; i++) {

                // to check if a number has
                // smallest factor as K
                ans = check(i, k);
                if (ans == 1)
                    count++;
                else
                    continue;
            }
        }

        return count;
    }

    // Driver code
    let a = 2020, b = 6300, k = 29;
    document.write(findCount(a, b, k));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
28
```