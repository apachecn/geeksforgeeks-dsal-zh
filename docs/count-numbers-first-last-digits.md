# 用相同的第一个和最后一个数字计数

> 原文:[https://www . geesforgeks . org/count-numbers-first-last-digits/](https://www.geeksforgeeks.org/count-numbers-first-last-digits/)

给定一个时间间隔，任务是计算具有相同的第一个和最后一个数字的数字。例如 **1** 23 **1** 的第一个和最后一个数字相同。

**示例:**

```
Input  : start = 7,  end : 68
Output : 9
Number with same first and last digits are,
7 8 9 11 22 33 44 55 66.

Input  : start = 5,  end : 40
Output : 8
```

让我们首先考虑下面的例子来理解这种方法。

```
From 120 to 130, only 121 has same starting and ending digit
From 440 to 450, only 444 has same starting and ending digit
From 1050 to 1060, only 1051 has same starting and ending digit
```

从上面的例子中，我们可以观察到，在每十个数字区间中，除了 1 到 10 之外，我们只有一个数字具有给定的性质，其中 9 个数字(都是一位数)具有相同的开始和结束数字。
利用上述性质我们可以解决给定的问题，首先我们把给定的区间分成两部分，即如果区间是 l 到 r，我们把这个区间分成 1 到 l 和 1 到 r，我们的答案是通过从第二个查询中减去第一个查询的结果得到的。
现在我们仍然要找到给定属性在 1 到 x 范围内的数字的计数，为此，我们将 x 除以 10，得到 10 跨度的数量。考虑到一位数，我们在跨度上加 9。如果 x 的最后一个数字小于 x 的第一个数字，那么在最终答案中应该减少 1 以丢弃最后十个跨度数，因为该数超出范围。

## C++

```
// C++ program to get count of numbers with
// same start and end digit in an interval
#include <bits/stdc++.h>
using namespace std;

// Utility method to get first digit of x
int getFirstDigit(int x)
{
    while (x >= 10)
        x /= 10;
    return x;
}

// method to return count of numbers with same
// starting and ending digit from 1 upto x
int getCountWithSameStartAndEndFrom1(int x)
{
    if (x < 10)
        return x;

    // get ten-spans from 1 to x
    int tens = x / 10;

    // add 9 to consider all 1 digit numbers
    int res = tens + 9;

    // Find first and last digits
    int firstDigit = getFirstDigit(x);
    int lastDigit = x % 10;

    // If last digit is smaller than first digit
    // then decrease count by 1
    if (lastDigit < firstDigit)
        res--;

    return res;
}

// Method to return count of numbers with same starting
// and ending digit between start and end
int getCountWithSameStartAndEnd(int start, int end)
{
    return getCountWithSameStartAndEndFrom1(end)
    - getCountWithSameStartAndEndFrom1(start - 1);
}

// Driver code to test above methods
int main()
{
    int start = 5, end = 40;

    cout << getCountWithSameStartAndEnd(start, end);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get count of numbers with
// same start and end digit in an interval
import java.util.*;

class Digits {
    // Utility method to get first digit of x
    public static int getFirstDigit(int x)
    {
        while (x >= 10)
            x /= 10;
        return x;
    }

    // method to return count of numbers with same
    // starting and ending digit from 1 upto x
    public static int getCountWithSameStartAndEndFrom1(int x)
    {
        if (x < 10)
            return x;

        // get ten-spans from 1 to x
        int tens = x / 10;

        // add 9 to consider all 1 digit numbers
        int res = tens + 9;

        // Find first and last digits
        int firstDigit = getFirstDigit(x);
        int lastDigit = x % 10;

        // If last digit is smaller than first
        // digit then decrease count by 1
        if (lastDigit < firstDigit)
            res--;

        return res;
    }

    // Method to return count of numbers with same
    // starting and ending digit between start and end
    public static int getCountWithSameStartAndEnd(int start,
                                                  int end)
    {
        return getCountWithSameStartAndEndFrom1(end)
        - getCountWithSameStartAndEndFrom1(start - 1);
    }

    // driver code
    public static void main(String[] args)
    {
        int start = 5, end = 40;
        System.out.print(getCountWithSameStartAndEnd(start,
                                                     end));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program to get count of numbers with
# same start and end digit in an interval

# Utility method to get first digit of x
def getFirstDigit(x) :
    while (x >= 10) :
        x //= 10
    return x

# method to return count of numbers with same
# starting and ending digit from 1 upto x
def getCountWithSameStartAndEndFrom1(x) :
    if (x < 10):
        return x

    # get ten-spans from 1 to x
    tens = x // 10

    # add 9 to consider all 1 digit numbers
    res = tens + 9

    # Find first and last digits
    firstDigit = getFirstDigit(x)
    lastDigit = x % 10

    # If last digit is smaller than first digit
    # then decrease count by 1
    if (lastDigit < firstDigit) :
        res = res - 1

    return res

# Method to return count of numbers with same starting
# and ending digit between start and end
def getCountWithSameStartAndEnd(start, end) :
    return (getCountWithSameStartAndEndFrom1(end) -
           getCountWithSameStartAndEndFrom1(start - 1))

# Driver Code
start = 5
end = 40
print(getCountWithSameStartAndEnd(start, end))

# This code is contributed by rishabh_jain
# Improved by cidacoder
```

## C#

```
// C# program to get count of numbers with
// same start and end digit in an interval
using System;

class GFG {

    // Utility method to get first digit
    // of x
    public static int getFirstDigit(int x)
    {
        while (x >= 10)
            x /= 10;

        return x;
    }

    // method to return count of numbers
    // with same starting and ending digit
    // from 1 upto x
    public static int getCountWithSameStartAndEndFrom1(
                                                  int x)
    {

        if (x < 10)
            return x;

        // get ten-spans from 1 to x
        int tens = x / 10;

        // add 9 to consider all 1 digit
        // numbers
        int res = tens + 9;

        // Find first and last digits
        int firstDigit = getFirstDigit(x);
        int lastDigit = x % 10;

        // If last digit is smaller than
        // first digit then decrease count
        // by 1
        if (lastDigit < firstDigit)
            res--;

        return res;
    }

    // Method to return count of numbers
    // with same starting and ending digit
    // between start and end
    public static int getCountWithSameStartAndEnd(
                                 int start, int end)
    {
        return getCountWithSameStartAndEndFrom1(end)
        - getCountWithSameStartAndEndFrom1(start - 1);
    }

    // driver code
    public static void Main()
    {
        int start = 5, end = 40;

        Console.Write(getCountWithSameStartAndEnd(start,
                                                end));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get count of numbers with
// same start and end digit in an interval

// method to get first digit of x
function getFirstDigit($x)
{
    while ($x >= 10)
        $x /= 10;
    return $x;
}

// method to return count
// of numbers with same
// starting and ending
// digit from 1 upto x
function getCountWithSameStartAndEndFrom1($x)
{
    if ($x < 10)
        return $x;

    // get ten-spans from 1 to x
    $tens = $x / 10;

    // add 9 to consider all
    // 1 digit numbers
    $res = $tens + 9;

    // Find first and last digits
    $firstDigit = getFirstDigit($x);
    $lastDigit = $x % 10;

    // If last digit is smaller
    // than first digit
    // then decrease count by 1
    if ($lastDigit < $firstDigit)
        $res--;

    return $res;
}

// Method to return count of
// numbers with same starting
// and ending digit between
// start and end
function getCountWithSameStartAndEnd($start, $end)
{
    return getCountWithSameStartAndEndFrom1($end)
          - getCountWithSameStartAndEndFrom1($start - 1);
}

    // Driver Code
    $start = 5;
    $end = 40;
    echo getCountWithSameStartAndEnd($start, $end);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to get count of numbers with
// same start and end digit in an interval

    // Utility method to get first digit of x
    function getFirstDigit(x)
    {
        while (x >= 10)
            x /= 10;
        return x;
    }

    // method to return count of numbers with same
    // starting and ending digit from 1 upto x
    function getCountWithSameStartAndEndFrom1(x)
    {
        if (x < 10)
            return x;

        // get ten-spans from 1 to x
        let tens = x / 10;

        // add 9 to consider all 1 digit numbers
        let res = tens + 9;

        // Find first and last digits
        let firstDigit = getFirstDigit(x);
        let lastDigit = x % 10;

        // If last digit is smaller than first
        // digit then decrease count by 1
        if (lastDigit < firstDigit)
            res--;

        return res;
    }

    // Method to return count of numbers with same
    // starting and ending digit between start and end
    function getCountWithSameStartAndEnd(start,
                                               end)
    {
        return getCountWithSameStartAndEndFrom1(end)
        - getCountWithSameStartAndEndFrom1(start - 1);
    }

// Driver code
      let start = 5, end = 40;
      document.write(getCountWithSameStartAndEnd(start,
                                                     end)); 
</script>
```

**输出:**

```
8
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。