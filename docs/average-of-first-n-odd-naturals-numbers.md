# 前 n 个奇数自然数的平均值

> 原文:[https://www . geesforgeks . org/average-of-first-n-奇数-naturals-numbers/](https://www.geeksforgeeks.org/average-of-first-n-odd-naturals-numbers/)

给定一个数 n，然后求前 n 个奇数的平均值
1 + 3 + 5 + 7 + 9 +…………。+(2n–1)
**例:**

```
Input  : 5
Output : 5
(1 + 3 + 5 + 7 + 9)/5 = 5 

Input  : 10
Output : 10
(1 + 3 + 5 + 7 + 9 + 11 + 13 + 15 + 17 + 19)/10 =10
```

**方法 1(天真方法:**
一个简单的解决方案是迭代循环形式 1 到 n 次。通过[所有奇数的和](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)并除以 N，这个解需要 O(N)个时间。

## C++

```
// A  C++ program to find average of
// sum of first n odd natural numbers.
#include <iostream>
using namespace std;

// Returns the Avg of
// first n odd numbers
int avg_of_odd_num(int n)
{

    // sum of first n odd number
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += (2 * i + 1);

    // Average of first
    // n odd numbers
    return sum / n;
}

// Driver Code
int main()
{
    int n = 20;
    cout << avg_of_odd_num(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find average of
// sum of first n odd natural numbers.
import java.io.*;

class GFG {

    // Returns the Avg of
    // first n odd numbers
    static int avg_of_odd_num(int n)
    {

        // sum of first n odd number
        int sum = 0;

        for (int i = 0; i < n; i++)
            sum += (2 * i + 1);

        // Average of first
        // n odd numbers
        return sum / n;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int n = 20;
        avg_of_odd_num(n);

        System.out.println(avg_of_odd_num(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# A Python 3 program
# to find average of
# sum of first n odd
# natural numbers.

# Returns the Avg of
# first n odd numbers
def avg_of_odd_num(n) :

    # sum of first n odd number
    sm = 0
    for i in range(0, n) :
        sm = sm + (2 * i + 1)

    # Average of first
    # n odd numbers
    return sm//n

# Driver Code
n = 20
print(avg_of_odd_num(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find average
// of sum of first n odd
// natural numbers.
using System;

class GFG {

    // Returns the Avg of
    // first n odd numbers
    static int avg_of_odd_num(int n)
    {

        // sum of first n odd number
        int sum = 0;

        for (int i = 0; i < n; i++)
            sum += (2 * i + 1);

        // Average of first
        // n odd numbers
        return sum / n;
    }

    // Driver code
    public static void Main()
    {

        int n = 20;
        avg_of_odd_num(n);

        Console.Write(avg_of_odd_num(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find average of
// sum of first n odd natural numbers.

// Returns the Avg of
// first n odd numbers
function avg_of_odd_num($n)
{

    // sum of first n odd number
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += (2 * $i + 1);

    // Average of first
    // n odd numbers
    return $sum / $n;
}

// Driver Code
$n = 20;
echo(avg_of_odd_num($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to find average of
// sum of first n odd natural numbers.

// Returns the Avg of
// first n odd numbers
function avg_of_odd_num( n)
{

    // sum of first n odd number
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += (2 * i + 1);

    // Average of first
    // n odd numbers
    return sum / n;
}

// Driver Code
    let n = 20;
    document.write(avg_of_odd_num(n));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
 20
```

**时间复杂度:O(n)**
**方法二(有效途径:**
思路是前 n 个奇数的[和为 **n <sup>2</sup>**](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/) ，求前 n 个奇数的平均值，所以除以 n，因此公式为 **n <sup>2</sup> /n = n** 。这需要时间。

```
                           Avg of sum of first N odd Numbers = N
```

## C++

```
// CPP Program to find the average
// of sum of first n odd numbers
#include <bits/stdc++.h>
using namespace std;

// Return the average of sum
// of first n odd numbers
int avg_of_odd_num(int n)
{
    return n;
}

// Driver Code
int main()
{
    int n = 8;
    cout << avg_of_odd_num(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java Program to find the average
// of sum of first n odd numbers
import java.io.*;

class GFG {

    // Return the average of sum
    // of first n odd numbers
    static int avg_of_odd_num(int n)
    {
        return n;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 8;

        System.out.println(avg_of_odd_num(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 Program to
# find the average
# of sum of first n
# odd numbers

# Return the average of sum
# of first n odd numbers
def avg_of_odd_num(n) :
    return n

# Driver Code
n = 8
print(avg_of_odd_num(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# Program to find the average
// of sum of first n odd numbers
using System;

class GFG {
    // Return the average of sum
    // of first n odd numbers
    static int avg_of_odd_num(int n)
    {
        return n;
    }

    // Driver Code
    public static void Main()
    {
        int n = 8;
        Console.Write(avg_of_odd_num(n));
    }
}
// This code is contributed by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the average
// of sum of first n odd numbers

// Return the average of sum
// of first n odd numbers
function avg_of_odd_num($n)
{
    return $n;
}

// Driver Code
$n = 8;
echo(avg_of_odd_num($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript Program to find the average
// of sum of first n odd numbers

    // Return the average of sum
    // of first n odd numbers
    function avg_of_odd_num(n)
    {
        return n;
    }

    // Driver Code
    var n = 8;
    document.write(avg_of_odd_num(n));

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
 8
```

**时间复杂度:O(1)**
**证明**

```
Sum of first n terms of an A.P.(Arithmetic Progression)
= (n/2) * [2*a + (n-1)*d].....(i)
where, a is the first term of the series 
and d is the difference between the adjacent 
terms of the series.

Here, a = 1, d = 2, applying these values to e. q., 
(i), we get
Sum = (n/2) * [2*1 + (n-1)*2]
    = (n/2) * [2 + 2*n - 2]
    = (n/2) * (2*n)
    = n*n
    = n2

Avg of first n odd numbers = n2/n
                           = n
```