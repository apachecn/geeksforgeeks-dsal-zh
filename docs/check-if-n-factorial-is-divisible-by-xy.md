# 检查 n 阶乘是否能被 X^Y 整除

> 原文:[https://www . geesforgeks . org/check-if-n-factorial-is-by-xy/](https://www.geeksforgeeks.org/check-if-n-factorial-is-divisible-by-xy/)

给定三个整数 N，X 和 Y，任务是检查**是否为 N！**可被**X<sup>Y</sup>T5
T7】整除示例:**T9】

> **输入:** N = 10，X = 2，Y = 8
> **输出:** YES
> **说明:**
> 10 的阶乘为–3628800
> ，X<sup>Y</sup>= 2<sup>8</sup>= 256
> 由于，3628800 可被 256 整除，因此回答为 YES。
> **输入:** N = 5，X = 2，Y = 4
> **输出:** NO
> **解释:**
> 5 的阶乘为–120
> ，X 的值 <sup>Y</sup> = 2 <sup>4</sup> = 16
> 由于，3628800 不能被 16 整除，因此答案为 NO.

**方法:**思路是分别求 N 阶乘和 X <sup>Y</sup> 的值，然后检查 N 阶乘的值是否能被 X <sup>Y</sup> 整除。
**算法:**

*   [计算 N 阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)的值
*   求 X <sup>Y</sup> 的值。
*   检查 N 的阶乘是否能被 X <sup>Y</sup> 整除。

**注**:该方法不适用于大数值 N.
以下是上述方法的实现:

## C++

```
// CPP implementation to check if
// the value of the N! % X^Y == 0
#include<bits/stdc++.h>
using namespace std;

    // Function to check if N! % X^Y == 0
    void check(int n,int x, int y){
        int fact = 1;

        // Loop to calculate N-factorial
        for (int i = 2; i <= n; i++) {
            fact *= i;
        }

        int divisor = pow(x, y);

        // Condition to check
        if (fact % divisor == 0)
            cout << "YES";
        else
            cout << "NO";

    }

    // Driver Code
        int main()
    {
        int n = 10;
        int x = 2;
        int y = 8;

        // Function Call
        check(n, x, y);
    }

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// the value of the N! % X^Y == 0
import java.util.*;
import java.lang.*;

class divisible {

    // Function to check if N! % X^Y == 0
    public static void check(int n,
                         int x, int y){
        long fact = 1;

        // Loop to calculate N-factorial
        for (int i = 2; i <= n; i++) {
            fact *= i;
        }

        long divisor = (long)Math.pow(x, y);

        // Condition to check
        if (fact % divisor == 0)
            System.out.println("YES");
        else
            System.out.println("NO");

    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;
        int x = 2;
        int y = 8;

        // Function Call
        check(n, x, y);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to check if
# the value of the N! % X^Y == 0

# Function to check if N! % X^Y == 0
def check(n, x, y) :
    fact = 1;

    # Loop to calculate N-factorial
    for i in range(2, n + 1) :
        fact *= i;
    divisor = x ** y;

    # Condition to check
    if (fact % divisor == 0) :
        print("YES");
    else :
        print("NO");

# Driver Code
if __name__ == "__main__" :

    n = 10;
    x = 2;
    y = 8;

    # Function Call
    check(n, x, y);

# This code is contributed by Yash_R
```

## C#

```
// C# implementation to check if
// the value of the N! % X^Y == 0
using System;

class divisible {

    // Function to check if N! % X^Y == 0
    public static void check(int n,
                         int x, int y){
        long fact = 1;

        // Loop to calculate N-factorial
        for (int i = 2; i <= n; i++) {
            fact *= i;
        }

        long divisor = (long)Math.Pow(x, y);

        // Condition to check
        if (fact % divisor == 0)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");

    }

    // Driver Code
    public static void Main(String []args)
    {
        int n = 10;
        int x = 2;
        int y = 8;

        // Function Call
        check(n, x, y);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation to check if
// the value of the N! % X^Y == 0

function check(n,x,y)
{
        var fact = 1;

        // Loop to calculate N-factorial
        for (var i = 2; i <= n; i++) {
            fact *= i;
        }

        var divisor = Math.pow(x, y);

        // Condition to check
        if (fact % divisor === 0)
            document.write("YES");
        else
            document.write("NO");

    }

        var n = 10;
        var x = 2;
        var y = 8;

        // Function Call
        check(n, x, y);

</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation to check if
// the value of the N! % X^Y == 0

function check($n,$x,$y)
{
        $fact = 1;

        // Loop to calculate N-factorial
        for ($i = 2; $i <= $n; $i++) {
            $fact *= $i;
        }

        $divisor = pow($x, $y);

        // Condition to check
        if ($fact % $divisor === 0)
            echo("YES");
        else
            echo("NO");

    }

        $n = 10;
        $x = 2;
        $y = 8;

        // Function Call
        check($n, $x, $y);

        // This code is contributed by _saurabh_jaiswal
?>
```

**输出:**

```
YES
```

**业绩分析:**

*   **时间复杂度:** O(N)
*   **辅助空间:** O(1)。