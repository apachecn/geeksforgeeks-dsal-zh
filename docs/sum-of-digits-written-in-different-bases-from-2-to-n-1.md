# 从 2 到 n-1 不同基数写的数字总和

> 原文:[https://www . geesforgeks . org/不同碱基的数字总和-从-2 到-n-1/](https://www.geeksforgeeks.org/sum-of-digits-written-in-different-bases-from-2-to-n-1/)

给定一个数 n，求从 2 到 n-1 的不同基数表示的 n 位数之和。
**例:**

```
Input : 5
Output : 2 3 2
Representation of 5 is 101, 12, 11 in bases 2 , 3 , 4 .

Input : 7
Output : 3 3 4 3 2
```

> 1.  Because a given problem wants the sum of digits of different cardinality, first we need to calculate the given number of different cardinality, and then add each number to the number of different cardinality.
> 2.  Therefore, in order to calculate the representation of each number, we multiply the modulus of a given number by the cardinality we want to represent the number.
> 3.  Then, we must add all these mod values, because the obtained mod values will represent the numbers in the cardinality.
> 4.  Finally, the sum of these mod values gives the sum of the digits of the number.

以下是这种方法的实现方式

## C++

```
// CPP program to find sum of digits of
// n in different bases from 2 to n-1.
#include <bits/stdc++.h>
using namespace std;

// function to calculate sum of
// digit for a given base
int solve(int n, int base)
{
    // Sum of digits
    int result = 0 ;

    // Calculating the number (n) by
    // taking mod with the base and adding
    // remainder to the result and
    // parallelly reducing the num value .
    while (n > 0)
    {
        int remainder = n % base ;
        result = result + remainder ;
        n = n / base;
    }

    // returning the result
    return result ;
}

void printSumsOfDigits(int n)
{
    // function calling for multiple bases
    for (int base = 2 ; base < n ; ++base)   
        cout << solve(n, base) <<" ";
}

// Driver program
int main()
{
    int n = 8;
    printSumsOfDigits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of digits of
// n in different bases from 2 to n-1.
class GFG
{
// function to calculate sum of
// digit for a given base
static int solve(int n, int base)
{
    // Sum of digits
    int result = 0 ;

    // Calculating the number (n) by
    // taking mod with the base and adding
    // remainder to the result and
    // parallelly reducing the num value .
    while (n > 0)
    {
        int remainder = n % base ;
        result = result + remainder ;
        n = n / base;
    }

    // returning the result
    return result ;
}

static void printSumsOfDigits(int n)
{
    // function calling for multiple bases
    for (int base = 2 ; base < n ; ++base)
        System.out.print(solve(n, base)+" ");
}

// Driver Code
public static void main(String[] args)
{
    int n = 8;
    printSumsOfDigits(n);
}
}
// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python program to find sum of digits of
# n in different bases from 2 to n-1.

# def to calculate sum of
# digit for a given base
def solve(n, base) :

    # Sum of digits
    result = 0

    # Calculating the number (n) by
    # taking mod with the base and adding
    # remainder to the result and
    # parallelly reducing the num value .
    while (n > 0) :

        remainder = n % base
        result = result + remainder 
        n = int(n / base)

    # returning the result
    return result

def printSumsOfDigits(n) :

    # def calling for
    # multiple bases
    for base in range(2, n) :
        print (solve(n, base), end=" ")

# Driver code
n = 8
printSumsOfDigits(n)

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// Java program to find the sum of digits of
// n in different base1s from 2 to n-1.
using System;

class GFG
{
// function to calculate sum of
// digit for a given base1
static int solve(int n, int base1)
{
    // Sum of digits
    int result = 0 ;

    // Calculating the number (n) by
    // taking mod with the base1 and adding
    // remainder to the result and
    // parallelly reducing the num value .
    while (n > 0)
    {
        int remainder = n % base1 ;
        result = result + remainder ;
        n = n / base1;
    }

    // returning the result
    return result ;
}

static void printSumsOfDigits(int n)
{
    // function calling for multiple base1s
    for (int base1 = 2 ; base1 < n ; ++base1)
        Console.Write(solve(n, base1)+" ");
}

// Driver Code
public static void Main()
{
    int n = 8;
    printSumsOfDigits(n);
}
}
// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of digits of
// n in different bases from 2 to n-1.

// function to calculate sum of
// digit for a given base
function solve($n, $base)
{

    // Sum of digits
    $result = 0 ;

    // Calculating the number (n) by
    // taking mod with the base and adding
    // remainder to the result and
    // parallelly reducing the num value .
    while ($n > 0)
    {
        $remainder = $n % $base ;
        $result = $result + $remainder ;
        $n = $n / $base;
    }

    // returning the result
    return $result ;
}

function printSumsOfDigits($n)
{

    // function calling for
    // multiple bases
    for ($base = 2 ; $base < $n ; ++$base)
    {
        echo(solve($n, $base));
        echo(" ");
    }
}

// Driver code
$n = 8;
printSumsOfDigits($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find sum of digits of
// n in different bases from 2 to n-1.

    // function to calculate sum of
    // digit for a given base
    function solve(n , base) {
        // Sum of digits
        var result = 0;

        // Calculating the number (n) by
        // taking mod with the base and adding
        // remainder to the result and
        // parallelly reducing the num value .
        while (n > 0) {
            var remainder = n % base;
            result = result + remainder;
            n = parseInt(n / base);
        }

        // returning the result
        return result;
    }

    function printSumsOfDigits(n) {
        // function calling for multiple bases
        for (base = 2; base < n; ++base)
            document.write(solve(n, base) + " ");
    }

    // Driver Code

        var n = 8;
        printSumsOfDigits(n);

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
1 4 2 4 3 2 
```