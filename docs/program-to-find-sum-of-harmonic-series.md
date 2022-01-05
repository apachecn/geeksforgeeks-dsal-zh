# 求调和级数和的程序

> 原文:[https://www . geesforgeks . org/program-to-find-sum-of-harmonic-series/](https://www.geeksforgeeks.org/program-to-find-sum-of-harmonic-series/)

[调和级数](https://www.geeksforgeeks.org/harmonic-progression/)是[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的倒数。一般来说，调和级数中的项可以表示为 1/a，1/(a + d)，1/(a + 2d)，1/(a + 3d) …。1/(a + nd)。
作为 *N <sup>第</sup>* 项的 AP 给出为(a+(N–1)d。因此，调和级数的 *N <sup>th</sup>* 项是 AP 的第 N 项的倒数，即 1/(a+(N–1)d)，其中“a”是 AP 的第 1 项，“d”是共同的区别。

**方法#1:** 简单方法

## C++

```
// C++ program to find sum of harmonic series
#include<bits/stdc++.h>
using namespace std;

// Function to return sum of harmonic series
double sum(int n)
{
  double i, s = 0.0;
  for(i = 1; i <= n; i++)
      s = s + 1 / i;

  return s;
}

// Driver code
int main()
{
    int n = 5;

    cout << "Sum is " << sum(n);
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program to find sum of harmonic series
#include <stdio.h>

// Function to return sum of harmonic series
double sum(int n)
{
  double i, s = 0.0;
  for (i = 1; i <= n; i++)
      s = s + 1/i;
  return s;
}

int main()
{
    int n = 5;
    printf("Sum is %f", sum(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of harmonic series
import java.io.*;

class GFG {

    // Function to return sum of
    // harmonic series
    static double sum(int n)
    {
      double i, s = 0.0;
      for (i = 1; i <= n; i++)
          s = s + 1/i;
      return s;
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 5;
        System.out.printf("Sum is %f", sum(n));       
    }
}
```

## 蟒蛇 3

```
# Python program to find the sum of harmonic series

def sum(n):
    i = 1
    s = 0.0
    for i in range(1, n+1):
        s = s + 1/i;
    return s;

# Driver Code
n = 5
print("Sum is", round(sum(n), 6))
```

## C#

```
// C# Program to find sum of harmonic series
using System;

class GFG {

    // Function to return sum of
    // harmonic series
    static float sum(int n)
    {
        double i, s = 0.0;

        for (i = 1; i <= n; i++)
            s = s + 1/i;

        return (float)s;
    }

    // Driven Program
    public static void Main()
    {
        int n = 5;       
        Console.WriteLine("Sum is "
                           + sum(n));       
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of harmonic series

// Function to return sum of
// harmonic series
function sum( $n)
{
    $i;
    $s = 0.0;
    for ($i = 1; $i <= $n; $i++)
        $s = $s + 1 / $i;
    return $s;
}

    // Driver Code
    $n = 5;
    echo("Sum is ");
    echo(sum($n));

?>
```

## java 描述语言

```
<script>
// JavaScript program to find sum of harmonic series

// Function to return sum of harmonic series
function sum(n)
{
let i, s = 0.0;
for(i = 1; i <= n; i++)
    s = s + 1 / i;

return s;
}

// Driver code
let n = 5;
document.write("Sum is " + sum(n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
Sum is 2.283333
```

**方法#2:** 使用递归

## C++

```
// CPP program to find sum of
// harmonic series using recursion
#include<bits/stdc++.h>
using namespace std;

float sum(float n)
{
    // Base condition
    if (n < 2)
        return 1;

    else
        return 1 / n + (sum(n - 1));
}

// Driven Code
int main()
{
    cout << (sum(8)) << endl;
    cout << (sum(10)) << endl;
    return 0;
}

// This code is contributed by
// Shashank_Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// harmonic series using recursion
import java.io.*;

class GFG
{

float sum(float n)
{
    // Base condition
    if (n < 2)
        return 1;

    else
        return 1 / n + (sum(n - 1));
}

// Driven Code
public static void main(String args[])
{
  GFG g = new GFG();
  System.out.println(g.sum(8));
  System.out.print(g.sum(10));
}
}

// This code is contributed by Shivi_Aggarwal
```

## 蟒蛇 3

```
# Python program to find sum of
# harmonic series using recursion

def sum(n):

    # Base condition
    if n < 2:
        return 1

    else:
        return 1 / n + (sum(n - 1))

print(sum(8))
print(sum(10))
```

## C#

```
//C# program to find sum of
// harmonic series using recursion
using System;

class GFG
{

static float sum(float n)
{
    // Base condition
    if (n < 2)
        return 1;

    else
        return 1 / n + (sum(n - 1));
}

// Driven Code
public static void Main()
{
    Console.WriteLine(sum(8));
    Console.WriteLine(sum(10));
}
}

// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// harmonic series using recursion

function sum($n)
{

    // Base condition
    if ($n < 2)
        return 1;

    else
        return 1 / $n + (sum($n - 1));
}

// Driver Code
echo sum(8) . "\n";
echo sum(10);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of
// harmonic series using recursion
function sum(n)
{

    // Base condition
    if (n < 2)
    {
        return 1
    }
    else
    {
        return 1 / n + (sum(n - 1))
    }
}

// Driver code
document.write(sum(8));
document.write("<br>");
document.write(sum(10));

// This code is contributed by bunnyram19

</script>
```

**Output:** 

```
2.7178571428571425
2.9289682539682538
```