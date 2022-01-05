# 如何检查给定的数字是否为斐波那契数？

> 原文:[https://www . geesforgeks . org/check-number-Fibonacci-number/](https://www.geeksforgeeks.org/check-number-fibonacci-number/)

给定一个数字‘n’，如何检查 n 是否为[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。前几个斐波那契数是 0，1，1，2，3，5，8，13，21，34，55，89，144，..
**例:**

```
Input : 8
Output : Yes

Input : 34
Output : Yes

Input : 41
Output : No
```

一个简单的方法是[生成斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，直到生成的数大于等于‘n’。下面是关于斐波那契数的一个有趣的属性，它也可以用来检查给定的数是否是斐波那契数。
*当且仅当(5*n <sup>2</sup> + 4)或(5 * n<sup>2</sup>–4)中的一个或两个是完美正方形*(来源: [Wiki](http://en.wikipedia.org/wiki/Fibonacci_number#Recognizing_Fibonacci_numbers) )时，一个数就是斐波那契数。下面是一个基于这个概念的简单程序。

## C++

```
// C++ program to check if x is a perfect square
#include <iostream>
#include <math.h>
using namespace std;

// A utility function that returns true if x is perfect square
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s*s == x);
}

// Returns true if n is a Fibinacci Number, else false
bool isFibonacci(int n)
{
    // n is Fibinacci if one of 5*n*n + 4 or 5*n*n - 4 or both
    // is a perferct square
    return isPerfectSquare(5*n*n + 4) ||
           isPerfectSquare(5*n*n - 4);
}

// A utility function to test above functions
int main()
{
  for (int i = 1; i <= 10; i++)
     isFibonacci(i)? cout << i << " is a Fibonacci Number \n":
                     cout << i << " is a not Fibonacci Number \n" ;
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if x is a perfect square

class GFG
{
    // A utility method that returns true if x is perfect square
    static  boolean isPerfectSquare(int x)
    {
        int s = (int) Math.sqrt(x);
        return (s*s == x);
    }

    // Returns true if n is a Fibonacci Number, else false
    static boolean isFibonacci(int n)
    {
        // n is Fibonacci if one of 5*n*n + 4 or 5*n*n - 4 or both
        // is a perfect square
        return isPerfectSquare(5*n*n + 4) ||
               isPerfectSquare(5*n*n - 4);
    }

    // Driver method
    public static void main(String[] args)
    {
        for (int i = 1; i <= 10; i++)
             System.out.println(isFibonacci(i) ?  i +  " is a Fibonacci Number" :
                                                  i + " is a not Fibonacci Number");
    }
}
//This code is contributed by Nikita Tiwari
```

## 计算机编程语言

```
# python program to check if x is a perfect square
import math

# A utility function that returns true if x is perfect square
def isPerfectSquare(x):
    s = int(math.sqrt(x))
    return s*s == x

# Returns true if n is a Fibinacci Number, else false
def isFibonacci(n):

    # n is Fibinacci if one of 5*n*n + 4 or 5*n*n - 4 or both
    # is a perferct square
    return isPerfectSquare(5*n*n + 4) or isPerfectSquare(5*n*n - 4)

# A utility function to test above functions
for i in range(1,11):
     if (isFibonacci(i) == True):
         print i,"is a Fibonacci Number"
     else:
         print i,"is a not Fibonacci Number "
```

## C#

```
// C# program to check if
// x is a perfect square
using System;

class GFG {

    // A utility function that returns
    // true if x is perfect square
    static bool isPerfectSquare(int x)
    {
        int s = (int)Math.Sqrt(x);
        return (s * s == x);
    }

    // Returns true if n is a
    // Fibonacci Number, else false
    static bool isFibonacci(int n)
    {
        // n is Fibonacci if one of
        // 5*n*n + 4 or 5*n*n - 4 or
        // both are a perfect square
        return isPerfectSquare(5 * n * n + 4) ||
               isPerfectSquare(5 * n * n - 4);
    }

    // Driver method
    public static void Main()
    {
        for (int i = 1; i <= 10; i++)
            Console.WriteLine(isFibonacci(i) ? i +
                              " is a Fibonacci Number" : i +
                              " is a not Fibonacci Number");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// x is a perfect square

// A utility function that
// returns true if x is
// perfect square
function isPerfectSquare($x)
{
    $s = (int)(sqrt($x));
    return ($s * $s == $x);
}

// Returns true if n is a
// Fibinacci Number, else false
function isFibonacci($n)
{
    // n is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or
    // both is a perferct square
    return isPerfectSquare(5 * $n * $n + 4) ||
           isPerfectSquare(5 * $n * $n - 4);
}

// Driver Code
for ($i = 1; $i <= 10; $i++)
if(isFibonacci($i))
echo "$i is a Fibonacci Number \n";
else
echo "$i is a not Fibonacci Number \n" ;

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to check if x is a perfect square

// A utility function that returns true if x is perfect square
function isPerfectSquare( x)
{
    let s = parseInt(Math.sqrt(x));
    return (s * s == x);
}

// Returns true if n is a Fibinacci Number, else false
function isFibonacci( n)
{

    // n is Fibinacci if one of 5*n*n + 4 or 5*n*n - 4 or both
    // is a perferct square
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// A utility function to test above functions
  for (let i = 1; i <= 10; i++)
     isFibonacci(i)?  document.write( i + " is a Fibonacci Number <br/>"):
                     document.write(i + " is a not Fibonacci Number <br/>") ;

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
1 is a Fibonacci Number
2 is a Fibonacci Number
3 is a Fibonacci Number
4 is a not Fibonacci Number
5 is a Fibonacci Number
6 is a not Fibonacci Number
7 is a not Fibonacci Number
8 is a Fibonacci Number
9 is a not Fibonacci Number
10 is a not Fibonacci Number
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

本文由**阿沛·拉提**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息