# 如何使用正则表达式

验证十六进制色码

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证十六进制颜色代码/](https://www.geeksforgeeks.org/how-to-validate-hexadecimal-color-code-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查字符串是否有效[十六进制色码](https://www.geeksforgeeks.org/how-to-get-hex-color-value-of-rgb-value/)。

> 有效的十六进制颜色代码必须满足以下条件。
> 
> 1.  它应该从“#”符号开始。
> 2.  后面应该是字母 a-f、A-F 和/或数字 0-9。
> 3.  十六进制颜色代码的长度应为 6 或 3，不包括“#”符号。

例如:#abc、#ABC、#000、#FFF、#000000、#FF0000、#00FF00、#0000FF、#FFFFFF 都是有效的十六进制颜色代码。
**例:**

> **输入:**str = " # 1 affa 1 "；
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。
> **输入:**str = " # F00 "；
> **输出:**真
> **说明:**
> 给定字符串满足上述所有条件。
> **输入:**str = " 123456 "；
> **输出:**为假
> **说明:**
> 给定的字符串不以“#”符号开头，因此不是有效的十六进制颜色代码。
> **输入:**str = " # 123 abce "；
> **输出:**假
> **说明:**
> 给定字符串长度为 7，有效的十六进制色码长度应为 6 或 3。因此它不是有效的十六进制颜色代码。
> **输入:**str =“# afafah”；
> **输出:**假
> **说明:**
> 给定的字符串包含‘h’，有效的十六进制颜色代码后面应该跟有字母 a-f，A-F，因此不是有效的十六进制颜色代码。

**方法:**这个问题可以用正则表达式来解决。

*   去拿绳子。
*   如下所述，创建一个正则表达式来检查有效的十六进制颜色代码:

```
regex = "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3}){content}quot;;
```

*   其中:
    *   **^** 代表弦的起点。
    *   **#** 代表十六进制颜色代码必须以“#”符号开头。
    *   **(** 代表组的开始。
    *   **【a-fa-F0-9】{ 6 }**代表字母 a-f、A-F 或 0-9 的数字，长度为 6。
    *   **|** 代表或。
    *   **【a-fa-F0-9】{ 3 }**代表字母 a-f、A-F 或 0-9 的数字，长度为 3。
    *   **)** 代表该组结束。
    *   **$** 代表字符串的结尾。
*   用正则表达式匹配给定的字符串，在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## C++

```
// C++ program to validate the
// hexadecimal color code using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the hexadecimal color code.
bool isValidHexaCode(string str)
{

  // Regex to check valid hexadecimal color code.
  const regex pattern("^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3}){content}quot;);

  // If the hexadecimal color code
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the hexadecimal color code
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
  string str1 = "#1AFFa1";
  cout << str1 + ": " << isValidHexaCode(str1) << endl;

  // Test Case 2:
  string str2 = "#F00";
  cout << str2 + ": " <<  isValidHexaCode(str2) << endl;

  // Test Case 3:
  string str3 = "123456";
  cout << str3 + ": " <<  isValidHexaCode(str3) << endl;

  // Test Case 4:
  string str4 = "#123abce";
  cout << str4 + ": " <<  isValidHexaCode(str4) << endl;

  // Test Case 5:
  string str5 = "#afafah";
  cout << str5 + ": " <<  isValidHexaCode(str5) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate hexadecimal
// colour code using Regular Expression

import java.util.regex.*;

class GFG {

    // Function to validate hexadecimal color code .
    public static boolean isValidHexaCode(String str)
    {
        // Regex to check valid hexadecimal color code.
        String regex = "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3}){content}quot;;

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
        String str1 = "#1AFFa1";
        System.out.println(
            str1 + ": "
            + isValidHexaCode(str1));

        // Test Case 2:
        String str2 = "#F00";
        System.out.println(
            str2 + ": "
            + isValidHexaCode(str2));

        // Test Case 3:
        String str3 = "123456";
        System.out.println(
            str3 + ": "
            + isValidHexaCode(str3));

        // Test Case 4:
        String str4 = "#123abce";
        System.out.println(
            str4 + ": "
            + isValidHexaCode(str4));

        // Test Case 5:
        String str5 = "#afafah";
        System.out.println(
            str5 + ": "
            + isValidHexaCode(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# hexadecimal colour code using
# Regular Expression
import re

# Function to validate
# hexadecimal color code .
def isValidHexaCode(str):

    # Regex to check valid
    # hexadecimal color code.
    regex = "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3}){content}quot;

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

# Driver Code.

# Test Case 1:
str1 = "#1AFFa1"
print(str1, ":", isValidHexaCode(str1))

# Test Case 2:
str2 = "#F00"
print(str2, ":", isValidHexaCode(str2))

# Test Case 3:
str3 = "123456"
print(str3, ":", isValidHexaCode(str3))

# Test Case 4:
str4 = "#123abce"
print(str4, ":", isValidHexaCode(str4))

# Test Case 5:
str5 = "#afafah"
print(str5, ":", isValidHexaCode(str5))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
#1AFFa1: true
#F00: true
123456: false
#123abce: false
#afafah: false
```