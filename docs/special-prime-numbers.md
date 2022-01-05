# 特殊质数

> 原文:[https://www.geeksforgeeks.org/special-prime-numbers/](https://www.geeksforgeeks.org/special-prime-numbers/)

给定两个数 n 和 k，从 2 到 n(含 2 到 n)查找是否至少存在 k 个**特殊**素数。
一个素数如果可以表示为三个整数之和:两个相邻的素数和 1，则称其为**特殊的**素数。例如，19 = 7 + 11 + 1，或者 13 = 5 + 7 + 1。
**注:-** 两个素数之间没有其他素数的称为邻素数。
**举例:**

```
Input : n = 27, k = 2
Output : YES
In this sample the answer is YES 
since at least two numbers are 
Special 13(5 + 7 + 1) and
19(7 + 11 + 1).

Input : n = 45, k = 7
Output : NO
In this example, the Special 
prime numbers are 13(5 + 7 + 1), 
19(7 + 11 + 1), 31(13 + 17 + 1),
37(17 + 19 + 1), 43(19 + 23 + 1).
As the no. of Special prime 
numbers from 2 to 45 is less than
k, the output is NO.
```

要解决这个问题，我们需要找到范围[2]内的素数..n]。所以我们用厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)来产生从 2 到 n 的所有素数。然后，取每对相邻的素数，检查它们的和加 1 是否也是素数。计算这些对的数量，将其与 K 进行比较，并输出结果。
以下是上述方法的实施:-

## C++

```
// CPP program to check whether there
// exist at least k or not in range [2..n]
#include <bits/stdc++.h>
using namespace std;

vector<int> primes;

// Generating all the prime numbers
// from 2 to n.
void SieveofEratosthenes(int n)
{
    bool visited[n];
    for (int i = 2; i <= n + 1; i++)
        if (!visited[i]) {
            for (int j = i * i; j <= n + 1; j += i)
                visited[j] = true;
            primes.push_back(i);
        }
}

bool specialPrimeNumbers(int n, int k)
{
    SieveofEratosthenes(n);
    int count = 0;
    for (int i = 0; i < primes.size(); i++) {
        for (int j = 0; j < i - 1; j++) {

            // If a prime number is Special prime
            // number, then we increments the
            // value of k.
            if (primes[j] + primes[j + 1] + 1
                == primes[i]) {
                count++;
                break;
            }
        }

        // If at least k Special prime numbers
        // are present, then we return 1.
        // else we return 0 from outside of
        // the outer loop.
        if (count == k)
            return true;
    }
    return false;
}

// Driver function
int main()
{
    int n = 27, k = 2;
    if (specialPrimeNumbers(n, k))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether there
// exist at least k or not in range [2..n]
import java.util.*;
class GFG{
static ArrayList<Integer> primes = new ArrayList<Integer>();
// Generating all the prime numbers
// from 2 to n.
static void SieveofEratosthenes(int n)
{
    boolean[] visited=new boolean[n*n+2];
    for (int i = 2; i <= n + 1; i++)
        if (!visited[i]) {
            for (int j = i * i; j <= n + 1; j += i)
                visited[j] = true;
            primes.add(i);
        }
}

static boolean specialPrimeNumbers(int n, int k)
{
    SieveofEratosthenes(n);
    int count = 0;
    for (int i = 0; i < primes.size(); i++) {
        for (int j = 0; j < i - 1; j++) {

            // If a prime number is Special prime
            // number, then we increments the
            // value of k.
            if (primes.get(j) + primes.get(j + 1) + 1
                == primes.get(i)) {
                count++;
                break;
            }
        }

        // If at least k Special prime numbers
        // are present, then we return 1.
        // else we return 0 from outside of
        // the outer loop.
        if (count == k)
            return true;
    }
    return false;
}

// Driver function
public static void main(String[] args)
{
    int n = 27, k = 2;
    if (specialPrimeNumbers(n, k))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to check whether there
# exist at least k or not in range [2..n]
primes = [];

# Generating all the prime numbers
# from 2 to n.
def SieveofEratosthenes(n):

    visited = [False] * (n + 2);
    for i in range(2, n + 2):
        if (visited[i] == False):
            for j in range(i * i, n + 2, i):
                visited[j] = True;
            primes.append(i);

def specialPrimeNumbers(n, k):

    SieveofEratosthenes(n);
    count = 0;
    for i in range(len(primes)):
        for j in range(i - 1):

            # If a prime number is Special
            # prime number, then we increments
            # the value of k.
            if (primes[j] +
                primes[j + 1] + 1 == primes[i]):
                count += 1;
                break;

        # If at least k Special prime numbers
        # are present, then we return 1.
        # else we return 0 from outside of
        # the outer loop.
        if (count == k):
            return True;

    return False;

# Driver Code
n = 27;
k = 2;
if (specialPrimeNumbers(n, k)):
    print("YES");
else:
    print("NO");

# This code is contributed by mits
```

## C#

```
// C# program to check whether there
// exist at least k or not in range [2..n]
using System;
using System.Collections;

class GFG{
static ArrayList primes = new ArrayList();
// Generating all the prime numbers
// from 2 to n.
static void SieveofEratosthenes(int n)
{
    bool[] visited=new bool[n*n+2];
    for (int i = 2; i <= n + 1; i++)
        if (!visited[i]) {
            for (int j = i * i; j <= n + 1; j += i)
                visited[j] = true;
            primes.Add(i);
        }
}

static bool specialPrimeNumbers(int n, int k)
{
    SieveofEratosthenes(n);
    int count = 0;
    for (int i = 0; i < primes.Count; i++) {
        for (int j = 0; j < i - 1; j++) {

            // If a prime number is Special prime
            // number, then we increments the
            // value of k.
            if ((int)primes[j] + (int)primes[j + 1] + 1
                == (int)primes[i]) {
                count++;
                break;
            }
        }

        // If at least k Special prime numbers
        // are present, then we return 1.
        // else we return 0 from outside of
        // the outer loop.
        if (count == k)
            return true;
    }
    return false;
}

// Driver function
public static void Main()
{
    int n = 27, k = 2;
    if (specialPrimeNumbers(n, k))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether there
// exist at least k or not in range [2..n]
$primes = array();

// Generating all the prime numbers
// from 2 to n.
function SieveofEratosthenes($n)
{
    global $primes;
    $visited = array_fill(0, $n, false);
    for ($i = 2; $i <= $n + 1; $i++)
        if (!$visited[$i])
        {
            for ($j = $i * $i;
                 $j <= $n + 1; $j += $i)
                $visited[$j] = true;
            array_push($primes, $i);
        }
}

function specialPrimeNumbers($n, $k)
{
    global $primes;
    SieveofEratosthenes($n);
    $count = 0;
    for ($i = 0; $i < count($primes); $i++)
    {
        for ($j = 0; $j < $i - 1; $j++)
        {

            // If a prime number is Special prime
            // number, then we increments the
            // value of k.
            if ($primes[$j] +
                $primes[$j + 1] + 1 == $primes[$i])
            {
                $count++;
                break;
            }
        }

        // If at least k Special prime numbers
        // are present, then we return 1.
        // else we return 0 from outside of
        // the outer loop.
        if ($count == $k)
            return true;
    }
    return false;
}

// Driver Code
$n = 27;
$k = 2;
if (specialPrimeNumbers($n, $k))
    echo "YES\n";
else
    echo "NO\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // Javascript program to check whether there
    // exist at least k or not in range [2..n]

    let primes = [];

    // Generating all the prime numbers
    // from 2 to n.
    function SieveofEratosthenes(n)
    {
        let visited = new Array(n);
        visited.fill(false);
        for (let i = 2; i <= n + 1; i++)
            if (!visited[i]) {
                for (let j = i * i; j <= n + 1; j += i)
                    visited[j] = true;
                primes.push(i);
            }
    }

    function specialPrimeNumbers(n, k)
    {
        SieveofEratosthenes(n);
        let count = 0;
        for (let i = 0; i < primes.length; i++) {
            for (let j = 0; j < i - 1; j++) {

                // If a prime number is Special prime
                // number, then we increments the
                // value of k.
                if (primes[j] + primes[j + 1] + 1
                    == primes[i]) {
                    count++;
                    break;
                }
            }

            // If at least k Special prime numbers
            // are present, then we return 1.
            // else we return 0 from outside of
            // the outer loop.
            if (count == k)
                return true;
        }
        return false;
    }

    let n = 27, k = 2;
    if (specialPrimeNumbers(n, k))
        document.write("YES");
    else
        document.write("NO");

</script>
```

**输出:-**

```
 YES
```