# 求数列 3、9、21、41、71 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-第 n 个术语-给定-数学-系列/](https://www.geeksforgeeks.org/find-nth-term-given-mathematical-series/)

给定一个数学级数为 3，9，21，41，71…对于给定的整数 n，你必须找到这个级数的第 n 个数。
**例:**

```
Input : n = 4 
Output : 41

Input : n = 2
Output : 9
```

我们解决这个问题的首要任务是破解这个系列。如果你仔细看一下这个系列，对于一般的第 n 项，该值将是**(σn<sup>2</sup>)+(σn)+1**，其中

*   **(σn<sup>2</sup>)**:为[前 n 个自然数](https://www.geeksforgeeks.org/sum-of-squares-of-first-n-natural-numbers/)的平方和。
*   **(σn)**:为[前 n 个自然数](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)之和。
*   1 是一个简单的常数值。

因此，为了计算给定序列的任何第 n 项，比如 f(n)，我们有:
T1】f(n)=(σn<sup>2</sup>)+(σn)+1T5 =((n *(n+1)*(2n+1))/6)+(n *(n+1)/2)+1
=(n<sup>3</sup>+3n<sup>2</sup>+2n+3)/3

## C++

```
// Program to calculate
// nth term of a series
#include <bits/stdc++.h>
using namespace std;

// func for calualtion
int seriesFunc(int n)
{
    // for summation of square
    // of first n-natural nos.
    int sumSquare = (n * (n + 1)
                  * (2 * n + 1)) / 6;

    // summation of first n natural nos.
    int sumNatural = (n * (n + 1) / 2);

    // return result
    return (sumSquare + sumNatural + 1);
}

// Driver Code
int main()
{
    int n = 8;   
    cout << seriesFunc(n) << endl;

    n = 13;
    cout << seriesFunc(13);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to calculate
// nth term of a series
import java.io.*;

class GFG
{
    // func for calualtion
    static int seriesFunc(int n)
    {
        // for summation of square
        // of first n-natural nos.
        int sumSquare = (n * (n + 1)
                        * (2 * n + 1)) / 6;

        // summation of first n natural nos.
        int sumNatural = (n * (n + 1) / 2);

        // return result
        return (sumSquare + sumNatural + 1);
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 8;
        System.out.println(seriesFunc(n));

        n = 13;
        System.out.println(seriesFunc(13));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Program to calculate
# nth term of a series

# func for calualtion
def seriesFunc(n):

    # for summation of square
    # of first n-natural nos.
    sumSquare = (n * (n + 1) *
                (2 * n + 1)) / 6

    # summation of first n
    # natural nos.
    sumNatural = (n * (n + 1) / 2)

    # return result
    return (sumSquare + sumNatural + 1)

# Driver Code
n = 8
print (int(seriesFunc(n)))

n = 13
print (int(seriesFunc(n)))

# This is code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to calculate
// nth term of a series
using System;

class GFG
{
    // Function for calualtion
    static int seriesFunc(int n)
    {
        // For summation of square
        // of first n-natural nos.
        int sumSquare = (n * (n + 1)
                        * (2 * n + 1)) / 6;

        // summation of first n natural nos.
        int sumNatural = (n * (n + 1) / 2);

        // return result
        return (sumSquare + sumNatural + 1);
    }

    // Driver Code
    public static void Main()
    {
        int n = 8;
        Console.WriteLine(seriesFunc(n));

        n = 13;
        Console.WriteLine(seriesFunc(13));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to calculate
// nth term of a series

// func for calualtion
function seriesFunc($n)
{
    // for summation of square
    // of first n-natural nos.
    $sumSquare = ($n * ($n + 1)
                * (2 * $n + 1)) / 6;

    // summation of first n natural nos.
    $sumNatural = ($n * ($n + 1) / 2);

    // return result
    return ($sumSquare + $sumNatural + 1);
}

// Driver Code
$n = 8;
echo(seriesFunc($n) . "\n");

$n = 13;
echo(seriesFunc($n) . "\n");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to calculate
// nth term of a series

    // func for calualtion
    function seriesFunc(n)
    {
        // for summation of square
        // of first n-natural nos.
        let sumSquare = (n * (n + 1)
                        * (2 * n + 1)) / 6;

        // summation of first n natural nos.
        let sumNatural = (n * (n + 1) / 2);

        // return result
        return (sumSquare + sumNatural + 1);
    }

// Driver code

        let n = 8;
        document.write(seriesFunc(n) + "<br/>");

        n = 13;
        document.write(seriesFunc(13));

</script>
```

**输出:**

```
241
911
```