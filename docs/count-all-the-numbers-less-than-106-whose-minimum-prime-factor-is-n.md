# 计算所有小于 10^6 的数，其最小质因数为 N

> 原文:[https://www . geesforgeks . org/count-all-the-numbers-小于-106-其最小质因数为-n/](https://www.geeksforgeeks.org/count-all-the-numbers-less-than-106-whose-minimum-prime-factor-is-n/)

给定一个素数 N。任务是找出所有小于或等于 10^6 的最小质因数为 n 的数。
**例:**

```
Input: N = 2
Output: 500000

Input: N = 3
Output: 166667
```

**方法:**用厄拉多塞的筛子寻找问题的解决方案。存储所有小于 10^6 的质数。形成另一个筛子，它将存储其最小质因数是筛子索引的所有数字的计数。然后显示素数 N 的计数(即 screen _ count[N]+1)，其中 N 是素数。
以下是上述办法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000

// the sieve of prime number and
// count of minimum prime factor
int sieve_Prime[MAX + 4] = { 0 },
                      sieve_count[MAX + 4] = { 0 };

// form the prime sieve
void form_sieve()
{
    // 1 is not a prime number
    sieve_Prime[1] = 1;

    // form the sieve
    for (int i = 2; i <= MAX; i++) {

        // if i is prime
        if (sieve_Prime[i] == 0) {
            for (int j = i * 2; j <= MAX; j += i) {

                // if i is the least prime factor
                if (sieve_Prime[j] == 0) {

                    // mark the number j as non prime
                    sieve_Prime[j] = 1;

                    // count the numbers whose least prime factor is i
                    sieve_count[i]++;
                }
            }
        }
    }
}

// Driver code
int main()
{
    // form the sieve
    form_sieve();

    int n = 2;

    // display
    cout << "Count = " << (sieve_count[n] + 1) << endl;

    n = 3;

    // display
    cout << "Count = " << (sieve_count[n] + 1) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG {

static int MAX = 1000000;

// the sieve of prime number and
// count of minimum prime factor
static int sieve_Prime[] = new int[MAX + 4];
static int sieve_count[] =  new int[MAX + 4];

// form the prime sieve
static void form_sieve()
{
    // 1 is not a prime number
    sieve_Prime[1] = 1;

    // form the sieve
    for (int i = 2; i <= MAX; i++) {

        // if i is prime
        if (sieve_Prime[i] == 0) {
            for (int j = i * 2; j <= MAX; j += i) {

                // if i is the least prime factor
                if (sieve_Prime[j] == 0) {

                    // mark the number j as non prime
                    sieve_Prime[j] = 1;

                    // count the numbers whose least prime factor is i
                    sieve_count[i]++;
                }
            }
        }
    }
}

// Driver code

    public static void main (String[] args) {
        // form the sieve
    form_sieve();

    int n = 2;

    // display
    System.out.println( "Count = " + (sieve_count[n] + 1));

    n = 3;

    // display
    System.out.println ("Count = "  +(sieve_count[n] + 1));
    }
}
// This code was contributed
// by inder_mca
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

MAX = 1000000

# the sieve of prime number and
# count of minimum prime factor
sieve_Prime = [0 for i in range(MAX + 4)]
sieve_count = [0 for i in range(MAX + 4)]

# form the prime sieve
def form_sieve():

    # 1 is not a prime number
    sieve_Prime[1] = 1

    # form the sieve
    for i in range(2, MAX + 1):

        # if i is prime
        if sieve_Prime[i] == 0:
            for j in range(i * 2, MAX + 1, i):

                # if i is the least prime factor
                if sieve_Prime[j] == 0:

                    # mark the number j
                    # as non prime
                    sieve_Prime[j] = 1

                    # count the numbers whose
                    # least prime factor is i
                    sieve_count[i] += 1

# Driver code

# form the sieve
form_sieve()

n = 2

# display
print("Count =", sieve_count[n] + 1)

n = 3

# display
print("Count =", sieve_count[n] + 1)

# This code was contributed
# by VishalBachchas
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

static int MAX = 1000000;

// the sieve of prime number and
// count of minimum prime factor
static int []sieve_Prime = new int[MAX + 4];
static int []sieve_count = new int[MAX + 4];

// form the prime sieve
static void form_sieve()
{
    // 1 is not a prime number
    sieve_Prime[1] = 1;

    // form the sieve
    for (int i = 2; i <= MAX; i++) {

        // if i is prime
        if (sieve_Prime[i] == 0) {
            for (int j = i * 2; j <= MAX; j += i) {

                // if i is the least prime factor
                if (sieve_Prime[j] == 0) {

                    // mark the number j as non prime
                    sieve_Prime[j] = 1;

                    // count the numbers whose least prime factor is i
                    sieve_count[i]++;
                }
            }
        }
    }
}

// Driver code

    public static void Main () {
        // form the sieve
    form_sieve();

    int n = 2;

    // display
    Console.WriteLine( "Count = " + (sieve_count[n] + 1));

    n = 3;

    // display
    Console.WriteLine ("Count = " +(sieve_count[n] + 1));
    }
}
// This code was contributed
// by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
$MAX = 1000000;

// the sieve of prime number and
// count of minimum prime factor
$sieve_Prime = array_fill(0, $MAX + 4, NULL);
$sieve_count = array_fill(0, $MAX + 4, NULL);

// form the prime sieve
function form_sieve()
{
    global $sieve_Prime, $sieve_count, $MAX;

    // 1 is not a prime number
    $sieve_Prime[1] = 1;

    // form the sieve
    for ($i = 2; $i <= $MAX; $i++)
    {

        // if i is prime
        if ($sieve_Prime[$i] == 0)
        {
            for ($j = $i * 2; $j <= $MAX; $j += $i)
            {

                // if i is the least prime factor
                if ($sieve_Prime[$j] == 0)
                {

                    // mark the number j as non prime
                    $sieve_Prime[$j] = 1;

                    // count the numbers whose least
                    // prime factor is i
                    $sieve_count[$i]++;
                }
            }
        }
    }
}

// Driver code

// form the sieve
form_sieve();

$n = 2;

// display
echo "Count = " . ($sieve_count[$n] + 1) . "\n";

$n = 3;

// display
echo "Count = " . ($sieve_count[$n] + 1) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

var MAX = 1000000;

// the sieve of prime number and
// count of minimum prime factor
var sieve_Prime = Array.from({length: MAX + 4},
(_, i) => 0);
var sieve_count =  Array.from({length: MAX + 4},
(_, i) => 0);

// form the prime sieve
function form_sieve()
{
    // 1 is not a prime number
    sieve_Prime[1] = 1;

    // form the sieve
    for (i = 2; i <= MAX; i++) {

        // if i is prime
        if (sieve_Prime[i] == 0) {
            for (j = i * 2; j <= MAX; j += i) {

                // if i is the least prime factor
                if (sieve_Prime[j] == 0) {

                    // mark the number j as non prime
                    sieve_Prime[j] = 1;

                    // count the numbers whose least
                    // prime factor is i
                    sieve_count[i]++;
                }
            }
        }
    }
}

// Driver code

// form the sieve
form_sieve();

var n = 2;

// display
document.write( "Count = " + (sieve_count[n] + 1));

n = 3;

// display
document.write("<br>Count = "  +(sieve_count[n] + 1));

// This code contributed by shikhasingrajput

</script>
```

**Output**

```
Count = 500000
Count = 166667
```

**时间复杂度:** O(N*log(log(N))，其中 N=10 <sup>6</sup> 。

**辅助空间:** O(10 <sup>6</sup>