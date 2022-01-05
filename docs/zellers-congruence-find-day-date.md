# 泽勒同余|寻找约会的日子

> 原文:[https://www . geesforgeks . org/zellers-同余-find-day-date/](https://www.geeksforgeeks.org/zellers-congruence-find-day-date/)

泽勒同余是克里斯蒂安·泽勒设计的一种算法，用于计算任何儒略历或公历日期的星期几。它可以被认为是基于儒略日和日历日期之间的转换。
这是一种为任何日期查找星期几的算法。
**对于公历它是:**
![h=\left ( q + [ \frac{13(m+1)}{5} ]+K +\left [ \frac{K}{4}\right ]+\left [ \frac{J}{4}\right ]+5J\right )mod7    ](img/f81bd26dbb8375f81848a6253058c976.png "Rendered by QuickLaTeX.com")
**对于儒略历它是:**
![h=\left ( q + \left [ \frac{13(m+1)}{5} \right ]+K +\left [ \frac{K}{4}\right ]+5-J\right )mod7    ](img/75e0814687a28d6c56df060bdd610b45.png "Rendered by QuickLaTeX.com")
在哪里，

1.  h 是一周中的某一天(0 =周六，1 =周日，2 =周一，…，6 =周五)
2.  q 是一个月中的哪一天
3.  m 是月份(3 = 3 月，4 = 4 月，5 = 5 月，…，14 = 2 月)
4.  k 是世纪之交(100 年)。
5.  j 是从零开始的世纪(实际上是⌊年/100 ⌋)例如，1995 年和 2000 年的从零开始的世纪分别是 19 世纪和 20 世纪(为了不与常见的序数世纪计数混淆，序数世纪计数在两种情况下都表示 20 世纪)。

```
NOTE: In this algorithm January and February are
      counted as months 13 and 14 of the previous
      year.E.g. if it is 2 February 2010, the 
      algorithm counts the date as the second day 
      of the fourteenth month of 2009 (02/14/2009 
      in DD/MM/YYYY format)
```

对于国际标准化组织周日期周日(1 =周一至 7 =周日)，使用

```
 d = ((h+5)%7) + 1 
```

## C++

```
// C++ program to find Find the Day
// for a Date
#include <cmath>
#include <cstring>
#include <iostream>
using namespace std;

int Zellercongruence(int day, int month, int year)
{
    if (month == 1) {
        month = 13;
        year--;
    }
    if (month == 2) {
        month = 14;
        year--;
    }
    int q = day;
    int m = month;
    int k = year % 100;
    int j = year / 100;
    int h
        = q + 13 * (m + 1) / 5 + k + k / 4 +
                              j / 4 + 5 * j;
    h = h % 7;
    switch (h) {
    case 0:
        cout << "Saturday \n";
        break;
    case 1:
        cout << "Sunday \n";
        break;
    case 2:
        cout << "Monday \n";
        break;
    case 3:
        cout << "Tuesday \n";
        break;
    case 4:
        cout << "Wednesday \n";
        break;
    case 5:
        cout << "Thursday \n";
        break;
    case 6:
        cout << "Friday \n";
        break;
    }
    return 0;
}

// Driver code
int main()
{
    Zellercongruence(22, 10, 2017); // date (dd/mm/yyyy)
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Find the Day
// for a Date
import java.util.*;

class GFG
{
    // Print Day for a Date
    static void Zellercongruence(int day, int month,
                                 int year)
    {
        if (month == 1)
        {
            month = 13;
            year--;
        }
        if (month == 2)
        {
            month = 14;
            year--;
        }
        int q = day;
        int m = month;
        int k = year % 100;
        int j = year / 100;
        int h = q + 13*(m + 1) / 5 + k + k / 4 + j / 4 + 5 * j;
        h = h % 7;
        switch (h)
        {
            case 0 : System.out.println("Saturday"); break;
            case 1 : System.out.println("Sunday"); break;
            case 2 : System.out.println("Monday"); break;
            case 3 : System.out.println("Tuesday"); break;
            case 4 : System.out.println("Wednesday"); break;
            case 5 : System.out.println("Thursday"); break;
            case 6 : System.out.println("Friday"); break;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        Zellercongruence(22, 10, 2017); //date (dd/mm/yyyy)
    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python3 program to find Find the Day
# for a Date

def switch(h) :
    return {
        0 : "Saturday",
        1 : "Sunday",
        2 : "Monday",
        3 : "Tuesday",
        4 : "Wednesday",
        5 : "Thursday",
        6 : "Friday",
    }[h]

def Zellercongruence(day, month, year) :
    if (month == 1) :
        month = 13
        year = year - 1

    if (month == 2) :
        month = 14
        year = year - 1
    q = day
    m = month
    k = year % 100;
    j = year // 100;
    h = q + 13 * (m + 1) // 5 + k + k // 4 + j // 4 + 5 * j
    h = h % 7
    print(switch (h))

# Driver code
Zellercongruence(22, 10, 2017) #date (dd/mm/yyyy)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to find Find the Day
// for a Date
using System;

class GFG {

    // Print Day for a Date
    static void Zellercongruence(int day,
                      int month, int year)
    {
        if (month == 1)
        {
            month = 13;
            year--;
        }
        if (month == 2)
        {
            month = 14;
            year--;
        }
        int q = day;
        int m = month;
        int k = year % 100;
        int j = year / 100;
        int h = q + 13 * (m + 1) / 5 + k + k / 4
                                 + j / 4 + 5 * j;
        h = h % 7;
        switch (h)
        {
            case 0 : Console.WriteLine("Saturday");
                     break;

            case 1 : Console.WriteLine("Sunday");
                     break;

            case 2 : Console.WriteLine("Monday");
                     break;

            case 3 : Console.WriteLine("Tuesday");
                     break;

            case 4 : Console.WriteLine("Wednesday");
                     break;

            case 5 : Console.WriteLine("Thursday");
                     break;

            case 6 : Console.WriteLine("Friday");
                     break;
        }
    }

    // Driver code
    public static void Main()
    {

        //date (dd/mm/yyyy)
        Zellercongruence(22, 10, 2017);
    }
}

/* This code is contributed by vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Find the Day
// for a Date

function Zellercongruence($day, $month, $year)
{
    if ($month == 1)
    {
        $month = 13;
        $year--;
    }

    if ($month == 2)
    {
        $month = 14;
        $year--;
    }

        $q = $day;
        $m = $month;
        $k = $year % 100;
        $j = $year / 100;
        $h = $q + 13*($m + 1) / 5 + $k +
               $k / 4 + $j / 4 + 5 * $j;
        $h = $h % 7;
    switch ($h)
    {
        case 1 : echo "Saturday \n";
        break;
        case 2 : echo "Sunday \n";
        break;
        case 3 : echo "Monday \n";
        break;
        case 4 : echo "Tuesday \n";
        break;
        case 5 : echo "Wednesday \n";
        break;
        case 6 : echo "Thursday \n";
        break;
        case 7 : echo "Friday \n";
        break;
    }
}

// Driver code
//date (dd/mm/yyyy)
Zellercongruence(22, 10, 2017);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find Find the Day for a Date

    // Print Day for a Date
    function Zellercongruence(day, month, year)
    {
        if (month == 1)
        {
            month = 13;
            year--;
        }
        if (month == 2)
        {
            month = 14;
            year--;
        }
        let q = day;
        let m = month;
        let k = year % 100;
        let j = parseInt(year / 100, 10);
        let h = q + parseInt(13 * (m + 1) / 5, 10) + k + parseInt(k / 4, 10) + parseInt(j / 4, 10) + 5 * j;
        h = h % 7;
        switch (h)
        {
            case 0 :
              document.write("Saturday");
              break;

            case 1 :
                document.write("Sunday");
                break;

            case 2 :
                document.write("Monday");
                break;

            case 3 :
                document.write("Tuesday");
                break;

            case 4 :
                document.write("Wednesday");
                break;

            case 5 :
                document.write("Thursday");
                break;

            case 6 :
                document.write("Friday");
                break;
        }
    }

    //date (dd/mm/yyyy)
      Zellercongruence(22, 10, 2017);

</script>
```

**输出:**

```
Sunday
```

本文由 **Amartya Ranjan Saikia** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。