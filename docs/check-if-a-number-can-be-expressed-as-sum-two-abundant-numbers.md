# 检查一个数是否可以表示为两个大数之和

> 原文:[https://www . geesforgeks . org/check-if-a-number-can-express-sum-two-fully-numbers/](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-sum-two-abundant-numbers/)

给定一个数 N，任务是将 N 表示为两个[大数](https://www.geeksforgeeks.org/abundant-number/)的和。如果不可能，请打印-1。

**示例:**

```
Input : N = 24 
Output : 12, 12

Input : N = 5
Output : -1 
```

**方法**:一种有效的方法是将所有丰富的数字存储在一个集合中。对于给定的数字，N 从 1 到 N 循环，检查 I 和 n-i 是否是大数。
以下是上述办法的实施情况:

## C++

```
// CPP program to check if number n is expressed
// as sum of two abundant numbers
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// Function to return all abundant numbers
// This function will be helpful for
// multiple queries
set<int> ABUNDANT()
{
    // To store abundant numbers
    set<int> v;

    for (int i = 1; i < N; i++) {

        // to store sum of the divisors
        // include 1 in the sum
        int sum = 1;
        for (int j = 2; j * j <= i; j++) {

            // if j is proper divisor
            if (i % j == 0) {
                sum += j;

                // if i is not a perfect square
                if (i / j != j)
                    sum += i / j;
            }
        }

        // if sum is greater than i then i is
        // a abundant number
        if (sum > i)
            v.insert(i);
    }

    return v;
}

// Check if number n is expressed
// as sum of two abundant numbers
void SumOfAbundant(int n)
{
    set<int> v = ABUNDANT();

    for (int i = 1; i <= n; i++) {

        // if both i and n-i are
        // abundant numbers
        if (v.count(i) and v.count(n - i)) {
            cout << i << " " << n - i;
            return;
        }
    }

    // can not be expressed
    cout << -1;
}

// Driver code
int main()
{
    int n = 24;
    SumOfAbundant(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if number n is expressed
// as sum of two abundant numbers
import java.util.*;
class GFG {

    static final int N = 100005;

// Function to return all abundant numbers
// This function will be helpful for
// multiple queries
    static Set<Integer> ABUNDANT() {
        // To store abundant numbers
        Set<Integer> v = new HashSet<>();

        for (int i = 1; i < N; i++) {

            // to store sum of the divisors
            // include 1 in the sum
            int sum = 1;
            for (int j = 2; j * j <= i; j++) {

                // if j is proper divisor
                if (i % j == 0) {
                    sum += j;

                    // if i is not a perfect square
                    if (i / j != j) {
                        sum += i / j;
                    }
                }
            }

            // if sum is greater than i then i is
            // a abundant number
            if (sum > i) {
                v.add(i);
            }
        }

        return v;
    }

// Check if number n is expressed
// as sum of two abundant numbers
    static void SumOfAbundant(int n) {
        Set<Integer> v = ABUNDANT();

        for (int i = 1; i <= n; i++) {

            // if both i and n-i are
            // abundant numbers
            if (v.contains(i) & v.contains(n - i)) {
                System.out.print(i + " " + (n - i));
                return;
            }
        }

        // can not be expressed
        System.out.print(-1);
    }

// Driver code
    public static void main(String[] args) {
        int n = 24;
        SumOfAbundant(n);
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to check if number n is
# expressed as sum of two abundant numbers

# from math lib import sqrt function
from math import sqrt

N = 100005

# Function to return all abundant numbers
# This function will be helpful for
# multiple queries
def ABUNDANT() :

    # To store abundant numbers
    v = set() ;

    for i in range(1, N) :

        # to store sum of the divisors
        # include 1 in the sum
        sum = 1
        for j in range(2, int(sqrt(i)) + 1) :

            # if j is proper divisor
            if (i % j == 0) :
                sum += j

            # if i is not a perfect square
            if (i / j != j) :
                sum += i // j

        # if sum is greater than i then i
        # is a abundant numbe
        if (sum > i) :
            v.add(i)

    return v

# Check if number n is expressed
# as sum of two abundant numbers
def SumOfAbundant(n) :
    v = ABUNDANT()

    for i in range(1, n + 1) :

        # if both i and n-i are abundant numbers
        if (list(v).count(i) and
            list(v).count(n - i)) :
            print(i, " ", n - i)
            return

    # can not be expressed
    print(-1)

# Driver code
if __name__ == "__main__" :
    n = 24
    SumOfAbundant(n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to check if number n is expressed
// as sum of two abundant numbers
using System;
using System.Collections.Generic;

class GFG {

    static readonly int N = 100005;

    // Function to return all abundant numbers
    // This function will be helpful for
    // multiple queries
    static HashSet<int> ABUNDANT()
    {
        // To store abundant numbers
        HashSet<int> v = new HashSet<int>();

        for (int i = 1; i < N; i++)
        {

            // to store sum of the divisors
            // include 1 in the sum
            int sum = 1;
            for (int j = 2; j * j <= i; j++)
            {

                // if j is proper divisor
                if (i % j == 0)
                {
                    sum += j;

                    // if i is not a perfect square
                    if (i / j != j)
                    {
                        sum += i / j;
                    }
                }
            }

            // if sum is greater than i then i is
            // a abundant number
            if (sum > i)
            {
                v.Add(i);
            }
        }
        return v;
    }

    // Check if number n is expressed
    // as sum of two abundant numbers
    static void SumOfAbundant(int n)
    {
        HashSet<int> v = ABUNDANT();

        for (int i = 1; i <= n; i++)
        {

            // if both i and n-i are
            // abundant numbers
            if (v.Contains(i) & v.Contains(n - i))
            {
                Console.Write(i + " " + (n - i));
                return;
            }
        }

        // can not be expressed
        Console.Write(-1);
    }

    // Driver code
    public static void Main()
    {
        int n = 24;
        SumOfAbundant(n);
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if number n is
// expressed as sum of two abundant numbers

// Function to return all abundant numbers
// This function will be helpful for
// multiple queries
function ABUNDANT()
{
    $N = 100005;

    // To store abundant numbers
    $v = array();

    for ($i = 1; $i < $N; $i++)
    {

        // to store sum of the divisors
        // include 1 in the sum
        $sum = 1;
        for ($j = 2; $j * $j <= $i; $j++)
        {

            // if j is proper divisor
            if ($i % $j == 0)
            {
                $sum += $j;

                // if i is not a perfect square
                if ($i / $j != $j)
                    $sum += $i / $j;
            }
        }

        // if sum is greater than i then
        // i is a abundant number
        if ($sum > $i)
            array_push($v, $i);
    }
    $v = array_unique($v);
    return $v;
}

// Check if number n is expressed
// as sum of two abundant numbers
function SumOfAbundant($n)
{
    $v = ABUNDANT();

    for ($i = 1; $i <= $n; $i++)
    {

        // if both i and n-i are
        // abundant numbers
        if (in_array($i, $v) &&
            in_array($n - $i, $v))
        {
            echo $i, " ", $n - $i;
            return;
        }
    }

    // can not be expressed
    echo -1;
}

// Driver code
$n = 24;
SumOfAbundant($n);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>

// javascript program to check if number n is expressed
// as sum of two abundant numbers

var N = 100005;

// Function to return all abundant numbers
// This function will be helpful for
// multiple queries
function ABUNDANT()
{
    // To store abundant numbers
    var v = new Set();

    var i,j;
    for (i = 1; i < N; i++) {

        // to store sum of the divisors
        // include 1 in the sum
        var sum = 1;
        for (j = 2; j * j <= i; j++) {

            // if j is proper divisor
            if (i % j == 0) {
                sum += j;

                // if i is not a perfect square
                if (parseInt(i / j) != j)
                    sum += parseInt(i / j);
            }
        }

        // if sum is greater than i then i is
        // a abundant number
        if (sum > i)
            v.add(i);
    }

    return v;
}

// Check if number n is expressed
// as sum of two abundant numbers
function SumOfAbundant(n)
{  
    var v = new Set();
    v = ABUNDANT();
    var i;
    for (i = 1; i <= n; i++) {

        // if both i and n-i are
        // abundant numbers
        if (v.has(i) && v.has(n - i)) {
            document.write(i+ ' ' + (n-i))
            return;
        }
    }

    // can not be expressed
    document.write(-1);
}

// Driver code
    var n = 24;
    SumOfAbundant(n);

</script>
```

**Output:** 

```
12 12
```