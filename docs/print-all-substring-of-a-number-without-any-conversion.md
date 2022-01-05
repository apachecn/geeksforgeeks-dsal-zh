# 不做任何转换打印一个数字的所有子串

> 原文:[https://www . geeksforgeeks . org/print-无任何转换的数字的所有子串/](https://www.geeksforgeeks.org/print-all-substring-of-a-number-without-any-conversion/)

给定一个整数 N，任务是打印 N 的所有子字符串，而不做任何转换，即将其转换为字符串或数组。

**示例**:

> **输入** : N = 12345
> **输出**:可能的子串:{1，12，123，1234，12345，2，23，234，2345，3，34，345，4，45，5}
> **输入** : N = 123
> **输出**:可能的子串:{1，12，123，2，23，3

**进场:**

1.  根据大小取 10 的幂。
2.  将数字除以 0，然后打印出来。
3.  然后通过取 k 的模，将该数改变到该数的下一个位置。
4.  更新位数。
5.  重复同样的过程，直到 n 变成 0。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the substrings of a number
void printSubstrings(int n)
{
    // Calculate the total number of digits
    int s = log10(n);

    // 0.5 has been added because of it will
    // return double value like 99.556
    int d = (int)(pow(10, s) + 0.5);
    int k = d;

    while (n) {

        // Print all the numbers from
        // starting position
        while (d) {
            cout << n / d << endl;
            d = d / 10;
        }

        // Update the no.
        n = n % k;

        // Update the no.of digits
        k = k / 10;
        d = k;
    }
}

// Driver code
int main()
{
    int n = 123;
    printSubstrings(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// Function to print the
// substrings of a number
static void printSubstrings(int n)
{
    // Calculate the total
    // number of digits
    int s = (int)Math.log10(n);

    // 0.5 has been added because
    // of it will return double
    // value like 99.556
    int d = (int)(Math.pow(10, s) + 0.5);
    int k = d;

    while (n > 0)
    {

        // Print all the numbers
        // from starting position
        while (d > 0)
        {
            System.out.println(n / d);
            d = d / 10;
        }

        // Update the no.
        n = n % k;

        // Update the no.of digits
        k = k / 10;
        d = k;
    }
}

// Driver code
public static void main(String args[])
{
    int n = 123;
    printSubstrings(n);
}
}

// This code is contributed
// by Subhadeep
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import math

# Function to print the substrings of a number
def printSubstrings(n):

    # Calculate the total number of digits
    s = int(math.log10(n));

    # 0.5 has been added because of it will
    # return double value like 99.556
    d = (math.pow(10, s));
    k = d;

    while (n > 0):

        # Print all the numbers from
        # starting position
        while (d > 0):
            print(int(n // d));
            d = int(d / 10);

        # Update the no.
        n = int(n % k);

        # Update the no.of digits
        k = int(k // 10);
        d = k;

# Driver code
if __name__ == '__main__':
    n = 123;
    printSubstrings(n);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation
// of above approach
using System;

class GFG
{
// Function to print the
// substrings of a number
static void printSubstrings(int n)
{
    // Calculate the total
    // number of digits
    int s = (int)Math.Log10(n);

    // 0.5 has been added because
    // of it will return double
    // value like 99.556
    int d = (int)(Math.Pow(10, s) + 0.5);
    int k = d;

    while (n > 0)
    {

        // Print all the numbers
        // from starting position
        while (d > 0)
        {
            Console.WriteLine(n / d);
            d = d / 10;
        }

        // Update the no.
        n = n % k;

        // Update the no.of digits
        k = k / 10;
        d = k;
    }
}

// Driver code
public static void Main()
{
    int n = 123;
    printSubstrings(n);
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to print the substrings
// of a number
function printSubstrings($n)
{
    // Calculate the total number
    // of digits
    $s = (int)log10($n);

    // 0.5 has been added because
    // of it will return double
    // value like 99.556
    $d = (int)(pow(10, $s) + 0.5);
    $k = $d;

    while ($n)
    {

        // Print all the numbers from
        // starting position
        while ($d)
        {
            echo (int)($n / $d) . "\n";
            $d = (int)($d / 10);
        }

        // Update the no.
        $n = $n % $k;

        // Update the no.of digits
        $k = (int)($k / 10);
        $d = $k;
    }
}

// Driver code
$n = 123;
printSubstrings($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript implementation
// of above approach
// Function to print the
// substrings of a number
function printSubstrings(n)
{
    // Calculate the total
    // number of digits
    var s = parseInt(Math.log10(n));

    // 0.5 has been added because
    // of it will return double
    // value like 99.556
    var d = parseInt((Math.pow(10, s) + 0.5));
    var k = d;

    while (n > 0)
    {

        // Print all the numbers
        // from starting position
        while (d > 0)
        {
            document.write(parseInt(n / d)+"<br>");
            d = parseInt(d / 10);
        }

        // Update the no.
        n = n % k;

        // Update the no.of digits
        k = parseInt(k / 10);
        d = k;
    }
}

// Driver code

var n = 123;
printSubstrings(n);

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
1
12
123
2
23
3
```