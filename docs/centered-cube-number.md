# 居中立方体编号

> 原文:[https://www.geeksforgeeks.org/centered-cube-number/](https://www.geeksforgeeks.org/centered-cube-number/)

给定一个数 n，求第 n 个**中心立方体数。
**中心立方体编号**计算由第 I 层的正方形面上的 i <sup>2</sup> 点在 3D 中被同心立方体层包围的点形成的点数。来源[【WIKI】](https://en.wikipedia.org/wiki/Centered_cube_number)。请参见[这张](https://en.wikipedia.org/wiki/Centered_cube_number#/media/File:Body_centered_cubic_35_balls.svg)图，看得更清楚。
前几个居中的立方体编号是:
1、9、35、91、189、341、559、855、1241、172…………………………
**示例:**** 

```
Input :  n = 1
Output : 9

Input  : n = 7
Output : 855
```

****第 n 个**中心立方数的数学公式由:
给出**

```
n-th Centered Cube Number = (2n + 1)(n<sup>2</sup> + n + 1)
```

**下面是上述公式的基本实现:** 

## **C++**

```
// Program to find nth Centered cube
// number
#include <bits/stdc++.h>
using namespace std;

// Function to find
// Centered cube number
int centered_cube(int n)
{
    // Formula to calculate nth
    // Centered cube number &
    // return it into main function.
    return (2 * n + 1) * ( n * n + n + 1);
}

// Driver Code
int main()
{
    int n = 3;
    cout << n << "th Centered cube number: ";
    cout << centered_cube(n);
    cout << endl;

    n = 10;
    cout << n << "th Centered cube number: ";
    cout << centered_cube(n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to find nth Centered
// cube number
import java.io.*;

class GFG {

    // Function to find
    // Centered cube number
    static int centered_cube(int n)
    {
        // Formula to calculate nth
        // Centered cube number &
        // return it into main function.
        return (2 * n + 1) * ( n * n + n + 1);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;
        System.out.print (n + "th Centered"
                         + " cube number: ");
        System.out.println (centered_cube(n));

        n = 10;
        System.out.print ( n + "th Centered"
                         + " cube number: ");
        System.out.println (centered_cube(n));
    }
}

// This code is contributed by m_kit.
```

## **蟒蛇 3**

```
# Python 3 Program to find
# nth Centered cube number

# Centered cube
# number function
def centered_cube(n) :

    # Formula to calculate
    # nth Centered cube
    # number return it
    # into main function.
    return (2 * n + 1) * (
                n * n + n + 1)

# Driver Code
if __name__ == '__main__' :

    n = 3
    print(n,"th Centered cube " +
                    "number : " ,
                centered_cube(n))

    n = 10
    print(n,"th Centered cube " +
                    "number : " ,
                centered_cube(n))

# This code is contributed by ajit
```

## **C#**

```
// C# Program to find nth
// Centered cube number
using System;

class GFG
{

    // Function to find
    // Centered cube number
    static int centered_cube(int n)
    {
        // Formula to calculate
        // nth Centered cube
        // number & return it
        // into main function.
        return (2 * n + 1) *
               (n * n + n + 1);
    }

    // Driver code
    static public void Main ()
    {
        int n = 3;
        Console.Write(n + "th Centered" +
                       " cube number: ");
    Console.WriteLine (centered_cube(n));

        n = 10;
        Console.Write( n + "th Centered" +
                        " cube number: ");
        Console.WriteLine(centered_cube(n));
    }
}

// This code is contributed by aj_36
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// Program to find nth
// Centered cube number

// Function to find
// Centered cube number
function centered_cube($n)
{
    // Formula to calculate nth
    // Centered cube number &
    // return it into main function.
    return (2 * $n + 1) *
           ($n * $n + $n + 1);
}

// Driver Code
$n = 3;
echo $n , "th Centered cube number: ";
echo centered_cube($n);
echo "\n";

$n = 10;
echo $n , "th Centered cube number: ";
echo centered_cube($n);

// This code is contributed by m_kit
?>
```

## **java 描述语言**

```
<script>
// Program to find nth Centered cube
// number

// Function to find
// Centered cube number
function centered_cube(n)
{
    // Formula to calculate nth
    // Centered cube number &
    // return it into main function.
    return (2 * n + 1) * ( n * n + n + 1);
}

// Driver Code
let n = 3;
document.write(n + "th Centered cube number: ");
document.write(centered_cube(n));
document.write("<br>");

n = 10;
document.write(n + "th Centered cube number: ");
document.write(centered_cube(n));

// This code is contributed by rishavmahato348.
</script>
```

****输出:**** 

```
 3th Centered cube number: 91
 10th Centered cube number: 2331
```

****时间复杂度:**O(1)
T3】辅助空间: O(1)**