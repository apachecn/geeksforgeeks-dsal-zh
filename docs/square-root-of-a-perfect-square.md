# 求平方根的巴比伦方法

> 原文:[https://www . geesforgeks . org/完美平方的平方根/](https://www.geeksforgeeks.org/square-root-of-a-perfect-square/)

**算法:**
这种方法可以从(但早于)牛顿-拉夫森方法推导出来。

```
1 Start with an arbitrary positive start value x (the closer to the 
   root, the better).
2 Initialize y = 1.
3\. Do following until desired approximation is achieved.
  a) Get the next approximation for root using average of x and y
  b) Set y = n/x
```

**执行:**

## C++

```
#include <iostream>
using namespace std;
class gfg {
    /*Returns the square root of n. Note that the function */
public:
    float squareRoot(float n)
    {
        /*We are using n itself as initial approximation
          This can definitely be improved */
        float x = n;
        float y = 1;
        float e = 0.000001; /* e decides the accuracy level*/
        while (x - y > e) {
            x = (x + y) / 2;
            y = n / x;
        }
        return x;
    }
};

/* Driver program to test above function*/
int main()
{
    gfg g;
    int n = 50;
    cout << "Square root of " << n << " is " << g.squareRoot(n);
    getchar();
}
```

## C

```
#include <stdio.h>

/*Returns the square root of n. Note that the function */
float squareRoot(float n)
{
    /*We are using n itself as initial approximation
   This can definitely be improved */
    float x = n;
    float y = 1;
    float e = 0.000001; /* e decides the accuracy level*/
    while (x - y > e) {
        x = (x + y) / 2;
        y = n / x;
    }
    return x;
}

/* Driver program to test above function*/
int main()
{
    int n = 50;
    printf("Square root of %d is %f", n, squareRoot(n));
    getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    /*Returns the square root of n.
    Note that the function */
    static float squareRoot(float n)
    {

        /*We are using n itself as
        initial approximation This
        can definitely be improved */
        float x = n;
        float y = 1;

        // e decides the accuracy level
        double e = 0.000001;
        while (x - y > e) {
            x = (x + y) / 2;
            y = n / x;
        }
        return x;
    }

    /* Driver program to test
    above function*/
    public static void main(String[] args)
    {
        int n = 50;

        System.out.printf("Square root of "
                          + n + " is " + squareRoot(n));
    }
}

// This code is contributed by
// Smitha DInesh Semwal
```

## 蟒蛇 3

```
# Returns the square root of n.
# Note that the function
def squareRoot(n):

    # We are using n itself as
    # initial approximation This
    # can definitely be improved
        x = n
        y = 1

        # e decides the accuracy level
        e = 0.000001
        while(x - y > e):

            x = (x + y)/2
            y = n / x

        return x

# Driver program to test
# above function
n = 50

print("Square root of", n, "is",
              round(squareRoot(n), 6))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program for Babylonian
// method of square root
using System;

class GFG {

    // Returns the square root of n.
    // Note that the function
    static float squareRoot(float n)
    {

        // We are using n itself as
        // initial approximation This
        // can definitely be improved
        float x = n;
        float y = 1;

        // e decides the
        // accuracy level
        double e = 0.000001;
        while (x - y > e) {
            x = (x + y) / 2;
            y = n / x;
        }
        return x;
    }

    // Driver Code
    public static void Main()
    {
        int n = 50;
        Console.Write("Square root of "
                      + n + " is " + squareRoot(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Returns the square root of n.
// Note that the function
function squareRoot($n)
{

    // We are using n itself
    // as initial approximation
    // This can definitely be
    // improved
    $x = $n;
    $y = 1;

    /* e decides the
       accuracy level */
    $e = 0.000001;
    while($x - $y > $e)
    {
        $x = ($x + $y)/2;
        $y = $n / $x;
    }
    return $x;
}

// Driver Code
{
    $n = 50;
    echo "Square root of $n is ", squareRoot($n);
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript Program to find the area
// of triangle

/*Returns the square root of n. Note that the function */
function squareRoot( n)
{

    /*We are using n itself as initial approximation
   This can definitely be improved */
    let x = n;
    let y = 1;
    let e = 0.000001; /* e decides the accuracy level*/
    while (x - y > e) {
        x = (x + y) / 2;
        y = n / x;
    }
    return x;
}

/* Driver program to test above function*/

    let n = 50;
  document.write( "Square root of "+n+" is " + squareRoot(n).toFixed(6));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Square root of 50 is 7.071068
```

时间复杂度:O(n <sup>1/2</sup> )

辅助空间:O(1)
**例:**

```
n = 4 /*n itself is used for initial approximation*/
Initialize x = 4, y = 1
Next Approximation x = (x + y)/2 (= 2.500000), 
y = n/x  (=1.600000)
Next Approximation x = 2.050000,
y = 1.951220
Next Approximation x = 2.000610,
y = 1.999390
Next Approximation x = 2.000000, 
y = 2.000000
Terminate as (x - y) > e now.
```

如果我们确定 n 是一个完美的正方形，那么我们可以使用下面的方法。该方法可以对非完美平方数进行无限循环。例如，对于 3，下面的 while 循环永远不会终止。

## C++

```
// C++ program for Babylonian
// method for square root
#include <iostream>
using namespace std;

class gfg {

    /* Returns the square root of
   n. Note that the function
   will not work for numbers
   which are not perfect
   squares*/
public:
    float squareRoot(float n)
    {
        /* We are using n itself as an initial
          approximation.  This can definitely be
          improved */
        float x = n;
        float y = 1;

        while (x > y) {
            x = (x + y) / 2;
            y = n / x;
        }
        return x;
    }
};

/* Driver code*/
int main()
{
    gfg g;
    int n = 49;
    cout << "Square root of " << n << " is " << g.squareRoot(n);
    getchar();
}

// This code is edited by Dark_Dante_
```

## C

```
// C program for Babylonian
// method for square root
#include <stdio.h>

/* Returns the square root of
   n. Note that the function
   will not work for numbers
   which are not perfect
   squares*/
unsigned int squareRoot(int n)
{
    int x = n;
    int y = 1;
    while (x > y) {
        x = (x + y) / 2;
        y = n / x;
    }
    return x;
}

// Driver Code
int main()
{
    int n = 49;
    printf("root of %d is %d", n, squareRoot(n));
    getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Babylonian
// method for square root
import java.io.*;

public class GFG {

    /* Returns the square root of
    n. Note that the function
    will not work for numbers
    which are not perfect
    squares*/
    static long squareRoot(int n)
    {
        int x = n;
        int y = 1;
        while (x > y) {
            x = (x + y) / 2;
            y = n / x;
        }
        return (long)x;
    }

    // Driver Code
    static public void main(String[] args)
    {
        int n = 49;
        System.out.println("root of "
                           + n + " is " + squareRoot(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# python3 program for Babylonian
# method for square root

# Returns the square root of n.
# Note that the function
# will not work for numbers
# which are not perfect squares

def squareRoot(n):
    x = n;
    y = 1;
    while(x > y):
        x = (x + y) / 2;
        y = n / x;
    return x;

# Driver Code
n = 49;
print("root of", n, "is", squareRoot(n));

# This code is contributed by mits.
```

## C#

```
// C# program for Babylonian
// method for square root

using System;

public class GFG {

    /* Returns the square root of
    n. Note that the function
    will not work for numbers
    which are not perfect
    squares*/
    static uint squareRoot(int n)
    {
        int x = n;
        int y = 1;
        while (x > y) {
            x = (x + y) / 2;
            y = n / x;
        }
        return (uint)x;
    }

    // Driver Code
    static public void Main()
    {
        int n = 49;
        Console.WriteLine("root of "
                          + n + " is " + squareRoot(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Babylonian
// method for square root

/* Returns the square root of
   n. Note that the function
   will not work for numbers
   which are not perfect
   squares */
function squareRoot( $n)
{
    $x = $n;
    $y = 1;
    while($x > $y)
    {
        $x = ($x + $y) / 2;
        $y =$n / $x;
    }
    return $x;
}

// Driver Code
$n = 49;
echo " root of ", $n, " is ", squareRoot($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program for Babylonian
// method for square root

    /*
     * Returns the square root of n. Note that the function will not work for
     * numbers which are not perfect squares
     */
    function squareRoot(n) {
        var x = n;
        var y = 1;
        while (x > y) {
            x = (x + y) / 2;
            y = n / x;
        }
        return  x;
    }

    // Driver Code
        var n = 49;
        document.write("root of " + n + " is " + squareRoot(n));

// This code contributed by shikhasingrajput
</script>
```

**输出:**

```
 root of 49 is 7
```

***时间复杂度:** O(n <sup>1/2</sup> )*

***辅助空间:**O(1)*
T5【参考文献；
[http://en.wikipedia.org/wiki/Square_root](http://en.wikipedia.org/wiki/Square_root)
[http://en . Wikipedia . org/wiki/babylan _ method # babylan _ method](http://en.wikipedia.org/wiki/Babylonian_method#Babylonian_method)
由 Snehal 提问
如发现以上程序/算法有 bug，或想分享更多关于 Babylonian method 的信息，请写评论。