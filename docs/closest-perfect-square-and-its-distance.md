# 最近的完美正方形及其距离

> 原文:[https://www . geeksforgeeks . org/最接近完美正方形及其距离/](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)

给定一个正整数![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")。任务是找到最接近 N 的完美平方数**以及从 **N** 到达该数所需的步数。
**注:**与 **N** 最接近的完美正方形可以小于、等于或大于 **N** ，steps 是指 N 与最接近的完美正方形的差。
**示例:**** 

> **输入:**N = 1500
> T3】输出:完美平方= 1521，步长= 21
> 对于 N = 1500
> 大于 N 的最近完美平方为 1521。
> 所以需要的步骤是 21。
> 小于 N 的最近完美平方为 1444。
> 所以需要的步骤是 56。
> 这两者的最小值为 1521，步长为 21。
> **输入:** N = 2
> **输出:**完美平方= 1，步长= 1
> 对于 N = 2
> 大于 N 的最近完美平方为 4。
> 所以需要的步骤是 2。
> 小于 N 的最近完美平方为 1。
> 所以需要的步骤是 1。
> 这两个的最小值是 1。

**进场:**

*   如果 **N** 是**完美正方形**，则打印 N 并步进为 **0** 。
*   否则，找到第一个[完美方块](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)编号 **> N** 并注意其与 **N** 的区别。
*   然后，找到第一个完美平方数 **< N** ，并注意其与 **N** 的区别。
*   并打印得到这两个差值的**最小值**的完美正方形，并将该差值作为最小步长。

以下是上述方法的实现:

## C++

```
// CPP program to find the closest perfect square
// taking minimum steps to reach from a number

#include<bits/stdc++.h>
using namespace std;

    // Function to check if a number is
    // perfect square or not
    bool isPerfect(int N)
    {
        if ((sqrt(N) - floor(sqrt(N))) != 0)
            return false;
        return true;
    }

    // Function to find the closest perfect square
    // taking minimum steps to reach from a number
    void getClosestPerfectSquare(int N)
    {
        if (isPerfect(N))
        {
            cout<<N<<" "<<"0"<<endl;
            return;
        }

        // Variables to store first perfect
        // square number
        // above and below N
        int aboveN = -1, belowN = -1;
        int n1;

        // Finding first perfect square
        // number greater than N
        n1 = N + 1;
        while (true) {
            if (isPerfect(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first perfect square
        // number less than N
        n1 = N - 1;
        while (true) {
            if (isPerfect(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        int diff1 = aboveN - N;
        int diff2 = N - belowN;

        if (diff1 > diff2)
            cout<<belowN<<" "<<diff2;
        else
            cout<<aboveN<<" "<<diff1;
    }

    // Driver code
    int main()
    {
        int N = 1500;

        getClosestPerfectSquare(N);
    }
//This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the closest perfect square
// taking minimum steps to reach from a number

class GFG {

    // Function to check if a number is
    // perfect square or not
    static boolean isPerfect(int N)
    {
        if ((Math.sqrt(N) - Math.floor(Math.sqrt(N))) != 0)
            return false;
        return true;
    }

    // Function to find the closest perfect square
    // taking minimum steps to reach from a number
    static void getClosestPerfectSquare(int N)
    {
        if (isPerfect(N)) {
            System.out.println(N + " "
                               + "0");
            return;
        }

        // Variables to store first perfect
        // square number
        // above and below N
        int aboveN = -1, belowN = -1;
        int n1;

        // Finding first perfect square
        // number greater than N
        n1 = N + 1;
        while (true) {
            if (isPerfect(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first perfect square
        // number less than N
        n1 = N - 1;
        while (true) {
            if (isPerfect(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        int diff1 = aboveN - N;
        int diff2 = N - belowN;

        if (diff1 > diff2)
            System.out.println(belowN + " " + diff2);
        else
            System.out.println(aboveN + " " + diff1);
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 1500;

        getClosestPerfectSquare(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the closest
# perfect square taking minimum steps
# to reach from a number

# Function to check if a number is
# perfect square or not
from math import sqrt, floor
def isPerfect(N):
    if (sqrt(N) - floor(sqrt(N)) != 0):
        return False
    return True

# Function to find the closest perfect square
# taking minimum steps to reach from a number
def getClosestPerfectSquare(N):
    if (isPerfect(N)):
        print(N, "0")
        return

    # Variables to store first perfect
    # square number above and below N
    aboveN = -1
    belowN = -1
    n1 = 0

    # Finding first perfect square
    # number greater than N
    n1 = N + 1
    while (True):
        if (isPerfect(n1)):
            aboveN = n1
            break
        else:
            n1 += 1

    # Finding first perfect square
    # number less than N
    n1 = N - 1
    while (True):
        if (isPerfect(n1)):
            belowN = n1
            break
        else:
            n1 -= 1

    # Variables to store the differences
    diff1 = aboveN - N
    diff2 = N - belowN

    if (diff1 > diff2):
        print(belowN, diff2)
    else:
        print(aboveN, diff1)

# Driver code
N = 1500
getClosestPerfectSquare(N)

# This code is contributed
# by sahishelangia
```

## C#

```
// C# program to find the closest perfect square
// taking minimum steps to reach from a number
using System;

class GFG {

    // Function to check if a number is
    // perfect square or not
    static bool isPerfect(int N)
    {
        if ((Math.Sqrt(N) - Math.Floor(Math.Sqrt(N))) != 0)
            return false;
        return true;
    }

    // Function to find the closest perfect square
    // taking minimum steps to reach from a number
    static void getClosestPerfectSquare(int N)
    {
        if (isPerfect(N)) {
            Console.WriteLine(N + " "
                            + "0");
            return;
        }

        // Variables to store first perfect
        // square number
        // above and below N
        int aboveN = -1, belowN = -1;
        int n1;

        // Finding first perfect square
        // number greater than N
        n1 = N + 1;
        while (true) {
            if (isPerfect(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first perfect square
        // number less than N
        n1 = N - 1;
        while (true) {
            if (isPerfect(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        int diff1 = aboveN - N;
        int diff2 = N - belowN;

        if (diff1 > diff2)
            Console.WriteLine(belowN + " " + diff2);
        else
            Console.WriteLine(aboveN + " " + diff1);
    }

    // Driver code
    public static void Main()
    {
        int N = 1500;

        getClosestPerfectSquare(N);
    }
}
// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the closest perfect
// square taking minimum steps to reach
// from a number

// Function to check if a number is
// perfect square or not
function isPerfect($N)
{
    if ((sqrt($N) - floor(sqrt($N))) != 0)
        return false;
    return true;
}

// Function to find the closest perfect square
// taking minimum steps to reach from a number
function getClosestPerfectSquare($N)
{
    if (isPerfect($N))
    {
        echo $N, " ", "0", "\n";
        return;
    }

    // Variables to store first perfect
    // square number
    // above and below N
    $aboveN = -1;
    $belowN = -1;
    $n1;

    // Finding first perfect square
    // number greater than N
    $n1 = $N + 1;
    while (true)
    {
        if (isPerfect($n1))
        {
            $aboveN = $n1;
            break;
        }
        else
            $n1++;
    }

    // Finding first perfect square
    // number less than N
    $n1 = $N - 1;
    while (true)
    {
        if (isPerfect($n1))
        {
            $belowN = $n1;
            break;
        }
        else
            $n1--;
    }

    // Variables to store the differences
    $diff1 = $aboveN - $N;
    $diff2 = $N - $belowN;

    if ($diff1 > $diff2)
        echo $belowN, " " , $diff2;
    else
        echo $aboveN, " ", $diff1;
}

// Driver code
$N = 1500;
getClosestPerfectSquare($N);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // the closest perfect square
    // taking minimum steps to reach
    // from a number

    // Function to check if a number is
    // perfect square or not
    function isPerfect(N)
    {
        if ((Math.sqrt(N) -
        Math.floor(Math.sqrt(N))) != 0)
            return false;
        return true;
    }

    // Function to find the closest perfect square
    // taking minimum steps to reach from a number
    function getClosestPerfectSquare(N)
    {
        if (isPerfect(N)) {
            document.write(N + " " + "0" + "</br>");
            return;
        }

        // Variables to store first perfect
        // square number
        // above and below N
        let aboveN = -1, belowN = -1;
        let n1;

        // Finding first perfect square
        // number greater than N
        n1 = N + 1;
        while (true) {
            if (isPerfect(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first perfect square
        // number less than N
        n1 = N - 1;
        while (true) {
            if (isPerfect(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        let diff1 = aboveN - N;
        let diff2 = N - belowN;

        if (diff1 > diff2)
            document.write(belowN + " " + diff2);
        else
            document.write(aboveN + " " + diff1);
    }

    let N = 1500;

      getClosestPerfectSquare(N);

</script>
```

**Output:** 

```
1521 21
```