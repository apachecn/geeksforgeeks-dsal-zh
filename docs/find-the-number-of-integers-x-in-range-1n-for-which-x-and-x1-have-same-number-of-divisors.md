# 求 x 和 x+1 具有相同除数的(1，N)范围内的整数 x 的个数

> 原文:[https://www . geeksforgeeks . org/find-整数数-x-in-range-1n-for-x-和-x1-具有相同的除数/](https://www.geeksforgeeks.org/find-the-number-of-integers-x-in-range-1n-for-which-x-and-x1-have-same-number-of-divisors/)

给定一个整数 **N** 。任务是求整数 **1 < x < N** 的个数，其中 **x** 和 **x + 1** 的正整数除数相同。

**示例:**

> **输入:** N = 3
> **输出:** 1
> 除数(1) = 1
> 除数(2) = 1 和 2
> 除数(3) = 1 和 3
> 仅有效 x 为 2。
> 
> **输入:**N = 15
> T3】输出: 2

**逼近:**求 **N** 以下所有数字的[除数](https://www.geeksforgeeks.org/total-number-divisors-given-number/)并存储成数组。并对整数 **x** 的个数进行计数，使得 **x** 和 **x + 1** 通过运行一个循环具有相同的正整数除数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// To store number of divisors and
// Prefix sum of such numbers
int d[N], pre[N];

// Function to find the number of integers
// 1 < x < N for which x and x + 1 have
// the same number of positive divisors
void Positive_Divisors()
{
    // Count the number of divisors
    for (int i = 1; i < N; i++) {

        // Run a loop upto sqrt(i)
        for (int j = 1; j * j <= i; j++) {

            // If j is divisor of i
            if (i % j == 0) {

                // If it is perfect square
                if (j * j == i)
                    d[i]++;
                else
                    d[i] += 2;
            }
        }
    }

    int ans = 0;

    // x and x+1 have same number of
    // positive divisors
    for (int i = 2; i < N; i++) {
        if (d[i] == d[i - 1])
            ans++;
        pre[i] = ans;
    }
}

// Driver code
int main()
{
    // Function call
    Positive_Divisors();

    int n = 15;

    // Required answer
    cout << pre[n] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int N =100005;

// To store number of divisors and
// Prefix sum of such numbers
static int d[] = new int[N], pre[] = new int[N];

// Function to find the number of integers
// 1 < x < N for which x and x + 1 have
// the same number of positive divisors
static void Positive_Divisors()
{
    // Count the number of divisors
    for (int i = 1; i < N; i++)
    {

        // Run a loop upto sqrt(i)
        for (int j = 1; j * j <= i; j++)
        {

            // If j is divisor of i
            if (i % j == 0)
            {

                // If it is perfect square
                if (j * j == i)
                    d[i]++;
                else
                    d[i] += 2;
            }
        }
    }

    int ans = 0;

    // x and x+1 have same number of
    // positive divisors
    for (int i = 2; i < N; i++)
    {
        if (d[i] == d[i - 1])
            ans++;
        pre[i] = ans;
    }
}

// Driver code
public static void main(String[] args)
{
    // Function call
    Positive_Divisors();

    int n = 15;

    // Required answer
    System.out.println(pre[n]);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import sqrt;

N = 100005

# To store number of divisors and
# Prefix sum of such numbers
d = [0] * N
pre = [0] * N

# Function to find the number of integers
# 1 < x < N for which x and x + 1 have
# the same number of positive divisors
def Positive_Divisors() :

    # Count the number of divisors
    for i in range(N) :

        # Run a loop upto sqrt(i)
        for j in range(1, int(sqrt(i)) + 1) :

            # If j is divisor of i
            if (i % j == 0) :

                # If it is perfect square
                if (j * j == i) :
                    d[i] += 1
                else :
                    d[i] += 2

    ans = 0

    # x and x+1 have same number of
    # positive divisors
    for i in range(2, N) :
        if (d[i] == d[i - 1]) :
            ans += 1
        pre[i] = ans

# Driver code
if __name__ == "__main__" :

    # Function call
    Positive_Divisors()

    n = 15

    # Required answer
    print(pre[n])

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N =100005;

// To store number of divisors and
// Prefix sum of such numbers
static int []d = new int[N];
static int []pre = new int[N];

// Function to find the number of integers
// 1 < x < N for which x and x + 1 have
// the same number of positive divisors
static void Positive_Divisors()
{
    // Count the number of divisors
    for (int i = 1; i < N; i++)
    {

        // Run a loop upto sqrt(i)
        for (int j = 1; j * j <= i; j++)
        {

            // If j is divisor of i
            if (i % j == 0)
            {

                // If it is perfect square
                if (j * j == i)
                    d[i]++;
                else
                    d[i] += 2;
            }
        }
    }

    int ans = 0;

    // x and x+1 have same number of
    // positive divisors
    for (int i = 2; i < N; i++)
    {
        if (d[i] == d[i - 1])
            ans++;
        pre[i] = ans;
    }
}

// Driver code
public static void Main(String[] args)
{
    // Function call
    Positive_Divisors();

    int n = 15;

    // Required answer
    Console.WriteLine(pre[n]);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

$N = 100005;

// To store number of divisors and
// Prefix sum of such numbers
$d = array_fill(0,$N,NULL);
$pre = array_fill(0,$N,NULL);

// Function to find the number of integers
// 1 < x < N for which x and x + 1 have
// the same number of positive divisors
function Positive_Divisors()
{
    global $N,$d,$pre;
    // Count the number of divisors
    for ($i = 1; $i < $N; $i++) {

        // Run a loop upto sqrt(i)
        for ($j = 1; $j * $j <= $i; $j++) {

            // If j is divisor of i
            if ($i % $j == 0) {

                // If it is perfect square
                if ($j * $j == $i)
                    $d[$i]++;
                else
                    $d[$i] += 2;
            }
        }
    }

    $ans = 0;

    // x and x+1 have same number of
    // positive divisors
    for ($i = 2; $i < $N; $i++) {
        if ($d[$i] == $d[$i - 1])
            $ans++;
        $pre[$i] = $ans;
    }
}

// Driver code

    // Function call
    Positive_Divisors();

    $n = 15;

    // Required answer
    echo $pre[$n] ;

    return 0;

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
const N = 100005;

// To store number of divisors and
// Prefix sum of such numbers
let d = new Array(N).fill(0);
let pre = new Array(N).fill(0);

// Function to find the number of integers
// 1 < x < N for which x and x + 1 have
// the same number of positive divisors
function Positive_Divisors()
{

    // Count the number of divisors
    for(let i = 1; i < N; i++)
    {

        // Run a loop upto sqrt(i)
        for(let j = 1; j * j <= i; j++)
        {

            // If j is divisor of i
            if (i % j == 0)
            {

                // If it is perfect square
                if (j * j == i)
                    d[i]++;
                else
                    d[i] += 2;
            }
        }
    }

    let ans = 0;

    // x and x+1 have same number of
    // positive divisors
    for(let i = 2; i < N; i++)
    {
        if (d[i] == d[i - 1])
            ans++;

        pre[i] = ans;
    }
}

// Driver code

// Function call
Positive_Divisors();
let n = 15;

// Required answer
document.write(pre[n]);

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
2
```