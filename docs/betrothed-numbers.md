# 订婚号码

> 原文:[https://www.geeksforgeeks.org/betrothed-numbers/](https://www.geeksforgeeks.org/betrothed-numbers/)

定数是两个正数，因此两个数的除数之和比另一个数的值多一(或加一)。我们的任务是高效地找到这些配对。
**例:**

```
(48, 75) is an example of Betrothed numbers
Divisors of 48 : 1, 2, 3, 4, 6, 8, 12, 
                 16, 24\. Their sum is 76.
Divisors of 75 : 1, 3, 5, 15, 25\. Their 
                 sum is 49.
```

给定一个正整数 n，打印所有混合数字(一对)，使得每对中的一个数字小于 n。
**示例:**

```
Input : n = 1000
Output : (48, 75), (140, 195)

Input : n = 10000
Output : (48, 75), (140, 195), (1050, 1925)
         (1575, 1648), (2024, 2295), (5775, 
         6128) (8892, 16587), (9504, 20735)
```

下面程序使用的思路很简单。我们遍历从 1 到 n-1 的所有数字。对于每一个数 num1，我们找到它的适当除数的[和，比如 sum1。在找到 sum1 之后，我们检查 num2 = sum1 + 1 这个数是否有作为 num1 + 1 的除数之和](https://www.geeksforgeeks.org/sum-proper-divisors-natural-numbers-array/) 

## C++

```
// CPP program to find Betrothed number pairs
// such that one of the numbers is smaller than
// a given number n.
#include <iostream>
using namespace std;

void BetrothedNumbers(int n)
{
    for (int num1 = 1; num1 < n; num1++) {

        // Calculate sum of num1's divisors
        int sum1 = 1; // 1 is always a divisor

        // i=2 because we don't want to include
        // 1 as a divisor.
        for (int i = 2; i * i <= num1; i++)
        {
            if (num1 % i == 0) {
                sum1 += i;

                // we do not want to include
                // a divisor twice
                if (i * i != num1)
                    sum1 += num1 / i;
            }
        }

        // Now check if num2 is the sum of
        // divisors of num1, so only the num
        // that equals to sum of divisors of
        // num1 is a nominee for num1.

         /* This if is for not to make a
            duplication of the nums, because
            if sum1 is smaller than num1, this
            means that we have already checked
            the smaller one.*/
        if (sum1 > num1)
        {
            int num2 = sum1 - 1;
            int sum2 = 1;
            for (int j = 2; j * j <= num2; j++)
            {
                if (num2 % j == 0) {
                    sum2 += j;
                    if (j * j != num2)
                        sum2 += num2 / j;
                }
            }

            // checks if the sum divisors of
            // num2 is equal to num1.
            if (sum2 == num1+1)
                printf("(%d, %d)\n", num1, num2);
        }
    }
}

// Driver code
int main()
{
    int n = 10000;
    BetrothedNumbers(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find Betrothed number
// pairs such that one of the numbers is
// smaller than a given number n.
import java.io.*;

class GFG{

    static void BetrothedNumbers(int n)
    {
    for (int num1 = 1; num1 < n; num1++) {

        // Calculate sum of num1's divisors
        int sum1 = 1; // 1 is always a divisor

        // i=2 because we don't want to include
        // 1 as a divisor.
        for (int i = 2; i * i <= num1; i++)
        {
            if (num1 % i == 0) {
                sum1 += i;

            // we do not want to include
            // a divisor twice
                if (i * i != num1)
                    sum1 += num1 / i;
            }
        }

        // Now check if num2 is the sum of
        // divisors of num1, so only the num
        // that equals to sum of divisors of
        // num1 is a nominee for num1.

        /* This if is for not to make a
        duplication of the nums, because
        if sum1 is smaller than num1, this
        means that we have already checked
        the smaller one.*/
        if (sum1 > num1)
        {
            int num2 = sum1 - 1;
            int sum2 = 1;
            for (int j = 2; j * j <= num2; j++)
            {
                if (num2 % j == 0) {
                    sum2 += j;
                    if (j * j != num2)
                        sum2 += num2 / j;
                }
            }

        // checks if the sum divisors of
        // num2 is equal to num1.
            if (sum2 == num1+1)
                System.out.println("(" + num1 +
                              ", " + num2 + ")");
        }
    }
    }

    // Driver code
    public static void main(String args[])
    {
    int n = 10000;
    BetrothedNumbers(n);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to find Betrothed number pairs
# such that one of the numbers is smaller than
# a given number n.

def BetrothedNumbers(n) :

    for num1 in range (1,n) :

        # Calculate sum of num1's divisors
        sum1 = 1 # 1 is always a divisor

        # i=2 because we don't want to include
        # 1 as a divisor.
        i = 2
        while i * i <= num1 :
            if (num1 % i == 0) :
                sum1 = sum1 + i

                # we do not want to include
                # a divisor twice
                if (i * i != num1) :
                    sum1 += num1 / i
            i =i + 1

        # Now check if num2 is the sum of
        # divisors of num1, so only the num
        # that equals to sum of divisors of
        # num1 is a nominee for num1.

        # This if is for not to make a
        #duplication of the nums, because
        #if sum1 is smaller than num1, this
        #means that we have already checked
        #the smaller one.
        if (sum1 > num1) :

            num2 = sum1 - 1
            sum2 = 1
            j = 2
            while j * j <= num2 :
                if (num2 % j == 0) :
                    sum2 += j
                    if (j * j != num2) :
                        sum2 += num2 / j
                j = j + 1

            # checks if the sum divisors of
            # num2 is equal to num1.
            if (sum2 == num1+1) :
                print ('('+str(num1)+', '+str(num2)+')')

# Driver code

n = 10000
BetrothedNumbers(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find Betrothed
// number pairs such that one
// of the numbers is smaller
// than a given number n.
using System;

class GFG
{
    static void BetrothedNumbers(int n)
    {
    for (int num1 = 1; num1 < n; num1++)
    {

        // Calculate sum of
        // num1's divisors

        // 1 is always a divisor
        int sum1 = 1;

        // i=2 because we don't want
        // to include 1 as a divisor.
        for (int i = 2; i * i <= num1; i++)
        {
            if (num1 % i == 0)
            {
                sum1 += i;

            // we do not want to include
            // a divisor twice
                if (i * i != num1)
                    sum1 += num1 / i;
            }
        }

        // Now check if num2 is the
        // sum of divisors of num1,
        // so only the num that equals
        // to sum of divisors of num1
        // is a nominee for num1.

        /* This if is for not to
        make a duplication of the
        nums, because if sum1 is
        smaller than num1, this
        means that we have already
        checked the smaller one.*/
        if (sum1 > num1)
        {
            int num2 = sum1 - 1;
            int sum2 = 1;
            for (int j = 2; j * j <= num2; j++)
            {
                if (num2 % j == 0)
                {
                    sum2 += j;
                    if (j * j != num2)
                        sum2 += num2 / j;
                }
            }

        // checks if the sum divisors
        // of num2 is equal to num1.
            if (sum2 == num1 + 1)
                Console.WriteLine("(" + num1 +
                           ", " + num2 + ")");
        }
    }
    }

    // Driver code
    public static void Main()
    {
    int n = 10000;
    BetrothedNumbers(n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Betrothed number pairs
// such that one of the numbers is smaller than
// a given number n.

function BetrothedNumbers($n)
{
    for ( $num1 = 1; $num1 < $n; $num1++) {

        // Calculate sum of num1's divisors
        // 1 is always a divisor
        $sum1 = 1;

        // i=2 because we don't want to include
        // 1 as a divisor.
        for ( $i = 2; $i * $i <= $num1; $i++)
        {
            if ($num1 % $i == 0) {
                $sum1 += $i;

                // we do not want to include
                // a divisor twice
                if ($i * $i != $num1)
                    $sum1 += $num1 / $i;
            }
        }

        // Now check if num2 is the sum of
        // divisors of num1, so only the num
        // that equals to sum of divisors of
        // num1 is a nominee for num1.

        /* This if is for not to make a
            duplication of the nums, because
            if sum1 is smaller than num1, this
            means that we have already checked
            the smaller one.*/
        if ($sum1 > $num1)
        {
            $num2 = $sum1 - 1;
            $sum2 = 1;
            for ($j = 2; $j * $j <= $num2; $j++)
            {
                if ($num2 % $j == 0) {
                    $sum2 += $j;
                    if ($j * $j != $num2)
                        $sum2 += $num2 / $j;
                }
            }

            // checks if the sum divisors of
            // num2 is equal to num1.
            if ($sum2 == $num1+1)
                echo"(",$num1," ",$num2,")\n";
        }
    }
}

    // Driver code
    $n = 10000;
    BetrothedNumbers($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find Betrothed number pairs
// such that one of the numbers is smaller than
// a given number n.
function BetrothedNumbers(n)
{
    for (let num1 = 1; num1 < n; num1++)
    {

        // Calculate sum of num1's divisors
        let sum1 = 1; // 1 is always a divisor

        // i=2 because we don't want to include
        // 1 as a divisor.
        for (let i = 2; i * i <= num1; i++)
        {
            if (num1 % i == 0) {
                sum1 += i;

                // we do not want to include
                // a divisor twice
                if (i * i != num1)
                    sum1 += parseInt(num1 / i);
            }
        }

        // Now check if num2 is the sum of
        // divisors of num1, so only the num
        // that equals to sum of divisors of
        // num1 is a nominee for num1.

         /* This if is for not to make a
            duplication of the nums, because
            if sum1 is smaller than num1, this
            means that we have already checked
            the smaller one.*/
        if (sum1 > num1)
        {
            let num2 = sum1 - 1;
            let sum2 = 1;
            for (let j = 2; j * j <= num2; j++)
            {
                if (num2 % j == 0) {
                    sum2 += j;
                    if (j * j != num2)
                        sum2 += parseInt(num2 / j);
                }
            }

            // checks if the sum divisors of
            // num2 is equal to num1.
            if (sum2 == (num1+1))
                document.write(`(${num1}, ${num2})<br>`);
        }
    }
}

// Driver code
    let n = 10000;
    BetrothedNumbers(n);

// This code is contributed by rishavmahato348.
</script>
```

**输出:**

```
(48, 75)
(140, 195)
(1050, 1925)
(1575, 1648)
(2024, 2295)
(5775, 6128)
(8892, 16587)
(9504, 20735)
```

本文由 [**什洛米·埃尔海亚尼**](https://www.facebook.com/shlomi.elhaiani?ref=bookmarks) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。