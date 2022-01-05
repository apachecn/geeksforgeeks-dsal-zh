# 掷出 2 个骰子 N 次得到和的概率

> 原文:[https://www . geeksforgeeks . org/投掷 2 骰子 n 次获得总和的概率/](https://www.geeksforgeeks.org/probability-of-getting-a-sum-on-throwing-2-dices-n-times/)

考虑到总数。任务是找出两个骰子掷 N 次的和出现的概率。
**概率**被定义为对结果总数有利的结果数。概率总是介于 0 和 1 之间。
**示例:**

```
Input: sum = 11, times = 1
Output: 2 / 36
favorable outcomes = (5, 6) and (6, 5) i.e 2
Total outcomes = (1, 1), (1, 2), (1, 3)...(6, 6) i.e 36
Probability = (2 / 36)

Input: sum = 7, times = 7
Output: 1 / 279936
```

**公式:-**

> 掷出 2 个骰子 n 次出现和的概率= **(有利/总)^ N**

**进场:-**

> 首先，计算 1 次掷出 2 个骰子的总和出现的概率。
> 假设概率 1。
> 现在，计算两个骰子掷 n 次之和出现的概率为:
> 概率 2 =(概率 1) ^ N. **即概率 1 升 n 次方**

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function that calculates Probability.
int Probability(int sum, int times)
{

    float favorable = 0.0, total = 36.0;
    long int probability = 0;

    // To calculate favorable outcomes
    // in thrown of 2 dices 1 times.
    for (int i = 1; i <= 6; i++) {
        for (int j = 1; j <= 6; j++) {
            if ((i + j) == sum)
                favorable++;
        }
    }

    int gcd1 = __gcd((int)favorable, (int)total);

    // Reduce to simplest Form.
    favorable = favorable / (float)gcd1;
    total = total / (float)gcd1;

    // Probability of occurring sum on 2 dice N times.
    probability = pow(total, times);

    return probability;
}

// Driver Code
int main()
{
    int sum = 7, times = 7;

    cout << "1"
         << "/" << Probability(sum, times);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

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

// function that calculates
// Probability.
static long Probability(int sum,
                        int times)
{

    float favorable = 0, total = 36;
    long probability = 0;

    // To calculate favorable outcomes
    // in thrown of 2 dices 1 times.
    for (int i = 1; i <= 6; i++)
    {
        for (int j = 1; j <= 6; j++)
        {
            if ((i + j) == sum)
                favorable++;
        }
    }

    int gcd1 = __gcd((int)favorable,
                     (int)total);

    // Reduce to simplest Form.
    favorable = favorable / (float)gcd1;
    total = total / (float)gcd1;

    // Probability of occurring
    // sum on 2 dice N times.
    probability = (long)Math.pow(total, times);

    return probability;
}

// Driver Code
public static void main (String[] args)
{
    int sum = 7, times = 7;

    System.out.println( "1" + "/" +
          Probability(sum, times));
}
}

// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# from math import everything
from math import *

# function that calculates Probability.
def Probability(sum, times) :
    favorable, total, probability = 0.0, 36.0, 0

    # To calculate favorable outcomes
    # in thrown of 2 dices 1 times.
    for i in range(7) :
        for j in range(7) :
            if ((i + j) == sum) :
                favorable += 1

    gcd1 = gcd(int(favorable), int(total))

    # Reduce to simplest Form.
    favorable = favorable / gcd1
    total = total / gcd1

    # Probability of occurring sum on 2 dice N times.
    probability = pow(total, times)

    return int(probability)

# Driver Code
if __name__ == "__main__" :

    sum, times = 7, 7

    print("1","/",Probability(sum, times))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach

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

// function that calculates
// Probability.
static long Probability(int sum,
                        int times)
{

    float favorable = 0, total = 36;
    long probability = 0;

    // To calculate favorable outcomes
    // in thrown of 2 dices 1 times.
    for (int i = 1; i <= 6; i++)
    {
        for (int j = 1; j <= 6; j++)
        {
            if ((i + j) == sum)
                favorable++;
        }
    }

    int gcd1 = __gcd((int)favorable,
                    (int)total);

    // Reduce to simplest Form.
    favorable = favorable / (float)gcd1;
    total = total / (float)gcd1;

    // Probability of occurring
    // sum on 2 dice N times.
    probability = (long)System.Math.Pow(total, times);

    return probability;
}

// Driver Code
public static void Main()
{
    int sum = 7, times = 7;

    System.Console.WriteLine( "1" + "/" +
        Probability(sum, times));
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// function to calculate gcd
function getGCDBetween($a, $b)
{
    while ($b != 0)
    {
        $m = $a % $b;
        $a = $b;
        $b = $m;
    }
    return $a;
}

// function that calculates Probability.
function Probability($sum, $times)
{

    $favorable = 0.0;
    $total = 36.0;
    $probability = 0;

    // To calculate favorable outcomes
    // in thrown of 2 dices 1 times.
    for ($i = 1; $i <= 6; $i++)
    {
        for ($j = 1; $j <= 6; $j++)
        {
            if (($i + $j) == $sum)
                $favorable++;
        }
    }

    $gcd1 = getGCDBetween((int)$favorable,
                          (int)$total);

    // Reduce to simplest Form.
    $favorable = $favorable / (float)$gcd1;
    $total = $total / (float)$gcd1;

    // Probability of occurring
    // sum on 2 dice N times.
    $probability = pow($total, $times);

    return $probability;
}

// Driver Code
$sum = 7;
$times = 7;

echo "1", "/", Probability($sum, $times);

// This code is contributed by ash264   
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

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

// function that calculates Probability.
function Probability(sum, times)
{
    var favorable = 0.0, total = 36.0;
    var probability = 0;

    // To calculate favorable outcomes
    // in thrown of 2 dices 1 times.
    for (var i = 1; i <= 6; i++) {
        for (var j = 1; j <= 6; j++) {
            if ((i + j) == sum)
                favorable++;
        }
    }

    var gcd1 = __gcd(favorable, total);

    // Reduce to simplest Form.
    favorable = favorable / gcd1;
    total = total / gcd1;

    // Probability of occurring sum on 2 dice N times.
    probability = Math.pow(total, times);

    return probability;
}

// Driver Code
var sum = 7, times = 7;
document.write( "1"
    + "/" + Probability(sum, times));

</script>
```

**Output:** 

```
1/279936
```