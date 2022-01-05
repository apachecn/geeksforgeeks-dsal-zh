# 找出第 n 个包含数字 k 或可被 k 整除的数字

> 原文:[https://www . geesforgeks . org/find-n-number-contains-digital-k-除尽-k/](https://www.geeksforgeeks.org/find-nth-number-contains-digit-k-divisible-k/)

你已经给出了两个数字 n 和 k，你需要找到第 n 个包含数字 k 或者能被 k 整除的数字(2 <= k <=9 ).
**)举例:**

```
Input       : n = 15, k = 3
Output      : 33
Explanation  : ( 3, 6, 9, 12, 13, 15, 18, 21, 23, 24,
27, 30, 31, 33 ). These are those number who contain 
the digit k = 3 or divisible by k and in this nth number
is 33\. so output is 33.

Input       : n = 10, k = 2
Output      : 20
Explanation : ( 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 )
These are those number who contain the digit k = 2 or
divisible by k and in this nth number is 20\. so output 
is 20.
```

**方法:**
从 k 开始检查每个包含数字 k 或可被 k 整除的数字，直到我们没有得到第 n 个数字。

## C++

```
// C++ program to find nth number that contains
// the digit k or divisible by k.
#include <bits/stdc++.h>
using namespace std;

// Function for checking if digit k
// is in n or not
int checkdigit(int n, int k)
{
    while (n)
    {
        // finding remainder
        int rem = n % 10;

        // if digit found
        if (rem == k)
            return 1;

        n = n / 10;
    }

    return 0;
}

// Function for finding nth number
int findNthNumber(int n, int k)
{
    // since k is the first which satisfy the
    // criteria, so consider it in count making count = 1
    //  and starting from i = k + 1
    for (int i = k + 1, count = 1; count < n; i++)
    {
        // checking that the number contain
        // k digit or divisible by k
        if (checkdigit(i, k) || (i % k == 0))
            count++;

        if (count == n)
        return i;
    }

    return -1;
}

// Driver code
int main()
{
    int n = 10, k = 2;
    cout << findNthNumber(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth number that contains
// the digit k or divisible by k.
import java.io.*;

class GFG
{
    // Function for checking if digit k
    // is in n or not
    public static boolean checkdigit(int n, int k)
    {
        while (n != 0)
        {
            // finding remainder
            int rem = n % 10;

            // if digit found
            if (rem == k)
                return true;

            n = n / 10;
        }

        return false;
    }

    // Function for finding nth number
    public static int findNthNumber(int n, int k)
    {
        // since k is the first which satisfy th
    // criteria, so consider it in count making count = 1
    //  and starting from i = k + 1
        for (int i = k + 1, count = 1; count < n; i++)
        {
        // checking that the number contain
        // k digit or divisible by k
        if (checkdigit(i, k) || (i % k == 0))
            count++;

        if (count == n)
        return i;
        }

    return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10, k = 2;
        System.out.println(findNthNumber(n, k));

    }
}

// This code is contributed
// by  UPENDRA BARTWAL
```

## 蟒蛇 3

```
# Python 3 program to find nth number that
# contains the digit k or divisible by k.

# Function for checking if
# digit k is in n or not
def checkdigit(n, k):

    while (n):

        # finding remainder
        rem = n % 10

        # if digit found
        if (rem == k):
            return 1

        n = n / 10

    return 0

# Function for finding nth number
def findNthNumber(n, k):

    i = k + 1
    count = 1
    while(count < n):

        # checking that the number contain
        # k digit or divisible by k
        if (checkdigit(i, k) or (i % k == 0)):
            count += 1

        if (count == n):
            return i
        i += 1
    return -1

# Driver code
n = 10
k = 2
print(findNthNumber(n, k))

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// C# program to find nth number that contains
// the digit k or divisible by k.
using System;

class GFG
{

    // Function for checking if digit k
    // is in n or not
    public static bool checkdigit(int n, int k)
    {
        while (n != 0)
        {

            // finding remainder
            int rem = n % 10;

            // if digit found
            if (rem == k)
                return true;

            n = n / 10;
        }

        return false;
    }

    // Function for finding nth number
    public static int findNthNumber(int n, int k)
    {
        for (int i = k + 1, count = 1; count < n; i++)
        {

            // checking that the number contain
            // k digit or divisible by k
            if (checkdigit(i, k) || (i % k == 0))
                count++;

            if (count == n)
                return i;
        }

    return -1;
    }

    // Driver code
    public static void Main ()
    {
        int n = 10, k = 2;

        Console.WriteLine(findNthNumber(n, k));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth number 
// that contains the digit k or
// divisible by k.

// Function for checking if
// digit k is in n or not
function checkdigit($n, $k)
{
    while ($n)
    {
        // finding remainder
        $rem = $n % 10;

        // if digit found
        if ($rem == $k)
            return 1;

        $n = $n / 10;
    }
    return 0;
}

// Function for finding nth number
function findNthNumber($n, $k)
{
    // since k is the first which
    // satisfy the criteria, so
    // consider it in count making
    // count = 1 and starting from
    // i = k + 1
    for ($i = $k + 1, $count = 1;
                      $count < $n; $i++)
    {
        // checking that the number contain
        // k digit or divisible by k
        if (checkdigit($i, $k) ||
                      ($i % $k == 0))
            $count++;

        if ($count == $n)
        return $i;
    }

    return -1;
}

// Driver code
$n = 10; $k = 2;
echo findNthNumber($n, $k);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
// JavaScript program to find nth number that contains
// the digit k or divisible by k.

    // Function for checking if digit k
    // is in n or not
    function checkdigit(n, k)
    {
        while (n != 0)
        {
            // finding remainder
            let rem = n % 10;

            // if digit found
            if (rem == k)
                return true;

            n = n / 10;
        }

        return false;
    }

    // Function for finding nth number
    function findNthNumber(n, k)
    {
        // since k is the first which satisfy th
    // criteria, so consider it in count making count = 1
    //  and starting from i = k + 1
        for (let i = k + 1, count = 1; count < n; i++)
        {
        // checking that the number contain
        // k digit or divisible by k
        if (checkdigit(i, k) || (i % k == 0))
            count++;

        if (count == n)
        return i;
        }

    return -1;
    }

// Driver Code

        let n = 10, k = 2;
        document.write(findNthNumber(n, k));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
 20 
```