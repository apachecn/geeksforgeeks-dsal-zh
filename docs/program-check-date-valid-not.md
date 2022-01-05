# 检查日期是否有效的程序

> 原文:[https://www.geeksforgeeks.org/program-check-date-valid-not/](https://www.geeksforgeeks.org/program-check-date-valid-not/)

给定一个日期，检查它是否有效。可以假设给定日期在 1800 年 1 月 1 日至 9999 年 12 月 31 日之间。

**示例:**

```
Input : d = 10, m = 12, y = 2000
Output : Yes
The given date 10/12/2000 is valid

Input  : d = 30, m = 2, y = 2000
Output : No
The given date 30/2/2000 is invalid. The
February month cannot have 30 as day.
```

想法很简单。我们需要处理以下事情。
1) y、m、d 在允许范围内。
2)2 月天数在允许范围内，[闰年](https://www.geeksforgeeks.org/program-check-given-year-leap-year/)处理。
3)处理 30 天月中的天数。

下面是检查给定年份是否有效的实现。

## C++

```
// C++ program to check if
// given date is valid or not.
#include<iostream>
using namespace std;

const int MAX_VALID_YR = 9999;
const int MIN_VALID_YR = 1800;

// Returns true if
// given year is valid.
bool isLeap(int year)
{
// Return true if year
// is a multiple pf 4 and
// not multiple of 100.
// OR year is multiple of 400.
return (((year % 4 == 0) &&
         (year % 100 != 0)) ||
         (year % 400 == 0));
}

// Returns true if given
// year is valid or not.
bool isValidDate(int d, int m, int y)
{
    // If year, month and day
    // are not in given range
    if (y > MAX_VALID_YR ||
        y < MIN_VALID_YR)
    return false;
    if (m < 1 || m > 12)
    return false;
    if (d < 1 || d > 31)
    return false;

    // Handle February month
    // with leap year
    if (m == 2)
    {
        if (isLeap(y))
        return (d <= 29);
        else
        return (d <= 28);
    }

    // Months of April, June,
    // Sept and Nov must have
    // number of days less than
    // or equal to 30.
    if (m == 4 || m == 6 ||
        m == 9 || m == 11)
        return (d <= 30);

    return true;
}

// Driver code
int main(void)
{
isValidDate(10, 12, 2000)? cout << "Yes\n" :
                           cout << "No\n";

isValidDate(31, 11, 2000)? cout << "Yes\n" :
                           cout << "No\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// given date is valid or not.
import java.io.*;

class GFG
{

    static int MAX_VALID_YR = 9999;
    static int MIN_VALID_YR = 1800;

    // Returns true if
    // given year is valid.
    static boolean isLeap(int year)
    {
        // Return true if year is
        // a multiple of 4 and not
        // multiple of 100.
        // OR year is multiple of 400.
        return (((year % 4 == 0) &&
                 (year % 100 != 0)) ||
                 (year % 400 == 0));
    }

    // Returns true if given
    // year is valid or not.
    static boolean isValidDate(int d,
                               int m,
                               int y)
    {
        // If year, month and day
        // are not in given range
        if (y > MAX_VALID_YR ||
            y < MIN_VALID_YR)
            return false;
        if (m < 1 || m > 12)
            return false;
        if (d < 1 || d > 31)
            return false;

        // Handle February month
        // with leap year
        if (m == 2)
        {
            if (isLeap(y))
                return (d <= 29);
            else
                return (d <= 28);
        }

        // Months of April, June,
        // Sept and Nov must have
        // number of days less than
        // or equal to 30.
        if (m == 4 || m == 6 ||
            m == 9 || m == 11)
            return (d <= 30);

        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        if (isValidDate(10, 12, 2000))
            System.out.println("Yes");
        else
            System.out.println("No");

        if (isValidDate(31, 11, 2000))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python Program to check
# if a date is valid or not

import datetime
def date_validation(day, month, year):

    isValidDate = True

    try :
        datetime.datetime(int(year),
                          int(month), int(day))

    except ValueError :
        isValidDate = False

    if(isValidDate) :
        print ("Yes")
    else :
        print ("No")

date_validation(10,12,2000)
date_validation(31,11,2000)

# This code is contributed by ajay0007
```

## C#

```
// C# program to check if
// given date is valid or not.
using System;

class GFG
{

    const int MAX_VALID_YR = 9999;
    const int MIN_VALID_YR = 1800;

    // Returns true if
    // given year is valid.
    static bool isLeap(int year)
    {

        // Return true if year is a
        // multiple of 4 and not
        // multiple of 100\. OR year
        // is multiple of 400.
        return (((year % 4 == 0) &&
                 (year % 100 != 0)) ||
                 (year % 400 == 0));
    }

    // Returns true if given
    // year is valid or not.
    static bool isValidDate(int d,
                            int m,
                            int y)
    {

        // If year, month and day
        // are not in given range
        if (y > MAX_VALID_YR ||
            y < MIN_VALID_YR)
            return false;
        if (m < 1 || m > 12)
            return false;
        if (d < 1 || d > 31)
            return false;

        // Handle February month
        // with leap year
        if (m == 2)
        {
            if (isLeap(y))
                return (d <= 29);
            else
                return (d <= 28);
        }

        // Months of April, June,
        // Sept and Nov must have
        // number of days less than
        // or equal to 30.
        if (m == 4 || m == 6 ||
            m == 9 || m == 11)
            return (d <= 30);

        return true;
    }

    // Driver code
    public static void Main()
    {

        if (isValidDate(10, 12, 2000))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        if (isValidDate(31, 11, 2000))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed
// by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// given date is valid or not.

// Returns true if
// given year is valid.
function isLeap($year)
{

// Return true if year is
// a multiple of 4 and
// not multiple of 100.
// OR year is multiple of 400.
return ((($year % 4 == 0) &&
         ($year % 100 != 0)) ||
         ($year % 400 == 0));
}
// Returns true if given
// year is valid or not.
function isValidDate($d, $m, $y)
{
    $MAX_VALID_YR = 9999;
    $MIN_VALID_YR = 1800;
    // If year, month and day
    // are not in given range
    if ($y > $MAX_VALID_YR ||
        $y < $MIN_VALID_YR)
    return false;
    if ($m < 1 || $m > 12)
    return false;
    if ($d < 1 || $d > 31)
    return false;

    // Handle February month
    // with leap year
    if ($m == 2)
    {
        if (isLeap($y))
        return ($d <= 29);
        else
        return ($d <= 28);
    }

    // Months of April, June,
    // Sept and Nov must have
    // number of days less than
    // or equal to 30.
    if ($m == 4 || $m == 6 ||
        $m == 9 || $m == 11)
        return ($d <= 30);

    return true;
}

// Driver code
{
if(isValidDate(10, 12, 2000))
echo "Yes\n" ;
else
echo "No\n";

if(isValidDate(31, 11, 2000))
    echo "Yes\n" ;
else
echo "No\n";

}

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if
// given date is valid or not.
const MAX_VALID_YR = 9999;
const MIN_VALID_YR = 1800;

// Returns true if
// given year is valid.
function isLeap(year)
{

    // Return true if year
    // is a multiple pf 4 and
    // not multiple of 100.
    // OR year is multiple of 400.
    return (((year % 4 == 0) &&
             (year % 100 != 0)) ||
             (year % 400 == 0));
}

// Returns true if given
// year is valid or not.
function isValidDate(d, m, y)
{

    // If year, month and day
    // are not in given range
    if (y > MAX_VALID_YR ||
        y < MIN_VALID_YR)
        return false;

    if (m < 1 || m > 12)
        return false;
    if (d < 1 || d > 31)
        return false;

    // Handle February month
    // with leap year
    if (m == 2)
    {
        if (isLeap(y))
            return (d <= 29);
        else
            return (d <= 28);
    }

    // Months of April, June,
    // Sept and Nov must have
    // number of days less than
    // or equal to 30.
    if (m == 4 || m == 6 ||
        m == 9 || m == 11)
        return (d <= 30);

    return true;
}

// Driver code
isValidDate(10, 12, 2000) ? document.write("Yes<br>") :
                            document.write("No<br>");

isValidDate(31, 11, 2000) ? document.write("Yes<br>") :
                            document.write("No<br>");

// This code is contributed by souravmahato348

</script>
```

**输出:**

```
Yes
No
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
本文由 **RAHUL NITKKR** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。