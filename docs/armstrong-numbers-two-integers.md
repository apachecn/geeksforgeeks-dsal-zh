# 两个整数之间的阿姆斯特朗数

> 原文:[https://www . geesforgeks . org/Armstrong-numbers-two-integer/](https://www.geeksforgeeks.org/armstrong-numbers-two-integers/)

如果满足以下条件，则具有数字 a、b、c、d…的正整数称为 n 阶[阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)。

```
abcd... = an + bn + cn + dn +...
```

```
153 = 1*1*1 + 5*5*5 + 3*3*3  
    =  1 + 125 + 27
    =  153        
Therefore, 153 is an Armstrong number.
```

**例:**

```
Input : 100 400
Output :153 370 371
Explanation : 100 and 400 are given 
two integers.(interval)
  153 = 1*1*1 + 5*5*5 + 3*3*3 
      = 1 + 125 + 27
      =  153  
  370 = 3*3*3 + 7*7*7 + 0
      = 27 + 343 
      = 370
  371 = 3*3*3 + 7*7*7 + 1*1*1
      = 27 + 343 +1
      = 371
```

下面实现的方法很简单。我们遍历给定范围内的所有数字。对于每个数字，我们首先计算其中的位数。设当前数的位数为 n，我们求出所有位数的 n 次方的和。如果总和等于 I，我们就打印这个数字。

## C++

```
// CPP program to find Armstrong numbers in a range
#include <bits/stdc++.h>
using namespace std;

// Prints Armstrong Numbers in given range
void findArmstrong(int low, int high)
{
    for (int i = low+1; i < high; ++i) {

        // number of digits calculation
        int x = i;
        int n = 0;
        while (x != 0) {
            x /= 10;
            ++n;
        }

        // compute sum of nth power of
        // its digits
        int pow_sum = 0;
        x = i;
        while (x != 0) {
            int digit = x % 10;
            pow_sum += pow(digit, n);
            x /= 10;
        }

        // checks if number i is equal to the
        // sum of nth power of its digits
        if (pow_sum == i)
            cout << i << " ";    
    }
}

// Driver code
int main()
{
    int num1 = 100;
    int num2 = 400;
    findArmstrong(num1, num2);
    cout << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find Armstrong
// numbers in a range
import java.io.*;
import java.math.*;

class GFG {

    // Prints Armstrong Numbers in given range
    static void findArmstrong(int low, int high)
    {
        for (int i = low + 1; i < high; ++i) {

            // number of digits calculation
            int x = i;
            int n = 0;
            while (x != 0) {
                x /= 10;
                ++n;
            }

            // compute sum of nth power of
            // its digits
            int pow_sum = 0;
            x = i;
            while (x != 0) {
                int digit = x % 10;
                pow_sum += Math.pow(digit, n);
                x /= 10;
            }

            // checks if number i is equal
            // to the sum of nth power of
            // its digits
            if (pow_sum == i)
                System.out.print(i + " ");    
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int num1 = 100;
        int num2 = 400;
        findArmstrong(num1, num2);
        System.out.println();
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# PYTHON program to find Armstrong
# numbers in a range
import math

# Prints Armstrong Numbers in given range
def findArmstrong(low, high) :

    for i in range(low + 1, high) :

        # number of digits calculation
        x = i
        n = 0
        while (x != 0) :
            x = x / 10
            n = n + 1

        # compute sum of nth power of
        pow_sum = 0
        x = i
        while (x != 0) :
            digit = x % 10
            pow_sum = pow_sum + math.pow(digit, n)
            x = x / 10

        # checks if number i is equal to
        # the sum of nth power of its digits
        if (pow_sum == i) :
            print(str(i) + " "),

# Driver code
num1 = 100
num2 = 400
findArmstrong(num1, num2)
print("")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find Armstrong
// numbers in a range
using System;

class GFG {

    // Prints Armstrong Numbers in given range
    static void findArmstrong(int low, int high)
    {
        for (int i = low + 1; i < high; ++i) {

            // number of digits calculation
            int x = i;
            int n = 0;
            while (x != 0) {
                x /= 10;
                ++n;
            }

            // compute sum of nth power of
            // its digits
            int pow_sum = 0;
            x = i;
            while (x != 0) {
                int digit = x % 10;
                pow_sum += (int)Math.Pow(digit, n);
                x /= 10;
            }

            // checks if number i is equal
            // to the sum of nth power of
            // its digits
            if (pow_sum == i)
                Console.Write(i + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int num1 = 100;
        int num2 = 400;
        findArmstrong(num1, num2);
        Console.WriteLine();
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// Armstrong numbers
// in a range

// Prints Armstrong
// Numbers in given range
function findArmstrong($low, $high)
{
    for ($i = $low + 1;
         $i < $high; ++$i)
    {

        // number of digits
        // calculation
        $x = $i;
        $n = 0;
        while ($x != 0)
        {
            $x = (int)($x / 10);
            ++$n;
        }

        // compute sum of nth
        // power of its digits
        $pow_sum = 0;
        $x = $i;
        while ($x != 0)
        {
            $digit = $x % 10;
            $pow_sum += (int)(pow($digit, $n));
            $x = (int)($x / 10);
        }

        // checks if number i is
        // equal to the sum of
        // nth power of its digits
        if ($pow_sum == $i)
            echo $i . " ";    
    }
}

// Driver code
$num1 = 100;
$num2 = 400;
findArmstrong($num1, $num2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to find
// Armstrong numbers
// in a range

// Prints Armstrong
// Numbers in given range
function findArmstrong(low, high)
{
    for (let i = low + 1;
         i < high; ++i)
    {

        // number of digits
        // calculation
        let x = i;
        let n = 0;
        while (x != 0)
        {
            x = parseInt(x / 10);
            ++n;
        }

        // compute sum of nth
        // power of its digits
        let pow_sum = 0;
        x = i;
        while (x != 0)
        {
            let digit = x % 10;
            pow_sum += parseInt(Math.pow(digit, n));
            x = parseInt(x / 10);
        }

        // checks if number i is
        // equal to the sum of
        // nth power of its digits
        if (pow_sum == i)
            document.write(i + " ");     
    }
}

// Driver code
let num1 = 100;
let num2 = 400;
findArmstrong(num1, num2);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
153 370 371
```

本文由 [**阿迪蒂亚·冉冉**](https://auth.geeksforgeeks.org/profile.php?user=aditya1011) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。