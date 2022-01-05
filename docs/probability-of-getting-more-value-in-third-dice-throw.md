# 第三次掷骰子获得更多价值的概率

> 原文:[https://www . geeksforgeeks . org/第三次掷骰子获得更多价值的概率/](https://www.geeksforgeeks.org/probability-of-getting-more-value-in-third-dice-throw/)

假设三个玩家在玩掷骰子的游戏。玩家 1 掷出一个骰子得到 A，玩家 2 掷出一个骰子得到 b。任务是找出玩家 3 赢得比赛的概率，如果玩家 3 得到的比他们两个都多，他就赢了。

**示例:**

```
Input: A = 2, B = 3
Output: 1/2
Player3 wins if he gets 4 or 5 or 6

Input: A = 1, B = 2
Output: 2/3
Player3 wins if he gets 3 or 4 or 5 or 6 
```

**进场:**思路是找出 A 和 B 的最大值，然后 6-max(A，B)给我们剩下的 C 应该拿到的数字来赢得比赛。所以，用这两者的 [GCD](https://write.geeksforgeeks.org/geek/find-any-pair-with-given-gcd-and-lcm-3/) 可以找到 6-max(A，B)和 6 除的答案。

## C++

```
// CPP program to find probability to C win the match
#include <bits/stdc++.h>
using namespace std;

// function to find probability to C win the match
void Probability(int A, int B)
{
    int C = 6 - max(A, B);

    int gcd = __gcd(C, 6);

    cout << C / gcd << "/" << 6 / gcd;
}

// Driver code
int main()
{
    int A = 2, B = 4;

    // function call
    Probability(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java program to find probability to C win the match

import java.io.*;

class GFG {// Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

// function to find probability to C win the match
static void Probability(int A, int B)
{
    int C = 6 - Math.max(A, B);

    int gcd = __gcd(C, 6);

    System.out.print( C / gcd + "/" + 6 / gcd);
}

// Driver code

    public static void main (String[] args) {
    int A = 2, B = 4;

    // function call
    Probability(A, B);
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 program to find probability
# to C win the match

# import gcd() from math lib.
from math import gcd

# function to find probability
# to C win the match
def Probability(A, B) :
    C = 6 - max(A, B)

    __gcd = gcd(C, 6)

    print(C // __gcd, "/", 6 // __gcd)

# Driver Code
if __name__ == "__main__" :

    A, B = 2, 4

    # function call
    Probability(A, B)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find probability
// to C win the match
using System;

class GFG
{

// Recursive function to return
// gcd of a and b
static int __gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// function to find probability
// to C win the match
static void Probability(int A, int B)
{
    int C = 6 - Math.Max(A, B);

    int gcd = __gcd(C, 6);

    Console.Write(C / gcd + "/" + 6 / gcd);
}

// Driver code
static public void Main ()
{
    int A = 2, B = 4;

    // function call
    Probability(A, B);
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find probability
// to C win the match

// Find gcd()
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);
}

// function to find probability
// to C win the match
function Probability($A, $B)
{
    $C = 6 - max($A, $B);

    $gcd = __gcd($C, 6);

    echo ($C / $gcd) . "/" .
                 (6 / $gcd);
}

// Driver code
$A = 2;
$B = 4;

// function call
Probability($A, $B);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to find probability
    // to C win the match

    // Recursive function to return
    // gcd of a and b
    function __gcd(a, b)
    {
        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // function to find probability
    // to C win the match
    function Probability(A, B)
    {
        let C = 6 - Math.max(A, B);

        let gcd = __gcd(C, 6);

        document.write(parseInt(C / gcd, 10) + "/" + parseInt(6 / gcd, 10));
    }

    let A = 2, B = 4;

    // function call
    Probability(A, B);

</script>
```

**Output:** 

```
1/3
```