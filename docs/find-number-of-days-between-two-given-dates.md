# 找出两个给定日期之间的天数

> 原文:[https://www . geesforgeks . org/find-两个给定日期之间的天数/](https://www.geeksforgeeks.org/find-number-of-days-between-two-given-dates/)

给定两个日期，找出它们之间的总天数。天数必须在 O(1)时间和 O(1)辅助空间中计算。

**示例:**

```
Input: dt1 = {10, 2, 2014}
       dt2 = {10, 3, 2015}
Output: 393
dt1 represents "10-Feb-2014" and dt2 represents "10-Mar-2015"
The difference is 365 + 28

Input: dt1 = {10, 2, 2000}
       dt2 = {10, 3, 2000}
Output: 29
Note that 2000 is a leap year

Input: dt1 = {10, 2, 2000}
       dt2 = {10, 2, 2000}
Output: 0
Both dates are same

Input:   dt1 = {1, 2, 2000};
         dt2 = {1, 2, 2004};
Output: 1461
Number of days is 365*4 + 1
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/find-number-of-days-between-two-given-dates5400/1)

一个简单的解决方案是从 dt1 开始，持续计算天数，直到到达 dt2。此解决方案需要超过 O(1)的时间。
一个更好更简单的解决方案是从开始统计 dt1 前的总天数，即从 00/00/0000 到 dt1 的总天数，然后统计 dt2 前的总天数。最后返回两个计数之间的差值。

```
Let the given two dates be "1-Feb-2000" and "1-Feb-2004"
dt1 = {1, 2, 2000};
dt2 = {1, 2, 2004};
Count number of days before dt1\. Let this count be n1.
Every leap year adds one extra day (29 Feb) to total days.
n1 = 2000*365 + 31 + 1 + Number of leap years 
Count of leap years for a date 'd/m/y' can be calculated 
using the following formula:
Number leap years 
 = floor(y/4) - floor(y/100) + floor(y/400) if m > 2
  = floor((y-1)/4) - floor((y-1)/100) + floor((y-1)/400) if m <= 2
All above divisions must be done using integer arithmetic
So that the remainder is ignored.
For 01/01/2000, leap year count is 1999/4 - 1999/100 
+ 1999/400 which is 499 - 19 + 4 = 484
Therefore n1 is 2000*365 + 31 + 1 + 484

Similarly, the count number of days before dt2\. 
Let this the count be n2.Finally, return n2-n1
```

以下是上述想法的实现。

## C++

```
// C++ program two find number of
// days between two given dates
#include <iostream>
using namespace std;

// A date has day 'd', month 'm' and year 'y'
struct Date {
    int d, m, y;
};

// To store number of days in
// all months from January to Dec.
const int monthDays[12]
    = { 31, 28, 31, 30, 31, 30,
       31, 31, 30, 31, 30, 31 };

// This function counts number of
// leap years before the given date
int countLeapYears(Date d)
{
    int years = d.y;

    // Check if the current year needs to be
    //  considered for the count of leap years
    // or not
    if (d.m <= 2)
        years--;

    // An year is a leap year if it
    // is a multiple of 4,
    // multiple of 400 and not a
     // multiple of 100.
    return years / 4
           - years / 100
           + years / 400;
}

// This function returns number of
// days between two given dates
int getDifference(Date dt1, Date dt2)
{
    // COUNT TOTAL NUMBER OF DAYS
    // BEFORE FIRST DATE 'dt1'

    // initialize count using years and day
    long int n1 = dt1.y * 365 + dt1.d;

    // Add days for months in given date
    for (int i = 0; i < dt1.m - 1; i++)
        n1 += monthDays[i];

    // Since every leap year is of 366 days,
    // Add a day for every leap year
    n1 += countLeapYears(dt1);

    // SIMILARLY, COUNT TOTAL NUMBER OF
    // DAYS BEFORE 'dt2'

    long int n2 = dt2.y * 365 + dt2.d;
    for (int i = 0; i < dt2.m - 1; i++)
        n2 += monthDays[i];
    n2 += countLeapYears(dt2);

    // return difference between two counts
    return (n2 - n1);
}

// Driver code
int main()
{
    Date dt1 = { 1, 2, 2000 };
    Date dt2 = { 1, 2, 2004 };

    // Function call
    cout << "Difference between two dates is "
         << getDifference(dt1, dt2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program two find number of
// days between two given dates

class GFG
{

    // A date has day 'd', month 'm' and year 'y'
    static class Date
    {
        int d, m, y;

        public Date(int d, int m, int y)
        {
            this.d = d;
            this.m = m;
            this.y = y;
        }

    };

    // To store number of days in
    // all months from January to Dec.
    static int monthDays[] = {31, 28, 31, 30, 31, 30,
                            31, 31, 30, 31, 30, 31};

    // This function counts number of
    // leap years before the given date
    static int countLeapYears(Date d)
    {
        int years = d.y;

        // Check if the current year needs to be considered
        // for the count of leap years or not
        if (d.m <= 2)
        {
            years--;
        }

        // An year is a leap year if it is a multiple of 4,
        // multiple of 400 and not a multiple of 100.
        return years / 4 - years / 100 + years / 400;
    }

    // This function returns number
    // of days between two given dates
    static int getDifference(Date dt1, Date dt2)
    {
        // COUNT TOTAL NUMBER OF DAYS BEFORE FIRST DATE 'dt1'

        // initialize count using years and day
        int n1 = dt1.y * 365 + dt1.d;

        // Add days for months in given date
        for (int i = 0; i < dt1.m - 1; i++)
        {
            n1 += monthDays[i];
        }

        // Since every leap year is of 366 days,
        // Add a day for every leap year
        n1 += countLeapYears(dt1);

        // SIMILARLY, COUNT TOTAL NUMBER OF DAYS BEFORE 'dt2'
        int n2 = dt2.y * 365 + dt2.d;
        for (int i = 0; i < dt2.m - 1; i++)
        {
            n2 += monthDays[i];
        }
        n2 += countLeapYears(dt2);

        // return difference between two counts
        return (n2 - n1);
    }

    // Driver code
    public static void main(String[] args)
    {
        Date dt1 = new Date(1, 2, 2000);
        Date dt2 = new Date(1, 2, 2004);
        System.out.println("Difference between two dates is " +
                            getDifference(dt1, dt2));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program two find number of
# days between two given dates

# A date has day 'd', month
# 'm' and year 'y'

class Date:
    def __init__(self, d, m, y):
        self.d = d
        self.m = m
        self.y = y

# To store number of days in
# all months from January to Dec.
monthDays = [31, 28, 31, 30, 31, 30,
             31, 31, 30, 31, 30, 31]

# This function counts number of
# leap years before the given date

def countLeapYears(d):

    years = d.y

    # Check if the current year needs
    # to be considered for the count
    # of leap years or not
    if (d.m <= 2):
        years -= 1

    # An year is a leap year if it is a
    # multiple of 4, multiple of 400 and
    # not a multiple of 100.
    ans = int(years / 4)
    ans -= int(years / 100)
    ans += int(years / 400)
    return ans

# This function returns number of
# days between two given dates

def getDifference(dt1, dt2):

    # COUNT TOTAL NUMBER OF DAYS
    # BEFORE FIRST DATE 'dt1'

    # initialize count using years and day
    n1 = dt1.y * 365 + dt1.d

    # Add days for months in given date
    for i in range(0, dt1.m - 1):
        n1 += monthDays[i]

    # Since every leap year is of 366 days,
    # Add a day for every leap year
    n1 += countLeapYears(dt1)

    # SIMILARLY, COUNT TOTAL NUMBER
    # OF DAYS BEFORE 'dt2'
    n2 = dt2.y * 365 + dt2.d
    for i in range(0, dt2.m - 1):
        n2 += monthDays[i]
    n2 += countLeapYears(dt2)

    # return difference between
    # two counts
    return (n2 - n1)

# Driver Code
dt1 = Date(1, 9, 2014)
dt2 = Date(3, 9, 2020)

# Function call
print("Difference between two dates is",
      getDifference(dt1, dt2))

# This code is contributed by Smitha
```

## C#

```
// C# program two find number of
// days between two given dates
using System;

class GFG {

    // A date has day 'd', month 'm' and year 'y'
    public class Date {
        public int d, m, y;

        public Date(int d, int m, int y)
        {
            this.d = d;
            this.m = m;
            this.y = y;
        }
    };

    // To store number of days in
    // all months from January to Dec.
    static int[] monthDays = { 31, 28, 31,
                               30, 31, 30,
                               31, 31, 30,
                               31, 30, 31 };

    // This function counts number of
    // leap years before the given date
    static int countLeapYears(Date d)
    {
        int years = d.y;

        // Check if the current year
        // needs to be considered
        // for the count of leap years or not
        if (d.m <= 2) {
            years--;
        }

        // An year is a leap year if it is
        // a multiple of 4, multiple of 400
        // and not a multiple of 100.
        return years / 4
               - years / 100
               + years / 400;
    }

    // This function returns number
    // of days between two given dates
    static int getDifference(Date dt1, Date dt2)
    {
        // COUNT TOTAL NUMBER OF DAYS
        // BEFORE FIRST DATE 'dt1'

        // initialize count using years and day
        int n1 = dt1.y * 365 + dt1.d;

        // Add days for months in given date
        for (int i = 0; i < dt1.m - 1; i++)
        {
            n1 += monthDays[i];
        }

        // Since every leap year is of 366 days,
        // Add a day for every leap year
        n1 += countLeapYears(dt1);

        // SIMILARLY, COUNT TOTAL
        // NUMBER OF DAYS BEFORE 'dt2'
        int n2 = dt2.y * 365 + dt2.d;
        for (int i = 0; i < dt2.m - 1; i++)
        {
            n2 += monthDays[i];
        }
        n2 += countLeapYears(dt2);

        // return difference between two counts
        return (n2 - n1);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Date dt1 = new Date(1, 2, 2000);
        Date dt2 = new Date(1, 2, 2004);

        // Function call
        Console.WriteLine("Difference between two dates is "
                          + getDifference(dt1, dt2));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program two find number of
// days between two given dates

// A date has day 'd', month 'm' and year 'y'
class Date
{
    constructor(d,m,y)
    {
        this.d = d;
            this.m = m;
            this.y = y;
    }
}

// To store number of days in
    // all months from January to Dec.
let monthDays=[31, 28, 31, 30, 31, 30,
                            31, 31, 30, 31, 30, 31];
// This function counts number of
    // leap years before the given date                           
function countLeapYears(d)
{
    let years = d.y;

        // Check if the current year needs to be considered
        // for the count of leap years or not
        if (d.m <= 2)
        {
            years--;
        }

        // An year is a leap year if it is a multiple of 4,
        // multiple of 400 and not a multiple of 100.
        return Math.floor(years / 4) - Math.floor(years / 100) +
        Math.floor(years / 400);
}

// This function returns number
    // of days between two given dates
function getDifference(dt1,dt2)
{
// COUNT TOTAL NUMBER OF DAYS BEFORE FIRST DATE 'dt1'

        // initialize count using years and day
        let n1 = dt1.y * 365 + dt1.d;

        // Add days for months in given date
        for (let i = 0; i < dt1.m - 1; i++)
        {
            n1 += monthDays[i];
        }

        // Since every leap year is of 366 days,
        // Add a day for every leap year
        n1 += countLeapYears(dt1);

        // SIMILARLY, COUNT TOTAL NUMBER OF DAYS BEFORE 'dt2'
        let n2 = dt2.y * 365 + dt2.d;
        for (let i = 0; i < dt2.m - 1; i++)
        {
            n2 += monthDays[i];
        }
        n2 += countLeapYears(dt2);

        // return difference between two counts
        return (n2 - n1);
}

 // Driver code
let dt1 = new Date(1, 2, 2000);
let dt2 = new Date(1, 2, 2004);
document.write("Difference between two dates is " +
                            getDifference(dt1, dt2));

// This code is contributed by rag2127

</script>
```

**Output**

```
Difference between two dates is 1461
```

时间复杂度:0(1)

辅助空间:0(1)

**注:以上程序从时间开始遵循公历。**

本文由**阿沛·拉提**供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论