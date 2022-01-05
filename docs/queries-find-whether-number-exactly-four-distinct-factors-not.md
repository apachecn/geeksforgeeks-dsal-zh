# 查询一个数字是否有四个截然不同的因子

> 原文:[https://www . geesforgeks . org/query-find-when-number-恰好-四个-distinct-factors-not/](https://www.geeksforgeeks.org/queries-find-whether-number-exactly-four-distinct-factors-not/)

给定一个正整数“q”和“n”。对于每个查询“q ”,找出一个数“n”是否正好有四个不同的除数。如果数字正好有四个除数，则打印“是”或“否”。1 <= q, n <= 10 <sup>6</sup>

```
Input:
2
10
12
Output:
Yes
No

Explanation:
For 1st query, n = 10 has exactly four divisor i.e., 1, 2, 5, 10.
For 2nd query, n = 12 has exactly six divisor i.e., 1, 2, 3, 4, 6, 12.
```

**简单的方法**就是用[这个](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)的方法生成一个数的所有除数来计数因子，之后检查所有因子的计数是否等于‘4’。这种方法的时间复杂度为 O(sqrt(n))。
**更好的做法**是用**数论**。一个数要有四个因子，必须满足以下条件:-

1.  如果数正好是两个质数的乘积(比如 p，q)。因此，我们可以保证它将有四个因素，即 1，p，q，n。
2.  如果一个数是素数的立方(或者这个数的立方根是素数)。例如，假设 n = 8，立方根= 2，这意味着“8”可以写成 2*2*2，因此四个因子是:- 1，2，4 和 8。

我们可以使用厄拉多塞的筛选，这样我们将预先计算从 1 到 10 <sup>6</sup> 的所有质因数。现在我们将通过使用两个“for loops”来标记所有是两个质数的乘积的数字，即 mark[p * q] =true。同时，我们还将通过取数字的立方来标记所有数字(立方根)，即，标记[p * p * p] = true。
之后，我们可以在 O(1)时间内轻松回答每个查询。
下面是伪代码，大家看看更好的理解

## C++

```
// C++ program to check whether number has
// exactly four distinct factors or not
#include <bits/stdc++.h>
using namespace std;

// Initialize global variable according
// to given condition so that it can be
// accessible to all function
const int N = 1e6;
bool fourDiv[N + 1];

// Function to calculate all number having
// four distinct distinct factors
void fourDistinctFactors()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    bool primeAll[N + 1];
    memset(primeAll, true, sizeof(primeAll));

    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed, then it
        // is a prime
        if (primeAll[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                primeAll[i] = false;
        }
    }

    // Initialize prime[] array which will
    // contains all the primes from 1-N
    vector<int> prime;

    for (int p = 2; p <= N; p++)
        if (primeAll[p])
            prime.push_back(p);

    // Set the marking of all primes to false
    memset(fourDiv, false, sizeof(fourDiv));

    // Iterate over all the prime numbers
    for (int i = 0; i < prime.size(); ++i) {
        int p = prime[i];

        // Mark cube root of prime numbers
        if (1LL * p * p * p <= N)
            fourDiv[p * p * p] = true;

        for (int j = i + 1; j < prime.size(); ++j) {
            int q = prime[j];

            if (1LL * p * q > N)
                break;

            // Mark product of prime numbers
            fourDiv[p * q] = true;
        }
    }
}

// Driver program
int main()
{
    fourDistinctFactors();

    int num = 10;
    if (fourDiv[num])
        cout << "Yes\n";
    else
        cout << "No\n";

    num = 12;
    if (fourDiv[num])
        cout << "Yes\n";
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether number has
// exactly four distinct factors or not
import java.util.*;
class GFG{
// Initialize global variable according
// to given condition so that it can be
// accessible to all function
static int N = (int)1E6;
static boolean[] fourDiv=new boolean[N + 1];

// Function to calculate all number having
// four distinct distinct factors
static void fourDistinctFactors()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    boolean[] primeAll=new boolean[N + 1];

    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed, then it
        // is a prime
        if (primeAll[p] == false) {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                primeAll[i] = true;
        }
    }

    // Initialize prime[] array which will
    // contains all the primes from 1-N
    ArrayList<Integer> prime=new ArrayList<Integer>();

    for (int p = 2; p <= N; p++)
        if (!primeAll[p])
            prime.add(p);

    // Iterate over all the prime numbers
    for (int i = 0; i < prime.size(); ++i) {
        int p = prime.get(i);

        // Mark cube root of prime numbers
        if (1L * p * p * p <= N)
            fourDiv[p * p * p] = true;

        for (int j = i + 1; j < prime.size(); ++j) {
            int q = prime.get(j);

            if (1L * p * q > N)
                break;

            // Mark product of prime numbers
            fourDiv[p * q] = true;
        }
    }
}

// Driver program
public static void main(String[] args)
{
    fourDistinctFactors();

    int num = 10;
    if (fourDiv[num])
        System.out.println("Yes");
    else
        System.out.println("No");

    num = 12;
    if (fourDiv[num])
        System.out.println("Yes");
    else
        System.out.println("No");

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to check whether number
# has exactly four distinct factors or not

# Initialize global variable according to
# given condition so that it can be
# accessible to all function
N = 1000001;
fourDiv = [False] * (N + 1);

# Function to calculate all number
# having four distinct factors
def fourDistinctFactors():

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is not a prime, else true.
    primeAll = [True] * (N + 1);
    p = 2;

    while (p * p <= N):

        # If prime[p] is not changed, then it
        # is a prime
        if (primeAll[p] == True):

            # Update all multiples of p
            i = p * 2;
            while (i <= N):
                primeAll[i] = False;
                i += p;
        p += 1;

    # Initialize prime[] array which will
    # contain all the primes from 1-N
    prime = [];

    for p in range(2, N + 1):
        if (primeAll[p]):
            prime.append(p);

    # Iterate over all the prime numbers
    for i in range(len(prime)):
        p = prime[i];

        # Mark cube root of prime numbers
        if (1 * p * p * p <= N):
            fourDiv[p * p * p] = True;

        for j in range(i + 1, len(prime)):
            q = prime[j];

            if (1 * p * q > N):
                break;

            # Mark product of prime numbers
            fourDiv[p * q] = True;

# Driver Code
fourDistinctFactors();

num = 10;
if (fourDiv[num]):
    print("Yes");
else:
    print("No");

num = 12;
if (fourDiv[num]):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
// C# program to check whether number has
// exactly four distinct factors or not
using System;
using System.Collections;

class GFG
{

// Initialize global variable according
// to given condition so that it can be
// accessible to all function
static int N = (int)1E6;
static bool[] fourDiv = new bool[N + 1];

// Function to calculate all number having
// four distinct distinct factors
static void fourDistinctFactors()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    bool[] primeAll = new bool[N + 1];

    for (int p = 2; p * p <= N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (primeAll[p] == false)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                primeAll[i] = true;
        }
    }

    // Initialize prime[] array which will
    // contains all the primes from 1-N
    ArrayList prime = new ArrayList();

    for (int p = 2; p <= N; p++)
        if (!primeAll[p])
            prime.Add(p);

    // Iterate over all the prime numbers
    for (int i = 0; i < prime.Count; ++i)
    {
        int p = (int)prime[i];

        // Mark cube root of prime numbers
        if (1L * p * p * p <= N)
            fourDiv[p * p * p] = true;

        for (int j = i + 1; j < prime.Count; ++j)
        {
            int q = (int)prime[j];

            if (1L * p * q > N)
                break;

            // Mark product of prime numbers
            fourDiv[p * q] = true;
        }
    }
}

// Driver Code
public static void Main()
{
    fourDistinctFactors();

    int num = 10;
    if (fourDiv[num])
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    num = 12;
    if (fourDiv[num])
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// GFG PHP Compiler not support 64-bit

// PHP program to check whether
// number has exactly four
// distinct factors or not

// Initialize global variable
// according to given condition
// so that it can be accessible
// to all function
$N = 1000001;
$fourDiv = array_fill(0,
           $N + 1, false);

// Function to calculate
// all number having four
// distinct factors
function fourDistinctFactors()
{
    global $N;
    global $fourDiv;

    // Create a boolean array
    // "prime[0..n]" and initialize
    // all entries it as true. A
    // value in prime[i] will finally
    // be false if i is not a prime,
    // else true.
    $primeAll = array_fill(0, $N + 1, true);

    for ($p = 2;
         $p * $p <= $N; $p++)
    {

        // If prime[p] is not
        // changed, then it
        // is a prime
        if ($primeAll[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $N; $i += $p)
                $primeAll[$i] = false;
        }
    }

    // Initialize prime[] array
    // which will contains all
    // the primes from 1-N
    $prime;
    $x = 0;

    for ($p = 2; $p <= $N; $p++)
        if ($primeAll[$p])
            $prime[$x++] = $p;

    // Iterate over all
    // the prime numbers
    for ($i = 0; $i < $x; ++$i)
    {
        $p = $prime[$i];

        // Mark cube root
        // of prime numbers
        if (1 * $p * $p * $p <= $N)
            $fourDiv[$p * $p * $p] = true;

        for ($j = $i + 1;
             $j < $x; ++$j)
        {
            $q = $prime[$j];

            if (1 * $p * $q > $N)
                break;

            // Mark product of
            // prime numbers
            $fourDiv[$p * $q] = true;
        }
    }
}

// Driver Code
fourDistinctFactors();

$num = 10;
if ($fourDiv[$num])
    echo "Yes\n";
else
    echo "No\n";

$num = 12;
if ($fourDiv[$num])
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to check whether number has
// exactly four distinct factors or not

// Initialize global variable according
// to given condition so that it can be
// accessible to all function
var N = 1000000;
var fourDiv = Array(N+1).fill(false);

// Function to calculate all number having
// four distinct distinct factors
function fourDistinctFactors()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    var primeAll = Array(N+1).fill(false);

    for (var p = 2; p * p <= N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (primeAll[p] == false)
        {

            // Update all multiples of p
            for (var i = p * 2; i <= N; i += p)
                primeAll[i] = true;
        }
    }

    // Initialize prime[] array which will
    // contains all the primes from 1-N
    var prime = [];

    for (var p = 2; p <= N; p++)
        if (!primeAll[p])
            prime.push(p);

    // Iterate over all the prime numbers
    for (var i = 0; i < prime.length; ++i)
    {
        var p = prime[i];

        // Mark cube root of prime numbers
        if (p * p * p <= N)
            fourDiv[p * p * p] = true;

        for(var j = i + 1; j < prime.length; ++j)
        {
            var q = prime[j];

            if (p * q > N)
                break;

            // Mark product of prime numbers
            fourDiv[p * q] = true;
        }
    }
}

// Driver Code
fourDistinctFactors();
var num = 10;
if (fourDiv[num])
    document.write("Yes<br>");
else
    document.write("No<br>");
num = 12;
if (fourDiv[num])
    document.write("Yes");
else
    document.write("No");

</script>
```

**输出:**

```
Yes
No
```

**时间复杂度:**每个查询 O(1)。
本文由[舒巴姆·班萨尔](https://www.quora.com/profile/Shubham-Bansal-209)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。