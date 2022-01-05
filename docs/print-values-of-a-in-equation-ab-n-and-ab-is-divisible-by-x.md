# 打印等式(a+b) <中‘a’的值= n，a+b 可被 x 整除

> 原文:[https://www . geesforgeks . org/print-values-of-in-equation-ab-n-and-ab-is-除尽-x/](https://www.geeksforgeeks.org/print-values-of-a-in-equation-ab-n-and-ab-is-divisible-by-x/)

给定三个数字 b，x，n。任务是在等式(a+b) <= n 中找到“a”的值，使得 a+b 可以被 x 整除。如果没有这样的值，则打印-1。

**例:**

```
Input: b = 10, x = 6, n = 40
Output: 2 8 14 20 26

Input: b = 10, x = 1, n = 10
Output: -1
```

**方法:**可以找到最小可能值(b/x + 1)*x–b，然后我们将答案增加 x，直到它不大于 n，这里(b/x+1)* x 是可被 x 整除的最小可能值
下面是上述方法的实现:

## C++

```
// CPP program to Find values of a, in equation
// (a+b)<=n and a+b is divisible by x.
#include <bits/stdc++.h>
using namespace std;

// function to Find values of a, in equation
// (a+b)<=n and a+b is divisible by x.
void PossibleValues(int b, int x, int n)
{
    // least possible which is divisible by x
    int leastdivisible = (b / x + 1) * x;

    int flag = 1;

    // run a loop to get required answer
    while (leastdivisible <= n) {

        if (leastdivisible - b >= 1) {
            cout << leastdivisible - b << " ";

            // increase value by x
            leastdivisible += x;

            // answer is possible
            flag = 0;
        }
        else
            break;
    }

    if (flag)
        cout << -1;
}

// Driver code
int main()
{
    int b = 10, x = 6, n = 40;

    // function call
    PossibleValues(b, x, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find values of a, in equation
// (a+b)<=n and a+b is divisible by x.

import java.io.*;

class GFG {

// function to Find values of a, in equation
// (a+b)<=n and a+b is divisible by x.
static void PossibleValues(int b, int x, int n)
{
    // least possible which is divisible by x
    int leastdivisible = (b / x + 1) * x;

    int flag = 1;

    // run a loop to get required answer
    while (leastdivisible <= n) {

        if (leastdivisible - b >= 1) {
            System.out.print( leastdivisible - b + " ");

            // increase value by x
            leastdivisible += x;

            // answer is possible
            flag = 0;
        }
        else
            break;
    }

    if (flag>0)
         System.out.println(-1);
}

// Driver code
    public static void main (String[] args) {
            int b = 10, x = 6, n = 40;

    // function call
    PossibleValues(b, x, n);
    }
}

// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 program to Find values of a, in equation
# (a+b)<=n and a+b is divisible by x.

# function to Find values of a, in equation
# (a+b)<=n and a+b is divisible by x.
def PossibleValues(b, x, n) :

    # least possible which is divisible by x
    leastdivisible = int(b / x + 1) * x

    flag = 1

    # run a loop to get required answer
    while (leastdivisible <= n) :

        if (leastdivisible - b >= 1) :
            print(leastdivisible - b ,end= " ")

            # increase value by x
            leastdivisible += x

            # answer is possible
            flag = 0

        else :
            break

    if (flag != 0) :
        print(-1)

# Driver code
if __name__=='__main__':
    b = 10
    x = 6
    n = 40
# function call
    PossibleValues(b, x, n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to Find values of a,
// in equation (a+b)<=n and a+b
// is divisible by x.
using System;

class GFG {

// function to Find values
// of a, in equation (a+b)<=n
// and a+b is divisible by x.
static void PossibleValues(int b, int x, int n)
{

    // least possible which
    // is divisible by x
    int leastdivisible = (b / x + 1) * x;

    int flag = 1;

    // run a loop to get required answer
    while (leastdivisible <= n) {

        if (leastdivisible - b >= 1) {

            Console.Write( leastdivisible - b + " ");

            // increase value by x
            leastdivisible += x;

            // answer is possible
            flag = 0;
        }
        else
            break;
    }

    if (flag > 0)
        Console.WriteLine(-1);
}

    // Driver code
    public static void Main ()
    {
        int b = 10, x = 6, n = 40;

        // function call
        PossibleValues(b, x, n);
    }
}

// This code is contributed by Shubadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find values of a,
// in equation (a+b)<=n and a+b is
// divisible by x.

// function to Find values of a,
// in equation (a+b)<=n and a+b
// is divisible by x.
function PossibleValues($b, $x, $n)
{
    // least possible which is
    // divisible by x
    $leastdivisible = (intval($b / $x) + 1) * $x;

    $flag = 1;

    // run a loop to get required answer
    while ($leastdivisible <= $n)
    {

        if ($leastdivisible - $b >= 1)
        {
            echo $leastdivisible - $b . " ";

            // increase value by x
            $leastdivisible += $x;

            // answer is possible
            $flag = 0;
        }
        else
            break;
    }

    if ($flag)
        echo "-1";
}

// Driver code
$b = 10;
$x = 6;
$n = 40;

// function call
PossibleValues($b, $x, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to Find values of a, in equation
// (a+b)<=n and a+b is divisible by x.

    // function to Find values of a, in equation
// (a+b)<=n and a+b is divisible by x.
    function PossibleValues(b,x,n)
    {
        // least possible which is divisible by x
    let leastdivisible = (Math.floor(b / x) + 1) * x;

    let flag = 1;

    // run a loop to get required answer
    while (leastdivisible <= n) {

        if (leastdivisible - b >= 1) {
            document.write( leastdivisible - b + " ");

            // increase value by x
            leastdivisible += x;

            // answer is possible
            flag = 0;
        }
        else
            break;
    }

    if (flag>0)
         document.write(-1+"<br>");
    }

    // Driver code
    let b = 10, x = 6, n = 40;

    // function call
    PossibleValues(b, x, n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
2 8 14 20 26
```