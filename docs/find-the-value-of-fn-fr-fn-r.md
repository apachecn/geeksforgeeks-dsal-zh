# 求 f(n) / f(r) * f(n-r)的值

> 原文:[https://www.geeksforgeeks.org/find-the-value-of-fn-fr-fn-r/](https://www.geeksforgeeks.org/find-the-value-of-fn-fr-fn-r/)

给定两个正整数 n 和 r，其中 n > r >1。任务是求 f(n)/(f(r)*f(n-r))的值。F(n)定义如下:

> **1<sup>-1</sup>* 2<sup>-2</sup>* 3<sup>-3</sup>*…..n <sup>-n</sup>**

**例:**

```
Input: n = 5, r = 3
Output: 1/200000

Input: n = 3, r = 2
Output: 1/27
```

**解决这个问题的一个天真的方法**是分别计算 f(n)、f(r)和 f(n-r)，然后按照给定的公式计算结果，但是这将花费有点高的时间复杂度。
A **解决这个问题的更好的方法**是找到 r 和 n-r 中的较大值，然后在使用给定函数的性质**f(n)= f(n-1)* n<sup>-n</sup>= f(n-1)/n<sup>n</sup>**后，从分子和分母中消除 f(r)和 f(n-r)中的较大值。然后使用简单循环和[幂函数](https://www.geeksforgeeks.org/power-function-cc/)计算剩余值。
**算法:**

> 查找 max(r，n-r)。
> 从 max(r，n-r)迭代到 n
> 结果=((结果***I<sup>-I</sup>T5)/(I-max(r，n-r)) **<sup>-(i-max(r，n-r))</sup>** )**

以下是上述方法的实现:

## C++

```
// CPP to find the value of f(n)/f(r)*f(n-r)
#include <bits/stdc++.h>
using namespace std;

// Function to find value of given F(n)
int calcFunction(int n, int r)
{
    int finalDenominator = 1;
    int mx = max(r, n - r);

    // iterate over n
    for (int i = mx + 1; i <= n; i++) {

        // calculate result
        int denominator = (int)pow(i, i);
        int numerator = (int)pow(i - mx, i - mx);
        finalDenominator = (finalDenominator
                            * denominator)
                           / numerator;
    }

    // return the result
    return finalDenominator;
}

// Driver code
int main()
{
    int n = 6, r = 2;
    cout << "1/" << calcFunction(n, r) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the value of f(n)/f(r)*f(n-r) 

class GFG {
// Function to find value of given F(n)

    static int calcFunction(int n, int r) {
        int finalDenominator = 1;
        int mx = Math.max(r, n - r);

        // iterate over n
        for (int i = mx + 1; i <= n; i++) {

            // calculate result
            int denominator = (int) Math.pow(i, i);
            int numerator = (int) Math.pow(i - mx, i - mx);
            finalDenominator = (finalDenominator
                    * denominator)
                    / numerator;
        }

        // return the result
        return finalDenominator;
    }

// Driver code
    public static void main(String[] args) {
        int n = 6, r = 2;
        System.out.println("1/" + calcFunction(n, r));

    }
}
// This code is contributed by RAJPUT-JI
```

## 蟒蛇 3

```
# Python3 to find the value of f(n)/f(r)*f(n-r)

# Function to find value of given F(n)
def calcFunction(n, r):

    finalDenominator = 1
    mx = max(r, n - r)

    # iterate over n
    for i in range(mx + 1, n + 1):

        # calculate result
        denominator = pow(i, i)
        numerator = pow(i - mx, i - mx)
        finalDenominator = (finalDenominator *
                            denominator) // numerator

    # return the result
    return finalDenominator

# Driver code
if __name__ == "__main__":

    n = 6
    r = 2
    print("1/", end = "")
    print(calcFunction(n, r))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the value of f(n)/f(r)*f(n-r)
using System;

public class GFG {
// Function to find value of given F(n)

    static int calcFunction(int n, int r) {
        int finalDenominator = 1;
        int mx = Math.Max(r, n - r);

        // iterate over n
        for (int i = mx + 1; i <= n; i++) {

            // calculate result
            int denominator = (int) Math.Pow(i, i);
            int numerator = (int) Math.Pow(i - mx, i - mx);
            finalDenominator = (finalDenominator
                    * denominator)
                    / numerator;
        }

        // return the result
        return finalDenominator;
    }

// Driver code
   public static void Main() {
        int n = 6, r = 2;
        Console.WriteLine("1/" + calcFunction(n, r));

    }
}
// This code is contributed by RAJPUT-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find the value of f(n)/f(r)*f(n-r)

// Function to find value of given F(n)
function calcFunction($n, $r)
{
    $finalDenominator = 1;
    $mx = max($r, $n - $r);

    // iterate over n
    for ($i = $mx + 1; $i <= $n; $i++)
    {

        // calculate result
        $denominator = pow($i, $i);
        $numerator = pow($i - $mx, $i - $mx);
        $finalDenominator = ($finalDenominator *
                             $denominator) /
                             $numerator;
    }

    // return the result
    return $finalDenominator;
}

// Driver code
$n = 6; $r = 2;
echo "1/" , calcFunction($n, $r);

// This code is contributed by anuj_67..
?>
```

## java 描述语言

```
<script>

// Javascript to find the value of f(n)/f(r)*f(n-r)

// Function to find value of given F(n)
function calcFunction(n, r)
{
    var finalDenominator = 1;
    var mx = Math.max(r, n - r);

    // iterate over n
    for (var i = mx + 1; i <= n; i++) {

        // calculate result
        var denominator = Math.pow(i, i);
        var numerator = Math.pow(i - mx, i - mx);
        finalDenominator = (finalDenominator
                            * denominator)
                           / numerator;
    }

    // return the result
    return finalDenominator;
}

// Driver code
var n = 6, r = 2;
document.write( "1/" + calcFunction(n, r));

</script>
```

**Output:** 

```
1/36450000
```