# 检查一个数字是否可以表示为 2^x + 2^y

> 原文:[https://www . geesforgeks . org/check-if-a-number-can-express-as-2x-2y/](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-2x-2y/)

给定一个数字 n，我们需要检查它是否可以表示为 2 <sup>x</sup> + 2 <sup>y</sup> 。这里 x 和 y 可以相等。
**例:**

```
Input  : 24
Output : Yes 
Explanation: 24 can be expressed as  
24 + 23 

Input  : 13
output : No
Explanation: It is not possible to 
express 13 as sum of two powers of 2.
```

如果我们举几个例子，我们可以注意到，如果一个数已经是 2 的幂(对于 n > 1)，或者我们从这个数中减去先前的 2 的幂后得到的余数也是 2 的幂，那么这个数可以用 2^x + 2^y 的形式表示。
以下是以上思路的实现

## C++

```
// CPP code to check if a number can be
// expressed as  2^x + 2^y
#include <bits/stdc++.h>
using namespace std;

// Utility function to check if
// a number is power of 2 or not
bool isPowerOfTwo(int n)
{
    return (n && !(n & (n - 1)));
}

// Utility function to determine the
// value of previous power of 2
int previousPowerOfTwo(int n)
{
    while (n & n - 1) {
        n = n & n - 1;
    }
    return n;
}

// function to check if n can be expressed
// as 2^x + 2^y or not
bool checkSum(int n)
{
    // if value of n is 0 or 1
    // it can not be expressed as
    // 2^x + 2^y
    if (n == 0 || n == 1)
       return false;

    // if a number is power of 2
    // then it can be expressed as
    // 2^x + 2^y
    else if (isPowerOfTwo(n)) {
        cout << " " << n / 2 << " " << n / 2;
        return true;
    }

    else {
        // if the remainder after
        // subtracting previous power of 2
        // is also a power of 2 then
        // it can be expressed as
        // 2^x + 2^y
        int x = previousPowerOfTwo(n);
        int y = n - x;
        if (isPowerOfTwo(y)) {
            cout << " " << x << " " << y;
            return true;
        }
    }

    return false;
}

// driver code
int main()
{
    int n1 = 20;
    if (checkSum(n1) == false)
        cout << "No";

    cout << endl;
    int n2 = 11;
    if (checkSum(n2) == false)
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a number
// can be expressed as 2^x + 2^y

class GFG {

    // Utility function to check if
    // a number is power of 2 or not
    static boolean isPowerOfTwo(int n)
    {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // Utility function to determine the
    // value of previous power of 2
    static int previousPowerOfTwo(int n)
    {
        while ((n & n - 1) > 1) {
            n = n & n - 1;
        }
        return n;
    }

    // function to check if
    // n can be expressed as
    // 2^x + 2^y or not
    static boolean checkSum(int n)
    {
        // if value of n is 0 or 1
        // it can not be expressed as
        // 2^x + 2^y
        if (n == 0 || n == 1)
            return false;

        // if a number is power of 2
        // it can be expressed as
        // 2^x + 2^y

        else if (isPowerOfTwo(n)) {
            System.out.println(n / 2 + " " + n / 2);
        }
        else {

            // if the remainder after
            // subtracting previous power of 2
            // is also a power of 2 then
            // it can be expressed as
            // 2^x + 2^y
            int x = previousPowerOfTwo(n);
            int y = n - x;
            if (isPowerOfTwo(y)) {

                System.out.println(x + " " + y);
                return true;
            }
        }

         return false;
    }
    // driver code
    public static void main(String[] argc)
    {
    int n1 = 20;
    if (checkSum(n1) == false)
        System.out.println("No");

    System.out.println();
    int n2 = 11;
    if (checkSum(n2) == false)
        System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 code to check if a number
# can be expressed as
# 2 ^ x + 2 ^ y

# Utility function to check if
# a number is power of 2 or not
def isPowerOfTwo( n):
    return (n and (not(n & (n - 1))) )

# Utility function to determine the
# value of previous power of 2       
def previousPowerOfTwo( n ):   
    while( n & n-1 ):
        n = n & n - 1
    return n

# function to check if
# n can be expressed as
# 2 ^ x + 2 ^ y or not
def checkSum(n):

        # if value of n is 0 or 1
        # it can not be expressed as
        # 2 ^ x + 2 ^ y
        if (n == 0 or n == 1 ):
            return False

        # if n is power of two then
        # it can be expressed as
        # sum of 2 ^ x + 2 ^ y
        elif(isPowerOfTwo(n)):
            print(n//2, n//2)
            return True

        # if the remainder after
        # subtracting previous power of 2
        # is also a power of 2 then
        # it can be expressed as
        # 2 ^ x + 2 ^ y
        else:
                x = previousPowerOfTwo(n)
                y = n-x;
                if (isPowerOfTwo(y)):
                    print(x, y)
                    return True
                else:                   
                    return False

# driver code
n1 = 20
if (checkSum(n1)):
  print("No")

n2 = 11
if (checkSum(n2)):
  print("No")
```

## C#

```
// C# code to check if a number
// can be expressed as
// 2^x + 2^y

using System;
class GFG {

    // Utility function to check if
    // a number is power of 2 or not
    static bool isPowerOfTwo(int n)
    {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // Utility function to determine the
    // value of previous power of 2
    static int previousPowerOfTwo(int n)
    {

        while ((n & n - 1) > 1) {
            n = n & n - 1;
        }
        return n;
    }

    // function to check if
    // n can be expressed as
    // 2^x + 2^y or not
    static bool checkSum(int n)
    {
        // if value of n is 0 or 1
        // it can not be expressed as
        // 2^x + 2^y
        if (n == 0 || n == 1) {
            Console.WriteLine("No");
            return false;
        }

        // if a number is power of
        // it can be expressed as
        // 2^x + 2^y

        else if (isPowerOfTwo(n)) {
            Console.WriteLine(n / 2 + " " + n / 2);
            return true;
        }

        else {

            // if the remainder after
            // subtracting previous power  of 2
            // is also a power of 2 then
            // it can be expressed as
            // 2^x + 2^y

            int x = previousPowerOfTwo(n);
            int y = n - x;
            if (isPowerOfTwo(y)) {
                Console.WriteLine(x + " " + y);
                return true;
            }
            else {
                return false;
            }
        }
    }
    // driver code
    public static void Main()
    {
    int n1 = 20;
    if (checkSum(n1) == false)
        Console.WriteLine("No");

    Console.WriteLine();
    int n2 = 11;
    if (checkSum(n2) == false)
        Console.WriteLine("No");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if a number
// can be expressed as 2^x + 2^y

// Utility function to check if
// a number is power of 2 or not
function isPowerOfTwo($n)
{
    return ($n and !($n & ($n - 1)));
}

// Utility function to determine
// the value of previous power of 2
function previousPowerOfTwo($n)
{
    while ($n & $n - 1)
    {
        $n = $n & $n - 1;
    }
    return $n;
}

// function to check if
// n can be expressed
// as 2^x + 2^y or not
function checkSum($n)
{
    // if value of n is 0 or 1
    // it can not be expressed
    // as 2^x + 2^y
    if ($n == 0 or $n == 1)
    return false;

    // if a number is power of 2
    // then it can be expressed
    // as 2^x + 2^y
    else if (isPowerOfTwo($n))
    {
        echo " " , $n / 2 , " " , $n / 2;
        return true;
    }

    else
    {
        // if the remainder after
        // subtracting previous power
        // of 2 is also a power of 2
        // then it can be expressed
        // as 2^x + 2^y
        $x = previousPowerOfTwo($n);
        $y = $n - $x;
        if (isPowerOfTwo($y))
        {
            echo $x, " ", $y;
            return true;
        }
    }

    return false;
}

// Driver code
$n1 = 20;
if (checkSum($n1) == false)
    echo "No";
echo"\n";

$n2 = 11;
if (checkSum($n2) == false)
    echo "No";

// This code is contributed
// by chandan_jnu.
?>
```

## java 描述语言

```
<script>
// javascript code to check if a number
// can be expressed as 2^x + 2^y
    // Utility function to check if
    // a number is power of 2 or not
    function isPowerOfTwo(n) {
        return n != 0 && ((n & (n - 1)) == 0);
    }

    // Utility function to determine the
    // value of previous power of 2
    function previousPowerOfTwo(n) {
        while ((n & n - 1) > 1) {
            n = n & n - 1;
        }
        return n;
    }

    // function to check if
    // n can be expressed as
    // 2^x + 2^y or not
    function checkSum(n)
    {

        // if value of n is 0 or 1
        // it can not be expressed as
        // 2^x + 2^y
        if (n == 0 || n == 1)
            return false;

        // if a number is power of 2
        // it can be expressed as
        // 2^x + 2^y

        else if (isPowerOfTwo(n))
        {
            document.write(n / 2 + " " + n / 2+"<br/>");
        }
        else
        {

            // if the remainder after
            // subtracting previous power of 2
            // is also a power of 2 then
            // it can be expressed as
            // 2^x + 2^y
            var x = previousPowerOfTwo(n);
            var y = n - x;
            if (isPowerOfTwo(y))
            {
                document.write(x + " " + y + "<br/>");
                return true;
            }
        }
        return false;
    }

    // driver code
        var n1 = 20;
        if (checkSum(n1) == false)
            document.write("No");

        document.write();
        var n2 = 11;
        if (checkSum(n2) == false)
            document.write("No");

// This code is contributed by gauravrajput1.
</script>
```

**Output:** 

```
16 4
No
```