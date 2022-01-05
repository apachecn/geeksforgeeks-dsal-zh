# 前 n 个自然数的平方和

> 原文:[https://www . geesforgeks . org/第一个 n 个自然数的平方和/](https://www.geeksforgeeks.org/sum-of-squares-of-first-n-natural-numbers/)

给定 n，求前 n 个自然数的平方和。
**例:**

```
Input : n = 2
Output : 5
Explanation: 1^2+2^2 = 5

Input : n = 8
Output : 204
Explanation : 
1^2 + 2^2 + 3^2 + 4^2 + 5^2 + 6^2 + 7^2 + 8^2 = 204 
```

**天真的方法:**
天真的方法是运行一个从 1 到 n 的循环，并总结所有的方块。

## C++

```
// CPP program to calculate
// 1^2+2^2+3^2+...
#include <iostream>
using namespace std;

// Function to calculate sum
int summation(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (i * i);

    return sum;
}

// Driver code
int main()
{
    int n = 2;
    cout << summation(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// 1^2+2^2+3^2+...
import java.util.*;
import java.lang.*;

class GFG
{
    // Function to calculate sum
    public static int summation(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += (i * i);

        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 2;
        System.out.println(summation(n));
    }
}

// This code is contributed
// by Sachin Bisht
```

## 蟒蛇 3

```
# Python3 program to
# calculate 1 ^ 2 + 2 ^ 2 + 3 ^ 2+..

# Function to calculate series
def summation(n):
    return sum([i**2 for i in
               range(1, n + 1)])

# Driver Code
if __name__ == "__main__":
    n = 2
    print(summation(n))
```

## C#

```
// C# program to calculate
// 1^2+2^2+3^2+...
using System;
class GFG
{

    // Function to calculate sum
    public static int summation(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += (i * i);

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int n = 2;

        Console.WriteLine(summation(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// 1^2+2^2+3^2+...

// Function to calculate sum
function summation($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += ($i * $i);

    return $sum;
}

    // Driver code
    $n = 2;
    echo summation($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// JavaScript program to calculate
// 1^2+2^2+3^2+...

    // Function to calculate sum
    function summation(n)
    {
        let sum = 0;
        for (let i = 1; i <= n; i++)
            sum += (i * i);

        return sum;
    }

    // Driver code

    let n = 2;
    document.write(summation(n));

// This code is contributed by Surbhi Tyagi

</script>
```

**输出:**

```
5
```

**有效方法:**
存在一个求前 n 个数平方和的公式。
1 + 2 + ………..+n = n(n+1)/2
1<sup>2</sup>+2<sup>2</sup>+……+n<sup>2</sup>= n(n+1)(2n+1)/6

```
n * (n + 1) * (2*n + 1) / 6

Example : n = 3
        = 3 * (3 + 1) * (2*3 + 1) / 6
        = (3 * 4 * 7) / 6
        = 84 / 6
        = 14
```

**这是如何工作的？**

```
We can prove this formula using induction.
We can easily see that the formula is true for
n = 1 and n = 2 as sums are 1 and 5 respectively.

Let it be true for n = k-1\. So sum of k-1 numbers
is (k - 1) * k * (2 * k - 1)) / 6

In the following steps, we show that it is true 
for k assuming that it is true for k-1.

Sum of k numbers = Sum of k-1 numbers + k2
           = (k - 1) * k * (2 * k - 1) / 6 + k2
           = ((k2 - k) * (2*k - 1) + 6k2)/6
           = (2k3 - 2k2 - k2 + k + 6k2)/6
           = (2k3 + 3k2 + k)/6
           = k * (k + 1) * (2*k + 1) / 6
```

## C++

```
// C++ program to get the sum
// of the following series
#include <iostream>
using namespace std;

// Function calculating
// the series
int summation(int n)
{
    return (n * (n + 1) *
        (2 * n + 1)) / 6;
}

// Driver Code
int main()
{
    int n = 10;
    cout << summation(n) << endl;
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to get the sum
// of the following series
#include <stdio.h>

// Function calculating
// the series
int summation(int n)
{
    return (n * (n + 1) *
           (2 * n + 1)) / 6;
}

// Driver Code
int main()
{
    int n = 10;
    printf("%d", summation(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get
// the sum of the series
import java.util.*;
import java.lang.*;

class GFG
{
    // Function calculating
    // the series
    public static int summation(int n)
    {
        return (n * (n + 1) *
               (2 * n + 1)) / 6;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(summation(n));
    }
}

// This code is contributed
// by Sachin Bisht
```

## 蟒蛇 3

```
# Python code to find sum of
# squares of first n natural numbers.
def summation(n):
    return (n * (n + 1) *
           (2 * n + 1)) / 6

# Driver Code
if __name__ == '__main__':
    n = 10
    print(summation(n))
```

## C#

```
// C# program to get the sum
// of the series
using System;

class GFG
{

    // Function calculating
    // the series
    public static int summation(int n)
    {
        return (n * (n + 1) *
               (2 * n + 1)) / 6;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;

        Console.WriteLine(summation(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get the
// sum of the following series

// Function calculating
// the series
function summation($n)
{
    return ($n * ($n + 1) *
           (2 * $n + 1)) / 6;
}

// Driver Code
$n = 10;
echo summation($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<p id="demo"></p>

<script>
var x = summation(10);
document.getElementById("demo").innerHTML = x;

function summation(n) {
  return (n * (n + 1) *
        (2 * n + 1)) / 6;
}
</script>
```

**输出:**

```
385
```