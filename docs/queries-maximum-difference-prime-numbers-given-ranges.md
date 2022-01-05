# 查询给定范围内素数的最大差值

> 原文:[https://www . geesforgeks . org/query-最大差值-质数-给定范围/](https://www.geeksforgeeks.org/queries-maximum-difference-prime-numbers-given-ranges/)

给定表单范围**【左，右】**的 **n** 个查询。任务是为每个查询找到范围内两个素数之间的最大差值。如果范围内没有质数，则打印 0。所有范围都低于 100005。

**示例:**

```
Input : Q = 3
        query1 = [2, 5]
        query2 = [2, 2]
        query3 = [24, 28]
Output : 3
         0
         0
In first query, 2 and 5 are prime number 
in the range with maximum difference which 
is 3\. In second there 
is only 1 prime number in range, so output
is 0\. And in third query, there is no prime number in the given range so the output is 0.
```

这个想法是使用厄拉多塞的[筛以及一些预计算来计算素数。](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

下面是解决问题的步骤:
**步骤 1:** 使用厄拉多塞的筛算法找到素数。
**步骤 2:** 制作一个数组，比如说*前缀[]* ，其中前缀[i]表示小于或等于 I 的最大素数。
**步骤 3:** 制作一个数组，比如说*后缀[]* ，其中后缀[i]表示大于或等于 I 的最小素数。
**步骤 4:** 现在对于每个有[L，R]的查询，执行以下操作:

```
  if (prefix[R]  R)
    return 0;
  else
    return prefix[R] - suffix[L];
```

下面是该方法的实现:

## C++

```
// CPP program to find maximum differences between
// two prime numbers in given ranges
#include <bits/stdc++.h>
using namespace std;
#define MAX 100005

// Declare global variables to assign heap memory and avoid
// stack overflow
bool prime[MAX];
int prefix[MAX], suffix[MAX];

// Precompute Sieve, Prefix array, Suffix array
void precompute(int prefix[], int suffix[])
{
    memset(prime, true, sizeof(prime));

    // Sieve of Eratosthenes
    for (int i = 2; i * i < MAX; i++) {
        if (prime[i]) {
            for (int j = i * i; j < MAX; j += i)
                prime[j] = false;
        }
    }

    prefix[1] = 1;
    suffix[MAX - 1] = 1e9 + 7;

    // Precomputing Prefix array.
    for (int i = 2; i < MAX; i++) {
        if (prime[i])
            prefix[i] = i;
        else
            prefix[i] = prefix[i - 1];
    }

    // Precompute Suffix array.
    for (int i = MAX - 1; i > 1; i--) {
        if (prime[i])
            suffix[i] = i;
        else
            suffix[i] = suffix[i + 1];
    }
}

// Function to solve each query
int query(int prefix[], int suffix[], int L, int R)
{
    if (prefix[R] < L || suffix[L] > R)
        return 0;
    else
        return prefix[R] - suffix[L];
}

// Driven Program
int main()
{
    int q = 3;
    int L[] = { 2, 2, 24 };
    int R[] = { 5, 2, 28 };

    precompute(prefix, suffix);

    for (int i = 0; i < q; i++)
        cout << query(prefix, suffix, L[i], R[i]) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum differences between
// two prime numbers in given ranges

public class GFG {

    final static int MAX = 100005;

    // Precompute Sieve, Prefix array, Suffix array
    static void precompute(int prefix[], int suffix[])
    {
        boolean prime[] = new boolean[MAX];
        for (int i = 0; i < MAX; i++) {
            prime[i] = true;
        }

        // Sieve of Eratosthenes
        for (int i = 2; i * i < MAX; i++) {
            if (prime[i]) {
                for (int j = i * i; j < MAX; j += i) {
                    prime[j] = false;
                }
            }
        }

        prefix[1] = 1;
        suffix[MAX - 1] = (int)1e9 + 7;

        // Precomputing Prefix array.
        for (int i = 2; i < MAX; i++) {
            if (prime[i]) {
                prefix[i] = i;
            }
            else {
                prefix[i] = prefix[i - 1];
            }
        }

        // Precompute Suffix array.
        for (int i = MAX - 2; i > 1; i--) {
            if (prime[i]) {
                suffix[i] = i;
            }
            else {
                suffix[i] = suffix[i + 1];
            }
        }
    }

    // Function to solve each query
    static int query(int prefix[], int suffix[], int L,
                     int R)
    {
        if (prefix[R] < L || suffix[L] > R) {
            return 0;
        }
        else {
            return prefix[R] - suffix[L];
        }
    }

    // Driven Program
    public static void main(String[] args)
    {
        int q = 3;
        int L[] = { 2, 2, 24 };
        int R[] = { 5, 2, 28 };

        int prefix[] = new int[MAX], suffix[]
                                     = new int[MAX];
        precompute(prefix, suffix);

        for (int i = 0; i < q; i++) {
            System.out.println(
                query(prefix, suffix, L[i], R[i]));
        }
    }
}
/*This code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python 3 program to find maximum
# differences between two prime numbers
# in given ranges
from math import sqrt

MAX = 100005

# Precompute Sieve, Prefix array, Suffix array
def precompute(prefix, suffix):
    prime = [True for i in range(MAX)]

    # Sieve of Eratosthenes
    k = int(sqrt(MAX))
    for i in range(2, k, 1):
        if (prime[i]):
            for j in range(i * i, MAX, i):
                prime[j] = False

    prefix[1] = 1
    suffix[MAX - 1] = int(1e9 + 7)

    # Precomputing Prefix array.
    for i in range(2, MAX, 1):
        if (prime[i]):
            prefix[i] = i
        else:
            prefix[i] = prefix[i - 1]

    # Precompute Suffix array.
    i = MAX - 2
    while(i > 1):
        if (prime[i]):
            suffix[i] = i
        else:
            suffix[i] = suffix[i + 1]
        i -= 1

# Function to solve each query

def query(prefix, suffix, L, R):
    if (prefix[R] < L or suffix[L] > R):
        return 0
    else:
        return prefix[R] - suffix[L]

# Driver Code
if __name__ == '__main__':
    q = 3
    L = [2, 2, 24]
    R = [5, 2, 28]

    prefix = [0 for i in range(MAX)]
    suffix = [0 for i in range(MAX)]
    precompute(prefix, suffix)

    for i in range(0, q, 1):
        print(query(prefix, suffix,
                    L[i], R[i]))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find maximum differences between
// two prime numbers in given ranges
using System;

public class GFG {

    static readonly int MAX = 100005;

    // Precompute Sieve, Prefix array, Suffix array
    static void precompute(int[] prefix, int[] suffix)
    {
        bool[] prime = new bool[MAX];
        for (int i = 0; i < MAX; i++) {
            prime[i] = true;
        }

        // Sieve of Eratosthenes
        for (int i = 2; i * i < MAX; i++) {
            if (prime[i]) {
                for (int j = i * i; j < MAX; j += i) {
                    prime[j] = false;
                }
            }
        }

        prefix[1] = 1;
        suffix[MAX - 1] = (int)1e9 + 7;

        // Precomputing Prefix array.
        for (int i = 2; i < MAX; i++) {
            if (prime[i]) {
                prefix[i] = i;
            }
            else {
                prefix[i] = prefix[i - 1];
            }
        }

        // Precompute Suffix array.
        for (int i = MAX - 2; i > 1; i--) {
            if (prime[i]) {
                suffix[i] = i;
            }
            else {
                suffix[i] = suffix[i + 1];
            }
        }
    }

    // Function to solve each query
    static int query(int[] prefix, int[] suffix, int L,
                     int R)
    {
        if (prefix[R] < L || suffix[L] > R) {
            return 0;
        }
        else {
            return prefix[R] - suffix[L];
        }
    }

    // Driven Program
    public static void Main()
    {
        int q = 3;
        int[] L = { 2, 2, 24 };
        int[] R = { 5, 2, 28 };

        int[] prefix = new int[MAX];
        int[] suffix = new int[MAX];
        precompute(prefix, suffix);

        for (int i = 0; i < q; i++) {
            Console.WriteLine(
                query(prefix, suffix, L[i], R[i]));
        }
    }
}

/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum differences
// between two prime numbers in given ranges
$MAX = 100005;

// Precompute Sieve, Prefix array,
// Suffix array
function precompute(&$prefix, &$suffix)
{
    global $MAX;
    $prime = array_fill(0, $MAX, true);

    // Sieve of Eratosthenes
    for ($i = 2; $i * $i < $MAX; $i++)
    {
        if ($prime[$i])
        {
            for ($j = $i * $i;
                 $j < $MAX; $j += $i)
                $prime[$j] = false;
        }
    }

    $prefix[1] = 1;
    $suffix[$MAX - 1] = 1e9 + 7;

    // Precomputing Prefix array.
    for ($i = 2; $i < $MAX; $i++)
    {
        if ($prime[$i])
            $prefix[$i] = $i;
        else
            $prefix[$i] = $prefix[$i - 1];
    }

    // Precompute Suffix array.
    for ($i = $MAX - 1; $i > 1; $i--)
    {
        if ($prime[$i])
            $suffix[$i] = $i;
        else
            $suffix[$i] = $suffix[$i + 1];
    }
}

// Function to solve each query
function query($prefix, $suffix, $L, $R)
{
    if ($prefix[$R] < $L || $suffix[$L] > $R)
        return 0;
    else
        return $prefix[$R] - $suffix[$L];
}

// Driver Code
$q = 3;
$L = array( 2, 2, 24 );
$R = array( 5, 2, 28 );

$prefix = array_fill(0, $MAX + 1, 0);
$suffix = array_fill(0, $MAX + 1, 0);
precompute($prefix, $suffix);

for ($i = 0; $i < $q; $i++)
    echo query($prefix, $suffix,
               $L[$i], $R[$i]) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum
// differences between two prime
// numbers in given ranges

let MAX = 100005;

// Precompute Sieve, Prefix array, Suffix array
function precompute(prefix, suffix)
{
    let prime = [];
    for(let i = 0; i < MAX; i++)
    {
        prime[i] = true;
    }

    // Sieve of Eratosthenes
    for(let i = 2; i * i < MAX; i++)
    {
        if (prime[i])
        {
            for(let j = i * i; j < MAX; j += i)
            {
                prime[j] = false;
            }
        }
    }

    prefix[1] = 1;
    suffix[MAX - 1] = 1e9 + 7;

    // Precomputing Prefix array.
    for(let i = 2; i < MAX; i++)
    {
        if (prime[i])
        {
            prefix[i] = i;
        }
        else
        {
            prefix[i] = prefix[i - 1];
        }
    }

    // Precompute Suffix array.
    for(let i = MAX - 2; i > 1; i--)
    {
        if (prime[i])
        {
            suffix[i] = i;
        }
        else
        {
            suffix[i] = suffix[i + 1];
        }
    }
}

// Function to solve each query
function query(prefix, suffix, L, R)
{
    if (prefix[R] < L || suffix[L] > R)
    {
        return 0;
    }
    else
    {
        return prefix[R] - suffix[L];
    }
}

// Driver Code
let q = 3;
let L = [ 2, 2, 24 ];
let R = [ 5, 2, 28 ];
let prefix = [], suffix = [];

precompute(prefix, suffix);

for(let i = 0; i < q; i++)
{
    document.write(query(prefix, suffix,
                         L[i], R[i]) + "<br/>");
}

// This code is contributed by sanjoy_62

</script>
```

**输出:**

```
3
0
0 
```