# 一个自然数的所有适当除数之和

> 原文:[https://www . geeksforgeeks . org/自然数整除之和/](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)

给定一个自然数，计算其所有适当除数的和。自然数的适当除数是严格小于该数的除数。
**例如**，数 20 有 5 个适当的除数:1、2、4、5、10，除数求和为:1 + 2 + 4 + 5 + 10 = 22。
**示例:**

```
Input : num = 10
Output: 8
// proper divisors 1 + 2 + 5 = 8 

Input : num = 36
Output: 55
// proper divisors 1 + 2 + 3 + 4 + 6 + 9 + 12 + 18 = 55 
```

这个问题有非常**简单的解法**，我们都知道对于任意一个数‘num’它的所有除数总是小于等于‘num/2’，所有质因数总是小于等于 **sqrt(num)** 。所以我们迭代‘I’直到 i < =sqrt(num)并且对于任何‘I’如果它除‘num’，那么我们得到两个除数‘I’和‘num/I’，连续地相加这些除数但是对于一些数字，除数‘I’和‘num/I’在这种情况下将相同，仅仅相加一个除数，例如；num=36 所以对于 i=6，我们将得到(num/i)=6，这就是为什么我们将在求和中只得到一次 6。最后我们加一，因为一是所有自然数的除数。

## C++

```
// C++ program to find sum of all divisors of
// a natural number
#include<bits/stdc++.h>
using namespace std;

// Function to calculate sum of all proper divisors
// num --> given natural number
int divSum(int num)
{
    // Final result of summation of divisors
    int result = 0;
    if(num == 1) // there will be no proper divisor
      return result;
    // find all divisors which divides 'num'
    for (int i=2; i<=sqrt(num); i++)
    {
        // if 'i' is divisor of 'num'
        if (num%i==0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i==(num/i))
                result += i;
            else
                result += (i + num/i);
        }
    }

    // Add 1 to the result as 1 is also a divisor
    return (result + 1);
}

// Driver program to run the case
int main()
{
    int num = 36;
    cout << divSum(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find sum of all divisors
// of a natural number
import java.math.*;

class GFG {

    // Function to calculate sum of all proper
    // divisors num --> given natural number
    static int divSum(int num)
    {
        // Final result of summation of divisors
        int result = 0;

        // find all divisors which divides 'num'
        for (int i = 2; i <= Math.sqrt(num); i++)
        {
            // if 'i' is divisor of 'num'
            if (num % i == 0)
            {
                // if both divisors are same then
                // add it only once else add both
                if (i == (num / i))
                    result += i;
                else
                    result += (i + num / i);
            }
        }

        // Add 1 to the result as 1 is also
        // a divisor
        return (result + 1);
    }

    // Driver program to run the case
    public static void main(String[] args)
    {
        int num = 36;
        System.out.println(divSum(num));
    }
}

/*This code is contributed by Nikita Tiwari*/
```

## 计算机编程语言

```
# PYTHON program to find sum of all
# divisors of a natural number
import math

# Function to calculate sum of all proper
# divisors num --> given natural number
def divSum(num) :

    # Final result of summation of divisors
    result = 0

    # find all divisors which divides 'num'
    i = 2
    while i<= (math.sqrt(num)) :

        # if 'i' is divisor of 'num'
        if (num % i == 0) :

            # if both divisors are same then
            # add it only once else add both
            if (i == (num / i)) :
                result = result + i;
            else :
                result = result +  (i + num/i);
        i = i + 1

    # Add 1 to the result as 1 is also
    # a divisor
    return (result + 1);

# Driver program to run the case
num = 36
print (divSum(num))

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to find sum of all
// divisorsof a natural number
using System;

class GFG {

    // Function to calculate sum of all proper
    // divisors num --> given natural number
    static int divSum(int num)
    {

        // Final result of summation of divisors
        int result = 0;

        // find all divisors which divides 'num'
        for (int i = 2; i <= Math.Sqrt(num); i++)
        {

            // if 'i' is divisor of 'num'
            if (num % i == 0)
            {

                // if both divisors are same then
                // add it only once else add both
                if (i == (num / i))
                    result += i;
                else
                    result += (i + num / i);
            }
        }

        // Add 1 to the result as 1
        // is also a divisor
        return (result + 1);
    }

    // Driver Code
    public static void Main()
    {
        int num = 36;
        Console.Write(divSum(num));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// all divisors of a natural number

// Function to calculate sum of
// all proper divisors
// num --> given natural number
function divSum($num)
{
    // Final result of
    // summation of divisors
    $result = 0;

    // find all divisors
    // which divides 'num'
    for ($i = 2; $i <= sqrt($num);
                 $i++)
    {
        // if 'i' is divisor of 'num'
        if ($num % $i == 0)
        {
            // if both divisors are
            // same then add it only
            // once else add both
            if ($i == ($num / $i))
                $result += $i;
            else
                $result += ($i + $num / $i);
        }
    }

    // Add 1 to the result as
    // 1 is also a divisor
    return ($result + 1);
}

// Driver Code
$num = 36;
echo(divSum($num));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of all divisors of
// a natural number

// Function to calculate sum of all proper divisors
// num --> given natural number
function divSum(num)
{
    // Final result of summation of divisors
    let result = 0;

    // find all divisors which divides 'num'
    for (let i=2; i<=Math.sqrt(num); i++)
    {
        // if 'i' is divisor of 'num'
        if (num%i==0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i==(num/i))
                result += i;
            else
                result += (i + num/i);
        }
    }

    // Add 1 to the result as 1 is also a divisor
    return (result + 1);
}

// Driver program to run the case

    let num = 36;
    document.write(divSum(num));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
55
```

请参考下面的帖子，以获得优化的解决方案和公式。
[**一个数的所有因子之和的高效解**](https://www.geeksforgeeks.org/sum-factors-number/)
本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。