# 使用自定义比较器

以升序对日期数组进行排序

> 原文:[https://www . geesforgeks . org/sort-按升序排列日期-使用自定义比较器/](https://www.geeksforgeeks.org/sort-an-array-of-dates-in-ascending-order-using-custom-comparator/)

给定一个“日-月-年”形式的 **N** 日期的数组 **arr[]** ，任务是按升序对这些日期进行排序。

**示例:**

> **输入:**arr[]= {“25-08-1996”、“03-08-1970”、“09-04-1994”}
> **输出:**
> 03-08-1970
> 09-04-1994
> 25-08-1996
> 
> **输入:**arr[]= {“03-08-1970”、“09-04-2020”、“19-04-2019”}
> **输出:**
> 03-08-1970
> 19-04-2019
> 09-04-2020

**进场:**

*   创建一个自定义比较器函数，如下比较两个日期:
    *   首先比较这两个元素的年份。年份较大的元素将排在另一个元素之后。
    *   如果两个日期的年份相同，则比较月份。月份较大的元素将在另一个元素之后。
    *   如果两个日期的月份相同，则比较日期。日期较大的元素将在另一个元素之后。
*   然后使用定义的自定义比较器对数组进行排序。在 C++中，它是这样完成的:

> [排序(初始位置、结束位置、比较器)](https://www.geeksforgeeks.org/sort-c-stl/)

*   打印修改后的数组。

下面是上述方法的实现:

## C++

```
// C++ implementation to sort the
// array of dates in the form of
// "DD-MM-YYYY" using custom comparator

#include <bits/stdc++.h>
using namespace std;

// Comparator to sort the array of dates
int myCompare(string date1,
              string date2)
{
    string day1 = date1.substr(0, 2);
    string month1 = date1.substr(3, 2);
    string year1 = date1.substr(6, 4);

    string day2 = date2.substr(0, 2);
    string month2 = date2.substr(3, 2);
    string year2 = date2.substr(6, 4);

    // Condition to check the year
    if (year1 < year2)
        return 1;
    if (year1 > year2)
        return 0;

    // Condition to check the month
    if (month1 < month2)
        return 1;
    if (month1 > month2)
        return 0;

    // Condition to check the day
    if (day1 < day2)
        return 1;
    if (day1 > day2)
        return 0;
}

// Function that prints the
// dates in ascensding order
void printDatesAscending(
    vector<string> arr)
{
    // Sort the dates using library
    // sort function with custom Comparator
    sort(arr.begin(), arr.end(), myCompare);

    // Loop to print the dates
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << "\n";
}

// Driver Code
int main()
{
    vector<string> arr;
    arr.push_back("25-08-1996");
    arr.push_back("03-08-1970");
    arr.push_back("09-04-1994");
    arr.push_back("29-08-1996");
    arr.push_back("14-02-1972");

    printDatesAscending(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the
// array of dates in the form of
// "DD-MM-YYYY" using custom comparator
import java.util.*;
import java.lang.*;

class GFG{

// Function that prints the
// dates in ascensding order
static void printDatesAscending(ArrayList<String> arr)
{

    // Sort the dates using library
    // sort function with custom Comparator
    Collections.sort(arr,new Comparator<>()
    {
        public int compare(String date1, String date2)
        {
            String day1 = date1.substring(0, 2);
            String month1 = date1.substring(3, 5);
            String year1 = date1.substring(6);

            String day2 = date2.substring(0, 2);
            String month2 = date2.substring(3, 5);
            String year2 = date2.substring(6);

            // Condition to check the year
            if (year2.compareTo(year1) > 0)
                return -1;
            else if (year2.compareTo(year1) < 0)
                return 1;

            // Condition to check the month    
            else if (month2.compareTo(month1) > 0)
                return -1;
            else if (month2.compareTo(month1) < 0)
                return 1;

            // Condition to check the day
            else if (day2.compareTo(day1) > 0)
                return -1;
            else
                return 1;
        }
    });

    // Loop to print the dates
    for(int i = 0; i < arr.size(); i++)
        System.out.println(arr.get(i));
} 

// Driver code
public static void main(String[] args)
{
    ArrayList<String> arr = new ArrayList<>();
    arr.add("25-08-1996");
    arr.add("03-08-1970");
    arr.add("09-04-1994");
    arr.add("29-08-1996");
    arr.add("14-02-1972");

    printDatesAscending(arr);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to sort the
# array of dates in the form of
# "DD-MM-YYYY" using custom comparator
from functools import cmp_to_key

# Comparator to sort the array of dates
def myCompare(date1, date2):

    day1 = date1[0 : 2]   
    month1 = date1[3 : 3 + 2]
    year1 = date1[6 : 6 + 4]

    day2 = date2[0 : 2]
    month2 = date2[3 : 3 + 2]
    year2 = date2[6 : 6 + 4]

    # Condition to check the year
    if (year1 < year2):
        return -1
    if (year1 > year2):
        return 1

    # Condition to check the month
    if (month1 < month2):
        return -1
    if (month1 > month2):
        return 1

    # Condition to check the day
    if (day1 < day2):
        return -1
    if (day1 > day2):
        return 1

# Function that prints the
# dates in ascensding order
def printDatesAscending(arr):

    # Sort the dates using library
    # sort function with custom Comparator
    arr = sorted(arr, key = cmp_to_key(
        lambda a, b: myCompare(a, b)))

    # Loop to print the dates
    for i in range(len(arr)):
        print(arr[i])

# Driver Code
arr = []
arr.append("25-08-1996")
arr.append("03-08-1970")
arr.append("09-04-1994")
arr.append("29-08-1996")
arr.append("14-02-1972")

printDatesAscending(arr)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to sort the
// array of dates in the form of
// "DD-MM-YYYY" using custom comparator
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Comparator to sort the array of dates
static int myCompare(string date1,
                     string date2)
{
    string day1 = date1.Substring(0, 2);
    string month1 = date1.Substring(3, 2);
    string year1 = date1.Substring(6, 4);

    string day2 = date2.Substring(0, 2);
    string month2 = date2.Substring(3, 2);
    string year2 = date2.Substring(6, 4);

    // Condition to check the year
    return string.Compare(year1, year2);

    // Condition to check the month
    return string.Compare(month1, month2);

    // Condition to check the day
    return string.Compare(day1, day2);
}

// Function that prints the
// dates in ascensding order
static void printDatesAscending(List<string> arr)
{

    // Sort the dates using library
    // sort function with custom Comparator
    arr.Sort(myCompare);

    // Loop to print the dates
    for(int i = 0; i < arr.Count; i++)
        Console.WriteLine(arr[i]);
}

// Driver Code
static public void Main()
{
    List<string> arr = new List<string>();
    arr.Add("25-08-1996");
    arr.Add("03-08-1970");
    arr.Add("09-04-1994");
    arr.Add("29-08-1996");
    arr.Add("14-02-1972");

    printDatesAscending(arr);
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Comparator to sort the array of dates
function myCompare(date1, date2)
{
    var day1 = date1.substr(0, 2);
    var month1 = date1.substr(3, 2);
    var year1 = date1.substr(6, 4);

    var day2 = date2.substr(0, 2);
    var month2 = date2.substr(3, 2);
    var year2 = date2.substr(6, 4);

    // Condition to check the year
    if (year1 < year2)
        return -1;
    if (year1 > year2)
        return 1;

    // Condition to check the month
    if (month1 < month2)
        return -1;
    if (month1 > month2)
        return 1;

    // Condition to check the day
    if (day1 < day2)
        return -1;
    if (day1 > day2)
        return 1;
}

// Function that prints the
// dates in ascensding order
function printDatesAscending( arr)
{
    var n = arr.length;
    // Sort the dates using library
    // sort function with custom Comparator
    arr.sort(myCompare);

    // Loop to print the dates

    for (var i = 0; i < n; i++)
        document.write(arr[i] + "<br>");
}

// Driver Code
var arr = [];
arr.push("25-08-1996");
arr.push("03-08-1970");
arr.push("09-04-1994");
arr.push("29-08-1996");
arr.push("14-02-1972");

printDatesAscending(arr);
</script>
```

**Output:** 

```
03-08-1970
14-02-1972
09-04-1994
25-08-1996
29-08-1996
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(1)