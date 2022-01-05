# 将 N 写成 4 个正方形之和的方式数

> 原文:[https://www . geeksforgeeks . org/写作方式数-n-as-sum-of-4-squares/](https://www.geeksforgeeks.org/number-of-ways-of-writing-n-as-a-sum-of-4-squares/)

给定一个数 N，任务是找出把 N 写成 4 个平方之和的方法数。如果两个表示的项的顺序不同，或者被求平方的整数(而不仅仅是平方)不同，则这两个表示被认为是不同的。

**示例:**

> **输入:** n=1
> **输出:**8
> 1<sup>2</sup>+0<sup>2</sup>+0<sup>2</sup>+0<sup>2</sup>T14】0<sup>2</sup>+1<sup>2</sup>+0<sup>2</sup>+0<sup>2</sup>T23】0<sup>2</sup>+0 + 0 <sup>2</sup> + 1 <sup>2</sup>
> 类似地，用-1
> 替换 1 还有 4 种其他可能的方法。因此有 8 种可能的方法。
> 
> **输入:**n = 5
> T3】输出: 48

**方法:**
[雅可比四平方定理](https://en.wikipedia.org/wiki/Jacobi%27s_four-square_theorem)指出，把 n 写成 4 个平方之和的方式，如果 n 是奇数，则为 n 除数之和的 8 倍，如果 n 是偶数，则为 n 除数之和的 24 倍。通过运行从 1 到 sqrt(n)的循环，求 n 的奇数除数和偶数除数。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Number of ways of writing n
// as a sum of 4 squares
int sum_of_4_squares(int n)
{
    // sum of odd and even factor
    int i, odd = 0, even = 0;

    // iterate from 1 to the number
    for (i = 1; i <= sqrt(n); i++) {
        // if i is the factor of n
        if (n % i == 0) {
            // if factor is even
            if (i % 2 == 0)
                even += i;

            // if factor is odd
            else
                odd += i;

            // n/i is also a factor
            if ((n / i) != i) {
                // if factor is even
                if ((n / i) % 2 == 0)
                    even += (n / i);

                // if factor is odd
                else
                    odd += (n / i);
            }
        }
    }
    // if n is odd
    if (n % 2 == 1)
        return 8 * (odd + even);

    // if n is even
    else
        return 24 * (odd);
}
// Driver code
int main()
{
    int n = 4;

    cout << sum_of_4_squares(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

// Number of ways of writing n
// as a sum of 4 squares
static int sum_of_4_squares(int n)
{
    // sum of odd and even factor
    int i, odd = 0, even = 0;

    // iterate from 1 to the number
    for (i = 1; i <= Math.sqrt(n); i++)
    {
        // if i is the factor of n
        if (n % i == 0)
        {
            // if factor is even
            if (i % 2 == 0)
                even += i;

            // if factor is odd
            else
                odd += i;

            // n/i is also a factor
            if ((n / i) != i)
            {
                // if factor is even
                if ((n / i) % 2 == 0)
                    even += (n / i);

                // if factor is odd
                else
                    odd += (n / i);
            }
        }
    }
    // if n is odd
    if (n % 2 == 1)
        return 8 * (odd + even);

    // if n is even
    else
        return 24 * (odd);
}

    // Driver code
    public static void main (String[] args)
    {
            int n = 4;
        System.out.println (sum_of_4_squares(n));
    }
}

// This code is contributed by tushil.
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Number of ways of writing n
# as a sum of 4 squares
def sum_of_4_squares(n):

    # sum of odd and even factor
    i, odd, even = 0,0,0

    # iterate from 1 to the number
    for i in range(1,int(n**(.5))+1):
        # if i is the factor of n
        if (n % i == 0):

            # if factor is even
            if (i % 2 == 0):
                even += i

            # if factor is odd
            else:
                odd += i

            # n/i is also a factor
            if ((n // i) != i):

                # if factor is even
                if ((n // i) % 2 == 0):
                    even += (n // i)

                # if factor is odd
                else:
                    odd += (n // i)

    # if n is odd
    if (n % 2 == 1):
        return 8 * (odd + even)

    # if n is even
    else :
        return 24 * (odd)

# Driver code

n = 4

print(sum_of_4_squares(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Number of ways of writing n
// as a sum of 4 squares
static int sum_of_4_squares(int n)
{
    // sum of odd and even factor
    int i, odd = 0, even = 0;

    // iterate from 1 to the number
    for (i = 1; i <= Math.Sqrt(n); i++)
    {
        // if i is the factor of n
        if (n % i == 0)
        {
            // if factor is even
            if (i % 2 == 0)
                even += i;

            // if factor is odd
            else
                odd += i;

            // n/i is also a factor
            if ((n / i) != i)
            {
                // if factor is even
                if ((n / i) % 2 == 0)
                    even += (n / i);

                // if factor is odd
                else
                    odd += (n / i);
            }
        }
    }
    // if n is odd
    if (n % 2 == 1)
        return 8 * (odd + even);

    // if n is even
    else
        return 24 * (odd);
}

// Driver code
static public void Main ()
{

    int n = 4;
    Console.WriteLine(sum_of_4_squares(n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Number of ways of writing n
// as a sum of 4 squares
function sum_of_4_squares(n)
{

    // Sum of odd and even factor
    var i, odd = 0, even = 0;

    // Iterate from 1 to the number
    for(i = 1; i <= Math.sqrt(n); i++)
    {

        // If i is the factor of n
        if (n % i == 0)
        {

            // If factor is even
            if (i % 2 == 0)
                even += i;

            // If factor is odd
            else
                odd += i;

            // n/i is also a factor
            if ((n / i) != i)
            {

                // If factor is even
                if ((n / i) % 2 == 0)
                    even += (n / i);

                // If factor is odd
                else
                    odd += (n / i);
            }
        }
    }

    // If n is odd
    if (n % 2 == 1)
        return 8 * (odd + even);

    // If n is even
    else
        return 24 * (odd);
}

// Driver code
var n = 4;

document.write(sum_of_4_squares(n));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
24
```

**时间复杂度:** O(sqrt(N))