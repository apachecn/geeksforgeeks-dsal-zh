# 第 n 个异或斐波那契数

> 原文:[https://www.geeksforgeeks.org/nth-xor-fibonacci-number/](https://www.geeksforgeeks.org/nth-xor-fibonacci-number/)

给定三个整数 **a** 、 **b** 和 **N** ，其中 **a** 和 **b** 是异或斐波那契数列的前两个项，任务是找到 **N <sup>第</sup>** 项。
异或斐波那契数列的第 n 项定义为**f(n)= f(n–1)^ f(n–2)**，其中 **^** 是按位异或。
**例:**

> **输入:** a = 1，b = 2，N = 5
> **输出:**3
> f(0)= 1
> f(1)= 2
> f(2)= 1 ^ 2 = 3
> f(3)= 2 ^ 3 = 1
> f(4)= 1 ^ 3 = 2
> f(5)= 1 ^ 2 = 3
> **输入:** a = 5，b = 11，n

**进场:**自， **a ^ a = 0** 并给出

> **F(0) =**

可以观察到，答案在每 **3** 个数字后重复一次。所以答案是 **F(N % 3)** 其中 **F(0) = a，F(1) = b 和 F(2) = a ^ b** 。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth XOR Fibonacci number
int nthXorFib(int n, int a, int b)
{
    if (n == 0)
        return a;
    if (n == 1)
        return b;
    if (n == 2)
        return (a ^ b);

    return nthXorFib(n % 3, a, b);
}

// Driver code
int main()
{
    int a = 1, b = 2, n = 10;

    cout << nthXorFib(n, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the
    // nth XOR Fibonacci number
    static int nthXorFib(int n, int a, int b)
    {
        if (n == 0)
            return a;
        if (n == 1)
            return b;
        if (n == 2)
            return (a ^ b);

        return nthXorFib(n % 3, a, b);
    }

    // Driver code
    public static void main (String[] args)
    {
        int a = 1, b = 2, n = 10;

        System.out.println(nthXorFib(n, a, b));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return
# the nth XOR Fibonacci number
def nthXorFib(n, a, b):
    if n == 0 :
        return a
    if n == 1 :
        return b
    if n == 2 :
        return a ^ b

    return nthXorFib(n % 3, a, b)

# Driver code
a = 1
b = 2
n = 10
print(nthXorFib(n, a, b))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the
    // nth XOR Fibonacci number
    static int nthXorFib(int n, int a, int b)
    {
        if (n == 0)
            return a;
        if (n == 1)
            return b;
        if (n == 2)
            return (a ^ b);

        return nthXorFib(n % 3, a, b);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int a = 1, b = 2, n = 10;

        Console.WriteLine(nthXorFib(n, a, b));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the nth XOR Fibonacci number
function nthXorFib(n, a, b)
{
    if (n == 0)
        return a;
    if (n == 1)
        return b;
    if (n == 2)
        return (a ^ b);

    return nthXorFib(n % 3, a, b);
}

// Driver code
    let a = 1, b = 2, n = 10;

    document.write(nthXorFib(n, a, b));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(1)