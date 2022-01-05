# 求所有友好数字的和，直到 N

> 原文:[https://www . geesforgeks . org/find-the-sum-of-all-友好数字-up-n/](https://www.geeksforgeeks.org/find-the-sum-of-the-all-amicable-numbers-up-to-n/)

给定一个数 n，求 n 以下所有友好数的和。如果 A 和 B 是[友好对](https://www.geeksforgeeks.org/pairs-amicable-numbers/)(如果第一个数等于第二个数的除数之和，则两个数是友好的)，那么 A 和 B 称为友好数。
**例:**

> **输入:** 284
> **输出:** 504
> **解释:** 220 和 284 是到 284
> **的两个友好号码输入:** 250
> **输出:** 220
> **解释:** 220 是唯一的友好号码

**方法** :
一种有效的方法是将所有友好的数字存储在一个集合中，对于给定的 N，集合中所有小于或等于 N 的数字相加。
下面的代码是上述方法的实现:

## C++

```
// CPP program to find sum of all
// amicable numbers up to n
#include <bits/stdc++.h>
using namespace std;

#define N 100005

// Function to return all amicable numbers
set<int> AMICABLE()
{
    int sum[N];
    memset(sum, 0, sizeof sum);
    for (int i = 1; i < N; i++) {

        // include 1
        sum[i]++;

        for (int j = 2; j * j <= i; j++) {

            // j is proper divisor of i
            if (i % j == 0) {
                sum[i] += j;

                // if i is not a perfect square
                if (i / j != j)
                    sum[i] += i / j;
            }
        }
    }

    set<int> s;
    for (int i = 2; i < N; i++) {

        // insert amicable numbers
        if (i != sum[i] and sum[i] < N and i == sum[sum[i]]
            and !s.count(i) and !s.count(sum[i])) {
            s.insert(i);
            s.insert(sum[i]);
        }
    }

    return s;
}

// function to find sum of all
// amicable numbers up to N
int SumOfAmicable(int n)
{
    // to store required sum
    int sum = 0;

    // to store all amicable numbers
    set<int> s = AMICABLE();

    // sum all amicable numbers upto N
    for (auto i = s.begin(); i != s.end(); ++i) {
        if (*i <= n)
            sum += *i;
        else
            break;
    }

    // required answer
    return sum;
}

// Driver code to test above functions
int main()
{
    int n = 284;

    cout << SumOfAmicable(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all
// amicable numbers up to n
import java.util.*;
class GFG
{

static final int N=100005;

// Function to return all amicable numbers
static Set<Integer> AMICABLE()
{
    int sum[] = new int[N];
    for(int i = 0; i < N; i++)
        sum[i]=0;

    for (int i = 1; i < N; i++) 
    {

        // include 1
        sum[i]++;

        for (int j = 2; j * j <= i; j++)
        {

            // j is proper divisor of i
            if (i % j == 0)
            {
                sum[i] += j;

                // if i is not a perfect square
                if (i / j != j)
                    sum[i] += i / j;
            }
        }
    }

    Set<Integer> s = new HashSet<Integer>();
    for (int i = 2; i < N; i++)
    {

        // insert amicable numbers
        if (i != sum[i] && sum[i] < N && i == sum[sum[i]])
        {
            s.add(i);
            s.add(sum[i]);
        }
    }
    return s;
}

// function to find sum of all
// amicable numbers up to N
static int SumOfAmicable(int n)
{
    // to store required sum
    int sum = 0;

    // to store all amicable numbers
    Set<Integer> s = AMICABLE();

    // sum all amicable numbers upto N
    for (Integer x : s)
    {
        if (x <= n)
            sum += x;
    }

    // required answer
    return sum;
}

// Driver code
public static void main(String args[])
{
    int n = 284;
    System.out.println( SumOfAmicable(n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to findSum of all
# amicable numbers up to n
import math as mt

N = 100005

# Function to return all amicable numbers
def AMICABLE():

    Sum = [0 for i in range(N)]

    for i in range(1, N):
        Sum[i] += 1

        for j in range(2, mt.ceil(mt.sqrt(i))):

            # j is proper divisor of i
            if (i % j == 0):
                Sum[i] += j

                # if i is not a perfect square
                if (i // j != j):
                    Sum[i] += i // j

    s = set()
    for i in range(2, N):
        if(i != Sum[i] and Sum[i] < N and
           i == Sum[Sum[i]] and i not in s and
                Sum[i] not in s):
            s.add(i)
            s.add(Sum[i])

    return s

# function to findSum of all amicable
# numbers up to N
def SumOfAmicable(n):

    # to store requiredSum
    Sum = 0

    # to store all amicable numbers
    s = AMICABLE()

    #Sum all amicable numbers upto N
    s = sorted(s)
    for i in s:
        if (i <= n):
            Sum += i
        else:
            break

    # required answer
    return Sum

# Driver Code
n = 284
print(SumOfAmicable(n))

# This code is contributed by
# mohit kumar 29
```

## C#

```
// C# program to find sum of all
// amicable numbers up to n
using System;
using System.Collections.Generic;

class GFG
{

static readonly int N = 100005;

// Function to return all amicable numbers
static HashSet<int> AMICABLE()
{
    int []sum = new int[N];
    for(int i = 0; i < N; i++)
        sum[i] = 0;

    for (int i = 1; i < N; i++)
    {

        // include 1
        sum[i]++;

        for (int j = 2; j * j <= i; j++)
        {

            // j is proper divisor of i
            if (i % j == 0)
            {
                sum[i] += j;

                // if i is not a perfect square
                if (i / j != j)
                    sum[i] += i / j;
            }
        }
    }

    HashSet<int> s = new HashSet<int>();
    for (int i = 2; i < N; i++)
    {

        // insert amicable numbers
        if (i != sum[i] && sum[i] < N &&
                            i == sum[sum[i]])
        {
            s.Add(i);
            s.Add(sum[i]);
        }
    }
    return s;
}

// function to find sum of all
// amicable numbers up to N
static int SumOfAmicable(int n)
{
    // to store required sum
    int sum = 0;

    // to store all amicable numbers
    HashSet<int> s = AMICABLE();

    // sum all amicable numbers upto N
    foreach (int x in s)
    {
        if (x <= n)
            sum += x;
    }

    // required answer
    return sum;
}

// Driver code
public static void Main()
{
    int n = 284;
    Console.WriteLine( SumOfAmicable(n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of all
// amicable numbers up to n
$N = 10005;

// Function to return all amicable
// numbers
function AMICABLE()
{
    global $N;
    $sum = array_fill(0, $N, 0);
    for ($i = 1; $i < $N; $i++)
    {

        // include 1
        $sum[$i]++;

        for ($j = 2; $j * $j <= $i; $j++)
        {

            // j is proper divisor of i
            if ($i % $j == 0)
            {
                $sum[$i] += $j;

                // if i is not a perfect square
                if ($i / $j != $j)
                    $sum[$i] += $i / $j;
            }
        }
    }

    $s = array();
    for ($i = 2; $i < $N; $i++)
    {

        // insert amicable numbers
        if ($i != $sum[$i] and $sum[$i] < $N and
                        $i == $sum[$sum[$i]] and
                           !in_array($i, $s) and
                           !in_array($sum[$i], $s))
        {
            array_push($s, $i);
            array_push($s, $sum[$i]);
        }
    }

    return $s;
}

// function to find sum of all
// amicable numbers up to N
function SumOfAmicable($n)
{
    // to store required sum
    $sum = 0;

    // to store all amicable numbers
    $s = AMICABLE();
    $s = array_unique($s);
    sort($s);

    // sum all amicable numbers upto N
    for ($i = 0; $i != count($s); ++$i)
    {
        if ($s[$i] <= $n)
            $sum += $s[$i];
        else
            break;
    }

    // required answer
    return $sum;
}

// Driver code
$n = 284;

echo SumOfAmicable($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all
// amicable numbers up to n

let N=100005;

// Function to return all amicable numbers
function  AMICABLE()
{
    let sum = new Array(N);
    for(let i = 0; i < N; i++)
        sum[i]=0;

    for (let i = 1; i < N; i++) 
    {

        // include 1
        sum[i]++;

        for (let j = 2; j * j <= i; j++)
        {

            // j is proper divisor of i
            if (i % j == 0)
            {
                sum[i] += j;

                // if i is not a perfect square
                if (i / j != j)
                    sum[i] += i / j;
            }
        }
    }

    let s = new Set();
    for (let i = 2; i < N; i++)
    {

        // insert amicable numbers
        if (i != sum[i] && sum[i] < N && i == sum[sum[i]])
        {
            s.add(i);
            s.add(sum[i]);
        }
    }
    return s;
}

// function to find sum of all
// amicable numbers up to N
function SumOfAmicable(n)
{
    // to store required sum
    let sum = 0;

    // to store all amicable numbers
    let s = AMICABLE();

    // sum all amicable numbers upto N
    for (let x of s.values())
    {
        if (x <= n)
            sum += x;
    }

    // required answer
    return sum;
}

// Driver code
let n = 284;
document.write( SumOfAmicable(n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
504
```