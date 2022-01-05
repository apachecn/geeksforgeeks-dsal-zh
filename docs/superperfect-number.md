# 超级完美号

> 原文:[https://www.geeksforgeeks.org/superperfect-number/](https://www.geeksforgeeks.org/superperfect-number/)

给定一个整数 n，检查数字 **n** 是否为超完美数字。超完美数是满足σ <sup>2</sup> (n) = σ(σ(n)) = 2n 的正整数，其中σ是[除数求和](https://en.wikipedia.org/wiki/Divisor_summatory_function)函数。

```
Input: n = 16
Output: yes
Explanation:
16 is a superperfect number as σ(16) = 1 + 2 + 4 + 8 + 16 = 31,
and σ(31) = 1 + 31 = 32, 
thus σ(σ(16)) = 32 = 2 × 16.

Input: n = 8
Output: no 
Explanation:
σ(8) = 1 + 2 + 4 + 8 = 15
and σ(15) = 1 + 3 + 5 + 15 = 24
thus ( σ(σ(8)) = 24 ) ≠ (2 * 8 = 26)
```

We strongly recommend that you click here and practice it, before moving on to the solution.

这个想法很简单。我们只需从 1 迭代到 sqrt(n)并求出 n 的所有除数之和，我们称这个和为 n1。现在我们再次需要从 1 迭代到 sqrt(n1)并找到所有除数的和。之后我们只需要检查结果和是否等于 2*n。

## C++

```
// C++ program to check whether number is
// superperfect or not
#include<bits/stdc++.h>
using namespace std;

// Function to calculate sum of all divisors
int divSum(int num)
{
    // Final result of summation of divisors
    int result = 0;

    // find all divisors which divides 'num'
    for (int i=1; i*i <= num; ++i)
    {
        // if 'i' is divisor of 'num'
        if (num%i == 0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i == (num/i))
                result += i;
            else
                result += (i + num/i);
        }
    }

    return result;
}

// Returns true if n is Super Perfect else false.
bool isSuperPerfect(int n)
{
    // Find the sum of all divisors of number n
    int n1 = divSum(n);

    // Again find the sum of all divisors of n1
    // and check if sum is equal to n1
    return (2*n == divSum(n1));
}

//Driver code
int main()
{
    int n = 16;
    cout << (isSuperPerfect(n) ? "Yes\n" : "No\n");

    n = 6;
    cout << (isSuperPerfect(n) ? "Yes\n" : "No\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether number is
// superperfect or not

public class Divisors
{
    // Function to calculate sum of all divisors
    static int divSum(int num)
    {
        // Final result of summation of divisors
        int result = 0;

        // find all divisors which divides 'num'
        for (int i=1; i*i <= num; ++i)
        {
            // if 'i' is divisor of 'num'
            if (num%i == 0)
            {
                // if both divisors are same then add
                // it only once else add both
                if (i == (num/i))
                    result += i;
                else
                    result += (i + num/i);
            }
        }
        return result;
    }

    // Returns true if n is Super Perfect else false.
    static boolean isSuperPerfect(int n)
    {
        // Find the sum of all divisors of number n
        int n1 = divSum(n);
        // Again find the sum of all divisors of n1
        // and check if sum is equal to n1
        return (2*n == divSum(n1));
    }

    public static void main (String[] args)
    {
        int n = 16;
        System.out.printf((isSuperPerfect(n) ? "Yes\n" : "No\n"));

        n = 6;
        System.out.printf((isSuperPerfect(n) ? "Yes\n" : "No\n"));
    }
}

// This code is contributed by Saket Kumar
```

## 计算机编程语言

```
# Python program to check whether number
# is superperfect or not
import math

# Function to calculate sum of all divisors
def divSum(num):

    # Final result of summation of divisors
    result = 0

    # find all divisors which divides 'num'
    sq = int(math.sqrt(num))
    for i in xrange(1, sq+1):

        # if 'i' is divisor of 'num'
        if num %i == 0:

            # if both divisors are same then add
            # it only once else add both
            if i == (num/i):
                result += i
            else:
                result += (i + num/i)

    return result

# Returns true if n is superperfect else false
def isSuperPerfect(n):

    # Find the sum of all divisors of number n
    n1 = divSum(n)

    # Again find the sum of all divisors of n1
    return divSum(n1) == 2*n

#Driver code
n = 16
print 'Yes' if isSuperPerfect(n) else 'No'

n = 6
print 'Yes' if isSuperPerfect(n) else 'No'
```

## C#

```
// C# program to check whether number is
// superperfect or not
using System;

class Divisors
{
    // Function to calculate sum of all divisors
    static int divSum(int num)
    {
        // Final result of summation of divisors
        int result = 0;

        // find all divisors which divides 'num'
        for (int i = 1; i * i <= num; ++i)
        {
            // if 'i' is divisor of 'num'
            if (num % i == 0)
            {
                // if both divisors are same then add
                // it only once else add both
                if (i == (num / i))
                    result += i;
                else
                    result += (i + num / i);
            }
        }
        return result;
    }

    // Returns true if n is Super Perfect else false.
    static bool isSuperPerfect(int n)
    {
        // Find the sum of all divisors of number n
        int n1 = divSum(n);
        // Again find the sum of all divisors of n1
        // and check if sum is equal to n1
        return (2 * n == divSum(n1));
    }

    public static void Main ()
    {
        int n = 16;
        Console.WriteLine((isSuperPerfect(n) ? "Yes" : "No"));

        n = 6;
        Console.WriteLine((isSuperPerfect(n) ? "Yes" : "No"));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// number is superperfect or not

// Function to calculate
// sum of all divisors
function divSum($num)
{

    // Final result of
    // summation of divisors
    $result = 0;

    // find all divisors
    // which divides 'num'
    for ($i = 1; $i * $i <= $num; ++$i)
    {

        // if 'i' is divisor
        // of 'num'
        if ($num % $i == 0)
        {

            // if both divisors
            // are same then add
            // it only once else
            // add both
            if ($i == ($num / $i))
                $result += $i;
            else
                $result += ($i + $num/$i);
        }
    }

    return $result;
}

// Returns true if n is
// Super Perfect else false.
function isSuperPerfect($n)
{

    // Find the sum of all
    // divisors of number n
    $n1 = divSum($n);

    // Again find the sum
    // of all divisors of n1
    // and check if sum is
    // equal to n1
    return (2 * $n == divSum($n1));
}

    // Driver code
    $n = 16;
    $hh = (isSuperPerfect($n) ? "Yes\n" : "No\n");
        echo($hh);

    $n = 6;
    $hh=(isSuperPerfect($n) ? "Yes\n" : "No\n");
        echo($hh);

// This code is contributed by AJit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to calculate sum of all divisors
    function divSum(num)
    {

        // Final result of summation of divisors
        let result = 0;

        // find all divisors which divides 'num'
        for (let i = 1; i * i <= num; ++i)
        {

            // if 'i' is divisor of 'num'
            if (num % i == 0)
            {

                // if both divisors are same then add
                // it only once else add both
                if (i == (num/i))
                    result += i;
                else
                    result += (i + num/i);
            }
        }
        return result;
    }

    // Returns true if n is Super Perfect else false.
    function isSuperPerfect(n)
    {

        // Find the sum of all divisors of number n
        let n1 = divSum(n);

        // Again find the sum of all divisors of n1
        // and check if sum is equal to n1
        return (2*n == divSum(n1));
    }

// Driver Code   
      let n = 16;
      document.write((isSuperPerfect(n) ? "Yes\n" : "No\n") + "<br />");

       n = 6;
      document.write((isSuperPerfect(n) ? "Yes\n" : "No\n") + "<br />");

// This code is contributed by splevel62.
</script>
```

```
Output:
Yes
No
```

**时间复杂度:** O(sqrt(n + n1))其中 n1 是 n 的除数之和
**辅助空间:** O(1)
**关于超数的事实:**

1.  如果 n 是偶数超完全数，那么 n 必须是 2 的幂，即 2 <sup>k</sup> ，这样 2<sup>k+1</sup>–1 就是一个[梅森素数](https://en.wikipedia.org/wiki/Mersenne_prime)。
2.  不知道是否有奇数个超完美数。奇数超完美数 n 必须是平方数，这样 n 或σ(n)至少可以被三个不同的素数整除。7×10 <sup>24</sup> 以下没有奇数个超完美数

**参考:**
https://en.wikipedia.org/wiki/Superperfect_number
本文由[舒巴姆班萨尔](https://www.facebook.com/banalshubham)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。