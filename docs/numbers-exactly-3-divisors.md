# 正好有 3 个除数的数

> 原文:[https://www.geeksforgeeks.org/numbers-exactly-3-divisors/](https://www.geeksforgeeks.org/numbers-exactly-3-divisors/)

给定一个数 N，打印 1 到 N 范围内正好有 3 个除数的所有数。

**示例:**

```
Input : N = 16
Output : 4 9
4 and 9 have exactly three divisors.
Divisor

Input : N = 49
Output : 4 9 25 49
4, 9, 25 and 49 have exactly three divisors.
```

仔细看了上面提到的例子后，你会注意到所有需要的数字都是完美的正方形，也只有素数。这背后的逻辑是，这样的数只能有三个数作为其除数，并且还包括 1，该数本身只产生一个除数，而不是一个数，因此我们可以很容易地得出结论，需要的是质数平方的数，这样它们只能有三个除数(1，数本身和 sqrt(数))。所以所有的素数 I，比如 i*i 小于等于 N，都是三素数。

**注意:**我们可以使用任何筛选方法高效地生成集合内的所有素数，然后我们应该生成所有素数 I，这样 **i*i < =N** 。

下面是上述方法的实现:

## C++

```
// C++ program to print all
// three-primes smaller than
// or equal to n using Sieve
// of Eratosthenes
#include <bits/stdc++.h>
using namespace std;

// Generates all primes upto n and
// prints their squares
void numbersWith3Divisors(int n)
{
    bool prime[n+1];
    memset(prime, true, sizeof(prime));
    prime[0] = prime[1] = 0;

    for (int p = 2; p*p <= n; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
           // Update all multiples of p
           for (int i = p*2; i <= n; i += p)
              prime[i] = false;
        }
    }

    // print squares of primes upto n.
    cout << "Numbers with 3 divisors :\n";
    for (int i=0;  i*i <= n ; i++)
        if (prime[i])
          cout << i*i << " ";
}

// Driver program
int main()
{
    // sieve();
    int n = 96;
    numbersWith3Divisors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// three-primes smaller than
// or equal to n using Sieve
// of Eratosthenes
import java.io.*;
import java.util.*;

class GFG
{

    // Generates all primes upto n
    // and prints their squares
    static void numbersWith3Divisors(int n)
    {
        boolean[] prime = new boolean[n+1];
        Arrays.fill(prime, true);
        prime[0] = prime[1] = false;

        for (int p = 2; p*p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {
                // Update all multiples of p
                for (int i=p*2; i<=n; i += p)
                    prime[i] = false;
            }
        }

        // print squares of primes upto n
        System.out.println("Numbers with 3 divisors : ");
        for (int i=0;  i*i <= n ; i++)
            if (prime[i])
                System.out.print(i*i + " ");
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 96;
        numbersWith3Divisors(n);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to print
# all three-primes smaller than
# or equal to n using Sieve
# of Eratosthenes

# Generates all primes upto n
# and prints their squares
def numbersWith3Divisors(n):

    prime=[True]*(n+1);
    prime[0] = prime[1] = False;
    p=2;
    while (p*p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p*2,n+1,p):
                prime[i] = False;
        p+=1;

    # print squares of primes upto n.
    print("Numbers with 3 divisors :");
    i=0;
    while (i*i <= n):
        if (prime[i]):
            print(i*i,end=" ");
        i+=1;

# Driver program

n = 96;
numbersWith3Divisors(n);

# This code is contributed by mits
```

## C#

```
// C# program to print all
// three-primes smaller than
// or equal to n using Sieve
// of Eratosthenes

class GFG
{

    // Generates all primes upto n
    // and prints their squares
    static void numbersWith3Divisors(int n)
    {
        bool[] prime = new bool[n+1];
        prime[0] = prime[1] = true;

        for (int p = 2; p*p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == false)
            {
                // Update all multiples of p
                for (int i = p*2; i <= n; i += p)
                    prime[i] = true;
            }
        }

        // print squares of primes upto n
        System.Console.WriteLine("Numbers with 3 divisors : ");
        for (int i=0; i*i <= n ; i++)
            if (!prime[i])
                System.Console.Write(i*i + " ");
    }

    // Driver program
    public static void Main()
    {
        int n = 96;
        numbersWith3Divisors(n);
    }
}

// This code is Contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all three-primes
// smaller than or equal to n using Sieve
// of Eratosthenes

// Generates all primes upto n and
// prints their squares
function numbersWith3Divisors($n)
{
    $prime = array_fill(0, $n + 1, true);
    $prime[0] = $prime[1] = false;

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {
        // Update all multiples of p
        for ($i = $p * 2; $i <= $n; $i += $p)
            $prime[$i] = false;
        }
    }

    // print squares of primes upto n.
    echo "Numbers with 3 divisors :\n";
    for ($i = 0; $i * $i <= $n ; $i++)
        if ($prime[$i])
        echo $i * $i . " ";
}

// Driver Code
$n = 96;
numbersWith3Divisors($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to print all
    // three-primes smaller than
    // or equal to n using Sieve
    // of Eratosthenes

    // Generates all primes upto n and
    // prints their squares
    function numbersWith3Divisors(n)
    {
        let prime = new Array(n+1);
        prime.fill(true);
        prime[0] = prime[1] = 0;

        for (let p = 2; p*p <= n; p++)
        {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {
               // Update all multiples of p
               for (let i = p*2; i <= n; i += p)
                  prime[i] = false;
            }
        }

        // print squares of primes upto n.
        document.write("Numbers with 3 divisors :" + "</br>");
        for (let i = 0;  i*i <= n ; i++)
            if (prime[i])
              document.write(i*i + " ");
    }

    // sieve();
    let n = 96;
    numbersWith3Divisors(n);

     // This code is contributed by mukesh07.
</script>
```

**输出:**

```
Numbers with 3 divisors :
4 9 25 49 
```

**另一种方法:**

要打印从 1 到 N 范围内正好有 3 个除数的所有数字，主要的计算方法是找出那些质数的平方小于或等于该数的数字。我们可以这样做:

1.  开始整数 **i** 从 **2** 到**n**的循环
2.  检查 **i** 是否为素数，这可以使用 **isPrime(n)** 方法轻松完成。
3.  如果 **i** 是素数，检查它的平方是否小于或等于给定的数。这将只检查素数的平方，因此减少了检查的次数。
4.  如果满足上述条件，数字将被打印，循环将持续到 **i < =n.**

这样，不需要额外的空间来存储任何东西。

下面是不使用额外空间的上述逻辑的实现；

## C++

```
// C++ program to print all
// three-primes smaller than
// or equal to n without using
// extra space
#include <bits/stdc++.h>
using namespace std;

void numbersWith3Divisors(int);
bool isPrime(int);

// Generates all primes upto n and
// prints their squares
void numbersWith3Divisors(int n)
{
    cout << "Numbers with 3 divisors : "
         << endl;

    for(int i = 2; i * i <= n; i++)
    {

        // Check prime
        if (isPrime(i))
        {
            if (i * i <= n)
            {

                // Print numbers in
                // the order of
                // occurence
                cout << i * i << " ";
            }
        }
    }
}

// Check if a number is prime or not
bool isPrime(int n)
{
    for(int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int n = 122;

    numbersWith3Divisors(n);

    return 0;
}

// This code is contributed by vishu2908
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// three-primes smaller than
// or equal to n without using
// extra space
import java.util.*;

class GFG
{

    // 3 divisor logic implementation
    // check if a number is
    // prime or not
    // if it is a prime then
    // check if its square
    // is less than or equal to
    // the given number
    static void numbersWith3Divisors(int n)
    {
        System.out.println("Numbers with 3 divisors : ");

        for (int i = 2; i * i <= n; i++)
        {

            // Check prime
            if (isPrime(i))
            {
                if (i * i <= n)
                {

                    // Print numbers in
                    // the order of
                    // occurence
                    System.out.print(i * i + " ");
                }
            }
        }
    }

    // Check if a number is prime or not
    public static boolean isPrime(int n)
    {
        for (int i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 122;
        numbersWith3Divisors(n);
    }
}

// Contributed by Parag Pallav Singh
```

## 蟒蛇 3

```
# Python3 program to print all
# three-primes smaller than
# or equal to n without using
# extra space

# 3 divisor logic implementation
# check if a number is  prime or
# not if it is a prime then check
# if its square is less than or
# equal to the given number
def numbersWith3Divisors(n):

    print("Numbers with 3 divisors : ")

    i = 2
    while i * i <= n:

        # Check prime
        if (isPrime(i)):
            if (i * i <= n):

                # Print numbers in the order
                # of occurence
                print(i * i, end = " ")

        i += 1

# Check if a number is prime or not
def isPrime(n):

    i = 2
    while i * i <= n:
        if n % i == 0:
            return False

        i += 1

    return True

# Driver code
n = 122

numbersWith3Divisors(n)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to print all
// three-primes smaller than
// or equal to n without using
// extra space
using System;

class GFG{

// 3 divisor logic implementation
// check if a number is prime or
// not if it is a prime then check
// if its square is less than or
// equal to the given number
static void numbersWith3Divisors(int n)
{
    Console.WriteLine("Numbers with 3 divisors : ");

    for(int i = 2; i * i <= n; i++)
    {

        // Check prime
        if (isPrime(i))
        {
            if (i * i <= n)
            {

                // Print numbers in the order
                // of occurence
                Console.Write(i * i + " ");
            }
        }
    }
}

// Check if a number is prime or not
public static bool isPrime(int n)
{
    for(int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Driver code
static void Main()
{
    int n = 122;

    numbersWith3Divisors(n);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program to print all
    // three-primes smaller than
    // or equal to n without using
    // extra space

      // 3 divisor logic implementation
    // check if a number is prime or
    // not if it is a prime then check
    // if its square is less than or
    // equal to the given number
    function numbersWith3Divisors(n)
    {
        document.write("Numbers with 3 divisors : ");

        for(let i = 2; i * i <= n; i++)
        {

            // Check prime
            if (isPrime(i))
            {
                if (i * i <= n)
                {

                    // Print numbers in the order
                    // of occurence
                    document.write(i * i + " ");
                }
            }
        }
    }

    // Check if a number is prime or not
    function isPrime(n)
    {
        if (n == 0 || n == 1)
            return false;

        for(let i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    let n = 122;

    numbersWith3Divisors(n);

// This code is contributed by suresh07.
</script>
```

**输出:**

```
Numbers with 3 divisors :
4 9 25 49 121
```

本文由[Shivam prad Han(anuj _ charm)](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。