# 计算两个数的平均值不溢出

> 原文:[https://www . geeksforgeeks . org/compute-average-两位数-无溢出/](https://www.geeksforgeeks.org/compute-average-two-numbers-without-overflow/)

给定两个数字，a 和 b。计算这两个数字的平均值。
熟知的公式 **(a + b) / 2** 在以下情况下可能失效:
If，**a = b =(2^31)–1**；即 INT_MAX。
现在，(a+b)会导致溢出，因此公式 **(a + b) / 2** 不起作用
下面是实现:

## C++

```
// C++ code to compute average of two numbers
#include <bits/stdc++.h>
using namespace std;

// Function to compute average of two numbers
int compute_average(int a, int b)
{
    return (a + b) / 2;
}

// Driver code
int main()
{
    // Assigning maximum integer value
    int a = INT_MAX, b = INT_MAX;

    // Average of two equal numbers is the same number
    cout << "Actual average : " << INT_MAX << endl;

    // Function to get the average of 2 numbers
    cout << "Computed average : " << compute_average(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to compute average of two numbers

import java.io.*;

class GFG {

// Function to compute average of two numbers
static int compute_average(int a, int b)
{
    return (a + b) / 2;
}

// Driver code
    public static void main (String[] args) {

    // Assigning maximum integer value
    int a = Integer.MAX_VALUE;
    int b = Integer.MAX_VALUE;

    // Average of two equal numbers is the same number
    System.out.println("Actual average : " + Integer.MAX_VALUE);

    // Function to get the average of 2 numbers
    System.out.println("Computed average : " + compute_average(a, b));

    }
// This code is contributed by ajit.   
}
```

## 蟒蛇 3

```
# Python 3 code to compute
# average of two numbers
import sys
from math import floor

INT_MAX = 2147483647

# Function to compute
# average of two numbers
def compute_average(a, b):
    return floor((a + b) / 2)

# Driver code
if __name__ == '__main__':

    # Assigning maximum integer value
    a = INT_MAX
    b = -INT_MAX - 1

    # Average of two equal numbers
    # is the same number
    print("Actual average : ", INT_MAX)

    # Function to get the
    # average of 2 numbers
    print("Computed average : ",
           compute_average(a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C#  code to compute average of two numbers
using System;

public class GFG{

// Function to compute average of two numbers
static int compute_average(int a, int b)
{
    return (a + b) / 2;
}

// Driver code
    static public void Main (){

    // Assigning maximum integer value
    int a =int.MaxValue;
    int b = int.MaxValue;

    // Average of two equal numbers is the same number
    Console.WriteLine("Actual average : " + int.MaxValue);

    // Function to get the average of 2 numbers
    Console.WriteLine("Computed average : " + compute_average(a, b));
    }
//This code is contributed by akt_mit   
}
```

## java 描述语言

```
<script>
    // Javascript code to compute average of two numbers

    const INT_MAX = 2147483647;

    // Function to compute average of two numbers
    function compute_average(a, b)
    {
        return Math.floor((a + b) / 2);
    }

    // Assigning maximum integer value
    let a = INT_MAX;
    let b = -INT_MAX-1;

    // Average of two equal numbers is the same number
    document.write("Actual average : " + INT_MAX + "</br>");

    // Function to get the average of 2 numbers
    document.write("Computed average : " + compute_average(a, b) + "</br>");

</script>
```

**输出:**

```
Actual average : 2147483647
Computed average : -1
```

**不引起溢出的改进公式:**
平均值=(a/2)+(b/2)+((a % 2)+(b % 2))/2)
下面是实现:

## C++

```
// C++ code to compute average of two numbers
#include <bits/stdc++.h>
using namespace std;

// Function to compute average of two numbers
int compute_average(int a, int b)
{
    return (a / 2) + (b / 2) + ((a % 2 + b % 2) / 2);
}

// Driver code
int main()
{
    // Assigning maximum integer value
    int a = INT_MAX, b = INT_MAX;

    // Average of two equal numbers is the same number
    cout << "Actual average : " << INT_MAX << endl;

    // Function to get the average of 2 numbers
    cout << "Computed average : " << compute_average(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to compute
// average of two numbers
import java.io.*;

class GFG
{

// Function to compute
// average of two numbers
static int compute_average(int a,
                           int b)
{
    return (a / 2) + (b / 2) +
           ((a % 2 + b % 2) / 2);
}

// Driver code
public static void main (String[] args)
{

// Assigning maximum
// integer value
int a = Integer.MAX_VALUE;
int b = Integer.MAX_VALUE;

// Average of two equal
// numbers is the same number
System.out.println("Actual average : " +
                     Integer.MAX_VALUE);

// Function to get the
// average of 2 numbers
System.out.print("Computed average : ");
System.out.println(compute_average(a, b));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python code to compute
# average of two numbers
INT_MAX=2147483647

# Function to compute
# average of two numbers
def compute_average(a,b):

    return (a // 2) + (b // 2) + ((a % 2 + b % 2) // 2)

# Driver code
if __name__ =="__main__":
    # Assigning maximum integer value
    a = INT_MAX
    b = INT_MAX

    # Average of two equal
    # numbers is the same number
    print( "Actual average : ",INT_MAX)

    # Function to get the
    # average of 2 numbers
    print( "Computed average : ",
            compute_average(a, b))

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# code to compute
// average of two numbers

using System;

class GFG
{

// Function to compute
// average of two numbers
static int compute_average(int a,
                           int b)
{
    return (a / 2) + (b / 2) +
           ((a % 2 + b % 2) / 2);
}

// Driver code
public static void Main ()
{

// Assigning maximum
// integer value
int a = int.MaxValue;
int b = int.MaxValue;

// Average of two equal
// numbers is the same number
Console.Write("Actual average : " +
                     int.MaxValue+"\n");

// Function to get the
// average of 2 numbers
Console.Write("Computed average : ");
Console.Write(compute_average(a, b));
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to compute
// average of two numbers
// Function to compute
// average of two numbers
function compute_average($a,$b)
{
    return ($a / 2) + ($b / 2) +
        (($a % 2 + $b % 2) / 2);
}

// Driver code

// Assigning maximum
// integer value
$a = 2147483648;
$b = 2147483648;

// Average of two equal
// numbers is the same number
$x = 2147483648;
print("Actual average : ".$x);

// Function to get the
// average of 2 numbers
print("\nComputed average : ");
print(compute_average($a, $b));

// This code is contributed by princiraj1992
?>
```

## java 描述语言

```
<script>

// javascript code to compute average of two numbers
const INT_MAX = 2147483647;

// Function to compute average of two numbers
function compute_average( a,  b)
{
    return parseInt(a / 2) + parseInt(b / 2) + ((a % 2 + b % 2) / 2);
}

// Driver code

    // Assigning maximum integer value
    let a = INT_MAX, b = INT_MAX;

    // Average of two equal numbers is the same number
    document.write( "Actual average : " + INT_MAX +"<br/>");

    // Function to get the average of 2 numbers
   document.write( "Computed average : " + compute_average(a, b));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Actual average : 2147483647
Computed average : 2147483647
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。