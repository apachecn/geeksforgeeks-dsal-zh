# 给定奇数之前奇数的平均值

> 原文:[https://www . geeksforgeeks . org/average-奇数-to-given-奇数/](https://www.geeksforgeeks.org/average-odd-numbers-till-given-odd-number/)

给定一个奇数 n，求从 1 到 n 的奇数平均值
例:

```
Input : n = 9
Output : 5
Explanation
(1 + 3 + 5 + 7 + 9)/5 
= 25/5 
= 5

Input : n = 221
Output : 111
```

**方法 1** 我们可以通过将每个奇数相加到 n，然后将总和除以计数来计算平均值。
以下是实施办法。

## C++

```
// Program to find average of odd numbers
// till a given odd number.
#include <stdio.h>

// Function to calculate the average
// of odd numbers
int averageOdd(int n)
{
    if (n % 2 == 0) {
        printf("Invalid Input");
        return -1;
    }

    int sum = 0, count = 0;
    while (n >= 1) {

        // count odd numbers
        count++;

        // store the sum of odd numbers
        sum += n;

        n = n - 2;
    }
    return sum / count;
}

// driver function
int main()
{
    int n = 15;
    printf("%d", averageOdd(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find average of odd numbers
// till a given odd number.
import java.io.*;

class GFG {

    // Function to calculate the average
    // of odd numbers
    static int averageOdd(int n)
    {
        if (n % 2 == 0) {
            System.out.println("Invalid Input");
            return -1;
        }

        int sum = 0, count = 0;
        while (n >= 1) {

            // count odd numbers
            count++;

            // store the sum of odd numbers
            sum += n;

            n = n - 2;
        }
        return sum / count;
    }

    // driver function
    public static void main(String args[])
    {
        int n = 15;
        System.out.println(averageOdd(n));
    }
}

/*This code is contributed by Nikita tiwari.*/
```

## 蟒蛇 3

```
# Program to find average
# of odd numbers till a
# given odd number.

# Function to calculate
# the average of odd
# numbers
def averageOdd(n) :

    if (n % 2 == 0) :
        print("Invalid Input")
        return -1

    sm = 0
    count = 0

    while (n >= 1) :

        # count odd numbers
        count = count + 1

        # store the sum of
        # odd numbers
        sm = sm + n

        n = n - 2

    return sm // count

# Driver function
n = 15
print(averageOdd(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find average 
// of odd numbers till a given
// odd number.
using System;

class GFG {

    // Function to calculate the
    // average of odd numbers
    static int averageOdd(int n)
    {
        if (n % 2 == 0) {
            Console.Write("Invalid Input");
            return -1;
        }

        int sum = 0, count = 0;
        while (n >= 1) {

            // count odd numbers
            count++;

            // store the sum of odd numbers
            sum += n;

            n = n - 2;
        }
        return sum / count;
    }

    // driver function
    public static void Main()
    {
        int n = 15;
        Console.Write(averageOdd(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find average of odd
// numbers till a given odd number.

// Function to calculate the
// average of odd numbers
function averageOdd($n)
{
    if ($n % 2 == 0)
    {
        echo("Invalid Input");
        return -1;
    }

    $sum = 0;
    $count = 0;
    while ($n >= 1)
    {

        // count odd numbers
        $count++;

        // store the sum of
        // odd numbers
        $sum += $n;

        $n = $n - 2;
    }
    return $sum / $count;
}

    // Driver Code
    $n = 15;
    echo(averageOdd($n));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// Javascript Program to find average of odd numbers
// till a given odd number.

    // Function to calculate the average
    // of odd numbers
    function averageOdd( n)
    {
        if (n % 2 == 0)
        {
            document.write("Invalid Input");
            return -1;
        }

        let sum = 0, count = 0;
        while (n >= 1) {

            // count odd numbers
            count++;

            // store the sum of odd numbers
            sum += n;
            n = n - 2;
        }
        return sum / count;
    }

    // driver function
    let n = 15;
    document.write(averageOdd(n));

// This code is contributed by gauravrajput1
</script>
```

输出:

```
8
```

**方法二**
奇数的平均值只能通过单步
求出，使用以下公式
**【n+1】/2**
其中 n 是最后一个奇数。
**这个公式是怎么用的？**

```
We know there are (n+1)/2 odd numbers till n.  

For example:
There are two odd numbers till 3 and there are
three odd numbers till 5.

Sum of first k odd numbers is k*k 

Sum of odd numbers till n is ((n+1)/2)2

Average of odd numbers till n is (n + 1)/2
```

下面是该方法的实现。

## C

```
// Program to find average of odd numbers
// till a given odd number.
#include <stdio.h>

// Function to calculate the average
// of odd numbers
int averageOdd(int n)
{
    if (n % 2 == 0) {
        printf("Invalid Input");
        return -1;
    }

    return (n + 1) / 2;
}

// driver function
int main()
{
    int n = 15;
    printf("%d", averageOdd(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find average of odd
// numbers till a given odd number.
import java.io.*;

class GFG
{
    // Function to calculate the
    // average of odd numbers
    static int averageOdd(int n)
    {
        if (n % 2 == 0)
        {
            System.out.println("Invalid Input");
            return -1;
        }

        return (n + 1) / 2;
    }

    // driver function
    public static void main(String args[])
    {
        int n = 15;
        System.out.println(averageOdd(n));
    }
}

// This code is contributed by Nikita tiwari.
```

## 蟒蛇 3

```
# Program to find average of odd
# numbers till a given odd number.

# Function to calculate the
# average of odd numbers
def averageOdd(n) :
    if (n % 2 == 0) :
        print("Invalid Input")
        return -1

    return (n + 1) // 2

# driver function
n = 15
print(averageOdd(n))

# This code is contributed by Nikita tiwari.
```

## C#

```
// C# Program to find average
// of odd numbers till a given
// odd number.
using System;

class GFG
{
    // Function to calculate the
    // average of odd numbers
    static int averageOdd(int n)
    {
        if (n % 2 == 0)
        {
            Console.Write("Invalid Input");
            return -1;
        }

        return (n + 1) / 2;
    }

    // driver function
    public static void Main()
    {
        int n = 15;
        Console.Write(averageOdd(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find average of odd
// numbers till a given odd number.

// Function to calculate the
// average of odd numbers
function averageOdd( $n)
{
    if ($n % 2 == 0)
    {
        echo("Invalid Input");
        return -1;
    }

    return ($n + 1) / 2;
}

    // Driver Code
    $n = 15;
    echo(averageOdd($n));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// javascript Program to find average of odd numbers
// till a given odd number.

// Function to calculate the average
// of odd numbers
function averageOdd( n)
{
    if (n % 2 == 0) {
        document.write("Invalid Input");
        return -1;
    }

    return (n + 1) / 2;
}

// driver function
    let n = 15;
    document.write( averageOdd(n));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
8
```