# 史密斯号

> 原文:[https://www.geeksforgeeks.org/smith-number/](https://www.geeksforgeeks.org/smith-number/)

给定一个数字 n，任务是找出这个数字是否是史密斯。史密斯数是一个复合数，其位数之和等于其素分解中的位数之和。
**例:**

```
Input  : n = 4
Output : Yes
Prime factorization = 2, 2  and 2 + 2 = 4
Therefore, 4 is a smith number

Input  : n = 6
Output : No
Prime factorization = 2, 3  and 2 + 3 is
not 6\. Therefore, 6 is not a smith number

Input   : n = 666
Output  : Yes
Prime factorization = 2, 3, 3, 37 and
2 + 3 + 3 + (3 + 7) = 6 + 6 + 6 = 18
Therefore, 666 is a smith number

Input   : n = 13
Output  : No
Prime factorization = 13 and 13 = 13,
But 13 is not a smith number as it is not
a composite number

```

这个想法是首先使用 Sundaram 的[筛找到一个极限以下的所有质数(这在我们要为 Smith 检查多个数时特别有用)。现在，对于每一个要检查史密斯的输入，我们检查它的所有质因数，并找到每个质因数的位数总和。我们还可以找到给定数字的位数总和。最后我们比较两个和。如果他们是一样的，我们还真。](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/) 

## C++

```
// C++ program to check whether a number is
// Smith Number or not.
#include<bits/stdc++.h>
using namespace std;
const int MAX  = 10000;

// array to store all prime less than and equal to 10^6
vector <int> primes;

// utility function for sieve of sundaram
void sieveSundaram()
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool marked[MAX/2 + 100] = {0};

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i=1; i<=(sqrt(MAX)-1)/2; i++)
        for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=MAX/2; i++)
        if (marked[i] == false)
            primes.push_back(2*i + 1);
}

// Returns true if n is a Smith number, else false.
bool isSmith(int n)
{
    int original_no = n;

    // Find sum the digits of prime factors of n
    int pDigitSum = 0;
    for (int i = 0; primes[i] <= n/2; i++)
    {
        while (n % primes[i] == 0)
        {
            // If primes[i] is a prime factor,
            // add its digits to pDigitSum.
            int p = primes[i];
            n = n/p;
            while (p > 0)
            {
                pDigitSum += (p % 10);
                p = p/10;
            }
        }
    }

    // If n!=1 then one prime factor still to be
    // summed up;
    if (n != 1 && n != original_no)
    {
        while (n > 0)
        {
            pDigitSum = pDigitSum + n%10;
            n = n/10;
        }
    }

    // All prime factors digits summed up
    // Now sum the original number digits
    int sumDigits = 0;
    while (original_no > 0)
    {
        sumDigits = sumDigits + original_no % 10;
        original_no = original_no/10;
    }

    // If sum of digits in prime factors and sum
    // of digits in original number are same, then
    // return true. Else return false.
    return (pDigitSum == sumDigits);
}

// Driver code
int main()
{
   // Finding all prime numbers before limit. These
   // numbers are used to find prime factors.
   sieveSundaram();

   cout << "Printing first few Smith Numbers"
           " using isSmith()n";
   for (int i=1; i<500; i++)
      if (isSmith(i))
          cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to to check whether a number is
// Smith Number or not.

import java.util.Vector;

class Test
{

    static int MAX  = 10000;

    // array to store all prime less than and equal to 10^6
    static Vector <Integer>  primes = new Vector<>();

    // utility function for sieve of sundaram
    static void sieveSundaram()
    {
        // In general Sieve of Sundaram, produces primes smaller
        // than (2*x + 2) for a number given number x. Since
        // we want primes smaller than MAX, we reduce MAX to half
        // This array is used to separate numbers of the form
        // i+j+2ij from others where 1 <= i <= j
        boolean marked[] = new boolean[MAX/2 + 100];

        // Main logic of Sundaram. Mark all numbers which
        // do not generate prime number by doing 2*i+1
        for (int i=1; i<=(Math.sqrt(MAX)-1)/2; i++)
            for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
                marked[j] = true;

        // Since 2 is a prime number
        primes.addElement(2);

        // Print other primes. Remaining primes are of the
        // form 2*i + 1 such that marked[i] is false.
        for (int i=1; i<=MAX/2; i++)
            if (marked[i] == false)
                primes.addElement(2*i + 1);
    }

    // Returns true if n is a Smith number, else false.
    static boolean isSmith(int n)
    {
        int original_no = n;

        // Find sum the digits of prime factors of n
        int pDigitSum = 0;
        for (int i = 0; primes.get(i) <= n/2; i++)
        {
            while (n % primes.get(i) == 0)
            {
                // If primes[i] is a prime factor,
                // add its digits to pDigitSum.
                int p = primes.get(i);
                n = n/p;
                while (p > 0)
                {
                    pDigitSum += (p % 10);
                    p = p/10;
                }
            }
        }

        // If n!=1 then one prime factor still to be
        // summed up;
        if (n != 1 && n != original_no)
        {
            while (n > 0)
            {
                pDigitSum = pDigitSum + n%10;
                n = n/10;
            }
        }

        // All prime factors digits summed up
        // Now sum the original number digits
        int sumDigits = 0;
        while (original_no > 0)
        {
            sumDigits = sumDigits + original_no % 10;
            original_no = original_no/10;
        }

        // If sum of digits in prime factors and sum
        // of digits in original number are same, then
        // return true. Else return false.
        return (pDigitSum == sumDigits);
    }

    // Driver method
    public static void main(String[] args) 
    {
        // Finding all prime numbers before limit. These
        // numbers are used to find prime factors.
        sieveSundaram();

        System.out.println("Printing first few Smith Numbers" +
                           " using isSmith()");

        for (int i=1; i<500; i++)
           if (isSmith(i))
              System.out.print(i + " ");
    }
}
```

## 计算机编程语言

```
# Python program to to check whether a number is
# Smith Number or not.

import math

MAX  = 10000

# array to store all prime less than and equal to 10^6
primes = []

# utility function for sieve of sundaram
def sieveSundaram ():
    #In general Sieve of Sundaram, produces primes smaller
    # than (2*x + 2) for a number given number x. Since
    # we want primes smaller than MAX, we reduce MAX to half
    # This array is used to separate numbers of the form
    # i+j+2ij from others where 1 <= i <= j
    marked  = [0] * ((MAX/2)+100)
    # Main logic of Sundaram. Mark all numbers which
    # do not generate prime number by doing 2*i+1
    i = 1
    while i <= ((math.sqrt (MAX)-1)/2) :
        j = (i* (i+1)) << 1
        while j <= MAX/2 :
            marked[j] = 1
            j = j+ 2 * i + 1
        i = i + 1
    # Since 2 is a prime number
    primes.append (2)

    # Print other primes. Remaining primes are of the
    # form 2*i + 1 such that marked[i] is false.
    i=1
    while i <= MAX /2 :
        if marked[i] == 0 :
            primes.append( 2* i + 1)
        i=i+1

#Returns true if n is a Smith number, else false.
def isSmith( n) :
    original_no = n

    #Find sum the digits of prime factors of n
    pDigitSum = 0;
    i=0
    while (primes[i] <= n/2 ) :

        while n % primes[i] == 0 :
            #If primes[i] is a prime factor ,
            # add its digits to pDigitSum.
            p = primes[i]
            n = n/p
            while p > 0 :
                pDigitSum += (p % 10)
                p = p/10
        i=i+1
    # If n!=1 then one prime factor still to be
    # summed up
    if not n == 1 and not n == original_no :
        while n > 0 :
            pDigitSum = pDigitSum + n%10
            n=n/10

    # All prime factors digits summed up
    # Now sum the original number digits
    sumDigits = 0
    while original_no > 0 :
        sumDigits = sumDigits + original_no % 10
        original_no = original_no/10

    #If sum of digits in prime factors and sum
    # of digits in original number are same, then
    # return true. Else return false.
    return pDigitSum == sumDigits
#-----end of function isSmith------

#Driver method
# Finding all prime numbers before limit. These
# numbers are used to find prime factors.
sieveSundaram();
print "Printing first few Smith Numbers using isSmith()"
i = 1
while i<500 :
    if isSmith(i) :
        print i,
    i=i+1

#This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to to check whether a number is 
// Smith Number or not. 
using System; 
using System.Collections; 

class Test 
{ 

    static int MAX = 10000; 

    // array to store all prime less than and equal to 10^6 
    static ArrayList primes = new ArrayList(10);

    // utility function for sieve of sundaram 
    static void sieveSundaram() 
    { 
        // In general Sieve of Sundaram, produces primes smaller 
        // than (2*x + 2) for a number given number x. Since 
        // we want primes smaller than MAX, we reduce MAX to half 
        // This array is used to separate numbers of the form 
        // i+j+2ij from others where 1 <= i <= j 
        bool[] marked = new bool[MAX/2 + 100]; 

        // Main logic of Sundaram. Mark all numbers which 
        // do not generate prime number by doing 2*i+1 
        for (int i=1; i<=(Math.Sqrt(MAX)-1)/2; i++) 
            for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1) 
                marked[j] = true; 

        // Since 2 is a prime number 
        primes.Add(2); 

        // Print other primes. Remaining primes are of the 
        // form 2*i + 1 such that marked[i] is false. 
        for (int i=1; i<=MAX/2; i++) 
            if (marked[i] == false) 
                primes.Add(2*i + 1); 
    } 

    // Returns true if n is a Smith number, else false. 
    static bool isSmith(int n) 
    { 
        int original_no = n; 

        // Find sum the digits of prime factors of n 
        int pDigitSum = 0; 
        for (int i = 0; (int)primes[i] <= n/2; i++) 
        { 
            while (n % (int)primes[i] == 0) 
            { 
                // If primes[i] is a prime factor, 
                // add its digits to pDigitSum. 
                int p = (int)primes[i]; 
                n = n/p; 
                while (p > 0) 
                { 
                    pDigitSum += (p % 10); 
                    p = p/10; 
                } 
            } 
        } 

        // If n!=1 then one prime factor still to be 
        // summed up; 
        if (n != 1 && n != original_no) 
        { 
            while (n > 0) 
            { 
                pDigitSum = pDigitSum + n%10; 
                n = n/10; 
            } 
        } 

        // All prime factors digits summed up 
        // Now sum the original number digits 
        int sumDigits = 0; 
        while (original_no > 0) 
        { 
            sumDigits = sumDigits + original_no % 10; 
            original_no = original_no/10; 
        } 

        // If sum of digits in prime factors and sum 
        // of digits in original number are same, then 
        // return true. Else return false. 
        return (pDigitSum == sumDigits); 
    } 

    // Driver method 
    public static void Main() 
    { 
        // Finding all prime numbers before limit. These 
        // numbers are used to find prime factors. 
        sieveSundaram(); 

        Console.WriteLine("Printing first few Smith Numbers" + 
                        " using isSmith()"); 

        for (int i=1; i<500; i++) 
        if (isSmith(i)) 
            Console.Write(i + " "); 
    } 
} 
// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to to check whether a 
// number is Smith Number or not.
$MAX = 10000;

// array to store all prime less
// than and equal to 10^6
$primes = array();

// utility function for sieve of sundaram
function sieveSundaram()
{
    global $MAX, $primes;

    // In general Sieve of Sundaram, produces 
    // primes smaller than (2*x + 2) for a 
    // number given number x. Since we want 
    // primes smaller than MAX, we reduce MAX 
    // to half. This array is used to separate 
    // numbers of the form i+j+2ij from others
    // where 1 <= i <= j
    $marked = array_fill(0, ($MAX / 2 + 100), false);

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for ($i = 1; $i <= (sqrt($MAX) - 1) / 2; $i++)
        for ($j = ($i * ($i + 1)) << 1; 
             $j <= $MAX / 2; $j = $j + 2 * $i + 1)
            $marked[$j] = true;

    // Since 2 is a prime number
    array_push($primes, 2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for ($i = 1; $i <= $MAX / 2; $i++)
        if ($marked[$i] == false)
            array_push($primes, 2 * $i + 1);
}

// Returns true if n is a Smith number, else false.
function isSmith($n)
{
    global $MAX, $primes;
    $original_no = $n;

    // Find sum the digits of prime 
    // factors of n
    $pDigitSum = 0;
    for ($i = 0; $primes[$i] <= $n / 2; $i++)
    {
        while ($n % $primes[$i] == 0)
        {
            // If primes[i] is a prime factor,
            // add its digits to pDigitSum.
            $p = $primes[$i];
            $n = $n / $p;
            while ($p > 0)
            {
                $pDigitSum += ($p % 10);
                $p = $p / 10;
            }
        }
    }

    // If n!=1 then one prime factor still
    // to be summed up;
    if ($n != 1 && $n != $original_no)
    {
        while ($n > 0)
        {
            $pDigitSum = $pDigitSum + $n % 10;
            $n = $n / 10;
        }
    }

    // All prime factors digits summed up
    // Now sum the original number digits
    $sumDigits = 0;
    while ($original_no > 0)
    {
        $sumDigits = $sumDigits + $original_no % 10;
        $original_no = $original_no / 10;
    }

    // If sum of digits in prime factors and sum
    // of digits in original number are same, then
    // return true. Else return false.
    return ($pDigitSum == $sumDigits);
}

// Driver code

// Finding all prime numbers before limit. These
// numbers are used to find prime factors.
sieveSundaram();

echo "Printing first few Smith Numbers" .
                    " using isSmith()\n";
for ($i = 1; $i < 500; $i++)
    if (isSmith($i))
        echo $i . " ";

// This code is contributed by mits
?>
```

**Output:**

```
Printing first few Smith Numbers using isSmith()
4 22 27 58 85 94 121 166 202 265 274 319 346 355 378 382 391 438 454 483 

```

本文由 **Sahil Chhabra(KILLER)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。