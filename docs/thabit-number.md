# 塔比特数

> 原文:[https://www.geeksforgeeks.org/thabit-number/](https://www.geeksforgeeks.org/thabit-number/)

给定一个正整数 n，任务是检查它是否是一个 Thabit 数。如果给定的数字是泰国数字，则打印“是”，否则打印“否”。
[**塔比特数**](https://en.wikipedia.org/wiki/Thabit_number) **:** 在数学中，塔比特数是 3* 2 形式的正整数<sup>n</sup>–1，其中 *n* 是非负整数。
前几个 Thabit 数字是–
2、5、11、23、47、95、191、383、767、1535、3071、6143、12287、24575、49151、98303、196607、393215、

**例:**

> 输入:47
> 输出:是
> 说明:对于 n=4，47 可以用 3.2 <sup>n</sup> -1 表示为 3.2 <sup>4</sup> -1。
> 输入:65
> 输出:否
> 不存在可以用*3.2<sup>n</sup>–1*形式表示 65 的 n 值

**进场:**

1.  给定的数字加 1，现在数字必须是**3 * 2<sup>n</sup>T3 的形式**
2.  用 3 除这个数，现在这个数必须是**2<sup>n</sup>T3 的形式**
3.  检查数字是否是 2 的幂，要检查数字是否是 2 的幂[请参考此处。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)
4.  如果数字是 2 的幂，则打印“是”，否则打印“否”。

## C++

```
// CPP program to check if a given
// number is Thabit number or not.
#include <bits/stdc++.h>
using namespace std;

// Utility function to check power of two
bool isPowerOfTwo(int n)
{
    return (n && !(n & (n - 1)));
}

// function to check if the given number
// is Thabit Number
bool isThabitNumber(int n)
{
    // Add 1 to the number
    n = n + 1;

    // Divide the number by 3
    if (n % 3 == 0)
        n = n / 3;
    else
        return false;

    // Check if the given number is power of 2
    if (isPowerOfTwo(n))
        return true;

    else
        return false;
}

// Driver Program
int main()
{
    int n = 47;
    if (isThabitNumber(n))
        cout << "YES";   
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check
// for thabit number

class GFG {

    // Utility function to check power of two
    static boolean isPowerOfTwo(int n)
    {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // function to check if the given number
    // is Thabit Number
    static boolean isThabitNumber(int n)
    {
        // Add 1 to the number
        n = n + 1;

        // Divide the number by 3
        if (n % 3 == 0)
            n = n / 3;
        else
            return false;

        // Check if the given number is power of 2
        if (isPowerOfTwo(n))
            return true;

        else
            return false;
    }

    // Driver Program
    public static void main(String[] args)
    {
        int n = 47;

        // Check if number is
        // thabit number

        if (isThabitNumber(n)) {
            System.out.println("YES");
        }
        else {
            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python code to check
# thabit number

# Utility function to Check
# power of two

def isPowerOfTwo(n):

    return (n and (not(n & (n - 1))))

# function to check if the given number
# is Thabit Number
def isThabitNumber( n ):

    # Add 1 to the number
    n = n + 1;

    # Divide the number by 3
    if (n % 3 == 0):
        n = n//3;
    else:
       return False

    # Check if the given number
    # is power of 2 
    if (isPowerOfTwo(n)):
        return True

    else:
         return False   

# Driver Program
n = 47

# Check if number is
# thabit number
if (isThabitNumber(n)):
    print("YES")
else: 
    print("NO")
```

## C#

```
// C# code to check
// thabit number

using System;
class GFG {

    // Utility function to check power of two
    static bool isPowerOfTwo(int n)
    {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // function to check if the given number
    // is Thabit Number
    static bool isThabitNumber(int n)
    {
        // Add 1 to the number
        n = n + 1;

        // Divide the number by 3
        if (n % 3 == 0)
            n = n / 3;
        else
            return false;

        // Check if the given number is power of 2
        if (isPowerOfTwo(n))
            return true;

        else
            return false;
    }
    // Driver Program
    public static void Main()
    {
        int n = 47;

        // Check if number is
        // thabit number

        if (isThabitNumber(n)) {
            Console.WriteLine("YES");
        }
        else {
            Console.WriteLine("NO");
        }
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given
// number is Thabit number or not.

// Utility function to check
// power of two
function isPowerOfTwo($n)
{
    return ($n && !($n & ($n - 1)));
}

// function to check if the
// given number is Thabit Number
function isThabitNumber($n)
{
    // Add 1 to the number
    $n = $n + 1;

    // Divide the number by 3
    if ($n % 3 == 0)
        $n = $n / 3;
    else
        return false;

    // Check if the given number
    // is power of 2
    if (isPowerOfTwo($n))
        return true;

    else
        return false;
}

// Driver Code
$n = 47;
if (isThabitNumber($n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a given
// number is Thabit number or not.

// Utility function to check power of two
function isPowerOfTwo(n)
{
    return (n && !(n & (n - 1)));
}

// function to check if the given number
// is Thabit Number
function isThabitNumber(n)
{
    // Add 1 to the number
    n = n + 1;

    // Divide the number by 3
    if (n % 3 == 0)
        n = n / 3;
    else
        return false;

    // Check if the given number is power of 2
    if (isPowerOfTwo(n))
        return true;

    else
        return false;
}

// Driver Program
var n = 47;
if (isThabitNumber(n))
    document.write( "YES");   
else
    document.write("NO");

</script>
```

**Output:** 

```
YES
```