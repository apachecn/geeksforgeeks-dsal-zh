# 交替负数的斐波那契数之和

> 原文:[https://www . geeksforgeeks . org/Fibonacci-numbers-with-alternate-negats/](https://www.geeksforgeeks.org/sum-of-fibonacci-numbers-with-alternate-negatives/)

给定一个正整数 n，任务是求 F<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>-……。+ (-1) <sup>n+1</sup> F <sub>n</sub> 其中 F <sub>i</sub> 表示第 I 个斐波那契数。
[斐波那契数列:](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)斐波那契数列是下列整数序列中的数字。

> 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ….

在数学术语中，斐波那契数的序列 Fn 由递归关系
定义

```
Fn = Fn-1 + Fn-2
```

种子值为 F <sub>0</sub> = 0，F <sub>1</sub> = 1。
**例**

```
Input: n = 5
Output: 4
Explanation: 1 - 1 + 2 - 3 + 5 = 4

Input: n = 8
Output: -12
Explanation: 1 - 1 + 2 - 3 + 5 - 8 + 13 - 21 =  -12
```

**方法一:(O(n)时间复杂度)**这种方法包括直接求解问题，找到所有斐波那契数直到 n，然后将交替和相加。但这需要 O(n)个时间复杂度。
以下是上述办法的实施情况:

## C++

```
// C++ Program to find alternate sum
// of Fibonacci numbers

#include <bits/stdc++.h>
using namespace std;

// Computes value of first fibonacci numbers
// and stores their alternate sum
int calculateAlternateSum(int n)
{
    if (n <= 0)
        return 0;

    int fibo[n + 1];
    fibo[0] = 0, fibo[1] = 1;

    // Initialize result
    int sum = pow(fibo[0], 2) + pow(fibo[1], 2);

    // Add remaining terms
    for (int i = 2; i <= n; i++) {
        fibo[i] = fibo[i - 1] + fibo[i - 2];

        // For even terms
        if (i % 2 == 0)
            sum -= fibo[i];

        // For odd terms
        else
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

    // Find the alternating sum
    cout << "Alternating Fibonacci Sum upto "
         << n << " terms: "
         << calculateAlternateSum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find alternate sum
// of Fibonacci numbers

public class GFG {

    //Computes value of first fibonacci numbers
    // and stores their alternate sum
    static double calculateAlternateSum(int n)
    {
        if (n <= 0)
            return 0;

        int fibo[] = new int [n + 1];
        fibo[0] = 0;
        fibo[1] = 1;

        // Initialize result
        double sum = Math.pow(fibo[0], 2) + Math.pow(fibo[1], 2);

        // Add remaining terms
        for (int i = 2; i <= n; i++) {
            fibo[i] = fibo[i - 1] + fibo[i - 2];

            // For even terms
            if (i % 2 == 0)
                sum -= fibo[i];

            // For odd terms
            else
                sum += fibo[i];
        }

        // Return the alternating sum
        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        // Get n
        int n = 8;

        // Find the alternating sum
        System.out.println("Alternating Fibonacci Sum upto "
              + n + " terms: "
              + calculateAlternateSum(n));

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 Program to find alternate sum
# of Fibonacci numbers

# Computes value of first fibonacci numbers
# and stores their alternate sum
def calculateAlternateSum(n):

    if (n <= 0):
        return 0

    fibo = [0]*(n + 1)
    fibo[0] = 0
    fibo[1] = 1

    # Initialize result
    sum = pow(fibo[0], 2) + pow(fibo[1], 2)

    # Add remaining terms
    for i in range(2, n+1) :
        fibo[i] = fibo[i - 1] + fibo[i - 2]

        # For even terms
        if (i % 2 == 0):
            sum -= fibo[i]

        # For odd terms
        else:
            sum += fibo[i]

    # Return the alternating sum
    return sum

# Driver program to test above function
if __name__ == "__main__":
    # Get n
    n = 8

    # Find the alternating sum
    print( "Alternating Fibonacci Sum upto "
        , n ," terms: "
        , calculateAlternateSum(n))

# this code is contributed by
# ChitraNayal
```

## C#

```
// C# Program to find alternate sum
// of Fibonacci numbers
using System;

class GFG
{

// Computes value of first fibonacci numbers
// and stores their alternate sum
static double calculateAlternateSum(int n)
{
    if (n <= 0)
        return 0;

    int []fibo = new int [n + 1];
    fibo[0] = 0;
    fibo[1] = 1;

    // Initialize result
    double sum = Math.Pow(fibo[0], 2) +
                 Math.Pow(fibo[1], 2);

    // Add remaining terms
    for (int i = 2; i <= n; i++)
    {
        fibo[i] = fibo[i - 1] + fibo[i - 2];

        // For even terms
        if (i % 2 == 0)
            sum -= fibo[i];

        // For odd terms
        else
            sum += fibo[i];
    }

    // Return the alternating sum
    return sum;
}

// Driver code
public static void Main()
{
    // Get n
    int n = 8;

    // Find the alternating sum
    Console.WriteLine("Alternating Fibonacci Sum upto " +
              n + " terms: " + calculateAlternateSum(n));

}
}

// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find alternate sum
// of Fibonacci numbers

// Computes value of first fibonacci
// numbers and stores their alternate sum
function calculateAlternateSum($n)
{
    if ($n <= 0)
        return 0;

    $fibo = array();
    $fibo[0] = 0;
    $fibo[1] = 1;

    // Initialize result
    $sum = pow($fibo[0], 2) +
           pow($fibo[1], 2);

    // Add remaining terms
    for ($i = 2; $i <= $n; $i++)
    {
        $fibo[$i] = $fibo[$i - 1] +
                    $fibo[$i - 2];

        // For even terms
        if ($i % 2 == 0)
            $sum -= $fibo[$i];

        // For odd terms
        else
            $sum += $fibo[$i];
    }

    // Return the alternating sum
    return $sum;
}

// Driver Code

// Get n
$n = 8;

// Find the alternating sum
echo ("Alternating Fibonacci Sum upto ");
echo $n ;
echo " terms: ";
echo (calculateAlternateSum($n)) ;

// This code isw contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript Program to find alternate sum
// of Fibonacci numbers

    // Computes value of first fibonacci numbers
    // and stores their alternate sum
    function calculateAlternateSum(n)
    {
        if (n <= 0)
            return 0;

        var fibo = Array(n + 1).fill(0);
        fibo[0] = 0;
        fibo[1] = 1;

        // Initialize result
        var sum = Math.pow(fibo[0], 2) +
        Math.pow(fibo[1], 2);

        // Add remaining terms
        for (i = 2; i <= n; i++) {
            fibo[i] = fibo[i - 1] + fibo[i - 2];

            // For even terms
            if (i % 2 == 0)
                sum -= fibo[i];

            // For odd terms
            else
                sum += fibo[i];
        }

        // Return the alternating sum
        return sum;
    }

    // Driver code

        // Get n
        var n = 8;

        // Find the alternating sum
        document.write(
        "Alternating Fibonacci Sum upto " + n +" terms: "
        + calculateAlternateSum(n)
        );

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Alternating Fibonacci Sum upto 8 terms: -12
```

**方法 2: (O(log n)复杂度)**该方法涉及以下观察以降低时间复杂度:

*   **n = 2，**T2<sub>F<sub>1</sub>–F<sub>2</sub>= 1–1
    = 0
    = 1+(-1)<sup>3</sup>* F<sub>1</sub></sub>
*   **n = 3，**T2<sub>F<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>T9】= 1–1+2
    = 2
    = 1+(-1)<sup>4</sup>* F<sub>2</sub></sub>
*   **n = 4，**T2<sub>F<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>–F<sub>4</sub>T11】= 1–1+2–3
    =-1
    = 1+(-1)<sup>5</sup>* F<sub>3</sub></sub>
*   **n = m 时，**T2<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>-……。+(-1)<sup>m+1</sup>* F<sub>m-1</sub>
    = 1+(-1)<sup>m+1</sup>F<sub>m-1</sub>
    假设这是真的。如果(n = m+1)也是真的，这意味着假设是正确的。否则，就是错的。
*   **n = m+1，**T2<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>-……。+(-1)<sup>m+1</sup>* F<sub>m</sub>+(-1)<sup>m+2</sup>* F<sub>m+1</sub>
    = 1+(-1)<sup>m+1</sup>* F<sub>m-1</sub>+(-1)<sup>m+2</sup>* F<sub>m+1</sub>
    = 1+(-1)

因此交替斐波那契和的一般术语是:

> **F<sub>1</sub>–F<sub>2</sub>+F<sub>3</sub>-……。+(-1)<sup>n+1</sup>F<sub>n</sub>= 1+(-1)<sup>n+1</sup>F<sub>n-1</sub>**

所以为了找到一个替代和，只需要找到第 n 个斐波那契项，可以在 O(log n)时间[内完成(参考本文的方法 5 或 6。)](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)
以下是本条方法 6 的实施:

## C++

```
// C++ Program to find alternate  Fibonacci Sum in
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

// Computes value of Alternate  Fibonacci Sum
int calculateAlternateSum(int n)
{
    if (n % 2 == 0)
        return (1 - fib(n - 1));
    else
        return (1 + fib(n - 1));
}

// Driver program to test above function
int main()
{
    // Get n
    int n = 8;

    // Find the alternating sum
    cout << "Alternating Fibonacci Sum upto "
         << n << " terms  : "
         << calculateAlternateSum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find alternate
// Fibonacci Sum in O(Log n) time.
class GFG {

    static final int MAX = 1000;

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
        if (f[n] > 0) {
            return f[n];
        }

        int k = (n % 2 == 1) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = (n % 2 == 1) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1))
                : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

    // Computes value of Alternate Fibonacci Sum
    static int calculateAlternateSum(int n) {
        if (n % 2 == 0) {
            return (1 - fib(n - 1));
        } else {
            return (1 + fib(n - 1));
        }
    }

// Driver program to test above function
    public static void main(String[] args) {
        // Get n
        int n = 8;

        // Find the alternating sum
        System.out.println("Alternating Fibonacci Sum upto "
                + n + " terms : "
                + calculateAlternateSum(n));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find alternative
# Fibonacci Sum in O(Log n) time.
MAX = 1000

# List for memorization
f = [0] * MAX

# Returns n'th fibonacci number
# using table f[]
def fib(n):

    # Base Cases
    if(n == 0):
        return(0)

    if(n == 1 or n == 2):
        f[n] = 1
        return(f[n])

    # If fib(n) is already computed
    if(f[n]):
        return(f[n])

    if(n & 1):
        k = (n + 1) // 2
    else:
        k = n // 2

    # Applying above formula [Note value n&1 is 1
    # if n is odd, else 0]
    if(n & 1):
        f[n] = (fib(k) * fib(k) +
                fib(k - 1) * fib(k - 1))
    else:
        f[n] = (2 * fib(k-1) + fib(k)) * fib(k)

    return(f[n])

# Computes value of Alternate Fibonacci Sum
def cal(n):

    if(n % 2 == 0):
        return(1 - fib(n - 1))
    else:
        return(1 + fib(n - 1))

# Driver Code
if(__name__=="__main__"):

    n = 8
    print("Alternating Fibonacci Sum upto",
           n, "terms :", cal(n))

# This code is contributed by arjunsaini9081
```

## C#

```
// C# Program to find alternate
// Fibonacci Sum in O(Log n) time.
using System;

class GFG
{
    static readonly int MAX = 1000;

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
        if (f[n] > 0)
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

    // Computes value of Alternate Fibonacci Sum
    static int calculateAlternateSum(int n)
    {
        if (n % 2 == 0)
        {
            return (1 - fib(n - 1));
        } else
        {
            return (1 + fib(n - 1));
        }
    }

    // Driver code
    public static void Main()
    {
        // Get n
        int n = 8;

        // Find the alternating sum
        Console.WriteLine("Alternating Fibonacci Sum upto "
                + n + " terms : "
                + calculateAlternateSum(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
 //Javascript implementation of the approach
MAX = 1000;

// Create an array for memoization
f = new Array(MAX);
f.fill(0);
// Returns n'th Fibonacci number
// using table f[]
function fib( n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n])
        return f[n];

    var k = (n & 1) ? (n + 1) / 2 : n / 2;

    // Applying above formula [Note value n&1 is 1
    // if n is odd, else 0].
    f[n] = (n & 1) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1))
                   : (2 * fib(k - 1) + fib(k)) * fib(k);

    return f[n];
}
// Computes value of Alternate  Fibonacci Sum
function calculateAlternateSum(n)
{
    if (n % 2 == 0)
        return (1 - fib(n - 1));
    else
        return (1 + fib(n - 1));
}

// Get n
var n = 8;
// Find the alternating sum
document.write( "Alternating Fibonacci Sum upto "+ n + " terms  : "
         + calculateAlternateSum(n) + "<br>");

getElement(a, n, S);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Alternating Fibonacci Sum upto 8 terms: -12
```