# 在给定数 N 的除数中找出最大的好数

> 原文:[https://www . geeksforgeeks . org/find-给定数的除数中最大的好数-n/](https://www.geeksforgeeks.org/find-the-largest-good-number-in-the-divisors-of-given-number-n/)

给定一个数 n .任务是在给定数 n 的除数中找到最大的好数.如果没有这样的正整数 a > 1，那么数 x 被定义为好数，这样 a^2 就是 x 的除数

**示例:**

```
Input: N = 10
Output: 10
In 1, 2, 5, 10\. 
10 is the largest good number

Input: N = 12
Output: 6
In 1, 2, 3, 4, 6, 12\. 
6 is the largest good number 
```

**方法:**求 n 的所有质因数，假设它们是 p1，p2，…，pk(在 O(sqrt(n))时间复杂度中)。如果答案是 a，那么我们知道，对于每一个 1 < = I < = k，很明显，a 不能被 pi^2(以及π的所有更大幂)整除。所以 a < = p1 × p2 ×… × pk。而且我们知道 p1 × p2 × … × pk 本身就是一个好数字。所以，答案是 p1 × p2 ×…× pk。

下面是上述方法的实现:

## C++

```
// CPP program to find the largest, good
// number in the divisors of given number N.
#include <bits/stdc++.h>
using namespace std;

// function to return distinct prime factors
vector<int> PrimeFactors(int n)
{
    // to store distinct prime factors
    vector<int> v;

    int x = n;

    // run a loop upto sqrt(n)
    for (int i = 2; i * i <= n; i++) {
        if (x % i == 0) {

            // place this prime factor in vector
            v.push_back(i);
            while (x % i == 0)
                x /= i;
        }
    }

    // This condition is to handle the case when n
    // is a prime number greater than 1
    if (x > 1)
        v.push_back(x);

    return v;
}

// function that returns good number
int GoodNumber(int n)
{
    // distinct prime factors
    vector<int> v = PrimeFactors(n);

    // to store answer
    int ans = 1;

    // product of all distinct prime
    // factors is required answer
    for (int i = 0; i < v.size(); i++)
        ans *= v[i];

    return ans;
}

// Driver code
int main()
{
    int n = 12;

    // function call
    cout << GoodNumber(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest, good
// number in the divisors of given number N.

import java.util.*;

class GFG {
    // function to return distinct prime factors

    static Vector<Integer> PrimeFactors(int n)
    {

        // to store distinct prime factors
        Vector<Integer> v = new Vector<Integer>();
        int x = n;

        // run a loop upto sqrt(n)
        for (int i = 2; i * i <= n; i++) {
            if (x % i == 0) {

                // place this prime factor in vector
                v.add(i);
                while (x % i == 0)
                    x /= i;
            }
        }

        // This condition is to handle the case when n
        // is a prime number greater than 1
        if (x > 1)
            v.add(x);

        return v;
    }

    // function that returns good number
    static int GoodNumber(int n)
    {
        // distinct prime factors
        Vector<Integer> v = new Vector<Integer>(PrimeFactors(n));

        // to store answer
        int ans = 1;

        // product of all distinct prime
        // factors is required answer
        for (int i = 0; i < v.size(); i++)
            ans *= v.get(i);

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 12;

        // function call
        System.out.println(GoodNumber(n));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to find the
# largest, good number in the
# divisors of given number N.

# function to return distinct
# prime factors
def PrimeFactors(n):

    # to store distinct
    # prime factors
    v = []

    x = n

    # run a loop upto sqrt(n)
    i = 2
    while(i * i <= n):
        if (x % i == 0) :

            # place this prime factor
            # in vector
            v.append(i)
            while (x % i == 0):
                x //= i

        i += 1

    # This condition is to handle
    # the case when n is a prime
    # number greater than 1
    if (x > 1):
        v.append(x)

    return v

# function that returns good number
def GoodNumber(n):

    # distinct prime factors
    v = PrimeFactors(n)

    # to store answer
    ans = 1

    # product of all distinct prime
    # factors is required answer
    for i in range(len(v)):
        ans *= v[i]

    return ans

# Driver code
if __name__ == "__main__":
    n = 12

    # function call
    print(GoodNumber(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the largest, good
// number in the divisors of given number N.
using System;
using System.Collections.Generic;
public class GFG {
    // function to return distinct prime factors

    static List<int> PrimeFactors(int n)
    {

        // to store distinct prime factors
        List<int> v = new List<int>();
        int x = n;

        // run a loop upto sqrt(n)
        for (int i = 2; i * i <= n; i++) {
            if (x % i == 0) {

                // place this prime factor in vector
                v.Add(i);
                while (x % i == 0)
                    x /= i;
            }
        }

        // This condition is to handle the case when n
        // is a prime number greater than 1
        if (x > 1)
            v.Add(x);

        return v;
    }

    // function that returns good number
    static int GoodNumber(int n)
    {
        // distinct prime factors
        List<int> v = new List<int>(PrimeFactors(n));

        // to store answer
        int ans = 1;

        // product of all distinct prime
        // factors is required answer
        for (int i = 0; i < v.Count; i++)
            ans *= v[i];

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 12;

        // function call
        Console.WriteLine(GoodNumber(n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the largest, good
// number in the divisors of given number N.

// function to return distinct prime factors
function PrimeFactors($n)
{
    // to store distinct prime factors
    $v = array();

    $x = $n;

    // run a loop upto sqrt(n)
    for ($i = 2; $i * $i <= $n; $i++)
    {
        if ($x % $i == 0)
        {

            // place this prime factor in vector
            array_push($v, $i);
            while ($x % $i == 0)
                $x /= $i;
        }
    }

    // This condition is to handle the case when n
    // is a prime number greater than 1
    if ($x > 1)
        array_push($v, $x);

    return $v;
}

// function that returns good number
function GoodNumber($n)
{
    // distinct prime factors
    $v = PrimeFactors($n);

    // to store answer
    $ans = 1;

    // product of all distinct prime
    // factors is required answer
    for ($i = 0; $i < count($v); $i++)
        $ans *= $v[$i];

    return $ans;
}

// Driver code
$n = 12;

// function call
echo GoodNumber($n);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
// Javascript program to find the largest, good
// number in the divisors of given number N.

    // function to return distinct prime factors
    function PrimeFactors(n)
    {
        // to store distinct prime factors
        let v = [];
        let x = n;

        // run a loop upto sqrt(n)
        for (let i = 2; i * i <= n; i++) {
            if (x % i == 0) {

                // place this prime factor in vector
                v.push(i);
                while (x % i == 0)
                    x = Math.floor(x/i);
            }
        }

        // This condition is to handle the case when n
        // is a prime number greater than 1
        if (x > 1)
            v.push(x);

        return v;
    }

    // function that returns good number
    function GoodNumber(n)
    {
        // distinct prime factors
        let v = PrimeFactors(n);

        // to store answer
        let ans = 1;

        // product of all distinct prime
        // factors is required answer
        for (let i = 0; i < v.length; i++)
            ans *= v[i];

        return ans;
    }

    // Driver code
    let n = 12;

    // function call
    document.write(GoodNumber(n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
6
```