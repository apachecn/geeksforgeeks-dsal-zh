# 计算给定数的 MDAS 阶乘

> 原文:[https://www . geeksforgeeks . org/calculate-mdas-factorial-of-给定数字/](https://www.geeksforgeeks.org/calculate-mdas-factorial-of-given-number/)

给定一个整数 **N** ，任务是找到 MDAS 阶乘。
号 **N** 的一般因子由下式给出:

> 阶乘(N)=(N)*(N-1)*(N-2)*(N-3)*(N-4)*(N-5)*(N-6)*(N-7)-––-(3)*(2)*(1)。

在 MDAS 阶乘中，我们不是简单地将数字从 N 乘以 1，而是以如下所示的重复模式执行四个运算:乘法(*)、除法(/)、加法(+)和减法(-)操作:

> MDAS _ 阶乘(N)=(N)*(N-1)/(N-2)+(N-3)–(N-4)––––最多 1。

通过使用递减顺序的整数，我们将乘法操作交换为固定的旋转操作:乘法(*)、除法(/)、加法(+)和减法(-)以上述顺序进行。

**示例:**

```
Input : N = 4
Output : 7
Explanation : MDAS_Factorial(4) = 4 * 3 / 2 + 1 = 7

Input : N = 10
Output : 12
Explanation : 
MDAS_Factorial(10) = 10 * 9 / 8 + 7 - 6 * 5 / 4 + 3 - 2 * 1 = 12 
```

**简单方法:**想法是对每个操作周期(*，/，+，-)使用一个循环，并计算 N 的 MDAS 阶乘。但如果 N 非常大，这可能会运行缓慢。这种方法的时间复杂度为 0(N)。

**有效方法:**
如果我们仔细观察，可以得出结论:

1.  如果 N 小于或等于 2，那么答案就是 N 本身。
2.  如果 N 是 3 或 N 是 4，答案是 N + 3。
3.  如果(N–4)完全能被 4 整除，那么答案就是 N + 1。
4.  如果(N–4)在除以 4 时给出余数 1 或 2，则答案为 N + 2。
5.  对于剩余的值，答案将是 N–1。

下面是上述方法的实现

## C++

```
// C++ Program to find MDAS_Factorial
#include <bits/stdc++.h>
using namespace std;

// Program to find MDAS_factorial
int MDAS_Factorial(int N)
{
    if (N <= 2)
        return N;

    if (N <= 4)
        return (N + 3);

    if ((N - 4) % 4 == 0)
        return (N + 1);

    else if ((N - 4) % 4 <= 2)
        return (N + 2);

    else
        return (N - 1);
}

// Driver code
int main()
{

    int N = 4;
    cout << MDAS_Factorial(N) << endl;
    N = 10;
    cout << MDAS_Factorial(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find MDAS_Factorial
import java.util.*;

class Count {
    public static int MDAS_Factorial(int N)
    {
        if (N <= 2)
            return N;

        if (N <= 4)
            return (N + 3);

        if ((N - 4) % 4 == 0)
            return (N + 1);

        else if ((N - 4) % 4 <= 2)
            return (N + 2);

        else
            return (N - 1);
    }

    public static void main(String[] args)
    {
        int N = 4;
        System.out.println(MDAS_Factorial(N));

        N = 10;
        System.out.println(MDAS_Factorial(N));
    }
}
```

## 蟒蛇 3

```
# Python3 code find MDAS_Factorial
def MDAS_Factorial( N ):

    if N <= 2:
        return N

    if N <= 4:
        return N + 3

    if (N - 4) % 4 == 0:
        return N + 1

    elif (N - 4) % 4 <= 2:
         return N + 2

    else:
         return N - 1

# Driver code
N = 4 
print(MDAS_Factorial( N ) )

N = 10
print(MDAS_Factorial( N ) )
```

## C#

```
// C# program to find MDAS_Factorial
using System;

class Count {
    public static int MDAS_Factorial(int N)
    {
        if (N <= 2)
            return N;

        if (N <= 4)
            return (N + 3);

        if ((N - 4) % 4 == 0)
            return (N + 1);

        else if ((N - 4) % 4 <= 2)
            return (N + 2);

        else
            return (N - 1);
    }

    // Driver code
    public static void Main()
    {
        int N = 4;
        Console.WriteLine(MDAS_Factorial(N));

        N = 10;
        Console.WriteLine(MDAS_Factorial(N));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program
// Program to find MDAS_factorial
function MDAS_Factorial($N)
{
    if ($N <= 2)
          return N;

    if ($N <= 4)
          return ($N + 3);

    if (($N - 4) % 4 == 0)
          return ($N + 1);

    else if (($N - 4) % 4 <= 2)
          return ($N + 2);

    else
          return ($N - 1);
}

// Driver code
$N  = 4;
echo MDAS_Factorial($N);
echo("\n");
$N  = 10;
echo MDAS_Factorial($N);
?>
```

## java 描述语言

```
// Javascript Program
// Program to find MDAS_factorial
function MDAS_Factorial(N)
{
    if (N <= 2)
        return N;

    if (N <= 4)
        return (N + 3);

    if ((N - 4) % 4 == 0)
        return (N + 1);

    else if ((N - 4) % 4 <= 2)
        return (N + 2);

    else
        return (N - 1);
}

// Driver code
let N = 4;
document.write(MDAS_Factorial(N) + "<br>")
N = 10;
document.write(MDAS_Factorial(N));

// This code is contributed by gfgking
```

**输出:**

```
7
12
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)