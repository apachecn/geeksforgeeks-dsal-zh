# 如何使用正则表达式

检查字符串是否为字母数字

> 原文:[https://www . geesforgeks . org/如何检查字符串是字母数字还是不使用正则表达式/](https://www.geeksforgeeks.org/how-to-check-string-is-alphanumeric-or-not-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查字符串是否为字母数字。

> 一个**字母数字字符串**是一个只包含 a-z、A-Z 字母和一些 0-9 数字的字符串。

**示例:**

> **输入:**str = " geeksforgeecks 123 "
> **输出:**真
> **解释:**
> 该字符串包含 a-z、A-Z 中的所有字母，以及 0-9 中的数字。因此，它是一个字母数字字符串。
> **输入:**str = " geeks forgeeks "
> **输出:** false
> **解释:**
> 该字符串包含 a-z、A-Z 中的所有字母，但不包含 0-9 中的任何数字。因此，它不是字母数字字符串。
> **输入:**str = " geeksforgeecks 123 @ # "
> **输出:** false
> **解释:**
> 这个字符串包含了从 a-z、A-Z 开始的所有字母，以及从 0-9 开始的数字以及一些特殊的符号。因此，它不是字母数字字符串。

**方法:**这个问题可以用正则表达式来解决。

*   去拿绳子。
*   如下所述，创建一个正则表达式来检查字符串是否为字母数字:

```
regex = "^(?=.*[a-zA-Z])(?=.*[0-9])[A-Za-z0-9]+{content}quot;;

```

*   其中:
    *   **^** 代表字符串的开始
    *   **(？=.*[a-za-z])** 代表从 A-Z、A-Z
    *   **(？=.*[0-9])** 代表 0-9 之间的任何数字
    *   **【A-Za-z0-9】**表示所有内容是字母还是数字
    *   **+** 代表一次或多次
    *   **$** 代表字符串的结尾
*   用正则表达式匹配给定的字符串，在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false

下面是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check string is
// alphanumeric or not using Regular Expression.

import java.util.regex.*;

class GFG {

    // Function to check string is alphanumeric or not
    public static boolean isAlphaNumeric(String str)
    {
        // Regex to check string is alphanumeric or not.
        String regex = "^(?=.*[a-zA-Z])(?=.*[0-9])[A-Za-z0-9]+{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given string
        // and regular expression.
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "GeeksforGeeks123";
        System.out.println(
            str1 + ": "
            + isAlphaNumeric(str1));

        // Test Case 2:
        String str2 = "GeeksforGeeks";
        System.out.println(
            str2 + ": "
            + isAlphaNumeric(str2));

        // Test Case 3:
        String str3 = "GeeksforGeeks123@#";
        System.out.println(
            str3 + ": "
            + isAlphaNumeric(str3));

        // Test Case 4:
        String str4 = "123";
        System.out.println(
            str4 + ": "
            + isAlphaNumeric(str4));

        // Test Case 5:
        String str5 = "@#";
        System.out.println(
            str5 + ": "
            + isAlphaNumeric(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to check
# string is alphanumeric or
# not using Regular Expression.
import re

# Function to check string
# is alphanumeric or not
def isAlphaNumeric(str):

    # Regex to check string is
    # alphanumeric or not.
    regex = "^(?=.*[a-zA-Z])(?=.*[0-9])[A-Za-z0-9]+{content}quot;

    # Compile the ReGex
    p = re.compile(regex)

    # If the string is empty
    # return false
    if(str == None):
        return False

    # Return if the string
    # matched the ReGex
    if(re.search(p, str)):
        return True
    else:
        return False

# Driver Code

# Test Case 1:
str1 = "GeeksforGeeks123"
print(str1, ":",
      isAlphaNumeric(str1))

# Test Case 2:
str2 = "GeeksforGeeks"
print(str2, ":",
      isAlphaNumeric(str2))

# Test Case 3:
str3 = "GeeksforGeeks123@#"
print(str3, ":",
      isAlphaNumeric(str3))

# Test Case 4:
str4 = "123"
print(str4, ":",
      isAlphaNumeric(str4))

# Test Case 5:
str5 = "@#"
print(str5, ":",
      isAlphaNumeric(str5))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
GeeksforGeeks123: true
GeeksforGeeks: false
GeeksforGeeks123@#: false
123: false
@#: false

```