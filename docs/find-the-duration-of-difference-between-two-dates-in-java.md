# 在 Java 中找到两个日期差的持续时间

> 原文:[https://www . geesforgeks . org/find-Java 中两个日期之间的差异持续时间/](https://www.geeksforgeeks.org/find-the-duration-of-difference-between-two-dates-in-java/)

给定两个日期**开始 _ 日期**和**结束 _ 日期**，时间以字符串形式表示，任务是在 [Java](https://www.geeksforgeeks.org/java/) 中找出两个日期之间的差异。

**示例:**

> **输入:**start _ date =“10-01-2018 01:10:20”，end _ date =“10-06-2020 06:30:50”
> **输出:** 2 年 152 天 5 小时 20 分 30 秒
> 
> **输入:**start _ date =“10-01-2019 01:00:00”，end _ date =“10-06-2020 06:00:00”
> T3】输出: 1 年 152 天 5 小时 0 分 0 秒

**方法一:**使用 [SimpleDateFormat](https://www.geeksforgeeks.org/java-simpledateformat-set-1/) 和 [Date](https://www.geeksforgeeks.org/date-class-java-examples/) 类查找两个日期的区别。以下是步骤:

1.  创建一个简单日期格式类的对象，并将字符串格式转换为日期对象。
2.  从一个字符串中解析 start_date 和 end_date 来产生日期，这可以通过使用 simpleDateFormat 类的 [parse()](https://www.geeksforgeeks.org/simpledateformat-parse-method-in-java-with-examples/) 方法来完成。
3.  使用 Java 中的方法 [getTime()作为**D2 . getTime()–D1 . getTime()**，以毫秒为单位求出两个日期之间的时间差。](https://www.geeksforgeeks.org/date-gettime-method-in-java-with-examples/)
4.  使用日期-时间数学公式找出两个日期之间的差异。它返回两个指定日期之间的年、日、小时、分钟和秒。
5.  打印最终结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

class GFG {

    // Function to print difference in
    // time start_date and end_date
    static void
    findDifference(String start_date,
                   String end_date)
    {

        // SimpleDateFormat converts the
        // string format to date object
        SimpleDateFormat sdf
            = new SimpleDateFormat(
                "dd-MM-yyyy HH:mm:ss");

        // Try Block
        try {

            // parse method is used to parse
            // the text from a string to
            // produce the date
            Date d1 = sdf.parse(start_date);
            Date d2 = sdf.parse(end_date);

            // Calucalte time difference
            // in milliseconds
            long difference_In_Time
                = d2.getTime() - d1.getTime();

            // Calucalte time difference in
            // seconds, minutes, hours, years,
            // and days
            long difference_In_Seconds
                = (difference_In_Time
                   / 1000)
                  % 60;

            long difference_In_Minutes
                = (difference_In_Time
                   / (1000 * 60))
                  % 60;

            long difference_In_Hours
                = (difference_In_Time
                   / (1000 * 60 * 60))
                  % 24;

            long difference_In_Years
                = (difference_In_Time
                   / (1000l * 60 * 60 * 24 * 365));

            long difference_In_Days
                = (difference_In_Time
                   / (1000 * 60 * 60 * 24))
                  % 365;

            // Print the date difference in
            // years, in days, in hours, in
            // minutes, and in seconds

            System.out.print(
                "Difference "
                + "between two dates is: ");

            System.out.println(
                difference_In_Years
                + " years, "
                + difference_In_Days
                + " days, "
                + difference_In_Hours
                + " hours, "
                + difference_In_Minutes
                + " minutes, "
                + difference_In_Seconds
                + " seconds");
        }

        // Catch the Exception
        catch (ParseException e) {
            e.printStackTrace();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given start Date
        String start_date
            = "10-01-2018 01:10:20";

        // Given end Date
        String end_date
            = "10-06-2020 06:30:50";

        // Function Call
        findDifference(start_date, end_date);
    }
}
```

**Output:**

> 两个日期的差别是:2 年 152 天 5 小时 20 分 30 秒

**方法二:**利用 Java 内置的[类 TimeUnit](https://www.geeksforgeeks.org/tag/java-timeunit/) ，我们可以更好的找到两个日期的差异。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// difference between two dates

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.concurrent.TimeUnit;
import java.util.Date;

class GFG {

    // Function to print difference in
    // time start_date and end_date
    static void findDifference(String start_date,
                               String end_date)
    {
        // SimpleDateFormat converts the
        // string format to date object
        SimpleDateFormat sdf
            = new SimpleDateFormat(
                "dd-MM-yyyy HH:mm:ss");

        // Try Class
        try {

            // parse method is used to parse
            // the text from a string to
            // produce the date
            Date d1 = sdf.parse(start_date);
            Date d2 = sdf.parse(end_date);

            // Calucalte time difference
            // in milliseconds
            long difference_In_Time
                = d2.getTime() - d1.getTime();

            // Calucalte time difference in seconds,
            // minutes, hours, years, and days
            long difference_In_Seconds
                = TimeUnit.MILLISECONDS
                      .toSeconds(difference_In_Time)
                  % 60;

            long difference_In_Minutes
                = TimeUnit
                      .MILLISECONDS
                      .toMinutes(difference_In_Time)
                  % 60;

            long difference_In_Hours
                = TimeUnit
                      .MILLISECONDS
                      .toHours(difference_In_Time)
                  % 24;

            long difference_In_Days
                = TimeUnit
                      .MILLISECONDS
                      .toDays(difference_In_Time)
                  % 365;

            long difference_In_Years
                = TimeUnit
                      .MILLISECONDS
                      .toDays(difference_In_Time)
                  / 365l;

            // Print the date difference in
            // years, in days, in hours, in
            // minutes, and in seconds
            System.out.print(
                "Difference"
                + " between two dates is: ");

            // Print result
            System.out.println(
                difference_In_Years
                + " years, "
                + difference_In_Days
                + " days, "
                + difference_In_Hours
                + " hours, "
                + difference_In_Minutes
                + " minutes, "
                + difference_In_Seconds
                + " seconds");
        }
        catch (ParseException e) {
            e.printStackTrace();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given start_date
        String start_date
            = "10-01-2018 01:10:20";

        // Given end_date
        String end_date
            = "10-06-2020 06:30:50";

        // Function Call
        findDifference(start_date,
                       end_date);
    }
}
```

**Output:**

> 两个日期的差别是:2 年 152 天 5 小时 20 分 30 秒

**方法三:**用 Java 中的[周期类](https://www.geeksforgeeks.org/tag/java-period/)找到两天的区别。 [Period.between()](https://www.geeksforgeeks.org/period-between-method-in-java-with-examples/) 方法用于计算年、月和日这两个日期之间的差异。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.time.*;
import java.util.*;

class GFG {

    // Function to print difference in
    // time start_date and end_date
    static void
    findDifference(LocalDate start_date,
                   LocalDate end_date)
    {

        // find the period between
        // the start and end date
        Period diff
            = Period
                  .between(start_date,
                           end_date);

        // Print the date difference
        // in years, months, and days
        System.out.print(
            "Difference "
            + "between two dates is: ");

        // Print the result
        System.out.printf(
            "%d years, %d months"
                + " and %d days ",
            diff.getYears(),
            diff.getMonths(),
            diff.getDays());
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Start date
        LocalDate start_date
            = LocalDate.of(2018, 01, 10);

        // End date
        LocalDate end_date
            = LocalDate.of(2020, 06, 10);

        // Function Call
        findDifference(start_date,
                       end_date);
    }
}
```

**Output:**

> 两个日期之间的差异是:2 年 5 个月零天