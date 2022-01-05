# 在两种不同类型的硬币中随机选择一枚硬币后获得两个连续头像的概率

> 原文:[https://www . geeksforgeeks . org/从两种不同类型的硬币中随机选择一枚硬币后获得两个连续头像的概率/](https://www.geeksforgeeks.org/probability-of-getting-two-consecutive-heads-after-choosing-a-random-coin-among-two-different-types-of-coins/)

给定两枚分别具有获得人头 *p%* 和 *q%* 概率的硬币，任务是在给定硬币中随机选择硬币后，确定获得两个连续人头的概率。
**例:**

> **输入:** p = 33，q = 66
> **输出:**0.55000000000000
> **输入:** p = 33，q = 66
> **输出:**0.5500000000000

**方法:**
由于两个硬币不相同，因此[贝叶斯定理](https://www.geeksforgeeks.org/bayess-theorem-for-conditional-probability/)将用于获得期望的概率。
由于硬币是随机选择的，因此可以选择其中任何一种，因此计算中将包括 *p* 和 *q* 。应用贝叶斯定理后，需要的答案将是 *(p * p + q * q) / (p + q)* ，因为如果选择第一枚硬币，那么两个头像背对背的概率是 *p * p* ，第二枚硬币也是一样。
是贝叶斯定理的应用。

> p(b | a)= p(a |^| b)/p(a)=(1/2 * p * p+1/2 * q * q)/(1/2 * p+1/2 * q)=(p * p+q * q)/(p+q)其中:
> P(B) =第二次投掷获得人头的概率，
> P(A) =第一次投掷获得人头的概率，
> P(A |^| B) =两次投掷都获得人头的概率。
> 所以，P(B | A)是第二次投掷获得人头的概率，前提是我们在第一次投掷中获得人头
> 。
> 此处 A、B 表示第 1、2 枚硬币。

以下是上述方法的实现:

## C++

```
// C++ program to get the probability
// of getting two consecutive heads
#include <bits/stdc++.h>
using namespace std;

// Function to return the probability
// of getting two consecutive heads
double getProbability(double p, double q)
{
    p /= 100;
    q /= 100;

    // Formula derived from Bayes's theorem
    double probability = (p * p + q * q) / (p + q);
    return probability;
}

// Driver code
int main()
{
    double p, q;

    // given the probability of getting
    // a head for both the coins
    p = 80;
    q = 40;

    cout << fixed
         << setprecision(15)
         << getProbability(p, q)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get the probability
// of getting two consecutive heads

import java.io.*;

class GFG {

// Function to return the probability
// of getting two consecutive heads
static double getProbability(double p, double q)
{
    p /= 100;
    q /= 100;

    // Formula derived from Bayes's theorem
    double probability = (p * p + q * q) / (p + q);
    return probability;
}

// Driver code

    public static void main (String[] args) {
            double p, q;

    // given the probability of getting
    // a head for both the coins
    p = 80;
    q = 40;

     System.out.println( getProbability(p, q));
    }
}
// This code is contributed by  anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to get the probability
# of getting two consecutive heads

# Function to return the probability
# of getting two consecutive heads
def getProbability(p, q):

    p /= 100
    q /= 100

    # Formula derived from Bayes's theorem
    probability = (p * p + q * q) / (p + q)
    return probability

# Driver code
if __name__ == "__main__":

    # given the probability of getting
    # a head for both the coins
    p = 80
    q = 40

    print(getProbability(p, q))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to get the probability
// of getting two consecutive heads
using System;

class GFG {

// Function to return the probability
// of getting two consecutive heads
static double getProbability(double p, double q)
{
    p /= 100;
    q /= 100;

    // Formula derived from Bayes's theorem
    double probability = (p * p + q * q) / (p + q);
    return probability;
}

// Driver code

    public static void Main () {
            double p, q;

    // given the probability of getting
    // a head for both the coins
    p = 80;
    q = 40;

    Console.WriteLine( getProbability(p, q));
    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get the probability
// of getting two consecutive heads

// Function to return the probability
// of getting two consecutive heads
function getProbability($p, $q)
{
    $p /= 100;
    $q /= 100;

    // Formula derived from
    // Bayes's theorem
    $probability = ($p * $p + $q * $q) /
                             ($p + $q);
    return $probability;
}

// Driver code

// given the probability of getting
// a head for both the coins
$p = 80;
$q = 40;

echo getProbability($p, $q);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to get the probability
// of getting two consecutive heads

// Function to return the probability
// of getting two consecutive heads
function getProbability(p, q)
{
    p /= 100;
    q /= 100;

    // Formula derived from Bayes's theorem
    let probability = (p * p + q * q) / (p + q);
    return probability;
}

// Driver code

// given the probability of getting
// a head for both the coins
let p = 80.0;
let q = 40.0;

document.write(getProbability(p, q).toPrecision(15));

</script>
```

**Output:** 

```
0.666666666666667
```