# 摩擦编号

> 原文:[https://www.geeksforgeeks.org/tribonacci-numbers/](https://www.geeksforgeeks.org/tribonacci-numbers/)

[摩擦数列](http://mathworld.wolfram.com/TribonacciNumber.html)是斐波那契数列的推广，其中每个项都是前面三个项的和。
**特里博纳奇序列:**
0，0，1，1，2，4，7，13，24，44，81，149，274，504，927，1705，3136，5768，10609，19513，35890，66012，121415，223317，410744，755476，196012

```
a(n) = a(n-1) + a(n-2) + a(n-3) 
with 
a(0) = a(1) = 0, a(2) = 1\. 
```

给定值 N，任务是打印前 N 个摩擦数。
**例:**

```
Input : 5
Output : 0, 0, 1, 1, 2

Input : 10
Output : 0, 0, 1, 1, 2, 4, 7, 13, 24, 44

Input : 20
Output : 0, 0, 1, 1, 2, 4, 7, 13, 24, 44,
         81, 149, 274, 504, 927, 1705, 3136, 
          5768, 10609, 19513
```

一个**简单的解决方案**就是简单的遵循递归公式并为其编写递归代码，

## C++

```
// A simple recursive CPP program to print
// first n Tribonacci numbers.
#include <iostream>
using namespace std;

int printTribRec(int n)
{
    if (n == 0 || n == 1 || n == 2)
        return 0;

    if (n == 3)
        return 1;
    else
        return printTribRec(n - 1) +
               printTribRec(n - 2) +
               printTribRec(n - 3);
}

void printTrib(int n)
{
    for (int i = 1; i < n; i++)
        cout << printTribRec(i) << " ";
}

// Driver code
int main()
{
    int n = 10;
    printTrib(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple recursive CPP program
// first n Tribonacci numbers.
import java.io.*;

class GFG {

    // Recursion Function
    static int printTribRec(int n)
    {

        if (n == 0 || n == 1 || n == 2)
            return 0;

        if (n == 3)
            return 1;
        else
            return printTribRec(n - 1) +
                   printTribRec(n - 2) +
                   printTribRec(n - 3);
    }

    static void printTrib(int n)
    {
        for (int i = 1; i < n; i++)
            System.out.print(printTribRec(i)
                             +" ");
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;

        printTrib(n);
    }
}

// This code is contributed by Nikita tiwari.
```

## 计算机编程语言

```
# A simple recursive CPP program to print
# first n Tribonacci numbers.

def printTribRec(n) :
    if (n == 0 or n == 1 or n == 2) :
        return 0
    elif (n == 3) :
        return 1
    else :
        return (printTribRec(n - 1) +
                printTribRec(n - 2) +
                printTribRec(n - 3))

def printTrib(n) :
    for i in range(1, n) :
        print( printTribRec(i) , " ", end = "")

# Driver code
n = 10
printTrib(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A simple recursive C# program
// first n Tribinocci numbers.
using System;

class GFG {

    // Recursion Function
    static int printTribRec(int n)
    {

        if (n == 0 || n == 1 || n == 2)
            return 0;

        if (n == 3)
            return 1;
        else
            return printTribRec(n - 1) +
                   printTribRec(n - 2) +
                   printTribRec(n - 3);
    }

    static void printTrib(int n)
    {
        for (int i = 1; i < n; i++)
            Console.Write(printTribRec(i)
                                    +" ");
    }

    // Driver code
    public static void Main()
    {
        int n = 10;

        printTrib(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple recursive PHP program to
// print first n Tribinocci numbers.

function printTribRec($n)
{
    if ($n == 0 || $n == 1 || $n == 2)
        return 0;

    if ($n == 3)
        return 1;
    else
        return printTribRec($n - 1) +
               printTribRec($n - 2) +
               printTribRec($n - 3);
}

function printTrib($n)
{
    for ($i = 1; $i <= $n; $i++)
        echo printTribRec($i), " ";
}

    // Driver Code
    $n = 10;
    printTrib($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// A simple recursive Javascript program to
// print first n Tribinocci numbers.

function printTribRec(n)
{
    if (n == 0 || n == 1 || n == 2)
        return 0;

    if (n == 3)
        return 1;
    else
        return printTribRec(n - 1) +
            printTribRec(n - 2) +
            printTribRec(n - 3);
}

function printTrib(n)
{
    for (let i = 1; i <= n; i++)
        document.write(printTribRec(i) + " ");
}

    // Driver Code
    let n = 10;
    printTrib(n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
0 0 1 1 2 4 7 13 24 44 
```

上述解的时间复杂度是指数的。
一个**更好的解决方案**是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。

## C++

```
// A DP based CPP
// program to print
// first n Tribonacci
// numbers.
#include <iostream>
using namespace std;

int printTrib(int n)
{
    int dp[n];
    dp[0] = dp[1] = 0;
    dp[2] = 1;

    for (int i = 3; i < n; i++)
        dp[i] = dp[i - 1] +
                dp[i - 2] +
                dp[i - 3];

    for (int i = 0; i < n; i++)
        cout << dp[i] << " ";
}

// Driver code
int main()
{
    int n = 10;
    printTrib(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A DP based Java program
// to print first n
// Tribonacci numbers.
import java.io.*;

class GFG {

    static void printTrib(int n)
    {
        int dp[]=new int[n];
        dp[0] = dp[1] = 0;
        dp[2] = 1;

        for (int i = 3; i < n; i++)
            dp[i] = dp[i - 1] +
                    dp[i - 2] +
                    dp[i - 3];

        for (int i = 0; i < n; i++)
            System.out.print(dp[i] + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        printTrib(n);
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# A DP based
# Python 3
# program to print
# first n Tribonacci
# numbers.

def printTrib(n) :

    dp = [0] * n
    dp[0] = dp[1] = 0;
    dp[2] = 1;

    for i in range(3,n) :
        dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3];

    for i in range(0,n) :
        print(dp[i] , " ", end="")

# Driver code
n = 10
printTrib(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A DP based C# program
// to print first n
// Tribonacci numbers.
using System;

class GFG {

    static void printTrib(int n)
    {
        int []dp = new int[n];
        dp[0] = dp[1] = 0;
        dp[2] = 1;

        for (int i = 3; i < n; i++)
            dp[i] = dp[i - 1] +
                    dp[i - 2] +
                    dp[i - 3];

        for (int i = 0; i < n; i++)
        Console.Write(dp[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        printTrib(n);
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A DP based PHP program
// to print first n
// Tribonacci numbers.

function printTrib($n)
{

    $dp[0] = $dp[1] = 0;
    $dp[2] = 1;

    for ($i = 3; $i < $n; $i++)
        $dp[$i] = $dp[$i - 1] +
                  $dp[$i - 2] +
                  $dp[$i - 3];

    for ($i = 0; $i < $n; $i++)
        echo $dp[$i] ," ";
}

// Driver code
$n = 10;
printTrib($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program
// to print first n
// Tribonacci numbers.
    function printTrib(n)
    {
        let dp = Array.from({length: n}, (_, i) => 0);
        dp[0] = dp[1] = 0;
        dp[2] = 1;

        for (let i = 3; i < n; i++)
            dp[i] = dp[i - 1] +
                    dp[i - 2] +
                    dp[i - 3];

        for (let i = 0; i < n; i++)
            document.write(dp[i] + " ");
    }

// driver function
        let n = 10;
        printTrib(n);

  // This code is contributed by code_hunt.
</script>   
```

**输出:**

```
0 0 1 1 2 4 7 13 24 44 
```

上面的时间复杂度是线性的，但是需要额外的空间。我们可以使用三个变量来跟踪前三个数字，从而优化上述解决方案中使用的空间。

## C++

```
// A space optimized
// based CPP program to
// print first n
// Tribonacci numbers.
#include <iostream>
using namespace std;

void printTrib(int n)
{
    if (n < 1)
        return;

    // Initialize first
    // three numbers
    int first = 0, second = 0;
    int third = 1;

    cout << first << " ";
    if (n > 1)
        cout << second << " ";

    if (n > 2)
        cout << second << " ";

    // Loop to add previous
    // three numbers for
    // each number starting
    // from 3 and then assign
    // first, second, third
    // to second, third, and
    // curr to third respectively
    for (int i = 3; i < n; i++)
    {
        int curr = first + second + third;
        first = second;
        second = third;
        third = curr;

        cout << curr << " ";
    }
}

// Driver code
int main()
{
    int n = 10;
    printTrib(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A space optimized
// based Java program
// to print first n
// Tribinocci numbers.
import java.io.*;

class GFG {

    static void printTrib(int n)
    {
        if (n < 1)
            return;

        // Initialize first
        // three numbers
        int first = 0, second = 0;
        int third = 1;

        System.out.print(first + " ");
        if (n > 1)
            System.out.print(second + " ");

        if (n > 2)
            System.out.print(second + " ");

        // Loop to add previous
        // three numbers for
        // each number starting
        // from 3 and then assign
        // first, second, third
        // to second, third, and curr
        // to third respectively
        for (int i = 3; i < n; i++)
        {
            int curr = first + second + third;
            first = second;
            second = third;
            third = curr;

            System.out.print(curr +" ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        printTrib(n);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# A space optimized
# based Python 3
# program to print
# first n Tribinocci
# numbers.

def printTrib(n) :
    if (n < 1) :
        return

    # Initialize first
    # three numbers
    first = 0
    second = 0
    third = 1

    print( first , " ", end="")
    if (n > 1) :
        print(second, " ",end="")
    if (n > 2) :
        print(second, " ", end="")

    # Loop to add previous
    # three numbers for
    # each number starting
    # from 3 and then assign
    # first, second, third
    # to second, third, and curr
    # to third respectively
    for i in range(3, n) :
        curr = first + second + third
        first = second
        second = third
        third = curr

        print(curr , " ", end="")

# Driver code
n = 10
printTrib(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A space optimized
// based C# program
// to print first n
// Tribinocci numbers.
using System;

class GFG {

    static void printTrib(int n)
    {
        if (n < 1)
            return;

        // Initialize first
        // three numbers
        int first = 0, second = 0;
        int third = 1;

        Console.Write(first + " ");
        if (n > 1)
        Console.Write(second + " ");

        if (n > 2)
        Console.Write(second + " ");

        // Loop to add previous
        // three numbers for
        // each number starting
        // from 3 and then assign
        // first, second, third
        // to second, third, and curr
        // to third respectively
        for (int i = 3; i < n; i++)
        {
            int curr = first + second + third;
            first = second;
            second = third;
            third = curr;

            Console.Write(curr +" ");
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        printTrib(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A space optimized
// based PHP program to
// print first n
// Tribinocci numbers.|

function printTrib($n)
{
    if ($n < 1)
        return;

    // Initialize first
    // three numbers
    $first = 0; $second = 0;
    $third = 1;

    echo $first, " ";
    if ($n > 1)
        echo $second , " ";

    if ($n > 2)
        echo $second , " ";

    // Loop to add previous
    // three numbers for
    // each number starting
    // from 3 and then assign
    // first, second, third
    // to second, third, and
    // curr to third respectively
    for ($i = 3; $i < $n; $i++)
    {
        $curr = $first + $second + $third;
        $first = $second;
        $second = $third;
        $third = $curr;

        echo $curr , " ";
    }
}

    // Driver code
    $n = 10;
    printTrib($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// A space optimized
// based Javascript program
// to print first n
// Tribonacci numbers.

    function printTrib(n)
    {
        if (n < 1)
            return;

        // Initialize first
        // three numbers
        let first = 0, second = 0;
        let third = 1;

        document.write(first + " ");
        if (n > 1)
            document.write(second + " ");

        if (n > 2)
            document.write(second + " ");

        // Loop to add previous
        // three numbers for
        // each number starting
        // from 3 and then assign
        // first, second, third
        // to second, third, and curr
        // to third respectively
        for (let i = 3; i < n; i++)
        {
            let curr = first + second + third;
            first = second;
            second = third;
            third = curr;

            document.write(curr +" ");
        }
    }

    // Driver code
    let n = 10;
    printTrib(n);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
0 0 0 1 2 4 7 13 24 44  
```

下面是使用[矩阵求幂](https://www.geeksforgeeks.org/matrix-exponentiation/)的更有效的解决方案。

## C++

```
#include <iostream>
using namespace std;

// Program to print first n
// tribonacci numbers Matrix
// Multiplication function
// for 3*3 matrix
void multiply(int T[3][3], int M[3][3])
{
    int a, b, c, d, e, f, g, h, i;
    a = T[0][0] * M[0][0] +
        T[0][1] * M[1][0] +
        T[0][2] * M[2][0];
    b = T[0][0] * M[0][1] +
        T[0][1] * M[1][1] +
        T[0][2] * M[2][1];
    c = T[0][0] * M[0][2] +
        T[0][1] * M[1][2] +
        T[0][2] * M[2][2];
    d = T[1][0] * M[0][0] +
        T[1][1] * M[1][0] +
        T[1][2] * M[2][0];
    e = T[1][0] * M[0][1] +
        T[1][1] * M[1][1] +
        T[1][2] * M[2][1];
    f = T[1][0] * M[0][2] +
        T[1][1] * M[1][2] +
        T[1][2] * M[2][2];
    g = T[2][0] * M[0][0] +
        T[2][1] * M[1][0] +
        T[2][2] * M[2][0];
    h = T[2][0] * M[0][1] +
        T[2][1] * M[1][1] +
        T[2][2] * M[2][1];
    i = T[2][0] * M[0][2] +
        T[2][1] * M[1][2] +
        T[2][2] * M[2][2];
    T[0][0] = a;
    T[0][1] = b;
    T[0][2] = c;
    T[1][0] = d;
    T[1][1] = e;
    T[1][2] = f;
    T[2][0] = g;
    T[2][1] = h;
    T[2][2] = i;
}

// Recursive function to raise
// the matrix T to the power n
void power(int T[3][3], int n)
{
    // base condition.
    if (n == 0 || n == 1)
        return;
    int M[3][3] = {{ 1, 1, 1 },
                   { 1, 0, 0 },
                   { 0, 1, 0 }};

    // recursively call to
    // square the matrix
    power(T, n / 2);

    // calculating square
    // of the matrix T
    multiply(T, T);

    // if n is odd multiply
    // it one time with M
    if (n % 2)
        multiply(T, M);
}
int tribonacci(int n)
{
    int T[3][3] = {{ 1, 1, 1 },
                   { 1, 0, 0 },
                   { 0, 1, 0 }};

    // base condition
    if (n == 0 || n == 1)
        return 0;
    else
        power(T, n - 2);

    // T[0][0] contains the
    // tribonacci number so
    // return it
    return T[0][0];
}

// Driver Code
int main()
{
    int n = 10;
    for (int i = 0; i < n; i++)
        cout << tribonacci(i) << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print
// first n tribonacci numbers
// Matrix Multiplication
// function for 3*3 matrix
import java.io.*;

class GFG
{
    static void multiply(int T[][], int M[][])
    {
        int a, b, c, d, e, f, g, h, i;
        a = T[0][0] * M[0][0] +
            T[0][1] * M[1][0] +
            T[0][2] * M[2][0];
        b = T[0][0] * M[0][1] +
            T[0][1] * M[1][1] +
            T[0][2] * M[2][1];
        c = T[0][0] * M[0][2] +
            T[0][1] * M[1][2] +
            T[0][2] * M[2][2];
        d = T[1][0] * M[0][0] +
            T[1][1] * M[1][0] +
            T[1][2] * M[2][0];
        e = T[1][0] * M[0][1] +
            T[1][1] * M[1][1] +
            T[1][2] * M[2][1];
        f = T[1][0] * M[0][2] +
            T[1][1] * M[1][2] +
            T[1][2] * M[2][2];
        g = T[2][0] * M[0][0] +
            T[2][1] * M[1][0] +
            T[2][2] * M[2][0];
        h = T[2][0] * M[0][1] +
            T[2][1] * M[1][1] +
            T[2][2] * M[2][1];
        i = T[2][0] * M[0][2] +
            T[2][1] * M[1][2] +
            T[2][2] * M[2][2];
        T[0][0] = a;
        T[0][1] = b;
        T[0][2] = c;
        T[1][0] = d;
        T[1][1] = e;
        T[1][2] = f;
        T[2][0] = g;
        T[2][1] = h;
        T[2][2] = i;
    }

    // Recursive function to raise
    // the matrix T to the power n
    static void power(int T[][], int n)
    {
        // base condition.
        if (n == 0 || n == 1)
            return;
        int M[][] = {{ 1, 1, 1 },
                     { 1, 0, 0 },
                     { 0, 1, 0 }};

        // recursively call to
        // square the matrix
        power(T, n / 2);

        // calculating square
        // of the matrix T
        multiply(T, T);

        // if n is odd multiply
        // it one time with M
        if (n % 2 != 0)
            multiply(T, M);
    }
    static int tribonacci(int n)
    {
        int T[][] = {{ 1, 1, 1 },
                     { 1, 0, 0 },
                     { 0, 1, 0 }};

        // base condition
        if (n == 0 || n == 1)
            return 0;
        else
            power(T, n - 2);

        // T[0][0] contains the
        // tribonacci number so
        // return it
        return T[0][0];
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;
        for (int i = 0; i < n; i++)
        System.out.print(tribonacci(i) + " ");
        System.out.println();
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Program to print first n tribonacci
# numbers Matrix Multiplication
# function for 3*3 matrix
def multiply(T, M):

    a = (T[0][0] * M[0][0] + T[0][1] *
         M[1][0] + T[0][2] * M[2][0])            
    b = (T[0][0] * M[0][1] + T[0][1] *
         M[1][1] + T[0][2] * M[2][1])
    c = (T[0][0] * M[0][2] + T[0][1] *
         M[1][2] + T[0][2] * M[2][2])
    d = (T[1][0] * M[0][0] + T[1][1] *
         M[1][0] + T[1][2] * M[2][0])
    e = (T[1][0] * M[0][1] + T[1][1] *
         M[1][1] + T[1][2] * M[2][1])
    f = (T[1][0] * M[0][2] + T[1][1] *
         M[1][2] + T[1][2] * M[2][2])
    g = (T[2][0] * M[0][0] + T[2][1] *
         M[1][0] + T[2][2] * M[2][0])
    h = (T[2][0] * M[0][1] + T[2][1] *
         M[1][1] + T[2][2] * M[2][1])
    i = (T[2][0] * M[0][2] + T[2][1] *
         M[1][2] + T[2][2] * M[2][2])

    T[0][0] = a
    T[0][1] = b
    T[0][2] = c
    T[1][0] = d
    T[1][1] = e
    T[1][2] = f
    T[2][0] = g
    T[2][1] = h
    T[2][2] = i

# Recursive function to raise
# the matrix T to the power n
def power(T, n):

    # base condition.
    if (n == 0 or n == 1):
        return;
    M = [[ 1, 1, 1 ],
                [ 1, 0, 0 ],
                [ 0, 1, 0 ]]

    # recursively call to
    # square the matrix
    power(T, n // 2)

    # calculating square
    # of the matrix T
    multiply(T, T)

    # if n is odd multiply
    # it one time with M
    if (n % 2):
        multiply(T, M)

def tribonacci(n):

    T = [[ 1, 1, 1 ],
        [1, 0, 0 ],
        [0, 1, 0 ]]

    # base condition
    if (n == 0 or n == 1):
        return 0
    else:
        power(T, n - 2)

    # T[0][0] contains the
    # tribonacci number so
    # return it
    return T[0][0]

# Driver Code
if __name__ == "__main__":
    n = 10
    for i in range(n):
        print(tribonacci(i),end=" ")
    print()

# This code is contributed by ChitraNayal
```

## C#

```
// C# Program to print
// first n tribonacci numbers
// Matrix Multiplication
// function for 3*3 matrix
using System;

class GFG
{
    static void multiply(int [,]T,
                         int [,]M)
    {
        int a, b, c, d, e, f, g, h, i;
        a = T[0,0] * M[0,0] +
            T[0,1] * M[1,0] +
            T[0,2] * M[2,0];
        b = T[0,0] * M[0,1] +
            T[0,1] * M[1,1] +
            T[0,2] * M[2,1];
        c = T[0,0] * M[0,2] +
            T[0,1] * M[1,2] +
            T[0,2] * M[2,2];
        d = T[1,0] * M[0,0] +
            T[1,1] * M[1,0] +
            T[1,2] * M[2,0];
        e = T[1,0] * M[0,1] +
            T[1,1] * M[1,1] +
            T[1,2] * M[2,1];
        f = T[1,0] * M[0,2] +
            T[1,1] * M[1,2] +
            T[1,2] * M[2,2];
        g = T[2,0] * M[0,0] +
            T[2,1] * M[1,0] +
            T[2,2] * M[2,0];
        h = T[2,0] * M[0,1] +
            T[2,1] * M[1,1] +
            T[2,2] * M[2,1];
        i = T[2,0] * M[0,2] +
            T[2,1] * M[1,2] +
            T[2,2] * M[2,2];
        T[0,0] = a;
        T[0,1] = b;
        T[0,2] = c;
        T[1,0] = d;
        T[1,1] = e;
        T[1,2] = f;
        T[2,0] = g;
        T[2,1] = h;
        T[2,2] = i;
    }

    // Recursive function to raise
    // the matrix T to the power n
    static void power(int [,]T, int n)
    {
        // base condition.
        if (n == 0 || n == 1)
            return;
        int [,]M = {{ 1, 1, 1 },
                    { 1, 0, 0 },
                    { 0, 1, 0 }};

        // recursively call to
        // square the matrix
        power(T, n / 2);

        // calculating square
        // of the matrix T
        multiply(T, T);

        // if n is odd multiply
        // it one time with M
        if (n % 2 != 0)
            multiply(T, M);
    }

    static int tribonacci(int n)
    {
        int [,]T = {{ 1, 1, 1 },
                    { 1, 0, 0 },
                    { 0, 1, 0 }};

        // base condition
        if (n == 0 || n == 1)
            return 0;
        else
            power(T, n - 2);

        // T[0][0] contains the
        // tribonacci number so
        // return it
        return T[0,0];
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        for (int i = 0; i < n; i++)
        Console.Write(tribonacci(i) + " ");
        Console.WriteLine();
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to print first n tribonacci numbers
// Matrix Multiplication function for 3*3 matrix
function multiply(&$T, $M)
{
    $a = $T[0][0] * $M[0][0] +
         $T[0][1] * $M[1][0] +
         $T[0][2] * $M[2][0];
    $b = $T[0][0] * $M[0][1] +
         $T[0][1] * $M[1][1] +
         $T[0][2] * $M[2][1];
    $c = $T[0][0] * $M[0][2] +
         $T[0][1] * $M[1][2] +
         $T[0][2] * $M[2][2];
    $d = $T[1][0] * $M[0][0] +
         $T[1][1] * $M[1][0] +
         $T[1][2] * $M[2][0];
    $e = $T[1][0] * $M[0][1] +
         $T[1][1] * $M[1][1] +
         $T[1][2] * $M[2][1];
    $f = $T[1][0] * $M[0][2] +
         $T[1][1] * $M[1][2] +
         $T[1][2] * $M[2][2];
    $g = $T[2][0] * $M[0][0] +
         $T[2][1] * $M[1][0] +
         $T[2][2] * $M[2][0];
    $h = $T[2][0] * $M[0][1] +
         $T[2][1] * $M[1][1] +
         $T[2][2] * $M[2][1];
    $i = $T[2][0] * $M[0][2] +
         $T[2][1] * $M[1][2] +
         $T[2][2] * $M[2][2];
    $T[0][0] = $a;
    $T[0][1] = $b;
    $T[0][2] = $c;
    $T[1][0] = $d;
    $T[1][1] = $e;
    $T[1][2] = $f;
    $T[2][0] = $g;
    $T[2][1] = $h;
    $T[2][2] = $i;
}

// Recursive function to raise
// the matrix T to the power n
function power(&$T,$n)
{
    // base condition.
    if ($n == 0 || $n == 1)
        return;
    $M = array(array( 1, 1, 1 ),
               array( 1, 0, 0 ),
               array( 0, 1, 0 ));

    // recursively call to
    // square the matrix
    power($T, (int)($n / 2));

    // calculating square
    // of the matrix T
    multiply($T, $T);

    // if n is odd multiply
    // it one time with M
    if ($n % 2)
        multiply($T, $M);
}

function tribonacci($n)
{
    $T = array(array( 1, 1, 1 ),
               array( 1, 0, 0 ),
               array( 0, 1, 0 ));

    // base condition
    if ($n == 0 || $n == 1)
        return 0;
    else
        power($T, $n - 2);

    // $T[0][0] contains the tribonacci
    // number so return it
    return $T[0][0];
}

// Driver Code
$n = 10;
for ($i = 0; $i < $n; $i++)
    echo tribonacci($i) . " ";
echo "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript Program to print
// first n tribonacci numbers
// Matrix Multiplication
// function for 3*3 matrix

    function multiply(T , M)
    {
        var a, b, c, d, e, f, g, h, i;
        a = T[0][0] * M[0][0] +
            T[0][1] * M[1][0] +
            T[0][2] * M[2][0];
        b = T[0][0] * M[0][1] +
            T[0][1] * M[1][1] +
            T[0][2] * M[2][1];
        c = T[0][0] * M[0][2] +
            T[0][1] * M[1][2] +
            T[0][2] * M[2][2];
        d = T[1][0] * M[0][0] +
            T[1][1] * M[1][0] +
            T[1][2] * M[2][0];
        e = T[1][0] * M[0][1] +
            T[1][1] * M[1][1] +
            T[1][2] * M[2][1];
        f = T[1][0] * M[0][2] +
            T[1][1] * M[1][2] +
            T[1][2] * M[2][2];
        g = T[2][0] * M[0][0] +
            T[2][1] * M[1][0] +
            T[2][2] * M[2][0];
        h = T[2][0] * M[0][1] +
            T[2][1] * M[1][1] +
            T[2][2] * M[2][1];
        i = T[2][0] * M[0][2] +
            T[2][1] * M[1][2] +
            T[2][2] * M[2][2];
        T[0][0] = a;
        T[0][1] = b;
        T[0][2] = c;
        T[1][0] = d;
        T[1][1] = e;
        T[1][2] = f;
        T[2][0] = g;
        T[2][1] = h;
        T[2][2] = i;
    }

    // Recursive function to raise
    // the matrix T to the power n
    function power(T , n)
    {
        // base condition.
        if (n == 0 || n == 1)
            return;
        var M = [[ 1, 1, 1 ],
                     [ 1, 0, 0 ],
                     [ 0, 1, 0 ]];

        // recursively call to
        // square the matrix
        power(T, parseInt(n / 2));

        // calculating square
        // of the matrix T
        multiply(T, T);

        // if n is odd multiply
        // it one time with M
        if (n % 2 != 0)
            multiply(T, M);
    }
    function tribonacci(n)
    {
        var T = [[ 1, 1, 1 ],
                     [ 1, 0, 0 ],
                     [ 0, 1, 0 ]];

        // base condition
        if (n == 0 || n == 1)
            return 0;
        else
            power(T, n - 2);

        // T[0][0] contains the
        // tribonacci number so
        // return it
        return T[0][0];
    }

    // Driver Code
    var n = 10;
    for (var i = 0; i < n; i++)
    document.write(tribonacci(i) + " ");
    document.write('<br>');

// This code contributed by shikhasingrajput
</script>
```

**输出:**

```
0 0 1 1 2 4 7 13 24 44 
```

本文由 [**萨赫勒拉吉普特**](http://inkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。