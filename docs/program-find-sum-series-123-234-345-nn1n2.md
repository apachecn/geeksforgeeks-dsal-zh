# 程序求数列 1*2*3 + 2*3*4+ 3*4*5 +的和。。。+ n*(n+1)*(n+2)

> 原文:[https://www . geesforgeks . org/program-find-sum-series-123-234-345-nn1n 2/](https://www.geeksforgeeks.org/program-find-sum-series-123-234-345-nn1n2/)

给定一个正整数 **n** ，任务是求数列 1*2*3 + 2*3*4 + 4*5*6 +的和。。。+ n*(n+1)*(n+2)。
示例:

```
Input : n = 10
Output : 4290
   1*2*3 + 2*3*4 + 3*4*5 + 4*5*6 + 5*6*7 + 6*7*8 + 
   7*8*9 + 8*9*10 + 9*10*11 + 10*11*12
 = 6 + 24 + 60 + 120 + 210 + 336 + 504 + 
   720 + 990 + 1320
 = 4290

Input : n = 7
Output : 1260
```

**方法 1:** 在这种情况下，循环将运行 **n 次**并计算总和。

## C++

```
// Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)
#include <bits/stdc++.h>
using namespace std;
// Function to calculate sum of series.
int sumOfSeries(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum = sum + i * (i + 1) * (i + 2);
    return sum;
}

// Driver function
int main()
{
    int n = 10;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)
public class GfG{

    // Function to calculate sum of series.
    static int sumOfSeries(int n)
    {
        int sum = 0;

        for (int i = 1; i <= n; i++)
            sum = sum + i * (i + 1) * (i + 2);

        return sum;
    }

    // Driver Code
    public static void main(String s[])
    {
        int n = 10;
        System.out.println(sumOfSeries(n));
    }
}

// This article is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python program to find the
# sum of series
# 1*2*3 + 2*3*4 + . . .
# + n*(n+1)*(n+1)

# Function to calculate sum
# of series.
def sumOfSeries(n):
    sum = 0;
    i = 1;
    while i<=n:
        sum = sum + i * (i + 1) * (
                                i + 2)
        i = i + 1
    return sum

# Driver code
n = 10
print(sumOfSeries(n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)
using System;

public class GfG
{

    // Function to calculate sum of series.
    static int sumOfSeries(int n)
    {
        int sum = 0;

        for (int i = 1; i <= n; i++)
            sum = sum + i * (i + 1) * (i + 2);

        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Console.WriteLine(sumOfSeries(n));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)

// Function to calculate sum of series.
function sumOfSeries($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum = $sum + $i * ($i + 1) *
                           ($i + 2);
    return $sum;
}

// Driver Code
$n = 10;
echo sumOfSeries($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)

// Function to calculate sum of series.
    function sumOfSeries( n) {
        let sum = 0;

        for ( let i = 1; i <= n; i++)
            sum = sum + i * (i + 1) * (i + 2);

        return sum;
    }

    // Driver Code
        let n = 10;
        document.write(sumOfSeries(n));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
4290
```

时间复杂度:O(n)
**方法二:**这种情况下我们用公式来加级数的和。

```
 Given series 1*2*3 + 2*3*4 + 3*4*5 + 4*5*6 + . . . + n*(n+1)*(n+2)
 sum of series = (n * (n+1) * (n+2) * (n+3)) / 4 

 Put n = 10 then 
 sum = (10 * (10+1) * (10+2) * (10+3)) / 4
     = (10 * 11 * 12 * 13) / 4
     = 4290
```

## C++

```
// Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of series.
int sumOfSeries(int n)
{
    return (n * (n + 1) * (n + 2) * (n + 3)) / 4;
}

// Driver function
int main()
{
    int n = 10;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find the
// sum of series
// 1*2*3 + 2*3*4 +
// . . . + n*(n+1)*(n+1)
import java.io.*;

class GFG {

    // Function to calculate
    // sum of series.
    static int sumOfSeries(int n)
    {
        return (n * (n + 1) *
            (n + 2) * (n + 3)) / 4;
    }

    // Driver function
    public static void main (String[] args) {
        int n = 10;
        System.out.println(sumOfSeries(n));

    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python program to find the
# sum of series
# 1*2*3 + 2*3*4 + . . .
# + n*(n+1)*(n+1)

# Function to calculate sum
# of series.
def sumOfSeries(n):
    return (n * (n + 1) * (n + 2
                    ) * (n + 3)) / 4

#Driver code
n = 10
print(sumOfSeries(n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// Program to find the
// sum of series
// 1*2*3 + 2*3*4 +
// . . . + n*(n+1)*(n+1)
using System;

class GFG {

    // Function to calculate
    // sum of series.
    static int sumOfSeries(int n)
    {
        return (n * (n + 1) *
            (n + 2) * (n + 3)) / 4;
    }

    // Driver function
    public static void Main () {
        int n = 10;
        Console.WriteLine(sumOfSeries(n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the sum of series
// 1*2*3 + 2*3*4 + . . . + n*(n+1)*(n+1)

// Function to calculate sum of series.
function sumOfSeries($n)
{
    return ($n * ($n + 1) * ($n + 2) *
                        ($n + 3)) / 4;
}

// Driver Code
$n = 10;
echo sumOfSeries($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// Program to find the
// sum of series
// 1*2*3 + 2*3*4 +
// . . . + n*(n+1)*(n+1)

    // Function to calculate
    // sum of series.
    function sumOfSeries(n) {
        return (n * (n + 1) * (n + 2) * (n + 3)) / 4;
    }

    // Driver function
    var n = 10;
    document.write(sumOfSeries(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
4290
```

时间复杂度:O(1)
**这个公式是如何工作的？**

```
We can prove working of this formula using
mathematical induction.

According to formula, sum of (k -1) terms is
((k - 1) * (k) * (k + 1) * (k + 2)) / 4

Sum of k terms
       = sum of k-1 terms + value of k-th term
       = ((k - 1) * (k) * (k + 1) * (k + 2)) / 4 + 
                             k * (k + 1) * (k + 2)
Taking common term (k + 1) * (k + 2) out.
               = (k + 1)*(k + 2) [k*(k-1)/4 + k]
               = (k + 1)*(k + 2) * k * (k + 3)/4
               = k * (k + 1) * (k + 2) * (k + 3)/4
```