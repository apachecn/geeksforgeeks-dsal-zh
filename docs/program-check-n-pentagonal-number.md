# 检查 N 是否为五边形数字的程序

> 原文:[https://www . geesforgeks . org/program-check-n-五边形-number/](https://www.geeksforgeeks.org/program-check-n-pentagonal-number/)

给定一个数字(N)，检查是否是[五边形](https://geeksforgeeks.org/nth-pentagonal-number/)。
**例:**

```
Input: 12 
Output: Yes
Explanation: 12 is the third pentagonal number

Input: 19
Output: No
Explanation: The third pentagonal number is 12
while the fourth pentagonal number is 22.
Hence 19 is not a pentagonal number.
```

[五边形数字](https://geeksforgeeks.org/nth-pentagonal-number/)是可以排列形成五边形的数字。如果 N 是五边形数字，那么我们可以用 N 个点或点来生成一个规则的五边形(请参见下图)。
前几个五边形数字是 1，5，12，22，35，51，70，…

图片来源: [Wiki](https://upload.wikimedia.org/wikipedia/commons/5/54/Polygonal_Number_5.gif)
**方法一(迭代)**
我们首先注意到第 n 个五边形数由
![P_n = \frac{3*n^2-n}{2}     ](img/06e784ddc57388e0f223f97aed3eaf26.png "Rendered by QuickLaTeX.com")
给出，遵循一个迭代过程。将 n = 1，2，3 …连续代入公式，并将结果存储在某个变量 M 中，停止，如果 M > = N，迭代后如果 M 等于 N，那么 N 一定是一个五边形数。否则如果 M 超过 N，那么 N 就不能是五边形数。
算法

```
function isPentagonal(N) 
    Set i = 1
    do 
        M = (3*i*i - i)/2
        i += 1
    while M < N

    if M == N
        print Yes
    else
        print No
```

下面是算法
的实现

## C++

```
// C++ program to check
// pentagonal numbers.
#include <iostream>
using namespace std;

// Function to determine
// if N is pentagonal or not.
bool isPentagonal(int N)
{
    int i = 1, M;

    do {

        // Substitute values of i
        // in the formula.
        M = (3*i*i - i)/2;
        i += 1;
    }
    while ( M < N );

    return (M == N);
}

// Driver Code
int main()
{
    int N = 12;

    if (isPentagonal(N))
        cout << N << " is pentagonal " << endl;   
    else
        cout << N << " is not pentagonal" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// pentagonal numbers.
import java.io.*;

class GFG {

// Function to determine
// if N is pentagonal or not.
static Boolean isPentagonal(int N)
{
    int i = 1, M;

    do {

        // Substitute values of
        // i in the formula.
        M = (3*i*i - i)/2;
        i += 1;
    }
    while ( M < N );

    return (M == N);
}
    public static void main (String[] args) {
    int N = 12;

    if (isPentagonal(N))
        System.out.println( N + " is pentagonal " );   
    else
        System.out.println( N + " is not pentagonal");

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python3 program to check
# pentagonal numbers.
import math

# Function to determine if
# N is pentagonal or not.
def isPentagonal( N ) :

    i = 1
    while True:

        # Substitute values of i
        # in the formula.
        M = (3 * i * i - i) / 2
        i += 1

        if ( M >= N ):
            break

    return (M == N)

# Driver method
N = 12
if (isPentagonal(N)):
    print(N , end = ' ')
    print ("is pentagonal " )
else:
    print (N , end = ' ')
    print ("is not pentagonal")

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to check pentagonal numbers.
using System;

class GFG {

// Function to determine
// if N is pentagonal or not.
static bool isPentagonal(int N)
{
    int i = 1, M;

    do {

        // Substitute values of
        // i in the formula.
        M = (3 * i * i - i) / 2;
        i += 1;
    }
    while ( M < N );

    return (M == N);
}

// Driver Code
public static void Main ()
{
    int N = 12;

    if (isPentagonal(N))
    Console.Write( N + " is pentagonal " );
    else
    Console.Write( N + " is not pentagonal");

}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// pentagonal numbers.

// Function to determine
// if N is pentagonal or not.
function isPentagonal(int $N)
{
    $i = 1;
    $M;

    do {

        // Substitute values of i
        // in the formula.
        $M = (3 * $i * $i - $i) / 2;
        $i += 1;
    }
    while ($M < $N);

    return ($M == $N);
}

    // Driver Code
    $N = 12;

    if (isPentagonal($N))
        echo $N , " is pentagonal " ;
    else
        echo $N ," is not pentagonal" ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to check
// pentagonal numbers.

// Function to determine
// if N is pentagonal or not.
function isPentagonal(N)
{
    var i = 1, M; 
    do
    {

        // Substitute values of
        // i in the formula.
        M = (3 * i * i - i)/2;
        i += 1;
    }
    while ( M < N );
        return (M == N);
}

var N = 12;

if (isPentagonal(N))
    document.write( N + " is pentagonal " );   
else
    document.write( N + " is not pentagonal");

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
12 is pentagonal 
```

这种方法的时间复杂度为 O(n)，因为我们需要计算五角数的连续值，直到 N.

**方法 2(高效)**
公式表明第 N 个五角数二次依赖于 N，因此，尝试寻找 N = P(n)方程的正整数根。
P(n) =第 N 个五边形数
N =给定数
求解为 n:
P(n) = N
或(3 * N * N–N)/2 = N
或 3 * N * N–N–2 * N = 0……(I)
方程(i)
n = (1 + sqrt(24N+1))/6
得到 N 后，检查是否为整数。如果 n–floor(n)为 0，则 n 为整数。
实施方法如下:

## C++

```
// C++ Program to check a
// pentagonal number
#include <bits/stdc++.h>
using namespace std;

// Function to determine if
// N is pentagonal or not.
bool isPentagonal(int N)
{   
    // Get positive root of
    // equation P(n) = N.
    float n = (1 + sqrt(24*N + 1))/6;

    // Check if n is an integral
    // value of not. To get the
    // floor of n, type cast to int.
    return (n - (int) n) == 0;
}

// Driver Code
int main()
{
    int N = 19;   
    if (isPentagonal(N))
        cout << N << " is pentagonal " << endl;   
    else
        cout << N << " is not pentagonal" << endl;   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// pentagonal numbers.
import java.io.*;

class GFG {

// Function to determine if
// N is pentagonal or not.
static Boolean isPentagonal(int N)
{
        // Get positive root of
    // equation P(n) = N.
    double n = (1 + Math.sqrt(24*N + 1))/6;

    // Check if n is an integral
    // value of not. To get the
    // floor of n, type cast to int.
    return (n - (int) n) == 0;
}
    public static void main (String[] args) {
    int N = 19;

    if (isPentagonal(N))
        System.out.println( N + " is pentagonal " );   
    else
        System.out.println( N + " is not pentagonal");

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 code Program to 
# check a pentagonal number

# Import math library
import math as m

# Function to determine if
# N is pentagonal or not
def isPentagonal( n ):

    # Get positive root of
    # equation P(n) = N.
    n = (1 + m.sqrt(24 * N + 1)) / 6

    # Check if n is an integral
    # value of not. To get the
    # floor of n, type cast to int
    return( (n - int (n)) == 0)

# Driver Code
N = 19

if (isPentagonal(N)):
    print ( N, " is pentagonal " )
else:
    print ( N, " is not pentagonal" )

# This code is contributed by 'saloni1297'
```

## C#

```
// C# program to check pentagonal numbers.
using System;

class GFG {

    // Function to determine if
    // N is pentagonal or not.
    static bool isPentagonal(int N)
    {
        // Get positive root of
        // equation P(n) = N.
        double n = (1 + Math.Sqrt(24 * N + 1)) / 6;

        // Check if n is an integral
        // value of not. To get the
        // floor of n, type cast to int.
        return (n - (int)n) == 0;
    }

    // Driver Code
    public static void Main()
    {
        int N = 19;

        if (isPentagonal(N))
            Console.Write(N + " is pentagonal ");
        else
            Console.Write(N + " is not pentagonal");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check
// a pentagonal number

// Function to determine if
// N is pentagonal or not.
function isPentagonal($N)
{
    // Get positive root of
    // equation P(n) = N.
    $n = (1 + sqrt(24 * $N + 1)) / 6;

    // Check if n is an integral
    // value of not. To get the
    // floor of n, type cast to int.
    return ($n - (int) $n) == 0;
}

// Driver Code
$N = 19;
if (isPentagonal($N))
    echo $N . " is pentagonal ";
else
    echo $N . " is not pentagonal";

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// javascript program to check
// pentagonal numbers.

// Function to determine if
// N is pentagonal or not.
function isPentagonal(N)
{
     // Get positive root of
    // equation P(n) = N.
    var n = (1 + Math.sqrt(24*N + 1))/6;

    // Check if n is an integral
    // value of not. To get the
    // floor of n, type cast to int.
    return (n - parseInt( n) == 0);
}

var N = 19;

if (isPentagonal(N))
    document.write( N + " is pentagonal " );   
else
    document.write( N + " is not pentagonal");

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
19 is not pentagonal
```

这种方法的时间和空间复杂度都是 O(1)。
参考文献:
1) [维基百科–五边形数字](https://en.wikipedia.org/wiki/Pentagonal_number)
2)[Wolfram Alpha–五边形数字](http://mathworld.wolfram.com/PentagonalNumber.html)