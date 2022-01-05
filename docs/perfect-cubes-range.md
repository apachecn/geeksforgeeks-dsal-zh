# 一个范围内的完美立方体

> 原文:[https://www.geeksforgeeks.org/perfect-cubes-range/](https://www.geeksforgeeks.org/perfect-cubes-range/)

给定两个给定的数字 a 和 b，其中 1 <= a <= b, find perfect cubes between a and b (a and b inclusive).
**示例:**

```
Input  :  a = 1, b = 100
Output : 1 8 27 64
Perfect cubes in the given range are 
1, 8, 27, 64

Input :  a = 24, b = 576
Output : 27 64 125 216 343 512
Perfect cubes in the given range are 
27, 64, 125, 216, 343, 512
```

这个问题类似于[两个数](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers)之间的完美平方。
**方法 1(天真):**一种天真的方法是检查 a 和 b(包括 a 和 b)
之间的所有数字，并打印出完美的立方体。以下是上述方法的代码:

## C++

```
// A Simple Method to count cubes between a and b
#include <bits/stdc++.h>
using namespace std;

void printCubes(int a, int b)
{
    // Traverse through all numbers in given range
    // and one by one check if number is prime
    for (int i = a; i <= b; i++) {
        // Check if current number 'i'
        // is perfect cube
        for (int j = 1; j * j * j <= i; j++) {
            if (j * j * j == i) {
                cout << j * j * j << "  ";
                break;
            }
        }
    }
}

// Driver code
int main()
{
    int a = 1, b = 100;
    cout << "Perfect cubes in given range:\n ";
    printCubes(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Method to count cubes between a and b

class Test {

    static void printCubes(int a, int b)
    {

        // Traverse through all numbers in given range
        // and one by one check if number is prime
        for (int i = a; i <= b; i++) {

            // Check if current number 'i'
            // is perfect cube
            for (int j = 1; j * j * j <= i; j++) {
                if (j * j * j == i) {
                    System.out.print(j * j * j + "  ");
                    break;
                }
            }
        }
    }
    // Driver method
    public static void main(String[] args)
    {
        int a = 1, b = 100;
        System.out.println("Perfect cubes in given range:");
        printCubes(a, b);
    }
}
```

## 蟒蛇 3

```
# A Simple Method to count cubes between a and b

def printCubes(a, b) :
    # Traverse through all numbers in given range
    # and one by one check if number is prime
    for i in range(a, b + 1) :

        # Check if current number 'i'
        # is perfect cube
        j = 1
        for j in range(j ** 3, i + 1 ) :

            if (j ** 3 == i) :
                print( j ** 3, end = " ")
                break

# Driver code

a = 1; b = 100
print("Perfect cubes in given range: ")
printCubes(a, b)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A Simple Method to count cubes
// between a and b
using System;

class GFG {

    static void printCubes(int a, int b)
    {

        // Traverse through all numbers
        // in given range and one by
        // one check if number is prime
        for (int i = a; i <= b; i++) {

            // Check if current number 'i'
            // is perfect cube
            for (int j = 1; j * j * j <= i; j++) {
                if (j * j * j == i) {
                    Console.Write(j * j * j + " ");
                    break;
                }
            }
        }
    }

    // Driver method
    public static void Main()
    {
        int a = 1, b = 100;

        Console.WriteLine("Perfect cubes in"
                          + " given range:");
        printCubes(a, b);
    }
}

// This code contribute by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple Method to count
// cubes between a and b

function printCubes($a, $b)
{

    // Traverse through all
    // numbers in given range
    // and one by one check
    // if number is prime
    for ($i = $a; $i <= $b; $i++)
    {

        // Check if current number 'i'
        // is perfect cube
        for ($j = 1; $j * $j * $j <= $i; $j++)
        {
            if ($j * $j * $j == $i)
            {
                echo $j * $j * $j, " ";
                break;
            }
        }
    }
}

    // Driver Code
    $a = 1;
    $b = 100;
    echo "Perfect cubes in given range:\n ";
    printCubes($a, $b);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// A Simple Method to count
// cubes between a and b
function printCubes(a, b)
{

    // Traverse through all
    // numbers in given range
    // and one by one check
    // if number is prime
    for (let i = a; i <= b; i++)
    {

        // Check if current number 'i'
        // is perfect cube
        for (let j = 1; j * j * j <= i; j++)
        {
            if (j * j * j == i)
            {
                document.write(j * j * j + " ");
                break;
            }
        }
    }
}

    // Driver Code
    let a = 1;
    let b = 100;
    document.write("Perfect cubes in given range: <br> ");
    printCubes(a, b);

// This code is contributed by gfgking.

</script>
```

输出:

```
Perfect cubes in given range:
 1 8 27 64
```

**方法二(高效):**
我们可以简单的取‘a’的立方根和‘b’的立方根，打印出它们之间的数的立方。

```
1-  Given a = 24 b = 576

2-  acr = cbrt(a))  bcr = cbrt(b)
    acr = 3 and bcr = 8

3-  Print cubes of 3 to 8 that comes under 
    the range of a and b(including a and b
    both)
    27, 64, 125, 216, 343, 512
```

下面是上述步骤的实现。

## C++

```
// Efficient method to print cubes
// between a and b
#include <cmath>
#include <iostream>
using namespace std;

// An efficient solution to print perfect
// cubes between a and b
void printCubes(int a, int b)
{
    // Find cube root of both a and b
    int acrt = cbrt(a);
    int bcrt = cbrt(b);

    // Print cubes between acrt and bcrt
    for (int i = acrt; i <= bcrt; i++)
        if (i * i * i >= a && i * i * i <= b)
            cout << i * i * i << " ";
}

// Driver code
int main()
{
    int a = 24, b = 576;
    cout << "Perfect cubes in given range:\n"
         << printCubes(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java progroam for Efficient method
// to print cubes between a and b

class Test {
    // An efficient solution to print perfect
    // cubes between a and b
    static void printCubes(int a, int b)
    {
        // Find cube root of both a and b
        int acrt = (int)Math.cbrt(a);
        int bcrt = (int)Math.cbrt(b);

        // Print cubes between acrt and bcrt
        for (int i = acrt; i <= bcrt; i++)
            if (i * i * i >= a && i * i * i <= b)
                System.out.print(i * i * i + " ");
    }

    // Driver method
    public static void main(String[] args)
    {
        int a = 24, b = 576;
        System.out.println("Perfect cubes in given range:");
        printCubes(a, b);
    }
}
```

## 蟒蛇 3

```
# Python3 code for Efficient method 
# to print cubes between a and b

def cbrt(n) :
    return (int)( n ** (1\. / 3))

# An efficient solution to print
# perfect cubes between a and b
def printCubes(a, b) :

    # Find cube root of
    # both a and b
    acrt = cbrt(a)
    bcrt = cbrt(b)

    # Print cubes between acrt and bcrt
    for i in range(acrt, bcrt + 1) :
        if (i * i * i >= a and i * i * i <= b) :
            print(i * i * i, " ", end ="")

# Driver code
a = 24
b = 576
print("Perfect cubes in given range:")
printCubes(a, b)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# progroam for Efficient
// method to print cubes
// between a and b
using System;

class GFG
{
    // An efficient solution
    // to print perfect
    // cubes between a and b
    static void printCubes(int a,
                           int b)
    {
        // Find cube root of
        // both a and b
        int acrt = (int)Math.Pow(a,
                             (double)1 / 3);
        int bcrt = (int)Math.Pow(b,
                             (double)1 / 3);

        // Print cubes between
        // acrt and bcrt
        for (int i = acrt;
                 i <= bcrt; i++)
            if (i * i * i >= a &&
                i * i * i <= b)
                Console.Write(i * i *
                              i + " ");
    }

    // Driver Code
    static public void Main ()
    {
        int a = 24;
        int b = 576;
        Console.WriteLine("Perfect cubes " +
                          "in given range:");
        printCubes(a, b);
    }
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient method to print
// cubes between a and b

// An efficient solution
// to print perfect
// cubes between a and b

function printCubes($a, $b)
{
    // Find cube root
    // of both a and b
    $acrt = (int)pow($a, 1 / 3);
    $bcrt = (int)pow($b, 1 / 3);

    // Print cubes between
    // acrt and bcrt
    for ($i = $acrt; $i <= $bcrt; $i++)
        if ($i * $i * $i >= $a &&
            $i * $i * $i <= $b)
                echo $i * $i * $i , " ";
}

// Driver code
$a = 24; $b = 576;
echo "Perfect cubes in given range:\n",
                    printCubes($a, $b);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript progroam for Efficient
    // method to print cubes
    // between a and b

    // An efficient solution
    // to print perfect
    // cubes between a and b
    function printCubes(a, b)
    {
        // Find cube root of
        // both a and b
        let acrt = parseInt(Math.pow(a, 1 / 3), 10);
        let bcrt = parseInt(Math.pow(b, 1 / 3), 10);

        // Print cubes between
        // acrt and bcrt
        for (let i = acrt; i <= bcrt; i++)
            if (i * i * i >= a && i * i * i <= b)
                document.write((i * i * i) + " ");
    }

    let a = 24;
    let b = 576;
    document.write("Perfect cubes " + "in given range:" + "</br>");
    printCubes(a, b);

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Perfect cubes in given range:
27 64 125 216 343 512
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。