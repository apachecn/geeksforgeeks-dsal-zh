# 两个数乘积的位数

> 原文:[https://www . geesforgeks . org/number-digits-product-two-numbers/](https://www.geeksforgeeks.org/number-digits-product-two-numbers/)

给定两个整数 **a** 和 **b** 。问题是求这两个整数乘积的位数。
**例:**

```
Input : a = 12, b = 4
Output : 2
12 * 4 = 48 (2 digits)

Input : a = 33, b = -24
Output : 3
33 * -24 = -792 (3 digits)
```

**天真方法:**将两个数字相乘，然后通过使用循环构造找到乘积中的位数。取乘积的绝对值求位数。

## C++

```
// C++ implementation to count number of digits
// in the product of two numbers
#include <bits/stdc++.h>

using namespace std;

// function to count number of digits
// in the product of two numbers
int countDigits(int a, int b)
{
    int count = 0;   

    // absolute value of the
    // product of two numbers
    int p = abs(a*b);

    // if product is 0
    if (p == 0)   
        return 1;

    // count number of digits in the product 'p'   
    while (p > 0)   
    {
        count++;
        p = p / 10;
    }

    // required count of digits   
    return count;
}

// Driver program to test above
int main()
{
    int a = 33;
    int b = -24;
    cout << "Number of digits = "
         << countDigits(a,b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// number of digits in the product
// of two numbers
import java.io.*;
import java.math.*;

class GFG {

    // function to count number of digits
    // in the product of two numbers
    static int countDigits(int a, int b)
    {
        int count = 0;

        // absolute value of the
        // product of two numbers
        int p = Math.abs(a * b);

        // if product is 0
        if (p == 0)
            return 1;

        // count number of digits in
        // the product 'p'
        while (p > 0)
        {
            count++;
            p = p / 10;
        }

        // required count of digits
        return count;
    }

    // Driver program to test above
    public static void main(String args[])
    {
        int a = 33;
        int b = -24;
        System.out.println("Number of digits = "
                           + countDigits(a, b));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 implementation to count
# number of digits in the product
# of two numbers

# function to count number of digits
# in the product of two numbers
def countDigits(a, b) :
    count = 0

    # absolute value of the
    # product of two numbers
    p = abs(a * b)

    # if product is 0
    if (p == 0) :
        return 1

    # count number of digits
    # in the product 'p'
    while (p > 0) :
        count = count + 1
        p = p // 10

    # required count of digits
    return count

# Driver program to test above
a = 33
b = -24
print("Number of digits = ",
       countDigits(a,b))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation to count
// number of digits in the product
// of two numbers
using System;

class GFG {

    // function to count number of digits
    // in the product of two numbers
    static int countDigits(int a, int b)
    {
        int count = 0;

        // absolute value of the
        // product of two numbers
        int p = Math.Abs(a * b);

        // if product is 0
        if (p == 0)
            return 1;

        // count number of digits in
        // the product 'p'
        while (p > 0) {
            count++;
            p = p / 10;
        }

        // required count of digits
        return count;
    }

    // Driver program to test above
    public static void Main()
    {
        int a = 33;
        int b = -24;
        Console.WriteLine("Number of digits = " +
                              countDigits(a, b));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count
// number of digits in the
// product of two numbers

// function to count number
// of digits in the product
// of two numbers
function countDigits($a, $b)
{
    $count = 0;

    // absolute value of the
    // product of two numbers
    $p = abs($a * $b);

    // if product is 0
    if ($p == 0)
        return 1;

    // count number of digits
    // in the product 'p'
    while ($p > 0)
    {
        $count++;
        $p = (int)($p / 10);
    }

    // required count of digits
    return $count;
}

// Driver Code
$a = 33;
$b = -24;
echo "Number of digits = " .
        countDigits($a, $b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to count number of digits
    // in the product of two numbers

    // function to count number of digits
    // in the product of two numbers
    function countDigits(a, b)
    {
        let count = 0;   

        // absolute value of the
        // product of two numbers
        let p = Math.abs(a*b);

        // if product is 0
        if (p == 0)   
            return 1;

        // count number of digits in the product 'p'   
        while (p > 0)   
        {
            count++;
            p = parseInt(p / 10, 10);
        }

        // required count of digits   
        return count;
    }

    let a = 33;
    let b = -24;
    document.write("Number of digits = " + countDigits(a,b));

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Number of digits = 3
```

**有效方法:**要计算两个数乘积的位数，我们可以使用下面给出的公式:

```
                count = floor(log<sub>10(a) + log10(b)) + 1</sub>
```

这里两个数字都必须是正整数。为此我们可以取 **a** 和 **b** 的绝对值。

## C++

```
// C++ implementation to count number of digits
// in the product of two numbers
#include <bits/stdc++.h>

using namespace std;

// function to count number of digits
// in the product of two numbers
int countDigits(int a, int b)
{
    // if either of the number is 0, then
    // product will be 0
    if (a == 0 || b == 0)
        return 1;

    // required count of digits           
    return floor(log10(abs(a)) + log10(abs(b))) + 1;   
}

// Driver program to test above
int main()
{
    int a = 33;
    int b = -24;
    cout << countDigits(a,b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Number of digits
// in the product of two numbers
class GFG {

    // function to count number of digits
    // in the product of two numbers
    public static int countDigits(int a, int b)
    {
        // if either of the number is 0, then
        // product will be 0
        if (a == 0 || b == 0)
            return 1;

        // required count of digits           
        return (int)Math.floor(Math.log10(Math.abs(a)) +
                            Math.log10(Math.abs(b))) + 1;   
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int a = 33;
        int b = -24;
        System.out.print(countDigits(a,b));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 implementation to count
# number of digits in the product
# of two numbers
import math

# function to count number of digits
# in the product of two numbers
def countDigits(a, b) :

    # if either of the number is 0,
    # then product will be 0
    if (a == 0 or b == 0) :
        return 1

    # required count of digits        
    return math.floor(math.log10(abs(a)) +
                   math.log10(abs(b))) + 1

# Driver program to test above
a = 33
b = -24
print(countDigits(a, b))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Code for Number of digits
// in the product of two numbers
using System;

class GFG {

    // function to count number of
    // digits in the product of two
    // numbers
    public static int countDigits(int a,
                                  int b)
    {
        // if either of the number is 0,
        // then product will be 0
        if (a == 0 || b == 0)
            return 1;

        // required count of digits        
        return (int)Math.Floor(
                 Math.Log10(Math.Abs(a))
          + Math.Log10(Math.Abs(b))) + 1;
    }

    // Driver code
    static void Main()
    {
        int a = 33;
        int b = -24;
        Console.Write(countDigits(a, b));

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count
// number of digits in the product
// of two numbers

// function to count number of digits
// in the product of two numbers
function countDigits($a, $b)
{
    // if either of the number is
    // 0, then product will be 0
    if ($a == 0 or $b == 0)
        return 1;

    // required count of digits    
    return floor(log10(abs($a)) +
                 log10(abs($b))) + 1;
}

// Driver Code
$a = 33;
$b = -24;
echo countDigits($a, $b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to count number of digits
// in the product of two numbers

// function to count number of digits
// in the product of two numbers
function countDigits(a, b)
{
    // if either of the number is 0, then
    // product will be 0
    if (a == 0 || b == 0)
        return 1;

    // required count of digits           
    return Math.floor(Math.log10(Math.abs(a)) + Math.log10(Math.abs(b))) + 1;   
}

// Driver program to test above
    let a = 33;
    let b = -24;
    document.write(countDigits(a,b));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
3
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。