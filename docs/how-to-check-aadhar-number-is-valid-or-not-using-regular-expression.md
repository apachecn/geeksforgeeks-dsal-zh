# 如何使用正则表达式

检查 Aadhar 数是否有效

> 原文:[https://www . geesforgeks . org/how-check-aad har-number-is-valid-or-not-use-正则表达式/](https://www.geeksforgeeks.org/how-to-check-aadhar-number-is-valid-or-not-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的 Aadhar 数。有效的 Aadhar 号码必须满足以下条件:

1.  它应该有 12 位数字。
2.  它不应该以 0 和 1 开头。
3.  它不应该包含任何字母和特殊字符。
4.  每 4 位数字后应该有空格。

**示例:**

> **输入:** str = "3675 9834 6012"
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，它是一个有效的 Aadhar 数。
> **输入:**str = " 3675 9834 6012 8 "
> **输出:**假
> **说明:**
> 给定字符串包含 13 位数字。因此，它不是有效的 Aadhar 数。

**做法:**思路是用正则表达式来解决这个问题。可以按照以下步骤计算答案:

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的 Aadhar 数:

> regex = " ^[2-9]{1}[0-9]{3}\\s[0-9]{4}\\s[0-9]{4}{content}#x201d；；

*   其中:
    *   **^** 代表弦的起点。
    *   **[2-9]{1}** 代表第一个数字应该是 2-9 中的任意一个。
    *   **[0-9]{3}** 代表第一个数字之后的下 3 个数字，应该是 0-9 之间的任意数字。
    *   **\\s** 代表空格。
    *   **[0-9]{4}** 代表接下来的 4 位数字应该是 0-9 之间的任意数字。
    *   **\\s** 代表空格。
    *   **[0-9]{4}** 代表接下来的 4 位数字应该是 0-9 之间的任意数字。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate the
// Aadhar number using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the Aadhar number.
bool isValidAadharNumber(string str)
{

  // Regex to check valid Aadhar number.
  const regex pattern("^[2-9]{1}[0-9]{3}\\s[0-9]{4}\\s[0-9]{4}{content}quot;);

  // If the Aadhar number
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the Aadhar number
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
  string str1 = "3675 9834 6015";
  cout << isValidAadharNumber(str1) << endl;

  // Test Case 2:
  string str2 = "4675 9834 6012 8";
  cout << isValidAadharNumber(str2) << endl;

  // Test Case 3:
  string str3 = "0175 9834 6012";
  cout << isValidAadharNumber(str3) << endl;

  // Test Case 4:
  string str4 = "3675 98AF 60#2";
  cout << isValidAadharNumber(str4) << endl;

  // Test Case 5:
  string str5 = "417598346012";
  cout << isValidAadharNumber(str5) << endl;
  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check valid
// Aadhar number using regex.

import java.util.regex.*;
class GFG {

    // Function to validate Aadhar number.
    public static boolean
    isValidAadharNumber(String str)
    {
        // Regex to check valid Aadhar number.
        String regex
            = "^[2-9]{1}[0-9]{3}\\s[0-9]{4}\\s[0-9]{4}{content}quot;;

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
        String str1 = "3675 9834 6015";
        System.out.println(isValidAadharNumber(str1));

        // Test Case 2:
        String str2 = "4675 9834 6012 8";
        System.out.println(isValidAadharNumber(str2));

        // Test Case 3:
        String str3 = "0175 9834 6012";
        System.out.println(isValidAadharNumber(str3));

        // Test Case 4:
        String str4 = "3675 98AF 60#2";
        System.out.println(isValidAadharNumber(str4));

        // Test Case 5:
        String str5 = "417598346012";
        System.out.println(isValidAadharNumber(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# Aadhar number using regex.
import re

# Function to validate Aadhar
# number.
def isValidAadharNumber(str):

    # Regex to check valid
    # Aadhar number.
    regex = ("^[2-9]{1}[0-9]{3}\\" +
             "s[0-9]{4}\\s[0-9]{4}{content}quot;)

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
str1 = "3675 9834 6015"
print(isValidAadharNumber(str1))

# Test Case 2:
str2 = "4675 9834 6012 8"
print(isValidAadharNumber(str2))

# Test Case 3:
str3 = "0175 9834 6012"
print(isValidAadharNumber(str3))

# Test Case 4:
str4 = "3675 98AF 60#2"
print(isValidAadharNumber(str4))

# Test Case 5:
str5 = "417598346012"
print(isValidAadharNumber(str5))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
true
false
false
false
false
```