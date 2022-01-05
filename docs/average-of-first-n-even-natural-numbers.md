# 前 n 个偶数自然数的平均值

> 原文:[https://www . geeksforgeeks . org/第一 n 个偶数自然数的平均值/](https://www.geeksforgeeks.org/average-of-first-n-even-natural-numbers/)

给定一个数 n，然后求前 n 个偶数自然数的平均值
Ex。= 2+4+6+8+10+12+……+2n。
**例:**

```
Input  : 7
Output : 8
(2 + 4 + 6 + 8 + 10 + 12 + 14)/7 = 8 

Input  : 5
Output : 6
(2 + 4 + 6 + 8 + 10)/5 = 6
```

**天真的方法:-** 在这个程序中迭代循环，找到前 N 个偶数的总和[并除以 N，需要 0(N)个时间。](https://www.geeksforgeeks.org/sum-first-n-even-numbers/) 

## C++

```
// C++ implementation to find Average
// of sum of first n natural even numbers
#include <bits/stdc++.h>
using namespace std;

// function to find average of
// sum of first n even numbers
int avg_of_even_num(int n)
{
    // sum of first n even numbers
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += 2*i;

    // calculating Average
    return sum/n;
}

// Driver Code
int main()
{
    int n = 9;
    cout << avg_of_even_num(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation to find Average
// of sum of first n natural even number
import java.io.*;

class GFG {

    // function to find average of
    // sum of first n even numbers
    static int avg_of_even_num(int n)
    {

    // sum of first n even numbers
    int sum = 0;

    for (int i = 1; i <= n; i++)
        sum += 2*i;

    // calculating Average
    return (sum / n);
    }
    public static void main (String[] args) {

    int n = 9;
    System.out.print(avg_of_even_num(n));

    }
}

// this code is contributed by 'vt_m'
```

## 蟒蛇 3

```
# Python3 implementation to
# find Average of sum of
# first n natural even
# number

# Function to find average
# of sum of first n even
# numbers
def avg_of_even_num(n):

    # sum of first n even
    # numbers
    sum=0
    for i in range(1, n + 1):
        sum=sum + 2 * i

    # calculating Average
    return sum / n

n=9
print(avg_of_even_num(n))

# This code is contributed by upendra singh bartwal
```

## C#

```
// C# implementation to find
// Average of sum of first
// n natural even number
using System;

class GFG {

    // function to find average of
    // sum of first n even numbers
    static int avg_of_even_num(int n)
    {

    // sum of first n even numbers
    int sum = 0;

    for (int i = 1; i <= n; i++)
        sum += 2 * i;

    // calculating Average
    return (sum / n);
    }

    // driver code
    public static void Main () {

    int n = 9;
    Console.Write(avg_of_even_num(n));

    }
}

// This code is contributed by 'vt_m'
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find Average
// of sum of first n natural even numbers

// function to find average of
// sum of first n even numbers
function avg_of_even_num($n)
{
    // sum of first n even numbers
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += 2 * $i;

    // calculating Average
    return $sum / $n;
}

// Driver Code
$n = 9;
echo(avg_of_even_num($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript implementation to find Average
// of sum of first n natural even numbers

// function to find average of
// sum of first n even numbers
function avg_of_even_num( n)
{

    // sum of first n even numbers
    let sum = 0;
    for (let i = 1; i <= n; i++)
        sum += 2*i;

    // calculating Average
    return sum/n;
}

// Driver Code
    let n = 9;
    document.write(avg_of_even_num(n));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
  10
```

**时间复杂度:O(N)**
**方法二:-** 思路是[前 N 个偶数之和](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)为 n(n+1)，用于求前 N 个偶数除以 N 的平均值，故公式为 **n(n + 1) / n = ( n + 1)** 。即前 n 个偶数的平均值为 **n+1** 。它需要 0(1)时间。

```
                  Avg of sum of N even natural number = (N + 1)
```

**证明**T2】

```
Sum of first n terms of an A.P.(Arithmetic Progression)
= (n/2) * [2*a + (n-1)*d].....(i)
where, a is the first term of the series and d is
the difference between the adjacent terms of the series.

Here, a = 2, d = 2, applying these values to eq.(i), get
Sum = (n/2) * [2*2 + (n-1)*2]
    = (n/2) * [4 + 2*n - 2]
    = (n/2) * (2*n + 2)
    = n * (n + 1)

 finding the Avg so divided by n = n*(n+1)/n
                                      = (n+1)
```

## C++

```
// CPP Program to find the average
// of sum of first n even numbers
#include <bits/stdc++.h>
using namespace std;

// Return the average of sum
// of first n even numbers
int avg_of_even_num(int n)
{
    return n+1;
}

// Driver Code
int main()
{
    int n = 8;
    cout << avg_of_even_num(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the average
// of sum of first n even numbers
import java.io.*;

class GFG
{

    // Return the average of sum
    // of first n even numbers
    static int avg_of_even_num(int n)
    {
        return n + 1;
    }

    public static void main (String[] args) {

        int n = 8;
        System.out.println(avg_of_even_num(n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 Program to
# find the average
# of sum of first n
# even numbers

# Return the average of sum
# of first n even numbers
def avg_of_even_num(n) :

    return n+1

# Driven Program
n = 8
print(avg_of_even_num(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# Program to find the average
// of sum of first n even numbers
using System;

class GFG {

    // Return the average of sum
    // of first n even numbers
    static int avg_of_even_num(int n)
    {
        return n + 1;
    }

    // driver code   
    public static void Main () {

        int n = 8;
        Console.Write(avg_of_even_num(n));

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the average
// of sum of first n even numbers

// Return the average of sum
// of first n even numbers
function avg_of_even_num($n)
{
    return $n + 1;
}

// Driver Code
$n = 8;
echo(avg_of_even_num($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript Program to find the average
// of sum of first n even numbers

// Return the average of sum
// of first n even numbers
function avg_of_even_num(n)
{
    return n + 1;
}
var n = 8;
document.write(avg_of_even_num(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
9
```

**时间复杂度:O(1)**