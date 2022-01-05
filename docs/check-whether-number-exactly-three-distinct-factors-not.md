# 检查一个数字是否有三个截然不同的因素

> 原文:[https://www . geesforgeks . org/check-when-number-just-三个不同的因素-not/](https://www.geeksforgeeks.org/check-whether-number-exactly-three-distinct-factors-not/)

给定正整数 n(1 <= n <= 10 <sup>18</sup> )。检查一个数字是否有三个截然不同的因素。打印“**是**”否则打印“**否**”。

**示例:**

```
Input : 9
Output: Yes
Explanation
Number 9 has exactly three factors:
1, 3, 9, hence answer is 'Yes'

Input  : 10
Output : No
```

**简单方法**就是用这种方法生成一个数的所有除数来计数因子，之后检查所有因子的计数是否等于‘3’。这种方法的时间复杂度为 O(sqrt(n))。

**更好的方法**是用**数论**。根据完美正方形的性质，“*每个完美正方形(x <sup>2</sup> )总是只有奇数个因子*”。

如果给定数的平方根(比如 x <sup>2</sup> )是素数(在确定该数是完美平方之后)，那么它必须正好有三个不同的因子，

1.  一个数字 **1** 当然。
2.  一个数的平方根，即 **x** (质数)。
3.  数字本身即**x<sup>2</sup>T3。**

下面是上述方法的实现:

## C++

```
// C++ program to check whether number
// has exactly three distinct factors
// or not
#include <bits/stdc++.h>
using namespace std;

// Utility function to check whether a
// number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check whether given number
// has three distinct factors or not
bool isThreeDisctFactors(long long n)
{
    // Find square root of number
    int sq = (int)sqrt(n);

    // Check whether number is perfect
    // square or not
    if (1LL * sq * sq != n)
        return false;

    // If number is perfect square, check
    // whether square root is prime or
    // not
    return isPrime(sq) ? true : false;
}

// Driver program
int main()
{
    long long num = 9;
    if (isThreeDisctFactors(num))
        cout << "Yes\n";
    else
        cout << "No\n";

    num = 15;
    if (isThreeDisctFactors(num))
        cout << "Yes\n";
    else
        cout << "No\n";

    num = 12397923568441;
    if (isThreeDisctFactors(num))
        cout << "Yes\n";
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether number
// has exactly three distinct factors
// or not
public class GFG {

// Utility function to check whether a
// number is prime or not
static boolean isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check whether given number
// has three distinct factors or not
static boolean isThreeDisctFactors(long n)
{
    // Find square root of number
    int sq = (int)Math.sqrt(n);

    // Check whether number is perfect
    // square or not
    if (1L * sq * sq != n)
        return false;

    // If number is perfect square, check
    // whether square root is prime or
    // not
    return isPrime(sq) ? true : false;
}

// Driver program
    public static void main(String[] args) {
        long num = 9;
    if (isThreeDisctFactors(num))
        System.out.println("Yes");
    else
        System.out.println("No");

    num = 15;
    if (isThreeDisctFactors(num))
        System.out.println("Yes");
    else
        System.out.println("No");

    num = 12397923568441L;
    if (isThreeDisctFactors(num))
        System.out.println("Yes");
    else
        System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check whether number
# has exactly three distinct factors
# or not

from math import sqrt
# Utility function to check whether a
# number is prime or not
def isPrime(n):
    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    k= int(sqrt(n))+1
    for i in range(5,k,6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# Function to check whether given number
# has three distinct factors or not
def isThreeDisctFactors(n):
    # Find square root of number
    sq = int(sqrt(n))

    # Check whether number is perfect
    # square or not
    if (1 * sq * sq != n):
        return False

    # If number is perfect square, check
    # whether square root is prime or
    # not
    if (isPrime(sq)):
        return True
    else:
        return False

# Driver program
if __name__ == '__main__':
    num = 9
    if (isThreeDisctFactors(num)):
        print("Yes")
    else:
        print("No")

    num = 15
    if (isThreeDisctFactors(num)):
        print("Yes")
    else:
        print("No")

    num = 12397923568441
    if (isThreeDisctFactors(num)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check whether number
// has exactly three distinct factors
// or not
using System;

public class GFG {

    // Utility function to check whether
    // a number is prime or not
    static bool isPrime(int n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can
        // skip middle five numbers in
        // below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to check whether given number
    // has three distinct factors or not
    static bool isThreeDisctFactors(long n)
    {

        // Find square root of number
        int sq = (int)Math.Sqrt(n);

        // Check whether number is perfect
        // square or not
        if (1LL * sq * sq != n)
            return false;

        // If number is perfect square, check
        // whether square root is prime or
        // not
        return isPrime(sq) ? true : false;
    }

    // Driver program
    static public void Main()
    {
        long num = 9;
        if (isThreeDisctFactors(num))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        num = 15;
        if (isThreeDisctFactors(num))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        num = 12397923568441;
        if (isThreeDisctFactors(num))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// number has exactly three
// distinct factors or not

// Utility function to check
// whether a number is prime
// or not
function isPrime($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n;
                   $i = $i + 6)
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
            return false;

    return true;
}

// Function to check
// whether given number
// has three distinct
// factors or not
function isThreeDisctFactors($n)
{
    // Find square root of number
    $sq = sqrt($n);

    // Check whether number is
    // perfect square or not
    if ($sq * $sq != $n)
        return false;

    // If number is perfect square,
    // check whether square root is
    // prime or not
    return isPrime($sq) ? true : false;
}

// Driver Code
$num = 9;
if (isThreeDisctFactors($num))
    echo "Yes\n";
else
    echo "No\n";

$num = 15;
if (isThreeDisctFactors($num))
    echo "Yes\n";
else
    echo "No\n";

$num = 12397923568441;
if (isThreeDisctFactors($num))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by ak_t
?>
```

## java 描述语言

```
<script>

// Javascript program to check whether
// number has exactly three distinct
// factors or not

// Utility function to check whether a
// number is prime or not
function isPrime(n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check whether given number
// has three distinct factors or not
function isThreeDisctFactors(n)
{

    // Find square root of number
    let sq = parseInt(Math.sqrt(n));

    // Check whether number is perfect
    // square or not
    if (sq * sq != n)
        return false;

    // If number is perfect square, check
    // whether square root is prime or
    // not
    return isPrime(sq) ? true : false;
}

// Driver code
let num = 9;
if (isThreeDisctFactors(num))
    document.write("Yes<br>");
else
    document.write("No<br>");

num = 15;
if (isThreeDisctFactors(num))
    document.write("Yes<br>");
else
    document.write("No<br>");

num = 12397923568441;
if (isThreeDisctFactors(num))
    document.write("Yes<br>");
else
    document.write("No<br>");

// This code is contributed by souravmahato348 

</script>
```

**输出:**

```
Yes
No
No
```

**时间复杂度:**O(n<sup>1/4</sup>)
T5】辅助空间: O(1)

本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。-