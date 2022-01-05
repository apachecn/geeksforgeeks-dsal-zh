# 程序评估表达式(√X+1)^6 + (√X-1)^6

> 原文:[https://www . geesforgeks . org/program-to-evaluate-the-expression-x16-x-16/](https://www.geeksforgeeks.org/program-to-evaluate-the-expression-x16-x-16/)

给定一个数字![X   ](img/762b631baf020ff3da5b384db552f364.png "Rendered by QuickLaTeX.com")。任务是为![X   ](img/762b631baf020ff3da5b384db552f364.png "Rendered by QuickLaTeX.com")的给定值找到下面表达式的值。

**例:**

> **输入** : X = √2
> **输出** : 198
> **解释** : ![2[(\sqrt[]{2})^6 + 15 (\sqrt[]{2})^4 + 15\sqrt[]{2})^2 + 1]   ](img/5ebbb3f1c8746c6237babeda822c18d5.png "Rendered by QuickLaTeX.com")
> = 198
> **输入** : X = 3
> **输出** : 4160

**方法:**思路是使用二项式表达式。我们可以把这两个项看作两个二项式。通过扩展这些项，我们可以找到期望的和。下面是术语的扩展。

> ![\newline (X+1)^6 = {6_C}_0 X^6+6_c_1 X^5+{6_C}_2 X^4+{6_C}_3 X^3+{6_C}_4 X^2+{6_C}_5 X+{6_C}_6 \newline (X-1)^6 = {6_C}_0 X^6-6_c_1 X^5+{6_C}_2 X^4-{6_C}_3 X^3+{6_C}_4 X^2-{6_C}_5 X+{6_C}_6 \newline (X+1)^6+(X-1)^6 =2[{6_C}_0 X^6+{6_C}_2 X^4+{6_C}_4 X^2+{6_C}_6] \newline \newline (X+1)^6+(X-1)^6=2[X^6 + 15 X^4 + 15 X^2 +1] ---EQ(1)   ](img/cc53453786ab6235e85247a497cfa61e.png "Rendered by QuickLaTeX.com")

**现在把 X=** ![  ](img/0faf5aa5dcca41fbedb26b2cadf9f952.png "Rendered by QuickLaTeX.com") **放到 EQ(1)** 

> ![\newline (\sqrt[]{2}+1)^6+(\sqrt[]{2}-1)^6 = 2[(\sqrt[]{2})^6 + 15 (\sqrt[]{2})^4 + 15\sqrt[]{2})^2 + 1] \newline = 2(8 + 15 x 4 + 15 x 2 + 1 ) \newline = 2(8 + 60 + 30 + 1) \newline = 198   ](img/d5961cfb1308de479f9e0b4ec46311fd.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// CPP program to evaluate the given expression
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
float calculateSum(float n)
{
    int a = int(n);

    return 2 * (pow(n, 6) + 15 * pow(n, 4)
            + 15 * pow(n, 2) + 1);
}

// Driver Code
int main()
{
    float n = 1.4142;

    cout << ceil(calculateSum(n)) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate the given expression
import java.util.*;

class gfg
{
// Function to find the sum
public static double calculateSum(double n)
{
    return 2 * (Math.pow(n, 6) + 15 * Math.pow(n, 4)
            + 15 * Math.pow(n, 2) + 1);
}

// Driver Code
public static void main(String[] args)
{
    double n = 1.4142;
    System.out.println((int)Math.ceil(calculateSum(n)));
}
}
//This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to evaluate
# the given expression

import math

#Function to find the sum
def calculateSum(n):

    a = int(n)

    return (2 * (pow(n, 6) + 15 * pow(n, 4)
            + 15 * pow(n, 2) + 1))

#Driver Code
if __name__=='__main__':
    n = 1.4142
    print(math.ceil(calculateSum(n)))

# this code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to evaluate the given expression
using System;
class gfg
{
// Function to find the sum
public static double calculateSum(double n)
{
    return 2 * (Math.Pow(n, 6) + 15 * Math.Pow(n, 4)
            + 15 * Math.Pow(n, 2) + 1);
}

// Driver Code
public static int Main()
{
    double n = 1.4142;
    Console.WriteLine(Math.Ceiling(calculateSum(n)));
    return 0;
}
}
//This code is contributed by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to evaluate
// the given expression

//Function to find the sum
function calculateSum($n)
{
    $a = (int)$n;

    return (2 * (pow($n, 6) +
            15 * pow($n, 4) +
            15 * pow($n, 2) + 1));
}

// Driver Code
$n = 1.4142;
echo ceil(calculateSum($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to evaluate the given expression

// Function to find the sum
function calculateSum(n)
{
    return 2 * (Math.pow(n, 6) + 15 * Math.pow(n, 4)
            + 15 * Math.pow(n, 2) + 1);
}

// Driver Code
var n = 1.4142;
document.write(parseInt(Math.ceil(calculateSum(n))));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
198
```