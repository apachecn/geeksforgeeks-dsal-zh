# 使用直接公式

打印前 n 个斐波那契数

> 原文:[https://www . geesforgeks . org/print-first-n-Fibonacci-numbers-use-direct-formula/](https://www.geeksforgeeks.org/print-first-n-fibonacci-numbers-using-direct-formula/)

给定一个数字 n，任务是打印前 n 个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
先决条件:[打印前 n 个斐波那契数的程序|设置 1](https://www.geeksforgeeks.org/program-to-print-first-n-fibonacci-numbers/)

**示例:**

```
Input : 7
Output :0 1 1 2 3 5 8

Input : 5
Output :0 1 1 2 3
```

**n-th Fibonacci number =[(1+√5)<sup>【n】</sup>(1-【5】<sup>【n】</sup>]/【2】<sup>*</sup>**

下面是实现。

## C++

```
// C++ code to print fibonacci
// numbers till n using direct formula.
#include<bits/stdc++.h>
using namespace std;

// Function to calculate fibonacci
// using recurrence relation formula
void fibonacci(int n){
    long long int fib;
    for ( long long int i = 0; i < n; i++)
    {
        // Using direct formula
        fib = (pow((1 + sqrt(5)), i) -
               pow((1 - sqrt(5)), i)) /
              (pow(2, i) * sqrt(5));

        cout << fib << " ";
    }
}

// Driver code
int main()
{
    long long int n = 8;   
    fibonacci(n);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print fibonacci
// numbers till n using direct formula.

class GFG{

// Function to calculate fibonacci
// using recurrence relation formula
static void fibonacci(double n){
    double fib;
    for (double i = 0; i < n; i++)
    {
        // Using direct formula
        fib = (Math.pow((1 + Math.sqrt(5)), i) -
            Math.pow((1 - Math.sqrt(5)), i)) /
            (Math.pow(2, i) * Math.sqrt(5));

        System.out.print((int)fib+" ");
    }
}

// Driver code
public static void main(String[] args)
{
    double n = 8;
    fibonacci(n);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 code to print fibonacci
# numbers till n using direct formula.
import math

# Function to calculate fibonacci
# using recurrence relation formula
def fibonacci(n):

    for i in range(n):
        # Using direct formula
        fib = ((pow((1 + math.sqrt(5)), i) -
                pow((1 - math.sqrt(5)), i)) /
               (pow(2, i) * math.sqrt(5)));

        print(int(fib), end = " ");

# Driver code
n = 8;
fibonacci(n);

# This code is contributed by mits
```

## C#

```
// C#  code to print fibonacci
// numbers till n using direct formula.\

using System;

public class GFG{

// Function to calculate fibonacci
// using recurrence relation formula
static void fibonacci(double n){
    double fib;
    for (double i = 0; i < n; i++)
    {
        // Using direct formula
        fib = (Math.Pow((1 + Math.Sqrt(5)), i) -
            Math.Pow((1 - Math.Sqrt(5)), i)) /
            (Math.Pow(2, i) * Math.Sqrt(5));

        Console.Write((int)fib+" ");
    }
}

// Driver code
    static public void Main (){
            double n = 8;
            fibonacci(n);
}
}
// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to print fibonacci
// numbers till n using direct formula.

// Function to calculate fibonacci
// using recurrence relation formula
function fibonacci($n)
{
    for ($i = 0; $i < $n; $i++)
    {
        // Using direct formula
        $fib = (pow((1 + sqrt(5)), $i) -
                pow((1 - sqrt(5)), $i)) /
               (pow(2, $i) * sqrt(5));

        echo $fib , " ";
    }
}

// Driver code
$n = 8;
fibonacci($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript code to print fibonacci
// numbers till n using direct formula.

// Function to calculate fibonacci
// using recurrence relation formula
function fibonacci(n)
{
    var fib;
    for(i = 0; i < n; i++)
    {

        // Using direct formula
        fib = (Math.pow((1 + Math.sqrt(5)), i) -
               Math.pow((1 - Math.sqrt(5)), i)) /
           (Math.pow(2, i) * Math.sqrt(5));

        document.write(parseInt(fib) + " ");
    }
}

// Driver code
var n = 8;

fibonacci(n);

// This code is contributed by gauravrajput1

</script>
```

**Output:** 

```
0 1 1 2 3 5 8 13
```

**注意:**上述程序与[方法 1](https://www.geeksforgeeks.org/program-to-print-first-n-fibonacci-numbers/) 相比成本较高，因为它会导致浮点运算。此外，由于浮点精度错误，它可能无法完美工作。