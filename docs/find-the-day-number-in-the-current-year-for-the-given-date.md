# 查找给定日期的本年日数

> 原文:[https://www . geesforgeks . org/查找给定日期的当前年份中的天数/](https://www.geeksforgeeks.org/find-the-day-number-in-the-current-year-for-the-given-date/)

给定一个表示日期格式为 **YYYY-MM-DD** 的字符串 **str** ，任务是查找当前年份的日号。比如**1<sup>ST</sup>**1 月是一年中的 **1 <sup>st</sup>** 日，**2<sup>nd</sup>T15】1 月是一年中的**2<sup>nd</sup>T19】日，**1<sup>ST</sup>T23】2 月是一年中的**32<sup>nd</sup>T27】日等等
**例:********** 

> **输入:** str = "2019-01-09"
> **输出:** 9
> **输入:** str = "2003-03-01"
> **输出:** 60

**进场:**

*   从给定日期中提取年、月和日，并将其存储在变量**年**、**月**和**日**中。
*   创建一个数组**days【】**其中**days【I】**将存储 **i <sup>th</sup>** 月的天数。
*   更新**计数=天[0] +天[1] + … +天[月–1]**获得前几个月所有过去天数的计数。
*   如果给定的年份是闰年，则将该计数增加 **1** ，以便计算 **29 <sup>日</sup>2 月**。
*   最后，将**日**加到当前月的日数上，打印出最终的**日数**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int days[] = { 31, 28, 31, 30, 31, 30,
               31, 31, 30, 31, 30, 31 };

// Function to return the day number
// of the year for the given date
int dayOfYear(string date)
{
    // Extract the year, month and the
    // day from the date string
    int year = stoi(date.substr(0, 4));
    int month = stoi(date.substr(5, 2));
    int day = stoi(date.substr(8));

    // If current year is a leap year and the date
    // given is after the 28th of February then
    // it must include the 29th February
    if (month > 2 && year % 4 == 0
        && (year % 100 != 0 || year % 400 == 0)) {
        ++day;
    }

    // Add the days in the previous months
    while (month-- > 0) {
        day = day + days[month - 1];
    }
    return day;
}

// Driver code
int main()
{
    string date = "2019-01-09";
    cout << dayOfYear(date);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static int days [] = { 31, 28, 31, 30, 31, 30,
                           31, 31, 30, 31, 30, 31 };

    // Function to return the day number
    // of the year for the given date
    static int dayOfYear(String date)
    {
        // Extract the year, month and the
        // day from the date string
        int year = Integer.parseInt(date.substring(0, 4));

        int month = Integer.parseInt(date.substring(5, 7));

        int day = Integer.parseInt(date.substring(8));

        // If current year is a leap year and the date
        // given is after the 28th of February then
        // it must include the 29th February
        if (month > 2 && year % 4 == 0 &&
           (year % 100 != 0 || year % 400 == 0))
        {
            ++day;
        }

        // Add the days in the previous months
        while (--month > 0)
        {
            day = day + days[month - 1];
        }
        return day;
    }

    // Driver code
    public static void main (String[] args)
    {
        String date = "2019-01-09";
        System.out.println(dayOfYear(date));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach
days = [31, 28, 31, 30, 31, 30,
        31, 31, 30, 31, 30, 31];

# Function to return the day number
# of the year for the given date
def dayOfYear(date):

    # Extract the year, month and the
    # day from the date string
    year = (int)(date[0:4]);
    month = (int)(date[5:7]);
    day = (int)(date[8:]);

    # If current year is a leap year and the date
    # given is after the 28th of February then
    # it must include the 29th February
    if (month > 2 and year % 4 == 0 and
       (year % 100 != 0 or year % 400 == 0)):
        day += 1;

    # Add the days in the previous months
    month -= 1;
    while (month > 0):
        day = day + days[month - 1];
        month -= 1;
    return day;

# Driver code
if __name__ == '__main__':
    date = "2019-01-09";
    print(dayOfYear(date));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int [] days = { 31, 28, 31, 30, 31, 30,
                           31, 31, 30, 31, 30, 31 };

    // Function to return the day number
    // of the year for the given date
    static int dayOfYear(string date)
    {
        // Extract the year, month and the
        // day from the date string
        int year = Int32.Parse(date.Substring(0, 4));

        int month = Int32.Parse(date.Substring(5, 2));

        int day = Int32.Parse(date.Substring(8));

        // If current year is a leap year and the date
        // given is after the 28th of February then
        // it must include the 29th February
        if (month > 2 && year % 4 == 0 &&
           (year % 100 != 0 || year % 400 == 0))
        {
            ++day;
        }

        // Add the days in the previous months
        while (--month > 0)
        {
            day = day + days[month - 1];

        }
        return day;
    }

    // Driver code
    public static void Main ()
    {
        String date = "2019-01-09";
        Console.WriteLine(dayOfYear(date));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var days= [31, 28, 31, 30, 31, 30,
               31, 31, 30, 31, 30, 31 ];

// Function to return the day number
// of the year for the given date
function dayOfYear( date)
{
    // Extract the year, month and the
    // day from the date string
    var year = parseInt(date.substring(0, 4));
    var month = parseInt(date.substring(5, 6));
    var day = parseInt(date.substring(8));

    // If current year is a leap year and the date
    // given is after the 28th of February then
    // it must include the 29th February
    if (month > 2 && year % 4 == 0
        && (year % 100 != 0 || year % 400 == 0)) {
        ++day;
    }

    // Add the days in the previous months
    while (month-- > 0) {
        day = day + days[month - 1];
    }
    return day;
}

// Driver code
var date = "2019-01-09";
document.write( dayOfYear(date));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
9
```