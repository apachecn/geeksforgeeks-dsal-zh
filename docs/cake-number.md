# 蛋糕号

> 原文:[https://www.geeksforgeeks.org/cake-number/](https://www.geeksforgeeks.org/cake-number/)

考虑一个 3D 立方体和 n 个平面。我们可以用给定的平面在立方体上切割。给定 n 的饼数是由 n 个平面形成的区域的最大数量。
**n 次平面切割后的系列(0 ≤ n)** :
1、2、4、8、15、26、42、64、93、130、176、232、299、378、470、576、697…

**示例:**

```
Input : 1
Output : 2
Explanation : 
With 1 plane cut the cube is divided into 2 regions

Input : 2
Output : 4
Explanation: 
With 2 plane cuts, we can divide the cube into 4 regions

Input : 4
Output : 15

Input : 5
Output : 26
```

[Recommended: Please try your approach on ***<u>{IDE}</u>*** first, before moving on to the solution.](https://ide.geeksforgeeks.org/) 

饼号第 n 项公式:

> 第 n 个蛋糕号码=<sup>n</sup>C<sup>3</sup>+<sup>n</sup>C<sup>2</sup>+<sup>n</sup>C<sup>1</sup>+<sup>n</sup>C<sup>0</sup>T16】=(n<sup>3</sup>+5 * n+6)/6

以下是上述方法的实现:

## C++

```
// CPP Program to find the
// nth Cake number
#include <iostream>
using namespace std;

// function for Cake number
int number_cake(int n)
{
    // formula for find  Cake number
    // nth term
    return (n * n * n + 5 * n + 6) / 6;
}

// Driver Code
int main()
{
    // For 2nd cake Number
    int n = 2;
    cout << number_cake(n) << endl;

    // For 8th cake Number
    n = 8;
    cout << number_cake(n) << endl;
    // For 25th cake Number
    n = 25;
    cout << number_cake(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the nth Cake number
import java.io.*;

class GFG {

    // function for Cake number
    static int number_cake(int n)
    {

        // formula for find Cake number
        // nth term
        return (n * n * n + 5 * n + 6) / 6;
    }

    // Driver Code
    public static void main (String[] args)
    {
        // For 2nd cake Number
        int n = 2;
        System.out.println( number_cake(n));

        // For 8th cake Number
        n = 8;
        System.out.println( number_cake(n));

        // For 25th cake Number
        n = 25;
        System.out.println( number_cake(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to find
# nth Cake number

# Function to calculate
# Cake number
def number_cake(n):

    # Formula to calculate nth
    # Cake number

    return (n * n * n + 5 * n + 6) // 6

# Driver Code
n = 2
print(number_cake(n))

n = 8
print(number_cake(n))

n = 25
print(number_cake(n))

# This code is contributed by aj_36                
```

## C#

```
// C# Program to find the nth Cake number
using System;

class GFG {

    // function for Cake number
    static int number_cake(int n)
    {

        // formula for find Cake number
        // nth term
        return (n * n * n + 5 * n + 6) / 6;
    }

    // Driver Code
    public static void Main ()
    {
        // For 2nd cake Number
        int n = 2;
        Console.WriteLine( number_cake(n));

        // For 8th cake Number
        n = 8;
        Console.WriteLine( number_cake(n));

        // For 25th cake Number
        n = 25;
        Console.WriteLine( number_cake(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// nth Cake number

// function for Cake number
function number_cake( $n)
{
    // formula for find Cake
    // number nth term
    return ($n * $n * $n +
             5 * $n + 6) / 6;
}

// Driver Code

// For 2nd cake Number
$n = 2;
echo number_cake($n) ,"\n";

// For 8th cake Number
$n = 8;
echo number_cake($n)," \n";
// For 25th cake Number
$n = 25;
echo number_cake($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find the nth Cake number

    // function for Cake number
    function number_cake(n)
    {

        // formula for find Cake number
        // nth term
        return parseInt((n * n * n + 5 * n + 6) / 6, 10);
    }

    // For 2nd cake Number
    let n = 2;
    document.write( number_cake(n) + "</br>");

    // For 8th cake Number
    n = 8;
    document.write( number_cake(n) + "</br>");

    // For 25th cake Number
    n = 25;
    document.write( number_cake(n));

</script>
```

**输出:**

```
4
93
2626
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)