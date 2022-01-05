# 一个数的超数

> 原文:[https://www.geeksforgeeks.org/hyperfactorial-of-a-number/](https://www.geeksforgeeks.org/hyperfactorial-of-a-number/)

给定一个数，任务是找到一个数的超导数。
给定数量的从 1 到给定数量的连续整数相乘的结果，每个整数的幂都被称为一个数的**超工厂**。

```
H(n)= 1 ^ 1 * 2 ^ 2 * 3 ^ 3 * . . . . . * n ^ n
```

**示例:**

> **输入:**2
> T3】输出: 4
> 
> **输入:** 4
> **输出:**27648
> h(4)= 1^1 * 2^2 * 3^3 * 4^4 = 27648

一种简单的方法是使用两个循环，一个寻找 i^i 的和，另一个寻找 i^i.，但是时间复杂度是 O(n)。
一种**高效的方法**是使用内置的 [pow()](https://www.geeksforgeeks.org/power-function-cc/) 函数或 [O(log n)方法](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/)找到 i^i，然后添加它。
以下是上述办法的实施情况。

## C++

```
/// C++ program to find the hyperfactorial
// of a number
#include <bits/stdc++.h>

using namespace std;
#define ll long long

// function to calculate the value of hyperfactorial
ll boost_hyperfactorial(ll num)
{
    // initialise the val to 1
    ll val = 1;
    for (int i = 1; i <= num; i++) {
        val = val * pow(i,i);
    }
    // returns the hyperfactorial of a number
    return val;
}

// Driver code
int main()
{
    int num = 5;
    cout << boost_hyperfactorial(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// hyperfactorial of a number

// function to calculate the
// value of hyperfactorial
class GFG
{
static long boost_hyperfactorial(long num)
{
    // initialise the val to 1
    long val = 1;
    for (int i = 1; i <= num; i++)
    {
        val = val * (long)Math.pow(i, i);
    }

    // returns the hyperfactorial
    // of a number
    return val;
}

// Driver code
public static void main(String args[])
{
    int num = 5;
    System.out.println(boost_hyperfactorial(num));
}
}

// This code is contributed
// by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find the
# hyperfactorial of a number

# function to calculate the
# value of hyperfactorial
def boost_hyperfactorial(num):

    # initialise the
    # val to 1
    val = 1;
    for i in range(1, num + 1):
        val = val * pow(i, i);

    # returns the hyperfactorial
    # of a number
    return val;

# Driver code
num = 5;
print(boost_hyperfactorial(num));

# This code is contributed
# by mits
```

## C#

```
// C# program to find the
// hyperfactorial of a number
using System;

class GFG
{

// function to calculate the
// value of hyperfactorial
static long boost_hyperfactorial(long num)
{
    // initialise the val to 1
    long val = 1;
    for (long i = 1; i <= num; i++)
    {
        val = val * (long)Math.Pow(i, i);
    }

    // returns the hyperfactorial
    // of a number
    return val;
}

// Driver code
public static void Main()
{
    int num = 5;
    Console.WriteLine(boost_hyperfactorial(num));
}
}

// This code is contributed
// by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// hyperfactorial of a number

// function to calculate the
// value of hyperfactorial
function boost_hyperfactorial($num)
{
    // initialise the
    // val to 1
    $val = 1;
    for ($i = 1; $i <= $num; $i++)
    {
        $val = $val * pow($i, $i);
    }

    // returns the hyperfactorial
    // of a number
    return $val;
}

// Driver code
$num = 5;
echo boost_hyperfactorial($num);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// hyperfactorial of a number

// function to calculate the
// value of hyperfactorial
function boost_hyperfactorial(num)
{
    // initialise the
    // val to 1
    let val = 1;
    for (let i = 1; i <= num; i++)
    {
        val = val * Math.pow(i, i);
    }

    // returns the hyperfactorial
    // of a number
    return val;
}

// Driver code
let num = 5;
document.write(boost_hyperfactorial(num));

// This code is contributed
// by gfgking

</script>
```

**Output:** 

```
86400000
```

**时间复杂度:** O(N * log N)
由于数字的超阶乘可能很大，因此数字会溢出。我们可以用 C++中的 [boost 库](https://www.geeksforgeeks.org/advanced-c-boost-library/)或者 Java 中的[big integer](https://www.geeksforgeeks.org/biginteger-class-in-java/)来存储一个数 n 的超阶乘。

## C++

```
// C++ program to find the hyperfactorial
// of a number using boost libraries
#include <bits/stdc++.h>
#include <boost/multiprecision/cpp_int.hpp>

using namespace boost::multiprecision;
using namespace std;

// function to calculate the value of hyperfactorial
int1024_t boost_hyperfactorial(int num)
{
    // initialise the val to 1
    int1024_t val = 1;
    for (int i = 1; i <= num; i++) {
        for (int j = 1; j <= i; j++) {
            // 1^1*2^2*3^3....
            val *= i;
        }
    }
    // returns the hyperfactorial of a number
    return val;
}

// Driver code
int main()
{
    int num = 5;
    cout << boost_hyperfactorial(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the hyperfactorial
// of a number using boost libraries

import java.io.*;

class GFG {

// function to calculate the value of hyperfactorial
static int boost_hyperfactorial(int num)
{
    // initialise the val to 1
    int val = 1;
    for (int i = 1; i <= num; i++) {
        for (int j = 1; j <= i; j++) {
            // 1^1*2^2*3^3....
            val *= i;
        }
    }
    // returns the hyperfactorial of a number
    return val;
}

// Driver code

    public static void main (String[] args) {
    int num = 5;
    System.out.println( boost_hyperfactorial(num));
    }
}
// This code is contributed
// by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find the hyperfactorial
# of a number using boost libraries

# function to calculate the value of hyperfactorial
def boost_hyperfactorial(num):

    # initialise the val to 1
    val = 1;
    for i in range(1,num+1):
        for j in range(1,i+1):

            # 1^1*2^2*3^3....
            val *= i;

    # returns the hyperfactorial of a number
    return val;

# Driver code
num = 5;
print( boost_hyperfactorial(num));

# This code is contributed by mits
```

## C#

```
// C# program to find the hyperfactorial
// of a number using boost libraries
using System;

class GFG
{

// function to calculate the
// value of hyperfactorial
static int boost_hyperfactorial(int num)
{
    // initialise the val to 1
    int val = 1;
    for (int i = 1; i <= num; i++)
    {
        for (int j = 1; j <= i; j++)
        {
            // 1^1*2^2*3^3....
            val *= i;
        }
    }

    // returns the hyperfactorial
    // of a number
    return val;
}

// Driver code
public static void Main ()
{
    int num = 5;
    Console.WriteLine(boost_hyperfactorial(num));
}
}

// This code is contributed
// by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the hyperfactorial
// of a number using boost libraries

// function to calculate the value
// of hyperfactorial
function boost_hyperfactorial($num)
{
    // initialise the val to 1
    $val = 1;
    for ($i = 1; $i <= $num; $i++)
    {
        for ($j = 1; $j <= $i; $j++)
        {
            // 1^1*2^2*3^3....
            $val *= $i;
        }
    }

    // returns the hyperfactorial
    // of a number
    return $val;
}

// Driver code
$num = 5;
echo boost_hyperfactorial($num);

// This code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>

// Javascript program to find the hyperfactorial
// of a number using boost libraries

// function to calculate the value of hyperfactorial
function boost_hyperfactorial(num)
{
    // initialise the val to 1
    var val = 1;
    for (var i = 1; i <= num; i++) {
        for (var j = 1; j <= i; j++) {
            // 1^1*2^2*3^3....
            val *= i;
        }
    }
    // returns the hyperfactorial of a number
    return val;
}

// Driver code
var num = 5;
document.write( boost_hyperfactorial(num));

</script>
```

**Output:** 

```
86400000
```