# 求数列 1–1/2+1/3–1/4…1/N 之和的递归程序

> 原文:[https://www . geeksforgeeks . org/递归程序查找系列之和-1-1-2-1-3-1-4-1-n/](https://www.geeksforgeeks.org/recursive-program-to-find-the-sum-of-the-series-1-1-2-1-3-1-4-1-n/)

给定一个正整数 **N** ，任务是求数列 1 –( 1/2)+(1/3)–(1/4)+…。(1/N)使用[递归](https://www.geeksforgeeks.org/recursion/)。

**示例:**

> **输入:** N = 3
> **输出:**0.833333333333
> **解释:**
> 1 –( 1/2)+(1/3)= 0.83333333333333333
> 
> **输入:** N = 4
> **输出:**0.5833333333333
> **解释:**
> 1-(1/2)+(1/3)–(1/4)= 0.58333333333333333

**方法:**思路是形成递归案例和基本案例，以便使用递归解决这个问题。因此:

*   **基本情况:**这个问题的基本情况是我们已经计算了和直到分母中 N 的值。因此，当计数器变量‘I’达到值 n 时，我们停止递归。
*   **递归情况:**这个问题的递归情况是求分母是偶数还是奇数。这是因为，很明显，对于每个奇数，前面的符号是“+”，对于每个偶数，前面的符号是“-”。因此，我们检查计数器变量是偶数还是奇数，并相应地加减该值。然后，对值“I”的下一个值递归调用该函数。

下面是上述方法的实现:

## C++

```
// C++ program to find the value of
// the given series
#include<bits/stdc++.h>
using namespace std;

// Recursive program to find the
// value of the given series
float sumOfSeries(int i, int n, float s)
{
    // Base case
    if (i > n )
        return s;

    // Recursive case
    else
    {

        // If we are currently looking
        // at the even number
        if (i % 2 == 0)
            s -= (float)1 / i;

        // If we are currently looking
        // at the odd number
        else
            s+= (float)1 / i;
        return sumOfSeries(i + 1, n, s);
    }
}

// Driver code
int main()
{

    // cout<<sumOfSeries(1,3,0);
    float sum = sumOfSeries(1, 3, 0);
    printf("%f", sum);
    return 0;
}

// This code is contributed by Rohit_ranjan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the value of
// the given series
import java.util.*;

class GFG{

// Recursive program to find the
// value of the given series
static float sumOfSeries(int i, int n, float s)
{

    // Base case
    if (i > n)
        return s;

    // Recursive case
    else
    {

        // If we are currently looking
        // at the even number
        if (i % 2 == 0)
            s -= (float)1 / i;

        // If we are currently looking
        // at the odd number
        else
            s += (float)1 / i;

        return sumOfSeries(i + 1, n, s);
    }
}

// Driver code
public static void main(String[] args)
{
    float sum = sumOfSeries(1, 3, 0);

    System.out.printf("%f", sum);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python program to find the value of
# the given series

# Recursive program to find the
# value of the given series
def sumOfSeries(i, n, s) :

    # Base case
    if i>n :
        return s

    # Recursive case
    else :

        # If we are currently looking
        # at the even number
        if i % 2 == 0 :
            s-= 1 / i

        # If we are currently looking
        # at the odd number
        else :
            s+= 1 / i
        return sumOfSeries(i + 1, n, s)

# Driver code
if __name__ == "__main__":
    print(sumOfSeries(1, 3, 0))
```

## C#

```
// C# program to find the value of
// the given series
using System;
class GFG{

// Recursive program to find the
// value of the given series
static float sumOfSeries(int i, int n, float s)
{
    // Base case
    if (i > n )
        return s;

    // Recursive case
    else
    {

        // If we are currently looking
        // at the even number
        if (i % 2 == 0)
            s -= (float)1 / i;

        // If we are currently looking
        // at the odd number
        else
            s += (float)1 / i;
        return sumOfSeries(i + 1, n, s);
    }
}

// Driver code
public static void Main()
{
    float sum = sumOfSeries(1, 3, 0);
    Console.Write(sum);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find the
// value of the given series

// Recursive program to find the
// value of the given series
function sumOfSeries(i, n, s)
{

    // Base case
    if (i > n)
        return s;

    // Recursive case
    else
    {

        // If we are currently looking
        // at the even number
        if (i % 2 == 0)
            s -= 1 / i;

        // If we are currently looking
        // at the odd number
        else
            s += 1 / i;

        return sumOfSeries(i + 1, n, s);
    }
}

// Driver code
let sum = sumOfSeries(1, 3, 0);

document.write(sum);

// This code is contributed by sravan kumar G

</script>
```

**Output:** 

```
0.8333333333333333
```