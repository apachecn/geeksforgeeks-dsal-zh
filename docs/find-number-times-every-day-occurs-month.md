# 求一个月内每天发生的次数

> 原文:[https://www . geesforgeks . org/find-number-times-every-day-occurs-month/](https://www.geeksforgeeks.org/find-number-times-every-day-occurs-month/)

给定开始日期和一个月中的天数。求一个月内每天发生的次数
例:

```
Input : Number of days in month = 28 
        First day = Wednesday 
Output : Monday = 4  
         Tuesday = 4 
         Wednesday = 4 
         Thursday = 4 
         Friday = 4 
         Saturday = 4 
         Sunday = 4
Explanation: In the month of February, 
every day occurs 4 times.  

Input : Number of days in  month = 31  
        First day = Tuesday  
Output : Monday = 4  
         Tuesday = 5 
         Wednesday = 5 
         Thursday = 5  
         Friday = 4 
         Saturday = 4 
         Sunday = 4 
Explanation: The month starts on Tuesday 
and ends on Thursday. 
```

**观察:**我们要做一些关键的观察。第一个是如果一个月有 28 天，那么每天发生 4 次。第二个是如果它有 29 天，那么这个月开始的那一天会出现 5 次。第三个是如果这个月有 30 天，那么这个月开始的那一天和第二天将发生 5 天。最后一个是如果这个月有 31 天，那么这个月开始的那一天和接下来的 2 天将发生 5 天，其余的各发生 4 次。
**方法:**创建一个计数数组，大小为 7，初始值为 4，最小出现次数为 4。**(天数-28)** 。找到第一天的索引。计算出现次数为 5 的天数。然后运行从 pos 到 pos+(天数-28)的循环，将事件标记为 5。如果 pos+(天数-28)超过 6，则使用%7 从头开始获取索引。
下面是上述方法的 C++实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count occurrence of days in a month
#include <bits/stdc++.h>
using namespace std;

// function to find occurrences
void occurrenceDays(int n, string firstday)
{
    // stores days in a week
    string days[] = { "Monday", "Tuesday", "Wednesday",
           "Thursday",  "Friday", "Saturday", "Sunday" };

    // Initialize all counts as 4.
    int count[7];
    for (int i = 0; i < 7; i++)
        count[i] = 4;

    // find index of the first day
    int pos;
    for (int i = 0; i < 7; i++) {
        if (firstday == days[i]) {
            pos = i;
            break;
        }
    }

    // number of days whose occurrence will be 5
    int inc = n - 28;

    // mark the occurrence to be 5 of n-28 days
    for (int i = pos; i < pos + inc; i++) {
        if (i > 6)
            count[i % 7] = 5;
        else
            count[i] = 5;
    }

    // print the days
    for (int i = 0; i < 7; i++) {
        cout << days[i] << " " << count[i] << endl;
    }
}

// driver program to test the above function
int main()
{
    int n = 31;
    string firstday = "Tuesday";
    occurrenceDays(n, firstday);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// occurrence of days in a month
import java.util.*;
import java.lang.*;

public class GfG{

    // function to find occurrences
    public static void occurrenceDays(int n, String firstday)
    {
        // stores days in a week
        String[] days = new String[]{ "Monday",
                "Tuesday", "Wednesday",
                "Thursday", "Friday",
                "Saturday", "Sunday" };

        // Initialize all counts as 4.
        int[] count = new int[7];
        for (int i = 0; i < 7; i++)
            count[i] = 4;

        // find index of the first day
        int pos = 0;
        for (int i = 0; i < 7; i++)
        {
            if (firstday == days[i])
            {
                pos = i;
                break;
            }
        }

        // number of days whose occurrence
        // will be 5
        int inc = n - 28;

        // mark the occurrence to be 5 of n-28 days
        for (int i = pos; i < pos + inc; i++)
        {
            if (i > 6)
                count[i % 7] = 5;
            else
                count[i] = 5;
        }

        // print the days
        for (int i = 0; i < 7; i++)
        {
            System.out.println(days[i] + " " + count[i]);
        }
    }

    // Driver function
    public static void main(String argc[]){
        int n = 31;
        String firstday = "Tuesday";
        occurrenceDays(n, firstday);
    }
}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
# Python program to count
# occurrence of days in a month
import math

# function to find occurrences
def occurrenceDays( n, firstday):

    # stores days in a week
    days = [ "Monday", "Tuesday", "Wednesday",
           "Thursday",  "Friday", "Saturday",
           "Sunday" ]

    # Initialize all counts as 4.
    count= [4 for i in range(0,7)]

    # find index of the first day
    pos=-1
    for i in range(0,7):
        if (firstday == days[i]):
            pos = i
            break

    # number of days whose occurrence will be 5
    inc = n - 28

    # mark the occurrence to be 5 of n-28 days
    for  i in range( pos, pos + inc):
        if (i > 6):
            count[i % 7] = 5
        else:
            count[i] = 5

    # print the days
    for i in range(0,7):
        print (days[i] , " " , count[i])

# driver program to test
# the above function
n = 31
firstday = "Tuesday"
occurrenceDays(n, firstday)

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to count occurrence of
// days in a month
using System;

public class GfG {

    // function to find occurrences
    public static void occurrenceDays(int n,
                              string firstday)
    {

        // stores days in a week
        String[] days = new String[]{ "Monday",
                        "Tuesday", "Wednesday",
                          "Thursday", "Friday",
                        "Saturday", "Sunday" };

        // Initialize all counts as 4.
        int[] count = new int[7];

        for (int i = 0; i < 7; i++)
            count[i] = 4;

        // find index of the first day
        int pos = 0;
        for (int i = 0; i < 7; i++)
        {
            if (firstday == days[i])
            {
                pos = i;
                break;
            }
        }

        // number of days whose occurrence
        // will be 5
        int inc = n - 28;

        // mark the occurrence to be 5 of
        // n-28 days
        for (int i = pos; i < pos + inc; i++)
        {
            if (i > 6)
                count[i % 7] = 5;
            else
                count[i] = 5;
        }

        // print the days
        for (int i = 0; i < 7; i++)
        {
            Console.WriteLine(days[i] + " "
                                    + count[i]);
        }
    }

    // Driver function
    public static void Main()
    {
        int n = 31;
        string firstday = "Tuesday";

        occurrenceDays(n, firstday);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to count
// occurrence of days in a month

    // function to find occurrences
    function occurrenceDays(n, firstday)
    {
        // stores days in a week
        let days = [ "Monday",
                "Tuesday", "Wednesday",
                "Thursday", "Friday",
                "Saturday", "Sunday" ];

        // Initialize all counts as 4.
        let count = [];
        for (let i = 0; i < 7; i++)
            count[i] = 4;

        // find index of the first day
        let pos = 0;
        for (let i = 0; i < 7; i++)
        {
            if (firstday == days[i])
            {
                pos = i;
                break;
            }
        }

        // number of days whose occurrence
        // will be 5
        let inc = n - 28;

        // mark the occurrence to be 5 of n-28 days
        for (let i = pos; i < pos + inc; i++)
        {
            if (i > 6)
                count[i % 7] = 5;
            else
                count[i] = 5;
        }

        // print the days
        for (let i = 0; i < 7; i++)
        {
            document.write(days[i] + " " + count[i] + "<br/>");
        }
    }

// Driver code

        let n = 31;
        let firstday = "Tuesday";
        occurrenceDays(n, firstday);

</script>
```

**输出:**

```
Monday 4
Tuesday 5
Wednesday 5
Thursday 5
Friday 4
Saturday 4
Sunday 4
```