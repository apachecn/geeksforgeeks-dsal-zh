# 不使用*、/和幂()计算一个数的平方

> 原文:[https://www . geeksforgeeks . org/不使用 and-power 计算数字平方/](https://www.geeksforgeeks.org/calculate-square-of-a-number-without-using-and-pow/)

给定一个整数 n，在不使用*、/和幂()的情况下计算一个数的平方。

**示例:**

```
Input: n = 5
Output: 25

Input: 7
Output: 49

Input: n = 12
Output: 144
```

一个**简单的解决方法**就是在结果上反复加 n。

下面是这个想法的实现。

## C++

```
// Simple solution to calculate square without
// using * and pow()
#include <iostream>
using namespace std;

int square(int n)
{
    // handle negative input
    if (n < 0)
        n = -n;

    // Initialize result
    int res = n;

    // Add n to res n-1 times
    for (int i = 1; i < n; i++)
        res += n;

    return res;
}

// Driver code
int main()
{
    for (int n = 1; n <= 5; n++)
        cout << "n = " << n << ", n^2 = " << square(n)
             << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Simple solution to calculate
// square without using * and pow()
import java.io.*;

class GFG {

    public static int square(int n)
    {

        // handle negative input
        if (n < 0)
            n = -n;

        // Initialize result
        int res = n;

        // Add n to res n-1 times
        for (int i = 1; i < n; i++)
            res += n;

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        for (int n = 1; n <= 5; n++)
            System.out.println("n = " + n
                               + ", n^2 = " + square(n));
    }
}

// This code is contributed by sunnysingh
```

## 蟒蛇 3

```
# Simple solution to
# calculate square without
# using * and pow()

def square(n):

    # handle negative input
    if (n < 0):
        n = -n

    # Initialize result
    res = n

    # Add n to res n-1 times
    for i in range(1, n):
        res += n

    return res

# Driver Code
for n in range(1, 6):
    print("n =", n, end=", ")
    print("n^2 =", square(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Simple solution to calculate
// square without using * and pow()
using System;

class GFG {
    public static int square(int n)
    {

        // handle negative input
        if (n < 0)
            n = -n;

        // Initialize result
        int res = n;

        // Add n to res n-1 times
        for (int i = 1; i < n; i++)
            res += n;

        return res;
    }

    // Driver code
    public static void Main()
    {

        for (int n = 1; n <= 5; n++)
            Console.WriteLine("n = " + n
                              + ", n^2 = " + square(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// calculate square
// without using * and pow()

function square($n)
{

// handle negative input
    if ($n < 0) $n = -$n;

// Initialize result
        $res = $n;

// Add n to res n-1 times
for ($i = 1; $i < $n; $i++)
    $res += $n;

return $res;
}

// Driver Code
for ($n = 1; $n<=5; $n++)
    echo "n = ", $n, ", ", "n^2 = ",
                  square($n), "\n ";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Simple solution to calculate square without
// using * and pow()

function square(n)
{
    // handle negative input
    if (n < 0)
        n = -n;

    // Initialize result
    let res = n;

    // Add n to res n-1 times
    for (let i = 1; i < n; i++)
        res += n;

    return res;
}

// Driver code

    for (let n = 1; n <= 5; n++)
        document.write("n= " + n +", n^2 = " + square(n)
            + "<br>");

//This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
n = 1, n^2 = 1
n = 2, n^2 = 4
n = 3, n^2 = 9
n = 4, n^2 = 16
n = 5, n^2 = 25
```

上述解的时间复杂度为 O(n)。

**方法 2:**

我们可以使用按位运算符在 **O(Logn)时间内完成。这个想法基于以下事实。**

```
  square(n) = 0 if n == 0
  if n is even 
     square(n) = 4*square(n/2) 
  if n is odd
     square(n) = 4*square(floor(n/2)) + 4*floor(n/2) + 1 

Examples
  square(6) = 4*square(3)
  square(3) = 4*(square(1)) + 4*1 + 1 = 9
  square(7) = 4*square(3) + 4*3 + 1 = 4*9 + 4*3 + 1 = 49
```

**这是如何工作的？**

```
If n is even, it can be written as
  n = 2*x 
  n2 = (2*x)2 = 4*x2
If n is odd, it can be written as 
  n = 2*x + 1
  n2 = (2*x + 1)2 = 4*x2 + 4*x + 1
```

floor(n/2)可以使用按位右移运算符来计算。可以计算 2*x 和 4*x

下面是基于上述思想的实现。

## C++

```
// Square of a number using bitwise operators
#include <bits/stdc++.h>
using namespace std;

int square(int n)
{
    // Base case
    if (n == 0)
        return 0;

    // Handle negative number
    if (n < 0)
        n = -n;

    // Get floor(n/2) using right shift
    int x = n >> 1;

    // If n is odd
    if (n & 1)
        return ((square(x) << 2) + (x << 2) + 1);
    else // If n is even
        return (square(x) << 2);
}

// Driver Code
int main()
{
    // Function calls
    for (int n = 1; n <= 5; n++)
        cout << "n = " << n << ", n^2 = " << square(n)
             << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Square of a number using
// bitwise operators
class GFG {
    static int square(int n)
    {

        // Base case
        if (n == 0)
            return 0;

        // Handle negative number
        if (n < 0)
            n = -n;

        // Get floor(n/2) using
        // right shift
        int x = n >> 1;

        // If n is odd
        ;
        if (n % 2 != 0)
            return ((square(x) << 2) + (x << 2) + 1);
        else // If n is even
            return (square(x) << 2);
    }

    // Driver code
    public static void main(String args[])
    {
        // Function calls
        for (int n = 1; n <= 5; n++)
            System.out.println("n = " + n
                               + " n^2 = " + square(n));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Square of a number using bitwise
# operators

def square(n):

    # Base case
    if (n == 0):
        return 0

    # Handle negative number
    if (n < 0):
        n = -n

    # Get floor(n/2) using
    # right shift
    x = n >> 1

    # If n is odd
    if (n & 1):
        return ((square(x) << 2)
                + (x << 2) + 1)

    # If n is even
    else:
        return (square(x) << 2)

# Driver Code
for n in range(1, 6):
    print("n = ", n, " n^2 = ",
          square(n))
# This code is contributed by Sam007
```

## C#

```
// Square of a number using bitwise
// operators
using System;

class GFG {

    static int square(int n)
    {

        // Base case
        if (n == 0)
            return 0;

        // Handle negative number
        if (n < 0)
            n = -n;

        // Get floor(n/2) using
        // right shift
        int x = n >> 1;

        // If n is odd
        ;
        if (n % 2 != 0)
            return ((square(x) << 2) + (x << 2) + 1);
        else // If n is even
            return (square(x) << 2);
    }

    // Driver code
    static void Main()
    {
        for (int n = 1; n <= 5; n++)
            Console.WriteLine("n = " + n
                              + " n^2 = " + square(n));
    }
}

// This code is contributed by Sam0007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Square of a number using
// bitwise operators

function square($n)
{

    // Base case
    if ($n==0) return 0;

    // Handle negative number
    if ($n < 0) $n = -$n;

    // Get floor(n/2)
    // using right shift
    $x = $n >> 1;

    // If n is odd
    if ($n & 1)
        return ((square($x) << 2) +
                    ($x << 2) + 1);
    else // If n is even
        return (square($x) << 2);
}

    // Driver Code
    for ($n = 1; $n <= 5; $n++)
        echo "n = ", $n, ", n^2 = ", square($n),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Square of a number using bitwise operators

function square(n)
{
    // Base case
    if (n == 0)
        return 0;

    // Handle negative number
    if (n < 0)
        n = -n;

    // Get floor(n/2) using right shift
    let x = n >> 1;

    // If n is odd
    if (n & 1)
        return ((square(x) << 2) + (x << 2) + 1);
    else // If n is even
        return (square(x) << 2);
}

// Driver Code
  // Function calls
    for (let n = 1; n <= 5; n++)
        document.write("n = " + n + ", n^2 = " + square(n)
             +"<br>");

//This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
n = 1, n^2 = 1
n = 2, n^2 = 4
n = 3, n^2 = 9
n = 4, n^2 = 16
n = 5, n^2 = 25
```

上述解的时间复杂度为 O(Logn)。

**进场 3:**

```
For a given number `num` we get square of it by multiplying number as `num * num`. 
Now write one of `num` in square `num * num` in terms of power of `2`. Check below examples.

Eg: num = 10, square(num) = 10 * 10 
                          = 10 * (8 + 2) = (10 * 8) + (10 * 2)
    num = 15, square(num) = 15 * 15 
                          = 15 * (8 + 4 + 2 + 1) = (15 * 8) + (15 * 4) + (15 * 2) + (15 * 1)

Multiplication with power of 2's can be done by left shift bitwise operator.
```

下面是基于上述思想的实现。

## C++

```
// Simple solution to calculate square without
// using * and pow()
#include <iostream>
using namespace std;

int square(int num)
{
    // handle negative input
    if (num < 0) num = -num;

    // Initialize result
    int result = 0, times = num;

    while (times > 0)
    {
        int possibleShifts = 0, currTimes = 1;

        while ((currTimes << 1) <= times)
        {
            currTimes = currTimes << 1;
            ++possibleShifts;
        }

        result = result + (num << possibleShifts);
        times = times - currTimes;
    }

    return result;
}

// Driver code
int main()
{
    // Function calls
    for (int n = 10; n <= 15; ++n)
        cout << "n = " << n << ", n^2 = " << square(n) << endl;
    return 0;
}

// This code is contributed by sanjay235
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple solution to calculate square
// without using * and pow()
import java.io.*;

class GFG{

public static int square(int num)
{

    // Handle negative input
    if (num < 0)
        num = -num;

    // Initialize result
    int result = 0, times = num;

    while (times > 0)
    {
        int possibleShifts = 0,
                 currTimes = 1;

        while ((currTimes << 1) <= times)
        {
            currTimes = currTimes << 1;
            ++possibleShifts;
        }

        result = result + (num << possibleShifts);
        times = times - currTimes;
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    for(int n = 10; n <= 15; ++n)
    {
        System.out.println("n = " + n +
                           ", n^2 = " +
                           square(n));
    }
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Simple solution to calculate square without
# using * and pow()
def square(num):

    # Handle negative input
    if (num < 0):
        num = -num

    # Initialize result
    result, times = 0, num

    while (times > 0):
        possibleShifts, currTimes = 0, 1

        while ((currTimes << 1) <= times):
            currTimes = currTimes << 1
            possibleShifts += 1

        result = result + (num << possibleShifts)
        times = times - currTimes

    return result

# Driver Code

# Function calls
for n in range(10, 16):
    print("n =", n, ", n^2 =", square(n))

# This code is contributed by divyesh072019
```

## C#

```
// Simple solution to calculate square
// without using * and pow()
using System;
class GFG {

    static int square(int num)
    {

        // Handle negative input
        if (num < 0)
            num = -num;

        // Initialize result
        int result = 0, times = num;

        while (times > 0)
        {
            int possibleShifts = 0,
                     currTimes = 1;

            while ((currTimes << 1) <= times)
            {
                currTimes = currTimes << 1;
                ++possibleShifts;
            }

            result = result + (num << possibleShifts);
            times = times - currTimes;
        }
        return result;
    }

  static void Main() {
        for(int n = 10; n <= 15; ++n)
        {
            Console.WriteLine("n = " + n +
                               ", n^2 = " +
                               square(n));
        }
  }
}

// This code is contributed by divyeshrabadiy07
```

## java 描述语言

```
<script>

// Simple solution to calculate square without
// using * and pow()

function square(num)
{
    // handle negative input
    if (num < 0) num = -num;

    // Initialize result
    let result = 0, times = num;

    while (times > 0)
    {
        let possibleShifts = 0, currTimes = 1;

        while ((currTimes << 1) <= times)
        {
            currTimes = currTimes << 1;
            ++possibleShifts;
        }

        result = result + (num << possibleShifts);
        times = times - currTimes;
    }

    return result;
}

// Driver code

    // Function calls
    for (let n = 10; n <= 15; ++n)
        document.write("n = " + n + ", n^2 = " + square(n) + "<br>");

//This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
n = 10, n^2 = 100
n = 11, n^2 = 121
n = 12, n^2 = 144
n = 13, n^2 = 169
n = 14, n^2 = 196
n = 15, n^2 = 225
```

上述解决方案的时间复杂度为 O(Log n)。感谢[桑杰](https://github.com/sanjay235)的进场 3 方案。

本文由 **Ujjwal Jain** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息