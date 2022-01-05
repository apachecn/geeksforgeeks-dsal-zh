# 小于 n 的循环素数

> 原文:[https://www.geeksforgeeks.org/circular-primes-less-than-n/](https://www.geeksforgeeks.org/circular-primes-less-than-n/)

找出所有小于给定数 n 的循环素数，如果一个素数所有可能的旋转都是素数，那么这个素数就是 [**循环素数**](https://en.wikipedia.org/wiki/Circular_prime) 。

**示例:**

```
79 is a circular prime.
as 79 and 97 are prime numbers.

But 23 is not a circular prime.
as 23 is prime but 32 is not a prime number. 
```

**算法:**

```
-> Find prime numbers up to n using Sieve of Sundaram algorithm.
-> Now for every prime number from sieve method,
  one after another, we should check whether its all
  rotations are prime or not:
   -> If yes then print that prime number.
   -> If no then skip that prime number.
```

下面是上述算法的实现:

## C++

```
// C++ program to print primes smaller than n using
// Sieve of Sundaram.
#include <bits/stdc++.h>
using namespace std;

// Prototypes of the methods used
void SieveOfSundaram(bool marked[], int);
int Rotate(int);
int countDigits(int);

// Print all circular primes
void circularPrime(int n)
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x.
    // Since we want primes smaller than n, we reduce n to half
    int nNew = (n - 2) / 2;

    // This array is used to separate numbers of the form i+j+2ij
    // from others where 1 <= i <= j
    bool marked[nNew + 1];

    // Initialize all elements as not marked
    memset(marked, false, sizeof(marked));

    SieveOfSundaram(marked, nNew);

    // if n > 2 then 2 is also a circular prime
    cout << "2 ";

    // According to Sieve of sundaram If marked[i] is false
    // then 2*i + 1 is a prime number.

    // loop to check all  prime numbers and their rotations
    for (int i = 1; i <= nNew; i++) {
        // Skip this number if not prime
        if (marked[i] == true)
            continue;

        int num = 2 * i + 1;
        num = Rotate(num); // function for rotation of prime

        // now we check for rotations of this prime number
        // if new rotation is prime check next rotation,
        // till new rotation becomes the actual prime number
        // and if new rotation if not prime then break
        while (num != 2 * i + 1) {
            if (num % 2 == 0) // check for even
                break;

            // if rotated number is prime then rotate
            // for next
            if (marked[(num - 1) / 2] == false)
                num = Rotate(num);
            else
                break;
        }

        // if checked number is circular prime print it
        if (num == (2 * i + 1))
            cout << num << " ";
    }
}

// Sieve of Sundaram for generating prime number
void SieveOfSundaram(bool marked[], int nNew)
{
    // Main logic of Sundaram. Mark all numbers of the
    // form i + j + 2ij as true where 1 <= i <= j
    for (int i = 1; i <= nNew; i++)
        for (int j = i; (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;
}

// Rotate function to right rotate the number
int Rotate(int n)
{
    int rem = n % 10; // find unit place number
    rem *= pow(10, countDigits(n)); // to put unit place
    // number as first digit.
    n /= 10; // remove unit digit
    n += rem; // add first digit to rest
    return n;
}

// Function to find total number of digits
int countDigits(int n)
{
    int digit = 0;
    while (n /= 10)
        digit++;
    return digit;
}

// Driver program to test above
int main(void)
{
    int n = 100;
    circularPrime(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print primes smaller
// than n using Sieve of Sundaram.
import java.util.Arrays;
class GFG {

    // Print all circular primes
    static void circularPrime(int n)
    {
        // In general Sieve of Sundaram, produces
        // primes smaller than (2*x + 2) for a
        // number given number x.Since we want
        // primes smaller than n, we reduce n to half
        int nNew = (n - 2) / 2;

        // This array is used to separate numbers of the
        // form i+j+2ij from others where 1 <= i <= j
        boolean marked[] = new boolean[nNew + 1];

        // Initialize all elements as not marked
        Arrays.fill(marked, false);

        SieveOfSundaram(marked, nNew);

        // if n > 2 then 2 is also a circular prime
        System.out.print("2 ");

        // According to Sieve of sundaram If marked[i] is false
        // then 2*i + 1 is a prime number.

        // loop to check all prime numbers and their rotations
        for (int i = 1; i <= nNew; i++) {
            // Skip this number if not prime
            if (marked[i] == true)
                continue;

            int num = 2 * i + 1;
            num = Rotate(num); // function for rotation of prime

            // now we check for rotations of this prime number
            // if new rotation is prime check next rotation,
            // till new rotation becomes the actual prime number
            // and if new rotation if not prime then break
            while (num != 2 * i + 1) {
                if (num % 2 == 0) // check for even
                    break;

                // if rotated number is prime then rotate
                // for next
                if (marked[(num - 1) / 2] == false)
                    num = Rotate(num);
                else
                    break;
            }

            // if checked number is circular prime print it
            if (num == (2 * i + 1))
                System.out.print(num + " ");
        }
    }

    // Sieve of Sundaram for generating prime number
    static void SieveOfSundaram(boolean marked[], int nNew)
    {
        // Main logic of Sundaram. Mark all numbers of the
        // form i + j + 2ij as true where 1 <= i <= j
        for (int i = 1; i <= nNew; i++)
            for (int j = i; (i + j + 2 * i * j) <= nNew; j++)
                marked[i + j + 2 * i * j] = true;
    }

    // Function to find total number of digits
    static int countDigits(int n)
    {
        int digit = 0;
        while ((n /= 10) > 0)
            digit++;
        return digit;
    }

    // Rotate function to right rotate the number
    static int Rotate(int n)
    {
        int rem = n % 10; // find unit place number
        rem *= Math.pow(10, countDigits(n)); // to put unit place
        // number as first digit.
        n /= 10; // remove unit digit
        n += rem; // add first digit to rest
        return n;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 100;
        circularPrime(n);
    }
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to print primes smaller
# than n using Sieve of Sundaram.

# Print all circular primes
def circularPrime(n):

    # In general Sieve of Sundaram,
    # produces primes smaller than
    # (2*x + 2) for a number given
    # number x. Since we want primes
    # smaller than n, we reduce n to half
    nNew = (n - 2) // 2

    # This array is used to separate numbers
    # of the form i+j+2ij from others
    # where 1 <= i <= j
    marked = [False for i in range(nNew + 1)]

    SieveOfSundaram(marked, nNew)

    # If n > 2 then 2 is also a
    # circular prime
    print("2", end = ' ')

    # According to Sieve of sundaram
    # If marked[i] is false then
    # 2*i + 1 is a prime number.

    # Loop to check all  prime numbers
    # and their rotations
    for i in range(1, nNew + 1):

        # Skip this number if not prime
        if (marked[i] == True):
            continue;

        num = 2 * i + 1

        # Function for rotation of prime
        num = Rotate(num)

        # Now we check for rotations of this
        # prime number if new rotation is
        # prime check next rotation, till
        # new rotation becomes the actual
        # prime number and if new rotation
        # if not prime then break
        while (num != 2 * i + 1):

            # Check for even
            if (num % 2 == 0):
                break

            # If rotated number is prime
            # then rotate for next
            if (marked[(num - 1) // 2] == False):
                num = Rotate(num);
            else:
                break;

        # If checked number is circular
        # prime print it
        if (num == (2 * i + 1)):
            print(num, end = ' ')

# Sieve of Sundaram for generating
# prime number
def SieveOfSundaram(marked, nNew):

    # Main logic of Sundaram. Mark
    # all numbers of the form
    # i + j + 2ij as true where 1 <= i <= j
    for i in range(1, nNew + 1):
        j = i
        while (i + j + 2 * i * j) <= nNew:
            marked[i + j + 2 * i * j] = True
            j += 1

# Rotate function to right rotate
# the number
def Rotate(n):

    # Find unit place number
    rem = n % 10

    # To put unit place
    rem = rem * (10 ** (countDigits(n) - 1))

    # Number as first digit.
    n = n // 10 # Remove unit digit
    n += rem # Add first digit to rest
    return n

# Function to find total number of digits
def countDigits(n):

    digit = 0

    while n != 0:
        n = n // 10
        digit += 1

    return digit

# Driver code
if __name__=="__main__":

    n = 100

    circularPrime(n)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print primes smaller
// than n using Sieve of Sundaram.
using System;

class GFG {

    // Print all circular primes
    static void circularPrime(int n)
    {
        // In general Sieve of Sundaram, produces
        // primes smaller than (2*x + 2) for a
        // number given number x.Since we want
        // primes smaller than n, we reduce n to half
        int nNew = (n - 2) / 2;

        // This array is used to separate numbers of the
        // form i+j+2ij from others where 1 <= i <= j
        bool[] marked = new bool[nNew + 1];

        // Initialize all elements as not marked
        // Arrays.fill(marked, false);

        SieveOfSundaram(marked, nNew);

        // if n > 2 then 2 is also a circular prime
        Console.Write("2 ");

        // According to Sieve of sundaram If
        // marked[i] is false then 2*i + 1 is a
        // prime number.

        // loop to check all prime numbers
        // and their rotations
        for (int i = 1; i <= nNew; i++) {

            // Skip this number if not prime
            if (marked[i] == true)
                continue;

            int num = 2 * i + 1;

            // function for rotation of prime
            num = Rotate(num);

            // now we check for rotations of this prime number
            // if new rotation is prime check next rotation,
            // till new rotation becomes the actual prime number
            // and if new rotation if not prime then break
            while (num != 2 * i + 1) {
                if (num % 2 == 0) // check for even
                    break;

                // if rotated number is prime
                // then rotate for next
                if (marked[(num - 1) / 2] == false)
                    num = Rotate(num);
                else
                    break;
            }

            // if checked number is circular prime print it
            if (num == (2 * i + 1))
                Console.Write(num + " ");
        }
    }

    // Sieve of Sundaram for generating prime number
    static void SieveOfSundaram(bool[] marked, int nNew)
    {
        // Main logic of Sundaram. Mark all numbers of the
        // form i + j + 2ij as true where 1 <= i <= j
        for (int i = 1; i <= nNew; i++)
            for (int j = i; (i + j + 2 * i * j) <= nNew; j++)
                marked[i + j + 2 * i * j] = true;
    }

    // Function to find total number of digits
    static int countDigits(int n)
    {
        int digit = 0;
        while ((n /= 10) > 0)
            digit++;
        return digit;
    }

    // Rotate function to right rotate the number
    static int Rotate(int n)
    {
        // find unit place number
        int rem = n % 10;

        // to put unit place
        rem *= (int)Math.Pow(10, countDigits(n));

        // number as first digit.
        n /= 10; // remove unit digit
        n += rem; // add first digit to rest
        return n;
    }

    // Driver code
    public static void Main()
    {
        int n = 100;
        circularPrime(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print primes smaller than
// n using Sieve of Sundaram.

// Print all circular primes
function circularPrime($n)
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a number
    // given number x. Since we want primes smaller
    // than n, we reduce n to half
    $nNew = (int)(($n - 2) / 2);

    // This array is used to separate numbers of
    // the form i+j+2ij from others where 1 <= i <= j
    $marked = array_fill(0, $nNew + 1, false);

    SieveOfSundaram($marked, $nNew);

    // if n > 2 then 2 is also a circular prime
    print("2 ");

    // According to Sieve of sundaram If marked[i]
    // is false then 2*i + 1 is a prime number.

    // loop to check all prime numbers
    // and their rotations
    for ($i = 1; $i <= $nNew; $i++)
    {
        // Skip this number if not prime
        if ($marked[$i] == true)
            continue;

        $num = 2 * $i + 1;
        $num = Rotate($num); // function for rotation of prime

        // now we check for rotations of this
        // prime number if new rotation is prime
        // check next rotation, till new rotation
        // becomes the actual prime number and if
        // new rotation if not prime then break
        while ($num != 2 * $i + 1)
        {
            if ($num % 2 == 0) // check for even
                break;

            // if rotated number is prime then
            // rotate for next
            if ($marked[(int)(($num - 1) / 2)] == false)
                $num = Rotate($num);
            else
                break;
        }

        // if checked number is circular
        // prime print it
        if ($num == (2 * $i + 1))
            print($num." ");
    }
}

// Sieve of Sundaram for generating prime number
function SieveOfSundaram(&$marked, $nNew)
{
    // Main logic of Sundaram. Mark all numbers of the
    // form i + j + 2ij as true where 1 <= i <= j
    for ($i = 1; $i <= $nNew; $i++)
        for ($j = $i;
            ($i + $j + 2 * $i * $j) <= $nNew; $j++)
            $marked[$i + $j + 2 * $i * $j] = true;
}

// Rotate function to right rotate the number
function Rotate($n)
{
    $rem = $n % 10; // find unit place number
    $rem *= pow(10, countDigits($n)); // to put unit place
    // number as first digit.
    $n = (int)($n / 10); // remove unit digit
    $n += $rem; // add first digit to rest
    return $n;
}

// Function to find total number of digits
function countDigits($n)
{
    $digit = 0;
    $n = (int)($n / 10);
    while ($n)
    {
        $digit++;
        $n = (int)($n / 10);
    }
    return $digit;
}

// Driver Code
$n = 100;
circularPrime($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print
// primes smaller
// than n using Sieve of Sundaram.
// Print all circular primes
function circularPrime(n)
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // number given number x.Since we want
    // primes smaller than n, we reduce n to half
    var nNew = (n - 2) / 2;

    // This array is used to
    // separate numbers of the
    // form i+j+2ij from others
    // where 1 <= i <= j
    marked = Array.from({length: nNew + 1},
            (_, i) => false);

    SieveOfSundaram(marked, nNew);

    // if n > 2 then 2 is also a circular prime
    document.write("2 ");

    // According to Sieve of sundaram
    // If marked[i] is false
    // then 2*i + 1 is a prime number.

    // loop to check all prime numbers
    // and their rotations
    for (i = 1; i <= nNew; i++) {
        // Skip this number if not prime
        if (marked[i] == true)
            continue;

        var num = 2 * i + 1;
        // function for rotation of prime
        num = Rotate(num);

        // now we check for rotations of
        // this prime number
        // if new rotation is prime check
        // next rotation,
        // till new rotation becomes
        // the actual prime number
        // and if new rotation if
        // not prime then break
        while (num != 2 * i + 1) {
            if (num % 2 == 0) // check for even
                break;

            // if rotated number is prime then rotate
            // for next
            if (marked[parseInt((num - 1) / 2)] == false)
                num = Rotate(num);
            else
                break;
        }

        // if checked number is circular prime print it
        if (num == (2 * i + 1))
            document.write(num + " ");
        }
}

// Sieve of Sundaram for generating prime number
function SieveOfSundaram(marked , nNew)
{
    // Main logic of Sundaram. Mark all numbers of the
// form i + j + 2ij as true where 1 <= i <= j
    for (i = 1; i <= nNew; i++)
        for (j = i; (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;
}

// Function to find total number of digits
function countDigits(n)
{
    var digit = 0;
    while ((n = parseInt(n/10)) > 0)
        digit++;
    return digit;
}

// Rotate function to right rotate the number
function Rotate(n)
{
    // find unit place number
    var rem = n % 10;
    // to put unit place
    rem *= Math.pow(10, countDigits(n));
    // number as first digit.
    n = parseInt(n/10) // remove unit digit
    n += rem; // add first digit to rest
        return n;
}

// Driver code
var n = 100;
circularPrime(n);

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
2 3 5 7 11 13 17 31 37 71 73 79 97
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。