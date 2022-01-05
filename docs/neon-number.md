# 霓虹号

> 原文:[https://www.geeksforgeeks.org/neon-number/](https://www.geeksforgeeks.org/neon-number/)

霓虹数字是一个数字的平方的位数和等于这个数字。任务是检查和打印一定范围内的霓虹灯号码。

示例:

```
Input : 9
Output : Neon Number
Explanation: square is 9*9 = 81 and 
sum of the digits of the square is 9.

Input :12
Output : Not a Neon Number
Explanation: square is 12*12 = 144 and 
sum of the digits of the square is 9 (1 
+ 4 + 4) which is not equal to 12.
```

实现很简单，我们先计算给定数字的平方，[求平方中数字的和](https://www.geeksforgeeks.org/how-can-we-sum-the-digits-of-a-given-number-in-single-statement/)。

## C++

```
// C/C++ program to check and print
// Neon Numbers upto 10000
#include <iostream>
using namespace std;
#include <math.h>

int checkNeon(int x)
{
    // storing the square of x
    int sq = x * x;

    // calculating the sum of sum of digits
    // of sq
    int sum_digits = 0;
    while (sq != 0) {
        sum_digits = sum_digits + sq % 10;
        sq = sq / 10;
    }
    return (sum_digits == x);
}

// Driver Code
int main(void)
{
    // Printing Neon Numbers upto 10000
    for (int i = 1; i <= 10000; i++)
        if (checkNeon(i))
            cout << i << " ";   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check and print
// Neon Numbers upto 10000
import java.io.*;

class GFG {
    // function to check Neon Number
    static boolean checkNeon(int x)
    {
        // storing the square of x
        int sq = x * x;

        // calculating the sum of sum of digits
        // of sq
        int sum_digits = 0;
        while (sq != 0) {
            sum_digits = sum_digits + sq % 10;
            sq = sq / 10;
        }
        return (sum_digits == x);
    }

    // Driver Code
    public static void main(String args[])
                        throws IOException
    {
        // Printing Neon Numbers upto 10000
        for (int i = 1; i <= 10000; i++)
            if (checkNeon(i))
                System.out.print(i + " ");       
    }
}
// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to check and print
# Neon Numbers upto 10000

# function to check Neon Number
def checkNeon (x) :
    # storing the square of x
    sq = x * x

    # calculating the sum of sum of digits
    # of sq
    sum_digits = 0
    while (sq != 0) :
        sum_digits = sum_digits + sq % 10
        sq = sq / 10

    return (sum_digits == x)

# Driver Code

i = 1
# Printing Neon Numbers upto 10000
while i <= 10000 :
    if (checkNeon(i)) :
        print i,
    i = i + 1

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check and print
// Neon Numbers upto 10000
using System;

class GFG
{
    // function to check Neon Number
    static bool checkNeon(int x)
    {
        // storing the square of x
        int sq = x * x;

        // calculating the sum of sum of digits
        // of sq
        int sum_digits = 0;
        while (sq != 0)
        {
            sum_digits = sum_digits + sq % 10;
            sq = sq / 10;
        }
        return (sum_digits == x);
    }

    // Driver Code
    public static void Main()

    {
        // Printing Neon Numbers upto 10000
        for (int i = 1; i <= 10000; i++)
            if (checkNeon(i))
                Console.Write(i + " ");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check and print
// Neon Numbers upto 10000

function checkNeon($x)
{

    // storing the square of x
    $sq = $x * $x;

    // calculating the sum of
    // sum of digits of sq
    $sum_digits = 0;
    while ($sq != 0)
    {
        $sum_digits = $sum_digits +
                         $sq % 10;
        $sq = $sq / 10;
    }
    return ($sum_digits == $x);
}

    // Driver Code
    // Printing Neon Numbers
    // upto 10000
    for ($i = 1; $i <= 10000; $i++)
        if (checkNeon($i))
            echo $i . " ";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to check and print
// Neon Numbers upto 10000

    // function to check Neon Number
    function checkNeon(x)
    {
        // storing the square of x
        let sq = x * x;

        // calculating the sum of sum of digits
        // of sq
        let sum_digits = 0;
        while (sq != 0) {
            sum_digits = sum_digits + sq % 10;
            sq = Math.floor(sq / 10);
        }
        return (sum_digits == x);
    }

// driver program

       // Printing Neon Numbers upto 10000
        for (let i = 1; i <= 10000; i++)
            if (checkNeon(i))
                document.write(i + " ");

</script>
```

**输出:**

```
1 9

```

本文由**尼基塔·蒂瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。