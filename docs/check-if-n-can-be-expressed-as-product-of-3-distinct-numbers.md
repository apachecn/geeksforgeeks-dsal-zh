# 检查 N 是否可以表示为 3 个不同数字的乘积

> 原文:[https://www . geesforgeks . org/check-if-n-can-express-as-product-of-3-distinct-numbers/](https://www.geeksforgeeks.org/check-if-n-can-be-expressed-as-product-of-3-distinct-numbers/)

给定一个数字 **N** 。打印三个不同的数字 **( > =1)** ，如果找不到三个数字，则打印-1。
**例:**

> **输入:** 64
> **输出:** 2 4 8
> **解释:**
> (2*4*8 = 64)
> **输入:** 24
> **输出:** 2 3 4
> **解释:**
> (2*3*4 = 24)
> **输入:** 12
> **输出:…**

**进场:**

1.  使用本文中讨论的方法，创建一个存储给定数的所有除数的数组
2.  让三个数字 a，b，c 初始化为 1
3.  遍历除数数组并检查以下条件:
    *   a 的值=除数数组第一个索引处的值。
    *   b 的值=除数数组第二和第三个索引处的值的乘积。如果除数数组只有一个或两个元素，那么不存在这样的三元组
    *   找到 a & b 后，c 的值=除数数组中其余所有元素的乘积。
4.  检查最终条件，使 a、b、c 的值必须不同且不等于 1。

下面是实现代码:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the
// three numbers
#include "bits/stdc++.h"
using namespace std;

// function to find 3 distinct number
// with given product
void getnumbers(int n)
{
    // Declare a vector to store
    // divisors
    vector<int> divisor;

    // store all divisors of number
    // in array
    for (int i = 2; i * i <= n; i++) {

        // store all the occurence of
        // divisors
        while (n % i == 0) {
            divisor.push_back(i);
            n /= i;
        }
    }

    // check if n is not equals to -1
    // then n is also a prime factor
    if (n != 1) {
        divisor.push_back(n);
    }

    // Initialize the variables with 1
    int a, b, c, size;
    a = b = c = 1;
    size = divisor.size();

    for (int i = 0; i < size; i++) {

        // check for first number a
        if (a == 1) {
            a = a * divisor[i];
        }

        // check for second number b
        else if (b == 1 || b == a) {
            b = b * divisor[i];
        }

        // check for third number c
        else {
            c = c * divisor[i];
        }
    }

    // check for all unwanted condition
    if (a == 1 || b == 1 || c == 1
        || a == b || b == c || a == c) {
        cout << "-1" << endl;
    }
    else {
        cout << a << ' ' << b
             << ' ' << c << endl;
    }
}

// Driver function
int main()
{
    int n = 64;
    getnumbers(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// three numbers
import java.util.*;

class GFG{

// function to find 3 distinct number
// with given product
static void getnumbers(int n)
{
    // Declare a vector to store
    // divisors
    Vector<Integer> divisor = new Vector<Integer>();

    // store all divisors of number
    // in array
    for (int i = 2; i * i <= n; i++) {

        // store all the occurence of
        // divisors
        while (n % i == 0) {
            divisor.add(i);
            n /= i;
        }
    }

    // check if n is not equals to -1
    // then n is also a prime factor
    if (n != 1) {
        divisor.add(n);
    }

    // Initialize the variables with 1
    int a, b, c, size;
    a = b = c = 1;
    size = divisor.size();

    for (int i = 0; i < size; i++) {

        // check for first number a
        if (a == 1) {
            a = a * divisor.get(i);
        }

        // check for second number b
        else if (b == 1 || b == a) {
            b = b * divisor.get(i);
        }

        // check for third number c
        else {
            c = c * divisor.get(i);
        }
    }

    // check for all unwanted condition
    if (a == 1 || b == 1 || c == 1
        || a == b || b == c || a == c) {
        System.out.print("-1" +"\n");
    }
    else {
        System.out.print(a +" "+ b
                +" "+ c +"\n");
    }
}

// Driver function
public static void main(String[] args)
{
    int n = 64;
    getnumbers(n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the
# three numbers

# function to find 3 distinct number
# with given product
def getnumbers(n):

     # Declare a vector to store
    # divisors
    divisor = []

    # store all divisors of number
    # in array
    for i in range(2, n + 1):

        # store all the occurence of
        # divisors
        while (n % i == 0):
            divisor.append(i)
            n //= i

    # check if n is not equals to -1
    # then n is also a prime factor
    if (n != 1):
        divisor.append(n)

    # Initialize the variables with 1
    a, b, c, size = 0, 0, 0, 0
    a = b = c = 1
    size = len(divisor)

    for i in range(size):

        # check for first number a
        if (a == 1):
            a = a * divisor[i]

        # check for second number b
        elif (b == 1 or b == a):
            b = b * divisor[i]

        # check for third number c
        else:
            c = c * divisor[i]

    # check for all unwanted condition
    if (a == 1 or b == 1 or c == 1
        or a == b or b == c or a == c):
        print("-1")
    else:
        print(a, b, c)

# Driver function

n = 64
getnumbers(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the
// three numbers
using System;
using System.Collections.Generic;

class GFG{

// function to find 3 distinct number
// with given product
static void getnumbers(int n)
{
    // Declare a vector to store
    // divisors
    List<int> divisor = new List<int>();

    // store all divisors of number
    // in array
    for (int i = 2; i * i <= n; i++) {

        // store all the occurence of
        // divisors
        while (n % i == 0) {
            divisor.Add(i);
            n /= i;
        }
    }

    // check if n is not equals to -1
    // then n is also a prime factor
    if (n != 1) {
        divisor.Add(n);
    }

    // Initialize the variables with 1
    int a, b, c, size;
    a = b = c = 1;
    size = divisor.Count;

    for (int i = 0; i < size; i++) {

        // check for first number a
        if (a == 1) {
            a = a * divisor[i];
        }

        // check for second number b
        else if (b == 1 || b == a) {
            b = b * divisor[i];
        }

        // check for third number c
        else {
            c = c * divisor[i];
        }
    }

    // check for all unwanted condition
    if (a == 1 || b == 1 || c == 1
        || a == b || b == c || a == c) {
        Console.Write("-1" +"\n");
    }
    else {
        Console.Write(a +" "+ b
                +" "+ c +"\n");
    }
}

// Driver function
public static void Main(String[] args)
{
    int n = 64;
    getnumbers(n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the
// three numbers

// function to find 3 distinct number
// with given product
function getnumbers(n)
{
    // Declare a vector to store
    // divisors
    let divisor = [];

    // store all divisors of number
    // in array
    for (let i = 2; i * i <= n; i++) {

        // store all the occurence of
        // divisors
        while (n % i == 0) {
            divisor.push(i);
            n = Math.floor(n/i);
        }
    }

    // check if n is not equals to -1
    // then n is also a prime factor
    if (n != 1) {
        divisor.push(n);
    }

    // Initialize the variables with 1
    let a, b, c, size;
    a = b = c = 1;
    size = divisor.length;

    for (let i = 0; i < size; i++) {

        // check for first number a
        if (a == 1) {
            a = a * divisor[i];
        }

        // check for second number b
        else if (b == 1 || b == a) {
            b = b * divisor[i];
        }

        // check for third number c
        else {
            c = c * divisor[i];
        }
    }

    // check for all unwanted condition
    if (a == 1 || b == 1 || c == 1
        || a == b || b == c || a == c) {
        document.write("-1" +"<br>");
    }
    else {
        document.write(a +" "+ b
                +" "+ c +"<br>");
    }
}

// Driver function
let n = 64;
getnumbers(n);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2 4 8
```

**时间复杂度:** O( **(log N)*sqrt(N)** )

**辅助空间:** O(sqrt(n))