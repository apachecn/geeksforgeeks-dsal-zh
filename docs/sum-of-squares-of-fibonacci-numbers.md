# 斐波那契数的平方和

> 原文:[https://www . geesforgeks . org/Fibonacci 数的平方和/](https://www.geeksforgeeks.org/sum-of-squares-of-fibonacci-numbers/)

给定一个正整数 N，任务是求所有[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)到第 N 个斐波那契数的平方和。也就是

```
f02 + f12 + f22+.......+fn2 

where fi indicates i-th fibonacci number.
```

**斐波那契数:** f <sub>0</sub> =0 和 f <sub>1</sub> =1 和 f<sub>I</sub>= f<sub>I-1</sub>+f<sub>I-2</sub>对于所有 i > =2。
**示例:**

```
Input: N = 3
Output: 6
Explanation: 0 + 1 + 1 + 4 = 6

Input: N = 6
Output: 104
Explanation: 0 + 1 + 1 + 4 + 9 + 25 + 64 = 104
```

**方法 1:** 找出所有的斐波那契数直到 N，并把它们的平方相加。该方法将花费 **O(n)** 的时间复杂度。
以下是本办法的实施情况:

## C++

```
// C++ Program to find sum of
// squares of Fibonacci numbers
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of
// squares of Fibonacci numbers
int calculateSquareSum(int n)
{
    if (n <= 0)
        return 0;

    int fibo[n + 1];
    fibo[0] = 0, fibo[1] = 1;

    // Initialize result
    int sum = (fibo[0] * fibo[0]) + (fibo[1] * fibo[1]);

    // Add remaining terms
    for (int i = 2; i <= n; i++) {
        fibo[i] = fibo[i - 1] + fibo[i - 2];
        sum += (fibo[i] * fibo[i]);
    }

    return sum;
}

// Driver program to test above function
int main()
{
    int n = 6;

    cout << "Sum of squares of Fibonacci numbers is : "
         << calculateSquareSum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of
// squares of Fibonacci numbers

public class Improve {

     // Function to calculate sum of
    // squares of Fibonacci numbers
    static int calculateSquareSum(int n)
    {
        if (n <= 0)
            return 0;

        int fibo[] = new int[n+1];
        fibo[0] = 0 ;
        fibo[1] = 1 ;

        // Initialize result
        int sum = (fibo[0] * fibo[0]) + (fibo[1] * fibo[1]);

        // Add remaining terms
        for (int i = 2; i <= n; i++) {
            fibo[i] = fibo[i - 1] + fibo[i - 2];
            sum += (fibo[i] * fibo[i]);
        }

        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
           int n = 6;
           System.out.println("Sum of squares of Fibonacci numbers is : " +
                                calculateSquareSum(n));

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 Program to find sum of
# squares of Fibonacci numbers

# Function to calculate sum of
# squares of Fibonacci numbers
def calculateSquareSum(n):
    fibo = [0] * (n + 1);
    if (n <= 0):
        return 0;
    fibo[0] = 0;
    fibo[1] = 1;

    # Initialize result
    sum = ((fibo[0] * fibo[0]) +
           (fibo[1] * fibo[1]));

    # Add remaining terms
    for i in range(2, n + 1):
        fibo[i] = (fibo[i - 1] +
                   fibo[i - 2]);
        sum += (fibo[i] * fibo[i]);

    return sum;

# Driver Code
n = 6;

print("Sum of squares of Fibonacci numbers is :",
                          calculateSquareSum(n));

# This Code is contributed by mits
```

## C#

```
// C# Program to find sum of
// squares of Fibonacci numbers

using System;
public class Improve {

     // Function to calculate sum of
    // squares of Fibonacci numbers
    static int calculateSquareSum(int n)
    {
        if (n <= 0)
            return 0;

        int[] fibo = new int[n+1];
        fibo[0] = 0 ;
        fibo[1] = 1 ;

        // Initialize result
        int sum = (fibo[0] * fibo[0]) + (fibo[1] * fibo[1]);

        // Add remaining terms
        for (int i = 2; i <= n; i++) {
            fibo[i] = fibo[i - 1] + fibo[i - 2];
            sum += (fibo[i] * fibo[i]);
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
           int n = 6;
           Console.Write("Sum of squares of Fibonacci numbers is : " +
                                calculateSquareSum(n));

    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// squares of Fibonacci numbers

// Function to calculate sum of
// squares of Fibonacci numbers
function calculateSquareSum($n)
{
    if ($n <= 0)
        return 0;
    $fibo[0] = 0;
    $fibo[1] = 1;

    // Initialize result
    $sum = ($fibo[0] * $fibo[0]) +
           ($fibo[1] * $fibo[1]);

    // Add remaining terms
    for ($i = 2; $i <= $n; $i++)
    {
        $fibo[$i] = $fibo[$i - 1] +
                    $fibo[$i - 2];
        $sum += ($fibo[$i] * $fibo[$i]);
    }

    return $sum;
}

// Driver Code
$n = 6;

echo "Sum of squares of Fibonacci numbers is : ",
                          calculateSquareSum($n);

// This Code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript Program to find sum of
// squares of Fibonacci numbers

    // Function to calculate sum of
    // squares of Fibonacci numbers
    function calculateSquareSum(n)
    {
        if (n <= 0)
            return 0;

        var fibo = Array(n + 1).fill(0);
        fibo[0] = 0;
        fibo[1] = 1;

        // Initialize result
        var sum = (fibo[0] * fibo[0]) +
                  (fibo[1] * fibo[1]);

        // Add remaining terms
        for (i = 2; i <= n; i++) {
            fibo[i] = fibo[i - 1] + fibo[i - 2];
            sum += (fibo[i] * fibo[i]);
        }

        return sum;
    }

    // Driver code

        var n = 6;
        document.write(
"Sum of squares of Fibonacci numbers is :"
+ calculateSquareSum(n)
);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Sum of squares of Fibonacci numbers is : 104
```

**方法 2:** 我们知道对于第 I 个斐波那契数，

```
fi+1 = fi + fi-1  for all i>0

Or, fi = fi+1 - fi-1 for all i>0
Or, fi2 = fifi+1 - fi-1fi
```

所以对于任何 n>0，我们看到，

> f<sub>0</sub><sup>【2】</sup>+f<sub>【1】</sub><sup>【2】</sup>+f<sub>【2】</sub>+2。+f<sub>n</sub><sup>2</sup>
> = f<sub>0</sub><sup>2</sup>+【f<sub>1</sub>f<sub>2</sub>+[f]t37]nf<sub>n+1</sub>–f<sub>n-1</sub>f<sub>n</sub>n]= f<sub>n</sub>f

这个恒等式也满足 n=0(对于 n=0，f<sub>0</sub><sup>2</sup>= 0 = f<sub>0</sub>f<sub>1</sub>)。
所以求和只需要求 f <sub>n</sub> 和 f <sub>n+1</sub> 。在 O(对数 n)时间内找到 f <sub>n</sub> 。参考本文[方法 5 或方法 6](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
以下是上述方法的实施:

## C++

```
// C++ Program to find sum of squares of
// Fibonacci numbers in O(Log n) time.
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1000;

// Create an array for memoization
int f[MAX] = { 0 };

// Returns n'th Fibonacci number using table f[]
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

// Function to calculate sum of
// squares of Fibonacci numbers
int calculateSumOfSquares(int n)
{
    return fib(n) * fib(n + 1);
}

// Driver Code
int main()
{
    int n = 6;

    cout << "Sum of Squares of Fibonacci numbers is : "
         << calculateSumOfSquares(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of squares of
// Fibonacci numbers in O(Log n) time.

class gfg {

    static int[] f = new int[1000];
// Create an array for memoization

// Returns n'th Fibonacci number using table f[]
    public static int fib(int n) {
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

        int k = ((n & 1) > 0) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = ((n & 1) > 0) ? (fib(k)
                * fib(k) + fib(k - 1) * fib(k - 1))
                : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

// Function to calculate sum of
// squares of Fibonacci numbers
    public static int calculateSumOfSquares(int n) {
        return fib(n) * fib(n + 1);
    }
}

// Driver Code
class geek {

    public static void main(String[] args) {
        gfg g = new gfg();
        int n = 6;
        System.out.println("Sum of Squares of Fibonacci numbers is : "
                + g.calculateSumOfSquares(n));
    }

}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find sum of squares
# of Fibonacci numbers in O(Log n) time.
MAX = 1000

# Create an array for memoization
f = [0 for i in range(MAX)]

# Returns n'th Fibonacci number using
# table f[]
def fib(n):

    # Base cases
    if n == 0:
        return 0
    if n == 1 or n == 2:
        return 1

    # If fib(n) is already computed
    if f[n]:
        return f[n]

    if n & 1:
        k = (n + 1) // 2
    else:
        k = n // 2

    # Applying above formula[Note value
    # n & 1 is 1 if n is odd, else 0].
    if n & 1:
        f[n] = (fib(k) * fib(k) +
                fib(k - 1) * fib(k - 1))
    else:
        f[n] = ((2 * fib(k - 1) +
                     fib(k)) * fib(k))
    return f[n]

# Function to calculate sum of
# squares of Fibonacci numbers
def calculateSumOfSquares(n):

    return fib(n) * fib(n + 1)

# Driver Code
n = 6
print("Sum of Squares of "
      "Fibonacci numbers is :",
      calculateSumOfSquares(n))

# This code is contributed by Gaurav Kumar Tailor
```

## C#

```
// C# Program to find sum of squares of
// Fibonacci numbers in O(Log n) time.
using System;
class gfg
{
 int []f = new int [1000];
  // Create an array for memoization

 // Returns n'th Fibonacci number using table f[] 
 public int fib(int n)
 {
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n]>0)
        return f[n];

    int k = ((n & 1)>0) ? (n + 1) / 2 : n / 2;

    // Applying above formula [Note value n&1 is 1
    // if n is odd, else 0].
    f[n] = ((n & 1)>0) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1))
                : (2 * fib(k - 1) + fib(k)) * fib(k);

    return f[n];
 }

// Function to calculate sum of
// squares of Fibonacci numbers
public int calculateSumOfSquares(int n)
 {
    return fib(n) * fib(n + 1);
 }
}

// Driver Code
class geek
{
 public static int Main()
 {
    gfg g = new gfg();
    int n = 6;
    Console.WriteLine( "Sum of Squares of Fibonacci numbers is : {0}", g.calculateSumOfSquares(n));
    return 0;
 }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of squares of
// Fibonacci numbers in O(Log n) time.

$MAX = 1000;
global $f;

// Create an array for memoization
$f = array_fill(0, $MAX, 0);

// Returns n'th Fibonacci number
// using table f[]
function fib($n)
{
    // Base cases
    if ($n == 0)
        return 0;
    if ($n == 1 || $n == 2)
        return ($f[$n] = 1);

    $k = ($n & 1) ? ($n + 1) / 2 : $n / 2;

    // Applying above formula [Note value
    // n&1 is 1 if n is odd, else 0].
    $f[$n] = ($n & 1) ? (fib($k) * fib($k) +
                         fib($k - 1) * fib($k - 1)) :
                    (2 * fib($k - 1) + fib($k)) * fib($k);

    return $f[$n];
}

// Function to calculate sum of
// squares of Fibonacci numbers
function calculateSumOfSquares( $n)
{
    return fib($n) * fib($n + 1);
}

// Driver Code
$n = 6;

echo "Sum of Squares of Fibonacci numbers is : ";
echo calculateSumOfSquares($n);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find sum of squares of
    // Fibonacci numbers in O(Log n) time.

    // Create an array for memoization
    let f = new Array(1000);
    f.fill(0);

    // Returns n'th Fibonacci number using table f[]
    function fib(n) {
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

        let k = ((n & 1) > 0) ? (n + 1) / 2 : n / 2;

        // Applying above formula [Note value n&1 is 1
        // if n is odd, else 0].
        f[n] = ((n & 1) > 0) ? (fib(k)
                * fib(k) + fib(k - 1) * fib(k - 1))
                : (2 * fib(k - 1) + fib(k)) * fib(k);

        return f[n];
    }

    // Function to calculate sum of
    // squares of Fibonacci numbers
    function calculateSumOfSquares(n) {
        return fib(n) * fib(n + 1);
    }

    let n = 6;

    document.write("Sum of Squares of Fibonacci numbers is : "
         + calculateSumOfSquares(n));

</script>
```

**Output:** 

```
Sum of Squares of Fibonacci numbers is : 104
```