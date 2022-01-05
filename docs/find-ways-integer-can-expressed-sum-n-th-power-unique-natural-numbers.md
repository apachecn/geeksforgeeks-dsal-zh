# 寻找一个整数可以表示为唯一自然数的 n 次方的和的方法

> 原文:[https://www . geesforgeks . org/find-way-integer-can-expressed-sum-n-th-power-unique-natural-numbers/](https://www.geeksforgeeks.org/find-ways-integer-can-expressed-sum-n-th-power-unique-natural-numbers/)

给定两个数字 x 和 n，找出 x 可以表示为唯一自然数的 n 次幂之和的几种方法。

**示例:**

> **输入:** x = 10，n = 2
> **输出:** 1
> **解释:** 10 = 1 <sup>2</sup> + 3 <sup>2</sup> ，因此共有 1 种可能性
> 
> **输入:** x = 100，n = 2
> **输出:** 3
> E **解释:**
> 100 = 10<sup>2</sup>OR 6<sup>2</sup>+8<sup>2</sup>OR 1<sup>2</sup>+3<sup>2</sup>+4<sup>2</sup>+5<sup>2</sup>+

想法很简单。我们从 1 开始遍历所有数字。对于每个数字，我们递归地尝试所有更大的数字，如果我们能够找到和，我们增加结果

## C++

```
// C++ program to count number of ways any
// given integer x can be expressed as n-th
// power of unique natural numbers.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and return the
// power of any given number
int power(int num, unsigned int n)
{
    if (n == 0)
        return 1;
    else if (n % 2 == 0)
        return power(num, n / 2) * power(num, n / 2);
    else
        return num * power(num, n / 2) * power(num, n / 2);
}

// Function to check power representations recursively
int checkRecursive(int x, int n, int curr_num = 1,
                   int curr_sum = 0)
{
    // Initialize number of ways to express
    // x as n-th powers of different natural
    // numbers
    int results = 0;

    // Calling power of 'i' raised to 'n'
    int p = power(curr_num, n);
    while (p + curr_sum < x) {
        // Recursively check all greater values of i
        results += checkRecursive(x, n, curr_num + 1,
                                  p + curr_sum);
        curr_num++;
        p = power(curr_num, n);
    }

    // If sum of powers is equal to x
    // then increase the value of result.
    if (p + curr_sum == x)
        results++;

    // Return the final result
    return results;
}

// Driver Code.
int main()
{
    int x = 10, n = 2;
    cout << checkRecursive(x, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways any
// given integer x can be expressed as n-th
// power of unique natural numbers.

class GFG {

    // Function to calculate and return the
    // power of any given number
    static int power(int num, int n)
    {
        if (n == 0)
            return 1;
        else if (n % 2 == 0)
            return power(num, n / 2) * power(num, n / 2);
        else
            return num * power(num, n / 2)
                * power(num, n / 2);
    }

    // Function to check power representations recursively
    static int checkRecursive(int x, int n, int curr_num,
                              int curr_sum)
    {
        // Initialize number of ways to express
        // x as n-th powers of different natural
        // numbers
        int results = 0;

        // Calling power of 'i' raised to 'n'
        int p = power(curr_num, n);
        while (p + curr_sum < x) {
            // Recursively check all greater values of i
            results += checkRecursive(x, n, curr_num + 1,
                                      p + curr_sum);
            curr_num++;
            p = power(curr_num, n);
        }

        // If sum of powers is equal to x
        // then increase the value of result.
        if (p + curr_sum == x)
            results++;

        // Return the final result
        return results;
    }

    // Driver Code.
    public static void main(String[] args)
    {
        int x = 10, n = 2;
        System.out.println(checkRecursive(x, n, 1, 0));
    }
}

// This code is contributed by mits
```

## 计算机编程语言

```
# Python3 program to count number of ways any
# given integer x can be expressed as n-th
# power of unique natural numbers.

# Function to calculate and return the
# power of any given number

def power(num, n):

    if(n == 0):
        return 1
    elif(n % 2 == 0):
        return power(num, n // 2) * power(num, n // 2)
    else:
        return num * power(num, n // 2) * power(num, n // 2)

# Function to check power representations recursively

def checkRecursive(x, n, curr_num=1, curr_sum=0):

    # Initialize number of ways to express
    # x as n-th powers of different natural
    # numbers
    results = 0

    # Calling power of 'i' raised to 'n'
    p = power(curr_num, n)
    while(p + curr_sum < x):

        # Recursively check all greater values of i
        results += checkRecursive(x, n, curr_num + 1, p + curr_sum)
        curr_num = curr_num + 1
        p = power(curr_num, n)

    # If sum of powers is equal to x
    # then increase the value of result.
    if(p + curr_sum == x):
        results = results + 1

    # Return the final result
    return results

# Driver Code.
if __name__ == '__main__':
    x = 10
    n = 2
    print(checkRecursive(x, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count number of ways any
// given integer x can be expressed as
// n-th power of unique natural numbers.
using System;

class GFG {

    // Function to calculate and return
    // the power of any given number
    static int power(int num, int n)
    {
        if (n == 0)
            return 1;
        else if (n % 2 == 0)
            return power(num, n / 2) * power(num, n / 2);
        else
            return num * power(num, n / 2)
                * power(num, n / 2);
    }

    // Function to check power
    // representations recursively
    static int checkRecursive(int x, int n, int curr_num,
                              int curr_sum)
    {
        // Initialize number of ways to express
        // x as n-th powers of different natural
        // numbers
        int results = 0;

        // Calling power of 'i' raised to 'n'
        int p = power(curr_num, n);
        while (p + curr_sum < x) {
            // Recursively check all greater values of i
            results += checkRecursive(x, n, curr_num + 1,
                                      p + curr_sum);
            curr_num++;
            p = power(curr_num, n);
        }

        // If sum of powers is equal to x
        // then increase the value of result.
        if (p + curr_sum == x)
            results++;

        // Return the final result
        return results;
    }

    // Driver Code.
    public static void Main()
    {
        int x = 10, n = 2;
        System.Console.WriteLine(
            checkRecursive(x, n, 1, 0));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of ways any
// given integer x can
// be expressed as n-th
// power of unique
// natural numbers.

// Function to calculate and return
// the power of any given number
function power($num, $n)
{

    if ($n == 0)
        return 1;
    else if ($n % 2 == 0)
        return power($num, (int)($n / 2)) *
               power($num, (int)($n / 2));
    else
        return $num * power($num, (int)($n / 2)) *
                      power($num, (int)($n / 2));
}

// Function to check power
// representations recursively
function checkRecursive($x, $n,
                        $curr_num = 1,
                        $curr_sum = 0)
{

    // Initialize number of
    // ways to express
    // x as n-th powers
    // of different natural
    // numbers
    $results = 0;

    // Calling power of 'i'
    // raised to 'n'
    $p = power($curr_num, $n);
    while ($p + $curr_sum < $x)
    {

        // Recursively check all
        // greater values of i
        $results += checkRecursive($x, $n,
                                   $curr_num + 1,
                                   $p + $curr_sum);
        $curr_num++;
        $p = power($curr_num, $n);
    }

    // If sum of powers
    // is equal to x
    // then increase the
    // value of result.
    if ($p + $curr_sum == $x)
        $results++;

    // Return the final result
    return $results;
}

// Driver Code.
$x = 10; $n = 2;
echo(checkRecursive($x, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to count number of ways any
// given integer x can be expressed as n-th
// power of unique natural numbers.

    // Function to calculate and return the
    // power of any given number
    function power(num , n)
    {
        if (n == 0)
            return 1;
        else if (n % 2 == 0)
            return power(num, parseInt(n / 2)) * power(num, parseInt(n / 2));
        else
            return num * power(num,parseInt(n / 2)) * power(num, parseInt(n / 2));
    }

    // Function to check power representations recursively
    function checkRecursive(x , n , curr_num , curr_sum)
    {

        // Initialize number of ways to express
        // x as n-th powers of different natural
        // numbers
        var results = 0;

        // Calling power of 'i' raised to 'n'
        var p = power(curr_num, n);
        while (p + curr_sum < x)
        {

            // Recursively check all greater values of i
            results += checkRecursive(x, n, curr_num + 1, p + curr_sum);
            curr_num++;
            p = power(curr_num, n);
        }

        // If sum of powers is equal to x
        // then increase the value of result.
        if (p + curr_sum == x)
            results++;

        // Return the final result
        return results;
    }

    // Driver Code.
        var x = 10, n = 2;
        document.write(checkRecursive(x, n, 1, 0));

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
1
```

**备选方案:**

以下是由 **Shivam Kanodia** 提供的另一个更简单的解决方案。

## C++

```
// C++ program to find number of ways to express
// a number as sum of n-th powers of numbers.
#include<bits/stdc++.h>
using namespace std;

int res = 0;
int checkRecursive(int num, int x, int k, int n)
{
    if (x == 0)
        res++;

    int r = (int)floor(pow(num, 1.0 / n));

    for (int i = k + 1; i <= r; i++)
    {
        int a = x - (int)pow(i, n);
        if (a >= 0)
            checkRecursive(num, x -
                          (int)pow(i, n), i, n);
    }
    return res;
}

// Wrapper over checkRecursive()
int check(int x, int n)
{
    return checkRecursive(x, x, 0, n);
}

// Driver Code
int main()
{
    cout << (check(10, 2));
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways to express a
// number as sum of n-th powers of numbers.
import java.io.*;
import java.util.*;

public class Solution {

    static int res = 0;
    static int checkRecursive(int num, int x, int k, int n)
    {
        if (x == 0)
            res++;

        int r = (int)Math.floor(Math.pow(num, 1.0 / n));

        for (int i = k + 1; i <= r; i++) {
            int a = x - (int)Math.pow(i, n);
          if (a >= 0)
            checkRecursive(num,
                   x - (int)Math.pow(i, n), i, n);
        }
        return res;
    }

    // Wrapper over checkRecursive()
    static int check(int x, int n)
    {
        return checkRecursive(x, x, 0, n);
    }

    public static void main(String[] args)
    {
        System.out.println(check(10, 2));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find number of ways to express
# a number as sum of n-th powers of numbers.

def checkRecursive(num, rem_num, next_int, n, ans=0):

    if (rem_num == 0):
        ans += 1

    r = int(num**(1 / n))

    for i in range(next_int + 1, r + 1):
        a = rem_num - int(i**n)
        if a >= 0:
            ans += checkRecursive(num, rem_num - int(i**n), i, n, 0)
    return ans

# Wrapper over checkRecursive()

def check(x, n):
    return checkRecursive(x, x, 0, n)

# Driver Code
if __name__ == '__main__':
    print(check(10, 2))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find number of
// ways to express a number as sum
// of n-th powers of numbers.
using System;

class Solution {

    static int res = 0;
    static int checkRecursive(int num, int x,
                                int k, int n)
    {
        if (x == 0)
            res++;

        int r = (int)Math.Floor(Math.Pow(num, 1.0 / n));

        for (int i = k + 1; i <= r; i++)
        {
            int a = x - (int)Math.Pow(i, n);
        if (a >= 0)
            checkRecursive(num, x -
                          (int)Math.Pow(i, n), i, n);
        }
        return res;
    }

    // Wrapper over checkRecursive()
    static int check(int x, int n)
    {
        return checkRecursive(x, x, 0, n);
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(check(10, 2));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of ways to express a number
// as sum of n-th powers of numbers.
$res = 0;

function checkRecursive($num, $x,
                        $k, $n)
{
    global $res;
    if ($x == 0)
        $res++;

    $r = (int)floor(pow($num,
                        1.0 / $n));

    for ($i = $k + 1;
         $i <= $r; $i++)
    {
        $a = $x - (int)pow($i, $n);
        if ($a >= 0)
            checkRecursive($num, $x -
                    (int)pow($i, $n),
                             $i, $n);
    }
    return $res;
}

// Wrapper over
// checkRecursive()
function check($x, $n)
{
    return checkRecursive($x, $x,
                          0, $n);
}

// Driver Code
echo (check(10, 2));

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    let res = 0;
    function checkRecursive(num, x, k, n)
    {
        if (x == 0)
            res++;

        let r = Math.floor(Math.pow(num, 1.0 / n));

        for (let i = k + 1; i <= r; i++) {
            let a = x - Math.pow(i, n);
          if (a >= 0)
            checkRecursive(num,
                   x - Math.pow(i, n), i, n);
        }
        return res;
    }

    // Wrapper over checkRecursive()
    function check(x, n)
    {
        return checkRecursive(x, x, 0, n);
    }

// Driver Code
      document.write(check(10, 2));

// This code is contributed by splevel62.
</script>
```

**Output**

```
1
```

**简单递归解:**

由 [**拉姆·琼达尔**](https://www.linkedin.com/in/ram-jondhale-a98255135/)T4 贡献。

## C++

```
#include <iostream>
#include<cmath>
using namespace std;

//Helper function
int getAllWaysHelper(int remainingSum, int power, int base){
      //calculate power
    int result = pow(base, power);

    if(remainingSum == result)
        return 1;
    if(remainingSum < result)
        return 0;
      //Two recursive calls one to include current base's power in sum another to exclude
    int x = getAllWaysHelper(remainingSum - result, power, base + 1);
    int y = getAllWaysHelper(remainingSum, power, base+1);
    return x + y;
}

int getAllWays(int sum, int power) {
    return getAllWaysHelper(sum, power, 1);
}

// Driver Code.
int main()
{
    int x = 10, n = 2;
    cout << getAllWays(x, n);
    return 0;
}
```

**Output**

```
1
```

本文由 [**丹麦 KALEEM**](https://www.linkedin.com/in/mohdanishh/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。