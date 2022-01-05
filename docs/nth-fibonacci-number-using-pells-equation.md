# 使用佩尔方程的第 n 个斐波那契数

> 原文:[https://www . geesforgeks . org/n th-Fibonacci-number-using-pells-equation/](https://www.geeksforgeeks.org/nth-fibonacci-number-using-pells-equation/)

给定一个整数 **N** ，任务是找到**N<sup>th</sup>T5[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。** 

> **输入:** N = 13
> **输出:** 144
> **输入:** N = 19
> **输出:** 2584

**方法:**利用[佩尔方程](https://www.geeksforgeeks.org/pell-number/)的根可以找到**N<sup>th</sup>T5【斐波那契数。佩尔斯方程一般形式为**(x<sup>2</sup>)–n(y<sup>2</sup>)= | 1 |**。
这里考虑 **y <sup>2</sup> = x，n = 1** 。另外，在右侧取正值(+1)。
现在方程变成**x<sup>2</sup>–x = 1**，与 **x <sup>2</sup> 相同–x–1 = 0**。
这里，**{ x =(p<sup>I</sup>–q<sup>I</sup>)/(p–q)}**被称为斐波那契数列的**N<sup>th</sup>T38】项，其中**I = N–1**和 **(p，q)** 是佩尔方程的根。**** 

> 求一般二次方程的根(a*x <sup>2</sup> + b*x + c = 0)。
> x1 =[-b+ math . sqrt(b<sup>2</sup>–4 * a * c)]/2 * a
> x2 =[-b–math . sqrt(b<sup>2</sup>–4 * a * c)]/2 * a
> 即
> p =(1+math . sqrt(5))/2
> q =(1–math . sqrt(5))/2

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// nth fibonacci number
int fib(int n)
{
    // Assign roots of the pell's
    // equation to p and q
    double p = ((1 + sqrt(5)) / 2);
    double q = ((1 - sqrt(5)) / 2);
    int i = n - 1;
    int x = (int) ((pow(p, i) -
                    pow(q, i)) / (p - q));
    return x;
}

// Driver code
int main()
{
    int n = 5;
    cout << fib(n);
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Assign roots of the pell's
// equation to p and q
static double p = ((1 + Math.sqrt(5)) / 2);
static double q = ((1 - Math.sqrt(5)) / 2);

// Function to return the
// nth fibonacci number
static int fib(int n)
{
    int i = n - 1;
    int x = (int) ((Math.pow(p, i) -
                    Math.pow(q, i)) / (p - q));
    return x;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    System.out.println(fib(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Assign roots of the pell's
# equation to p and q
p = (1 + math.sqrt(5)) / 2
q = (1 - math.sqrt(5)) / 2

# Function to return the
# nth fibonacci number
def fib(n):
    i = n - 1
    x = (p**i - q**i) / (p - q)
    return int(x)

# Driver code
n = 5
print(fib(n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Assign roots of the pell's
// equation to p and q
static double p = ((1 + Math.Sqrt(5)) / 2);
static double q = ((1 - Math.Sqrt(5)) / 2);

// Function to return the
// nth fibonacci number
static int fib(int n)
{
    int i = n - 1;
    int x = (int) ((Math.Pow(p, i) -
                    Math.Pow(q, i)) / (p - q));
    return x;
}

// Driver code
static public void Main ()
{
    int n = 5;
    Console.Write(fib(n));
}
}

// This code is contributed by @ajit..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// nth fibonacci number
function fib(n)
{
    // Assign roots of the pell's
    // equation to p and q
    let p = ((1 + Math.sqrt(5)) / 2);
    let q = ((1 - Math.sqrt(5)) / 2);
    let i = n - 1;
    let x = parseInt((Math.pow(p, i) -
                    Math.pow(q, i)) / (p - q));
    return x;
}

// Driver code
    let n = 5;
    document.write(fib(n));

</script>
```

**Output:** 

```
3
```