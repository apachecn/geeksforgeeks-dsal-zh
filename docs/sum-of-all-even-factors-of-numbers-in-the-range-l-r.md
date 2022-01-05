# 范围[l，r]

内所有偶数因子之和

> 原文:[https://www . geeksforgeeks . org/范围内所有偶数因子之和-l-r/](https://www.geeksforgeeks.org/sum-of-all-even-factors-of-numbers-in-the-range-l-r/)

给定一个范围**【l，r】**，任务是从给定的范围内找出所有偶数因子的和。
**例:**

> **输入:** l = 6，r = 8
> **输出:** 22
> 因子(6) = 1，2，3，6，偶数因子(6) = 2，6 sumEvenFactors(6) = 2 + 6 = 8
> 因子(7) = 1，7，无偶数因子
> 因子(8) = 1，2，4，8，偶数因子(8) = 2，4，8 sumEvenFactors(8) = 2 + 4 + 8 = 14
> 因此

**方法:**我们可以修改【厄拉多塞的 T2】筛将一个数的所有偶数因子的和存储在其对应的索引处。然后我们将创建一个前缀数组来存储该索引的总和。现在每个查询都可以用前缀[r]–前缀[l–1]在 O(1)中回答。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

const int MAX = 100000;

ll prefix[MAX];

// Function to calculate the prefix sum
// of all the even factors
void sieve_modified()
{
    for (int i = 2; i < MAX; i += 2) {

        // Add i to all the multiples of i
        for (int j = i; j < MAX; j += i)
            prefix[j] += i;
    }

    // Update the prefix sum
    for (int i = 1; i < MAX; i++)
        prefix[i] += prefix[i - 1];
}

// Function to return the sum of
// all the even factors of the
// numbers in the given range
ll sumEvenFactors(int L, int R)
{
    return (prefix[R] - prefix[L - 1]);
}

// Driver code
int main()
{
    sieve_modified();
    int l = 6, r = 10;
    cout << sumEvenFactors(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static final int MAX = 100000;
    static long prefix[] = new long[MAX];

    // Function to calculate the prefix sum
    // of all the even factors
    static void sieve_modified()
    {
        for (int i = 2; i < MAX; i += 2) {

            // Add i to all the multiples of i
            for (int j = i; j < MAX; j += i)
                prefix[j] += i;
        }

        // Update the prefix sum
        for (int i = 1; i < MAX; i++)
            prefix[i] += prefix[i - 1];
    }

    // Function to return the sum of
    // all the even factors of the
    // numbers in the given range
    static long sumEvenFactors(int L, int R)
    {
        return (prefix[R] - prefix[L - 1]);
    }

    // Driver code
    public static void main(String args[])
    {
        sieve_modified();
        int l = 6, r = 10;
        System.out.print(sumEvenFactors(l, r));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach.

# Function to calculate the prefix sum
# of all the even factors
def sieve_modified():

    for i in range(2, MAX, 2):

        # Add i to all the multiples of i
        for j in range(i, MAX, i):
            prefix[j] += i

    # Update the prefix sum
    for i in range(1, MAX):
        prefix[i] += prefix[i - 1]

# Function to return the sum of
# all the even factors of the
# numbers in the given range
def sumEvenFactors(L, R):

    return (prefix[R] - prefix[L - 1])

# Driver code
if __name__ == "__main__":

    MAX = 100000
    prefix = [0] * MAX
    sieve_modified()
    l, r = 6, 10
    print(sumEvenFactors(l, r))

# This code is contributed by Rituraj Jain
```

## C#

```
using System;
// C# implementation of the approach
using System;

class GFG
{

    public const int MAX = 100000;
    public static long[] prefix = new long[MAX];

    // Function to calculate the prefix sum
    // of all the even factors
    public static void sieve_modified()
    {
        for (int i = 2; i < MAX; i += 2)
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
    // all the even factors of the
    // numbers in the given range
    public static long sumEvenFactors(int L, int R)
    {
        return (prefix[R] - prefix[L - 1]);
    }

    // Driver code
    public static void Main(string[] args)
    {
        sieve_modified();
        int l = 6, r = 10;
        Console.Write(sumEvenFactors(l, r));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 10000;

$prefix = array_fill(0, $MAX, 0);

// Function to calculate the prefix sum
// of all the even factors
function sieve_modified()
{
    global $MAX, $prefix;
    for ($i = 2; $i < $MAX; $i += 2)
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
// all the even factors of the
// numbers in the given range
function sumEvenFactors($L, $R)
{
    global $MAX, $prefix;
    return ($prefix[$R] - $prefix[$L - 1]);
}

// Driver code
sieve_modified();
$l = 6;
$r = 10;
echo sumEvenFactors($l, $r);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
var MAX = 100000;
prefix = Array(MAX).fill(0);

// Function to calculate the prefix sum
// of all the even factors
function sieve_modified()
{
    for (var i = 2; i < MAX; i += 2) {

        // Add i to all the multiples of i
        for (var j = i; j < MAX; j += i)
            prefix[j] += i;
    }

    // Update the prefix sum
    for (var i = 1; i < MAX; i++)
        prefix[i] += prefix[i - 1];
}

// Function to return the sum of
// all the even factors of the
// numbers in the given range
function sumEvenFactors(L, R)
{
    return (prefix[R] - prefix[L - 1]);
}

// Driver code
sieve_modified();
var l = 6, r = 10;
document.write(sumEvenFactors(l, r));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
34
```