# kaprekar 编号

> 原文:[https://www.geeksforgeeks.org/kaprekar-number/](https://www.geeksforgeeks.org/kaprekar-number/)

Kaprekar 数是这样一个数，它的平方被分成两部分，这样两部分的和等于原始数，并且没有一部分的值为 0。(来源: [Wiki](https://en.wikipedia.org/wiki/Kaprekar_number) )
给定一个号码，任务是检查是否是 Kaprekar 号码。
**示例:**

```
Input :  n = 45  
Output : Yes
Explanation : 452 = 2025 and 20 + 25 is 45

Input : n = 13
Output : No
Explanation : 132 = 169\. Neither 16 + 9 nor 1 + 69 is equal to 13

Input  : n = 297  
Output : Yes
Explanation:  2972 = 88209 and 88 + 209 is 297

Input  : n = 10 
Output : No
Explanation:  102 = 100\. It is not a Kaprekar number even if
sum of 100 + 0 is 100\. This is because of the condition that 
none of the parts should have value 0.
```

1.  求 n 的平方，并计算平方中的位数。
2.  在不同的位置拆分正方形，看看任何拆分中两个部分的和是否等于 n。

下面是这个想法的实现。

## C++

```
//C++ program to check if a number is Kaprekar number or not
#include<bits/stdc++.h>
using namespace std;

// Returns true if n is a Kaprekar number, else false
bool iskaprekar(int n)
{
    if (n == 1)
    return true;

    // Count number of digits in square
    int sq_n = n * n;
    int count_digits = 0;
    while (sq_n)
    {
        count_digits++;
        sq_n /= 10;
    }

    sq_n = n*n; // Recompute square as it was changed

    // Split the square at different poitns and see if sum
    // of any pair of splitted numbers is equal to n.
    for (int r_digits=1; r_digits<count_digits; r_digits++)
    {
        int eq_parts = pow(10, r_digits);

        // To avoid numbers like 10, 100, 1000 (These are not
        // Karprekar numbers
        if (eq_parts == n)
            continue;

        // Find sum of current parts and compare with n
        int sum = sq_n/eq_parts + sq_n % eq_parts;
        if (sum == n)
        return true;
    }

    // compare with original number
    return false;
}

// Driver code
int main()
{
cout << "Printing first few Kaprekar Numbers"
        " using iskaprekar()\n";
for (int i=1; i<10000; i++)
    if (iskaprekar(i))
        cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// Kaprekar number or not

class GFG
{
    // Returns true if n is a Kaprekar number, else false
    static boolean iskaprekar(int n)
    {
        if (n == 1)
           return true;

        // Count number of digits in square
        int sq_n = n * n;
        int count_digits = 0;
        while (sq_n != 0)
        {
            count_digits++;
            sq_n /= 10;
        }

        sq_n = n*n; // Recompute square as it was changed

        // Split the square at different poitns and see if sum
        // of any pair of splitted numbers is equal to n.
        for (int r_digits=1; r_digits<count_digits; r_digits++)
        {
             int eq_parts = (int) Math.pow(10, r_digits);

             // To avoid numbers like 10, 100, 1000 (These are not
             // Karprekar numbers
             if (eq_parts == n)
                continue;

             // Find sum of current parts and compare with n
             int sum = sq_n/eq_parts + sq_n % eq_parts;
             if (sum == n)
               return true;
        }

        // compare with original number
        return false;
    }

    // Driver method
    public static void main (String[] args)
    {
        System.out.println("Printing first few Kaprekar Numbers" +
                             " using iskaprekar()");

        for (int i=1; i<10000; i++)
            if (iskaprekar(i))
                 System.out.print(i + " ");
    }
}
```

## 计算机编程语言

```
# Python program to check if a number is Kaprekar number or not

import math

# Returns true if n is a Kaprekar number, else false
def iskaprekar( n):
    if n == 1 :
        return True

    #Count number of digits in square
    sq_n = n * n
    count_digits = 1
    while not sq_n == 0 :
        count_digits = count_digits + 1
        sq_n = sq_n / 10

    sq_n = n*n  # Recompute square as it was changed

    # Split the square at different poitns and see if sum
    # of any pair of splitted numbers is equal to n.
    r_digits = 0
    while r_digits< count_digits :
        r_digits = r_digits + 1
        eq_parts = (int) (math.pow(10, r_digits))

        # To avoid numbers like 10, 100, 1000 (These are not
        # Karprekar numbers
        if eq_parts == n :
            continue

        # Find sum of current parts and compare with n

        sum = sq_n/eq_parts + sq_n % eq_parts
        if sum == n :
            return True

    # compare with original number
    return False

# Driver method
i=1
while i<10000 :
    if (iskaprekar(i)) :
        print i," ",
    i = i + 1
# code contributed by Nikita Tiwari
```

## C#

```
// C# program to check if a number is
// Kaprekar number or not
using System;

class GFG {

    // Returns true if n is a Kaprekar
    // number, else false
    static bool iskaprekar(int n)
    {
        if (n == 1)
            return true;

        // Count number of digits
        // in square
        int sq_n = n * n;
        int count_digits = 0;
        while (sq_n != 0) {
            count_digits++;
            sq_n /= 10;
        }

        // Recompute square as it was changed
        sq_n = n * n;

        // Split the square at different poitns
        // and see if sum of any pair of splitted
        // numbers is equal to n.
        for (int r_digits = 1; r_digits < count_digits;
                                            r_digits++)
        {

            int eq_parts = (int)Math.Pow(10, r_digits);

            // To avoid numbers like 10, 100, 1000
            // These are not Karprekar numbers
            if (eq_parts == n)
                continue;

            // Find sum of current parts and compare
            // with n
            int sum = sq_n / eq_parts + sq_n % eq_parts;
            if (sum == n)
                return true;
        }

        // compare with original number
        return false;
    }

    // Driver method
    public static void Main()
    {

        Console.WriteLine("Printing first few "
        + "Kaprekar Numbers using iskaprekar()");

        for (int i = 1; i < 10000; i++)
            if (iskaprekar(i))
                Console.Write(i + " ");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is Kaprekar number or not

// Returns true if n is a Kaprekar
// number, else false
function iskaprekar($n)
{
    if ($n == 1)
    return true;

    // Count number of digits
    // in square
    $sq_n = $n * $n;
    $count_digits = 0;
    while ($sq_n)
    {
        $count_digits++;
        $sq_n = (int)($sq_n / 10);
    }

    $sq_n1 = $n * $n; // Recompute square
                      // as it was changed

    // Split the square at different
    // points and see if sum of any
    // pair of splitted numbers is equal to n.
    for ($r_digits = 1;
         $r_digits < $count_digits;
         $r_digits++)
    {
        $eq_parts = pow(10, $r_digits);

        // To avoid numbers like
        // 10, 100, 1000 (These are not
        // Karprekar numbers
        if ($eq_parts == $n)
            continue;

        // Find sum of current parts
        // and compare with n
        $sum = (int)($sq_n1 / $eq_parts) +
                     $sq_n1 % $eq_parts;
        if ($sum == $n)
        return true;
    }

    // compare with original number
    return false;
}

// Driver code
echo "Printing first few Kaprekar " .
      "Numbers using iskaprekar()\n";
for ($i = 1; $i < 10000; $i++)
    if (iskaprekar($i))
        echo $i . " ";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// is Kaprekar number or not

// Returns true if n is a Kaprekar
// number, else false
function iskaprekar(n)
{
    if (n == 1)
    return true;

    // Count number of digits
    // in square
    let sq_n = n * n;
    let count_digits = 0;
    while (sq_n)
    {
        count_digits++;
        sq_n = parseInt(sq_n / 10);
    }

    let sq_n1 = n * n; // Recompute square
                    // as it was changed

    // Split the square at different
    // points and see if sum of any
    // pair of splitted numbers is equal to n.
    for (let r_digits = 1;
        r_digits < count_digits;
        r_digits++)
    {
        let eq_parts = Math.pow(10, r_digits);

        // To avoid numbers like
        // 10, 100, 1000 (These are not
        // Karprekar numbers
        if (eq_parts == n)
            continue;

        // Find sum of current parts
        // and compare with n
        let sum = parseInt((sq_n1 / eq_parts) +
                    sq_n1 % eq_parts);
        if (sum == n)
        return true;
    }

    // compare with original number
    return false;
}

// Driver code
document.write("Printing first few Kaprekar " +
    "Numbers using iskaprekar()<br>");

for (let i = 1; i < 10000; i++)
    if (iskaprekar(i))
        document.write(i + " ");

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Printing first few Kaprekar Numbers using iskaprekar()
1 9 45 55 99 297 703 999 2223 2728 4879 4950 5050 5292 7272 7777 9999 
```

**参考:**
[【https://en.wikipedia.org/wiki/Kaprekar_number】](https://en.wikipedia.org/wiki/Kaprekar_number)
**相关文章:**
[Kaprekar 常量](https://www.geeksforgeeks.org/kaprekar-constant/)
本文由[**Sahil Chhabra(KILLER)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。