# 素数点(将一个数分成两个素数的点)

> 原文:[https://www . geeksforgeeks . org/prime-points-将一个数拆分为两个素数的点/](https://www.geeksforgeeks.org/prime-points-points-that-split-a-number-into-two-primes/)

给定一个 n 位数。素数点是左右边数字
为素数的数字的索引。打印数字的所有素数。如果不存在素数点，打印-1。

**示例:**

```
Input : 2317
Output : 1 2
Explanation : Left and right side numbers of index 
              point 1 are 2 and 17 respectively and
              both are primes. Left and right side 
              numbers of index point 2 are 23 and 7 
              respectively and both are prime. 

Input : 2418
Output : -1
Explanation : No index point has both the left 
              and right side numbers as prime.

Note: First and last index can never be a prime 
      point as they do not have left and right 
      side numbers pair.
```

**算法**

```
   Count number of digits of the given number, n.
   If count == 1 || count == 2
       print "Not Possible"      
   Else 
   {
      For index points = 1 to (count - 1)
      {
         Calculate left number(L) and right number(R)
             If both L and R are prime
             print index point i
      }
   }

How to find L and R for an index point 'i'?
   L = n / (10(count-i))
   R = n % (10(count-i-1))
```

素数检查基于[优化的学校方法](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)

## C++

```
// C++ program to print all prime points
#include <bits/stdc++.h>
using namespace std;

// Function to count number of digits
int countDigits(int n)
{
    int count = 0;
    while (n > 0)
    {
        count++;
        n = n/10;
    }
    return count;
}

// Function to check whether a number is
// prime or not. Returns 0 if prime else -1
int checkPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return -1;
    if (n <= 3)
        return 0;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0)
        return -1;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
            return -1;

    return 0;
}

// Function to print prime points
void printPrimePoints(int n)
{
    // counting digits
    int count = countDigits(n);

    // As single and double digit numbers do not
    // have left and right number pairs
    if (count==1 || count==2)
    {
        cout << "-1";
        return;
    }

    // Finding all left and right pairs. Printing
    // the prime points accordingly. Discarding
    // first and last index point
    bool found = false;
    for (int i=1; i<(count-1); i++)
    {
        // Calculating left number
        int left = n / ((int)pow(10,count-i));

        // Calculating right number
        int right = n % ((int)pow(10,count-i-1));

        // Prime point condition
        if (checkPrime(left) == 0 &&
            checkPrime(right) == 0)
        {
            cout << i << " ";
            found = true;
        }
    }

    // No prime point found
    if (found == false)
        cout << "-1";
}

// Driver Program
int main()
{
    int n = 2317;
    printPrimePoints(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// all prime points
import java.io.*;

class GFG
{
// Function to count
// number of digits
static int countDigits(int n)
{
    int count = 0;
    while (n > 0)
    {
        count++;
        n = n / 10;
    }
    return count;
}

// Function to check whether
// a number is prime or not.
// Returns 0 if prime else -1
static int checkPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return -1;
    if (n <= 3)
        return 0;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return -1;

    for (int i = 5;
             i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return -1;

    return 0;
}

// Function to print
// prime points
static void printPrimePoints(int n)
{
    // counting digits
    int count = countDigits(n);

    // As single and double
    // digit numbers do not
    // have left and right
    // number pairs
    if (count == 1 || count == 2)
    {
        System.out.print("-1");
        return;
    }

    // Finding all left and right
    // pairs. Printing the prime
    // points accordingly. Discarding
    // first and last index point
    boolean found = false;
    for (int i = 1; i < (count - 1); i++)
    {
        // Calculating left number
        int left = n / ((int)Math.pow(10,
                                  count - i));

        // Calculating right number
        int right = n % ((int)Math.pow(10,
                                   count - i - 1));

        // Prime point condition
        if (checkPrime(left) == 0 &&
            checkPrime(right) == 0)
        {
                System.out.print(i + " ");
            found = true;
        }
    }

    // No prime point found
    if (found == false)
            System.out.print("-1");
}

// Driver Code
public static void main (String[] args)
{
    int n = 2317;
    printPrimePoints(n);
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# python3 program to print all prime points

# Function to count number of digits
def countDigits(n):
    count = 0
    while (n > 0):
        count+=1
        n = n//10

    return count

#Function to check whether a number is
# prime or not. Returns 0 if prime else -1
def checkPrime(n):
    # Corner cases
    if (n <= 1):
        return -1
    if (n <= 3):
        return 0

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n%2 == 0 or n%3 == 0):
        return -1

    i=5
    while i*i<=n:
        if (n%i == 0 or n%(i+2) == 0):
            return -1
        i+=6

    return 0

# Function to print prime points
def printPrimePoints(n):

    # counting digits
    count = countDigits(n)

    # As single and double digit numbers do not
    # have left and right number pairs
    if (count==1 or count==2):

        print ("-1")
        return

    # Finding all left and right pairs. Printing
    # the prime points accordingly. Discarding
    # first and last index point
    found = False
    for i in range(1,(count-1)):
        #Calculating left number
        left = n //(pow(10,count-i))

        #Calculating right number
        right = n % (pow(10,count-i-1))

        # Prime point condition
        if (checkPrime(left) == 0 and
            checkPrime(right) == 0):

            print (i ,end=" ")
            found = True

    # No prime point found
    if (found == False):
        print ("-1")

# Driver Program
if __name__ == "__main__":

    n = 2317
    printPrimePoints(n)

```

## C#

```
// C# program to print
// all prime points
using System;

class GFG
{

// Function to count
// number of digits
static int countDigits(int n)
{
    int count = 0;
    while (n > 0)
    {
        count++;
        n = n / 10;
    }
    return count;
}

// Function to check whether
// a number is prime or not.
// Returns 0 if prime else -1
static int checkPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return -1;
    if (n <= 3)
        return 0;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if (n % 2 == 0 ||
        n % 3 == 0)
        return -1;

    for (int i = 5;
             i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return -1;

    return 0;
}

// Function to print
// prime points
static void printPrimePoints(int n)
{
    // counting digits
    int count = countDigits(n);

    // As single and double
    // digit numbers do not
    // have left and right
    // number pairs
    if (count == 1 ||
        count == 2)
    {
        Console.Write("-1");
        return;
    }

    // Finding all left and right
    // pairs. Printing the prime
    // points accordingly. Discarding
    // first and last index point
    bool found = false;
    for (int i = 1;
             i < (count - 1); i++)
    {
        // Calculating left number
        int left = n / ((int)Math.Pow(10,
                             count - i));

        // Calculating right number
        int right = n % ((int)Math.Pow(10,
                              count - i - 1));

        // Prime point condition
        if (checkPrime(left) == 0 &&
            checkPrime(right) == 0)
        {
            Console.Write(i + " ");
            found = true;
        }
    }

    // No prime point found
    if (found == false)
            Console.Write("-1");
}

// Driver Code
static public void Main ()
{
    int n = 2317;
    printPrimePoints(n);
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all prime points

// Function to count number of digits
function countDigits($n)
{
    $count = 0;
    while ($n > 0)
    {
        $count++;
        $n = (int)($n / 10);
    }
    return $count;
}

// Function to check whether a
// number is prime or not.
// Returns 0 if prime else -1
function checkPrime($n)
{
    // Corner cases
    if ($n <= 1)
        return -1;
    if ($n <= 3)
        return 0;

    // This is checked so that we
    // can skip middle five numbers
    // in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return -1;

    for ($i = 5; $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
            return -1;

    return 0;
}

// Function to print prime points
function printPrimePoints($n)
{
    // counting digits
    $count = countDigits($n);

    // As single and double digit
    // numbers do not have left
    // and right number pairs
    if ($count == 1 || $count == 2)
    {
        echo "-1";
        return;
    }

    // Finding all left and right pairs.
    // Printing the prime points accordingly. 
    // Discarding first and last index point
    $found = false;
    for ($i = 1; $i < ($count - 1); $i++)
    {
        // Calculating left number
        $left = (int)($n /
               ((int)pow(10, $count - $i)));

        // Calculating right number
        $right = $n % ((int)pow(10, $count - $i - 1));

        // Prime point condition
        if (checkPrime($left) == 0 &&
            checkPrime($right) == 0)
        {
            echo $i , " ";
            $found = true;
        }
    }

    // No prime point found
    if ($found == false)
        echo "-1";
}

// Driver Code
$n = 2317;
printPrimePoints($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to print
// all prime points

// Function to count
// number of digits
function countDigits(n)
{
    let count = 0;

    while (n > 0)
    {
        count++;
        n = Math.floor(n / 10);
    }
    return count;
}

// Function to check whether
// a number is prime or not.
// Returns 0 if prime else -1
function checkPrime(n)
{

    // Corner cases
    if (n <= 1)
        return -1;
    if (n <= 3)
        return 0;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return -1;

    for(let i = 5;
            i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return -1;

    return 0;
}

// Function to print
// prime points
function printPrimePoints(n)
{

    // Counting digits
    let count = countDigits(n);

    // As single and double
    // digit numbers do not
    // have left and right
    // number pairs
    if (count == 1 || count == 2)
    {
        document.write("-1");
        return;
    }

    // Finding all left and right
    // pairs. Printing the prime
    // points accordingly. Discarding
    // first and last index point
    let found = false;
    for(let i = 1; i < (count - 1); i++)
    {

        // Calculating left number
        let left = Math.floor(
            n / (Math.pow(10, count - i)));

        // Calculating right number
        let right = n % (Math.pow(
            10, count - i - 1));

        // Prime point condition
        if (checkPrime(left) == 0 &&
            checkPrime(right) == 0)
        {
            document.write(i + " ");
            found = true;
        }
    }

    // No prime point found
    if (found == false)
        document.write("-1");
}

// Driver Code
let n = 2317;

printPrimePoints(n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
1 2
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。