# 范围[l，r]

内所有奇数因子之和

> 原文:[https://www . geeksforgeeks . org/所有范围内奇数因子之和-l-r/](https://www.geeksforgeeks.org/sum-of-all-odd-factors-of-numbers-in-the-range-l-r/)

给定一个范围**【l，r】**，任务是从给定的范围内找出所有奇数因子的和。
**例:**

> **输入:** l = 6，r = 8
> **输出:** 32
> 因子(6) = 1，2，3，6，奇数因子(6) = 1，3 sum_Odd_Factors(6) = 1 + 3 = 4
> 因子(7) = 1，7，oddfactors(6) = 1 7，sum_Odd_Factors(7) = 1 + 7 = 8
> 因子(8) = 1，2，4，8，oddfactors(6) = 1，sum

**方法:**我们可以修改【厄拉多塞的 T2】筛将一个数的所有奇数因子的和存储在其对应的索引处。然后我们将创建一个前缀数组来存储该索引的总和。现在每个查询都可以用前缀[r]–前缀[l–1]在 O(1)中回答。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

const int MAX = 100001;

ll prefix[MAX];

// Function to calculate the prefix sum
// of all the odd factors
void sieve_modified()
{
    for (int i = 1; i < MAX; i += 2) {

        // Add i to all the multiples of i
        for (int j = i; j < MAX; j += i)
            prefix[j] += i;
    }

    // Update the prefix sum
    for (int i = 1; i < MAX; i++)
        prefix[i] += prefix[i - 1];
}

// Function to return the sum of
// all the odd factors of the
// numbers in the given range
ll sumOddFactors(int L, int R)
{
    return (prefix[R] - prefix[L - 1]);
}

// Driver code
int main()
{
    sieve_modified();
    int l = 6, r = 10;
    cout << sumOddFactors(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int MAX = 100001;
static int prefix[] = new int[MAX];

// Function to calculate the prefix sum
// of all the odd factors
static void sieve_modified()
{
    for (int i = 1; i < MAX; i += 2)
    {

        // Add i to all the multiples of i
        for (int j = i; j < MAX; j += i)
            prefix[j] += i;
    }

    // Update the prefix sum
    for (int i = 1; i < MAX; i++)
        prefix[i] += prefix[i - 1];
}

// Function to return the sum of
// all the odd factors of the
// numbers in the given range
static int sumOddFactors(int L, int R)
{
    return (prefix[R] - prefix[L - 1]);
}

    // Driver code
    public static void main (String[] args)
    {
        sieve_modified();
        int l = 6, r = 10;
        System.out.println (sumOddFactors(l, r));
    }
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100001;

prefix = [0] * MAX;

# Function to calculate the prefix sum
# of all the odd factors
def sieve_modified():

    for i in range(1, MAX, 2):

        # Add i to all the multiples of i
        for j in range(i, MAX, i):
            prefix[j] += i;

    # Update the prefix sum
    for i in range(1, MAX):
        prefix[i] += prefix[i - 1];

# Function to return the sum of
# all the odd factors of the
# numbers in the given range
def sumOddFactors(L, R):

    return (prefix[R] - prefix[L - 1]);

# Driver code
sieve_modified();
l = 6;
r = 10;
print(sumOddFactors(l, r));

# this code is contributed by chandan_jnu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

public static int MAX = 100001;
public static int[] prefix = new int[MAX];

// Function to calculate the prefix sum
// of all the odd factors
public static void sieve_modified()
{
    for (int i = 1; i < MAX; i += 2)
    {

        // Add i to all the multiples of i
        for (int j = i; j < MAX; j += i)
        {
            prefix[j] += i;
        }
    }

    // Update the prefix sum
    for (int i = 1; i < MAX; i++)
    {
        prefix[i] += prefix[i - 1];
    }
}

// Function to return the sum of
// all the odd factors of the
// numbers in the given range
public static int sumOddFactors(int L, int R)
{
    return (prefix[R] - prefix[L - 1]);
}

// Driver code
public static void Main(string[] args)
{
    sieve_modified();
    int l = 6, r = 10;
    Console.WriteLine(sumOddFactors(l, r));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$MAX = 10001;

$prefix = array_fill(0, $MAX, 0);

// Function to calculate the prefix
// sum of all the odd factors
function sieve_modified()
{
    global $prefix, $MAX;
    for ($i = 1; $i < $MAX; $i += 2)
    {

        // Add i to all the multiples of i
        for ($j = $i; $j < $MAX; $j += $i)
            $prefix[$j] += $i;
    }

    // Update the prefix sum
    for ($i = 1; $i < $MAX; $i++)
        $prefix[$i] += $prefix[$i - 1];
}

// Function to return the sum of
// all the odd factors of the
// numbers in the given range
function sumOddFactors($L, $R)
{
    global $prefix;
    return ($prefix[$R] -
            $prefix[$L - 1]);
}

// Driver code
sieve_modified();
$l = 6;
$r = 10;
echo sumOddFactors($l, $r);

// This code is conyributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
var MAX = 100001;
prefix = Array(MAX).fill(0)

// Function to calculate the prefix sum
// of all the odd factors
function sieve_modified()
{
    for (var i = 1; i < MAX; i += 2) {

        // Add i to all the multiples of i
        for (var j = i; j < MAX; j += i)
            prefix[j] += i;
    }

    // Update the prefix sum
    for (var i = 1; i < MAX; i++)
        prefix[i] += prefix[i - 1];
}

// Function to return the sum of
// all the odd factors of the
// numbers in the given range
function sumOddFactors(L, R)
{
    return (prefix[R] - prefix[L - 1]);
}

// Driver code
sieve_modified();
var l = 6, r = 10;
document.write(sumOddFactors(l, r));

// This code is contributed by noob2000.

</script>
```

**Output:** 

```
32
```