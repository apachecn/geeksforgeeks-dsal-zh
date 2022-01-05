# 如何使用正则表达式

验证 12 小时格式的时间

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证 12 小时格式时间/](https://www.geeksforgeeks.org/how-to-validate-time-in-12-hour-format-using-regular-expression/)

给定一个字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查该字符串是否为 12 小时格式的有效时间。
12 小时格式的有效时间必须满足以下条件:

1.  它应该从 1，2，… 9 或 10，11，12 开始。
2.  后面应该跟一个冒号(:)。
3.  后面应该是 00 到 59 之间的两位数。
4.  它应该只允许一个空格，尽管这是可选的。
5.  它应该以“am”、“pm”或“AM”、“PM”结尾。

**示例:**

> **输入:** str = 12:15 AM
> **输出:**真
> **说明:**给定的字符串满足上述所有条件。
> 
> **输入:** str = 9:45PM
> **输出:**真
> **说明:**给定的字符串满足上述所有条件。
> 
> **输入:** str = 1:15
> **输出:**假
> **说明:**给定的字符串不以‘AM’或‘PM’结尾，因此不是 12 小时格式的有效时间。
> 
> **输入:** str =下午 17:30
> **输出:**假
> **说明:**给定的字符串没有 1 到 12 之间的小时，因此不是 12 小时格式的有效时间。

**方法:**这个问题可以用正则表达式来解决。

1.  去拿绳子。
2.  创建一个正则表达式来检查 12 小时格式的时间，如下所述:

```
regex = "(1[012]|[1-9]):[0-5][0-9](\\s)?(?i)(am|pm)";
```

1.  其中:
    *   **(** 代表组的开始。
    *   **1[012]|[1-9]** 代表时间从 10、11、12 或 1、2、…。9
    *   **)** 代表该组结束。
    *   **:** 表示时间后面必须跟冒号(:)。
    *   **【0-5】【0-9】**代表 00 到 59 之间的时间。
    *   **(\\s)？**代表空白，时间后面跟着空白，空白是可选的。
    *   **(？i)** 表示不区分大小写，“am”、“pm”或“AM”、“PM”分别相同。
    *   **(am|pm)** 代表时间应以‘AM’‘PM’或‘AM’‘PM’结束。
2.  用正则表达式匹配给定的字符串，在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
3.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate the time in
// 12-hour format using Regular Expression.

import java.util.regex.*;

class GFG {

    // Function to validate the time in 12-hour format.
    public static boolean isValidTime(String time)
    {

        // Regex to check valid time in 12-hour format.
        String regexPattern
            = "(1[012]|[1-9]):"
              + "[0-5][0-9](\\s)"
              + "?(?i)(am|pm)";

        // Compile the ReGex
        Pattern compiledPattern
            = Pattern.compile(regexPattern);

        // If the time is empty
        // return false
        if (time == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given time
        // and regular expression.
        Matcher m = compiledPattern.matcher(time);

        // Return if the time
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "12:15 AM";
        System.out.println(isValidTime(str1));

        // Test Case 2:
        String str2 = "9:45PM";
        System.out.println(isValidTime(str2));

        // Test Case 3:
        String str3 = "1:15";
        System.out.println(isValidTime(str3));

        // Test Case 4:
        String str4 = "17:30";
        System.out.println(isValidTime(str4));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate the time in
# 12-hour format using Regular Expression.
import re

# Function to validate the time in 12-hour format.
def isValidTime(time) :

    # Regex to check valid time in 12-hour format.
    regexPattern = "(1[012]|[1-9]):"+ "[0-5][0-9](\\s)"+ "?(?i)(am|pm)";

    # Compile the ReGex
    compiledPattern = re.compile(regexPattern);

    # If the time is empty
    # return false
    if (time == None) :
        return False;

    # re library contains search() method
    # to find matching between given time
    # and regular expression.
    # Return if the time
    # matched the ReGex
    if re.search(compiledPattern,time):
        return True
    else :
        return False

# Driver Code.
if __name__ == "__main__" :

    # Test Case 1:
    str1 = "12:15 AM";
    print(isValidTime(str1));

    # Test Case 2:
    str2 = "9:45PM";
    print(isValidTime(str2));

    # Test Case 3:
    str3 = "1:15";
    print(isValidTime(str3));

    # Test Case 4:
    str4 = "17:30";
    print(isValidTime(str4));

# This code is contributed by AnkitRai01
```

## C++

```
// C++ program to validate
// time in 12-hour format
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate time in 12-hour format
bool isValidTime(string str)
{

    // Regex to check valid time in 12-hour format
    const regex pattern(
        "((([1-9])|(1[0-2])):([0-5])([0-9])(\\s)(A|P)M)");

    // If the time in 12-hour format
    // is empty return false
    if (str.empty())
    {
        return false;
    }

    // Return true if the time in 12-hour format
    // matched the ReGex
    if (regex_match(str, pattern))
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver Code
int main()
{
    // Test Case 1:
    string str1 = "12:15 AM";
    cout << isValidTime(str1) << endl;

    // Test Case 2:
    string str2 = "9:45 PM";
    cout << isValidTime(str2) << endl;

    // Test Case 3:
    string str3 = "1:15";
    cout << isValidTime(str3) << endl;

    // Test Case 4:
    string str4 = "17:30";
    cout << isValidTime(str4) << endl;

    return 0;
}

// This code is contributed by yuvraj_chandra
```

**Output**

```
true
true
false
false
```