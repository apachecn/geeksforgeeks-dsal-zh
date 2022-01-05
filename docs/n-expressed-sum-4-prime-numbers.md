# N 表示为 4 个素数之和

> 原文:[https://www . geesforgeks . org/n-expressed-sum-4-质数/](https://www.geeksforgeeks.org/n-expressed-sum-4-prime-numbers/)

将一个给定的数表示为 4 个正素数的和。如果无法表达，则打印“-1”。

**示例:**

```
Input: 24
Output: 3 11 3 7  
Explanation : 3+11+3+7 = 24 and 3, 11, 7 are all prime. 

Input: 46
Output: 11 11 17 7 
explanation : 11+11+17+7 = 46 and 11, 7, 17 are all prime.
```

**逼近:**每一个大于 2 的偶数都可以用 [**哥德巴赫猜想**](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/) 表示为两个数之和。
下面是一些将一个数表示为 4 个素数之和的事实。

*   数字必须大于或等于 8，因为 2 是最小的素数
*   如果给定的数是偶数，我们可以把它分解为(2 + 2) + x，这样 x 保持偶数，可以分解成两个素数。
*   如果给定的数是奇数，我们可以把它分解为(2 + 3) + x，这样 x 保持偶数，可以分解成两个素数。

现在我们可以很容易地用 [**链接**](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/) 将 n 表示为两个素数之和

## C++

```
// CPP program to express n as sum of 4 primes.
#include <bits/stdc++.h>
using namespace std;

// function to check if a number is prime or not
int isPrime(int x)
{
    // does square root of the number
    int s = sqrt(x);

    // traverse from 2 to sqrt(n)
    for (int i = 2; i <= s; i++)

        // if any divisor found then non prime
        if (x % i == 0)
            return 0;

    // if no divisor is found then it is a prime
    return 1;
}

void Num(int x, int& a, int& b)
{
    // iterates to check prime or not
    for (int i = 2; i <= x / 2; i++) {

        // calls function to check if i and x-i
        // is prime or not
        if (isPrime(i) && isPrime(x - i)) {

            a = i;
            b = x - i;

            // if two prime numbers are found,
            // then return
            return;
        }
    }
}

// function to generate 4 prime numbers adding upto n
void generate(int n)
{
    // if n<=7 then 4 numbers cannot sum to
    // get that number
    if (n <= 7)
        cout << "Impossible to form" << endl;

    // a and b stores the last two numbers
    int a, b;

    // if it is not even then 2 and 3 are first
    // two of sequence
    if (n % 2 != 0) {

        // calls the function to get the other
        // two prime numbers considering first two
        // primes as 2 and 3 (Note 2 + 3 = 5)
        Num(n - 5, a, b);

        // print 2 and 3 as the firsts two prime
        // and a and b as the last two.
        cout << "2 3 " << a << " " << b << endl;
    }

    // if it is even then 2 and 2 are first two
    // of sequence
    else {

        /// calls the function to get the other
        // two prime numbers considering first two
        // primes as 2 and 2 (Note 2 + 2 = 4)
        Num(n - 4, a, b);

        // print 2 and 2 as the firsts two prime
        // and a and b as the last two.
        cout << "2 2 " << a << " " << b << endl;
    }
}

// driver program to test the above function
int main()
{
    int n = 28;
    generate(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to express n as sum of
// 4 primes.
class GFG {

    static int a = 0, b = 0;

    // function to check if a number
    // is prime or not
    static int isPrime(int x)
    {

        // does square root of the
        // number
        int s = (int)Math.sqrt(x);

        // traverse from 2 to sqrt(n)
        for (int i = 2; i <= s; i++)

            // if any divisor found
            // then non prime
            if (x % i == 0)
                return 0;

        // if no divisor is found
        // then it is a prime
        return 1;
    }

    static void Num(int x)
    {

        // iterates to check prime
        // or not
        for (int i = 2; i <= x / 2; i++) {

            // calls function to check
            // if i and x-i is prime
            // or not
            if (isPrime(i) != 0 && isPrime(x - i) != 0) {

                a = i;
                b = x - i;

                // if two prime numbers
                // are found, then return
                return;
            }
        }
    }

    // function to generate 4 prime
    // numbers adding upto n
    static void generate(int n)
    {

        // if n<=7 then 4 numbers cannot
        // sum to get that number
        if (n <= 7)
            System.out.println("Impossible"
                               + " to form");

        // if it is not even then 2 and 3
        // are first two of sequence
        if (n % 2 != 0) {

            // calls the function to get the
            // other two prime numbers
            // considering first two primes
            // as 2 and 3 (Note 2 + 3 = 5)
            Num(n - 5);

            // print 2 and 3 as the firsts
            // two prime and a and b as the
            // last two.
            System.out.println("2 3 " + a + " " + b);
        }

        // if it is even then 2 and 2 are
        // first two of sequence
        else {

            /// calls the function to get the
            // other two prime numbers
            // considering first two primes as
            // 2 and 2 (Note 2 + 2 = 4)
            Num(n - 4);

            // print 2 and 2 as the firsts
            // two prime and a and b as the
            // last two.
            System.out.println("2 2 " + a + " " + b);
        }
    }

    // Driver function to test the above
    // function
    public static void main(String[] args)
    {
        int n = 28;

        generate(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to express
# n as sum of 4 primes.
import math;
# function to check if a
# number is prime or not
def isPrime(x):
    # does square root
    # of the number
    s = int(math.sqrt(x))

    # traverse from 2 to sqrt(n)
    for i in range(2,s+1):
        # if any divisor found
        # then non prime
        if (x % i == 0):
            return 0
    # if no divisor is found
    # then it is a prime
    return 1

def Num(x):
    # iterates to check
    # prime or not
    ab=[0]*2
    for i in range(2,int(x / 2)+1):
        # calls function to check
        # if i and x-i is prime
        # or not
        if (isPrime(i) != 0 and isPrime(x - i) != 0):
            ab[0] = i
            ab[1] = x - i
            # if two prime numbers
            # are found, then return
            return ab

# function to generate 4 prime
# numbers adding upto n
def generate(n):
    # if n<=7 then 4 numbers cannot
    # sum to get that number
    if(n <= 7):
        print("Impossible to form")

    # if it is not even then 2 and
    # 3 are first two of sequence

    if (n % 2 != 0):
        # calls the function to get
        # the other two prime numbers
        # considering first two primes
        # as 2 and 3 (Note 2 + 3 = 5)
        ab=Num(n - 5)

        # print 2 and 3 as the firsts
        # two prime and a and b as the
        # last two.
        print("2 3",ab[0],ab[1])

        # if it is even then 2 and 2 are
        # first two of sequence
    else:
        # calls the function to get
        # the other two prime numbers
        # considering first two primes
        # as 2 and 2 (Note 2 + 2 = 4)
        ab=Num(n - 4)

        # print 2 and 2 as the firsts
        # two prime and a and b as the
        # last two.
        print("2 2",ab[0],ab[1])

# Driver Code
if __name__=='__main__':
    n = 28
    generate(n)

# This code is contributed by mits.
```

## C#

```
// C# program to express n as sum of
// 4 primes.
using System;

class GFG {

    static int a = 0, b = 0;

    // function to check if a number
    // is prime or not
    static int isPrime(int x)
    {

        // does square root of the
        // number
        int s = (int)Math.Sqrt(x);

        // traverse from 2 to sqrt(n)
        for (int i = 2; i <= s; i++)

            // if any divisor found
            // then non prime
            if (x % i == 0)
                return 0;

        // if no divisor is found
        // then it is a prime
        return 1;
    }

    static void Num(int x)
    {

        // iterates to check prime
        // or not
        for (int i = 2; i <= x / 2; i++)
        {

            // calls function to check
            // if i and x-i is prime
            // or not
            if (isPrime(i) != 0 &&
                     isPrime(x - i) != 0)
            {

                a = i;
                b = x - i;

                // if two prime numbers
                // are found, then return
                return;
            }
        }
    }

    // function to generate 4 prime
    // numbers adding upto n
    static void generate(int n)
    {

        // if n<=7 then 4 numbers cannot
        // sum to get that number
        if (n <= 7)
            Console.Write("Impossible"
                        + " to form");

        // if it is not even then 2 and
        // 3 are first two of sequence
        if (n % 2 != 0) {

            // calls the function to get
            // the other two prime numbers
            // considering first two primes
            // as 2 and 3 (Note 2 + 3 = 5)
            Num(n - 5);

            // print 2 and 3 as the firsts
            // two prime and a and b as the
            // last two.
            Console.Write("2 3 " + a + " "
                                      + b);
        }

        // if it is even then 2 and 2 are
        // first two of sequence
        else {

            /// calls the function to get
            // the other two prime numbers
            // considering first two primes
            // as 2 and 2 (Note 2 + 2 = 4)
            Num(n - 4);

            // print 2 and 2 as the firsts
            // two prime and a and b as the
            // last two.
            Console.Write("2 2 " + a + " "
                                      + b);
        }
    }

    // Driver function to test the above
    // function
    public static void Main()
    {
        int n = 28;

        generate(n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to express
// n as sum of 4 primes.
$a = 0;
$b = 0;

// function to check if a
// number is prime or not
function isPrime($x)
{

// does square root
// of the number
$s = (int)(sqrt($x));

// traverse from 2 to sqrt(n)
for ($i = 2; $i <= $s; $i++)

// if any divisor found
// then non prime
if ($x % $i == 0)
return 0;

// if no divisor is found
// then it is a prime
return 1;
}

function Num($x)
{
global $a;
global $b;

// iterates to check
// prime or not
for ($i = 2;
     $i <= (int)($x / 2); $i++)
{

// calls function to check
// if i and x-i is prime
// or not
if (isPrime($i) != 0 &&
    isPrime($x - $i) != 0)
    {
    $a = $i;
    $b = $x - $i;

    // if two prime numbers
    // are found, then return
    return;
    }
}
}

// function to generate 4 prime
// numbers adding upto n
function generate($n)
{
global $a;
global $b;

// if n<=7 then 4 numbers cannot
// sum to get that number
if ($n <= 7)
    echo "Impossible to form";

// if it is not even then 2 and
// 3 are first two of sequence
if ($n % 2 != 0)
{
    // calls the function to get
    // the other two prime numbers
    // considering first two primes
    // as 2 and 3 (Note 2 + 3 = 5)
    Num($n - 5);

    // print 2 and 3 as the firsts
    // two prime and a and b as the
    // last two.
    echo "2 3 $a $b";
}

// if it is even then 2 and 2 are
// first two of sequence
else
{
    // calls the function to get
    // the other two prime numbers
    // considering first two primes
    // as 2 and 2 (Note 2 + 2 = 4)
    Num($n - 4);

    // print 2 and 2 as the firsts
    // two prime and a and b as the
    // last two.
    echo "2 2 $a $b";    
}
}

// Driver Code
$n = 28;
generate($n);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// JavaScript program to express n as sum of
// 4 primes.

    let a = 0, b = 0;

    // function to check if a number
    // is prime or not
    function isPrime(x)
    {

        // does square root of the
        // number
        let s = Math.sqrt(x);

        // traverse from 2 to sqrt(n)
        for (let i = 2; i <= s; i++)

            // if any divisor found
            // then non prime
            if (x % i == 0)
                return 0;

        // if no divisor is found
        // then it is a prime
        return 1;
    }

    function Num(x)
    {

        // iterates to check prime
        // or not
        for (let i = 2; i <= x / 2; i++) {

            // calls function to check
            // if i and x-i is prime
            // or not
            if (isPrime(i) != 0 && isPrime(x - i) != 0) {

                a = i;
                b = x - i;

                // if two prime numbers
                // are found, then return
                return;
            }
        }
    }

    // function to generate 4 prime
    // numbers adding upto n
    function generate(n)
    {

        // if n<=7 then 4 numbers cannot
        // sum to get that number
        if (n <= 7)
            document.write("Impossible"
                               + " to form");

        // if it is not even then 2 and 3
        // are first two of sequence
        if (n % 2 != 0) {

            // calls the function to get the
            // other two prime numbers
            // considering first two primes
            // as 2 and 3 (Note 2 + 3 = 5)
            Num(n - 5);

            // print 2 and 3 as the firsts
            // two prime and a and b as the
            // last two.
            document.write("2 3 " + a + " " + b);
        }

        // if it is even then 2 and 2 are
        // first two of sequence
        else {

            /// calls the function to get the
            // other two prime numbers
            // considering first two primes as
            // 2 and 2 (Note 2 + 2 = 4)
            Num(n - 4);

            // print 2 and 2 as the firsts
            // two prime and a and b as the
            // last two.
            document.write("2 2 " + a + " " + b);
        }
    }

// Driver Code

    let n = 28;

    generate(n);

</script>
```

**输出:**

```
2 2 5 19
```

**时间复杂度:** O(n sqrt(n))
**辅助空间:** O(1)

本文由 [**Raja Vikramaditya**](https://www.facebook.com/raja.vikramaditya.7) 投稿，如果你喜欢 GeeksforGeeks 并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章，或者将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。