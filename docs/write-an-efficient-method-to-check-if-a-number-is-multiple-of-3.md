# 写一个有效的方法来检查一个数是否是 3 的倍数

> 原文:[https://www . geeksforgeeks . org/write-一种高效的检查数字是否为 3 的倍数的方法/](https://www.geeksforgeeks.org/write-an-efficient-method-to-check-if-a-number-is-multiple-of-3/)

我们想到的第一个解决方案是我们在学校学到的。如果一个数的数字总和是 3 的倍数，那么这个数就是 3 的倍数，例如，对于 612，数字总和是 9，所以它是 3 的倍数。但是这种解决方案效率不高。你必须一个接一个地得到所有的十进制数字，把它们相加，然后检查总和是否是 3 的倍数。

数字的二进制表示中有一种模式，可以用来查找数字是否是 3 的倍数。如果奇数设置位(设置在奇数位置的位)和偶数设置位的计数之差是 3 的倍数，则为数字。
**例:** 23 (00..10111)
1)获取奇数位置的所有设置位的计数(对于 23，为 3)。
2)计算偶数位置的所有设置位的数量(23 为 1)。
3)如果上述两个计数之差是 3 的倍数，则该数也是 3 的倍数。
(23 是 2，所以 23 不是 3 的倍数)
再举一些例子，比如 21，15 等等……

```
Algorithm: isMutlipleOf3(n)
1) Make n positive if n is negative.
2) If number is 0 then return 1
3) If number is 1 then return 0
4) Initialize: odd_count = 0, even_count = 0
5) Loop while n != 0
    a) If rightmost bit is set then increment odd count.
    b) Right-shift n by 1 bit
    c) If rightmost bit is set then increment even count.
    d) Right-shift n by 1 bit
6) return isMutlipleOf3(odd_count - even_count)
```

**证明:**
以上可以以十进制数中的 11 为例来证明。(在本文中，十进制数中的 11 与二进制数中的 3 相同)
如果奇数和偶数之和的差是 11 的倍数，则十进制数是 11 的倍数。让我们看看如何。
我们以十进制 2 位数为例
AB = 11A-A+B = 11A+(B–A)
所以如果(B–A)是 11 的倍数，那么就是 AB。
我们取 3 位数。
ABC = 99A+A+11B–b+ C =(99A+11B)+(A+C–B)
所以如果(A+C–B)是 11 的倍数，那么就是(ABC)
现在我们取 4 位数。
ABCD = 1001 A+D+11C–C+999 B+B–A
=(1001 A–999 B+11C)+(D+B–A-C)
所以，如果(b+ D–A–C)是 11 的倍数，那么就是 ABCD。
对于所有十进制数都可以继续。
上述概念同样可以证明为二进制数中的 3。
**时间复杂度:** O(logn)
**程序:**

## C++

```
// CPP program to check if n is a multiple of 3
#include <bits/stdc++.h>
using namespace std;

/* Function to check if n is a multiple of 3*/
int isMultipleOf3(int n)
{
    int odd_count = 0;
    int even_count = 0;

    /* Make no positive if +n is multiple of 3
    then is -n. We are doing this to avoid
    stack overflow in recursion*/
    if (n < 0)
        n = -n;
    if (n == 0)
        return 1;
    if (n == 1)
        return 0;

    while (n) {
        /* If odd bit is set then
        increment odd counter */
        if (n & 1)
            odd_count++;

        /* If even bit is set then
        increment even counter */
        if (n & 2)
            even_count++;
        n = n >> 2;
    }

    return isMultipleOf3(abs(odd_count - even_count));
}

/* Program to test function isMultipleOf3 */
int main()
{
    int num = 24;
    if (isMultipleOf3(num))
        printf("%d is multiple of 3", num);
    else
        printf("%d is not a multiple of 3", num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// n is a multiple of 3
import java.lang.*;
import java.util.*;

class GFG {
    // Function to check if n
    // is a multiple of 3
    static int isMultipleOf3(int n)
    {
        int odd_count = 0;
        int even_count = 0;

        /* Make no positive if +n is multiple
    of 3 then is -n. We are doing this to
    avoid stack overflow in recursion*/
        if (n < 0)
            n = -n;
        if (n == 0)
            return 1;
        if (n == 1)
            return 0;

        while (n != 0) {
            /* If odd bit is set then
        increment odd counter */
            if ((n & 1) != 0)
                odd_count++;

            /* If even bit is set then
        increment even counter */
            if ((n & 2) != 0)
                even_count++;

            n = n >> 2;
        }

        return isMultipleOf3(Math.abs(odd_count - even_count));
    }

    /* Program to test function isMultipleOf3 */
    public static void main(String[] args)
    {
        int num = 24;

        if (isMultipleOf3(num) != 0)
            System.out.println(num + " is multiple of 3");
        else
            System.out.println(num + " is not a multiple of 3");
    }
}

// This code is contributed by Sahil_Bansall
```

## 蟒蛇 3

```
# Python program to check if n is a multiple of 3

# Function to check if n is a multiple of 3
def isMultipleOf3(n):

    odd_count = 0
    even_count = 0

    # Make no positive if + n is multiple of 3
    # then is -n. We are doing this to avoid
    # stack overflow in recursion
    if(n < 0):
        n = -n
    if(n == 0):
        return 1
    if(n == 1):
        return 0

    while(n):

        # If odd bit is set then
        # increment odd counter
        if(n & 1):
            odd_count += 1

        # If even bit is set then
        # increment even counter
        if(n & 2):
            even_count += 1
        n = n >> 2

    return isMultipleOf3(abs(odd_count - even_count))

# Program to test function isMultipleOf3
num = 24
if (isMultipleOf3(num)):
    print(num, 'is multiple of 3')
else:
    print(num, 'is not a multiple of 3')

# This code is contributed by Danish Raza
```

## C#

```
// C# program to check if
// n is a multiple of 3
using System;

class GFG {

    // Function to check if n
    // is a multiple of 3
    static int isMultipleOf3(int n)
    {
        int odd_count = 0, even_count = 0;

        /* Make no positive if +n is multiple
        of 3 then is -n. We are doing this to
        avoid stack overflow in recursion*/
        if (n < 0)
            n = -n;
        if (n == 0)
            return 1;
        if (n == 1)
            return 0;

        while (n != 0) {

            /* If odd bit is set then
            increment odd counter */
            if ((n & 1) != 0)
                odd_count++;

            /* If even bit is set then
            increment even counter */
            if ((n & 2) != 0)
                even_count++;

            n = n >> 2;
        }

        return isMultipleOf3(Math.Abs(odd_count - even_count));
    }

    // Driver Code
    public static void Main()
    {
        int num = 24;

        if (isMultipleOf3(num) != 0)
            Console.Write(num + " is multiple of 3");
        else
            Console.Write(num + " is not a multiple of 3");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if n
// is a multiple of 3

// Function to check if n
// is a multiple of 3
function isMultipleOf3( $n)
{
    $odd_count = 0;
    $even_count = 0;

    // Make no positive if +n
    // is multiple of 3 then is -n.
    // We are doing this to avoid
    // stack overflow in recursion
    if($n < 0) $n = -$n;
    if($n == 0) return 1;
    if($n == 1) return 0;

    while($n)
    {
        // If odd bit is set then
        // increment odd counter
        if($n & 1)
        $odd_count++;

        // If even bit is set then
        // increment even counter
        if($n & 2)
            $even_count++;
        $n = $n >> 2;
    }

    return isMultipleOf3(abs($odd_count -
                             $even_count));
}

// Driver Code
$num = 24;
if (isMultipleOf3($num))
    echo $num, "is multiple of 3";
else
    echo $num, "is not a multiple of 3";

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
/*Function to check if n is a multiple of 3*/
    function isMultipleof3(n)
    {
        odd_count = 0;
        even_count = 0;

        /* Make no positive if +n is multiple of 3
        then is -n. We are doing this to avoid
        stack overflowin recursion*/

        if(n < 0)
        n = -n;
        if(n == 0)
        return 1;
        if(n == 1)
        return 0;

         while (n)
         {
             /*If odd bit is set then
             increment odd counter*/
             if(n & 1)
             odd_count++;

             /*If even bit is set then
             increment even counter*/
             if(n & 2)
             even_count++;
             n = n>>2;
         }
         return isMultipleof3(Math.abs(odd_count-even_count));
    }     

       /*Program to test function isMultipleof3*/    
          num = 24;
          if(isMultipleof3(num))
             document.write(num + " is multiple of 3");
          else
             document.write(num + " is not a multiple of 3");

 // This code is contributed by simranarora5sos 
</script>
```

**Output**

```
24 is multiple of 3
```