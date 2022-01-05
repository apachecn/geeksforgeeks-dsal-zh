# 阶乘以 n 个零结束的数字

> 原文:[https://www . geesforgeks . org/numbers-what-阶乘-以 n-零结尾/](https://www.geeksforgeeks.org/numbers-whose-factorials-end-with-n-zeros/)

给定一个整数 n，我们需要找到阶乘以 n 个零结束的正整数的个数。
**例:**

```
Input : n = 1
Output : 5 6 7 8 9
Explanation: Here, 5! = 120, 6! = 720,
7! = 5040, 8! = 40320 and 9! = 362880.

Input : n = 2
Output : 10 11 12 13 14 

```

先决条件:[阶乘](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)中的尾随零。
**天真的做法:**我们只需要遍历整数的范围，找到所有数字的尾随零的个数，打印出带有 n 个尾随零的数字。
**高效方法:**在这种方法中，我们使用二分搜索法。对该范围内的所有数字使用二分搜索法，得到第一个带有 n 个尾随零的数字。找出数字后面有 m 个尾随零的所有数字。

## C++

```
// Binary search based CPP program to find
// numbers with n trailing zeros.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate trailing zeros
int trailingZeroes(int n)
{
    int cnt = 0;
    while (n > 0) {
        n /= 5;
        cnt += n;
    }
    return cnt;
}

void binarySearch(int n)
{
    int low = 0;
    int high = 1e6; // range of numbers

    // binary search for first number with
    // n trailing zeros
    while (low < high) {
        int mid = (low + high) / 2;
        int count = trailingZeroes(mid);
        if (count < n)
            low = mid + 1;
        else
            high = mid;
    }

    // Print all numbers after low with n
    // trailing zeros.
    vector<int> result;
    while (trailingZeroes(low) == n) {
        result.push_back(low);
        low++;
    }

    // Print result
    for (int i = 0; i < result.size(); i++)
        cout << result[i] << " ";
}

// Driver code
int main()
{
    int n = 2;
    binarySearch(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Binary search based Java
// program to find numbers
// with n trailing zeros.
import java.io.*;

class GFG {

    // Function to calculate
    // trailing zeros
    static int trailingZeroes(int n)
    {
        int cnt = 0;
        while (n > 0)
        {
            n /= 5;
            cnt += n;
        }
        return cnt;
    }

    static void binarySearch(int n)
    {
        int low = 0;

        // range of numbers
        int high = 1000000;

        // binary search for first number
        // with n trailing zeros
        while (low < high) {
            int mid = (low + high) / 2;
            int count = trailingZeroes(mid);
            if (count < n)
                low = mid + 1;
            else
                high = mid;
        }

        // Print all numbers after low
        // with n trailing zeros.
        int result[] = new int[1000];
        int k = 0;
        while (trailingZeroes(low) == n) {
            result[k] = low;
            k++;
            low++;
        }

        // Print result
        for (int i = 0; i < k; i++)
            System.out.print(result[i] + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 3;
        binarySearch(n);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Binary search based Python3 code to find
# numbers with n trailing zeros.

# Function to calculate trailing zeros
def trailingZeroes( n ):
    cnt = 0
    while n > 0:
        n =int(n/5)
        cnt += n
    return cnt

def binarySearch( n ):
    low = 0
    high = 1e6  # range of numbers

    # binary search for first number with
    # n trailing zeros
    while low < high:
        mid = int((low + high) / 2)
        count = trailingZeroes(mid)
        if count < n:
            low = mid + 1
        else:
            high = mid

    # Print all numbers after low with n
    # trailing zeros.
    result = list()
    while trailingZeroes(low) == n:
        result.append(low)
        low+=1

    # Print result
    for i in range(len(result)):
        print(result[i],end=" ")

# Driver code
n = 2
binarySearch(n)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// Binary search based C#
// program to find numbers
// with n trailing zeros.
using System;

class GFG {

    // Function to calculate
    // trailing zeros
    static int trailingZeroes(int n)
    {
        int cnt = 0;

        while (n > 0)
        {
            n /= 5;
            cnt += n;
        }

        return cnt;
    }

    static void binarySearch(int n)
    {
        int low = 0;

        // range of numbers
        int high = 1000000;

        // binary search for first number
        // with n trailing zeros
        while (low < high) {
            int mid = (low + high) / 2;
            int count = trailingZeroes(mid);

            if (count < n)
                low = mid + 1;
            else
                high = mid;
        }

        // Print all numbers after low
        // with n trailing zeros.
        int []result = new int[1000];
        int k = 0;
        while (trailingZeroes(low) == n) {
            result[k] = low;
            k++;
            low++;
        }

        // Print result
        for (int i = 0; i < k; i++)
            Console.Write(result[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int n = 2;

        binarySearch(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Binary search based PHP program to
// find numbers with n trailing zeros.

// Function to calculate trailing zeros
function trailingZeroes($n)
{
    $cnt = 0;
    while ($n > 0)
    {
        $n = intval($n / 5);
        $cnt += $n;
    }
    return $cnt;
}

function binarySearch($n)
{
    $low = 0;
    $high = 1e6; // range of numbers

    // binary search for first number
    // with n trailing zeros
    while ($low < $high)
    {
        $mid = intval(($low + $high) / 2);
        $count = trailingZeroes($mid);
        if ($count < $n)
            $low = $mid + 1;
        else
            $high = $mid;
    }

    // Print all numbers after low with n
    // trailing zeros.
    $result = array();
    while (trailingZeroes($low) == $n)
    {
        array_push($result, $low);
        $low++;
    }

    // Print result
    for ($i = 0;
         $i < sizeof($result); $i++)
        echo $result[$i] . " ";
}

// Driver code
$n = 2;
binarySearch($n);

// This code is contributed by Ita_c
?>
```

## java 描述语言

```
<script>

// Binary search based JavaScript program to find
// numbers with n trailing zeros.

// Function to calculate trailing zeros
function trailingZeroes(n)
{
    var cnt = 0;
    while (n > 0) {
        n = parseInt(n/5);
        cnt += n;
    }
    return cnt;
}

function binarySearch(n)
{
    var low = 0;
    var high = 1e6; // range of numbers

    // binary search for first number with
    // n trailing zeros
    while (low < high) {
        var mid = parseInt((low + high) / 2);
        var count = trailingZeroes(mid);
        if (count < n)
            low = mid + 1;
        else
            high = mid;
    }

    // Print all numbers after low with n
    // trailing zeros.
    var result = [];
    while (trailingZeroes(low) == n) {
        result.push(low);
        low++;
    }

    // Print result
    for (var i = 0; i < result.length; i++)
        document.write( result[i] + " ");
}

// Driver code
var n = 2;
binarySearch(n);

</script>
```

**输出:**

```
10 11 12 13 14 
```