# 计算 o(n^1/3 n 的除数)

> 原文:[https://www.geeksforgeeks.org/count-divisors-n-on13/](https://www.geeksforgeeks.org/count-divisors-n-on13/)

给定一个数 n，计算它的所有不同除数。

**示例:**

```
Input : 18
Output : 6
Divisors of 18 are 1, 2, 3, 6, 9 and 18.

Input : 100
Output : 9
Divisors of 100 are 1, 2, 4, 5, 10, 20,
25, 50 and 100
```

一个简单的解决方案是将所有的数字从 1 迭代到 sqrt(n)，检查该数字是否除以 n，并增加除数。这种方法需要 0(sqrt(n))时间。

## C++

```
// C implementation of Naive method to count all
// divisors
#include <bits/stdc++.h>
using namespace std;

// function to count the divisors
int countDivisors(int n)
{
    int cnt = 0;
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            // If divisors are equal,
            // count only one
            if (n / i == i)
                cnt++;

            else // Otherwise count both
                cnt = cnt + 2;
        }
    }
    return cnt;
}

/* Driver program to test above function */
int main()
{
    printf("Total distinct divisors of 100 are : %d",
           countDivisors(100));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of Naive method
// to count all divisors
import java.io.*;
import java.math.*;

class GFG {

    // function to count the divisors
    static int countDivisors(int n)
    {
        int cnt = 0;
        for (int i = 1; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0) {
                // If divisors are equal,
                // count only one
                if (n / i == i)
                    cnt++;

                else // Otherwise count both
                    cnt = cnt + 2;
            }
        }
        return cnt;
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
        System.out.println("Total distinct "
                  + "divisors of 100 are : " 
                       + countDivisors(100));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 implementation of Naive method
# to count all divisors

import math

# function to count the divisors
def countDivisors(n) :
    cnt = 0
    for i in range(1, (int)(math.sqrt(n)) + 1) :
        if (n % i == 0) :

            # If divisors are equal,
            # count only one
            if (n / i == i) :
                cnt = cnt + 1
            else : # Otherwise count both
                cnt = cnt + 2

    return cnt

# Driver program to test above function */

print("Total distinct divisors of 100 are : ",
      countDivisors(100))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation of Naive method
// to count all divisors
using System;

class GFG {

    // function to count the divisors
    static int countDivisors(int n)
    {
        int cnt = 0;
        for (int i = 1; i <= Math.Sqrt(n);
                                      i++)
        {
            if (n % i == 0) {

                // If divisors are equal,
                // count only one
                if (n / i == i)
                    cnt++;

                // Otherwise count both
                else
                    cnt = cnt + 2;
            }
        }

        return cnt;
    }

    // Driver program
    public static void Main()
    {
        Console.WriteLine("Total distinct"
               + " divisors of 100 are : "
                    + countDivisors(100));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of Naive
// method to count all divisors

// function to count the divisors

function countDivisors($n)
{
    $cnt = 0;
    for ($i = 1; $i <= sqrt($n); $i++)
    {
        if ($n % $i == 0)
        {
            // If divisors are equal,
            // count only one
            if ($n / $i == $i)
            $cnt++;

            // Otherwise count both
            else
                $cnt = $cnt + 2;
        }
    }
    return $cnt;
}

// Driver Code
echo "Total distinct divisors of 100 are : ",
        countDivisors(100);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // function to count the divisors
    function countDivisors(n)
    {
        let cnt = 0;
        for (let i = 1; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0) {
                // If divisors are equal,
                // count only one
                if (n / i == i)
                    cnt++;

                else // Otherwise count both
                    cnt = cnt + 2;
            }
        }
        return cnt;
    }

// Driver Code

    document.write("Total distinct "
                  + "divisors of 100 are : " 
                       + countDivisors(100));

// This code is contributed by susmitakundugoaldanga.           
</script>
```

**输出:**

```
Total distinct divisors of 100 are : 9
```

**优化解决方案(O(n^1/3))**

对于一个数 n，我们试图找到一个数 X ≤ ∛N，即 X^3 ≤ N，这样它就可以除以这个数，另一个数 y，这样 N = X * Y. X 由 n 的所有质因数组成，n 小于∛N，y 包含所有大于 n 的质因数。因此，它们没有共同的因素，它们的 HCF 为 1。

我们遍历数字 1 到∛N，对于所有的素数，我们检查这个数是否除以 n。

如果质数是可分的，我们从数字 N 开始尽可能多地对它进行除法运算，这样，那个特定的质因数就不再存在了。我们继续这样做，所有质因数都小于∛N.，因此，循环后剩余的数不会有任何质因数小于∛N.

对于 N = p1<sup>E1</sup>* p2<sup>E2</sup>* p3<sup>E3</sup>…其中 P1、p2、P3..是质因数，除数由(e1+1) * (e2+1) * (e3+1)给出…

for 循环给出了小于∛N.的每个质因数的乘积(e+1)

剩余的数最多只能有 2 个质因数。我们将用矛盾来证明这一点。

> 假设 Y = p1 * p2 * p3，其中 p1、p2、p3 是素数，p1、p2、P3 > ∛n[如上所述]。
> 
> 因为 p1 >∛N 和 p2 > ∛N 和 p3 > ∛N
> 
> P1 * p2 * P3 > * n * * n * * n
> 
> => p1*p2*p3 > N .但是 Y 是 N 的因子，不能大于 N
> 
> 因此，存在矛盾，这意味着 p1、p2、p3 中的一个必须小于∛N.
> 
> 但是由于所有小于∛N 的质数都被 x 吸收了，这是不可能的。
> 
> 所以，Y 不能超过 2 个质因数。

因此，y 可以具有:

1 个质因数，如果它是指数为 1 的质数(Y)

1 个素数因子，如果它是素数的平方(sqrt(Y))，指数为 2

指数为 1 和 1 的复合(p1，p2)的 2 个质因数

因此，我们倍增:

如果 Y 是素数= >(Y 的指数，即 1 +1) = 2

如果 Y 是素数的平方= >(sqrt(Y)的指数，即 2+1) = 3

如果 Y 是复合的= >(P1+1 的指数)*(p2+1 的指数)= 2 * 2 = 4

## C++

```
// C++ program to count distinct divisors
// of a given number n
#include <bits/stdc++.h>
using namespace std;

void SieveOfEratosthenes(int n, bool prime[],
                         bool primesquare[], int a[])
{

    //For more details check out: https://www.geeksforgeeks.org/sieve-of-eratosthenes/

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    for (int i = 2; i <= n; i++)
        prime[i] = true;

    // Create a boolean array "primesquare[0..n*n+1]"
    // and initialize all entries it as false. A value
    // in squareprime[i] will finally be true if i is
    // square of prime, else false.
    for (int i = 0; i <= (n * n + 1); i++)
        primesquare[i] = false;

    // 1 is not a prime number
    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {
            // Update all multiples of p starting from p * p
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    int j = 0;
    for (int p = 2; p <= n; p++) {
        if (prime[p]) {
            // Storing primes in an array
            a[j] = p;

            // Update value in primesquare[p*p],
            // if p is prime.
            primesquare[p * p] = true;
            j++;
        }
    }
}

// Function to count divisors
int countDivisors(int n)
{
    // If number is 1, then it will have only 1
    // as a factor. So, total factors will be 1.
    if (n == 1)
        return 1;

    bool prime[n + 1], primesquare[n * n + 1];

    int a[n]; // for storing primes upto n

    // Calling SieveOfEratosthenes to store prime
    // factors of n and to store square of prime
    // factors of n
    SieveOfEratosthenes(n, prime, primesquare, a);

    // ans will contain total number of distinct
    // divisors
    int ans = 1;

    // Loop for counting factors of n
    for (int i = 0;; i++) {
        // a[i] is not less than cube root n
        if (a[i] * a[i] * a[i] > n)
            break;

        // Calculating power of a[i] in n.
        int cnt = 1; // cnt is power of prime a[i] in n.
        while (n % a[i] == 0) // if a[i] is a factor of n
        {
            n = n / a[i];
            cnt = cnt + 1; // incrementing power
        }

        // Calculating the number of divisors
        // If n = a^p * b^q then total divisors of n
        // are (p+1)*(q+1)
        ans = ans * cnt;
    }

    // if a[i] is greater than cube root of n

    // First case
    if (prime[n])
        ans = ans * 2;

    // Second case
    else if (primesquare[n])
        ans = ans * 3;

    // Third case
    else if (n != 1)
        ans = ans * 4;

    return ans; // Total divisors
}

// Driver Program
int main()
{
    cout << "Total distinct divisors of 100 are : "
         << countDivisors(100) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to count distinct
// divisors of a given number n
import java.io.*;

class GFG {

    static void SieveOfEratosthenes(int n, boolean prime[],
                                    boolean primesquare[], int a[])
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        for (int i = 2; i <= n; i++)
            prime[i] = true;

        /* Create a boolean array "primesquare[0..n*n+1]"
         and initialize all entries it as false.
         A value in squareprime[i] will finally
         be true if i is square of prime,
         else false.*/
        for (int i = 0; i < ((n * n) + 1); i++)
            primesquare[i] = false;

        // 1 is not a prime number
        prime[1] = false;

        for (int p = 2; p * p <= n; p++) {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        int j = 0;
        for (int p = 2; p <= n; p++) {
            if (prime[p]) {
                // Storing primes in an array
                a[j] = p;

                // Update value in
                // primesquare[p*p],
                // if p is prime.
                primesquare[p * p] = true;
                j++;
            }
        }
    }

    // Function to count divisors
    static int countDivisors(int n)
    {
        // If number is 1, then it will
        // have only 1 as a factor. So,
        // total factors will be 1.
        if (n == 1)
            return 1;

        boolean prime[] = new boolean[n + 1];
        boolean primesquare[] = new boolean[(n * n) + 1];

        // for storing primes upto n
        int a[] = new int[n];

        // Calling SieveOfEratosthenes to
        // store prime factors of n and to
        // store square of prime factors of n
        SieveOfEratosthenes(n, prime, primesquare, a);

        // ans will contain total number
        // of distinct divisors
        int ans = 1;

        // Loop for counting factors of n
        for (int i = 0;; i++) {
            // a[i] is not less than cube root n
            if (a[i] * a[i] * a[i] > n)
                break;

            // Calculating power of a[i] in n.
            // cnt is power of prime a[i] in n.
            int cnt = 1;

            // if a[i] is a factor of n
            while (n % a[i] == 0) {
                n = n / a[i];

                // incrementing power
                cnt = cnt + 1;
            }

            // Calculating the number of divisors
            // If n = a^p * b^q then total
            // divisors of n are (p+1)*(q+1)
            ans = ans * cnt;
        }

        // if a[i] is greater than cube root
        // of n

        // First case
        if (prime[n])
            ans = ans * 2;

        // Second case
        else if (primesquare[n])
            ans = ans * 3;

        // Third case
        else if (n != 1)
            ans = ans * 4;

        return ans; // Total divisors
    }

    // Driver Program
    public static void main(String args[])
    {
        System.out.println("Total distinct divisors"
                           + " of 100 are : " + countDivisors(100));
    }
}

/*This code is contributed by Nikita Tiwari*/
```

## 蟒蛇 3

```
# Python3 program to count distinct
# divisors of a given number n

def SieveOfEratosthenes(n, prime,primesquare, a):
    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as
    # true. A value in prime[i] will finally
    # be false if i is not a prime, else true.
    for i in range(2,n+1):
        prime[i] = True

    # Create a boolean array "primesquare[0..n*n+1]"
    # and initialize all entries it as false.
    # A value in squareprime[i] will finally be
    # true if i is square of prime, else false.
    for i in range((n * n + 1)+1):
        primesquare[i] = False

    # 1 is not a prime number
    prime[1] = False

    p = 2
    while(p * p <= n):
        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):
            # Update all multiples of p
            i = p * 2
            while(i <= n):
                prime[i] = False
                i += p
        p+=1

    j = 0
    for p in range(2,n+1):
        if (prime[p]==True):
            # Storing primes in an array
            a[j] = p

            # Update value in primesquare[p*p],
            # if p is prime.
            primesquare[p * p] = True
            j+=1

# Function to count divisors
def countDivisors(n):
    # If number is 1, then it will
    # have only 1 as a factor. So,
    # total factors will be 1.
    if (n == 1):
        return 1

    prime = [False]*(n + 2)
    primesquare = [False]*(n * n + 2)

    # for storing primes upto n
    a = [0]*n

    # Calling SieveOfEratosthenes to
    # store prime factors of n and to
    # store square of prime factors of n
    SieveOfEratosthenes(n, prime, primesquare, a)

    # ans will contain total
    # number of distinct divisors
    ans = 1

    # Loop for counting factors of n
    i=0
    while(1):
        # a[i] is not less than cube root n
        if(a[i] * a[i] * a[i] > n):
            break

        # Calculating power of a[i] in n.
        cnt = 1 # cnt is power of
                # prime a[i] in n.
        while (n % a[i] == 0): # if a[i] is a factor of n
            n = n / a[i]
            cnt = cnt + 1 # incrementing power

        # Calculating number of divisors
        # If n = a^p * b^q then total
        # divisors of n are (p+1)*(q+1)
        ans = ans * cnt
        i+=1

    # if a[i] is greater than
    # cube root of n

    n=int(n)
    # First case
    if (prime[n]==True):
        ans = ans * 2

    # Second case
    elif (primesquare[n]==True):
        ans = ans * 3

    # Third case
    elif (n != 1):
        ans = ans * 4

    return ans # Total divisors

# Driver Code
if __name__=='__main__':
    print("Total distinct divisors of 100 are :",countDivisors(100))

# This code is contributed
# by mits
```

## C#

```
// C# program to count distinct
// divisors of a given number n
using System;

class GFG {

    static void SieveOfEratosthenes(int n, bool[] prime,
                                    bool[] primesquare, int[] a)
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        for (int i = 2; i <= n; i++)
            prime[i] = true;

        /* Create a boolean array "primesquare[0..n*n+1]"
        and initialize all entries it as false.
        A value in squareprime[i] will finally
        be true if i is square of prime,
        else false.*/
        for (int i = 0; i < ((n * n) + 1); i++)
            primesquare[i] = false;

        // 1 is not a prime number
        prime[1] = false;

        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        int j = 0;
        for (int p = 2; p <= n; p++) {
            if (prime[p]) {

                // Storing primes in an array
                a[j] = p;

                // Update value in
                // primesquare[p*p],
                // if p is prime.
                primesquare[p * p] = true;
                j++;
            }
        }
    }

    // Function to count divisors
    static int countDivisors(int n)
    {

        // If number is 1, then it will
        // have only 1 as a factor. So,
        // total factors will be 1.
        if (n == 1)
            return 1;

        bool[] prime = new bool[n + 1];
        bool[] primesquare = new bool[(n * n) + 1];

        // for storing primes upto n
        int[] a = new int[n];

        // Calling SieveOfEratosthenes to
        // store prime factors of n and to
        // store square of prime factors of n
        SieveOfEratosthenes(n, prime, primesquare, a);

        // ans will contain total number
        // of distinct divisors
        int ans = 1;

        // Loop for counting factors of n
        for (int i = 0;; i++) {

            // a[i] is not less than cube root n
            if (a[i] * a[i] * a[i] > n)
                break;

            // Calculating power of a[i] in n.
            // cnt is power of prime a[i] in n.
            int cnt = 1;

            // if a[i] is a factor of n
            while (n % a[i] == 0) {
                n = n / a[i];

                // incrementing power
                cnt = cnt + 1;
            }

            // Calculating the number of divisors
            // If n = a^p * b^q then total
            // divisors of n are (p+1)*(q+1)
            ans = ans * cnt;
        }

        // if a[i] is greater than cube root
        // of n

        // First case
        if (prime[n])
            ans = ans * 2;

        // Second case
        else if (primesquare[n])
            ans = ans * 3;

        // Third case
        else if (n != 1)
            ans = ans * 4;

        return ans; // Total divisors
    }

    // Driver Program
    public static void Main()
    {
        Console.Write("Total distinct divisors"
                      + " of 100 are : " + countDivisors(100));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count distinct
// divisors of a given number n

function SieveOfEratosthenes($n, &$prime,
                             &$primesquare, &$a)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as
    // true. A value in prime[i] will finally
    // be false if i is not a prime, else true.
    for ($i = 2; $i <= $n; $i++)
        $prime[$i] = true;

    // Create a boolean array "primesquare[0..n*n+1]"
    // and initialize all entries it as false.
    // A value in squareprime[i] will finally be
    // true if i is square of prime, else false.
    for ($i = 0; $i <= ($n * $n + 1); $i++)
        $primesquare[$i] = false;

    // 1 is not a prime number
    $prime[1] = false;

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    $j = 0;
    for ($p = 2; $p <= $n; $p++)
    {
        if ($prime[$p])
        {
            // Storing primes in an array
            $a[$j] = $p;

            // Update value in primesquare[p*p],
            // if p is prime.
            $primesquare[$p * $p] = true;
            $j++;
        }
    }
}

// Function to count divisors
function countDivisors($n)
{
    // If number is 1, then it will
    // have only 1 as a factor. So,
    // total factors will be 1.
    if ($n == 1)
        return 1;

    $prime = array_fill(false, $n + 1, NULL);
    $primesquare = array_fill(false,
                          $n * $n + 1, NULL);

    // for storing primes upto n
    $a = array_fill(0, $n, NULL);

    // Calling SieveOfEratosthenes to
    // store prime factors of n and to
    // store square of prime factors of n
    SieveOfEratosthenes($n, $prime,
                        $primesquare, $a);

    // ans will contain total
    // number of distinct divisors
    $ans = 1;

    // Loop for counting factors of n
    for ($i = 0;; $i++)
    {
        // a[i] is not less than cube root n
        if ($a[$i] * $a[$i] * $a[$i] > $n)
            break;

        // Calculating power of a[i] in n.
        $cnt = 1; // cnt is power of
                  // prime a[i] in n.
        while ($n % $a[$i] == 0) // if a[i] is a
                                 // factor of n
        {
            $n = $n / $a[$i];
            $cnt = $cnt + 1; // incrementing power
        }

        // Calculating the number of divisors
        // If n = a^p * b^q then total
        // divisors of n are (p+1)*(q+1)
        $ans = $ans * $cnt;
    }

    // if a[i] is greater than
    // cube root of n

    // First case
    if ($prime[$n])
        $ans = $ans * 2;

    // Second case
    else if ($primesquare[$n])
        $ans = $ans * 3;

    // Third case
    else if ($n != 1)
        $ans = $ans * 4;

    return $ans; // Total divisors
}

// Driver Code
echo "Total distinct divisors of 100 are : ".
                    countDivisors(100). "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to count distinct
// divisors of a given number n

function SieveOfEratosthenes(n, prime, primesquare, a)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    for(let i = 2; i <= n; i++)
        prime[i] = true;

    // Create a boolean array "primesquare[0..n*n+1]"
    // and initialize all entries it as false.
    // A value in squareprime[i] will finally
    // be true if i is square of prime,
    // else false.
    for(let i = 0; i < ((n * n) + 1); i++)
        primesquare[i] = false;

    // 1 is not a prime number
    prime[1] = false;

    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    let j = 0;
    for(let p = 2; p <= n; p++)
    {
        if (prime[p])
        {

            // Storing primes in an array
            a[j] = p;

            // Update value in
            // primesquare[p*p],
            // if p is prime.
            primesquare[p * p] = true;
            j++;
        }
    }
}

// Function to count divisors
function countDivisors(n)
{

    // If number is 1, then it will
    // have only 1 as a factor. So,
    // total factors will be 1.
    if (n == 1)
        return 1;

    let prime = new Array(n + 1);
    let primesquare = new Array((n * n) + 1);

    // For storing primes upto n
    let a = new Array(n);
    for(let i = 0; i < n; i++)
    {
        a[i] = 0;
    }

    // Calling SieveOfEratosthenes to
    // store prime factors of n and to
    // store square of prime factors of n
    SieveOfEratosthenes(n, prime, primesquare, a);

    // ans will contain total number
    // of distinct divisors
    let ans = 1;

    // Loop for counting factors of n
    for(let i = 0;; i++)
    {

        // a[i] is not less than cube root n
        if (a[i] * a[i] * a[i] > n)
            break;

        // Calculating power of a[i] in n.
        // cnt is power of prime a[i] in n.
        let cnt = 1;

        // If a[i] is a factor of n
        while (n % a[i] == 0)
        {
            n = n / a[i];

            // Incrementing power
            cnt = cnt + 1;
        }

        // Calculating the number of divisors
        // If n = a^p * b^q then total
        // divisors of n are (p+1)*(q+1)
        ans = ans * cnt;
    }

    // If a[i] is greater than cube root
    // of n

    // First case
    if (prime[n])
        ans = ans * 2;

    // Second case
    else if (primesquare[n])
        ans = ans * 3;

    // Third case
    else if (n != 1)
        ans = ans * 4;

    // Total divisors
    return ans;
}

// Driver Code
document.write("Total distinct divisors" +
               " of 100 are : " + countDivisors(100));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Total distinct divisors of 100 are : 9
```

**时间复杂度:** O(n <sup>1/3</sup>

本文由 **Karun Anantharaman** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。