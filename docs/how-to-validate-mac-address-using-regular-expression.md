# 如何使用正则表达式

验证 MAC 地址

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证 mac 地址/](https://www.geeksforgeeks.org/how-to-validate-mac-address-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的 [MAC 地址](https://www.geeksforgeeks.org/introduction-of-mac-address-in-computer-network/)。

> 有效的[媒体访问控制地址](https://www.geeksforgeeks.org/introduction-of-mac-address-in-computer-network/)必须满足以下条件:
> 
> 1.  它必须包含 12 个十六进制数字。
> 2.  表示它们的一种方法是用连字符(-)或冒号(:)分隔六对字符。例如，01-23-45-67-89-AB 是有效的 MAC 地址。
> 3.  表示它们的另一种方法是形成三组四个十六进制数字，用点(。).例如，0123.4567.89AB 是有效的媒体访问控制地址。

**示例:**

> **输入:**str = " 01-23-45-67-89-AB "；
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，它是一个有效的媒体访问控制地址。
> 
> **输入:**str = " 01-23-45-67-89-AH "；
> **输出:**假
> **解释:**
> 给定的字符串包含‘H’，有效的十六进制数字后面应该是字母 a-f、A-F 和 0-9。因此，它不是有效的媒体访问控制地址。
> 
> **输入:**str = " 01-23-45-67-AH "；
> **输出:**假
> **解释:**
> 给定的字符串有五组两个十六进制数字。因此，它不是有效的媒体访问控制地址。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案。

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的 MAC 地址:

> regex = " ^([0-9a-fa-f]{2}[:-]){5}([0-9a-fa-f]{2})|([0-9a-fa-f]{4}\\.[0-9a-fA-F]{4}\\。[0-9a-Fa-F]{ 4 }){ content } # x201；；

*   其中:
    *   **^** 代表弦的起点。
    *   **([0-9A-Fa-f]{2}[:-]){5}** 代表由连字符(-)或冒号(:)分隔的五组两个十六进制数字
    *   **([0-9A-Fa-f]{2})** 代表一组两个十六进制数字。
    *   **|** 代表或。
    *   **(** 代表组的开始。
    *   **[0-9a-fA-F]{4}\\。**表示由点()分隔的四个十六进制数字的第一部分。).
    *   **[0-9a-fA-F]{4}\\。**表示由点()分隔的四个十六进制数字的第二部分。).
    *   **【0-9a-fA-F】{ 4 }**代表四个十六进制数字的第三部分。
    *   **)** 代表团体结束。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// MAC address using
// regular expression

import java.util.regex.*;
class GFG {

    // Function to validate
    // MAC address
    // using regular expression
    public static boolean isValidMACAddress(String str)
    {
        // Regex to check valid
        // MAC address
        String regex = "^([0-9A-Fa-f]{2}[:-])"
                       + "{5}([0-9A-Fa-f]{2})|"
                       + "([0-9a-fA-F]{4}\\."
                       + "[0-9a-fA-F]{4}\\."
                       + "[0-9a-fA-F]{4}){content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null)
        {
            return false;
        }

        // Find match between given string
        // and regular expression
        // uSing Pattern.matcher()

        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver code
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "01-23-45-67-89-AB";
        System.out.println(isValidMACAddress(str1));

        // Test Case 2:
        String str2 = "01:23:45:67:89:AB";
        System.out.println(isValidMACAddress(str2));

        // Test Case 3:
        String str3 = "0123.4567.89AB";
        System.out.println(isValidMACAddress(str3));

        // Test Case 4:
        String str4 = "01-23-45-67-89-AH";
        System.out.println(isValidMACAddress(str4));

        // Test Case 5:
        String str5 = "01-23-45-67-AH";
        System.out.println(isValidMACAddress(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# MAC address using
# using regular expression
import re

# Function to validate MAC address.

def isValidMACAddress(str):

    # Regex to check valid
    # MAC address
    regex = ("^([0-9A-Fa-f]{2}[:-])" +
             "{5}([0-9A-Fa-f]{2})|" +
             "([0-9a-fA-F]{4}\\." +
             "[0-9a-fA-F]{4}\\." +
             "[0-9a-fA-F]{4}){content}quot;)

    # Compile the ReGex
    p = re.compile(regex)

    # If the string is empty
    # return false
    if (str == None):
        return False

    # Return if the string
    # matched the ReGex
    if(re.search(p, str)):
        return True
    else:
        return False

# Driver code

# Test Case 1:
str1 = "01-23-45-67-89-AB"
print(isValidMACAddress(str1))

# Test Case 2:
str2 = "01:23:45:67:89:AB"
print(isValidMACAddress(str2))

# Test Case 3:
str3 = "0123.4567.89AB"
print(isValidMACAddress(str3))

# Test Case 4:
str4 = "01-23-45-67-89-AH"
print(isValidMACAddress(str4))

# Test Case 5:
str5 = "01-23-45-67-AH"
print(isValidMACAddress(str5))

# This code is contributed by avanitrachhadiya2155
```

## C++

```
// C++ program to validate the
// MAC address
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the MAC address
bool isValidMACAddress(string str)
{

    // Regex to check valid MAC address
    const regex pattern(
    "^([0-9A-Fa-f]{2}[:-]){5}"
      "([0-9A-Fa-f]{2})|([0-9a-"
    "fA-F]{4}\\.[0-9a-fA-F]"
      "{4}\\.[0-9a-fA-F]{4}){content}quot;);

    // If the MAC address
    // is empty return false
    if (str.empty())
    {
        return false;
    }

    // Return true if the MAC address
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
    string str1 = "01-23-45-67-89-AB";
    cout << isValidMACAddress(str1) << endl;

    // Test Case 2:
    string str2 = "01:23:45:67:89:AB";
    cout << isValidMACAddress(str2) << endl;

    // Test Case 3:
    string str3 = "0123.4567.89AB";
    cout << isValidMACAddress(str3) << endl;

    // Test Case 4:
    string str4 = "01-23-45-67-89-AH";
    cout << isValidMACAddress(str4) << endl;

    // Test Case 5:
    string str5 = "01-23-45-67-AH";
    cout << isValidMACAddress(str5) << endl;

    return 0;
}

// This code is contributed by yuvraj_chandra
```

**Output**

```
true
true
true
false
false
```