# 递归程序打印 n 个整数的 GCD 公式

> 原文:[https://www . geesforgeks . org/单行命令-gcd-n-integers/](https://www.geeksforgeeks.org/single-line-command-gcd-n-integers/)

给定一个函数 **gcd(a，b)** 求两个数的 gcd(最大公约数)。还知道三个元素的 gcd 可以通过 gcd(a，gcd(b，c))找到，同样对于四个元素它可以通过 gcd(a，gcd(b，gcd(c，d))找到 GCD。给定正整数 **n** 。任务是打印公式，使用给定的 gcd()函数找到 n 个整数的 GCD。
**例** :

```
Input : n = 3
Output : gcd(int, gcd(int, int))

Input : n = 5
Output : gcd(int, gcd(int, gcd(int, gcd(int, int))))
```

**方法:**思路是用递归打印单行命令。现在，要编写一个递归函数，比如 recursivefunn(n)，所需的字符串由 gcd(int，+recursivefunn(n–1)+)组成。这意味着递归函数(n)应该返回一个包含对自身调用的字符串，为了计算该值，递归函数将对 n–1 重新开始。这又会返回另一个调用 n–1 的字符串，直到 n == 1，递归函数返回字符串“int”。
以下是上述方法的实施:

## C++

```
// CPP Program to print single line command
// to find the GCD of n integers
#include <bits/stdc++.h>
using namespace std;

// Function to print single line command
// to find GCD of n elements.
string recursiveFun(int n)
{
    // base case
    if (n == 1)
        return "int";

    // Recursive Step
    return "gcd(int, " + recursiveFun(n - 1) + ")";
}

// Driver Program
int main()
{
    int n = 5;

    cout << recursiveFun(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print
// single line command to
// find the GCD of n integers
class GFG
{

// Function to print single
// line command to find GCD
// of n elements.
static String recursiveFun(int n)
{
    // base case
    if (n == 1)
        return "int";

    // Recursive Step
    return "gcd(int, " +
            recursiveFun(n - 1) + ")";
}

// Driver Code
public static void main(String [] arg)
{
    int n = 5;

    System.out.println(recursiveFun(n));
}
}

// This code is contributed
// by Smitha
```

## 蟒蛇 3

```
# Python 3 Program to print single line
# command to find the GCD of n integers

# Function to print single line command
# to find GCD of n elements.
def recursiveFun(n):

    # base case
    if (n == 1):
        return "int"

    # Recursive Step
    return "gcd(int, " + recursiveFun(n - 1) + ")"

# Driver Code
if __name__ == '__main__':
    n = 5
    print(recursiveFun(n))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# Program to print single
// line command to find the
// GCD of n integers
using System;
class GFG
{

// Function to print single
// line command to find GCD
// of n elements.
static String recursiveFun(int n)
{
    // base case
    if (n == 1)
        return "int";

    // Recursive Step
    return "gcd(int, " +
            recursiveFun(n - 1) + ")";
}

// Driver Code
public static void Main()
{
    int n = 5;

    Console.Write(recursiveFun(n));
}
}

// This code is contributed
// by smitha
```

## java 描述语言

```
<script>
// javascript Program to print
// single line command to
// find the GCD of n integers   
// Function to print single
    // line command to find GCD
    // of n elements.
    function recursiveFun(n)
    {

        // base case
        if (n == 1)
            return "int";

        // Recursive Step
        return "gcd(int, " + recursiveFun(n - 1) + ")";
    }

    // Driver Code
        var n = 5;

        document.write(recursiveFun(n));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
gcd(int, gcd(int, gcd(int, gcd(int, int))))
```

**时间复杂度:** O(N)，其中 N 为给定数。