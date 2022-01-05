# 平衡给定化学方程式的程序

> 原文:[https://www . geesforgeks . org/程序平衡给定的化学方程式/](https://www.geeksforgeeks.org/program-to-balance-the-given-chemical-equation/)

给定以下类型的简单化学方程式的值 **x，y，p，q**:
![b_{1}\text{ }A_{x} + b_{2}\text{ }B_{y} \rightarrow b_{3}\text{ }A_{p}B_{q}    ](img/36b407fac789503b6fbcab70d43073c6.png "Rendered by QuickLaTeX.com")
任务是找到常数**b<sub>1</sub>T8】**b<sub>2</sub>**， **b <sub>3</sub>** 的值，使得方程式两边平衡，且必须是简化形式。**

**示例:**

> **输入:** x = 2，y = 3，p = 4，q = 5
> **输出:** b1 = 6，b2 = 5，b3 = 3
> 
> **输入:** x = 1，y = 2，p = 3，q = 1
> **输出:** b1 = 6，b2 = 1，b3 = 2

**进场:**

1.检查 **p % x = 0 和 q % y = 0** 是否存在。

2.如果是，那么我们可以简单地说

```
b1 = p / x, 
b2 = q / y, and 
b3 = 1
```

3.否则我们需要使用 [gcd](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 来计算 b1，b2，b3。我们需要简化的形式，这样 gcd 就可以帮助它。

下面是上述方法的实现。

## C++

```
// C++ program to balance
// the given Chemical Equation
#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate b1, b2 and b3
void balance(int x, int y, int p, int q)
{
    // Variable declaration
    int b1, b2, b3;

    if (p % x == 0 && q % y == 0) {
        b1 = p / x;
        b2 = q / y;
        b3 = 1;
    }

    else {
        p = p * y;
        q = q * x;
        b3 = x * y;

        // temp variable to store gcd
        int temp = gcd(p, gcd(q, b3));

        // Computing GCD
        b1 = p / temp;
        b2 = q / temp;
        b3 = b3 / temp;
    }

    cout << b1 << " " << b2
         << " " << b3 << endl;
}

// Driver code
int main()
{
    int x = 2, y = 3, p = 4, q = 5;

    balance(x, y, p, q);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to balance
// the given Chemical Equation

import java.util.*;

class GFG{

// Function to calculate GCD
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate b1, b2 and b3
static void balance(int x, int y, int p, int q)
{
    // Variable declaration
    int b1, b2, b3;

    if (p % x == 0 && q % y == 0) {
        b1 = p / x;
        b2 = q / y;
        b3 = 1;
    }

    else {
        p = p * y;
        q = q * x;
        b3 = x * y;

        // temp variable to store gcd
        int temp = gcd(p, gcd(q, b3));

        // Computing GCD
        b1 = p / temp;
        b2 = q / temp;
        b3 = b3 / temp;
    }

    System.out.print(b1 + " " +  b2
        + " " +  b3 +"\n");
}

// Driver code
public static void main(String[] args)
{
    int x = 2, y = 3, p = 4, q = 5;

    balance(x, y, p, q);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to balance
# the given Chemical Equation

# Function to calculate GCD
def gcd(a,b):
    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to calculate b1, b2 and b3
def balance(x, y, p, q):

    # Variable declaration
    if (p % x == 0 and q % y == 0):
        b1 = p // x
        b2 = q // y
        b3 = 1

    else:
        p = p * y
        q = q * x
        b3 = x * y

        # temp variable to store gcd
        temp = gcd(p, gcd(q, b3))

        # Computing GCD
        b1 = p // temp
        b2 = q // temp
        b3 = b3 // temp

    print(b1,b2,b3)

# Driver code
if __name__ == '__main__':
    x = 2
    y = 3
    p = 4
    q = 5

    balance(x, y, p, q)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to balance
// the given Chemical Equation

using System;

public class GFG{

// Function to calculate GCD
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate b1, b2 and b3
static void balance(int x, int y, int p, int q)
{
    // Variable declaration
    int b1, b2, b3;

    if (p % x == 0 && q % y == 0) {
        b1 = p / x;
        b2 = q / y;
        b3 = 1;
    }

    else {
        p = p * y;
        q = q * x;
        b3 = x * y;

        // temp variable to store gcd
        int temp = gcd(p, gcd(q, b3));

        // Computing GCD
        b1 = p / temp;
        b2 = q / temp;
        b3 = b3 / temp;
    }

    Console.Write(b1 + " " + b2
                  + " " + b3 +"\n");
}

// Driver code
public static void Main(String[] args)
{
    int x = 2, y = 3, p = 4, q = 5;

    balance(x, y, p, q);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to balance
// the given Chemical Equation

// Function to calculate GCD
function gcd(a, b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate b1, b2 and b3
function balance(x, y, p, q)
{
    // Variable declaration
    let b1, b2, b3;

    if (p % x == 0 && q % y == 0) {
        b1 = p / x;
        b2 = q / y;
        b3 = 1;
    }

    else {
        p = p * y;
        q = q * x;
        b3 = x * y;

        // temp variable to store gcd
        let temp = gcd(p, gcd(q, b3));

        // Computing GCD
        b1 = p / temp;
        b2 = q / temp;
        b3 = b3 / temp;
    }

    document.write(b1 + " " +  b2
        + " " +  b3 +"\n");
}

// Driver Code

    let x = 2, y = 3, p = 4, q = 5;

    balance(x, y, p, q);

</script>
```

**Output:** 

```
6 5 3
```

时间复杂度:0(对数(最大值(a，b))

辅助空间:0(对数(最大值(a，b))