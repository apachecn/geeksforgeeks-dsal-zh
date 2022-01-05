# 打印质因数集是 X 的质因数集的子集的所有数字

> 原文:[https://www . geesforgeks . org/print-all-numbers-其素因子集是 x 素因子集的子集/](https://www.geeksforgeeks.org/print-all-numbers-whose-set-of-prime-factors-is-a-subset-of-the-set-of-the-prime-factors-of-x/)

给定一个 X 数和一个 N 数的数组。任务是打印数组中质因数集是 x 的质因数集的子集的所有数字。
**示例:**

> **输入:** X = 60，a[] = {2，5，10，7，17}
> **输出:**2 5 10
> 60 的素因子集:{2，3，5 }
> 2 的素因子集:{2 }
> 5 的素因子集:{ 5 }
> 10 的素因子集:{ 2，5 }
> 7 的素因子集:{ 7 }
> 17 的素因子集:{17
> **输入:** X = 15，a[] = {2，8}
> **输出:**没有这样的数字

**逼近**:对数组中的每一个元素进行迭代，继续将该数除以该数的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 和 **X** ，直到该数和 **X** 的 gcd 变为 1。如果在连续除法运算后，最后的数字变成 1，那么就打印这个数字。
以下是上述方法的实施:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the numbers
void printNumbers(int a[], int n, int x)
{

    bool flag = false;

    // Iterate for every element in the array
    for (int i = 0; i < n; i++) {

        int num = a[i];

        // Find the gcd
        int g = __gcd(num, x);

        // Iterate till gcd is 1
        // of number and x
        while (g != 1) {

            // Divide the number by gcd
            num /= g;

            // Find the new gcdg
            g = __gcd(num, x);
        }

        // If the number is 1 at the end
        // then print the number
        if (num == 1) {
            flag = true;
            cout << a[i] << " ";
        }
    }

    // If no numbers have been there
    if (!flag)
        cout << "There are no such numbers";
}

// Drivers code
int main()
{
    int x = 60;
    int a[] = { 2, 5, 10, 7, 17 };
    int n = sizeof(a) / sizeof(a[0]);

    printNumbers(a, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

// Function to print all the numbers
static void printNumbers(int a[], int n, int x)
{

    boolean flag = false;

    // Iterate for every element in the array
    for (int i = 0; i < n; i++)
    {

        int num = a[i];

        // Find the gcd
        int g = __gcd(num, x);

        // Iterate till gcd is 1
        // of number and x
        while (g != 1)
        {

            // Divide the number by gcd
            num /= g;

            // Find the new gcdg
            g = __gcd(num, x);
        }

        // If the number is 1 at the end
        // then print the number
        if (num == 1)
        {
            flag = true;
            System.out.print(a[i] + " ");
        }
    }

    // If no numbers have been there
    if (!flag)
        System.out.println("There are no such numbers");
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Drivers code
public static void main(String[] args)
{
    int x = 60;
    int a[] = { 2, 5, 10, 7, 17 };
    int n = a.length;

    printNumbers(a, n, x);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import gcd

# Function to print all the numbers
def printNumbers(a, n, x) :

    flag = False

    # Iterate for every element in the array
    for i in range(n) :

        num = a[i]

        # Find the gcd
        g = gcd(num, x)

        # Iterate till gcd is 1
        # of number and x
        while (g != 1) :

            # Divide the number by gcd
            num //= g

            # Find the new gcdg
            g = gcd(num, x)

        # If the number is 1 at the end
        # then print the number
        if (num == 1) :
            flag = True;
            print(a[i], end = " ");

    # If no numbers have been there
    if (not flag) :
        print("There are no such numbers")

# Driver Code
if __name__ == "__main__" :

    x = 60
    a = [ 2, 5, 10, 7, 17 ]
    n = len(a)

    printNumbers(a, n, x)

# This code is contributed by Ryuga
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to print all the numbers
static void printNumbers(int []a, int n, int x)
{

    bool flag = false;

    // Iterate for every element in the array
    for (int i = 0; i < n; i++)
    {

        int num = a[i];

        // Find the gcd
        int g = __gcd(num, x);

        // Iterate till gcd is 1
        // of number and x
        while (g != 1)
        {

            // Divide the number by gcd
            num /= g;

            // Find the new gcdg
            g = __gcd(num, x);
        }

        // If the number is 1 at the end
        // then print the number
        if (num == 1)
        {
            flag = true;
            Console.Write(a[i] + " ");
        }
    }

    // If no numbers have been there
    if (!flag)
        Console.WriteLine("There are no such numbers");
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver code
public static void Main(String[] args)
{
    int x = 60;
    int []a = { 2, 5, 10, 7, 17 };
    int n = a.Length;

    printNumbers(a, n, x);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function to print all the numbers
function printNumbers($a, $n, $x)
{

    $flag = false;

    // Iterate for every element in the array
    for ($i = 0; $i < $n; $i++)
    {

        $num = $a[$i];

        // Find the gcd
        $g = __gcd($num, $x);

        // Iterate till gcd is 1
        // of number and x
        while ($g != 1)
        {

            // Divide the number by gcd
            $num /= $g;

            // Find the new gcdg
            $g = __gcd($num, $x);
        }

        // If the number is 1 at the end
        // then print the number
        if ($num == 1)
        {
            $flag = true;
            echo $a[$i] , " ";
        }
    }

    // If no numbers have been there
    if (!$flag)
        echo ("There are no such numbers");
}

function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);

}

// Driver code

$x = 60;
$a = array(2, 5, 10, 7, 17 );
$n = count($a);

printNumbers($a, $n, $x);

// This code has been contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to print all the numbers

// Find the gcd
function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

function printNumbers(a, n, x)
{

    let flag = false;

    // Iterate for every element in the array
    for (let i = 0; i < n; i++) {

        let num = a[i];

        // Find the gcd
        let g = __gcd(num, x);

        // Iterate till gcd is 1
        // of number and x
        while (g != 1) {

            // Divide the number by gcd
            num = parseInt(num/g);

            // Find the new gcdg
            g = __gcd(num, x);
        }

        // If the number is 1 at the end
        // then print the number
        if (num == 1) {
            flag = true;
            document.write(a[i] + " ");
        }
    }

    // If no numbers have been there
    if (!flag)
        document.write("There are no such numbers");
}

// Drivers code

    let x = 60;
    let a = [ 2, 5, 10, 7, 17 ];
    let n = a.length;

    printNumbers(a, n, x);

</script>
```

**Output:** 

```
2 5 10
```