# 计算复利的程序

> 原文:[https://www . geesforgeks . org/program-find-复利/](https://www.geeksforgeeks.org/program-find-compound-interest/)

**什么是“复利”？**
**复利**是贷款或存款本金加上利息，换句话说，就是利息的利息。它是利息再投资的结果，而不是支付利息，这样下一期的利息就可以从本金加上以前积累的利息中获得。复利是金融学和经济学的标准。
复利可能和单利形成对比，单利没有利息加本金，所以没有复利。
**复利公式:**

计算年复利的公式为:
**金额= P(1 + R/100) <sup>t</sup>**

**复利=金额–P**
其中，
P 为本金金额
R 为利率，
T 为时间跨度

**伪代码:**

```
Input principle amount. Store it in some variable say principle.
Input time in some variable say time.
Input rate in some variable say rate.
Calculate Amount using formula, 
Amount = principle * (1 + rate / 100)  time).
Calculate Compound Interest using Formula.
Finally, print the resultant value of CI.
```

**例:**

```
Input : Principle (amount): 1200
        Time: 2
        Rate: 5.4
Output : Compound Interest = 133.099243
```

## C++

```
// CPP program to find compound interest for
// given values.
#include <bits/stdc++.h>
using namespace std;

int main()
{
    double principle = 10000, rate = 5, time = 2;

    /* Calculate compound interest */
    double A = principle * (pow((1 + rate / 100), time));
      double CI = A- principle;

    cout << "Compound interest is " << CI;

    return 0;
}
//This Code is Contributed by Sahil Rai.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find compound interest for
// given values.
import java.io.*;

class GFG
{
    public static void main(String args[])
    {
        double principle = 10000, rate = 5, time = 2;

        /* Calculate compound interest */
        double A = principle *
                    (Math.pow((1 + rate / 100), time));
          double CI = A - principle;

        System.out.println("Compound Interest is "+ CI);
    }
}

//This Code is Contributed by Sahil Rai.
```

## 蟒蛇 3

```
# Python3 program to find compound
# interest for given values.

def compound_interest(principle, rate, time):

    # Calculates compound interest
    A = principle * (pow((1 + rate / 100), time))
    CI= A - principle
    print("Compound interest is", CI)

compound_interest(10000, 5, 2)

#This Code is Contributed by Sahil Rai.
```

## C#

```
// C# program to find compound
// interest for given values
using System;

class GFG {

    // Driver Code
    public static void Main()
    {
        double principle = 10000, rate = 5, time = 2;

        // Calculate compound interest
        double A = principle * (Math.Pow((1 +
                    rate / 100), time));
          double CI = A - principle;

        Console.Write("Compound Interest is "+ CI);
    }
}

//This Code is Contributed by Sahil Rai.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// compound interest for
// given values.

$principle = 10000;
$rate = 5;
$time = 2;

// Calculate compound interest
$A = $principle * (pow((1 +
      $rate / 100), $time));
$CI = $A - $principle;

echo("Compound interest is " . $CI);

?>
```

## java 描述语言

```
<script>

// JavaScript program to
// find compound interest for
// given values.

    let principle = 10000, rate = 5,
        time = 2;

    /* Calculate compound interest */
    let A = principle *
        (Math.pow((1 + rate / 100), time));
    let CI = A - principle;

    document.write("Compound interest is " + CI);
</script>

// This Code is Contributed by Sahil Rai.
```

**输出:**

```
Compound interest is 1025
```