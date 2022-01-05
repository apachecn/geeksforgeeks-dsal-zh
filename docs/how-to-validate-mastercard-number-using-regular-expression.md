# 如何使用正则表达式

验证万事达卡号

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证万事达卡号码/](https://www.geeksforgeeks.org/how-to-validate-mastercard-number-using-regular-expression/)

给定字符串**字符串**，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的主卡号。
有效的主卡号必须满足以下条件。

1.  它应该有 16 位数长。
2.  它应该以两位数开始，可以是 51 到 55，也可以是 2221 到 2720。
3.  在 51 到 55 的情况下，接下来的 14 位数字应该是 0-9 之间的任何数字。
4.  在 2221 到 2720 的情况下，接下来的 12 位数字应该是 0-9 之间的任何数字。
5.  它不应该包含任何字母和特殊字符。

**示例:**

> **输入:**str = " 5114496353984312 "；
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，它是一个有效的主卡号。
> **输入:**str = " 5582822410 "；
> **输出:**假
> **说明:**
> 给定字符串有 10 位数字。因此，它不是有效的主卡号。
> **输入:**str = " 6082822463100051 "；
> **输出:**假
> **解释:**
> 给定的字符串不是以两位数开始，可能是 51 到 55，也可能是 4 位数，可能是 2221 到 2720。因此，它不是有效的主卡号。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案。

*   获取字符串。
*   创建一个正则表达式来检查有效的主卡号，如下所述:

> regex = " ^5[1-5][0-9]{14}|^(222[1-9]|22[3-9]\\d|2[3-6]\\d{2}|27[0-1]\\d|2720)[0-9]{12}{content}#x201d；；

*   其中:
    *   **^** 代表弦的起点。
    *   **5[1-5]** 代表第一个两位数，范围从 51 到 55。
    *   **[0-9]{14}** 代表接下来的十四位数字应该是 0-9 之间的任意数字。
    *   **|** 代表或。
    *   **(** 代表组的开始。
    *   **222[1-9]** 代表第一个四位数，范围从 2221 到 2229。
    *   **|** 代表或。
    *   **22[3-9]\\d** 代表第一个四位数，范围从 2230 到 2299。
    *   **|** 代表或。
    *   **2[3-6]\\d{2}** 表示第一个四位数，范围从 2300 到 2699。
    *   **|** 代表或。
    *   **27[0-1]\\d** 代表第一个四位数，范围从 2700 到 2719。
    *   **|** 代表或。
    *   **2720** 代表第一个四位数可能以 2720 开始。
    *   **)** 代表团体结束。
    *   **[0-9]{12}** 代表接下来的十二位数字应该是 0-9 之间的任意数字。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。
    在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/)
    来实现；在 C++中，这可以通过使用 [regex_match()](https://www.geeksforgeeks.org/regex-regular-expression-in-c/) 来实现
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate
// Master Card number
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate Master Card number
bool isValidMasterCardNo(string str)
{

  // Regex to check valid Master Card number
  const regex pattern("^5[1-5][0-9]{14}|^(222[1-9]|22[3-9]\\d|2[3-6]\\d{2}|27[0-1]\\d|2720)[0-9]{12}{content}quot;);

  // If the Master Card number
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the Master Card number
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
  string str1 = "5114496353984312";
  cout << isValidMasterCardNo(str1) << endl;

  // Test Case 2:
  string str2 = "2720822463109651";
  cout << isValidMasterCardNo(str2) << endl;

  // Test Case 3:
  string str3 = "5582822410";
  cout << isValidMasterCardNo(str3) << endl;

  // Test Case 4:
  string str4 = "6082822463100051";
  cout << isValidMasterCardNo(str4) << endl;

  // Test Case 5:
  string str5 = "2221149a635##843";
  cout << isValidMasterCardNo(str5) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// Master Card number
// using regular expression

import java.util.regex.*;
class GFG {

    // Function to validate
    // Master Card number
    // using regular expression.
    public static boolean
    isValidMasterCardNo(String str)
    {

        // Regex to check valid
        // Master Card number.
        String regex = "^5[1-5][0-9]{14}|"
                       + "^(222[1-9]|22[3-9]\\d|"
                       + "2[3-6]\\d{2}|27[0-1]\\d|"
                       + "2720)[0-9]{12}{content}quot;;

        // Compile the ReGex
        Pattern p
            = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null) {
            return false;
        }

        // Find match between given string
        // and regular expression
        // using Pattern.matcher()
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver code
    public static void main(String args[])
    {
        // Test Case 1:
        String str1 = "5114496353984312";
        System.out.println(
            isValidMasterCardNo(str1));

        // Test Case 2:
        String str2 = "2720822463109651";
        System.out.println(
            isValidMasterCardNo(str2));

        // Test Case 3:
        String str3 = "5582822410";
        System.out.println(
            isValidMasterCardNo(str3));

        // Test Case 4:
        String str4 = "6082822463100051";
        System.out.println(
            isValidMasterCardNo(str4));

        // Test Case 5:
        String str5 = "2221149a635##843";
        System.out.println(
            isValidMasterCardNo(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# Master Card number
# using regular expression
import re

# Function to validate
# Master Card number
# using regular expression.
def isValidMasterCardNo(str):

    # Regex to check valid
    # Master Card number.
    regex = "^5[1-5][0-9]{14}|" +
            "^(222[1-9]|22[3-9]\\d|" +
            "2[3-6]\\d{2}|27[0-1]\\d|" +
            "2720)[0-9]{12}{content}quot;

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
str1 = "5114496353984312"
print(isValidMasterCardNo(str1))

# Test Case 2:
str2 = "2720822463109651"
print(isValidMasterCardNo(str2))

# Test Case 3:
str3 = "5582822410"
print(isValidMasterCardNo(str3))

# Test Case 4:
str4 = "6082822463100051"
print(isValidMasterCardNo(str4))

# Test Case 5:
str5 = "2221149a635##843"
print(isValidMasterCardNo(str5))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
true
true
false
false
false
```