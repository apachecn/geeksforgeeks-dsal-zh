# 斐波那契数列中给定范围内数字总和的最后一位数字

> 原文:[https://www . geesforgeks . org/斐波那契数列中给定范围内数字总和的最后一位数字/](https://www.geeksforgeeks.org/last-digit-of-sum-of-numbers-in-the-given-range-in-the-fibonacci-series/)

给定两个非负整数 **M，N** ，表示 M ≤ N 的范围【M，N】，任务是求**F<sub>M</sub>+F<sub>M+1</sub>……+F<sub>N</sub>T9】的和的最后一位，其中 F <sub>K</sub> 是[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)中的 K <sup>第</sup>个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。** 

> 0、1、1、2、3、5、8、13、21、34、55、89、144……

**例:**

> **输入:** M = 3，N = 9
> **输出:** 6
> **解释:**
> 我们需要找到 F<sub>3</sub>+F<sub>4</sub>+F<sub>5</sub>+F<sub>6</sub>+F<sub>7</sub>+F<sub>8</sub>+F<sub>9</sub>
> =>
> 很明显，总和的最后一位数字是 6。
> **输入:** M = 3，N = 7
> **输出:** 1
> **解释:**
> 我们需要找到 F<sub>3</sub>+F<sub>4</sub>+F<sub>5</sub>+F<sub>6</sub>+F<sub>7</sub>
> =>2+3+5+8+13 = 0
> 很明显，总和的最后一位是 1。

**天真法:**这个问题的天真法是一个接一个地求出所有 K <sup>第</sup>个斐波那契数的和，其中 K 位于范围【M，N】内，最后返回和的最后一位数字。这种方法的时间复杂度是 **O(N)** 并且这种方法对于 N 的高阶值是失败的。
**有效方法:**解决这个问题的有效方法是使用[皮萨诺周期](https://www.geeksforgeeks.org/fibonacci-number-modulo-m-and-pisano-period/)的概念。

*   其思想是分别计算**(M–1)**和 **N** 斐波那契数之和，并减去计算值的最后一位。
*   这是因为 K 位于范围**【M，N】**内的所有 K <sup>个</sup>斐波那契数之和的最后一位等于范围**【0，N】**内的所有 K <sup>个</sup>个斐波那契数之和的最后一位与范围**【0，M–1】**内的所有 K <sup>个</sup>个斐波那契数之和的差。
*   这些值可以分别用皮萨诺周期的概念在很短的时间内计算出来。
*   让我们了解一下比萨诺时期是如何运作的。下表说明了前 10 个斐波那契数以及对这些数进行模 2 时获得的值。

<figure class="table">

| 我 | Zero | one | Two | three | four | five | six | seven | eight | nine | Ten |
| F <sub>i</sub> | Zero | one | one | Two | three | five | eight | Thirteen | Twenty-one | Thirty-four | Fifty-five |
| f<sub>和</sub>对 2 | Zero | one | one | Zero | one | one | Zero | one | one | Zero | Ten |

</figure>

*   显然，(F <sub>i</sub> mod 2)的 Pisano 周期是 3，因为 011 自身重复，长度(011) = 3。
*   现在，让我们观察以下身份:

> 7 = 2 * 3 + 1
> 被除数=(商×除数)+余数
> =>F<sub>7</sub>mod 2 = F<sub>1</sub>mod 2 = 1。

*   因此，我们不计算范围**【0，N】**中所有数字之和的最后一位，而是简单地计算该和，直到给定 F <sub>i</sub> mod 10 的 Pisano 周期为 60 的余数。

以下是上述方法的实现:

## C++

```
// C++ program to calculate
// last digit of the sum of the
// fibonacci numbers from M to N
#include<bits/stdc++.h>
using namespace std;

// Calculate the sum of the first
// N Fibonacci numbers using Pisano
// period
long long fib(long long n)
{

    // The first two Fibonacci numbers
    long long f0 = 0;
    long long f1 = 1;

    // Base case
    if (n == 0)
        return 0;
    if (n == 1)
        return 1;
    else
    {
        // Pisano period for % 10 is 60
        long long rem = n % 60;

        // Checking the remainder
        if(rem == 0)
           return 0;

        // The loop will range from 2 to
        // two terms after the remainder
        for(long long i = 2; i < rem + 3; i++)
        {
           long long f = (f0 + f1) % 60;
           f0 = f1;
           f1 = f;
        }

        long long s = f1 - 1;
        return s;
    }
}

// Driver Code
int main()
{
    long long m = 10087887;
    long long n = 2983097899;

    long long final = abs(fib(n) - fib(m - 1));
    cout << final % 10 << endl;
}

// This code is contributed by Bhupendra_Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// last digit of the sum of the
// fibonacci numbers from M to N
import java.util.*;

class GFG{

// Calculate the sum of the first
// N Fibonacci numbers using Pisano
// period
static int fib(long n)
{

    // The first two Fibonacci numbers
    int f0 = 0;
    int f1 = 1;

    // Base case
    if (n == 0)
        return 0;
    if (n == 1)
        return 1;
    else
    {

        // Pisano period for % 10 is 60
        int rem = (int) (n % 60);

        // Checking the remainder
        if(rem == 0)
        return 0;

        // The loop will range from 2 to
        // two terms after the remainder
        for(int i = 2; i < rem + 3; i++)
        {
           int f = (f0 + f1) % 60;
           f0 = f1;
           f1 = f;
        }

        int s = f1 - 1;
        return s;
    }
}

// Driver Code
public static void main(String args[])
{
    int m = 10087887;
    long n = 2983097899L;
    int Final = (int)Math.abs(fib(n) -
                              fib(m - 1));

    System.out.println(Final % 10);
}
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to calculate
# Last Digit of the sum of the
# Fibonacci numbers from M to N

# Calculate the sum of the first
# N Fibonacci numbers using Pisano
# period
def fib(n):

    # The first two Fibonacci numbers
    f0 = 0
    f1 = 1

    # Base case
    if (n == 0):
        return 0
    if (n == 1):
        return 1
    else:

        # Pisano Period for % 10 is 60
        rem = n % 60

        # Checking the remainder
        if(rem == 0):
            return 0

        # The loop will range from 2 to
        # two terms after the remainder
        for i in range(2, rem + 3):
            f =(f0 + f1)% 60
            f0 = f1
            f1 = f

        s = f1-1
        return(s)

# Driver code
if __name__ == '__main__':

    m = 10087887
    n = 2983097899

    final = fib(n)-fib(m-1)

    print(final % 10)
```

## C#

```
// C# program to calculate
// last digit of the sum of the
// fibonacci numbers from M to N
using System;

class GFG{

// Calculate the sum of the first
// N fibonacci numbers using Pisano
// period
static int fib(long n)
{

    // The first two fibonacci numbers
    int f0 = 0;
    int f1 = 1;

    // Base case
    if (n == 0)
        return 0;
    if (n == 1)
        return 1;
    else
    {

        // Pisano period for % 10 is 60
        int rem = (int)(n % 60);

        // Checking the remainder
        if(rem == 0)
           return 0;

        // The loop will range from 2 to
        // two terms after the remainder
        for(int i = 2; i < rem + 3; i++)
        {
           int f = (f0 + f1) % 60;
           f0 = f1;
           f1 = f;
        }

        int s = f1 - 1;
        return s;
    }
}

// Driver Code
public static void Main()
{
    int m = 10087887;
    long n = 2983097899L;
    int Final = (int)Math.Abs(fib(n) -
                              fib(m - 1));

    Console.WriteLine(Final % 10);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript program to calculate
// last digit of the sum of the
// fibonacci numbers from M to N

    // Calculate the sum of the first
    // N Fibonacci numbers using Pisano
    // period
    function fib(n) {

        // The first two Fibonacci numbers
        var f0 = 0;
        var f1 = 1;

        // Base case
        if (n == 0)
            return 0;
        if (n == 1)
            return 1;
        else {

            // Pisano period for % 10 is 60
            var rem = parseInt( (n % 60));

            // Checking the remainder
            if (rem == 0)
                return 0;

            // The loop will range from 2 to
            // two terms after the remainder
            for (i = 2; i < rem + 3; i++) {
                var f = (f0 + f1) % 60;
                f0 = f1;
                f1 = f;
            }

            var s = f1 - 1;
            return s;
        }
    }

    // Driver Code
    var m = 10087887;
    var n = 2983097899;
    var Final = parseInt( Math.abs(fib(n) - fib(m - 1)));

    document.write(Final % 10);

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
5
```

**时间复杂度:** *O(1)* ，因为这个代码对于任何输入的数字都要运行差不多 60 次。

**辅助空间:** O(1)