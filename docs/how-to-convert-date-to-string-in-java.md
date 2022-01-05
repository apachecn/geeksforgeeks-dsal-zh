# 如何在 Java 中将日期转换为字符串

> 原文:[https://www . geesforgeks . org/如何将日期转换为 java 字符串/](https://www.geeksforgeeks.org/how-to-convert-date-to-string-in-java/)

给定一个日期，任务是编写一个 Java 程序，将给定的日期转换成字符串。

**示例:**

> **输入:**日期=【2020-07-27】
> T3】输出: 2020-07-27
> 
> **输入:**日期=【2018-02-17】
> T3】输出: 2018-02-17

#### **方法一:使用 [DateFormat.format()方法](https://www.geeksforgeeks.org/dateformat-format-method-in-java-with-examples/)T3】**

**进场:**

1.  获取要转换的日期。
2.  创建一个*简单日期格式* *类*的实例来格式化日期对象的字符串表示。
3.  使用*日历对象*获取日期。
4.  使用*格式()方法*将给定日期转换为字符串。
5.  打印结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert Date to String

import java.util.Calendar;
import java.util.Date;
import java.text.DateFormat;
import java.text.SimpleDateFormat;

class GFG {

    // Function to convert date to string
    public static String
    convertDateToString(String date)
    {
        // Converts the string
        // format to date object
        DateFormat df = new SimpleDateFormat(date);

        // Get the date using calendar object
        Date today = Calendar.getInstance()
                         .getTime();

        // Convert the date into a
        // string using format() method
        String dateToString = df.format(today);

        // Return the result
        return (dateToString);
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given Date
        String date = "07-27-2020";

        // Convert and print the result
        System.out.print(
            convertDateToString(date));
    }
}
```

**Output:**

```
07-27-2020

```

#### **方法二:使用 [LocalDate.toString()方法](https://www.geeksforgeeks.org/localdate-tostring-method-in-java-with-examples/)T3】**

**进场:**

1.  从*日期*获取*本地日期*的实例。
2.  使用*本地日期类*的 *toString()方法*将给定日期转换为字符串。
3.  打印结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert Date to String

import java.time.LocalDate;

class GFG {

    // Function to convert date to string
    public static String
    convertDateToString(String date)
    {

        // Get an instance of LocalTime
        // from date
        LocalDate givenDate = LocalDate.parse(date);

        // Convert the given date into a
        // string using toString()method
        String dateToString
            = givenDate.toString();

        // Return the result
        return (dateToString);
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given Date
        String date = "2020-07-27";

        // Convert and print the result
        System.out.print(
            convertDateToString(date));
    }
}
```

**Output:**

```
2020-07-27

```