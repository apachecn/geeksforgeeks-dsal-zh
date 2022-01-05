# 如何使用正则表达式

验证印度驾照号码

> 原文:[https://www . geesforgeks . org/如何验证-印度-驾驶执照-号码-使用-正则表达式/](https://www.geeksforgeeks.org/how-to-validate-indian-driving-license-number-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的印度驾照号码。
有效的印度驾照号码必须满足以下条件:

1.  长度应为 16 个字符(包括空格或连字符(-))。
2.  驾驶执照号码可以用以下任何格式输入:

```
HR-0619850034761
 OR 
HR06 19850034761
```

1.  前两个字符应该是代表状态代码的大写字母。
2.  接下来的两个字符应该是代表实时操作系统代码的数字。
3.  接下来的四个字符应该是代表许可证颁发年份的数字。
4.  接下来的七个字符应该是 0-9 之间的任意数字。

**注:**在本文中，我们将检查 1900-2099 年的许可证发放年份。可以自定义以更改许可证颁发年份。

**示例:**

> **输入:**str = " HR-0619850034761 "；
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。所以不是有效的印度驾照号码。
> 
> **输入:**str = " MH27 30120034761 "；
> **输出:**假
> **解释:**
> 给定的字符串有许可证颁发年份 3012，那不是有效年份，因为在本文中我们验证了 1900-2099 年。所以不是有效的印度驾照号码。
> 
> **输入:**str = " GJ-2420180 "；
> **输出:**假
> **说明:**
> 给定字符串有 10 个字符。所以不是有效的印度驾照号码。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案:

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的印度驾照号码:

> regex = " ^(([a-z]{2}[0-9]{2})( " |([a-z]{ 2 }-[0-9]{ 2 })((19 | 20)[0-9][0-9])[0-9]{ 7 } { content }；；

*   其中:
    *   **^** 代表弦的起点。
    *   **(** 代表第 1 组开始。
    *   **(** 代表第 2 组开始。
    *   **【A-Z】{ 2 }**代表前两个字符应该是大写字母。
    *   **[0-9]{2}** 代表接下来的两个字符应该是数字。
    *   **)** 代表第二组结束。
    *   **( )** 代表空格字符。
    *   **|** 代表或。
    *   **(** 代表第 3 组开始。
    *   **【A-Z】{ 2 }**代表前两个字符应该是大写字母。
    *   **–**代表连字符。
    *   **[0-9]{2}** 代表接下来的两个字符应该是数字。
    *   **)** 代表第三组的结束。
    *   **)** 代表第 1 组的结束。
    *   **((19|20)[0-9][0-9])** 代表 1900-2099 年。
    *   **[0-9]{7}** 代表接下来的七个字符应该是 0-9 之间的任意数字。
    *   **$** 代表字符串的结尾。
*   用正则表达式匹配给定的字符串，在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// Indian driving license number
// using regular expression

import java.util.regex.*;
class GFG {

    // Function to validate
    // Indian driving license number
    // using regular expression
    public static boolean isValidLicenseNo(String str)
    {
        // Regex to check valid
        // Indian driving license number
        String regex = "^(([A-Z]{2}[0-9]{2})"
                       + "( )|([A-Z]{2}-[0-9]"
                       + "{2}))((19|20)[0-9]"
                       + "[0-9])[0-9]{7}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null) {
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
        String str1 = "HR-0619850034761";
        System.out.println(isValidLicenseNo(str1));

        // Test Case 2:
        String str2 = "UP14 20160034761";
        System.out.println(isValidLicenseNo(str2));

        // Test Case 3:
        String str3 = "12HR-37200602347";
        System.out.println(isValidLicenseNo(str3));

        // Test Case 4:
        String str4 = "MH27 30123476102";
        System.out.println(isValidLicenseNo(str4));

        // Test Case 5:
        String str5 = "GJ-2420180";
        System.out.println(isValidLicenseNo(str5));
    }
}
```

## 蟒蛇 3

```
# Python program to validate
# Indian driving license number
# using regular expression

import re

# Function to validate Indian
# driving license number.
def isValidLicenseNo(str):

    # Regex to check valid
    # Indian driving license number
    regex = ("^(([A-Z]{2}[0-9]{2})" +
             "( )|([A-Z]{2}-[0-9]" +
             "{2}))((19|20)[0-9]" +
             "[0-9])[0-9]{7}{content}quot;)

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
str1 = "HR-0619850034761"
print(isValidLicenseNo(str1))

# Test Case 2:
str2 = "UP14 20160034761"
print(isValidLicenseNo(str2))

# Test Case 3:
str3 = "12HR-37200602347"
print(isValidLicenseNo(str3))

# Test Case 4:
str4 = "MH27 30123476102"
print(isValidLicenseNo(str4))

# Test Case 5:
str5 = "GJ-2420180"
print(isValidLicenseNo(str5))

# This code is contributed by avanitrachhadiya2155
```

## C++

```
// C++ program to validate the
// Indian driving license number
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the
// Indian driving license number
bool isValidLicenseNo(string str)
{

    // Regex to check valid
    // Indian driving license number
    const regex pattern("^(([A-Z]{2}[0-9]{2})( "
                        ")|([A-Z]{2}-[0-9]{2}))"
                        "((19|20)[0-"
                        "9][0-9])[0-9]{7}{content}quot;);

    // If the Indian driving
    // license number is empty return false
    if (str.empty())
    {
        return false;
    }

    // Return true if the Indian
    // driving license number
    // matched the ReGex
    if (regex_match(str, pattern))
    {
        return true;
    }
    else {
        return false;
    }
}

// Driver Code
int main()
{
    // Test Case 1:
    string str1 = "HR-0619850034761";
    cout << isValidLicenseNo(str1) << endl;

    // Test Case 2:
    string str2 = "UP14 20160034761";
    cout << isValidLicenseNo(str2) << endl;

    // Test Case 3:
    string str3 = "12HR-37200602347";
    cout << isValidLicenseNo(str3) << endl;

    // Test Case 4:
    string str4 = "MH27 30123476102";
    cout << isValidLicenseNo(str4) << endl;

    // Test Case 5:
    string str5 = "GJ-2420180";
    cout << isValidLicenseNo(str5) << endl;

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
false

```