# 大数为 7 的余数

> 原文:[https://www.geeksforgeeks.org/remainder-7-large-numbers/](https://www.geeksforgeeks.org/remainder-7-large-numbers/)

给定一个大的数作为字符串，求数除以 7 的余数。
**例:**

```
Input : num = 1234
Output : 2

Input : num = 1232
Output : 0

Input : num = 12345
Output : 4
```

简单的方法是将字符串转换成数字并执行 mod 操作。但是这种方法不适用于长字符串。
有一种方法也适用于大数。以下是步骤。
给定数字为“num”

1.  我们用数列 1，3，2，-1，-3，-2 来求余数(数列背后的直觉在下面讨论)。
2.  将结果初始化为 0。
3.  从头到尾遍历编号，从开始遍历以上系列。对于每个遍历的数字，将其与序列的下一个数字相乘，并将相乘结果相加。
4.  当有更多的数字需要处理时，继续重复步骤 3。如果位数超过 6(系列中的项数)，则开始从头开始遍历系列。
5.  在每一步之后，我们继续做 result = result % 7，以确保结果保持小于 7。

插图:

```
let us take above Example where number is 12345\. 

We reverse the number from end and series from 
the beginning and keep adding multiplication to
the result.
(12345 % 7) = (5*1 + 4*3 + 3*2 + 2*(-1) + 1*(-3)) % 7
            = (5 + 12 + 6 - 2 - 3)%7
            = (18) % 7
            = 4
hence 4 will be the remainder when we divide
the number 12345 by 7\. 
```

**这个系列公式是如何工作的？**
下图是系列
背后的直觉

```
1  % 7 = 1
10 % 7 = 3
100 % 7 = 2
1000 % 7 = 6 = (-1) % 7
10000 % 7 = 4 = (-3) % 7
100000 % 7 = 5 = (-2) % 7

The series repeats itself for larger powers
1000000 % 7 = 1
10000000 % 7 = 3
..............
...............

The above property of modular division with 7 and 
associative properties of modular arithmetic are 
the basis of the approach used here.
```

**执行:**

## C++

```
// C++ program to find remainder of a large
// number when divided by 7.
#include<iostream>
using namespace std;

/* Function which returns Remainder after dividing
   the number by 7 */
int remainderWith7(string num)
{
    // This series is used to find remainder with 7
    int series[] = {1, 3, 2, -1, -3, -2};

    // Index of next element in series
    int series_index = 0;

    int result = 0;  // Initialize result

    // Traverse num from end
    for (int i=num.size()-1; i>=0; i--)
    {
        /* Find current digit of nun */
        int digit = num[i] - '0';

        // Add next term to result
        result += digit * series[series_index];

        // Move to next term in series
        series_index = (series_index + 1) % 6;

        // Make sure that result never goes beyond 7.
        result %= 7;
    }

    // Make sure that remainder is positive
    if (result < 0)
      result = (result + 7) % 7;

    return result;
}

/* Driver program */
int main()
{
    string str = "12345";
    cout << "Remainder with 7 is "
         << remainderWith7(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find remainder of a large
// number when divided by 7.

class GFG
{
    // Function which return Remainder
    // after dividingthe number by 7
    static int remainderWith7(String num)
    {
        // This series is used to
        // find remainder with 7
        int series[] = {1, 3, 2, -1, -3, -2};

        // Index of next element in series
        int series_index = 0;

        // Initialize result
        int result = 0;

        // Traverse num from end
        for (int i = num.length() - 1; i >= 0; i--)
        {
            /* Find current digit of nun */
            int digit = num.charAt(i) - '0';

            // Add next term to result
            result += digit * series[series_index];

            // Move to next term in series
            series_index = (series_index + 1) % 6;

            // Make sure that result never goes beyond 7.
            result %= 7;
        }

        // Make sure that remainder is positive
        if (result < 0)
        result = (result + 7) % 7;

        return result;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "12345";
        System.out.print("Remainder with 7 is "
                          +remainderWith7(str));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find remainder of
# a large number when divided by 7.

# Function which return Remainder
# after dividing the number by 7
def remainderWith7(num):

    # This series is used to
    # find remainder with 7
    series = [1, 3, 2, -1, -3, -2];

    # Index of next element
    # in series
    series_index = 0;

    # Initialize result
    result = 0;

    # Traverse num from end
    for i in range((len(num) - 1), -1, -1):

        # Find current digit of num
        digit = ord(num[i]) - 48;

        # Add next term to result
        result += digit * series[series_index];

        # Move to next term in series
        series_index = (series_index + 1) % 6;

        # Make sure that result
        # never goes beyond 7.
        result %= 7;

    # Make sure that remainder
    # is positive

    if (result < 0):
        result = (result + 7) % 7;
    return result;

# Driver Code
str = "12345";
print("Remainder with 7 is",
       remainderWith7(str));

# This code is contributed by mits
```

## C#

```
// C# program to find the remainder of
// a large number when divided by 7.
using System;

class GFG
{
    // Function which return Remainder
    // after dividingthe number by 7
    static int remainderWith7(String num)
    {
        // This series is used to
        // find remainder with 7
        int []series = {1, 3, 2, -1, -3, -2};

        // Index of next element in series
        int series_index = 0;

        // Initialize result
        int result = 0;

        // Traverse num from end
        for (int i = num.Length - 1; i >= 0; i--)
        {
            /* Find current digit of nun */
            int digit = num[i] - '0';

            // Add next term to result
            result += digit * series[series_index];

            // Move to next term in series
            series_index = (series_index + 1) % 6;

            // Make sure that result never goes beyond 7.
            result %= 7;
        }

        // Make sure that remainder is positive
        if (result < 0)
        result = (result + 7) % 7;

        return result;
    }

    // Driver code
    public static void Main ()
    {
        String str = "12345";
        Console.Write("Remainder with 7 is " +
                         remainderWith7(str));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find remainder of
// a large number when divided by 7.

/* Function which return Remainder
   after dividing the number by 7 */
function remainderWith7($num)
{

    // This series is used to
    // find remainder with 7
    $series = array(1, 3, 2, -1, -3, -2);

    // Index of next element
    // in series
    $series_index = 0;

    // Initialize result
    $result = 0;

    // Traverse num from end
    for($i = strlen($num) - 1; $i >= 0; $i--)
    {

        // Find current digit of num
        $digit = $num[$i] - '0';

        // Add next term to result
        $result += $digit *
                   $series[$series_index];

        // Move to next term in series
        $series_index = ($series_index + 1) % 6;

        // Make sure that result
        // never goes beyond 7.
        $result %= 7;
    }

    // Make sure that remainder
    // is positive
    if ($result < 0)
    $result = ($result + 7) % 7;

    return $result;
}

// Driver Code
{
    $str = "12345";
    echo "Remainder with 7 is ",
         (remainderWith7($str));
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find remainder of a large
// number when divided by 7.

/* Function which returns Remainder after dividing
the number by 7 */
function remainderWith7(num)
{

    // This series is used to find remainder with 7
    series = [1, 3, 2, -1, -3, -2]

    // Index of next element in series
    var series_index = 0;

    var result = 0; // Initialize result

    // Traverse num from end
    for (var i = num.length - 1; i >= 0; i--)
    {

        /* Find current digit of nun */
        var digit = num[i] - '0';

        // Add next term to result
        result += digit * series[series_index];

        // Move to next term in series
        series_index = (series_index + 1) % 6;

        // Make sure that result never goes beyond 7.
        result %= 7;
    }

    // Make sure that remainder is positive
    if (result < 0)
    result = (result + 7) % 7;

    return result;
}

/* Driver program */
var str = "12345";
document.write("Remainder with 7 is " + remainderWith7(str));

// This code is contributed by oob2000.

</script>
```

**输出:**

```
Remainder with 7 is 4
```

本文由**库尔迪普·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。