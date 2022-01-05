# 自定义斐波那契数列的第 n 项

> 原文:[https://www . geesforgeks . org/n-自定义术语-斐波那契数列/](https://www.geeksforgeeks.org/nth-term-of-a-custom-fibonacci-series/)

给定三个整数 **A** 、 **B** 和 **N** 。自定义斐波那契数列定义为**F(x)= F(x–1)+F(x+1)**，其中 F(1) = A，F(2) = B，现在的任务是找到这个数列的 **N <sup>第</sup>** 项。
**示例:**

> **输入:** A = 10，B = 17，N = 3
> **输出:** 7
> 10，17，7，-10，-17，…
> **输入:** A = 50，B = 12，N = 10
> **输出:** -50

**进场:**可以观察到该系列会像 **A、B、B–A、-A、-B、A–B、A、B、B–A、…**T4 一样进行下去【下图为上述进场的实施:

## C++

```
// C++ implementation of the Custom Fibonacci series

#include <bits/stdc++.h>
using namespace std;

// Function to return the nth term
// of the required sequence
int nth_term(int a, int b, int n)
{
    int z = 0;
    if (n % 6 == 1)
        z = a;
    else if (n % 6 == 2)
        z = b;
    else if (n % 6 == 3)
        z = b - a;
    else if (n % 6 == 4)
        z = -a;
    else if (n % 6 == 5)
        z = -b;
    if (n % 6 == 0)
        z = -(b - a);
    return z;
}

// Driver code
int main()
{
    int a = 10, b = 17, n = 3;

    cout << nth_term(a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// Custom Fibonacci series
class GFG
{

// Function to return the nth term
// of the required sequence
static int nth_term(int a, int b, int n)
{
    int z = 0;
    if (n % 6 == 1)
        z = a;
    else if (n % 6 == 2)
        z = b;
    else if (n % 6 == 3)
        z = b - a;
    else if (n % 6 == 4)
        z = -a;
    else if (n % 6 == 5)
        z = -b;
    if (n % 6 == 0)
        z = -(b - a);
    return z;
}

// Driver code
public static void main(String[] args)
{
    int a = 10, b = 17, n = 3;

    System.out.println(nth_term(a, b, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the
# Custom Fibonacci series

# Function to return the nth term
# of the required sequence
def nth_term(a, b, n):
    z = 0
    if (n % 6 == 1):
        z = a
    elif (n % 6 == 2):
        z = b
    elif (n % 6 == 3):
        z = b - a
    elif (n % 6 == 4):
        z = -a
    elif (n % 6 == 5):
        z = -b
    if (n % 6 == 0):
        z = -(b - a)
    return z

# Driver code
if __name__ == '__main__':
    a = 10
    b = 17
    n = 3

    print(nth_term(a, b, n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the
// Custom Fibonacci series
using System;

class GFG
{

// Function to return the nth term
// of the required sequence
static int nth_term(int a, int b, int n)
{
    int z = 0;
    if (n % 6 == 1)
        z = a;
    else if (n % 6 == 2)
        z = b;
    else if (n % 6 == 3)
        z = b - a;
    else if (n % 6 == 4)
        z = -a;
    else if (n % 6 == 5)
        z = -b;
    if (n % 6 == 0)
        z = -(b - a);
    return z;
}

// Driver code
static public void Main ()
{
    int a = 10, b = 17, n = 3;

    Console.Write(nth_term(a, b, n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
// javascript implementation of the
// Custom Fibonacci series   

// Function to return the nth term
    // of the required sequence
    function nth_term(a , b , n)
    {
        var z = 0;
        if (n % 6 == 1)
            z = a;
        else if (n % 6 == 2)
            z = b;
        else if (n % 6 == 3)
            z = b - a;
        else if (n % 6 == 4)
            z = -a;
        else if (n % 6 == 5)
            z = -b;
        if (n % 6 == 0)
            z = -(b - a);
        return z;
    }

    // Driver code
    var a = 10, b = 17, n = 3;
    document.write(nth_term(a, b, n));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
7
```