# 给定偶数之前偶数的平均值

> 原文:[https://www . geesforgeks . org/average-偶数-to-给定偶数/](https://www.geeksforgeeks.org/average-even-numbers-till-given-even-number/)

给定一个偶数 n，求从 1 到 n 的偶数的平均值。
例:

```
Input : 10
Output : 6
Explanation:
(2 + 4 + 6 + 8 + 10 )/5
= 30/5
= 6 

Input : 100
Output : 51
```

**方法 1**
我们可以通过将每个偶数加到 n，然后用计数除和来计算平均值。

## C++

```
// Program to find average of even numbers
// till a given even number.
#include <stdio.h>

// Function to calculate the average
// of even numbers
int averageEven(int n)
{
    if (n % 2 != 0) {
        printf("Invalid Input");
        return -1;
    }

    int sum = 0, count = 0;
    while (n >= 2) {

        // count even numbers
        count++;

        // store the sum of even numbers
        sum += n;

        n = n - 2;
    }
    return sum / count;
}

// driver function
int main()
{
    int n = 16;
    printf("%d", averageEven(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find average of even numbers
// till a given even number.
import java.io.*;

class GFG {

    // Function to calculate the average
    // of even numbers
    static int averageEven(int n)
    {
        if (n % 2 != 0) {
        System.out.println("Invalid Input");
            return -1;
        }

        int sum = 0, count = 0;
        while (n >= 2) {

         // count even numbers
         count++;

         // store the sum of even numbers
         sum += n;

         n = n - 2;
        }
        return sum / count;
    }

    // driver function
    public static void main(String args[])
    {
        int n = 16;
        System.out.println(averageEven(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Program to find average of
# even numbers till a given
# even number.

# Function to calculate the
# average of even numbers
def averageEven(n) :

    if (n % 2 != 0) :
        print("Invalid Input")
        return -1

    sm = 0
    count = 0

    while (n >= 2) :

        # count even numbers
        count = count + 1

        # store the sum of even
        # numbers
        sm = sm + n

        n = n - 2

    return sm // count

# driver function
n = 16
print(averageEven(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find average
// of even numbers till a
// given even number.
using System;

class GFG {

    // Function to calculate the
    // average of even numbers
    static int averageEven(int n)
    {
        if (n % 2 != 0) {
        Console.Write("Invalid Input");
            return -1;
        }

        int sum = 0, count = 0;
        while (n >= 2) {

        // count even numbers
        count++;

        // store the sum of even numbers
        sum += n;

        n = n - 2;
        }
        return sum / count;
    }

    // driver function
    public static void Main()
    {
        int n = 16;
        Console.Write(averageEven(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find average of even
// numbers till a given even number.

// Function to calculate the
// average of even numbers
function averageEven( $n)
{
    if ($n % 2 != 0)
    {
        echo("Invalid Input");
        return -1;
    }

    $sum = 0;
    $count = 0;
    while ($n >= 2)
    {

        // count even numbers
        $count++;

        // store the sum of
        // even numbers
        $sum += $n;

        $n = $n - 2;
    }
    return $sum / $count;
}

    // Driver Code
    $n = 16;
    echo(averageEven($n));

//This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// javascript Program to find average of even numbers
// till a given even number.

// Function to calculate the average
// of even numbers
function averageEven( n)
{
    if (n % 2 != 0) {
        document.write("Invalid Input");
        return -1;
    }

    let sum = 0, count = 0;
    while (n >= 2) {

        // count even numbers
        count++;

        // store the sum of even numbers
        sum += n;

        n = n - 2;
    }
    return sum / count;
}

// driver function
let n = 16;
    document.write( averageEven(n));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
9
```

**方法二**
偶数的平均数只能用单步
求，公式如下:-
**【n+2】/2 其中 n 是最后一个偶数。**
**这个公式是怎么用的？**
我们知道 n 之前有(n)/2 个偶数，比如 4 之前有两个偶数，6 之前有三个偶数。
[前 k 个偶数之和为 k * (k + 1)](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)
把 k = n/2，我们得到**前 n/2 个偶数之和**为 n/2(n/2 + 1)
**前 n/2 个偶数(或偶数直到 n) = (n + 2)/2** 

## C++

```
// Program to find average of even numbers
// till a given even nend number.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the average
// of even numbers
int averageEven(int n)
{
    if (n % 2 != 0) {
        cout<<"Invalid Input";
        return -1;
    }

    return (n + 2) / 2;
}

// driver function
int main()
{
    int n = 16;
    cout<<averageEven(n)<<endl;
    return 0;
}

// This code is contributed by noob2000.
```

## C

```
// Program to find average of even numbers
// till a given even number.
#include <stdio.h>

// Function to calculate the average
// of even numbers
int averageEven(int n)
{
    if (n % 2 != 0) {
        printf("Invalid Input");
        return -1;
    }

    return (n + 2) / 2;
}

// driver function
int main()
{
    int n = 16;
    printf("%d", averageEven(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find average of even numbers
// till a given even number.
import java.io.*;

class GFG {

    // Function to calculate the average
    // of even numbers
    static int averageEven(int n)
    {
        if (n % 2 != 0) {
        System.out.println("Invalid Input");
            return -1;
        }

        return (n + 2) / 2;
    }

    // driver function
    public static void main(String args[])
    {
        int n = 16;
        System.out.println(averageEven(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 program to find average of even
# numbers till a given even number.

# Function to calculate the
# average of even numbers
def averageEven(n) :
    if (n % 2 != 0) :
        print("Invalid Input")
        return -1

    return (n + 2) // 2

# Driver function
n = 16
print(averageEven(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find average
// of even numbers till a
// given even number.
using System;

class GFG {

    // Function to calculate the
    // average of even numbers
    static int averageEven(int n)
    {
        if (n % 2 != 0) {
        Console.Write("Invalid Input");
            return -1;
        }

        return (n + 2) / 2;
    }

    // driver function
    public static void Main()
    {
        int n = 16;
        Console.Write(averageEven(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find average of even
// numbers till a given even number.

// Function to calculate the average
// of even numbers
function averageEven( $n)
{
    if ($n % 2 != 0)
    {
        echo("Invalid Input");
        return -1;
    }

    return ($n + 2) / 2;
}

    // Driver Code
    $n = 16;
    echo (averageEven($n));
    return 0;

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript Program to find average of even numbers
// till a given even number.

// Function to calculate the average
// of even numbers
function averageEven( n)
{
    if (n % 2 != 0)
    {
        document.write("Invalid Input");
        return -1;
    }
    return (n + 2) / 2;
}

// driver function
    let n = 16;
     document.write(averageEven(n));

// This code is contributed by Rajput-Ji

</script>
```

输出:

```
9
```