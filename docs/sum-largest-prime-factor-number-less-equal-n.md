# 每个小于等于 n 的数的最大质因数之和

> 原文:[https://www . geesforgeks . org/sum-最大-质因数-数-减-等-n/](https://www.geeksforgeeks.org/sum-largest-prime-factor-number-less-equal-n/)

给定一个非负整数 **n** 。问题是求小于等于 **n** 的每个数的最大质因数之和。

示例:

```
Input : n = 10
Output : 32
Largest prime factor of each number
Prime factor of 2 = 2
Prime factor of 3 = 3
Prime factor of 4 = 2
Prime factor of 5 = 5
Prime factor of 6 = 3
Prime factor of 7 = 7
Prime factor of 8 = 2
Prime factor of 9 = 3
Prime factor of 10 = 5

Sum = (2+3+2+5+3+7+2+3+5) = 32

Input : n = 12
Output : 46

```

**算法:**

```
sumOfLargePrimeFactor(n)
    Declare prime[n+1] and initialize all value to 0
    Initialize sum = 0
    max = n / 2

    for p = 2 to max
        if prime[p] == 0 then
            i = p*2
            while i <= n
                prime[i] = p
                i = i + p

    for p = 2 to n
        if prime[p] then
               sum = sum + prime[p]
           else
              sum = sum + p

    return sum
```

## C++

```
// C++ implementation to find sum of largest prime factor
// of each number less than equal to n
#include <bits/stdc++.h>

using namespace std;

// function to find sum of largest prime factor
// of each number less than equal to n
int sumOfLargePrimeFactor(int n)
{
    // Create an integer array "prime[0..n]" and initialize
    // all entries of it as 0\. A value in prime[i] will
    // finally be 0 if 'i' is a prime, else it will
    // contain the largest prime factor of 'i'.
    int prime[n+1], sum = 0;
    memset(prime, 0, sizeof(prime));
    int max = n / 2;

    for (int p=2; p<=max; p++)
    {
        // If prime[p] is '0', then it is a
        // prime number
        if (prime[p] == 0)
        {
            // Update all multiples of p
            for (int i=p*2; i<=n; i += p)
                prime[i] = p;
        }
    }

    // Sum up the largest prime factor of all
    // the numbers
    for (int p=2; p<=n; p++)
    {
        // if 'p' is a non- prime number then
        // prime[p] gives its largesr prime
        // factor
        if (prime[p])
             sum += prime[p];

        // 'p' is a prime number        
        else
             sum += p;
    }

    // required sum
    return sum;     
}

// Driver program to test above
int main()
{
    int n = 12;
    cout << "Sum = "
         << sumOfLargePrimeFactor(n);
    return 0;        
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum
// of largest prime factor of each
// number less than equal to n
import java.io.*;
import java.util.*;

class GFG {

    // function to find sum of largest
    // prime factorof each number
    // less than equal to n
    static int sumOfLargePrimeFactor(int n)
    {
        // Create an integer array "prime[0..n]"
        // and initialize all entries of it as 0.
        // A value in prime[i] will finally be 0
        // if 'i' is a prime, else it will contain
        // the largest prime factor of 'i'.
        int prime[] = new int[n + 1], sum = 0;
        Arrays.fill(prime, 0);
        int max = n / 2;

        for (int p = 2; p <= max; p++)
        {
            // If prime[p] is '0', then it is a
            // prime number
            if (prime[p] == 0)
            {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = p;
            }
        }

        // Sum up the largest prime factor of all
        // the numbers
        for (int p = 2; p <= n; p++)
        {
            // if 'p' is a non- prime number then
            // prime[p] gives its largesr prime
            // factor
            if (prime[p] != 0)
                sum += prime[p];

            // 'p' is a prime number        
            else
                sum += p;
        }

        // required sum
        return sum;    
    }

    // Driver program
    public static void main(String args[])
    {
        int n = 12;
        System.out.println("Sum = "
                           + sumOfLargePrimeFactor(n));
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 code implementation to find
# sum of largest prime factor of
# each number less than equal to n

# function to find sum of largest
# prime factor of each number less
# than equal to n
def sumOfLargePrimeFactor( n ):

    # Create an integer array "prime[0..n]"
    # and initialize all entries of it
    # as 0\. A value in prime[i] will
    # finally be 0 if 'i' is a prime,
    # else it will contain the largest
    # prime factor of 'i'.
    prime = [0] * (n + 1)
    sum = 0
    max = int(n / 2)
    for p in range(2, max + 1):

        # If prime[p] is '0', then
        # it is a prime number
        if prime[p] == 0:

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                prime[i] = p

    # Sum up the largest prime factor
    # of all the numbers
    for p in range(2, n + 1):

        # if 'p' is a non- prime
        # number then prime[p] gives
        # its largesr prime factor
        if prime[p]:
            sum += prime[p]

        # 'p' is a prime number
        else:
            sum += p

    # required sum
    return sum

# Driver code to test above function
n = 12
print("Sum =", sumOfLargePrimeFactor(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# implementation to find sum
// of largest prime factor of each
// number less than equal to n
using System;

class GFG {

    // function to find sum of largest
    // prime factorof each number
    // less than equal to n
    static int sumOfLargePrimeFactor(int n)
    {
        // Create an integer array "prime[0..n]"
        // and initialize all entries of it as 0.
        // A value in prime[i] will finally be 0
        // if 'i' is a prime, else it will contain
        // the largest prime factor of 'i'.
        int[] prime = new int[n + 1];
        int sum = 0;

        for (int i = 1; i < n + 1; i++)
            prime[i] = 0;

        int max = n / 2;

        for (int p = 2; p <= max; p++)
        {
            // If prime[p] is '0', then it is a
            // prime number
            if (prime[p] == 0)
            {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = p;
            }
        }

        // Sum up the largest prime factor of all
        // the numbers
        for (int p = 2; p <= n; p++)
        {
            // if 'p' is a non- prime number then
            // prime[p] gives its largesr prime
            // factor
            if (prime[p] != 0)
                sum += prime[p];

            // 'p' is a prime number
            else
                sum += p;
        }

        // required sum
        return sum;
    }

    // Driver program
    public static void Main()
    {
        int n = 12;
        Console.WriteLine("Sum = " + sumOfLargePrimeFactor(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find sum of largest prime factor
// of each number less than equal to n

// function to find sum of largest prime factor
// of each number less than equal to n
function sumOfLargePrimeFactor($n)
{
    // Create an integer array "prime[0..n]" and initialize
    // all entries of it as 0\. A value in prime[i] will
    // finally be 0 if 'i' is a prime, else it will
    // contain the largest prime factor of 'i'.
    $prime=array_fill(0,$n+1,0);
    $sum = 0;
    $max = (int)($n / 2);

    for ($p=2; $p<=$max; $p++)
    {
        // If prime[p] is '0', then it is a
        // prime number
        if ($prime[$p] == 0)
        {
            // Update all multiples of p
            for ($i=$p*2; $i<=$n; $i += $p)
                $prime[$i] = $p;
        }
    }

    // Sum up the largest prime factor of all
    // the numbers
    for ($p=2; $p<=$n; $p++)
    {
        // if 'p' is a non- prime number then
        // prime[p] gives its largesr prime
        // factor
        if ($prime[$p])
            $sum += $prime[$p];

        // 'p' is a prime number        
        else
            $sum += $p;
    }

    // required sum
    return $sum;    
}

// Driver program to test above

    $n = 12;
    echo "Sum = ".sumOfLargePrimeFactor($n);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find sum
// of largest prime factor of each
// number less than equal to n

// function to find sum of largest prime factor
// of each number less than equal to n
function sumOfLargePrimeFactor(n)
{

    // Create an integer array "prime[0..n]"
    // and initialize all entries of it as
    // 0\. A value in prime[i] will finally
    // be 0 if 'i' is a prime, else it will
    // contain the largest prime factor of 'i'.
    let prime = new Array(n + 1);
    let sum = 0;
    let max = n / 2;

    for(let i = 0; i < n + 1; i++)
        prime[i] = 0;

    for(let p = 2; p <= max; p++)
    {

        // If prime[p] is '0', then it is a
        // prime number
        if (prime[p] == 0)
        {

            // Update all multiples of p
            for(let i = p * 2; i <= n; i += p)
                prime[i] = p;
        }
    }

    // Sum up the largest prime factor of all
    // the numbers
    for(let p = 2; p <= n; p++)
    {

        // If 'p' is a non- prime number then
        // prime[p] gives its largesr prime
        // factor
        if (prime[p])
             sum += prime[p];

        // 'p' is a prime number        
        else
             sum += p;
    }

    // Required sum
    return sum;     
}

// Driver code
let n = 12;
document.write("Sum = " +
               sumOfLargePrimeFactor(n));

// This code is contributed by mohit kumar 29

</script>
```

**输出:**

```
Sum = 46
```

时间复杂度:O(N*log(logN))

辅助空间:O(N)