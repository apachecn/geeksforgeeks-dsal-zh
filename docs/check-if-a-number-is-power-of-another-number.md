# 检查一个数是否是另一个数的幂

> 原文:[https://www . geesforgeks . org/check-如果一个数字是另一个数字的幂/](https://www.geeksforgeeks.org/check-if-a-number-is-power-of-another-number/)

给定两个正数 x 和 y，检查 y 是否是 x 的幂。
**例:**

```
Input:  x = 10, y = 1
Output: True
x^0 = 1

Input:  x = 10, y = 1000
Output: True
x^3 = 1

Input:  x = 10, y = 1001
Output: False
```

一个简单的解决方法是重复计算 x 的幂，如果一个幂等于 y，那么 y 就是一个幂，否则不是。

## C++

```
// C++ program to check if a number is power of
// another number
#include <bits/stdc++.h>
using namespace std;

/* Returns 1 if y is a power of x */
bool isPower(int x, long int y)
{
    // The only power of 1 is 1 itself
    if (x == 1)
        return (y == 1);

    // Repeatedly comput power of x
    long int pow = 1;
    while (pow < y)
        pow *= x;

    // Check if power of x becomes y
    return (pow == y);
}

/* Driver program to test above function */
int main()
{
    cout << isPower(10, 1) << endl;
    cout << isPower(1, 20) << endl;
    cout << isPower(2, 128) << endl;
    cout << isPower(2, 30) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is power of
// another number
public class Test {
    // driver method to test power method
    public static void main(String[] args)
    {
        // check the result for true/false and print.
        System.out.println(isPower(10, 1) ? 1 : 0);
        System.out.println(isPower(1, 20) ? 1 : 0);
        System.out.println(isPower(2, 128) ? 1 : 0);
        System.out.println(isPower(2, 30) ? 1 : 0);
    }
    /* Returns true if y is a power of x */
    public static boolean isPower(int x, int y)
    {
        // The only power of 1 is 1 itself
        if (x == 1)
            return (y == 1);

        // Repeatedly compute power of x
        int pow = 1;
        while (pow < y)
            pow = pow * x;

        // Check if power of x becomes y
        return (pow == y);
    }
}

// This code is contributed by Jyotsna.
```

## 蟒蛇 3

```
# python program to check
# if a number is power of
# another number

# Returns true if y is a
# power of x
def isPower (x, y):

    # The only power of 1
    # is 1 itself
    if (x == 1):
        return (y == 1)

    # Repeatedly compute
    # power of x
    pow = 1
    while (pow < y):
        pow = pow * x

    # Check if power of x
    # becomes y
    return (pow == y)

# Driver Code
# check the result for
# true/false and print.
if(isPower(10, 1)):
    print(1)
else:
    print(0)

if(isPower(1, 20)):
    print(1)
else:
    print(0)
if(isPower(2, 128)):
    print(1)
else:
    print(0)
if(isPower(2, 30)):
    print(1)
else:
    print(0)

# This code is contributed
# by Sam007.
```

## C#

```
// C# program to check if a number
// is power of another number
using System;

class GFG
{

    // Returns true if y is a power of x
    public static bool isPower (int x, int y)
    {
        // The only power of 1 is 1 itself
        if (x == 1)
        return (y == 1);

        // Repeatedly compute power of x
        int pow = 1;
        while (pow < y)
        pow = pow * x;

        // Check if power of x becomes y
        return (pow == y);
    }

    // Driver Code
    public static void Main ()
    {
        //check the result for true/false and print.
        Console.WriteLine(isPower(10, 1) ? 1 : 0);
        Console.WriteLine(isPower(1, 20) ? 1 : 0);
        Console.WriteLine(isPower(2, 128) ? 1 : 0);
        Console.WriteLine(isPower(2, 30) ? 1 : 0);
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// number is power of another number

/* Returns 1 if y is a power of x */
function isPower($x, $y)
{
    // The only power of 1 is 1 itself
    if ($x == 1)
        return ($y == 1 ? 1 : 0);

    // Repeatedly comput power of x
    $pow = 1;
    while ($pow < $y)
        $pow *= $x;

    // Check if power of x becomes y
    return ($pow == $y ? 1 : 0);
}

// Driver Code
echo isPower(10, 1) . "\n";
echo isPower(1, 20) . "\n";
echo isPower(2, 128) . "\n";
echo isPower(2, 30) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if a number
// is power of another number

/* Returns true if y is a power of x */
    function isPower(x, y)
    {
        // The only power of 1 is 1 itself
        if (x == 1)
            return (y == 1);

        // Repeatedly compute power of x
        let pow = 1;
        while (pow < y)
            pow = pow * x;

        // Check if power of x becomes y
        return (pow == y);
    }

// Driver Code

        //check the result for true/false and print.
        document.write((isPower(10, 1) ? 1 : 0) + "<br/>");
           document.write((isPower(1, 20) ? 1 : 0) + "<br/>");
        document.write((isPower(2, 128) ? 1 : 0) + "<br/>");
        document.write((isPower(2, 30) ? 1 : 0) + "<br/>");

</script>
```

**输出:**

```
1
0
1
0
```

以上解的时间复杂度为 O(Log <sub>x</sub> y)
**优化:**
我们可以优化以上解在 O(Log Log Log y)下工作。这个想法是做幂的平方，而不是乘以 x，即把 y 和 x^2、x^4、x^8…等比较。如果 x 等于 y，则返回 true。如果 x 变得大于 y，那么我们对 x 在先前幂和当前幂之间，即在 x^i 和 x^(i/2).之间的幂做二分搜索法
以下是详细步骤。

```
1) Initialize pow = x, i = 1
2) while (pow < y)
   {
      pow = pow*pow 
      i *= 2
   }    
3) If pow == y
     return true;
4) Else construct an array of powers
   from x^i to x^(i/2)
5) Binary Search for y in array constructed
   in step 4\. If not found, return false. 
   Else return true.
```

**替代解:**
想法是取 y 的对数在基数 x 上，如果结果是整数，我们就返回 true。否则就是假的。

## C++

```
// CPP program to check given number number y
// is power of x
#include <iostream>
#include <math.h>
using namespace std;

bool isPower(int x, int y)
{
    // logarithm function to calculate value
    int res1 = log(y) / log(x);
    double res2 = log(y) / log(x); // Note : this is double

    // compare to the result1 or result2 both are equal
    return (res1 == res2);
}

// Driven program
int main()
{
    cout << isPower(27, 729) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check given
// number y is power of x

class GFG
{
    static boolean isPower(int x,
                           int y)
    {
        // logarithm function to
        // calculate value
        int res1 = (int)Math.log(y) /
                   (int)Math.log(x);

         // Note : this is double         
        double res2 = Math.log(y) /
                      Math.log(x);

        // compare to the result1 or
        // result2 both are equal
        return (res1 == res2);
    }

    // Driver Code
    public static void main(String args[])
    {
        if(isPower(27, 729))
            System.out.println("1");
        else
            System.out.println("0");
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to check
# given number number y
import math
def isPower(x, y):
    # logarithm function to
    # calculate value
    res1 = math.log(y) // math.log(x);

    # Note : this is double
    res2 = math.log(y) / math.log(x);

    # compare to the result1 or
    # result2 both are equal
    return 1 if(res1 == res2) else 0;

# Driver Code
if __name__=='__main__':
    print(isPower(27, 729));

# This code is contributed by mits
# Improved by hsagarthegr8
```

## C#

```
// C# program to check given
// number y is power of x
using System;
class GFG
{
static bool isPower(int x, int y)
{
    // logarithm function to
    // calculate value
    int res1 = (int)Math.Log(y) /
               (int)Math.Log(x);

    // Note : this is double        
    double res2 = Math.Log(y) /
                  Math.Log(x);

    // compare to the result1 or
    // result2 both are equal
    return (res1 == res2);
}

// Driver Code
static void Main()
{
    if(isPower(27, 729))
        Console.WriteLine("1");
    else
        Console.WriteLine("0");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// given number number y
function isPower($x, $y)
{
    // logarithm function to
    // calculate value
    $res1 = log($y) / log($x);

    // Note : this is double
    $res2 = log($y) / log($x);

    // compare to the result1 or
    // result2 both are equal
    return ($res1 == $res2);
}

// Driver Code
echo isPower(27, 729) ;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// javascript program to check given
// number y is power of x{
function isPower(x, y)
{

    // logarithm function to
    // calculate value
    var res1 = parseInt(Math.log(y)) /
               parseInt(Math.log(x));

     // Note : this is var         
    var res2 = Math.log(y) /
                  Math.log(x);

    // compare to the result1 or
    // result2 both are equal
    return (res1 == res2);
}

// Driver Code
if(isPower(27, 729))
    document.write("1");
else
    document.write("0");

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
1
```

感谢 **Gyayak Jain** 提出这个解决方案。
本文由**马尼什·古普塔**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息