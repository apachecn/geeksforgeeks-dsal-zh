# 当给出命中目标的概率时，找出玩家获胜的概率

> 原文:[https://www . geeksforgeeks . org/find-当给出击中目标的概率时，玩家获胜的概率/](https://www.geeksforgeeks.org/find-probability-that-a-player-wins-when-probabilities-of-hitting-the-target-are-given/)

给定四个整数 **p** 、 **q** 、 **r** 和 **s** 。两个玩家正在玩一个游戏，其中两个玩家都击中了一个目标，第一个击中目标的玩家赢得了游戏。第一个玩家击中目标的概率为 **p / q** ，第二个玩家击中目标的概率为 **r / s** 。任务是找出第一个玩家赢得游戏的概率。

**示例:**

> **输入:** p = 1，q = 4，r = 3，s = 4
> T3】输出: 0.307692308
> 
> **输入:** p = 1，q = 2，r = 1，s = 2
> T3】输出: 0.666666667

**进场:**第一个玩家命中目标的概率为 **p / q** ，未命中目标的概率为**1–p/q**。
第二个玩家命中目标的概率为 **r / s** ，错过目标的概率为**1–r/s**。
让第一个玩家为 **x** ，第二个玩家为 **y** 。
所以总概率会是 **x 赢了+ (x 输了* y 输了* x 赢了)+ (x 输了* y 输了* x 输了* y 输了* x 赢了)+……如此类推**。
因为 **x** 任何回合都能赢，所以是无限序列。
让**t =(1–p/q)*(1–r/s)**。这里 **t < 1** 作为 **p / q** 和 **r / s** 始终是**T42【1】T32】。
所以级数会变成，**p/q+(p/q)* t+(p/q)* t<sup>2</sup>+……**
这是一个无穷的 GP 级数，公比小于 1，其和会是**(p/q)/(1–t)**。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the probability of the winner
double find_probability(double p, double q,
                        double r, double s)
{

    double t = (1 - p / q) * (1 - r / s);

    double ans = (p / q) / (1 - t);

    return ans;
}

// Driver Code
int main()
{
    double p = 1, q = 2, r = 1, s = 2;

    // Will print 9 digits after the decimal point
    cout << fixed << setprecision(9)
         << find_probability(p, q, r, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.text.DecimalFormat;

class solution
{

// Function to return the probability of the winner
static double find_probability(double p, double q,
                        double r, double s)
{

    double t = (1 - p / q) * (1 - r / s);

    double ans = (p / q) / (1 - t);

    return ans;
}

// Driver Code
public static void main(String args[])
{
    double p = 1, q = 2, r = 1, s = 2;

    // Will print 9 digits after the decimal point
    DecimalFormat dec = new DecimalFormat("#0.000000000");
    System.out.println(dec.format(find_probability(p, q, r, s)));
}
}
// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the probability
# of the winner
def find_probability(p, q, r, s) :

    t = (1 - p / q) * (1 - r / s)

    ans = (p / q) / (1 - t);

    return round(ans, 9)

# Driver Code
if __name__ == "__main__" :

    p, q, r, s = 1, 2, 1, 2

    # Will print 9 digits after
    # the decimal point
    print(find_probability(p, q, r, s))

# This code is contributed by Ryuga
```

## C#

```
// C# mplementation of the approach
using System;

class GFG
{

// Function to return the probability of the winner
static double find_probability(double p, double q,
                        double r, double s)
{

    double t = (1 - p / q) * (1 - r / s);

    double ans = (p / q) / (1 - t);

    return ans;
}

// Driver Code
public static void Main()
{
    double p = 1, q = 2, r = 1, s = 2;
    Console.WriteLine(find_probability(p, q, r, s));
}
}

// This code is contributed by
// anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the probability
// of the winner
function find_probability($p, $q, $r, $s)
{
    $t = (1 - $p / $q) * (1 - $r / $s);

    $ans = ($p / $q) / (1 - $t);

    return $ans;
}

// Driver Code
$p = 1; $q = 2;
$r = 1; $s = 2;

// Will print 9 digits after
// the decimal point
$res = find_probability($p, $q, $r, $s);
$update = number_format($res, 7);
echo $update;

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the probability of the winner
function find_probability(p, q, r, s)
{

    var t = (1 - p / q) * (1 - r / s);

    var ans = (p / q) / (1 - t);

    return ans;
}

// Driver Code
var p = 1, q = 2, r = 1, s = 2;
// Will print 9 digits after the decimal point
document.write( find_probability(p, q, r, s).toFixed(9));

</script>
```

**Output:** 

```
0.666666667
```