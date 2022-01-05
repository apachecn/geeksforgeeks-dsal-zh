# 自然数平方的平均值

> 原文:[https://www . geesforgeks . org/average-squares-natural-numbers/](https://www.geeksforgeeks.org/average-squares-natural-numbers/)

给定一个数 n，求自然数平方的平均值直到 n
**例:**

```
Input : n = 2
Output :2.5
12 + 22 = 2.5

Input  : n = 3
Output : 4.666667
12 + 22 + 32 = 4.666667
```

**天真的方法:**
天真的方法是运行一个从 1 到 n 的循环，并找出所有平方的平均值。

## C

```
// C program to calculate 1^2+2^2+3^2+... average
// of square number
#include <stdio.h>

// Function to calculate  average of square number
float AvgofSquareN(int n)
{
    float sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (i * i);
    return sum/n;
}

// Driver code
int main()
{
    int n = 2;
    printf("%f", AvgofSquareN(n));
    return 0;
}
```

## C++

```
// C++ program to calculate 1^2+2^2+3^2+...
// average of square number
#include<bits/stdc++.h>
using namespace std;

// Function to calculate average of squares
float AvgofSquareN(int n)
{
    float sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (i * i);
    return sum/n;
}

// Driver code
int main()
{
    int n = 2;
    cout << AvgofSquareN(n) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate 1^2+2^2+3^2+
// ... average of square number
import java.io.*;

public class GFG{

// Function to calculate average
// of square number
static float AvgofSquareN(int n)
{
    float sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (i * i);
    return sum / n;
}

// Driver code
static public void main (String[] args)
{
    int n = 2;
    System.out.println(AvgofSquareN(n));

}
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to
# calculate 1^2+2^2+3^2+...
# average of square number

# Function to calculate
# average of square number
def AvgofSquareN(n) :

    sum = 0
    for i in range(1, n + 1) :
        sum += (i * i)
    return sum/n

# Driver code
n = 2
print (AvgofSquareN(n))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to calculate 1^2+2^2+3^2+
// ... average of square number
using System;

public class GFG{

// Function to calculate average
// of square number
static float AvgofSquareN(int n)
{
    float sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (i * i);
    return sum / n;
}

// Driver code
static public void Main (String []args)
{
    int n = 2;
    Console.WriteLine(AvgofSquareN(n));

}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate 1^2+2^2+3^2+...
// average of square number

// Function to calculate average
// of square number
function AvgofSquareN( $n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += ($i * $i);
    return $sum/$n;
}

    // Driver code
    $n = 2;
    echo(AvgofSquareN($n));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript program to calculate 1^2+2^2+3^2+... average
// of square number

// Function to calculate  average of square number
function AvgofSquareN( n)
{
    let sum = 0;
    for (let i = 1; i <= n; i++)
        sum += (i * i);
    return sum/n;
}

// Driver code
    let n = 2;
    document.write(AvgofSquareN(n).toFixed(6));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
2.500000
```

***时间复杂度:** O(n)*
***空间复杂度:** O(1)*
**高效逼近:** [自然数平方和](https://www.geeksforgeeks.org/sum-squares-first-n-natural-numbers/) **(n + 1)(2n + 1) / 6** 。因此平均值为 n(n + 1)(2n + 1) / 6 * n = (n + 1)(2n + 1) / 6。

## C

```
// C program to get the  Average of Square
// of first n natural numbers
#include <stdio.h>

float AvgofSquareN(int n)
{
    return (float)((n + 1) * (2 * n + 1)) / 6;
}

// Driver Code
int main()
{
    int n = 10;
    printf("%f", AvgofSquareN(n));
    return 0;
}
```

## C++

```
// C++ program to get the  Average of Square
// of first n natural numbers
#include<bits/stdc++.h>
using namespace std;

float AvgofSquareN(int n)
{
    return (float)((n + 1) * (2 * n + 1)) / 6;
}

// Driver Code
int main()
{
    int n = 10;
    cout << AvgofSquareN(n) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get the Average of
// square of first n natural numbers
import java.io.*;

public class GFG{

// Function to get the average
static float AvgofSquareN(int n)
{
    return (float)((n + 1) * (2 *
                    n + 1)) / 6;
}

// Driver Code
static public void main (String[] args)
{
    int n = 2;
    System.out.println(AvgofSquareN(n));

}
}

// This code is contributed by vt_m. 
```

## 蟒蛇 3

```
# PHP program to get the Average of
# Square of first n natural numbers

def AvgofSquareN(n) :

    return ((n + 1) * (2 * n + 1)) / 6;

# Driver Code
n = 2;
print (AvgofSquareN(n));

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to get the Average of
// squareof first n natural numbers
using System;

public class GFG{

// Function to calculate average
static float AvgofSquareN(int n)
{
    return (float)((n + 1) * (2 *
                    n + 1)) / 6;
}

// Driver Code
static public void Main (String []args)
{
    int n = 2;
    Console.WriteLine(AvgofSquareN(n));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get the Average of
// Square of first n natural numbers

function AvgofSquareN( $n)
{
    return (($n + 1) * (2 * $n + 1)) / 6;
}

    // Driver Code
    $n = 2;
    echo(AvgofSquareN($n));

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript program to get the Average of
// square of first n natural numberspublic

// Function to get the average
function AvgofSquareN(n)
{
    return ((n + 1) * (2 *
                    n + 1)) / 6;
}

// Driver Code
var n = 2;
document.write(AvgofSquareN(n));

// This code is contributed by Amit Katiyar
</script>
```

```
2.500000
```

***时间复杂度:** O(1)*
***空间复杂度:** O(1)*