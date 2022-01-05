# 模幂运算(递归)

> 原文:[https://www . geesforgeks . org/modular-幂运算-递归/](https://www.geeksforgeeks.org/modular-exponentiation-recursive/)

给定三个数字 a、b 和 c，我们需要找到(a <sup>b</sup> ) % c
现在为什么求幂后做“% c”，因为 a <sup>b</sup> 即使对于相对较小的 a、b 值也会非常大，这是一个问题，因为我们试图编码问题的语言的数据类型很可能不会让我们存储这么大的数字。
**例:**

```
Input : a = 2312 b = 3434 c = 6789
Output : 6343

Input : a = -3 b = 5 c = 89 
Output : 24
```

这个想法是基于以下属性。
**属性 1:**
(m * n) % p 有一个很有意思的属性:
(m * n) % p =((m % p) * (n % p)) % p
属性 2:
如果 b 是偶数:
(a ^ b) % c = ((a ^ b/2) * (a ^ b/2))%c？这就暗示了分治
如果 b 是奇数:
(a ^ b)% c =(a *(a ^( B- 1))% c
**属性 3:**
如果我们必须返回绝对值小于 y 的负数 x 的 mod:
那么(x + y) % y 就会做同样的把戏
**注:**
也是(a ^ b/2) * (a ^ b/2)的乘积

## C++

```
// Recursive C++ program to compute modular power
#include <bits/stdc++.h>
using namespace std;

int exponentMod(int A, int B, int C)
{
    // Base cases
    if (A == 0)
        return 0;
    if (B == 0)
        return 1;

    // If B is even
    long y;
    if (B % 2 == 0) {
        y = exponentMod(A, B / 2, C);
        y = (y * y) % C;
    }

    // If B is odd
    else {
        y = A % C;
        y = (y * exponentMod(A, B - 1, C) % C) % C;
    }

    return (int)((y + C) % C);
}

// Driver code
int main()
{
    int A = 2, B = 5, C = 13;
    cout << "Power is " << exponentMod(A, B, C);
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// Recursive C program to compute modular power
#include <stdio.h>

int exponentMod(int A, int B, int C)
{
    // Base cases
    if (A == 0)
        return 0;
    if (B == 0)
        return 1;

    // If B is even
    long y;
    if (B % 2 == 0) {
        y = exponentMod(A, B / 2, C);
        y = (y * y) % C;
    }

    // If B is odd
    else {
        y = A % C;
        y = (y * exponentMod(A, B - 1, C) % C) % C;
    }

    return (int)((y + C) % C);
}

// Driver program to test above functions
int main()
{
   int A = 2, B = 5, C = 13;
   printf("Power is %d", exponentMod(A, B, C));
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program
// to compute modular power
import java.io.*;

class GFG
{
static int exponentMod(int A,
                       int B, int C)
{

    // Base cases
    if (A == 0)
        return 0;
    if (B == 0)
        return 1;

    // If B is even
    long y;
    if (B % 2 == 0)
    {
        y = exponentMod(A, B / 2, C);
        y = (y * y) % C;
    }

    // If B is odd
    else
    {
        y = A % C;
        y = (y * exponentMod(A, B - 1,
                             C) % C) % C;
    }

    return (int)((y + C) % C);
}

// Driver Code
public static void main(String args[])
{
    int A = 2, B = 5, C = 13;
    System.out.println("Power is " +
                        exponentMod(A, B, C));
}
}

// This code is contributed
// by Swetank Modi.
```

## 蟒蛇 3

```
# Recursive Python program
# to compute modular power
def exponentMod(A, B, C):

    # Base Cases
    if (A == 0):
        return 0
    if (B == 0):
        return 1

    # If B is Even
    y = 0
    if (B % 2 == 0):
        y = exponentMod(A, B / 2, C)
        y = (y * y) % C

    # If B is Odd
    else:
        y = A % C
        y = (y * exponentMod(A, B - 1,
                             C) % C) % C
    return ((y + C) % C)

# Driver Code
A = 2
B = 5
C = 13
print("Power is", exponentMod(A, B, C))

# This code is contributed
# by Swetank Modi.
```

## C#

```
// Recursive C# program
// to compute modular power
class GFG
{
static int exponentMod(int A, int B, int C)
{

    // Base cases
    if (A == 0)
        return 0;
    if (B == 0)
        return 1;

    // If B is even
    long y;
    if (B % 2 == 0)
    {
        y = exponentMod(A, B / 2, C);
        y = (y * y) % C;
    }

    // If B is odd
    else
    {
        y = A % C;
        y = (y * exponentMod(A, B - 1,
                             C) % C) % C;
    }

    return (int)((y + C) % C);
}

// Driver Code
public static void Main()
{
    int A = 2, B = 5, C = 13;
    System.Console.WriteLine("Power is " +
                    exponentMod(A, B, C));
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to
// compute modular power
function exponentMod($A, $B, $C)
{
    // Base cases
    if ($A == 0)
        return 0;
    if ($B == 0)
        return 1;

    // If B is even
    if ($B % 2 == 0)
    {
        $y = exponentMod($A, $B / 2, $C);
        $y = ($y * $y) % $C;
    }

    // If B is odd
    else
    {
        $y = $A % $C;
        $y = ($y * exponentMod($A, $B - 1,
                               $C) % $C) % $C;
    }

    return (($y + $C) % $C);
}

// Driver Code
$A = 2;
$B = 5;
$C = 13;
echo "Power is " . exponentMod($A, $B, $C);

// This code is contributed
// by Swetank Modi.
?>
```

## java 描述语言

```
<script>

// Recursive Javascript program
// to compute modular power

// Function to check if a given
// quadilateral is valid or not
function exponentMod(A, B, C)
{

    // Base cases
    if (A == 0)
        return 0;
    if (B == 0)
        return 1;

    // If B is even
    var y;
    if (B % 2 == 0)
    {
        y = exponentMod(A, B / 2, C);
        y = (y * y) % C;
    }

    // If B is odd
    else
    {
        y = A % C;
        y = (y * exponentMod(A, B - 1,
                             C) % C) % C;
    }

    return parseInt(((y + C) % C));
}

// Driver code
var A = 2, B = 5, C = 13;
document.write("Power is " +
               exponentMod(A, B, C));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Power is 6
```

[**迭代模幂运算。**](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)