# 如何在 Java 中从日期中获取日、月、年

> 原文:[https://www . geesforgeks . org/如何获取 java 中的日-月-年-日期/](https://www.geeksforgeeks.org/how-to-get-day-month-and-year-from-date-in-java/)

给定一个字符串形式的日期，任务是*编写一个* [*Java 程序*](https://www.geeksforgeeks.org/java/) *来获取给定日期的日、月、年*。

**示例:**

> **输入:**日期=“2020-07-18”
> **输出:**
> 日:18
> 月:7 月
> 年:2020
> **说明:**给定日期为‘2020-07-18’，所以日为:18，月为:7 月，年为:2020。
> 
> **输入:**日期=“2018-05-10”
> **输出:**
> 日:10
> 月:5 月
> 年:2018
> **说明:**给定日期为‘2018-05-10’，所以日为:10，月为:5 月，年为:2018。

**方法一:在 Java** 中使用 [**LocalDate 类:**](https://www.geeksforgeeks.org/localdate-format-method-in-java/)

*   其思想是利用*****类*的方法从日期中获取日、月、年。****
*   *******getDayOfMonth()*** 方法返回给定日期代表的日期，*T5】getMonth()*方法返回给定日期代表的月份，*T9】getYear()*方法返回给定日期代表的年份。****

****下面是上述方法的实现:****

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.Date;
import java.time.Month;
import java.time.LocalDate;

class GFG {

    // Function to get day, month, and
    // year from date
    public static void
    getDayMonthYear(String date)
    {

        // Get an instance of LocalTime
        // from date
        LocalDate currentDate
            = LocalDate.parse(date);

        // Get day from date
        int day = currentDate.getDayOfMonth();

        // Get month from date
        Month month = currentDate.getMonth();

        // Get year from date
        int year = currentDate.getYear();

        // Print the day, month, and year
        System.out.println("Day: " + day);
        System.out.println("Month: " + month);
        System.out.println("Year: " + year);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given Date
        String date = "2020-07-18";

        // Function Call
        getDayMonthYear(date);
    }
}**
```

******Output:** 

```
Day: 18
Month: JULY
Year: 2020
```**** 

******方法二:在 Java 中使用** [**日历类**](https://www.geeksforgeeks.org/calendar-class-in-java-with-examples/) :****

*   ****其思路是用*历类*的 [*get()*](https://www.geeksforgeeks.org/calendar-get-method-in-java/) 方法从日期中获取日、月、年。****
*   *******get()*** 方法取*整数* *类型*的一个参数，从给定日期返回传递字段的值。****
*   ****它返回月份索引，而不是月份名称。****

****下面是上述方法的实现:****

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG {

    // Driver Code
    public static void main(String args[])
    {
        // Creating a calendar object
        Calendar cal
            = new GregorianCalendar(
                2020, 07, 18);

        // Getting the values of day,
        // month, and year from calendar
        // object
        int day = cal.get(Calendar.DAY_OF_MONTH);
        int month = cal.get(Calendar.MONTH);
        int year = cal.get(Calendar.YEAR);

        // Printing the day, month, and year
        System.out.println("Day: " + day);
        System.out.println("Month: " + month);
        System.out.println("Year: " + year);
    }
}**
```

******Output:** 

```
Day: 18
Month: 7
Year: 2020
```**** 

******方法三:使用**Java 中的[**string . split()**](https://www.geeksforgeeks.org/split-string-java-examples/):****

1.  ****想法是用*弦类*的[分裂()](https://www.geeksforgeeks.org/split-string-java-examples/)法。****
2.  ****它根据提供的模式拆分字符串，并返回字符串数组。****

****下面是上述方法的实现:****

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
class GFG {

    // Function to get day, month, and
    // year from date
    public static void findDate(String date)
    {
        // Splitting the given date by '-'
        String dateParts[] = date.split("-");

        // Getting day, month, and year
        // from date
        String day = dateParts[0];
        String month = dateParts[1];
        String year = dateParts[2];

        // Printing the day, month, and year
        System.out.println("Day: " + day);
        System.out.println("Month: " + month);
        System.out.println("Year: " + year);
    }

    // Driver Code
    public static void
    main(String args[])
    {
        // Given date
        String date = "18-07-2020";

        findDate(date);
    }
}**
```

******Output:** 

```
Day: 18
Month: 07
Year: 2020
```****