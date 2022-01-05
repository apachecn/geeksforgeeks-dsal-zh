# 从字符串中找出不同年份的总数

> 原文:[https://www . geeksforgeeks . org/find-从字符串中找出不同年份的总数/](https://www.geeksforgeeks.org/find-total-number-of-distinct-years-from-a-string/)

给定一个包含单词和日期的字符串，任务是找到该字符串中提到的不同年份的总数。
**注:**假设日期为‘日-月-年’格式。

**示例:**

```
Input:  str = "UN was established on 24-10-1945.
                India got freedom on 15-08-1947."
Output: 2
2 distinct years i.e. 1945 and 1947 have been referenced.

Input: str = "Soon after the world war 2 ended on 02-09-1945.
        The UN was established on 24-10-1945."
Output: 1
Only 1 Year, i.e 1945 has been referenced .
```

**进场:**

1.  开始解开绳子。
2.  检查当前字符是否为数字。将其存储在另一个字符串中，即 dateString。
3.  检查当前字符是否为“-”，然后删除存储在日期字符串中的字符。
4.  检查日期字符串的长度是否等于 4，这意味着它是一年。
5.  将年份存储在无序集中。
6.  返回无序集的大小，因为它只包含唯一的值。

下面是上述方法的实现:

## C++

```
// C++ Program to find the total
// number of distinct years
#include <bits/stdc++.h>
using namespace std;

// function to find the total
// number of distinct years
int distinct_year(string str)
{
    string str2 = "";

    unordered_set<string> uniqueDates;

    for (int i = 0; i < str.length(); i++) {

        if (isdigit(str[i])) {
            str2.push_back(str[i]);
        }

        // if we found - then clear the str2
        if (str[i] == '-') {
            str2.clear();
        }

        // if length of str2 becomes 4
        // then store it in a set
        if (str2.length() == 4) {
            uniqueDates.insert(str2);
            str2.clear();
        }
    }

    // return the size of set
    return uniqueDates.size();
}

// Driver code
int main()
{
    string str = "UN was established on 24-10-1945."
                 "India got freedom on 15-08-1947.";

    cout << distinct_year(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashSet;
import java.util.Set;

// Java Program to find the total
// number of distinct years
public class GFG {

// function to find the total
// number of distinct years
    static int distinct_year(String str) {
        String str2 = "";

        Set<String> uniqueDates = new HashSet<>();

        for (int i = 0; i < str.length(); i++) {

            if (Character.isDigit(str.charAt(i))) {
                str2 += (str.charAt(i));
            }

            // if we found - then clear the str2
            if (str.charAt(i) == '-') {
                str2 = "";
            }

            // if length of str2 becomes 4
            // then store it in a set
            if (str2.length() == 4) {
                uniqueDates.add(str2);
                str2 = "";
            }
        }

        // return the size of set
        return uniqueDates.size();
    }

// Driver code
    static public void main(String[] args) {
        String str = "UN was established on 24-10-1945."
                + "India got freedom on 15-08-1947.";

        System.out.println(distinct_year(str));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to find the total
# number of distinct years

# function to find the total
# number of distinct years
import re
def distinct_years(str):
    str2 = ""

    uniqueDates = set()
    pattern="[0-9][0-9]-[0-9][0-9]-[0-9][0-9][0-9][0-9]"
    dates = re.findall(pattern,str)
    for item in dates:
        uniqueDates.add(item.split('-')[-1])
    # return the size of se
    return len(uniqueDates)

# Driver code
if __name__ == "__main__":
    str = "UN was established on 24-10-1945.\
           India got freedom on 15-08-1947."

    print(distinct_years(str))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# Program to find the total
// number of distinct years
using System;
using System.Collections.Generic;

class GFG
{

    // function to find the total
    // number of distinct years
    static int distinct_year(String str)
    {
        String str2 = "";

        HashSet<String> uniqueDates = new HashSet<String>();

        for (int i = 0; i < str.Length; i++)
        {
            if (char.IsDigit(str[i]))
            {
                str2 += (str[i]);
            }

            // if we found - then clear the str2
            if (str[i] == '-')
            {
                str2 = "";
            }

            // if length of str2 becomes 4
            // then store it in a set
            if (str2.Length == 4)
            {
                uniqueDates.Add(str2);
                str2 = "";
            }
        }

        // return the size of set
        return uniqueDates.Count;
    }

    // Driver code
    static public void Main(String[] args)
    {
        String str = "UN was established on 24-10-1945." +
                     "India got freedom on 15-08-1947.";

        Console.WriteLine(distinct_year(str));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript Program to find the total
// number of distinct years

// function to find the total
// number of distinct years
function distinct_year(str)
{
    var str2 = "";

    var uniqueDates = new Set();

    for (var i = 0; i < str.length; i++) {

        if (parseInt(str[i])) {
            str2+=(str[i]);
        }

        // if we found - then clear the str2
        if (str[i] == '-') {
            str2 = "";
        }

        // if length of str2 becomes 4
        // then store it in a set
        if (str2.length == 4) {
            uniqueDates.add(str2);
            str2 = "";
        }
    }

    // return the size of set
    return uniqueDates.size;
}

// Driver code
var str = "UN was established on 24-10-1945." +
             "India got freedom on 15-08-1947.";
document.write( distinct_year(str));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n)