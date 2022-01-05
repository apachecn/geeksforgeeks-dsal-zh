# 给定范围内所有可被 6 整除的数的和

> 原文:[https://www . geesforgeks . org/sum-numbers-除数-6-给定范围/](https://www.geeksforgeeks.org/sum-numbers-divisible-6-given-range/)

给定一个 L-R 范围，在 L-R 范围内找到所有可被 6 整除的数的和
L 和 R 都很大。
示例:

```
Input : 1 20
Output : 36 
Explanation: 6 + 12 + 18 = 36 

Input : 5 7  
Output : 6
Explanation: 6 is the only divisible number 
in range 5-7 
```

一种天真的方法是从 L 到 R 循环，将所有能被 6 整除的数字相加。
一个**有效的方法**是将所有可被 6 整除的数加起来，直到和为 R，将所有可被 6 整除的数加起来，直到 L-1。然后减法就会有答案。
总和= 6 + 12 + 8 + ……。(第 6 条)条款。
总和= 6(1 + 2 + 3……R/6 项)

> sumR = 3 * (R/6) * (R/6+1)

同样，我们得到

> sumL 为 3 *(L-1)/6)*((L-1/6)+1)

最后的答案是 SumR–SumL。

## C++

```
// CPP program to find sum of numbers divisible
// by 6 in a given range.
#include <bits/stdc++.h>
using namespace std;

// function to calculate the sum of
// all numbers divisible by 6 in range L-R..
int sum(int L, int R)
{
    // no of multiples of 6 upto r
    int p = R / 6;

    // no of multiples of 6 upto l-1
    int q = (L - 1) / 6;

    // summation of all multiples of 6 upto r
    int sumR = 3 * (p * (p + 1));

    // summation of all multiples of 6 upto l-1
    int sumL = (q * (q + 1)) * 3;

    // returns the answer
    return sumR - sumL;
}

// driver program to test the above function
int main()
{
    int L = 1, R = 20;
    cout << sum(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of numbers
// divisible by 6 in a given range.
import java.io.*;
class GFG {

// function to calculate the sum
// of all numbers divisible by 6
// in range L-R..
static int sum(int L, int R)
{
    // no of multiples of 6 upto r
    int p = R / 6;

    // no of multiples of 6 upto l-1
    int q = (L - 1) / 6;

    // summation of all multiples of
    // 6 upto r
    int sumR = 3 * (p * (p + 1));

    // summation of all multiples of
    // 6 upto l-1
    int sumL = (q * (q + 1)) * 3;

    // returns the answer
    return sumR - sumL;
}

// driver program
public static void main(String[] args)
{
    int L = 1, R = 20;
    System.out.println(sum(L, R));
}
}

// This code is contributed by Prerna Saini
```

## 计算机编程语言

```
# Python3 program to find sum of numbers divisible
# by 6 in a given range.

def sumDivisible(L, R):

    # no of multiples of 6 upto r
    p = int(R/6)

    # no of multiples of 6 upto l-1
    q = int((L-1)/6)

    # summation of all multiples of 6 upto r
    sumR = 3 * (p * (p + 1))

    # summation of all multiples of 6 upto l-1
    sumL = (q * (q + 1)) * 3

    # returns the answer
    return sumR - sumL

# driver code
L = 1
R = 20
print(sumDivisible(L,R))

# This code is contributed by 'Abhishek Sharma 44'.
```

## C#

```
// C# program to find sum of numbers
// divisible by 6 in a given range.
using System;

class GFG {

    // function to calculate the sum
    // of all numbers divisible by 6
    // in range L-R..
    static int sum(int L, int R)
    {

        // no of multiples of 6 upto r
        int p = R / 6;

        // no of multiples of 6 upto l-1
        int q = (L - 1) / 6;

        // summation of all multiples of
        // 6 upto r
        int sumR = 3 * (p * (p + 1));

        // summation of all multiples of
        // 6 upto l-1
        int sumL = (q * (q + 1)) * 3;

        // returns the answer
        return sumR - sumL;
    }

    // driver program
    public static void Main()
    {
        int L = 1, R = 20;

        Console.WriteLine(sum(L, R));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of numbers
// divisible by 6 in a given range.

// function to calculate the sum of
// all numbers divisible by 6 in range L-R..
function sum($L, $R)
{

    // no of multiples of 6 upto r
    $p = intval($R / 6);

    // no of multiples of 6 upto l-1
    $q = intval(($L - 1) / 6);

    // summation of all multiples
    // of 6 upto r
    $sumR = intval(3 * ($p * ($p + 1)));

    // summation of all multiples
    // of 6 upto l-1
    $sumL = intval(($q * ($q + 1)) * 3);

    // returns the answer
    return $sumR - $sumL;
}

// Driver Code
$L = 1;
$R = 20;
echo sum($L, $R);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
// Javascript program to find sum of numbers divisible
// by 6 in a given range.
<script>

    // function to calculate the sum of
    // all numbers divisible by 6 in range L-R..
    function sum(L, R)
    {
        // no of multiples of 6 upto r
        let p = Math.floor(R / 6);

        // no of multiples of 6 upto l-1
        let q = Math.floor((L - 1) / 6);

        // summation of all multiples of 6 upto r
        let sumR = Math.floor(3 * (p * (p + 1)));

        // summation of all multiples of 6 upto l-1
        let sumL = Math.floor((q * (q + 1)) * 3);

        // returns the answer
        return sumR - sumL;
    }

    // Driver Code
    let L = 1, R = 20;
    document.write(sum(L, R));

    // This code is contributed by ajaykrsharma132.
</script>
```

输出:

```
36
```

时间复杂度:O(1)