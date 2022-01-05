# 在给定条件下，当 X 和 Y 发生变化时，找到最终的 X 和 Y

> 原文:[https://www . geeksforgeeks . org/find-the-final-x-and-y-当他们在给定条件下改变时/](https://www.geeksforgeeks.org/find-the-final-x-and-y-when-they-are-altering-under-given-condition/)

给定两个正整数 **X** 和 **Y** 的初始值，根据以下修改求 X 和 Y 的最终值:

> 1.如果 **X=0** 或 **Y=0** ，终止该过程。否则，转到步骤 2；
> 2。如果 **X > = 2*Y** ，则将 **X 的值改为 X–2 * Y**，重复步骤 1。否则，转到步骤 3；
> 3。如果 **Y > = 2*X** ，则将 **Y 的值赋给 Y–2 * X**，重复步骤 1。否则，结束这个过程。
> 约束:1 < =X，Y < =10^18

**例:**

```
Input: X=12, Y=5
Output: X=0, Y=1
Explanation: 
    Initially X = 12, Y = 5 
    --> X = 2, Y = 5 (as X = X-2*Y)
    --> X = 2, Y = 1 (as Y = Y-2*X) 
    --> X = 0, Y = 1 (as X = X-2*Y)
    --> Stop         (as X = 0)

Input: X=31, Y=12
Output: X=7, Y=12
Explanation: 
    Initially X = 31, Y = 12 
    --> X = 7, Y = 12 (as X = X-2*Y)
    --> Stop          (as (Y - 2*X) < 0)
```

**方法:**由于 x 和 y 的初始值可以高达 10^18.简单的暴力方法是行不通的。
如果我们仔细观察，问题陈述只不过是一种[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)，在这里我们将用模替换所有的减法。
**实施:**

## C++

```
// CPP tp implement above approach

#include <iostream>
using namespace std;

// Function to get final value of X and Y
void alter(long long int x, long long int y)
{
    // Following the sequence
    // but by replacing minus with modulo
    while (true) {

        // Step 1
        if (x == 0 || y == 0)
            break;

        // Step 2
        if (x >= 2 * y)
            x = x % (2 * y);

        // Step 3
        else if (y >= 2 * x)
            y = y % (2 * x);

        // Otherwise terminate
        else
            break;
    }

    cout << "X=" << x << ", "
         << "Y=" << y;
}

// Driver function
int main()
{

    // Get the initial X and Y values
    long long int x = 12, y = 5;

    // Find the result
    alter(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java tp implement above approach
import java.io.*;

class GFG
{

// Function to get final value of X and Y
static void alter(long x, long y)
{
    // Following the sequence but by
    // replacing minus with modulo
    while (true)
    {

        // Step 1
        if (x == 0 || y == 0)
            break;

        // Step 2
        if (x >= 2 * y)
            x = x % (2 * y);

        // Step 3
        else if (y >= 2 * x)
            y = y % (2 * x);

        // Otherwise terminate
        else
            break;
    }

    System.out.println("X = " + x + ", " +
                       "Y = " + y);
}

// Driver Code
public static void main (String[] args)
{
    // Get the initial X and Y values
    long x = 12, y = 5;

    // Find the result
    alter(x, y);
}
}

// This code is contributed by
// shk
```

## 蟒蛇 3

```
# Python3 tp implement above approach
import math as mt

# Function to get final value of X and Y
def alter(x, y):

    # Following the sequence but by
    # replacing minus with modulo
    while (True):

        # Step 1
        if (x == 0 or y == 0):
            break

        # Step 2
        if (x >= 2 * y):
            x = x % (2 * y)

        # Step 3
        elif (y >= 2 * x):
            y = y % (2 * x)

        # Otherwise terminate
        else:
            break

    print("X =", x, ", ", "Y =", y)

# Driver Code

# Get the initial X and Y values
x, y = 12, 5

# Find the result
alter(x, y)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to get final value of X and Y
    static void alter(long x, long y)
    {
    // Following the sequence but by
    // replacing minus with modulo
    while (true)
    {

        // Step 1
        if (x == 0 || y == 0)
            break;

        // Step 2
        if (x >= 2 * y)
            x = x % (2 * y);

        // Step 3
        else if (y >= 2 * x)
            y = y % (2 * x);

        // Otherwise terminate
        else
            break;
        }

        Console.WriteLine("X = " + x + ", " + "Y = " + y);
    }

    // Driver Code
    public static void Main ()
    {
        // Get the initial X and Y values
        long x = 12, y = 5;

        // Find the result
        alter(x, y);
    }
}

// This code is contributed by aishwarya.27
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to get final value of X and Y
function alter($x, $y)
{
    // Following the sequence but by
    // replacing minus with modulo
    while (true)
    {

        // Step 1
        if ($x == 0 || $y == 0)
            break;

        // Step 2
        if ($x >= 2 * $y)
            $x = $x % (2 * $y);

        // Step 3
        else if ($y >= 2 * $x)
            $y = $y % (2 * $x);

        // Otherwise terminate
        else
            break;
    }

    echo "X = ", $x, ", ", "Y = ", $y;
}

// Driver Code

// Get the initial X and Y values
$x = 12 ;
$y = 5 ;

// Find the result
alter($x, $y);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript to implement above approach

// Function to get final value of X and Y
function alter(x, y)
{

    // Following the sequence but by
    // replacing minus with modulo
    while (true)
    {

        // Step 1
        if (x == 0 || y == 0)
            break;

        // Step 2
        if (x >= 2 * y)
            x = x % (2 * y);

        // Step 3
        else if (y >= 2 * x)
            y = y % (2 * x);

        // Otherwise terminate
        else
            break;
    }

    document.write("X = " + x + ", " +
                   "Y = " + y);
}

// Driver Code

// Get the initial X and Y values
var x = 12, y = 5;

// Find the result
alter(x, y);

// This code is contributed by Kirti

</script>
```

**Output:** 

```
X=0, Y=1
```