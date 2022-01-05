# 将 Unix 时间戳转换为 DD/MM/YYYY HH:MM:SS 格式

> 原文:[https://www . geesforgeks . org/convert-UNIX-timestamp-to-DD-mm-yyyy-hhmmss-format/](https://www.geeksforgeeks.org/convert-unix-timestamp-to-dd-mm-yyyy-hhmmss-format/)

给定给定时间点的 [Unix 时间戳](https://en.wikipedia.org/wiki/Unix_time) **T** (以秒为单位)，任务是将其转换为人类可读的格式(DD/MM/YYYY HH:MM:SS)

**示例:**

> **输入:** T = 1595497956
> **输出:** 23/7/2020 9:52:36
> **说明:**在 unix 时间 T 有 1595497956 秒，所以它总共有 50 年 7 个月 23 天 9 小时 52 分 36 秒。
> 
> **输入:**T = 345234235
> T3】输出: 9/12/1980 18:23:55

**进场:**

1.  [将给定的秒数除以一天中的秒数(86400)转换为天数](https://www.geeksforgeeks.org/converting-seconds-into-days-hours-minutes-and-seconds/)，并存储剩余的秒数。
2.  因为我们统计了自 1970 年 1 月 1 日以来的天数。因此，计算当前年份时要牢记闰年的概念。从 1970 年开始。如果年份是闰年，从天数中减去 366，否则减去 365。增加 1 岁。
3.  重复步骤 2，直到天数少于 365 天(不能构成一年)。
4.  在剩余天数(计算年份后的额外天数)中添加 1，因为剩余天数将为我们提供到前一天的天数，并且我们必须包括当前日期和月份计算。
5.  将月数增加 1，并继续从额外天数中减去月数(请记住，闰年 2 月将有 29 天，否则将有 28 天)。
6.  重复步骤 5，直到从额外的天数中减去一个月中的天数得到一个否定的结果。
7.  如果额外天数大于零，则按月递增 1。
8.  现在利用第一步的额外时间。
9.  用额外时间除以 3600 计算**小时**，用剩余秒除以 60 计算**分钟**，剩余秒即为**秒**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

// Unix time is in seconds and
// Humar Readable Format:
// DATE:MONTH:YEAR:HOUR:MINUTES:SECONDS,
// Start of unix time:01 Jan 1970, 00:00:00
#include <bits/stdc++.h>
using namespace std;

// Function to convert unix time to
// Human readable format
string
unixTimeToHumanReadable(long int seconds)
{

    // Save the time in Human
    // readable format
    string ans = "";

    // Number of days in month
    // in normal year
    int daysOfMonth[] = { 31, 28, 31, 30, 31, 30,
                          31, 31, 30, 31, 30, 31 };

    long int currYear, daysTillNow, extraTime,
        extraDays, index, date, month, hours,
        minutes, secondss, flag = 0;

    // Calculate total days unix time T
    daysTillNow = seconds / (24 * 60 * 60);
    extraTime = seconds % (24 * 60 * 60);
    currYear = 1970;

    // Calculating current year
    while (daysTillNow >= 365) {
        if (currYear % 400 == 0
            || (currYear % 4 == 0
                && currYear % 100 != 0)) {
            daysTillNow -= 366;
        }
        else {
            daysTillNow -= 365;
        }
        currYear += 1;
    }

    // Updating extradays because it
    // will give days till previous day
    // and we have include current day
    extraDays = daysTillNow + 1;

    if (currYear % 400 == 0
        || (currYear % 4 == 0
            && currYear % 100 != 0))
        flag = 1;

    // Calculating MONTH and DATE
    month = 0, index = 0;
    if (flag == 1) {
        while (true) {

            if (index == 1) {
                if (extraDays - 29 < 0)
                    break;
                month += 1;
                extraDays -= 29;
            }
            else {
                if (extraDays
                        - daysOfMonth[index]
                    < 0) {
                    break;
                }
                month += 1;
                extraDays -= daysOfMonth[index];
            }
            index += 1;
        }
    }
    else {
        while (true) {

            if (extraDays
                    - daysOfMonth[index]
                < 0) {
                break;
            }
            month += 1;
            extraDays -= daysOfMonth[index];
            index += 1;
        }
    }

    // Current Month
    if (extraDays > 0) {
        month += 1;
        date = extraDays;
    }
    else {
        if (month == 2 && flag == 1)
            date = 29;
        else {
            date = daysOfMonth[month - 1];
        }
    }

    // Calculating HH:MM:YYYY
    hours = extraTime / 3600;
    minutes = (extraTime % 3600) / 60;
    secondss = (extraTime % 3600) % 60;

    ans += to_string(date);
    ans += "/";
    ans += to_string(month);
    ans += "/";
    ans += to_string(currYear);
    ans += " ";
    ans += to_string(hours);
    ans += ":";
    ans += to_string(minutes);
    ans += ":";
    ans += to_string(secondss);

    // Return the time
    return ans;
}

// Driver Code
int main()
{
    // Given unix time
    long int T = 1595497956;

    // Function call to convert unix
    // time to human read able
    string ans = unixTimeToHumanReadable(T);

    // Print time in format
    // DD:MM:YYYY:HH:MM:SS
    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

// Unix time is in seconds and
// Humar Readable Format:
// DATE:MONTH:YEAR:HOUR:MINUTES:SECONDS,
// Start of unix time:01 Jan 1970, 00:00:00
import java.util.*;

class GFG{

// Function to convert unix time to
// Human readable format
static String unixTimeToHumanReadable(int seconds)
{

    // Save the time in Human
    // readable format
    String ans = "";

    // Number of days in month
    // in normal year
    int daysOfMonth[] = { 31, 28, 31, 30, 31, 30,
                          31, 31, 30, 31, 30, 31 };

    int currYear, daysTillNow, extraTime,
        extraDays, index, date, month, hours,
        minutes, secondss, flag = 0;

    // Calculate total days unix time T
    daysTillNow = seconds / (24 * 60 * 60);
    extraTime = seconds % (24 * 60 * 60);
    currYear = 1970;

    // Calculating current year
    while (daysTillNow >= 365)
    {
        if (currYear % 400 == 0 ||
           (currYear % 4 == 0 &&
            currYear % 100 != 0))
        {
            daysTillNow -= 366;
        }
        else
        {
            daysTillNow -= 365;
        }
        currYear += 1;
    }

    // Updating extradays because it
    // will give days till previous day
    // and we have include current day
    extraDays = daysTillNow + 1;

    if (currYear % 400 == 0 ||
       (currYear % 4 == 0 &&
        currYear % 100 != 0))
        flag = 1;

    // Calculating MONTH and DATE
    month = 0; index = 0;
    if (flag == 1)
    {
        while (true)
        {
            if (index == 1)
            {
                if (extraDays - 29 < 0)
                    break;

                month += 1;
                extraDays -= 29;
            }
            else
            {
                if (extraDays -
                    daysOfMonth[index] < 0)
                {
                    break;
                }
                month += 1;
                extraDays -= daysOfMonth[index];
            }
            index += 1;
        }
    }
    else
    {
        while (true)
        {
            if (extraDays - daysOfMonth[index] < 0)
            {
                break;
            }
            month += 1;
            extraDays -= daysOfMonth[index];
            index += 1;
        }
    }

    // Current Month
    if (extraDays > 0)
    {
        month += 1;
        date = extraDays;
    }
    else
    {
        if (month == 2 && flag == 1)
            date = 29;
        else
        {
            date = daysOfMonth[month - 1];
        }
    }

    // Calculating HH:MM:YYYY
    hours = extraTime / 3600;
    minutes = (extraTime % 3600) / 60;
    secondss = (extraTime % 3600) % 60;

    ans += String.valueOf(date);
    ans += "/";
    ans += String.valueOf(month);
    ans += "/";
    ans += String.valueOf(currYear);
    ans += " ";
    ans += String.valueOf(hours);
    ans += ":";
    ans += String.valueOf(minutes);
    ans += ":";
    ans += String.valueOf(secondss);

    // Return the time
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given unix time
    int T = 1595497956;

    // Function call to convert unix
    // time to human read able
    String ans = unixTimeToHumanReadable(T);

    // Print time in format
    // DD:MM:YYYY:HH:MM:SS
    System.out.print(ans + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Unix time is in seconds and
# Humar Readable Format:
# DATE:MONTH:YEAR:HOUR:MINUTES:SECONDS,
# Start of unix time:01 Jan 1970, 00:00:00

# Function to convert unix time to
# Human readable format
def unixTimeToHumanReadable(seconds):

    # Save the time in Human
    # readable format
    ans = ""

    # Number of days in month
    # in normal year
    daysOfMonth = [ 31, 28, 31, 30, 31, 30,
                    31, 31, 30, 31, 30, 31 ]

    (currYear, daysTillNow, extraTime,
     extraDays, index, date, month, hours,
     minutes, secondss, flag) = ( 0, 0, 0, 0, 0,
                                  0, 0, 0, 0, 0, 0 )

    # Calculate total days unix time T
    daysTillNow = seconds // (24 * 60 * 60)
    extraTime = seconds % (24 * 60 * 60)
    currYear = 1970

    # Calculating current year
    while (daysTillNow >= 365):
        if (currYear % 400 == 0 or
           (currYear % 4 == 0 and
            currYear % 100 != 0)):
            daysTillNow -= 366

        else:
            daysTillNow -= 365

        currYear += 1

    # Updating extradays because it
    # will give days till previous day
    # and we have include current day
    extraDays = daysTillNow + 1

    if (currYear % 400 == 0 or
       (currYear % 4 == 0 and
        currYear % 100 != 0)):
        flag = 1

    # Calculating MONTH and DATE
    month = 0
    index = 0

    if (flag == 1):
        while (True):

            if (index == 1):
                if (extraDays - 29 < 0):
                    break

                month += 1
                extraDays -= 29

            else:
                if (extraDays - daysOfMonth[index] < 0):
                    break

                month += 1
                extraDays -= daysOfMonth[index]

            index += 1

    else:
        while (True):
            if (extraDays - daysOfMonth[index] < 0):
                break

            month += 1
            extraDays -= daysOfMonth[index]
            index += 1

    # Current Month
    if (extraDays > 0):
        month += 1
        date = extraDays

    else:
        if (month == 2 and flag == 1):
            date = 29
        else:
            date = daysOfMonth[month - 1]

    # Calculating HH:MM:YYYY
    hours = extraTime // 3600
    minutes = (extraTime % 3600) // 60
    secondss = (extraTime % 3600) % 60

    ans += str(date)
    ans += "/"
    ans += str(month)
    ans += "/"
    ans += str(currYear)
    ans += " "
    ans += str(hours)
    ans += ":"
    ans += str(minutes)
    ans += ":"
    ans += str(secondss)

    # Return the time
    return ans

# Driver code   
if __name__=="__main__":

    # Given unix time
    T = 1595497956

    # Function call to convert unix
    # time to human read able
    ans = unixTimeToHumanReadable(T)

    # Print time in format
    # DD:MM:YYYY:HH:MM:SS
    print(ans)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach

// Unix time is in seconds and
// Humar Readable Format:
// DATE:MONTH:YEAR:HOUR:MINUTES:SECONDS,
// Start of unix time:01 Jan 1970, 00:00:00
using System;

class GFG{

// Function to convert unix time to
// Human readable format
static String unixTimeToHumanReadable(int seconds)
{

    // Save the time in Human
    // readable format
    String ans = "";

    // Number of days in month
    // in normal year
    int []daysOfMonth = { 31, 28, 31, 30, 31, 30,
                          31, 31, 30, 31, 30, 31 };

    int currYear, daysTillNow, extraTime,
        extraDays, index, date, month, hours,
        minutes, secondss, flag = 0;

    // Calculate total days unix time T
    daysTillNow = seconds / (24 * 60 * 60);
    extraTime = seconds % (24 * 60 * 60);
    currYear = 1970;

    // Calculating current year
    while (daysTillNow >= 365)
    {
        if (currYear % 400 == 0 ||
           (currYear % 4 == 0 &&
            currYear % 100 != 0))
        {
            daysTillNow -= 366;
        }
        else
        {
            daysTillNow -= 365;
        }
        currYear += 1;
    }

    // Updating extradays because it
    // will give days till previous day
    // and we have include current day
    extraDays = daysTillNow + 1;

    if (currYear % 400 == 0 ||
       (currYear % 4 == 0 &&
        currYear % 100 != 0))
        flag = 1;

    // Calculating MONTH and DATE
    month = 0; index = 0;
    if (flag == 1)
    {
        while (true)
        {
            if (index == 1)
            {
                if (extraDays - 29 < 0)
                    break;

                month += 1;
                extraDays -= 29;
            }
            else
            {
                if (extraDays -
                    daysOfMonth[index] < 0)
                {
                    break;
                }
                month += 1;
                extraDays -= daysOfMonth[index];
            }
            index += 1;
        }
    }
    else
    {
        while (true)
        {
            if (extraDays - daysOfMonth[index] < 0)
            {
                break;
            }
            month += 1;
            extraDays -= daysOfMonth[index];
            index += 1;
        }
    }

    // Current Month
    if (extraDays > 0)
    {
        month += 1;
        date = extraDays;
    }
    else
    {
        if (month == 2 && flag == 1)
            date = 29;
        else
        {
            date = daysOfMonth[month - 1];
        }
    }

    // Calculating HH:MM:YYYY
    hours = extraTime / 3600;
    minutes = (extraTime % 3600) / 60;
    secondss = (extraTime % 3600) % 60;

    ans += String.Join("", date);
    ans += "/";
    ans += String.Join("", month);
    ans += "/";
    ans += String.Join("", currYear);
    ans += " ";
    ans += String.Join("", hours);
    ans += ":";
    ans += String.Join("", minutes);
    ans += ":";
    ans += String.Join("", secondss);

    // Return the time
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given unix time
    int T = 1595497956;

    // Function call to convert unix
    // time to human read able
    String ans = unixTimeToHumanReadable(T);

    // Print time in format
    // DD:MM:YYYY:HH:MM:SS
    Console.Write(ans + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Unix time is in seconds and
    // Humar Readable Format:
    // DATE:MONTH:YEAR:HOUR:MINUTES:SECONDS,
    // Start of unix time:01 Jan 1970, 00:00:00

    // Function to convert unix time to
    // Human readable format
    function unixTimeToHumanReadable(seconds)
    {

        // Save the time in Human
        // readable format
        let ans = "";

        // Number of days in month
        // in normal year
        let daysOfMonth = [ 31, 28, 31, 30, 31, 30,
                              31, 31, 30, 31, 30, 31 ];

        let currYear, daysTillNow, extraTime,
            extraDays, index, date, month, hours,
            minutes, secondss, flag = 0;

        // Calculate total days unix time T
        daysTillNow = parseInt(seconds / (24 * 60 * 60), 10);
        extraTime = seconds % (24 * 60 * 60);
        currYear = 1970;

        // Calculating current year
        while (daysTillNow >= 365)
        {
            if (currYear % 400 == 0 ||
               (currYear % 4 == 0 &&
                currYear % 100 != 0))
            {
                daysTillNow -= 366;
            }
            else
            {
                daysTillNow -= 365;
            }
            currYear += 1;
        }

        // Updating extradays because it
        // will give days till previous day
        // and we have include current day
        extraDays = daysTillNow + 1;

        if (currYear % 400 == 0 ||
           (currYear % 4 == 0 &&
            currYear % 100 != 0))
            flag = 1;

        // Calculating MONTH and DATE
        month = 0; index = 0;
        if (flag == 1)
        {
            while (true)
            {
                if (index == 1)
                {
                    if (extraDays - 29 < 0)
                        break;

                    month += 1;
                    extraDays -= 29;
                }
                else
                {
                    if (extraDays -
                        daysOfMonth[index] < 0)
                    {
                        break;
                    }
                    month += 1;
                    extraDays -= daysOfMonth[index];
                }
                index += 1;
            }
        }
        else
        {
            while (true)
            {
                if (extraDays - daysOfMonth[index] < 0)
                {
                    break;
                }
                month += 1;
                extraDays -= daysOfMonth[index];
                index += 1;
            }
        }

        // Current Month
        if (extraDays > 0)
        {
            month += 1;
            date = extraDays;
        }
        else
        {
            if (month == 2 && flag == 1)
                date = 29;
            else
            {
                date = daysOfMonth[month - 1];
            }
        }

        // Calculating HH:MM:YYYY
        hours = parseInt(extraTime / 3600, 10);
        minutes = parseInt((extraTime % 3600) / 60, 10);
        secondss = parseInt((extraTime % 3600) % 60, 10);

        ans += date.toString();
        ans += "/";
        ans += month.toString();
        ans += "/";
        ans += currYear.toString();
        ans += " ";
        ans += hours.toString();
        ans += ":";
        ans += minutes.toString();
        ans += ":";
        ans += secondss.toString();

        // Return the time
        return ans;
    }

    // Given unix time
    let T = 1595497956;

    // Function call to convert unix
    // time to human read able
    let ans = unixTimeToHumanReadable(T);

    // Print time in format
    // DD:MM:YYYY:HH:MM:SS
    document.write(ans + "</br>");

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
23/7/2020 9:52:36
```