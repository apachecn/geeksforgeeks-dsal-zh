# 求两个四次幂之差等于 N 的数

> 原文:[https://www . geesforgeks . org/find-二进制数-其四次幂之差等于-n/](https://www.geeksforgeeks.org/find-two-numbers-whose-difference-of-fourth-power-is-equal-to-n/)

给定一个整数 **N** ，任务是找出两个非负整数 **X** 和 **Y** ，使得**X<sup>4</sup>–Y<sup>4</sup>= N**。如果不存在这样的配对，请打印-1。
**示例:**

> **输入:** N = 15
> **输出:** X = 2，Y = 1
> **说明:**T8】X<sup>4</sup>–Y<sup>4</sup>=(2)<sup>4</sup>–(1)<sup>4</sup>=(16)–(1)= 15
> 
> **输入:** N = 10
> **输出:** -1
> **说明:**
> 不存在满足条件的 X、Y 这样的值。

**方法:**
为了解决上面提到的问题，我们必须观察到，我们需要找到 x 和 y 的**最小值和最大值**，这可能满足等式。

*   两个整数的最小值可以是 **0** ，因为 **X** & **Y** 是非负的*。*
*   ***X****Y**的最大值可以是 **ceil(N <sup>(1/4)</sup> )** 。*
*   *因此，迭代范围**【0】、ceil(N<sup>(1/4)</sup>)】**，找到满足条件的任意一对合适的 **X** 和 **Y** 。*

*以下是上述方法的实现:* 

## *C++*

```
*// C++ implementation to find the
// values of x and y for the given
// equation with integer N

#include <bits/stdc++.h>
using namespace std;

// Function which find required x & y
void solve(int n)
{
    // Upper limit of x & y,
    // if such x & y exists
    int upper_limit = ceil(pow(
        n, 1.0 / 4));

    for (int x = 0; x <= upper_limit; x++) {

        for (int y = 0; y <= upper_limit; y++) {

            // num1 stores x^4
            int num1 = x * x * x * x;

            // num2 stores y^4
            int num2 = y * y * y * y;

            // If condition is satisfied
            // the print and return
            if (num1 - num2 == n) {
                cout << "x = " << x
                     << ", y = " << y;
                return;
            }
        }
    }

    // If no such pair exists
    cout << -1 << endl;
}

// Driver code
int main()
{
    int n = 15;

    solve(n);

    return 0;
}*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java implementation to find the
// values of x and y for the given
// equation with integer N
import java.util.*;

class GFG{

// Function which find required x & y
static void solve(int n)
{

    // Upper limit of x & y,
    // if such x & y exists
    int upper_limit = (int) (Math.ceil
                            (Math.pow(n, 1.0 / 4)));

    for(int x = 0; x <= upper_limit; x++)
    {
       for(int y = 0; y <= upper_limit; y++)
       {

          // num1 stores x^4
          int num1 = x * x * x * x;

          // num2 stores y^4
          int num2 = y * y * y * y;

          // If condition is satisfied
          // the print and return
          if (num1 - num2 == n)
          {
              System.out.print("x = " + x +
                             ", y = " + y);
              return;
          }
       }
    }

    // If no such pair exists
    System.out.print(-1);
}

// Driver code
public static void main(String[] args)
{
    int n = 15;

    solve(n);
}
}

// This code is contributed by shivanisinghss2110*
```

## *蟒蛇 3*

```
*# Python3 implementation to find the
# values of x and y for the given
# equation with integer N
from math import pow, ceil

# Function which find required x & y
def solve(n) :

    # Upper limit of x & y,
    # if such x & y exists
    upper_limit = ceil(pow(n, 1.0 / 4));

    for x in range(upper_limit + 1) :

        for y in range(upper_limit + 1) :

            # num1 stores x^4
            num1 = x * x * x * x;

            # num2 stores y^4
            num2 = y * y * y * y;

            # If condition is satisfied
            # the print and return
            if (num1 - num2 == n) :
                print("x =", x, ", y =" , y);
                return;

    # If no such pair exists
    print(-1) ;

# Driver code
if __name__ == "__main__" :

    n = 15;

    solve(n);

# This code is contributed by AnkitRai01*
```

## *C#*

```
*// C# implementation to find the
// values of x and y for the given
// equation with integer N
using System;

class GFG{

// Function which find required x & y
static void solve(int n)
{

    // Upper limit of x & y,
    // if such x & y exists
    int upper_limit = (int) (Math.Ceiling
                            (Math.Pow(n, 1.0 / 4)));

    for(int x = 0; x <= upper_limit; x++)
    {
       for(int y = 0; y <= upper_limit; y++)
       {

          // num1 stores x^4
          int num1 = x * x * x * x;

          // num2 stores y^4
          int num2 = y * y * y * y;

          // If condition is satisfied
          // the print and return
          if (num1 - num2 == n)
          {
              Console.Write("x = " + x +
                          ", y = " + y);
              return;
          }
       }
    }

    // If no such pair exists
    Console.Write(-1);
}

// Driver code
public static void Main(String[] args)
{
    int n = 15;

    solve(n);
}
}

// This code is contributed by shivanisinghss2110*
```

## *java 描述语言*

```
*<script>

    // Javascript implementation to find the
    // values of x and y for the given
    // equation with integer N

    // Function which find required x & y
    function solve(n)
    {
        // Upper limit of x & y,
        // if such x & y exists
        let upper_limit = Math.ceil(Math.pow(n, 1.0 / 4));

        for (let x = 0; x <= upper_limit; x++) {

            for (let y = 0; y <= upper_limit; y++) {

                // num1 stores x^4
                let num1 = x * x * x * x;

                // num2 stores y^4
                let num2 = y * y * y * y;

                // If condition is satisfied
                // the print and return
                if (num1 - num2 == n) {
                    document.write("x = " + x + ", y = " + y);
                    return;
                }
            }
        }

        // If no such pair exists
        document.write(-1);
    }

    let n = 15;

    solve(n);

</script>*
```

***Output:** 

```
x = 2, y = 1
```* 

***时间复杂度:** *O(sqrt(N))**