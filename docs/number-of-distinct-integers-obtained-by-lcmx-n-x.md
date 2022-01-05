# LCM(X，N)/X

得到的不同整数个数

> 原文:[https://www . geesforgeks . org/distinct-integer-number-by-lcmx-n-x/](https://www.geeksforgeeks.org/number-of-distinct-integers-obtained-by-lcmx-n-x/)

给定一个数 N，求 **LCM** ***(X，N)/X*** 得到的不同整数个数，其中 X 可以是任意正数。

**示例**:

```
Input: N = 2  
Output: 2
if X is 1, then lcm(1, 2)/1 is 2/1=2\. 
if X is 2, then lcm(2, 2)/2 is 2/2=1\. 
For any X greater than 2 we cannot 
obtain a distinct integer.

Input: N = 3
Output: 2  
```

已知 **LCM(x，y) = x*y/GCD(x，y)** 。
因此，

```
lcm(X, N) = X*N/gcd(X, N)
or, lcm(X, N)/X = N/gcd(X, N)
```

所以只有![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")的相异因子才可能是相异的整数。因此，计算 N 的不同因子的数量，包括 1 和 N 本身，这是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ program to find distinct integers
// obtained by lcm(x, num)/x
#include <cmath>
#include <iostream>

using namespace std;

// Function to count the number of distinct
// integers obtained by lcm(x, num)/x
int numberOfDistinct(int n)
{
    int ans = 0;

    // iterate to count the number of factors
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            ans++;
            if ((n / i) != i)
                ans++;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int n = 3;

    cout << numberOfDistinct(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find distinct integers
// obtained by lcm(x, num)/x

import java.io.*;

class GFG {

// Function to count the number of distinct
// integers obtained by lcm(x, num)/x
static int numberOfDistinct(int n)
{
    int ans = 0;

    // iterate to count the number of factors
    for (int i = 1; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {
            ans++;
            if ((n / i) != i)
                ans++;
        }
    }

    return ans;
}

// Driver Code
    public static void main (String[] args) {
        int n = 3;

        System.out.println (numberOfDistinct(n));

    }
}
```

## 蟒蛇 3

```
# Python 3 program to find distinct integers
# obtained by lcm(x, num)/x

import math

# Function to count the number of distinct
# integers obtained by lcm(x, num)/x
def numberOfDistinct(n):
    ans = 0

    # iterate to count the number of factors
    for i in range( 1, int(math.sqrt(n))+1):
        if (n % i == 0) :
            ans += 1
            if ((n // i) != i):
                ans += 1
    return ans

# Driver Code
if __name__ == "__main__":
    n = 3

    print(numberOfDistinct(n))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to find distinct integers
// obtained by lcm(x, num)/x
using System;

class GFG
{

// Function to count the number
// of distinct integers obtained
// by lcm(x, num)/x
static int numberOfDistinct(int n)
{
    int ans = 0;

    // iterate to count the number
    // of factors
    for (int i = 1; i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0)
        {
            ans++;
            if ((n / i) != i)
                ans++;
        }
    }

    return ans;
}

// Driver Code
static public void Main ()
{
    int n = 3;
    Console.WriteLine(numberOfDistinct(n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find distinct
// integers obtained by lcm(x, num)/x

// Function to count the number
// of distinct integers obtained
// by lcm(x, num)/x
function numberOfDistinct($n)
{
    $ans = 0;

    // iterate to count the
    // number of factors
    for ($i = 1; $i <= sqrt($n); $i++)
    {
        if ($n % $i == 0)
        {
            $ans++;
            if (($n / $i) != $i)
                $ans++;
        }
    }

    return $ans;
}

// Driver Code
$n = 3;
echo numberOfDistinct($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript  program to find distinct integers
// obtained by lcm(x, num)/x    
// Function to count the number of distinct
    // integers obtained by lcm(x, num)/x
    function numberOfDistinct(n) {
        var ans = 0;

        // iterate to count the number of factors
        for (i = 1; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {
                ans++;
                if ((n / i) != i)
                    ans++;
            }
        }

        return ans;
    }

    // Driver Code

        var n = 3;

        document.write(numberOfDistinct(n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(sqrt(n))