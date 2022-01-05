# 如何使用正则表达式

验证 24 小时格式的时间

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证 24 小时格式时间/](https://www.geeksforgeeks.org/how-to-validate-time-in-24-hour-format-using-regular-expression/)

给定一个字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查该字符串是否为 24 小时格式的有效时间。

> 24 小时格式的有效时间必须满足以下条件。
> 
> 1.  应该从 0-23 或者 00-23 开始。
> 2.  后面应该跟一个':'(冒号)。
> 3.  后面应该是从 00 到 59 的两位数。
> 4.  它不应该以“am”、“pm”或“AM”、“PM”结尾。

**例:**

> **输入:** str = "13:05"
> **输出:**真
> **说明:**给定字符串满足上述所有条件。
> **输入:** str = "02:15"
> **输出:**真
> **说明:**给定字符串满足上述所有条件。
> **输入:** str = "24:00"
> **输出:**假
> **解释:**给定的字符串不在 0-23 或 00-23 的范围内(即小时超出范围)，因此不是 24 小时格式的有效时间。
> **输入:** str = "10:60"
> **输出:**假
> **说明:**给定的字符串不在 00 到 59 的范围内(即分钟超出范围)，因此不是 24 小时格式的有效时间。
> **输入:** str = "10:15 PM"
> **输出:** false
> **解释:**给定字符串以‘AM’或‘PM’结尾，因此不是 24 小时格式的有效时间。

**方法:**这个问题可以用正则表达式来解决。

1.  去拿绳子。
2.  创建一个正则表达式来检查 24 小时格式的时间，如下所述:

```
regex = "([01]?[0-9]|2[0-3]):[0-5][0-9]";
```

1.  其中:
    *   **(** 代表组的开始。
    *   **【01】？[0-9]** 代表时间从 0-9、1-9、00-09、10-19 开始。
    *   **|** 代表或。
    *   **2[0-3]** 代表从 20-23 开始的时间。
    *   **)** 代表该组结束。

    *   **:** 表示时间后应该跟一个冒号(:)。
    *   **【0-5】【0-9】**表示 00 到 59 之间的时间
2.  用正则表达式匹配给定的字符串，在 Java 中，这可以通过使用 Pattern.matcher()来完成。
3.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate
// time in 24-hour format
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate time in 24-hour format
bool isValidTime(string str)
{

  // Regex to check valid time in 24-hour format
  const regex pattern("([01]?[0-9]|2[0-3]):[0-5][0-9]");

  // If the time in 24-hour format
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the time in 24-hour format
  // matched the ReGex
  if(regex_match(str, pattern))
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
  string str1 = "13:05";
  cout << str1 + ": "<< isValidTime(str1) << endl;

  // Test Case 2:
  string str2 = "02:15";
  cout << str2 + ": "<< isValidTime(str2) << endl;

  // Test Case 3:
  string str3 = "24:00";
  cout << str3 + ": "<< isValidTime(str3) << endl;

  // Test Case 4:
  string str4 = "10:60";
  cout << str4 + ": "<< isValidTime(str4) << endl;

  // Test Case 5:
  string str5 = "10:15 PM";
  cout << str5 + ": "<< isValidTime(str5) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate the time in
// 24-hour format using Regular Expression.

import java.util.regex.*;

class GFG {

    // Function to validate the time in 24-hour format
    public static boolean isValidTime(String time)
    {

        // Regex to check valid time in 24-hour format.
        String regex = "([01]?[0-9]|2[0-3]):[0-5][0-9]";

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the time is empty
        // return false
        if (time == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given time
        // and regular expression.
        Matcher m = p.matcher(time);

        // Return if the time
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "13:05";
        System.out.println(str1 + ": "
                           + isValidTime(str1));

        // Test Case 2:
        String str2 = "02:15";
        System.out.println(str2 + ": "
                           + isValidTime(str2));

        // Test Case 3:
        String str3 = "24:00";
        System.out.println(str3 + ": "
                           + isValidTime(str3));

        // Test Case 4:
        String str4 = "10:60";
        System.out.println(str4 + ": "
                           + isValidTime(str4));

        // Test Case 5:
        String str5 = "10:15 PM";
        System.out.println(str5 + ": "
                           + isValidTime(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate the time in
# 24-hour format using Regular Expression.
import re

# Function to validate the time
# in 24-hour format
def isValidTime(time):

    # Regex to check valid time in 24-hour format.
    regex = "^([01]?[0-9]|2[0-3]):[0-5][0-9]{content}quot;;

    # Compile the ReGex
    p = re.compile(regex);

    # If the time is empty
    # return false
    if (time == "") :
        return False;

    # Pattern class contains matcher() method
    # to find matching between given time
    # and regular expression.
    m = re.search(p, time);

    # Return True if the time
    # matched the ReGex otherwise False
    if m is None :
        return False;
    else :
        return True

# Driver Code.
if __name__ == "__main__" :

    # Test Case 1:
    str1 = "13:05";
    print(str1, ": ", isValidTime(str1));

    # Test Case 2:
    str2 = "02:15";
    print(str2, ": ", isValidTime(str2));

    # Test Case 3:
    str3 = "24:00";
    print(str3, ": ", isValidTime(str3));

    # Test Case 4:
    str4 = "10:60";
    print(str4, ": ", isValidTime(str4));

    # Test Case 5:
    str5 = "10:15 PM";
    print(str5, ": ", isValidTime(str5));

# This code is contributed by AnkitRai01
```

**Output:** 

```
13:05: true
02:15: true
24:00: false
10:60: false
10:15 PM: false
```