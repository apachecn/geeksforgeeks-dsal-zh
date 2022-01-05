# 求数的因子的最小和

> 原文:[https://www . geesforgeks . org/find-minimum-sum-factors-number/](https://www.geeksforgeeks.org/find-minimum-sum-factors-number/)

给定一个数，求其因子的最小和。
示例:

```
Input : 12
Output : 7
Explanation: 
Following are different ways to factorize 12 and
sum of factors in different ways.
12 = 12 * 1 = 12 + 1 = 13
12 = 2 * 6 = 2 + 6 = 8
12 = 3 * 4 = 3 + 4 = 7
12 = 2 * 2 * 3 = 2 + 2 + 3 = 7
Therefore minimum sum is 7

Input : 105
Output : 15
```

为了使总和最小化，我们必须尽可能长时间地分解因素。有了这个过程，我们[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。所以要求数的积的最小和，就要求积的素因子的和。

## C++

```
// CPP program to find minimum
// sum of product of number
#include <bits/stdc++.h>
using namespace std;

// To find minimum sum of
// product of number
int findMinSum(int num)
{
    int sum = 0;

    // Find factors of number
    // and add to the sum
    for (int i = 2; i * i <= num; i++) {
        while (num % i == 0) {
            sum += i;
            num /= i;
        }
    }
    sum += num;

    // Return sum of numbers
    // having minimum product
    return sum;
}

// Driver program to test above function
int main()
{
    int num = 12;

    cout << findMinSum(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// sum of product of number

public class Main {

    // To find minimum sum of
    // product of number
    static int findMinSum(int num)
    {
        int sum = 0;

        // Find factors of number
        // and add to the sum
        for (int i = 2; i * i <= num; i++) {
            while (num % i == 0) {
                sum += i;
                num /= i;
            }
        }
        sum += num;

        // Return sum of numbers
        // having minimum product
        return sum;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int num = 12;
        System.out.println(findMinSum(num));
    }
}
```

## 计算机编程语言

```
# Python program to find minimum
# sum of product of number

# To find minimum sum of
# product of number
def findMinSum(num):
    sum = 0

    # Find factors of number
    # and add to the sum
    i = 2
    while(i * i <= num):
        while(num % i == 0):
            sum += i
            num /= i
        i += 1
    sum += num

    # Return sum of numbers
    # having minimum product
    return sum

# Driver Code
num = 12
print findMinSum(num)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find minimum
// sum of product of number
using System;

public class GFG {

    // To find minimum sum of
    // product of number
    static int findMinSum(int num)
    {
        int sum = 0;

        // Find factors of number
        // and add to the sum
        for (int i = 2; i * i <= num; i++) {
            while (num % i == 0) {
                sum += i;
                num /= i;
            }
        }
        sum += num;

        // Return sum of numbers
        // having minimum product
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int num = 12;
        Console.Write(findMinSum(num));
    }

}

// This Code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// sum of product of number

// To find minimum sum of
// product of number
function findMinSum($num)
{
    $sum = 0;

    // Find factors of number
    // and add to the sum
    for ($i = 2; $i * $i <= $num; $i++)
    {
        while ($num % $i == 0)
        {
            $sum += $i;
            $num /= $i;
        }
    }
    $sum += $num;

    // Return sum of numbers
    // having minimum product
    return $sum;
}

// Driver Code
$num = 12;

echo(findMinSum($num));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum
// sum of product of number

// To find minimum sum of
// product of number
function findMinSum(num)
{
    let sum = 0;

    // Find factors of number
    // and add to the sum
    for (let i = 2; i * i <= num; i++) 
    {
        while (num % i == 0) 
        {
            sum += i;
            num /= i;
        }
    }
    sum += num;

    // Return sum of numbers
    // having minimum product
    return sum;
}

// Driver Code
let num = 12;

document.write(findMinSum(num));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
7
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。