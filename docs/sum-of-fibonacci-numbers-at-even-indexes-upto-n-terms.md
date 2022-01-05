# 偶数索引处的斐波那契数之和直到 N 项

> 原文:[https://www . geesforgeks . org/Fibonacci-numbers-at-偶数索引-up-n-terms/](https://www.geeksforgeeks.org/sum-of-fibonacci-numbers-at-even-indexes-upto-n-terms/)

给定一个正整数 N，任务是找出 F<sub>2</sub>+F<sub>4</sub>+F<sub>6</sub>+……+F<sub>2n</sub>到 N 项的值，其中 F <sub>i</sub> 表示第 I 个斐波那契数。
[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是下列整数序列中的数字。

> 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ……

**例:**

> **输入:** n = 5
> **输出:** 88
> N = 5，所以斐波那契数列将从第 0 项到第 10 项生成:
> 0、1、1、2、3、5、8、13、21、34、55
> 偶数索引处的元素之和= 0 + 1 + 3 + 8 + 21 + 55
> **输入:** n = 8
> **输出:【T11**

**方法-1:** 该方法包括直接求解问题，找到 2n 个之前的所有斐波那契数，并将仅有的偶数个指数相加。但这需要 O(n)个时间复杂度。
以下是上述办法的实施情况:

## C++

```
// C++ Program to find  sum
// of even-indiced Fibonacci numbers
#include <bits/stdc++.h>
using namespace std;

// Computes value of first fibonacci numbers
// and stores the even-indexed sum
int calculateEvenSum(int n)
{
    if (n <= 0)
        return 0;

    int fibo[2 * n + 1];
    fibo[0] = 0, fibo[1] = 1;

    // Initialize result
    int sum = 0;

    // Add remaining terms
    for (int i = 2; i <= 2 * n; i++) {
        fibo[i] = fibo[i - 1] + fibo[i - 2];

        // For even indices
        if (i % 2 == 0)
            sum += fibo[i];
    }

    // Return the alternating sum
    return sum;
}

// Driver program to test above function
int main()
{

    // Get n
    int n = 8;

    // Find the even-indiced sum
    cout << "Even indexed Fibonacci Sum upto "
         << n << " terms: "
         << calculateEvenSum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum
// of even-indiced Fibonacci numbers

import java.io.*;

class GFG {

// Computes value of first fibonacci numbers
// and stores the even-indexed sum
static int calculateEvenSum(int n)
{
    if (n <= 0)
        return 0;

    int fibo[] = new int[2 * n + 1];
    fibo[0] = 0; fibo[1] = 1;

    // Initialize result
    int sum = 0;

    // Add remaining terms
    for (int i = 2; i <= 2 * n; i++) {
        fibo[i] = fibo[i - 1] + fibo[i - 2];

        // For even indices
        if (i % 2 == 0)
            sum += fibo[i];
    }

    // Return the alternating sum
    return sum;
}

// Driver program
    public static void main (String[] args) {
            // Get n
    int n = 8;

    // Find the even-indiced sum
    System.out.println("Even indexed Fibonacci Sum upto "
        + n + " terms: "+
        + calculateEvenSum(n));

    }
}

// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 Program to find sum
# of even-indiced Fibonacci numbers

# Computes value of first fibonacci
# numbers and stores the even-indexed sum
def calculateEvenSum(n) :

    if n <= 0 :
        return 0

    fibo = [0] * (2 * n + 1)
    fibo[0] , fibo[1] = 0 , 1

    # Initialize result
    sum = 0

    # Add remaining terms
    for i in range(2, 2 * n + 1) :

        fibo[i] = fibo[i - 1] + fibo[i - 2]

        # For even indices
        if i % 2 == 0 :
            sum += fibo[i]

    # Return the alternating sum
    return sum

# Driver code
if __name__ == "__main__" :

    # Get n
    n = 8

    # Find the even-indiced sum
    print("Even indexed Fibonacci Sum upto",
           n, "terms:", calculateEvenSum(n))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# Program to find sum of
// even-indiced Fibonacci numbers
using System;

class GFG
{

// Computes value of first fibonacci
// numbers and stores the even-indexed sum
static int calculateEvenSum(int n)
{
    if (n <= 0)
        return 0;

    int []fibo = new int[2 * n + 1];
    fibo[0] = 0; fibo[1] = 1;

    // Initialize result
    int sum = 0;

    // Add remaining terms
    for (int i = 2; i <= 2 * n; i++)
    {
        fibo[i] = fibo[i - 1] +
                  fibo[i - 2];

        // For even indices
        if (i % 2 == 0)
            sum += fibo[i];
    }

    // Return the alternating sum
    return sum;
}

// Driver Code
static public void Main ()
{
    // Get n
    int n = 8;

    // Find the even-indiced sum
    Console.WriteLine("Even indexed Fibonacci Sum upto " +
                    n + " terms: " + calculateEvenSum(n));
}
}

// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// even-indiced Fibonacci numbers

// Computes value of first fibonacci
// numbers and stores the even-indexed sum
function calculateEvenSum($n)
{
    if ($n <= 0)
        return 0;

    $fibo[2 * $n + 1] = array();
    $fibo[0] = 0; $fibo[1] = 1;

    // Initialize result
    $sum = 0;

    // Add remaining terms
    for ($i = 2; $i <= 2 * $n; $i++)
    {
        $fibo[$i] = $fibo[$i - 1] +
                    $fibo[$i - 2];

        // For even indices
        if ($i % 2 == 0)
            $sum += $fibo[$i];
    }

    // Return the alternating sum
    return $sum;
}

// Driver Code

// Get n
$n = 8;

// Find the even-indiced sum
echo "Even indexed Fibonacci Sum upto " . $n .
     " terms: " . calculateEvenSum($n) . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// Javascript Program to find sum
// of even-indiced Fibonacci numbers

    // Computes value of first fibonacci numbers
    // and stores the even-indexed sum
    function calculateEvenSum( n)
    {
        if (n <= 0)
            return 0;

        let fibo = Array(2 * n + 1);
        fibo[0] = 0;
        fibo[1] = 1;

        // Initialize result
        let sum = 0;

        // Add remaining terms
        for ( i = 2; i <= 2 * n; i++)
        {
            fibo[i] = fibo[i - 1] + fibo[i - 2];

            // For even indices
            if (i % 2 == 0)
                sum += fibo[i];
        }

        // Return the alternating sum
        return sum;
    }

    // Driver program

        // Get n
        let n = 8;

        // Find the even-indiced sum
        document.write("Even indexed Fibonacci Sum upto " + n + " terms: " + +calculateEvenSum(n));

// This code is contributed by 29AjayKumar 
</script>
```

**Output:** 

```
Even indexed Fibonacci Sum upto 8 terms: 1596
```

**方法-2:**

> 可以清楚地看到，这样就可以得到所需的总和:
> 2(F<sub>2</sub>+F<sub>4</sub>+F<sub>6</sub>+……+F<sub>2n</sub>)**=**(F<sub>1</sub>+F<sub>2</sub>+F<sub>3</sub>+F<sub>4</sub>+……+F<sub>2n</sub> –(F<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>–F<sub>4</sub>+……+F<sub>2n</sub>)
> 现在如果我们把 2n 而不是 n 放在这里[给出的公式中](https://www.geeksforgeeks.org/sum-fibonacci-numbers/)就可以得到第一项。
> 因此 F<sub>1</sub>+F<sub>2</sub>+F<sub>3</sub>+F<sub>4</sub>+……+F<sub>2n</sub>T45】=F<sub>2n+2</sub>–1。
> 如果我们在这里给出的公式
> 中放 2n 而不是 n，也可以找到第二个术语因此，F<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>–F<sub>4</sub>+……-F<sub>2n</sub>**=**1+(-1)<sup>2n+1</sup>F
> 所以， 2(F<sub>2</sub>+F<sub>4</sub>+F<sub>6</sub>+……+F<sub>2n</sub>
> **=**F<sub>2n+2</sub>–1–1+F<sub>2n-1</sub>
> **=**F<sub>2n+2</sub>+F<sub>2n-1</sub>–2
> T97】=F<sub>2n</sub>+F<sub>2n+1</sub>+F

所以为了找到需要的和，任务是只找到需要 O(log n)时间的 F <sub>2n+1</sub> 。(参考[这篇](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)文章中的方法 5 或方法 6。
以下是上述方法的实施:

## C++

```
// C++ Program to find even indexed Fibonacci Sum in
// O(Log n) time.

#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

// Create an array for memoization
int f[MAX] = { 0 };

// Returns n'th Fibonacci number
// using table f[]
int fib(int n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n])
        return f[n];

    int k = (n & 1) ? (n + 1) / 2 : n / 2;

    // Applying above formula [Note value n&1 is 1
    // if n is odd, else 0].
    f[n] = (n & 1) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1))
                   : (2 * fib(k - 1) + fib(k)) * fib(k);

    return f[n];
}

// Computes value of even-indexed  Fibonacci Sum
int calculateEvenSum(int n)
{
    return (fib(2 * n + 1) - 1);
}

// Driver program to test above function
int main()
{
    // Get n
    int n = 8;

    // Find the alternating sum
    cout << "Even indexed Fibonacci Sum upto "
         << n << " terms: "
         << calculateEvenSum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find even indexed Fibonacci Sum in
// O(Log n) time.

class GFG {

    static int MAX = 1000;

   // Create an array for memoization
    static int f[] = new int[MAX];

// Returns n'th Fibonacci number
// using table f[]
    static int fib(int n) {
        // Base cases
        if (n == 0) {
            return 0;
        }
        if (n == 1 || n == 2) {
            return (f[n] = 1);
        }

        // If fib(n) is already computed
        if (f[n] == 1) {
            return f[n];
        }

        int k = (n % 2 == 1) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = (n % 2 == 1) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1))
                : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

// Computes value of even-indexed Fibonacci Sum
    static int calculateEvenSum(int n) {
        return (fib(2 * n + 1) - 1);
    }

// Driver program to test above function
    public static void main(String[] args) {
        // Get n
        int n = 8;

        // Find the alternating sum
        System.out.println("Even indexed Fibonacci Sum upto "
                + n + " terms: "
                + calculateEvenSum(n));
    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to find even indexed
# Fibonacci Sum in O(Log n) time.
MAX = 1000;

# Create an array for memoization
f = [0] * MAX;

# Returns n'th Fibonacci number
# using table f[]
def fib(n):

    # Base cases
    if (n == 0):
        return 0;
    if (n == 1 or n == 2):
        f[n] = 1;
        return f[n];

    # If fib(n) is already computed
    if (f[n]):
        return f[n];

    k = (n + 1) // 2 if (n % 2 == 1) else n // 2;

    # Applying above formula [Note value n&1 is 1
    # if n is odd, else 0].
    f[n] = (fib(k) * fib(k) + fib(k - 1) * fib(k - 1)) \
    if (n % 2 == 1) else (2 * fib(k - 1) + fib(k)) * fib(k);

    return f[n];

# Computes value of even-indexed Fibonacci Sum
def calculateEvenSum(n):
    return (fib(2 * n + 1) - 1);

# Driver Code
if __name__ == '__main__':

    # Get n
    n = 8;

    # Find the alternating sum
    print("Even indexed Fibonacci Sum upto",
          n, "terms:", calculateEvenSum(n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# Program to find even indexed Fibonacci Sum in
// O(Log n) time.
using System;

class GFG
{

    static int MAX = 1000;

    // Create an array for memoization
    static int []f = new int[MAX];

    // Returns n'th Fibonacci number
    // using table f[]
    static int fib(int n)
    {
        // Base cases
        if (n == 0)
        {
            return 0;
        }
        if (n == 1 || n == 2)
        {
            return (f[n] = 1);
        }

        // If fib(n) is already computed
        if (f[n] == 1)
        {
            return f[n];
        }

        int k = (n % 2 == 1) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = (n % 2 == 1) ? (fib(k) * fib(k) +
                                fib(k - 1) * fib(k - 1))
                : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

    // Computes value of even-indexed Fibonacci Sum
    static int calculateEvenSum(int n)
    {
        return (fib(2 * n + 1) - 1);
    }

    // Driver code
    public static void Main()
    {
        // Get n
        int n = 8;

        // Find the alternating sum
        Console.WriteLine("Even indexed Fibonacci Sum upto "
                + n + " terms: "
                + calculateEvenSum(n));
    }
}

//This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript Program to find even indexed Fibonacci Sum in
// O(Log n) time.
    var MAX = 1000;

    // Create an array for memoization
    var f = Array(MAX).fill(0);

    // Returns n'th Fibonacci number
    // using table f
    function fib(n) {
        // Base cases
        if (n == 0) {
            return 0;
        }
        if (n == 1 || n == 2) {
            return (f[n] = 1);
        }

        // If fib(n) is already computed
        if (f[n] == 1) {
            return f[n];
        }

        var k = (n % 2 == 1) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = (n % 2 == 1) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1)) : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

    // Computes value of even-indexed Fibonacci Sum
    function calculateEvenSum(n) {
        return (fib(2 * n + 1) - 1);
    }

    // Driver program to test above function

        // Get n
        var n = 8;

        // Find the alternating sum
        document.write("Even indexed Fibonacci Sum upto " + n + " terms: " + calculateEvenSum(n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Even indexed Fibonacci Sum upto 8 terms: 1596
```