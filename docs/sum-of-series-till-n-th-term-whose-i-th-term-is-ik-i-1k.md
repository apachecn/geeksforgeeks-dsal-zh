# 直到第 n 项的级数和，第 I 项是 i^k–(i-1)^k

> 原文:[https://www . geesforgeks . org/series-sum-to-n-term-what-I-term-is-ik-I-1k/](https://www.geeksforgeeks.org/sum-of-series-till-n-th-term-whose-i-th-term-is-ik-i-1k/)

给定 N 和 k 的值，任务是找到直到第 N 项的级数和，第 I 项由 T<sub>I</sub>= I<sup>k</sup>+(I–1)<sup>k</sup>给出。因为级数的和可能非常大，所以以 1000000007 为模计算它的和。

**示例:**

```
Input : n = 5, k = 2
Output: 25
first 5 term of the series :
T1 = ( 1 )2 + ( 1 - 1 )2  = 1
T2 = ( 2 )2 + ( 2 - 1 )2  = 3
T3 = ( 3 )2 + ( 3 - 1 )2  = 5
T4 = ( 4 )2 + ( 4 - 1 )2  = 7
T4 = ( 5 )2 + ( 5 - 1 )2  = 9
Sum of the series = 1 + 3 + 5 + 7 + 9 =  25

Input: n = 4, k = 3
Output : 64
First 4 term of the series:
T2 = ( 1 )3 + ( 1 - 1 )3  = 1
T3 = ( 2 )3 + ( 2 - 1 )3  = 7
T4 = ( 3 )3 + ( 3 - 1 )3  = 19
T4 = ( 4 )3 + ( 4 - 1 )3  = 37
Sum of the series = 1 + 7 + 19 + 37 = 64 
```

**天真的方法**一个简单的解决方案是生成 n 个以下的所有术语并添加它们。时间复杂度将为 0(N)。由于 N 非常大，该方法将产生 TLE。

**更好的解决方案**
我们来看看系列图案。

> 考虑 N = 4， K = 3
> 则系列为:
> 1<sup>3</sup>–(1–1)<sup>3</sup>**+**2<sup>3</sup>–(2–1)<sup>3</sup>**+**1<sup>3</sup>–(3–1)<sup>3</sup>**+**4<sup>3</sup>–(4–1) <sup>3</sup>
> 即 1<sup>3</sup>–0<sup>3</sup>+2<sup>3</sup>–1<sup>3</sup>+3<sup>3</sup>–2<sup>3</sup>+4<sup>3</sup>–3<sup>3</sup>
> 将相同的异能改写在一起，我们得到。
> 0<sup>3</sup>+1<sup>3</sup>–1<sup>3</sup>+2<sup>3</sup>–2<sup>3</sup>+3<sup>3</sup>–3+4<sup>3</sup>T59】即~~0~~T62】3+~~1【T64 3–~~3~~<sup>3</sup>+4<sup>3</sup>
> 因此最终结果将是 4 <sup>3</sup> (即 n <sup>k</sup> )
> 因此最终公式为 N<sup>K</sup>T98】~~

下面是计算 N <sup>K</sup> 的天真方法。

## C++

```
// CPP Code to find sum of series

#include <bits/stdc++.h>
using namespace std;

#define MOD 1000000007

// function to calculate sum of series
int calculateSum(int n, int k)
{
    // Initialize result
    long long res = 1;

    // loop to calculate n^k
    for (int i = 0; i < k; i++) {
        res = (res * n) % MOD;
    }

    return res;
}

// Driver code
int main()
{
    int n = 4, k = 3;

    // function calling
    cout << calculateSum(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to find
// Sum of series

class GFG {

    // function to calculate sum of series
    static long calculateSum(int n, int k)
    {

        // Initialize res and MOD

        long res = 1;
        long MOD = 1000000007;

        // loop to calculate n^k % MOD
        for (int i = 0; i < k; i++) {

            res = (res * n) % MOD;
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 4;
        int k = 3;
        System.out.print(calculateSum(n, k));
    }
};
```

## 蟒蛇 3

```
# Python 3 code to find
# the sum of series

# function to calculate sum of series
def calculateSum(n, k):

    # initialize res
    res = 1

    # initialize MOD
    MOD = 1000000007

    # loop to calculate n ^ k % MOD
    for i in range ( 0, k):
        res = ( res * n ) % MOD

    return res

# Driver code
n = 4
k = 3

# function calling
print(calculateSum(n, k))
```

## C#

```
// C# code to find the
// sum of the series

using System;

class GFG {
    // function to calculate sum of the series
    static int calculateSum(int n, int k)
    {
        // initialize res
        int res = 1;

        // Initialize MOD
        int MOD = 1000000007;

        // loop to calculate n^k % MOD
        for (int i = 0; i < k; i++) {

            res = (res * n) % MOD;
        }
        return res;
    }

    // Driver Code
    static public void Main()
    {
        int n = 4;
        int k = 3;

        // function calling
        Console.WriteLine(calculateSum(n, k));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
// PHP code to find
// the sum of series

<?php

// function to calculate sum of the series
function calculateSum($n, $k)
{

    // Initialize res
    $res = 1;    

    // Initialize MOD
    $MOD = 1000000007;

    // loop to calculate n^k % MOD
    for( $i=0 ; $i < $k ; $i++)
    {
          $res =( $res * $n )% $MOD;
    }
    return $res;
}

// Driver Code
$n = 4;
$k = 3;

// function calling
echo calculateSum($n, $k);

?>
```

## java 描述语言

```
<script>
// javascript Code to find sum of series
const MOD = 1000000007;

// function to calculate sum of series
function calculateSum( n,  k)
{

    // Initialize result
    let res = 1;

    // loop to calculate n^k
    for (let i = 0; i < k; i++)
    {
        res = (res * n) % MOD;
    }
    return res;
}

// Driver code
    let n = 4, k = 3;

    // function calling
    document.write( calculateSum(n, k));

    // This code is contributed by gauravrajput1

</script>
```

**Output**

```
64
```

**时间复杂度** : O(K)
N <sup>K</sup> 可以用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)在 O(log N)中计算。

## C++

```
// CPP Code to find sum of series
#include <bits/stdc++.h>
using namespace std;

#define MOD 1000000007

// function to calculate sum of series
int calculateSum(int n, int k)
{
    // initialize res
    long long res = 1;

    // loop to calculate n^k % MOD
    // using modular Arithmetic
    while (k > 0) {

        // if k is odd
        // multiply it with res
        if (k & 1)
            res = (res * n) % MOD;

        // k must be even now
        // change k to k/2
        k = k / 2;

        // change n to  n^2
        n = (n * n) % MOD;
    }
    return res;
}

// Driver code
int main()
{
    int n = 4, k = 3;
    cout << calculateSum(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to find sum of series

class GFG {

    // Function to calculate sum of series
    static long calculateSum(int n, int k)
    {

        // initialize res and MOD
        int res = 1;
        int MOD = 1000000007;

        // loop to calculate n^k % MOD
        // using modular Arithmetic
        while (k > 0) {
            // if k is odd
            // multiply n with res
            if ((k & 1) == 1)
                res = (res * n) % MOD;

            // k must be even now
            // change k to k / 2
            k = k / 2;

            // change n to n^2
            n = (n * n) % MOD;
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, k = 3;
        System.out.print(calculateSum(n, k));
    }
};
```

## 蟒蛇 3

```
# Python code to calculate sum of series

# function to calculate sum of series
def calculateSum(n, k):

    # Initialize res
    res = 1

    # initialize MOD
    MOD = 1000000007

    # loop to calculate n ^ k % MOD
    # using Modular arithmetic
    while k > 0 :

          # if k is odd
          # Multiply n with res  
          if ( k & 1 ) == 1 :
              res = ( res * n ) % MOD

          # k must be even now
          # change k to k / 2
          k = k // 2

          # change n to n ^ 2
          n =( n * n ) % MOD

    return res

# Driver code

n = 4
k = 3

print(calculateSum(n, k))
```

## C#

```
// C# code to calculate
// sum of series

using System;

class GFG {

    // Function to calculate sum of series
    static int calculateSum(int n, int k)
    {
        int res = 1; // Initialize res

        int MOD = 1000000007;

        // Loop to calculate n^k % MOD
        while (k > 0) {
            // If y is odd
            // multiply  res with n
            if ((k & 1) == 1)
                res = (res * n) % MOD;

            // k must be even now
            // change k to k/2
            k = k / 2;

            // change n to n^2
            n = (n * n) % MOD;
        }
        return res;
    }

    // Driver Code
    static public void Main()
    {
        int n = 4;
        int k = 3;

        // Function calling
        Console.WriteLine(calculateSum(n, k));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
// PHP code to calculate
// Sum of series

<?php

// Function to calculate sum of series
function calculateSum($n, $k)
{

    // Initialize res
    $res = 1;    

    // Initialize MOD
    $MOD = 1000000007;

    // Loop to calculate n^k % MOD
    // using Modular arithmetic
    while ($k > 0)
    {

        // If y is odd
        // multiply with result
        if ($k & 1)
            $res = ( $res * $n ) % $MOD;

        // k must be even now
        // Change k to k/2 
        $k = $k / 2;

        // Change n to n^2
        $n =( $n * $n ) % $MOD;
    }
    return $res;
}

// Driver Code
$n = 4;
$k = 3;

// Function calling
echo calculateSum($n, $k);

?>
```

## java 描述语言

```
<script>
// javascript code to find sum of series

    // Function to calculate sum of series
    function calculateSum(n, k)
    {

        // initialize res and MOD
        let res = 1;
        let MOD = 1000000007;

        // loop to calculate n^k % MOD
        // using modular Arithmetic
        while (k > 0)
        {

            // if k is odd
            // multiply n with res
            if ((k & 1) == 1)
                res = (res * n) % MOD;

            // k must be even now
            // change k to k / 2
            k = parseInt(k / 2);

            // change n to n^2
            n = (n * n) % MOD;
        }
        return res;
    }

    // Driver code
    let n = 4, k = 3;
    document.write(calculateSum(n, k));

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
64
```

**时间复杂度:** O(log n)