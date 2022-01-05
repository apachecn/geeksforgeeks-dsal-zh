# 找到 XXXX 的价值…..(N 次)% M 其中 N 大

> 原文:[https://www . geesforgeks . org/find-the-value-of-xxxx-n-times-m-where-n-is-large/](https://www.geeksforgeeks.org/find-the-value-of-xxxx-n-times-m-where-n-is-large/)

给定三个整数 **X** 、 **N** 和 **M** 。任务是从范围**【1，9】**中找到**XXX……(N 次)% M** ，其中 **X** 可以是任意数字。

**示例:**

> **输入:** X = 7，N = 7，M = 50
> T3】输出: 27
> 7777777 % 50 = 27
> 
> **输入:** X = 1，N = 10，M = 9
> **输出:** 1
> 1111111111 % 9 = 1

**方法:**使用[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)技术可以解决问题。像 X，XX，XXX 等较小数字的模。可以很容易地计算出来。但是问题出现在更大的数字上。因此，该数字可以拆分如下:

1.  如果 **N 为偶数** - > XXX…(N 次)= (XXX…(N/2 次)* 10 <sup>N/2</sup> ) + XXX..(N/2 倍)。
2.  如果 **N 为奇数** - > XXX…(N 次)= (XXX…(N/2 次)* 10<sup>(N/2)+1</sup>+(XXX…(N/2 次)* 10) + X。

通过使用上述公式，数字被分成更小的部分，这些部分的模块化操作很容易找到。利用属性 **(a + b) % m = (a % m + b % m) % m** ，利用较小数的结果进行递归分治求解，求出较大数的模。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Iterative function to calculate
// (x ^ y) % p in O(log y)
int power(int x, unsigned int y, int p)
{

    // Initialize result
    int res = 1;

    // Update x if it is >= p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function to return XXX.....(N times) % M
int findModuloByM(int X, int N, int M)
{

    // Return the mod by M of smaller numbers
    if (N < 6) {

        // Creating a string of N X's
        string temp(N, (char)(48 + X));

        // Converting the string to int
        // and calculating the modulo
        int res = stoi(temp) % M;

        return res;
    }

    // Checking the parity of N
    if (N % 2 == 0) {

        // Dividing the number into equal half
        int half = findModuloByM(X, N / 2, M) % M;

        // Utilizing the formula for even N
        int res = (half * power(10, N / 2, M)
                   + half)
                  % M;

        return res;
    }
    else {
        // Dividing the number into equal half
        int half = findModuloByM(X, N / 2, M) % M;

        // Utilizing the formula for odd N
        int res = (half * power(10, N / 2 + 1, M)
                   + half * 10 + X)
                  % M;

        return res;
    }
}

// Driver code
int main()
{
    int X = 6, N = 14, M = 9;

    // Print XXX...(N times) % M
    cout << findModuloByM(X, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Iterative function to calculate
    // (x ^ y) % p in O(log y)
    static int power(int x, int y, int p)
    {

        // Initialize result
        int res = 1;

        // Update x if it is >= p
        x = x % p;

        while (y > 0)
        {

            // If y is odd, multiply x with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            // y = y / 2
            y = y >> 1;
            x = (x * x) % p;
        }
        return res;
    }

    // Function to return XXX.....(N times) % M
    static int findModuloByM(int X, int N, int M)
    {

        // Return the mod by M of smaller numbers
        if (N < 6)
        {

            // Creating a string of N X's
            String temp="";
            for(int i = 0; i< N ; i++)
                temp = temp + (char)(X + 48);

            // Converting the string to int
            // and calculating the modulo
            int res = Integer.parseInt(temp) % M;

            return res;
        }

        // Checking the parity of N
        if (N % 2 == 0)
        {

            // Dividing the number into equal half
            int half = findModuloByM(X, N / 2, M) % M;

            // Utilizing the formula for even N
            int res = (half * power(10, N / 2, M)
                    + half)
                    % M;

            return res;
        }
        else
        {
            // Dividing the number into equal half
            int half = findModuloByM(X, N / 2, M) % M;

            // Utilizing the formula for odd N
            int res = (half * power(10, N / 2 + 1, M)
                    + half * 10 + X)
                    % M;

            return res;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int X = 6, N = 14, M = 9;

        // Print XXX...(N times) % M
        System.out.println(findModuloByM(X, N, M));
    }
}    

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Iterative function to calculate
# (x ^ y) % p in O(log y)
def power(x, y, p) :

    # Initialize result
    res = 1;

    # Update x if it is >= p
    x = x % p;

    while (y > 0) :

        # If y is odd, multiply x with result
        if (y and 1) :
            res = (res * x) % p;

        # y must be even now
        # y = y // 2
        y = y >> 1;
        x = (x * x) % p;

    return res;

# Function to return XXX.....(N times) % M
def findModuloByM(X, N, M) :

    # Return the mod by M of smaller numbers
    if (N < 6) :

        # Creating a string of N X's
        temp = chr(48 + X) * N

        # Converting the string to int
        # and calculating the modulo
        res = int(temp) % M;

        return res;

    # Checking the parity of N
    if (N % 2 == 0) :

        # Dividing the number into equal half
        half = findModuloByM(X, N // 2, M) % M;

        # Utilizing the formula for even N
        res = (half * power(10, N // 2,
                                M) + half) % M;

        return res;

    else :

        # Dividing the number into equal half
        half = findModuloByM(X, N // 2, M) % M;

        # Utilizing the formula for odd N
        res = (half * power(10, N // 2 + 1, M) +
               half * 10 + X) % M;

        return res;

# Driver code
if __name__ == "__main__" :

    X = 6; N = 14; M = 9;

    # Print XXX...(N times) % M
    print(findModuloByM(X, N, M));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Iterative function to calculate
    // (x ^ y) % p in O(log y)
    static int power(int x, int y, int p)
    {

        // Initialize result
        int res = 1;

        // Update x if it is >= p
        x = x % p;

        while (y > 0)
        {

            // If y is odd, multiply x with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            // y = y / 2
            y = y >> 1;
            x = (x * x) % p;
        }
        return res;
    }

    // Function to return XXX.....(N times) % M
    static int findModuloByM(int X, int N, int M)
    {

        // Return the mod by M of smaller numbers
        if (N < 6)
        {

            // Creating a string of N X's
            string temp="";
            for(int i = 0; i< N ; i++)
                temp = temp + (char)(X + 48);

            // Converting the string to int
            // and calculating the modulo
            int res = Convert.ToInt32(temp) % M;

            return res;
        }

        // Checking the parity of N
        if (N % 2 == 0)
        {

            // Dividing the number into equal half
            int half = findModuloByM(X, N / 2, M) % M;

            // Utilizing the formula for even N
            int res = (half * power(10, N / 2, M)
                    + half)
                    % M;

            return res;
        }
        else
        {
            // Dividing the number into equal half
            int half = findModuloByM(X, N / 2, M) % M;

            // Utilizing the formula for odd N
            int res = (half * power(10, N / 2 + 1, M)
                    + half * 10 + X)
                    % M;

            return res;
        }
    }

    // Driver code
    public static void Main ()
    {
        int X = 6, N = 14, M = 9;

        // Print XXX...(N times) % M
        Console.WriteLine(findModuloByM(X, N, M));
    }
}    

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Iterative function to calculate
// (x ^ y) % p in O(log y)
function power($x, $y, $p)
{

    // Initialize result
    $res = 1;

    // Update x if it is >= p
    $x = $x % $p;

    while ($y > 0)
    {

        // If y is odd, multiply x with result
        if ($y&1)
            $res = ($res * $x) % $p;

        // y must be even now
        // y = y // 2
        $y = $y >> 1;
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Function to return XXX.....(N times) % M
function findModuloByM($X, $N, $M)
{

    // Return the mod by M of smaller numbers
    if ($N < 6)
    {

        // Creating a string of N X's
        $temp = chr(48 + $X) * $N;

        // Converting the string to int
        // and calculating the modulo
        $res = intval($temp) % $M;

        return $res;
    }

    // Checking the parity of N
    if ($N % 2 == 0)
    {

        // Dividing the number into equal half
        $half = findModuloByM($X, (int)($N / 2), $M) % $M;

        // Utilizing the formula for even N
        $res = ($half * power(10,(int)($N / 2),
                             $M) + $half) % $M;

        return $res;
    }
    else
    {
        // Dividing the number into equal half
        $half = findModuloByM($X, (int)($N / 2), $M) % $M;

        // Utilizing the formula for odd N
        $res = ($half * power(10, (int)($N / 2) + 1, $M) +
                $half * 10 + $X) % $M;

        return $res;
    }
}

// Driver code
$X = 6;
$N = 14;
$M = 9;

// Print XXX...(N times) % M
print(findModuloByM($X, $N, $M));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Iterative function to calculate
// (x ^ y) % p in O(log y)
function power(x, y, p)
{

    // Initialize result
    var res = 1;

    // Update x if it is >= p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function to return XXX.....(N times) % M
function findModuloByM(X, N, M)
{

    // Return the mod by M of smaller numbers
    if (N < 6)
    {
        var temp = "";

        // Creating a string of N X's
        for(var i = 1; i < N; i++)
        {
            temp += String.fromCharCode(48 + X);
        }

        // Converting the string to int
        // and calculating the modulo
        var res = parseInt(temp) % M;

        return res;
    }

    // Checking the parity of N
    if (N % 2 == 0)
    {

        // Dividing the number into equal half
        var half = findModuloByM(X, N / 2, M) % M;

        // Utilizing the formula for even N
        var res = (half *
                   power(10, N / 2, M) + half) % M;

        return res;
    }
    else
    {

        // Dividing the number into equal half
        var half = findModuloByM(X, N / 2, M) % M;

        // Utilizing the formula for odd N
        var res = (half * power(10, N / 2 + 1, M) +
                   half * 10 + X) % M;

        return res;
    }
}

// Driver code
var X = 6, N = 14, M = 9;

// Print XXX...(N times) % M
document.write( findModuloByM(X, N, M));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
3
```