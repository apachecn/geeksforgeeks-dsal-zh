# 当给定单个击中目标的概率时，A 赢得比赛的概率

> 原文:[https://www . geeksforgeeks . org/给定击中目标的个人概率时赢得比赛的概率/](https://www.geeksforgeeks.org/probability-of-a-winning-the-match-when-individual-probabilities-of-hitting-the-target-given/)

给定四个整数 **a** 、 **b** 、 **c** 和 **d** 。玩家 **A** & **B** 尝试点球得分。A 射击目标的概率为 **a / b** ，B 射击目标的概率为 **c / d** 。先罚点球的球员获胜。任务是找出 A 赢得比赛的概率。
**举例:**

> **输入:** a = 1，b = 3，c = 1，d = 3
> **输出:** 0.6
> **输入:** a = 1，b = 2，c = 10，d = 11
> **输出:** 0.52381

**进场:**如果我们考虑变量 **K = a / b** 为 A 击中目标的概率，**R =(1 –( A/B))*(1–(c/d))**为 A 和 B 都没有击中目标的概率。
因此，解形成几何级数**K * R<sup>0</sup>+K * R<sup>1</sup>+K * R<sup>2</sup>+…..**其和为**(K/1–R)**。将 **K** 和 **R** 的值放在一起后，我们得到公式为**K *(1/(1 –( 1–R)*(1–K))**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the probability of A winning
double getProbability(int a, int b, int c, int d)
{

    // p and q store the values
    // of fractions a / b and c / d
    double p = (double)a / (double)b;
    double q = (double)c / (double)d;

    // To store the winning probability of A
    double ans = p * (1 / (1 - (1 - q) * (1 - p)));
    return ans;
}

// Driver code
int main()
{
    int a = 1, b = 2, c = 10, d = 11;
    cout << getProbability(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the probability
// of A winning
static double getProbability(int a, int b,
                             int c, int d)
{

    // p and q store the values
    // of fractions a / b and c / d
    double p = (double) a / (double) b;
    double q = (double) c / (double) d;

    // To store the winning probability of A
    double ans = p * (1 / (1 - (1 - q) *
                               (1 - p)));
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a = 1, b = 2, c = 10, d = 11;
    System.out.printf("%.5f",
               getProbability(a, b, c, d));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the probability
# of A winning
def getProbability(a, b, c, d) :

    # p and q store the values
    # of fractions a / b and c / d
    p = a / b;
    q = c / d;

    # To store the winning probability of A
    ans = p * (1 / (1 - (1 - q) * (1 - p)));

    return round(ans,5);

# Driver code
if __name__ == "__main__" :

    a = 1; b = 2; c = 10; d = 11;
    print(getProbability(a, b, c, d));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the probability
// of A winning
public static double getProbability(int a, int b,
                                    int c, int d)
{

    // p and q store the values
    // of fractions a / b and c / d
    double p = (double) a / (double) b;
    double q = (double) c / (double) d;

    // To store the winning probability of A
    double ans = p * (1 / (1 - (1 - q) *
                               (1 - p)));
    return ans;
}

// Driver code
public static void Main(string[] args)
{
    int a = 1, b = 2, c = 10, d = 11;
    Console.Write("{0:F5}",
                   getProbability(a, b, c, d));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the probability
// of A winning
function getProbability($a, $b, $c, $d)
{

    // p and q store the values
    // of fractions a / b and c / d
    $p = $a / $b;
    $q = $c / $d;

    // To store the winning probability of A
    $ans = $p * (1 / (1 - (1 - $q) * (1 - $p)));
    return round($ans,6);
}

// Driver code
$a = 1;
$b = 2;
$c = 10;
$d = 11;
echo getProbability($a, $b, $c, $d);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach   

// Function to return the probability
// of A winning
    function getProbability(a , b , c , d) {

        // p and q store the values
        // of fractions a / b and c / d
        var p =  a /  b;
        var q =  c /  d;

        // To store the winning probability of A
        var ans = p * (1 / (1 - (1 - q) * (1 - p)));
        return ans;
    }

    // Driver code

        var a = 1, b = 2, c = 10, d = 11;
        document.write( getProbability(a, b, c, d).toFixed(5));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
0.52381
```