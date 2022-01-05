# 查询一个数的所有因子的奇数位数和之和

> 原文:[https://www . geeksforgeeks . org/关于奇数数字总和的查询-所有数字因子的总和/](https://www.geeksforgeeks.org/queries-on-sum-of-odd-number-digit-sums-of-all-the-factors-of-a-number/)

给出 **Q** 查询。每个查询包含一个正整数 **n** 。任务是输出 n.
**所有除数中包含的奇数位数之和的和示例:**

> 输入:Q = 2，n1 = 10，n2 = 36
> 输出:7 18
> 对于查询 1，
> 10 的除数是 1，2，5，10。
> 1 中的奇数之和为 1，2 中的奇数为 0，5 中的奇数为 5，10 中的奇数为 1。
> 于是，总和变成了 7。
> 对于查询 2，
> 36 的除数是 1、2、3、4、6、9、12、18、36。
> 1 中的奇数之和是 1，2 中的是 0，3 中的是 3，4 中的是 0，
> 中的 6 是 0，9 中的是 9，12 中的是 1，18 中的是 1，36 中的是 3。
> 于是，总和变成了 18。

其思想是预计算所有数字的奇数位数之和。另外，我们可以用前一个数的奇数位数之和来计算当前数的奇数位数之和。
比如计算“123”的奇数位数之和，可以用“12”和“3”的奇数位数之和。因此，“123”的奇数位之和= 12 的奇数位之和+如果最后一位是奇数(即 3)，则加上最后一位。
现在，要求因子奇数位数之和的和，我们可以利用厄拉多塞的[筛的跳跃现象。所以，对于所有可能的因素，把它们的贡献加到倍数上。
例如，对于 1 作为因子，将 1(因为 1 只有 1 个奇数)加到它的所有倍数上。
2 为因子，所有 2 的倍数加 0，即 2，4，8，…
3 为因子，所有 3 的倍数加 1，即 3，6，9，…..
以下是本办法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP Program to answer queries on sum
// of sum of odd number digits of all
// the factors of a number
#include <bits/stdc++.h>
using namespace std;
#define N 1000005

// finding sum of odd digit number in each integer.
void sumOddDigit(int digitSum[])
{
    // for each number
    for (int i = 1; i < N; i++) {

        // using previous number sum, finding
        // the current number num of odd digit
        // also, adding last digit if it is odd.
        digitSum[i] = digitSum[i / 10] + (i & 1) * (i % 10);
    }
}

// finding sum of sum of odd digit of all
// the factors of a number.
void sumFactor(int digitSum[], int factorDigitSum[])
{
    // for each possible factor
    for (int i = 1; i < N; i++) {
        for (int j = i; j < N; j += i) {

            // adding the contribution.
            factorDigitSum[j] += digitSum[i];
        }
    }
}

// Wrapper function
void wrapper(int q, int n[])
{
    int digitSum[N];
    int factorDigitSum[N];

    sumOddDigit(digitSum);
    sumFactor(digitSum, factorDigitSum);

    for (int i = 0; i < q; i++)
        cout << factorDigitSum[n[i]] << " ";
}

// Driver Program
int main()
{
    int q = 2;
    int n[] = { 10, 36 };

    wrapper(q, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to answer queries
// on sum of sum of odd number 
// digits of all the factors of
// a number
class GFG
{
    static int N = 1000005;

    // finding sum of odd digit
    // number in each integer.
    static void sumOddDigit(int digitSum[])
    {

        // for each number
        for (int i = 1; i < N; i++)
        {

            // using previous number sum,
            // finding the current number
            // num of odd digit also,
            // adding last digit if it
            // is odd.
            digitSum[i] = digitSum[i / 10] +
                         (i & 1) * (i % 10);
        }
    }

    // finding sum of sum of odd digit
    // of all the factors of a number.
    static void sumFactor(int digitSum[],
                    int factorDigitSum[])
    {

        // for each possible factor
        for (int i = 1; i < N; i++)
        {
            for (int j = i; j < N; j += i)
            {
                // adding the contribution.
                factorDigitSum[j] += digitSum[i];
            }
        }
    }

    // Wrapper function
    static void wrapper(int q, int n[])
    {
        int digitSum[] = new int[N];
        int factorDigitSum[] = new int[N];

        sumOddDigit(digitSum);
        sumFactor(digitSum, factorDigitSum);

        for (int i = 0; i < q; i++)
            System.out.print(factorDigitSum[n[i]]
                                          + " ");
    }

    // Driver Code
    public static void main(String args[])
    {
        int q = 2;
        int n[] = new int[]{10, 36};

        wrapper(q, n);

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python Program to answer queries
# on sum of sum of odd number
# digits of all the factors
# of a number
N = 100
digitSum = [0] * N
factorDigitSum = [0] * N

# finding sum of odd digit
# number in each integer.
def sumOddDigit() :
    global N,digitSum,factorDigitSum

    # for each number
    for i in range(1, N) :

        # using previous number
        # sum, finding the current
        # number num of odd digit
        # also, adding last digit
        # if it is odd.
        digitSum[i] = (digitSum[int(i / 10)]
                    + int(i & 1) * (i % 10))

# finding sum of sum of
# odd digit of all the
# factors of a number.
def sumFactor() :
    global N,digitSum,factorDigitSum
    j = 0

    # for each possible factor
    for i in range(1, N) :
        j = i
        while (j < N) :

            # adding the contribution.
            factorDigitSum[j] = (factorDigitSum[j]
                                   + digitSum[i])
            j = j + i

# Wrapper def
def wrapper(q, n) :

    global N,digitSum,factorDigitSum

    for i in range(0, N) :    
        digitSum[i] = 0
        factorDigitSum[i] = 0

    sumOddDigit()
    sumFactor()

    for i in range(0, q) :
        print ("{} ".
        format(factorDigitSum[n[i]]), end = "")

# Driver Code
q = 2
n = [ 10, 36 ]
wrapper(q, n)

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program to answer queries on sum
// of sum of odd number digits of all
// the factors of a number
using System;

class GFG {

    static int N = 1000005;

    // finding sum of odd digit number in
    // each integer.
    static void sumOddDigit(int []digitSum)
    {

        // for each number
        for (int i = 1; i < N; i++) {

            // using previous number sum,
            // finding the current number
            // num of odd digit also,
            // adding last digit if it
            // is odd.
            digitSum[i] = digitSum[i / 10]
                     + (i & 1) * (i % 10);
        }
    }

    // finding sum of sum of odd digit
    // of all the factors of a number.
    static void sumFactor(int []digitSum,
                     int []factorDigitSum)
    {

        // for each possible factor
        for (int i = 1; i < N; i++) {
            for (int j = i; j < N; j += i)
            {
                // adding the contribution.
                factorDigitSum[j] += digitSum[i];
            }
        }
    }

    // Wrapper function
    static void wrapper(int q, int []n)
    {
        int []digitSum = new int[N];
        int []factorDigitSum = new int[N];

        sumOddDigit(digitSum);
        sumFactor(digitSum, factorDigitSum);

        for (int i = 0; i < q; i++)
            Console.Write(factorDigitSum[n[i]]
                                       + " ");
    }

    // Driver code
    public static void Main()
    {
        int q = 2;
        int []n = new int[]{ 10, 36 };

        wrapper(q, n);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to answer queries
// on sum of sum of odd number
// digits of all the factors
// of a number
$N = 1000005;

// finding sum of odd digit
// number in each integer.
function sumOddDigit(&$digitSum)
{
    global $N;
    // for each number
    for ($i = 1; $i < $N; $i++)
    {

        // using previous number
        // sum, finding the current
        // number num of odd digit
        // also, adding last digit
        // if it is odd.
        $digitSum[$i] = $digitSum[intval($i / 10)] +
                                  intval($i & 1) *
                                        ($i % 10);
    }
}

// finding sum of sum of
// odd digit of all the
// factors of a number.
function sumFactor($digitSum,
                   &$factorDigitSum)
{
    global $N;

    // for each possible factor
    for ($i = 1; $i < $N; $i++)
    {
        for ($j = $i; $j < $N; $j += $i)
        {

            // adding the contribution.
            $factorDigitSum[$j] += $digitSum[$i];
        }
    }
}

// Wrapper function
function wrapper($q, $n)
{
    global $N;
    $digitSum = array();
    $factorDigitSum = array();

    for ($i = 0; $i < $N; $i++)
    {
        $digitSum[$i] = 0;
        $factorDigitSum[$i] = 0;
    }
    sumOddDigit($digitSum);
    sumFactor($digitSum, $factorDigitSum);

    for ($i = 0; $i < $q; $i++)
        echo ($factorDigitSum[$n[$i]]. " ");
}

// Driver Code
$q = 2;
$n = array( 10, 36 );
wrapper($q, $n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript Program to answer queries on sum
// of sum of odd number digits of all
// the factors of a number
var N = 1000005;

// finding sum of odd digit number in each integer.
function sumOddDigit(digitSum)
{
    // for each number
    for (var i = 1; i < N; i++) {

        // using previous number sum, finding
        // the current number num of odd digit
        // also, adding last digit if it is odd.
        digitSum[i] = digitSum[parseInt(i / 10)] + (i & 1) * (i % 10);
    }
}

// finding sum of sum of odd digit of all
// the factors of a number.
function sumFactor(digitSum, factorDigitSum)
{
    // for each possible factor
    for (var i = 1; i < N; i++) {
        for (var j = i; j < N; j += i) {

            // adding the contribution.
            factorDigitSum[j] += digitSum[i];
        }
    }
}

// Wrapper function
function wrapper(q, n)
{
    var digitSum = Array(N).fill(0);
    var factorDigitSum = Array(N).fill(0);

    sumOddDigit(digitSum);
    sumFactor(digitSum, factorDigitSum);

    for (var i = 0; i < q; i++)
        document.write( factorDigitSum[n[i]] + " ");
}

// Driver Program
var q = 2;
var n = [ 10, 36 ];
wrapper(q, n);

// This code is contributed by noob2000.
</script>
```

**Output :** 

```
7 18
```