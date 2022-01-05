# 范围[L，R]内的数字，其除数既是偶数又是素数

> 原文:[https://www . geeksforgeeks . org/numbers-in-range-l-r-so-他们的除数都是偶数和素数/](https://www.geeksforgeeks.org/numbers-in-range-l-r-such-that-the-count-of-their-divisors-is-both-even-and-prime/)

给定一个范围[L，R]，任务是从这个范围中找出除素数外还有除数的数。
然后，打印找到的数字的计数。l 和 r 的值小于 10^6 和 L < R.
**例:**

```
Input: L=3, R=9
Output: Count = 3
Explanation: The numbers are 3, 5, 7 

Input : L=3, R=17
Output : Count: 6
```

> 1.  The unique prime number, also an even number, is' 2'.
> 2.  Therefore, we need to find all numbers with exactly two divisors in a given range,
>     is the prime number.

**简单的方法:**

1.  从“l”到“r”开始循环，检查数字是否为质数(对于更大的范围需要更多的时间)。
2.  如果数字是质数，则递增计数变量。
3.  最后，打印计数的值。

**一种有效的方法:**

*   我们必须计算范围[L，R]内的素数。
*   首先，创建一个筛子，它将有助于确定这个数字在 O(1)时间内是否是质数。
*   然后，创建一个前缀数组来存储素数的计数，其中，索引“I”处的元素保存从“1”到“I”的素数计数。
*   现在，如果我们想找到范围[L，R]内素数的计数，计数将是(sum[R]–sum[L-1])
*   最后，打印结果(即总和[R]–总和[L-1])

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000

// stores whether the number is prime or not
bool prime[MAX + 1];

// stores the count of prime numbers
// less than or equal to the index
int sum[MAX + 1];

// create the sieve
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all the entries as true. A value in prime[i] will
    // finally be false if 'i' is Not a prime, else true.
    memset(prime, true, sizeof(prime));
    memset(sum, 0, sizeof(sum));
    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p]) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // stores the prefix sum of number
    // of primes less than or equal to 'i'
    for (int i = 1; i <= MAX; i++) {
        if (prime[i] == true)
            sum[i] = 1;

        sum[i] += sum[i - 1];
    }
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();

    // 'l' and 'r' are the lower and upper bounds
    // of the range
    int l = 3, r = 9;

    // get the value of count
    int c = (sum[r] - sum[l - 1]);

    // display the count
    cout << "Count: " << c << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int MAX=1000000;

    // stores whether the number is prime or not
    static boolean []prime=new boolean[MAX + 1];

    // stores the count of prime numbers
    // less than or equal to the index
    static int []sum=new int[MAX + 1];

    // create the sieve
    static void SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..n]" and initialize
        // all the entries as true. A value in prime[i] will
        // finally be false if 'i' is Not a prime, else true.
        for(int i=0;i<=MAX;i++)
            prime[i]=true;

         for(int i=0;i<=MAX;i++)
            sum[i]=0;

        prime[1] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p]) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }

        // stores the prefix sum of number
        // of primes less than or equal to 'i'
        for (int i = 1; i <= MAX; i++) {
            if (prime[i] == true)
                sum[i] = 1;

            sum[i] += sum[i - 1];
        }
    }

    // Driver code
    public static void main(String []args)
    {
        // create the sieve
        SieveOfEratosthenes();

        // 'l' and 'r' are the lower and upper bounds
        // of the range
        int l = 3, r = 9;

        // get the value of count
        int c = (sum[r] - sum[l - 1]);

        // display the count
        System.out.println("Count: " + c);

    }

}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 1000000

# stores whether the number is prime or not
prime = [True] * (MAX + 1)

# stores the count of prime numbers
# less than or equal to the index
sum = [0] * (MAX + 1)

# create the sieve
def SieveOfEratosthenes():

    prime[1] = False

    p = 2
    while p * p <= MAX:

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p
            i = p * 2
            while i <= MAX:
                prime[i] = False
                i += p

        p += 1

    # stores the prefix sum of number
    # of primes less than or equal to 'i'
    for i in range(1, MAX + 1):
        if (prime[i] == True):
            sum[i] = 1

        sum[i] += sum[i - 1]

# Driver code
if __name__ == "__main__":

    # create the sieve
    SieveOfEratosthenes()

    # 'l' and 'r' are the lower and
    # upper bounds of the range
    l = 3
    r = 9

    # get the value of count
    c = (sum[r] - sum[l - 1])

    # display the count
    print("Count:", c)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach

using System;
class GFG
{
    static int MAX=1000000;

    // stores whether the number is prime or not
    static bool []prime=new bool[MAX + 1];

    // stores the count of prime numbers
    // less than or equal to the index
    static int []sum=new int[MAX + 1];

    // create the sieve
    static void SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..n]" and initialize
        // all the entries as true. A value in prime[i] will
        // finally be false if 'i' is Not a prime, else true.
        for(int i=0;i<=MAX;i++)
            prime[i]=true;

         for(int i=0;i<=MAX;i++)
            sum[i]=0;

        prime[1] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p]) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }

        // stores the prefix sum of number
        // of primes less than or equal to 'i'
        for (int i = 1; i <= MAX; i++) {
            if (prime[i] == true)
                sum[i] = 1;

            sum[i] += sum[i - 1];
        }
    }

    // Driver code
    public static void Main()
    {
        // create the sieve
        SieveOfEratosthenes();

        // 'l' and 'r' are the lower and upper bounds
        // of the range
        int l = 3, r = 9;

        // get the value of count
        int c = (sum[r] - sum[l - 1]);

        // display the count
        Console.WriteLine("Count: " + c);

    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 100000;

// Create a boolean array "prime[0..n]"
// and initialize all the entries as
// true. A value in prime[i] will finally
// be false if 'i' is Not a prime, else true.

// stores whether the number
// is prime or not
$prime = array_fill(0, $MAX + 1, true);

// stores the count of prime numbers
// less than or equal to the index
$sum = array_fill(0, $MAX + 1, 0);

// create the sieve
function SieveOfEratosthenes()
{
    global $MAX, $sum, $prime;
    $prime[1] = false;

    for ($p = 2; $p * $p <= $MAX; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p])
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $MAX; $i += $p)
                $prime[$i] = false;
        }
    }

    // stores the prefix sum of number
    // of primes less than or equal to 'i'
    for ($i = 1; $i <= $MAX; $i++)
    {
        if ($prime[$i] == true)
            $sum[$i] = 1;

        $sum[$i] += $sum[$i - 1];
    }
}

// Driver code

// create the sieve
SieveOfEratosthenes();

// 'l' and 'r' are the lower
// and upper bounds of the range
$l = 3;
$r = 9;

// get the value of count
$c = ($sum[$r] - $sum[$l - 1]);

// display the count
echo "Count: " . $c . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MAX = 1000000;

// stores whether the number is prime or not
var prime = Array(MAX+1).fill(true);

// stores the count of prime numbers
// less than or equal to the index
var sum = Array(MAX+1).fill(0);

// create the sieve
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all the entries as true. A value in prime[i] will
    // finally be false if 'i' is Not a prime, else true.

    prime[1] = false;

    for (var p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p]) {

            // Update all multiples of p
            for (var i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // stores the prefix sum of number
    // of primes less than or equal to 'i'
    for (var i = 1; i <= MAX; i++) {
        if (prime[i] == true)
            sum[i] = 1;

        sum[i] += sum[i - 1];
    }
}

// Driver code
// create the sieve
SieveOfEratosthenes();
// 'l' and 'r' are the lower and upper bounds
// of the range
var l = 3, r = 9;
// get the value of count
var c = (sum[r] - sum[l - 1]);
// display the count
document.write( "Count: " + c );

</script>
```

**Output:** 

```
Count: 3
```