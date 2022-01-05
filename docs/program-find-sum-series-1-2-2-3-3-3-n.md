# 程序求数列 1 + 2 + 2 + 3 + 3 + 3 +的和。。。+ n

> 原文:[https://www . geesforgeks . org/program-find-sum-series-1-2-2-3-3-3-n/](https://www.geeksforgeeks.org/program-find-sum-series-1-2-2-3-3-3-n/)

给定一个正整数 n，任务是求数列 1 + 2 + 2 + 3 + 3 + 3 +的和。。。+ n.
示例:

```
Input : n = 5
Output : 55
   = 1 + 2 + 2 + 3 + 3 + 3 + 4 + 4 + 4 + 
     4 + 5 + 5 + 5 + 5 + 5.
   = 55

Input : n = 10
Output : 385
```

**加法法:**加法法将所有元素逐一求和。
以下是本办法的实施情况。

## C++

```
// Program to find
// sum of series
// 1 + 2 + 2 + 3 +
// . . . + n
#include <bits/stdc++.h>
using namespace std;

// Function that find
// sum of series.
int sumOfSeries(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++)
            sum = sum + i;
    return sum;
}

// Driver function
int main()
{
    int n = 10;

    // Function call
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to
// find sum of
// series
// 1 + 2 + 2 + 3 +
// . . . + n
public class GfG{

    // Function that find
    // sum of series.
    static int sumOfSeries(int n)
    {
        int sum = 0;

        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= i; j++)
                sum = sum + i;

        return sum;
    }

    // Driver Code
    public static void main(String s[])
    {
        int n = 10;
        System.out.println(sumOfSeries(n));

    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Python3 Program to
# find sum of series
# 1 + 2 + 2 + 3 +
# . . . + n
import math

# Function that find
# sum of series.
def sumOfSeries( n):
    sum = 0
    for i in range(1, n+1):
        sum = sum + i * i
    return sum

# Driver method
n = 10

# Function call
print (sumOfSeries(n))

# This code is contributed by Gitanjali
```

## C#

```
// C# Program to find sum of
// series 1 + 2 + 2 + 3 + . . . + n
using System;

public class GfG {

    // Function that find
    // sum of series.
    static int sumOfSeries(int n)
    {
        int sum = 0;

        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= i; j++)
                sum = sum + i;

        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Console.Write(sumOfSeries(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find
// sum of series
// 1 + 2 + 2 + 3 +
// . . . + n

// Function that find
// sum of series.
function sumOfSeries($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        for ($j = 1; $j <= $i; $j++)
            $sum = $sum + $i;
    return $sum;
}

// Driver Code
$n = 10;

// Function call
echo(sumOfSeries($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript Program to
// find sum of
// series
// 1 + 2 + 2 + 3 +
// . . . + n

    // Function that find
    // sum of series.
    function sumOfSeries( n) {
        let sum = 0;

        for (let i = 1; i <= n; i++)
            for (let j = 1; j <= i; j++)
                sum = sum + i;

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
385
```

时间复杂度:O(n <sup>2</sup> )

**辅助空间:** O(1)
**乘法方法:**在乘法方法中，每个元素自身相乘，然后相加。

```
   Input n = 10
   sum = 1 + 2 + 2 + 3 + 3 + 3 + 4 + . . . + 10
       = 1 + 2 * 2 + 3 * 3 + 4 * 4 + . . . + 10 * 10
       = 1 + 4 + 9 + 16 + . . . + 100
       = 385
```

## C++

```
// Program to find
// sum of series
// 1 + 2 + 2 + 3 +
// . . . + n
#include <bits/stdc++.h>
using namespace std;

// Function to find
// sum of series.
int sumOfSeries(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum = sum + i * i;
    return sum;
}

// Driver function.
int main()
{
    int n = 10;

    // Function call
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to
// find sum of series
// 1 + 2 + 2 + 3 +
// . . . + n
public class GfG{

    // Function that find sum of series.
    static int sumOfSeries(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum = sum + i * i;
        return sum;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(sumOfSeries(n));

    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Python3 Program to
# find sum of series
# 1 + 2 + 2 + 3 +
# . . . + n
import math

# Function that find
# sum of series.
def sumOfSeries( n):
    sum = 0
    for i in range(1, n+1):
        sum = sum + i * i
    return sum

# Driver method
n = 10
# Function call
print (sumOfSeries(n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to find sum of series
// 1 + 2 + 2 + 3 + . . . + n
using System;

class GfG {

    // Function that find sum of series.
    static int sumOfSeries(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum = sum + i * i;
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Console.WriteLine(sumOfSeries(n));

    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find
// sum of series
// 1 + 2 + 2 + 3 +
// . . . + n

// Function to find
// sum of series.
function sumOfSeries($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum = $sum + $i * $i;
    return $sum;
}

// Driver Code
$n = 10;

// Function call
echo(sumOfSeries($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript Program to
// find sum of series
// 1 + 2 + 2 + 3 +
// . . . + n

    // Function that find sum of series.
    function sumOfSeries(n)
    {
        var sum = 0;
        for (let i = 1; i <= n; i++)
            sum = sum + i * i;
        return sum;
    }

    // Driver Code
    var n = 10;
    document.write(sumOfSeries(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
385
```

时间复杂度:0(n)

**辅助空间:** O(1)
**利用公式:**我们还利用公式求出级数的和。

```
    Input n = 10;
   Sum of series = (n * (n + 1) * (2 * n + 1)) / 6
    put n = 10 in the above formula
    sum = (10 * (10 + 1) * (2 * 10 + 1)) / 6
        = (10 * 11 * 21) / 6
        = 385
```

## C++

```
// C++ Program to
// find sum of series
// 1 + 2 + 2 + 3 +
// . . . + n
#include <bits/stdc++.h>
using namespace std;

// Function to find
// sum of series.
int sumOfSeries(int n)
{
    return (n * (n + 1) * (2 * n + 1)) / 6;
}

// Driver function
int main()
{
    int n = 10;

    // Function call
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to
// find sum of series
// 1 + 2 + 2 + 3 +
// . . . + n
public class GfG
{
    // Function that find
    // sum of series.
    static int sumOfSeries(int n)
    {
        return (n * (n + 1) * (2 * n + 1)) / 6;
    }

    // Driver Code
    public static void main(String s[])
    {
        int n = 10;
        System.out.println(sumOfSeries(n));

    }
}

// This code is contributed by 'Gitanjali'.
```

## 蟒蛇 3

```
# Python3 Program to
# find sum of series
# 1 + 2 + 2 + 3 +
# . . . + n
import math

# Function that find
# sum of series.
def sumOfSeries( n):
    return ((n * (n + 1) * (2 * n + 1)) / 6)

# Driver method
n = 10

# Function call
print (sumOfSeries(n))

# This code is contributed by Gitanjali
```

## C#

```
// C# Program to find sum of series
// 1 + 2 + 2 + 3 + . . . + n
using System;

public class GfG {

    // Function that find
    // sum of series.
    static int sumOfSeries(int n)
    {
        return (n * (n + 1) * (2 * n + 1)) / 6;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Console.WriteLine(sumOfSeries(n));
    }
}

// This code is contributed by 'vt_m'.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to
// find sum of series
// 1 + 2 + 2 + 3 +
// . . . + n

// Function to find
// sum of series.
function sumOfSeries($n)
{
    return ($n * ($n + 1) *
           (2 * $n + 1)) / 6;
}

// Driver Code
$n = 10;

// Function call
echo(sumOfSeries($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript Program to
// find sum of series
// 1 + 2 + 2 + 3 +
// . . . + n

// Function that find
// sum of series.
function sumOfSeries(n)
{
    return (n * (n + 1) * (2 * n + 1)) / 6;
}

// Driver Code
var n = 10;
document.write(sumOfSeries(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
385
```

时间复杂度:0(1)

辅助空间:O(1)
以上公式及更多优化详见[自然数平方和](https://www.geeksforgeeks.org/sum-squares-first-n-natural-numbers/)。