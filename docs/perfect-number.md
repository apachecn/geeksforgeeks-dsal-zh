# 完全数

> 原文:[https://www.geeksforgeeks.org/perfect-number/](https://www.geeksforgeeks.org/perfect-number/)

如果一个数等于它的适当除数之和，也就是它的正除数之和而不包括数本身，那么这个数就是一个完全数。编写一个函数来检查给定的数字是否完美。
**例:**

```
Input: n = 15
Output: false
Divisors of 15 are 1, 3 and 5\. Sum of 
divisors is 9 which is not equal to 15.

Input: n = 6
Output: true
Divisors of 6 are 1, 2 and 3\. Sum of 
divisors is 6.
```

一个**简单的解决方法**就是把从 1 到 n-1 的每一个数都过一遍，检查它是不是除数。保持所有因子的和。如果和等于 n，则返回真，否则返回假。
一个**有效的解决方案**是通过数直到 n 的平方根。如果一个数“I”除以 n，然后将“I”和 n/i 相加。
下面是高效解决方案的实现。

## C++

```
// C++ program to check if a given number is perfect
// or not
#include<iostream>
using namespace std;

// Returns true if n is perfect
bool isPerfect(long long int n)
{
    // To store sum of divisors
    long long int sum = 1;

    // Find all divisors and add them
    for (long long int i=2; i*i<=n; i++)
    {
        if (n%i==0)
        {
            if(i*i!=n)
                sum = sum + i + n/i;
            else
                sum=sum+i;
        }
    }
     // If sum of divisors is equal to
     // n, then n is a perfect number
     if (sum == n && n != 1)
          return true;

     return false;
}

// Driver program
int main()
{
    cout << "Below are all perfect numbers till 10000\n";
    for (int n =2; n<10000; n++)
        if (isPerfect(n))
            cout << n << " is a perfect number\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// number is perfect or not
class GFG
{

// Returns true if n is perfect
static boolean isPerfect(int n)
{
    // To store sum of divisors
    int sum = 1;

    // Find all divisors and add them
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i==0)
        {
            if(i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }
    // If sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Driver program
public static void main (String[] args)
{
    System.out.println("Below are all perfect" +
                                "numbers till 10000");
    for (int n = 2; n < 10000; n++)
        if (isPerfect(n))
            System.out.println( n +
                    " is a perfect number");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 code to check if a given
# number is perfect or not

# Returns true if n is perfect
def isPerfect( n ):

    # To store sum of divisors
    sum = 1

    # Find all divisors and add them
    i = 2
    while i * i <= n:
        if n % i == 0:
            sum = sum + i + n/i
        i += 1

    # If sum of divisors is equal to
    # n, then n is a perfect number

    return (True if sum == n and n!=1 else False)

# Driver program
print("Below are all perfect numbers till 10000")
n = 2
for n in range (10000):
    if isPerfect (n):
        print(n , " is a perfect number")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to check if a given
// number is perfect or not

class GFG
{

// Returns true if n is perfect
static bool isPerfect(int n)
{
    // To store sum of divisors
    int sum = 1;

    // Find all divisors and add them
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i==0)
        {
            if(i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }
    // If sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Driver program
static void Main()
{
    System.Console.WriteLine("Below are all perfect" +
                                "numbers till 10000");
    for (int n = 2; n < 10000; n++)
        if (isPerfect(n))
            System.Console.WriteLine( n +
                    " is a perfect number");
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given number
// is perfect or not

// Returns true if n is perfect
function isPerfect($n)
{
    // To store sum of divisors
    $sum = 1;

    // Find all divisors and add them
    for ($i = 2; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            if($i * $i != $n)
                $sum = $sum + $i + (int)($n / $i);
            else
                $sum = $sum + $i;
        }
    }
    // If sum of divisors is equal to
    // n, then n is a perfect number
    if ($sum == $n && $n != 1)
        return true;

    return false;
}

// Driver Code
echo "Below are all perfect numbers till 10000\n";
for ($n = 2; $n < 10000; $n++)
    if (isPerfect($n))
        echo "$n is a perfect number\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a given number is perfect
// or not

// Returns true if n is perfect
function isPerfect(n)
{
    // To store sum of divisors
    sum = 1;

    // Find all divisors and add them
    for (let i=2; i*i<=n; i++)
    {
        if (n%i==0)
        {
            if(i*i!=n)
                sum = sum + i + n/i;
            else
                sum=sum+i;
        }
    }
    // If sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Driver program

    document.write("Below are all perfect numbers till 10000" + "<br>");
    for (let n =2; n<10000; n++)
        if (isPerfect(n))
            document.write(n + " is a perfect number" + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Below are all perfect numbers till 10000
6 is a perfect number
28 is a perfect number
496 is a perfect number
8128 is a perfect number
```

**时间复杂度:** √n
下面是一些关于完全数的有趣事实:
1)每个偶数完全数都是 2*T5【p*T8】的形式？1 (2 *<sup>p</sup>* ？1)2*<sup>p</sup>*在哪里？1 是质数。
2)是否有奇数完全数未知。
**参考文献:**
[https://en.wikipedia.org/wiki/Perfect_number](https://en.wikipedia.org/wiki/Perfect_number)
如发现有不正确的地方，请写评论，或者想分享以上讨论话题的更多信息