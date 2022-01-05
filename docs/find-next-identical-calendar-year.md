# 查找下一个相同的日历年

> 原文:[https://www . geesforgeks . org/find-next-相同-日历年/](https://www.geeksforgeeks.org/find-next-identical-calendar-year/)

给你一个 Y 年，找到下一个与 Y 相同的日历年。
**例:**

```
Input : 2017
Output : 2023

Input : 2018
Output : 2029
```

如果满足以下两个条件，一年 **x** 与给定的上一年 **y** 相同。

1.  x 和 y 从同一天开始。
2.  如果 y 是闰年，那么 x 也是。如果 y 不是闰年，那么 x 也不是。

想法是逐一检查所有年份(从明年开始)。我们记录前进的天数。如果总移动天数为 7 天，则当年从同一天开始。我们还检查当年的闰是否与 y 相同。如果两个条件都满足，我们就返回当年。

## C++

```
// C++ program to find next identical year
#include<iostream>
using namespace std;

// Function for finding extra days of year
// more than complete weeks
int extraDays(int y)
{
    // If current year is a leap year, then
    // it number of weekdays move ahead by
    // 2 in terms of weekdays.
    if (y%400==0 || y%100!=0 && y%4==0)
        return 2;

    // Else number of weekdays move ahead
    // by 1.
    return 1;
}

// Returns next identical year.
int nextYear(int y)
{
    // Find number of days moved ahead by y
    int days = extraDays(y);

    // Start from next year
    int x = y + 1;

    // Count total number of weekdays
    // moved ahead so far.
    for (int sum=0; ; x++)
    {
        sum = (sum + extraDays(x)) % 7;

        // If sum is divisible by 7 and leap-ness
        // of x is same as y, return x.
        if ( sum==0 && (extraDays(x) == days))
            return x;
    }

    return x;
}

// driver program
int main()
{
    int y = 2018;
    cout << nextYear(y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next identical year
class GFG {

// Function for finding extra days of year
// more than complete weeks
static int extraDays(int y)
{
    // If current year is a leap year, then
    // it number of weekdays move ahead by
    // 2 in terms of weekdays.
    if (y % 400 == 0 || y % 100 != 0 && y % 4 == 0)
        return 2;

    // Else number of weekdays move ahead
    // by 1.
    return 1;
}

// Returns next identical year.
static int nextYear(int y)
{
    // Find number of days moved ahead by y
    int days = extraDays(y);

    // Start from next year
    int x = y + 1;

    // Count total number of weekdays
    // moved ahead so far.
    for (int sum = 0; ; x++)
    {
        sum = (sum + extraDays(x)) % 7;

        // If sum is divisible by 7 and leap-ness
        // of x is same as y, return x.
        if ( sum == 0 && (extraDays(x) == days))
            return x;
    }

}

// Driver code
public static void main(String[] args)
{
    int y = 2018;
    System.out.println(nextYear(y));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find next identical year

# Function for finding extra days of year
# more than complete weeks
def extraDays(y) :

    # If current year is a leap year, then
    # it number of weekdays move ahead by
    # 2 in terms of weekdays.
    if (y % 400 == 0 or y % 100 != 0 and y % 4 == 0) :
        return 2

    # Else number of weekdays move ahead
    # by 1.
    return 1

# Returns next identical year.
def nextYear(y) :

    # Find number of days moved ahead by y
    days = extraDays(y)

    # Start from next year
    x = y + 1

    # Count total number of weekdays
    # moved ahead so far.
    Sum = 0
    while(True) :

        Sum = (Sum + extraDays(x)) % 7

        # If sum is divisible by 7 and leap-ness
        # of x is same as y, return x.
        if ( Sum == 0 and (extraDays(x) == days)) :
            return x

        x += 1

    return x

y = 2018
print(nextYear(y))

# This code is contributed by mukesh07.
```

## C#

```
// C# program to find next identical year
using System;

class GFG
{

// Function for finding extra days of year
// more than complete weeks
static int extraDays(int y)
{
    // If current year is a leap year, then
    // it number of weekdays move ahead by
    // 2 in terms of weekdays.
    if (y % 400 == 0 || y % 100 != 0 && y % 4 == 0)
        return 2;

    // Else number of weekdays move ahead
    // by 1.
    return 1;
}

// Returns next identical year.
static int nextYear(int y)
{
    // Find number of days moved ahead by y
    int days = extraDays(y);

    // Start from next year
    int x = y + 1;

    // Count total number of weekdays
    // moved ahead so far.
    for (int sum = 0; ; x++)
    {
        sum = (sum + extraDays(x)) % 7;

        // If sum is divisible by 7 and leap-ness
        // of x is same as y, return x.
        if ( sum == 0 && (extraDays(x) == days))
            return x;
    }

}

// Driver code
public static void Main(String[] args)
{
    int y = 2018;
    Console.WriteLine(nextYear(y));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// next identical year

// Function for finding extra days
// of year more than complete weeks

function extraDays($y)
{
    // If current year is a leap year,
    // then number of weekdays move
    // ahead by 2 in terms of weekdays.
    if ($y % 400 == 0 ||
        $y % 100 != 0 &&
        $y % 4 == 0)
        return 2;

    // Else number of weekdays
    // move ahead by 1.
    return 1;
}

// Returns next identical year.
function nextYear($y)
{
    // Find number of days
    // moved ahead by y
    $days = extraDays($y);

    // Start from next year
    $x = $y + 1;

    // Count total number of weekdays
    // moved ahead so far.
    for ($sum = 0; ; $x++)
    {
        $sum = ($sum + extraDays($x)) % 7;

        // If sum is divisible by 7
        // and leap-ness of x is
        // same as y, return x.
        if ( $sum == 0 && (extraDays($x) == $days))
            return $x;
    }

    return $x;
}

// Driver Code
$y = 2018;
echo nextYear($y);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function for finding extra days of year
// more than complete weeks
function extraDays(y)
{

    // If current year is a leap year, then
    // it number of weekdays move ahead by
    // 2 in terms of weekdays.
    if (y % 400 == 0 || y % 100 != 0 && y % 4 == 0)
        return 2;

    // Else number of weekdays move ahead
    // by 1.
    return 1;
}

// Returns next identical year.
function nextYear(y)
{
    // Find number of days moved ahead by y
    let days = extraDays(y);

    // Start from next year
    let x = y + 1;

    // Count total number of weekdays
    // moved ahead so far.
    for (let sum = 0; ; x++)
    {
        sum = (sum + extraDays(x)) % 7;

        // If sum is divisible by 7 and leap-ness
        // of x is same as y, return x.
        if ( sum == 0 && (extraDays(x) == days))
            return x;
    }

}

// Driver Code
    let y = 2018;
    document.write(nextYear(y));

        // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
2029
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。