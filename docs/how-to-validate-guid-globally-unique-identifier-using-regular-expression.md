# 如何使用正则表达式

验证 GUID(全球唯一标识符)

> 原文:[https://www . geesforgeks . org/如何验证-guid-全局唯一标识符-使用-正则表达式/](https://www.geeksforgeeks.org/how-to-validate-guid-globally-unique-identifier-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的 GUID(全球唯一标识符)。
有效的 [GUID(全球唯一标识符)](https://en.wikipedia.org/wiki/Universally_unique_identifier)必须指定以下条件:

1.  应该是 128 位数字。
2.  长度应为 36 个字符(32 个十六进制字符和 4 个连字符)。
3.  它应该显示在由连字符(-)分隔的五个组中。
4.  Microsoft GUIDs 有时用周围的大括号表示。

**示例:**

> **输入:**str = " 123 e 4567-e89 B- 12 D3-a456-9ac 7 cbdcee52 "
> **输出:**真
> **解释:**
> 给定字符串满足上述所有条件。因此，它是一个有效的 GUID(全球唯一标识符)。
> **输入:**str = " 123 e 4567-h89 B- 12 D3-a456-9ac 7 cbdcee52 "
> **输出:** false
> **解释:**
> 给定字符串包含‘h’，有效的十六进制字符后面应该跟有来自 a-f、A-F 和 0-9 的字符。因此，它不是有效的 GUID(全球唯一标识符)。
> **输入:**str = " 123 e 4567-h89 B- 12 D3-a456 "
> **输出:**假
> **解释:**
> 给定字符串有 20 个字符。因此，它不是有效的 GUID(全球唯一标识符)。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案:

*   获取字符串。
*   创建一个正则表达式来检查有效的 GUID(全球唯一标识符)，如下所述:

> regex =“^[{”？[0-9a-fA-F]{ 8 }-([0-9a-fA-F]{ 4 }-){ 3 }[0-9a-fA-F]{ 12 }[}]？{ content } # x201D

*   其中:
    *   **^** 代表弦的起点。
    *   **[{]？**表示可选的' { 0 } '字符。
    *   **【0-9a-fa-f】{ 8 }**代表 A-F、A-F、0-9 的 8 个字符。
    *   **–**代表连字符。
    *   **([0-9a-fa-f]{4}-){3}** 表示重复 3 次的 A-F、A-F 和 0-9 的 4 个字符，用连字符(-)分隔。
    *   **【0-9a-fa-f】{ 12 }**代表 A-F、A-F、0-9 中的 12 个字符。
    *   **[}]？**表示可选的“}”字符。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate the
// GUID (Globally Unique Identifier) using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the GUID (Globally Unique Identifier).
bool isValidGUID(string str)
{

  // Regex to check valid GUID (Globally Unique Identifier).
  const regex pattern("^[{]?[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}[}]?{content}quot;);

  // If the GUID (Globally Unique Identifier)
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the GUID (Globally Unique Identifier)
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
  string str1 = "123e4567-e89b-12d3-a456-9AC7CBDCEE52";
  cout << isValidGUID(str1) << endl;

  // Test Case 2:
  string str2 = "{123e4567-e89b-12d3-a456-9AC7CBDCEE52}";
  cout <<  isValidGUID(str2) << endl;

  // Test Case 3:
  string str3 = "123e4567-h89b-12d3-a456-9AC7CBDCEE52";
  cout <<  isValidGUID(str3) << endl;

  // Test Case 4:
  string str4 = "123e4567-h89b-12d3-a456";
  cout <<  isValidGUID(str4) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// GUID (Globally Unique Identifier)
// using regular expression

import java.util.regex.*;

class GFG {

    // Function to validate
    // GUID (Globally Unique Identifier)
    // using regular expression
    public static boolean
    isValidGUID(String str)
    {
        // Regex to check valid
        // GUID (Globally Unique Identifier)
        String regex
            = "^[{]?[0-9a-fA-F]{8}"
              + "-([0-9a-fA-F]{4}-)"
              + "{3}[0-9a-fA-F]{12}[}]?{content}quot;;

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
        String str2
            = "123e4567-e89b-12d3"
              + "-a456-9AC7CBDCEE52";
        System.out.println(
            isValidGUID(str2));

        // Test Case 2:
        String str3
            = "{123e4567-e89b-12d3-"
              + "a456-9AC7CBDCEE52}";
        System.out.println(
            isValidGUID(str3));

        // Test Case 3:
        String str1
            = "123e4567-h89b-12d3-a456"
              + "-9AC7CBDCEE52";
        System.out.println(
            isValidGUID(str1));

        // Test Case 4:
        String str4
            = "123e4567-h89b-12d3-a456";
        System.out.println(
            isValidGUID(str4));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# GUID (Globally Unique Identifier)
# using regular expression
import re

# Function to validate GUID
# (Globally Unique Identifier)
def isValidGUID(str):

    # Regex to check valid
    # GUID (Globally Unique Identifier)
    regex = "^[{]?[0-9a-fA-F]{8}" + "-([0-9a-fA-F]{4}-)" + "{3}[0-9a-fA-F]{12}[}]?{content}quot;

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
str1 = "123e4567-e89b-12d3" + "-a456-9AC7CBDCEE52"
print(isValidGUID(str1))

# Test Case 2:
str2 = "{123e4567-e89b-12d3-" + "a456-9AC7CBDCEE52}"
print(isValidGUID(str2))

# Test Case 3:
str3 = "123e4567-h89b-12d3-a456" + "-9AC7CBDCEE52"
print(isValidGUID(str3))

# Test Case 4:
str4 = "123e4567-h89b-12d3-a456"
print(isValidGUID(str4))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
true
true
false
false
```