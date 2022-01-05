# n 倍以上的最小整数

> 原文:[https://www.geeksforgeeks.org/smallest-integer-n-factors/](https://www.geeksforgeeks.org/smallest-integer-n-factors/)

给定 n，找出有 n 个或更多因子的最小整数。可以假设结果小于 1000001。

**示例:**

```
Input : n = 3
Output : 4
Explanation: 4 has factors 1, 2 and 4.

Input : n = 2 
Output : 2
Explanation: 2 has one factor 1 and 2\. 
```

计算因子数的方法有很多，但最有效的方法可以在这里找到
**简单方法:**一个简单的方法是运行一个循环来找出一个数的因子。求一个数在 O(x)中的因子的一种方法是从 1 到 x 运行一个循环，看到所有除以 x 的数。
时间复杂度:对于我们尝试的每个数 x，O(x)，直到找到答案或达到极限。

**有效方法:**我们可以找出每次迭代的 [sqrt(x)](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 中的因素。
时间复杂度:O(sqrt(x))对于我们尝试的每个数字 x，直到找到答案或达到极限。

**最好的方法**是遍历每一个数，计算[数的因子](https://www.geeksforgeeks.org/efficient-program-print-number-factors-n-numbers/)。然后检查计数是否等于或大于 n，然后我们得到所需的具有 n 个或更多因子的最小整数。
以下是上述方法的实施:

## C++

```
// c++ program to print the smallest
// integer with n factors or more
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000001;

// array to store prime factors
int factor[MAX] = { 0 };

// function to generate all prime factors
// of numbers from 1 to 10^6
void generatePrimeFactors()
{
    factor[1] = 1;

    // Initializes all the positions
    // with their value.
    for (int i = 2; i < MAX; i++)
        factor[i] = i;

    // Initializes all multiples of 2 with 2
    for (int i = 4; i < MAX; i += 2)
        factor[i] = 2;

    // A modified version of Sieve of
    // Eratosthenes to store the smallest
    // prime factor that divides every number.
    for (int i = 3; i * i < MAX; i++) {

        // check if it has no prime factor.
        if (factor[i] == i) {

            // Initializes of j starting from i*i
            for (int j = i * i; j < MAX; j += i) {

                // if it has no prime factor
                // before, then stores the
                // smallest prime divisor
                if (factor[j] == j)
                    factor[j] = i;
            }
        }
    }
}

// function to calculate number of factors
int calculateNoOFactors(int n)
{
    if (n == 1)
        return 1;

    int ans = 1;

    // stores the smallest prime number
    // that divides n
    int dup = factor[n];

    // stores the count of number of times
    // a prime number divides n.
    int c = 1;

    // reduces to the next number after prime
    // factorization of n
    int j = n / factor[n];

    // false when prime factorization is done
    while (j != 1) {

        // if the same prime number is dividing n,
        // then we increase the count
        if (factor[j] == dup)
            c += 1;

        /* if its a new prime factor that is
           factorizing n, then we again set c=1
           and change dup to the new prime factor,
           and apply the formula explained above. */
        else {
            dup = factor[j];
            ans = ans * (c + 1);
            c = 1;
        }

        // prime factorizes a number
        j = j / factor[j];
    }

    // for the last prime factor
    ans = ans * (c + 1);

    return ans;
}

// function to find the smallest integer
// with n factors or more.
int smallest(int n)
{
    for (int i = 1;; i++)

        // check if no of factors is more
        // than n or not
        if (calculateNoOFactors(i) >= n)
            return i;
}

// Driver program to test above function
int main()
{
    // generate prime factors of number
    // upto 10^6
    generatePrimeFactors();

    int n = 4;
    cout << smallest(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the smallest
// integer with n factors or more
import java.util.*;
import java.lang.*;

public class GfG{
    private static final int MAX = 1000001;

    // array to store prime factors
    private static final int[] factor = new int [MAX];

    // function to generate all prime factors
    // of numbers from 1 to 10^6
    public static void generatePrimeFactors()
    {
        factor[1] = 1;

        // Initializes all the positions
        // with their value.
        for (int i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of 2 with 2
        for (int i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the smallest
        // prime factor that divides every number.
        for (int i = 3; i * i < MAX; i++) {

            // check if it has no prime factor.
            if (factor[i] == i) {

                // Initializes of j starting from i*i
                for (int j = i * i; j < MAX; j += i) {

                    // if it has no prime factor
                    // before, then stores the
                    // smallest prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate number of factors
    public static int calculateNoOFactors(int n)
    {
        if (n == 1)
            return 1;

        int ans = 1;

        // stores the smallest prime number
        // that divides n
        int dup = factor[n];

        // stores the count of number of times
        // a prime number divides n.
        int c = 1;

        // reduces to the next number after prime
        // factorization of n
        int j = n / factor[n];

        // false when prime factorization is done
        while (j != 1) {

            // if the same prime number is dividing n,
            // then we increase the count
            if (factor[j] == dup)
                c += 1;

            /* if its a new prime factor that is
            factorizing n, then we again set c=1
            and change dup to the new prime factor,
            and apply the formula explained above. */
            else {
                dup = factor[j];
                ans = ans * (c + 1);
                c = 1;
            }

            // prime factorizes a number
            j = j / factor[j];
        }

        // for the last prime factor
        ans = ans * (c + 1);

        return ans;
    }

    // function to find the smallest integer
    // with n factors or more.
    public static int smallest(int n)
    {
        for (int i = 1;; i++)

            // check if no of factors is more
            // than n or not
            if (calculateNoOFactors(i) >= n)
                return i;
    }

    // driver function
    public static void main(String args[])
    {
        // generate prime factors of number
        // upto 10^6
        generatePrimeFactors();

        int n = 4;
        System.out.println(smallest(n));
    }
}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python3 program to print the
# smallest integer with n
# factors or more
MAX = 100001;

# array to store
# prime factors
factor = [0] * MAX;

# function to generate all
# prime factors of numbers
# from 1 to 10^6
def generatePrimeFactors():

    factor[1] = 1;

    # Initializes all the
    # positions with their value.
    for i in range(2, MAX):
        factor[i] = i;

    # Initializes all
    # multiples of 2 with 2
    i = 4
    while(i < MAX):
        factor[i] = 2;
        i += 2;

    # A modified version of
    # Sieve of Eratosthenes
    # to store the smallest
    # prime factor that
    # divides every number.
    i = 3;
    while(i * i < MAX):

        # check if it has
        # no prime factor.
        if (factor[i] == i):

            # Initializes of j
            # starting from i*i
            j = i * i;
            while(j < MAX):

                # if it has no prime factor
                # before, then stores the
                # smallest prime divisor
                if (factor[j] == j):
                    factor[j] = i;
                j += i;
        i += 1;

# function to calculate
# number of factors
def calculateNoOFactors(n):
    if (n == 1):
        return 1;

    ans = 1;

    # stores the smallest prime
    # number that divides n
    dup = factor[n];

    # stores the count of
    # number of times a
    # prime number divides n.
    c = 1;

    # reduces to the next
    # number after prime
    # factorization of n
    j = int(n / factor[n]);

    # false when prime
    # factorization is done
    while (j != 1):

        # if the same prime number
        # is dividing n, then we
        # increase the count
        if (factor[j] == dup):
            c += 1;

        # if its a new prime factor
        # that is factorizing n, then
        # we again set c=1 and change
        # dup to the new prime factor,
        # and apply the formula
        # explained above.
        else:
            dup = factor[j];
            ans = ans * (c + 1);
            c = 1;

        # prime factorizes a number
        j = int(j / factor[j]);

    # for the last prime factor
    ans = ans * (c + 1);

    return ans;

# function to find the
# smallest integer with
# n factors or more.
def smallest(n):
    i = 1;
    while(True):

        # check if no of
        # factors is more
        # than n or not
        if (calculateNoOFactors(i) >= n):
            return i;
        i += 1;

# Driver Code

# generate prime factors
# of number upto 10^6
generatePrimeFactors();

n = 4;
print(smallest(n));

# This code is contributed by mits
```

## C#

```
// C# program to print the smallest
// integer with n factors or more
using System;

class GfG {
    private static int MAX = 1000001;

    // array to store prime factors
    private static int []factor = new int [MAX];

    // function to generate all prime
    // factorsof numbers from 1 to 10^6
    public static void generatePrimeFactors()
    {
        factor[1] = 1;

        // Initializes all the positions
        // with their value.
        for (int i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of 2 with 2
        for (int i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the smallest
        // prime factor that divides every number.
        for (int i = 3; i * i < MAX; i++) {

            // check if it has no prime factor.
            if (factor[i] == i) {

                // Initializes of j starting from i*i
                for (int j = i * i; j < MAX; j += i)
                {

                    // if it has no prime factor
                    // before, then stores the
                    // smallest prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate number of factors
    public static int calculateNoOFactors(int n)
    {
        if (n == 1)
            return 1;

        int ans = 1;

        // stores the smallest prime number
        // that divides n
        int dup = factor[n];

        // stores the count of number of times
        // a prime number divides n.
        int c = 1;

        // reduces to the next number after prime
        // factorization of n
        int j = n / factor[n];

        // false when prime factorization is done
        while (j != 1) {

            // if the same prime number is dividing n,
            // then we increase the count
            if (factor[j] == dup)
                c += 1;

            // if its a new prime factor that is
            // factorizing n, then we again set c=1
            // and change dup to the new prime factor,
            // and apply the formula explained above.
            else {
                dup = factor[j];
                ans = ans * (c + 1);
                c = 1;
            }

            // prime factorizes a number
            j = j / factor[j];
        }

        // for the last prime factor
        ans = ans * (c + 1);

        return ans;
    }

    // function to find the smallest integer
    // with n factors or more.
    public static int smallest(int n)
    {
        for (int i = 1; ; i++)

            // check if no of factors is more
            // than n or not
            if (calculateNoOFactors(i) >= n)
                return i;
    }

    // Driver Code
    public static void Main()
    {

        // generate prime factors of
        // number upto 10^6
        generatePrimeFactors();

        int n = 4;
        Console.Write(smallest(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the
// smallest integer with n
// factors or more

$MAX = 100001;

// array to store
// prime factors
$factor = array_fill(0, $MAX, 0);

// function to generate all
// prime factors of numbers
// from 1 to 10^6
function generatePrimeFactors()
{
    global $MAX;
    global $factor;
    $factor[1] = 1;

    // Initializes all the
    // positions with their value.
    for ($i = 2; $i < $MAX; $i++)
        $factor[$i] = $i;

    // Initializes all
    // multiples of 2 with 2
    for ($i = 4; $i < $MAX; $i += 2)
        $factor[$i] = 2;

    // A modified version of
    // Sieve of Eratosthenes
    // to store the smallest
    // prime factor that
    // divides every number.
    for ($i = 3; $i * $i < $MAX; $i++)
    {

        // check if it has
        // no prime factor.
        if ($factor[$i] == $i)
        {

            // Initializes of j
            // starting from i*i
            for ($j = $i * $i;
                 $j < $MAX; $j += $i)
            {

                // if it has no prime factor
                // before, then stores the
                // smallest prime divisor
                if ($factor[$j] == $j)
                    $factor[$j] = $i;
            }
        }
    }
}

// function to calculate
// number of factors
function calculateNoOFactors($n)
{
    global $factor;
    if ($n == 1)
        return 1;

    $ans = 1;

    // stores the smallest prime
    // number that divides n
    $dup = $factor[$n];

    // stores the count of
    // number of times a
    // prime number divides n.
    $c = 1;

    // reduces to the next
    // number after prime
    // factorization of n
    $j = (int)($n / $factor[$n]);

    // false when prime
    // factorization is done
    while ($j != 1)
    {

        // if the same prime number
        // is dividing n, then we
        // increase the count
        if ($factor[$j] == $dup)
            $c += 1;

        /* if its a new prime factor
        that is factorizing n, then
        we again set c=1 and change
        dup to the new prime factor,
        and apply the formula
        explained above. */
        else
        {
            $dup = $factor[$j];
            $ans = $ans * ($c + 1);
            $c = 1;
        }

        // prime factorizes a number
        $j = (int)($j / $factor[$j]);
    }

    // for the last prime factor
    $ans = $ans * ($c + 1);

    return $ans;
}

// function to find the
// smallest integer with
// n factors or more.
function smallest($n)
{
    for ($i = 1;; $i++)

        // check if no of
        // factors is more
        // than n or not
        if (calculateNoOFactors($i) >= $n)
            return $i;
}

// Driver Code

// generate prime factors
// of number upto 10^6
generatePrimeFactors();

$n = 4;
echo smallest($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to print the smallest
// integer with n factors or more

    var MAX = 1000001;

    // array to store prime factors
    var factor = Array(MAX).fill(0);

    // function to generate all prime factors
    // of numbers from 1 to 10^6
    function generatePrimeFactors() {
        factor[1] = 1;

        // Initializes all the positions
        // with their value.
        for (i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of 2 with 2
        for (i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the smallest
        // prime factor that divides every number.
        for (i = 3; i * i < MAX; i++) {

            // check if it has no prime factor.
            if (factor[i] == i) {

                // Initializes of j starting from i*i
                for (j = i * i; j < MAX; j += i) {

                    // if it has no prime factor
                    // before, then stores the
                    // smallest prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate number of factors
    function calculateNoOFactors(n) {
        if (n == 1)
            return 1;

        var ans = 1;

        // stores the smallest prime number
        // that divides n
        var dup = factor[n];

        // stores the count of number of times
        // a prime number divides n.
        var c = 1;

        // reduces to the next number after prime
        // factorization of n
        var j = n / factor[n];

        // false when prime factorization is done
        while (j != 1) {

            // if the same prime number is dividing n,
            // then we increase the count
            if (factor[j] == dup)
                c += 1;

            /*
             * if its a new prime factor that is factorizing n, then we again set c=1 and
             * change dup to the new prime factor, and apply the formula explained above.
             */
            else {
                dup = factor[j];
                ans = ans * (c + 1);
                c = 1;
            }

            // prime factorizes a number
            j = j / factor[j];
        }

        // for the last prime factor
        ans = ans * (c + 1);

        return ans;
    }

    // function to find the smallest integer
    // with n factors or more.
    function smallest(n) {
        for (i = 1;; i++)

            // check if no of factors is more
            // than n or not
            if (calculateNoOFactors(i) >= n)
                return i;
    }

    // driver function

        // generate prime factors of number
        // upto 10^6
        generatePrimeFactors();

        var n = 4;
        document.write(smallest(n));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
6
```

**时间复杂度:** O(log(max(number)))对于我们在得到答案之前检查的每个计算数。