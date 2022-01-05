# 性感质数

> 原文:[https://www.geeksforgeeks.org/sexy-prime/](https://www.geeksforgeeks.org/sexy-prime/)

在数学中， [**【性感素数】**](https://en.wikipedia.org/wiki/Sexy_prime) 是彼此相差 6 的素数。例如，数字 5 和 11 都是性感的质数，因为它们相差 6。如果 p + 2 或 p + 4(其中 p 是下素数)也是素数。
可分为:

*   性感质数对:它的形式是(p，p + 6)，其中 p 和 p + 6 是质数。
    eg(11，17)是性感的质数对。

*   性感质数三胞胎:p + 18 复合的质数三胞胎(p，p + 6，p + 12)称为性感质数三胞胎。
    例(7，13，19)是性感的三胞胎。

*   性感质数四胞胎:性感质数四胞胎(p，p + 6，p + 12，p + 18)只能以十进制表示中以 1 结尾的质数开始(p = 5 的四胞胎除外)。
    eg(41，47，53，59)是性感的质数四胞胎。

*   性感质数五胞胎:在一个五项算术级数中，公差为 6，其中一项必须能被 5 整除，因为这两个数相对质数。因此，唯一性感的黄金五胞胎是(5，11，17，23，29)；性感质数不再可能出现。

给定一个范围的形式**【L，R】**。任务是打印范围内所有性感的质数对。
**例:**

```
Input : L = 6, R = 59
Output : (7, 13) (11, 17) (13, 19) 
(17, 23) (23, 29) (31, 37) (37, 43) 
(41, 47) (47, 53) (53, 59) 

Input : L = 1, R = 19
Output : (5, 11) (7, 13) (11, 17) (13, 19)
```

使用厄拉多塞的[筛可以生成范围【L，R】内的性感素。其思想是生成筛的布尔数组，运行 I 从 L 到 R–6(含)的循环，并检查 I 和 i + 6 是否是素数。如果两者都是质数，打印两个数字。
以下是本办法的实施情况:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP Program to print sexy prime in a range.
#include <bits/stdc++.h>
using namespace std;

// Print the sexy prime in a range
void sexyprime(int l, int r)
{
    // Sieve Of Eratosthenes for generating
    // prime number.
    bool prime[r + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= r; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= r; i += p)
                prime[i] = false;
        }
    }

    // From L to R - 6, checking if i,
    // i + 6 are prime or not.
    for (int i = l; i <= r - 6; i++)
        if (prime[i] && prime[i + 6])
            cout << "(" << i << ", "
                 << i + 6 << ") ";   
}

// Driven Program
int main()
{
    int L = 6, R = 59;
    sexyprime(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print sexy prime in a range.
import java.util.Arrays;
import java.util.Collections;

class GFG
{
    // Print the sexy prime in a range
    public static void sexyprime(int l, int r)
    {
        // Sieve Of Eratosthenes for generating
        // prime number.
        boolean [] prime= new boolean[r + 1];

        // memset(prime, true, sizeof(prime));
        Arrays.fill(prime, true);

        for (int p = 2; p * p <= r; p++)
        {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {
                // Update all multiples of p
                for (int i = p * 2; i <= r; i += p)
                    prime[i] = false;
            }
        }

        // From L to R - 6, checking if i,
        // i + 6 are prime or not.
        for (int i = l; i <= r - 6; i++)
            if (prime[i] && prime[i + 6])
                System.out.print( "(" + i + ", "
                        + (i + 6) + ") ");
    }

    // Driver program to test above methods
    public static void main(String[] args)
    {
        int L = 6, R = 59;
        sexyprime(L, R);
    }
}

// This code is contributed by Chhavi
```

## 蟒蛇 3

```
# Python 3 Program to print
# sexy prime in a range.

# Print the sexy prime in a range
def sexyprime(l, r) :

    # Sieve Of Eratosthenes
    # for generating
    # prime number.
    prime=[True] * (r + 1)

    p = 2

    while(p * p <= r) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            for i in range( p * 2, r+1 ,p) :
                   prime[i] = False

        p = p + 1

    # From L to R - 6, checking if i,
    # i + 6 are prime or not.
    for i in range( l,r - 6 + 1) :

        if (prime[i] and prime[i + 6]) :
            print("(", i , ",", i + 6,")", end="")

# Driven Program
L = 6
R = 59
sexyprime(L, R)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to print sexy
// prime in a range.
using System;

class GFG
{
    // Print the sexy
    // prime in a range
    public static void sexyprime(int l,
                                 int r)
    {
        // Sieve Of Eratosthenes
        // for generating prime number.
        int[] prime = new int[r + 1];

        // memset(prime, true,
        // sizeof(prime));
        for (int i = 0; i < r + 1; i++)
            prime[i] = 1;

        for (int p = 2; p * p <= r; p++)
        {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == 1)
            {
                // Update all multiples of p
                for (int i = p * 2;
                         i <= r; i += p)
                    prime[i] = 0;
            }
        }

        // From L to R - 6, checking
        // if i, i + 6 are prime or not.
        for (int i = l; i <= r - 6; i++)
            if (prime[i] == 1 && prime[i + 6] == 1)
                Console.Write("(" + i + ", " +
                               (i + 6) + ") ");
    }

    // Driver Code
    public static void Main()
    {
        int L = 6, R = 59;
        sexyprime(L, R);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print
// sexy prime in a range.

// Print the sexy
// prime in a range
function sexyprime($l, $r)
{
    // Sieve Of Eratosthenes for
    // generating prime number.
    $prime = array_fill(0, $r + 1,
                            true);

    for ($p = 2;
         $p * $p <= $r; $p++)
    {

        // If prime[p] is not
        // changed, then it
        // is a prime
        if ($prime[$p] == true)
        {

            // Update all
            // multiples of p
            for ($i = $p * 2;
                 $i <= $r; $i += $p)
                $prime[$i] = false;
        }
    }

    // From L to R - 6,
    // checking if i,
    // i + 6 are prime or not.
    for ($i = $l; $i <= $r - 6; $i++)
        if ($prime[$i] &&
            $prime[$i + 6])
            echo "(" , $i , ", ",
                       $i + 6 , ") ";
}

// Driver Code
$L = 6;
$R = 59;
sexyprime($L, $R);

// This code is contributed
// by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript Program to print sexy prime in a range.

// Print the sexy prime in a range
function sexyprime(l, r)
{
    // Sieve Of Eratosthenes for generating
    // prime number.
    var prime = Array(r+1).fill(true);

    for (var p = 2; p * p <= r; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (var i = p * 2; i <= r; i += p)
                prime[i] = false;
        }
    }

    // From L to R - 6, checking if i,
    // i + 6 are prime or not.
    for (var i = l; i <= r - 6; i++)
        if (prime[i] && prime[i + 6])
            document.write( "(" + i + ", "
                 + (i + 6) + ") ");   
}

// Driven Program
var L = 6, R = 59;
sexyprime(L, R);

</script>
```

**输出:**

```
(7, 13) (11, 17) (13, 19) (17, 23) 
(23, 29) (31, 37) (37, 43) (41, 47) 
(47, 53) (53, 59) 
```