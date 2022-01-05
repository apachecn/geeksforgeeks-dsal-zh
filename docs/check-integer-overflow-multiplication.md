# 检查乘法时的整数溢出

> 原文:[https://www . geesforgeks . org/check-integer-overflow-乘法/](https://www.geeksforgeeks.org/check-integer-overflow-multiplication/)

给定两个整数 a 和 b，找出它们的乘积(a x b)是否超过有符号的 64 位整数。如果超过打印是否则打印编号
**示例:**

```
Input : a = 100, b = 200 
Output : No

Input : a = 10000000000,
        b = -10000000000
Output : Yes
```

**进场:**

1.  如果这两个数字中的任何一个是 0，那么它将永远不会超出范围。
2.  否则如果两者的乘积除以一等于另一，那么它也在范围内。
3.  在任何其他情况下都会发生溢出。

## C++

```
// CPP program to check for integer
// overflow on multiplication
#include <iostream>
using namespace std;

// Function to check whether there is
// overflow in a * b or not. It returns
// true if there is overflow.
bool isOverflow(long long a, long long b)
{
    // Check if either of them is zero
    if (a == 0 || b == 0)
        return false;

    long long result = a * b;
    if (a == result / b)
        return false;
    else
        return true;
}

// Driver code
int main()
{
    long long a = 10000000000, b = -10000000000;
    if (isOverflow(a, b))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check for integer
// overflow on multiplication
import java.util.*;
import java.lang.*;

public class GfG{

    // Function to check whether there is
    // overflow in a * b or not. It
    // returns true if there is overflow.
    static Boolean isOverflow( long a, long b)
    {
        // Check if either of them is zero
        if (a == 0 || b == 0)
            return false;

        long result = a * b;
        if (a == result / b)
            return false;
        else
            return true;
    }

    // driver function
    public static void main(String argc[])
    {
        long a = Long.parseLong("10000000000");
        long b = Long.parseLong("-10000000000");

        if (isOverflow(a, b))
        System.out.print("Yes");
    else
        System.out.print("No");
    }
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python program to check for integer
# overflow on multiplication

# Function to check whether there is
# overflow in a * b or not. It returns
# true if there is overflow.
def isOverflow(a, b):

    # Check if either of them is zero
    if (a == 0 or b == 0) :
        return False

    result = a * b
    if (result >= 9223372036854775807 or
        result <= -9223372036854775808):
        result=0
    if (a == (result // b)):
        print(result // b)
        return False
    else:
        return True

# Driver code
if __name__ =="__main__":
    a = 10000000000
    b = -10000000000
    if (isOverflow(a, b)):
        print( "Yes")
    else:
        print( "No")

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to check for integer
// overflow on multiplication
using System;

public class GfG
{

    // Function to check whether there is
    // overflow in a * b or not. It
    // returns true if there is overflow.
    static bool isOverflow( long a, long b)
    {
        // Check if either of them is zero
        if (a == 0 || b == 0)
            return false;

        long result = a * b;
        if (a == result / b)
            return false;
        else
            return true;
    }

    // Driver function
    public static void Main()
    {
        long a = 10000000000;
        long b = -10000000000 ;

        if (isOverflow(a, b))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check for integer
// overflow on multiplication

// Function to check whether there is
// overflow in a * b or not. It returns
// true if there is overflow.
function isOverflow($a, $b)
{
    // Check if either of them is zero
    if ($a == 0 || $b == 0)
        return false;

    $result = $a * $b;
    if ($a == (int)$result / $b)
        return false;
    else
        return true;
}

// Driver code
$a = 10000000000;
$b = -10000000000;
if (isOverflow($a, $b))
    echo "Yes";
else
    echo "No";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check for integer
// overflow on multiplication

// Function to check whether there is
// overflow in a * b or not. It returns
// true if there is overflow.
function isOverflow(a, b)
{
    // Check if either of them is zero
    if (a == 0 || b == 0)
        return false;

    var result = a*b;
    if (result >= 9223372036854775807 ||
        result <= -9223372036854775808)
        result=0
    if (a == parseInt(result / b))
        return false;
    else
        return true;
}

// Driver code
var a = 10000000000, b = -10000000000;
if (isOverflow(a, b))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(1)