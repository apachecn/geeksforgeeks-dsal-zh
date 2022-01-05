# 求最小值 x，使得(x % k)*(x/k)= n

> 原文:[https://www . geesforgeks . org/find-minimum-x-so-x-k-x-k-n/](https://www.geeksforgeeks.org/find-minimum-x-such-that-x-k-x-k-n/)

给定两个正整数 n 和 k，求最小正整数 x，使得(x % k) * (x / k) == n，其中%是模运算符，/是整数除法运算符。
**例:**

```
Input : n = 4, k = 6
Output :10
Explanation : (10 % 6) * (10 / 6) = (4) * (1) = 4 which is equal to n

Input : n = 5, k = 5
Output : 26
```

**天真的解决方案:**一个简单的方法是运行 while 循环，直到我们找到满足给定方程的解决方案，但这将非常慢。
**高效解决方案:**这里的关键思想是注意(x % k)的值在[1，k–1]的范围内。(不包括 0，因为当它为零时，我们不能用(x % k)除 n)。现在，我们需要在除 n 的范围内找到最大的可能数，因此给定的方程变成 x = (n * k) / (x % k) + (x % k)。
**注意:** (x % k)被添加到答案中，因为对于模的当前值(x % k)，它必须不矛盾，一方面 x 是这样的，即除以 k 后的余数是(x % k)，另一方面 x 是(n * k) / (x % k)，当我们将该值除以 k 时，余数简单为零。
下面是上述方法的实现。

## C++

```
// CPP Program to find the minimum
// positive X such that the given
// equation holds true
#include <bits/stdc++.h>
using namespace std;

// This function gives the required
// answer
int minimumX(int n, int k)
{
    int ans = INT_MAX;

    // Iterate over all possible
    // remainders
    for (int rem = k - 1; rem > 0; rem--) {

        // it must divide n
        if (n % rem == 0)
            ans = min(ans, rem + (n / rem) * k);
    }
    return ans;
}

// Driver Code to test above function
int main()
{
    int n = 4, k = 6;
    cout << minimumX(n, k) << endl;

    n = 5, k = 5;
    cout << minimumX(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum
// positive X such that the given
// equation holds true
class Solution
{
// This function gives the required
// answer
static int minimumX(int n, int k)
{
    int ans =Integer.MAX_VALUE;

    // Iterate over all possible
    // remainders
    for (int rem = k - 1; rem > 0; rem--) {

        // it must divide n
        if (n % rem == 0)
            ans = Math.min(ans, rem + (n / rem) * k);
    }
    return ans;
}

// Driver Code to test above function
public static void main(String args[])
{
    int n = 4, k = 6;
    System.out.println( minimumX(n, k));

    n = 5; k = 5;
    System.out.println(minimumX(n, k));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find the minimum positive
# x such that the given equation holds true

# This function gives the required answer
def minimumX(n, k):

    ans = 10 ** 18

    # Iterate over all possible remainders
    for i in range(k - 1, 0, -1):
        if n % i == 0:
            ans = min(ans, i + (n / i) * k)
    return ans

# Driver Code
n, k = 4, 6

print(minimumX(n, k))

n, k = 5, 5

print(minimumX(n, k))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# Program to find the minimum
// positive X such that the given
// equation holds true

using System;

public class GFG{
    // This function gives the required
// answer
static int minimumX(int n, int k)
{
    int ans =int.MaxValue;

    // Iterate over all possible
    // remainders
    for (int rem = k - 1; rem > 0; rem--) {

        // it must divide n
        if (n % rem == 0)
            ans = Math.Min(ans, rem + (n / rem) * k);
    }
    return ans;
}

// Driver Code to test above function
    static public void Main (){
        int n = 4, k = 6;
        Console.WriteLine( minimumX(n, k));

        n = 5; k = 5;
        Console.WriteLine(minimumX(n, k));

}
}
//This code is contributed by Sachin.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the minimum
// positive X such that the given
// equation holds true

// This function gives the required
// answer
function minimumX($n, $k)
{
    $ans = PHP_INT_MAX;

    // Iterate over all possible
    // remainders
    for ($rem = $k - 1; $rem > 0; $rem--)
    {

        // it must divide n
        if ($n % $rem == 0)
            $ans = min($ans, $rem +
                      ($n / $rem) * $k);
    }
    return $ans;
}

// Driver Code
$n = 4 ;
$k = 6 ;

echo minimumX($n, $k), "\n" ;

$n = 5 ;
$k = 5 ;

echo minimumX($n, $k) ;

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find the minimum
    // positive X such that the given
    // equation holds true

    // This function gives the required
    // answer
    function minimumX(n, k)
    {
        let ans = Number.MAX_VALUE;

        // Iterate over all possible
        // remainders
        for (let rem = k - 1; rem > 0; rem--) {

            // it must divide n
            if (n % rem == 0)
                ans = Math.min(ans, rem + (n / rem) * k);
        }
        return ans;
    }

// Driver code to test above function   
    let n = 4, k = 6;
    document.write(minimumX(n, k) + "</br>");

    n = 5, k = 5;
    document.write(minimumX(n, k));

</script>
```

**Output:** 

```
10
26
```

**时间复杂度:** O(k)，其中 k 是给定的正整数。