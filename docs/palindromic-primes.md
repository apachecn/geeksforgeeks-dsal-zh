# 回文素数

> 原文:[https://www.geeksforgeeks.org/palindromic-primes/](https://www.geeksforgeeks.org/palindromic-primes/)

一个**回文素数**(有时称为一个**触须**)是一个素数，也是一个回文数。
给定一个数字 n，打印所有小于或等于 n 的回文素数，例如 n 为 10，输出应为“2，3，5，7′。如果 n 是 20，输出应该是“2，3，5，7，11”。
思路是生成所有小于等于给定数 n 的素数，并检查每个素数是否回文。
**使用的方法**

*   寻找给定的数是否是质数- [埃拉托斯特尼筛方法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   检查给定号码是否为回文号码:[检查回文的递归函数](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)

以下是上述算法的实现:

## C++

```
// C++ Program to print all palindromic primes
// smaller than or equal to n.
#include<bits/stdc++.h>
using namespace std;

// A function that returns true only if num
// contains one digit
int oneDigit(int num)
{
    // comparison operation is faster than
    // division operation. So using following
    // instead of "return num / 10 == 0;"
    return (num >= 0 && num < 10);
}

// A recursive function to find out whether
// num is palindrome or not. Initially, dupNum
// contains address of a copy of num.
bool isPalUtil(int num, int* dupNum)
{
    // Base case (needed for recursion termination):
    // This statement/ mainly compares the first
    // digit with the last digit
    if (oneDigit(num))
        return (num == (*dupNum) % 10);

    // This is the key line in this method. Note
    // that all recursive/ calls have a separate
    // copy of num, but they all share same copy
    // of *dupNum. We divide num while moving up
    // the recursion tree
    if (!isPalUtil(num/10, dupNum))
        return false;

    // The following statements are executed when
    // we move up the recursion call tree
    *dupNum /= 10;

    // At this point, if num%10 contains i'th
    // digit from beginning, then (*dupNum)%10
    // contains i'th digit from end
    return (num % 10 == (*dupNum) % 10);
}

// The main function that uses recursive function
// isPalUtil() to find out whether num is palindrome
// or not
int isPal(int num)
{
    // If num is negative, make it positive
    if (num < 0)
       num = -num;

    // Create a separate copy of num, so that
    // modifications made to address dupNum don't
    // change the input number.
    int *dupNum = new int(num); // *dupNum = num

    return isPalUtil(num, dupNum);
}

// Function to generate all primes and checking
// whether number is palindromic or not
void printPalPrimesLessThanN(int n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    bool prime[n+1];
    memset(prime, true, sizeof(prime));

    for (int p=2; p*p<=n; p++)
    {
        // If prime[p] is not changed, then it is
        // a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i=p*2; i<=n; i += p)
                prime[i] = false;
        }
    }

    // Print all palindromic prime numbers
    for (int p=2; p<=n; p++)

       // checking whether the given number is
       // prime palindromic or not
       if (prime[p] && isPal(p))
          cout << p << " ";
}

// Driver Program
int main()
{
    int n = 100;
    printf("Palindromic primes smaller than or "
           "equal to %d are :\n", n);
    printPalPrimesLessThanN(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print all palindromic primes
// smaller than or equal to n.
import java.util.*;

class GFG {

    // A function that returns true only if num
    // contains one digit
    static boolean oneDigit(int num)
    {
        // comparison operation is faster than
        // division operation. So using following
        // instead of "return num / 10 == 0;"
        return (num >= 0 && num < 10);
    }

    // A recursive function to find out whether
    // num is palindrome or not. Initially, dupNum
    // contains address of a copy of num.
    static boolean isPalUtil(int num, int dupNum)
    {
        // Base case (needed for recursion termination):
        // This statement/ mainly compares the first
        // digit with the last digit
        if (oneDigit(num))
            return (num == (dupNum) % 10);

        // This is the key line in this method. Note
        // that all recursive/ calls have a separate
        // copy of num, but they all share same copy
        // of dupNum. We divide num while moving up
        // the recursion tree
        if (!isPalUtil(num/10, dupNum))
            return false;

        // The following statements are executed when
        // we move up the recursion call tree
        dupNum /= 10;

        // At this point, if num%10 contains ith
        // digit from beginning, then (dupNum)%10
        // contains ith digit from end
        return (num % 10 == (dupNum) % 10);
    }

    // The main function that uses recursive function
    // isPalUtil() to find out whether num is palindrome
    // or not
    static boolean isPal(int num)
    {
        // If num is negative, make it positive
        if (num < 0)
           num = -num;

        // Create a separate copy of num, so that
        // modifications made to address dupNum don't
        // change the input number.
        int dupNum = num; // dupNum = num

        return isPalUtil(num, dupNum);
    }

    // Function to generate all primes and checking
    // whether number is palindromic or not
    static void printPalPrimesLessThanN(int n)
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        boolean prime[] = new boolean[n+1];

        Arrays.fill(prime, true);

        for (int p = 2; p*p <= n; p++)
        {
            // If prime[p] is not changed, then it is
            // a prime
            if (prime[p])
            {
                // Update all multiples of p
                for (int i = p*2; i <= n; i += p){
                    prime[i] = false;}
            }
        }

        // Print all palindromic prime numbers
        for (int p = 2; p <= n; p++){

           // checking whether the given number is
           // prime palindromic or not
           if (prime[p] && isPal(p)){
              System.out.print(p + " ");
              }
           }
    }

    // Driver function
    public static void main(String[] args)
    {
         int n = 100;
            System.out.printf("Palindromic primes smaller than or "
                   +"equal to %d are :\n", n);
            printPalPrimesLessThanN(n);
        }
    }

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 Program to print all palindromic
# primes smaller than or equal to n.

# A function that returns true only if
# num contains one digit
def oneDigit(num):

    # comparison operation is faster than
    # division operation. So using following
    # instead of "return num / 10 == 0;"
    return (num >= 0 and num < 10);

# A recursive function to find out whether
# num is palindrome or not. Initially, dupNum
# contains address of a copy of num.
def isPalUtil(num, dupNum):

    # Base case (needed for recursion termination):
    # This statement/ mainly compares the first
    # digit with the last digit
    if (oneDigit(num)):
        return (num == (dupNum) % 10);

    # This is the key line in this method. Note
    # that all recursive/ calls have a separate
    # copy of num, but they all share same copy
    # of dupNum. We divide num while moving up
    # the recursion tree
    if (not isPalUtil(int(num / 10), dupNum)):
        return False;

    # The following statements are executed
    # when we move up the recursion call tree
    dupNum =int(dupNum/10);

    # At this point, if num%10 contains ith
    # digit from beginning, then (dupNum)%10
    # contains ith digit from end
    return (num % 10 == (dupNum) % 10);

# The main function that uses recursive
# function isPalUtil() to find out whether
# num is palindrome or not
def isPal(num):

    # If num is negative, make it positive
    if (num < 0):
        num = -num;

    # Create a separate copy of num, so that
    # modifications made to address dupNum
    # don't change the input number.
    dupNum = num; # dupNum = num

    return isPalUtil(num, dupNum);

# Function to generate all primes and checking
# whether number is palindromic or not
def printPalPrimesLessThanN(n):

    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true. A value
    # in prime[i] will finally be false if i is
    # Not a prime, else true.
    prime = [True] * (n + 1);
    p = 2;
    while (p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                prime[i] = False;
        p += 1;

    # Print all palindromic prime numbers
    for p in range(2, n + 1):

        # checking whether the given number
        # is prime palindromic or not
        if (prime[p] and isPal(p)):
            print(p, end = " ");

# Driver Code
n = 100;
print("Palindromic primes smaller",
      "than or equal to", n, "are :");
printPalPrimesLessThanN(n);

# This code is contributed by chandan_jnu
```

## C#

```
// C# Program to print all palindromic
// primes smaller than or equal to n.
using System;

class GFG {

    // A function that returns true only
    // if num contains one digit
    static bool oneDigit(int num)
    {
        // comparison operation is faster than
        // division operation. So using following
        // instead of "return num / 10 == 0;"
        return (num >= 0 && num < 10);
    }

    // A recursive function to find out whether
    // num is palindrome or not. Initially, dupNum
    // contains address of a copy of num.
    static bool isPalUtil(int num, int dupNum)
    {
        // Base case (needed for recursion termination):
        // This statement/ mainly compares the first
        // digit with the last digit
        if (oneDigit(num))
            return (num == (dupNum) % 10);

        // This is the key line in this method. Note
        // that all recursive/ calls have a separate
        // copy of num, but they all share same copy
        // of dupNum. We divide num while moving up
        // the recursion tree
        if (!isPalUtil(num/10, dupNum))
            return false;

        // The following statements are executed when
        // we move up the recursion call tree
        dupNum /= 10;

        // At this point, if num%10 contains ith
        // digit from beginning, then (dupNum)%10
        // contains ith digit from end
        return (num % 10 == (dupNum) % 10);
    }

    // The main function that uses recursive
    // function isPalUtil() to find out
    // whether num is palindrome or not
    static bool isPal(int num)
    {
        // If num is negative, make it positive
        if (num < 0)
        num = -num;

        // Create a separate copy of num, so that
        // modifications made to address dupNum don't
        // change the input number.
        int dupNum = num; // dupNum = num

        return isPalUtil(num, dupNum);
    }

    // Function to generate all primes and checking
    // whether number is palindromic or not
    static void printPalPrimesLessThanN(int n)
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        bool []prime = new bool[n+1];

    for (int i=0;i<n+1;i++)
    prime[i]=true;

        for (int p = 2; p*p <= n; p++)
        {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {
                // Update all multiples of p
                for (int i = p*2; i <= n; i += p){
                    prime[i] = false;}
            }
        }

        // Print all palindromic prime numbers
        for (int p = 2; p <= n; p++){

        // checking whether the given number is
        // prime palindromic or not
        if (prime[p] && isPal(p)){
            Console.Write(p + " ");
            }
        }
    }

    // Driver function
    public static void Main()
    {
        int n = 100;
        Console.Write("Palindromic primes smaller than or " +
                      "equal to are :\n", n);
        printPalPrimesLessThanN(n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print all palindromic
// primes smaller than or equal to n.

// A function that returns true only
// if num contains one digit
function oneDigit($num)
{
    // comparison operation is faster than
    // division operation. So using following
    // instead of "return num / 10 == 0;"
    return ($num >= 0 && $num < 10);
}

// A recursive function to find out whether
// num is palindrome or not. Initially,
// dupNum contains address of a copy of num.
function isPalUtil($num, $dupNum)
{
    // Base case (needed for recursion termination):
    // This statement/ mainly compares the first
    // digit with the last digit
    if (oneDigit($num))
        return ($num == ($dupNum) % 10);

    // This is the key line in this method. Note
    // that all recursive/ calls have a separate
    // copy of num, but they all share same copy
    // of dupNum. We divide num while moving up
    // the recursion tree
    if (!isPalUtil((int)($num/10), $dupNum))
        return false;

    // The following statements are executed 
    // when we move up the recursion call tree
    $dupNum = (int)($dupNum / 10);

    // At this point, if num%10 contains ith
    // digit from beginning, then (dupNum)%10
    // contains ith digit from end
    return ($num % 10 == ($dupNum) % 10);
}

// The main function that uses recursive
// function isPalUtil() to find out whether
// num is palindrome or not
function isPal($num)
{
    // If num is negative, make it positive
    if ($num < 0)
    $num = -$num;

    // Create a separate copy of num, so that
    // modifications made to address dupNum
    // don't change the input number.
    $dupNum = $num; // dupNum = num

    return isPalUtil($num, $dupNum);
}

// Function to generate all primes and checking
// whether number is palindromic or not
function printPalPrimesLessThanN($n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    $prime = array_fill(0, $n + 1, true);

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p])
        {
            // Update all multiples of p
            for ($i = $p * 2; $i <= $n; $i += $p)
            {
                $prime[$i] = false;
            }
        }
    }

    // Print all palindromic prime numbers
    for ($p = 2; $p <= $n; $p++)
    {

    // checking whether the given number 
    // is prime palindromic or not
    if ($prime[$p] && isPal($p))
    {
        print($p . " ");
    }
    }
}

// Driver Code
$n = 100;
print("Palindromic primes smaller " .
      "than or equal to ".$n." are :\n");
printPalPrimesLessThanN($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript Program to print all palindromic primes
// smaller than or equal to n.

    // A function that returns true only if num
    // contains one digit
    function oneDigit(num)
    {
        // comparison operation is faster than
        // division operation. So using following
        // instead of "return num / 10 == 0;"
        return (num >= 0 && num < 10);
    }

    // A recursive function to find out whether
    // num is palindrome or not. Initially, dupNum
    // contains address of a copy of num.
    function isPalUtil(num , dupNum)
    {
        // Base case (needed for recursion termination):
        // This statement/ mainly compares the first
        // digit with the last digit
        if (oneDigit(num))
            return (num == (dupNum) % 10);

        // This is the key line in this method. Note
        // that all recursive/ calls have a separate
        // copy of num, but they all share same copy
        // of dupNum. We divide num while moving up
        // the recursion tree
        if (!isPalUtil(parseInt(num/10), dupNum))
            return false;

        // The following statements are executed when
        // we move up the recursion call tree
        dupNum = parseInt(dupNum/10);

        // At this point, if num%10 contains ith
        // digit from beginning, then (dupNum)%10
        // contains ith digit from end
        return (num % 10 == (dupNum) % 10);
    }

    // The main function that uses recursive function
    // isPalUtil() to find out whether num is palindrome
    // or not
    function isPal(num)
    {
        // If num is negative, make it positive
        if (num < 0)
           num = -num;

        // Create a separate copy of num, so that
        // modifications made to address dupNum don't
        // change the input number.
        var dupNum = num; // dupNum = num

        return isPalUtil(num, dupNum);
    }

    // Function to generate all primes and checking
    // whether number is palindromic or not
    function printPalPrimesLessThanN(n)
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        var prime = Array.from({length: n+1}, (_, i) => true);

        for (p = 2; p*p <= n; p++)
        {
            // If prime[p] is not changed, then it is
            // a prime
            if (prime[p])
            {
                // Update all multiples of p
                for (i = p*2; i <= n; i += p){
                    prime[i] = false;}
            }
        }

        // Print all palindromic prime numbers
        for (p = 2; p <= n; p++){

           // checking whether the given number is
           // prime palindromic or not
           if (prime[p] && isPal(p)){
              document.write(p + " ");
              }
           }
    }

    // Driver function
    var n = 100;
    document.write('Palindromic primes smaller than or equal to '+n+' are :<br>');
    printPalPrimesLessThanN(n);

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
Palindromic primes smaller than or equal to 100 are :
2 3 5 7 11 
```

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。