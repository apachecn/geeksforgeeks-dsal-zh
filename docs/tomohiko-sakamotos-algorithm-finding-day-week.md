# 坂本智子的算法——寻找一周中的某一天

> 原文:[https://www . geesforgeks . org/tomo hiko-saka motos-算法-查找-日-周/](https://www.geeksforgeeks.org/tomohiko-sakamotos-algorithm-finding-day-week/)

根据公历给定任何日期，任务是返回该特定日期的日期(星期一、星期二等)。
示例:

```
Input :  Date: 13 July 2017 [13.07.2017]
Output : 4 i.e Thursday

Input : Date: 15 August 2012 [15.08.2012]
Output : 3 i.e Wednesday

Input : Date: 24 December 2456 [24.12.2456]
Output : 0 i.e Sunday
```

虽然有很多方法可以解决这个问题，但是最不为人知也是最强大的方法之一是**坂本智子的算法**。
**解说**
公元 1 月 1 日是公历的一个星期一。
让我们考虑第一种情况，我们没有闰年，因此每年的总天数是 365 天。1 月有 31 天，即 7*4+3 天，因此 2 月 1 日总是比 1 月 1 日提前 3 天。现在 2 月有 28 天(不包括闰年)，正好是 7 的倍数(7*4=28)，因此 3 月没有变化，也比当年 1 月 1 日提前 3 天。考虑到这种模式，如果我们为每个月创建一个前导天数数组，那么它将给出为 t[] = {0，3，3，6，1，4，6，2，5，0，3，5}。
现在我们来看看有闰年的真实案例。每 4 年，我们的计算会多一天。除非每 100 年一次。除非每 400 年一次。我们如何投入这些额外的时间？嗯，只要加上 y/4–y/100+y/400。注意，所有除法都是整数除法。这正好增加了所需的闰日数。但是这里有一个问题，闰日是 2 月 29 日而不是 1 月 0 日。这意味着当前年份不应计入前两个月的闰日计算。假设如果月份是一月或二月，我们从年中减去 1。这意味着在这几个月中，y/4 值将是前一年的值，不会被计算在内。如果我们从 2 月以后每个月的 t[]值中减去 1？这将填补空白，闰年问题就解决了。也就是说，我们需要做如下改动:
1.t[]现在变成{0，3，2，5，0，3，5，1，4，6，2，4}。
2 .如果 m 对应 1 月/2 月(即月< 3)，我们将 y 减 1。
3 .模量内的年增量现在是 y+y/4–y/100+y/400，而不是 y。

下面是这个算法的实现:

## C++

```
// A CPP program to implement
// the Tomohiko Sakamoto Algorithm
#include <bits/stdc++.h>
using namespace std;

// function to implement tomohiko
// sakamoto algorithm
int day_of_the_week(int y, int m, int d)
{
    // array with leading number of days values
    int t[] = { 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 };

    // if month is less than 3 reduce year by 1
    if (m < 3)
        y -= 1;

    return ((y + y / 4 - y / 100 + y / 400 + t[m - 1] + d) % 7);
}

// Driver Code
int main(void)
{
    int day = 13, month = 7, year = 2017;
    cout<<(day_of_the_week(year, month, day));
    return 0 ;
}

// This code is contributed by Nikita Tiwari.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A java program to implement
// the Tomohiko Sakamoto Algorithm

class tomohiko_sakamoto
{
    // function to implement tomohiko sakamoto algorithm
    public static int day_of_the_week(int y, int m, int d)
    {
        // array with leading number of days values
        int t[] = { 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 };

        // if month is less than 3 reduce year by 1
        if (m < 3)
            y -= 1;

        return (y + y / 4 - y / 100 + y / 400 + t[m - 1] + d) % 7;
    }
    // Driver Code
    public static void main(String args[])
    {
        int day = 13, month = 7, year = 2017;
        System.out.println(day_of_the_week(year, month, day));
    }
}
```

## 蟒蛇 3

```
# A Python 3 program to implement
# the Tomohiko Sakamoto Algorithm

# function to implement tomohiko
# sakamoto algorithm
def day_of_the_week(y,  m, d) :

    # array with leading number of days values
    t = [ 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 ]

    # if month is less than 3 reduce year by 1
    if (m < 3) :
        y = y - 1

    return (y + y // 4 - y // 100 + y // 400 + t[m - 1] + d) % 7

# Driver Code
day = 13
month = 7
year = 2017

print(day_of_the_week(year, month, day))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A C# program to implement
// the Tomohiko Sakamoto Algorithm
using System;

class GFG {

    // function to implement tomohiko
    // sakamoto algorithm
    public static int day_of_the_week(int y,
                                 int m, int d)
    {

        // array with leading number of days
        // values
        int []t = { 0, 3, 2, 5, 0, 3, 5, 1,
                                4, 6, 2, 4 };

        // if month is less than 3 reduce
        // year by 1
        if (m < 3)
            y -= 1;

        return (y + y / 4 - y / 100 + y / 400
                          + t[m - 1] + d) % 7;
    }

    // Driver Code
    public static void Main()
    {
        int day = 13, month = 7, year = 2017;

        Console.WriteLine(day_of_the_week(year,
                                   month, day));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the Tomohiko Sakamoto Algorithm

// function to implement tomohiko
// sakamoto algorithm
function day_of_the_week($y, $m, $d)
{

    // array with leading number
    // of days values
    $t = array(0, 3, 2, 5, 0, 3,
               5, 1, 4, 6, 2, 4);

    // if month is less than
    // 3 reduce year by 1
    if ($m < 3)
        $y -= 1;

    return (($y + $y / 4 - $y / 100 + $y /
             400 + $t[$m - 1] + $d) % 7);
}

    // Driver Code
    $day = 13;
    $month = 7;
    $year = 2017;
    echo day_of_the_week($year, $month, $day);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript  program to implement
// the Tomohiko Sakamoto Algorithm

// function to implement tomohiko sakamoto algorithm
    function day_of_the_week(y, m, d)
    {
        // array with leading number of days values
        let t = [ 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 ];

        // if month is less than 3 reduce year by 1
        if (m < 3)
            y -= 1;

        return (y + y / 4 - y / 100 + y / 400 + t[m - 1] + d) % 7;
    }

// Driver code

        let  day = 13, month = 7, year = 2017;
         document.write(Math.round(day_of_the_week(year, month, day)));

</script>
```

**输出:**

```
 4 
```