# 如何使用正则表达式

验证 SSN(社保号)

> 原文:[https://www . geesforgeks . org/how-validate-SSN-social-security-number-use-正则表达式/](https://www.geeksforgeeks.org/how-to-validate-ssn-social-security-number-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否有效 **SSN(社保号)**。
有效的 SSN(社会安全号码)必须满足以下条件:

1.  应该有 9 位数。
2.  它应该用连字符(-)分成 3 部分。
3.  第一部分应该有 3 个数字，不应该是 000、666 或 900 到 999 之间。
4.  第二部分应该有 2 位数字，应该从 01 到 99。
5.  第三部分应该有 4 位数字，应该是从 0001 到 9999。

**示例:**

> **输入:**str = " 856-45-6789 "；
> **输出:**真
> **说明:**给定的字符串满足上述所有条件。因此，这是一个有效的 SSN(社会安全号码)。
> 
> **输入:**str = " 000-45-6789 "；
> **输出:**假
> **说明:**给定字符串以 000 开头。因此，它不是有效的 SSN(社会安全号码)。
> 
> **输入:**str = " 856-452-6789 "；
> **输出:**假
> **说明:**这个字符串的第二部分有 3 位数字。因此，它不是有效的 SSN(社会安全号码)。
> 
> **输入:**str = " 856-45-0000 "；
> **输出:**假
> **说明:**此串第三部分为 0000。因此，它不是有效的 SSN(社会安全号码)。

**做法:**思路是用正则表达式来解决这个问题。可以按照以下步骤计算答案。

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的 SSN(社会安全号码):

```
regex = "^(?!666|000|9\\d{2})\\d{3}-(?!00)\\d{2}-(?!0{4})\\d{4}{content}quot;;
```

*   其中:
    *   **^** 代表弦的起点。
    *   **(？！666|000|9\\d{2})\\d{3}** 表示前 3 位不应以 000、666 或 900 到 999 开头。
    *   **–**表示后跟连字符(-)的字符串。
    *   **(？！00)\\d{2}** 表示接下来的 2 位数字不应该以 00 开头，它应该是 01-99 之间的任何数字。
    *   **–**表示后跟连字符(-)的字符串。
    *   **(？！0{4})\\d{4}** 表示后面 4 位数字不能是 0000，应该是 0001-9999 之间的任意数字。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check valid
// SSN (Social Security Number) using
// regex.
import java.util.regex.*;
class GFG {

    // Function to validate
    // SSN (Social Security Number).
    public static boolean isValidSSN(String str)
    {
        // Regex to check SSN
        // (Social Security Number).
        String regex = "^(?!666|000|9\\d{2})\\d{3}"
                       + "-(?!00)\\d{2}-"
                       +"(?!0{4})\\d{4}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null)
        {
            return false;
        }

        // Pattern class contains matcher()
        //  method to find matching between
        //  given string and regular expression.
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "856-45-6789";
        ;
        System.out.println(isValidSSN(str1));

        // Test Case 2:
        String str2 = "000-45-6789";
        ;
        System.out.println(isValidSSN(str2));

        // Test Case 3:
        String str3 = "856-452-6789";
        System.out.println(isValidSSN(str3));

        // Test Case 4:
        String str4 = "856-45-0000";
        System.out.println(isValidSSN(str4));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# SSN (Social Security Number)
# using regular expression
import re

# Function to validate SSN
# (Social Security Number).

def isValidSSN(str):

    # Regex to check valid
    # SSN (Social Security Number).
    regex = "^(?!666|000|9\\d{2})\\d{3}-(?!00)\\d{2}-(?!0{4})\\d{4}{content}quot;

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
str1 = "856-45-6789"
print(isValidSSN(str1))

# Test Case 2:
str2 = "000-45-6789"
print(isValidSSN(str2))

# Test Case 3:
str3 = "856-452-6789"
print(isValidSSN(str3))

# Test Case 4:
str4 = "856-45-0000"
print(isValidSSN(str4))

# This code is contributed by avanitrachhadiya2155
```

## C++

```
// C++ program to validate the
// SSN (Social Security Number)
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the SSN
// (Social Security Number)
bool isValidSSN(string str)
{

    // Regex to check valid SSN
    // (Social Security Number)
    const regex pattern("^(?!666|000|9\\d{2})"
                        "\\d{3}-(?!00)"
                        "\\d{2}-(?!0{4})\\d{4}{content}quot;);

    // If the SSN (Social Security Number)
    // is empty return false
    if (str.empty())
    {
        return false;
    }

    // Return true if the SSN
    // (Social Security Number)
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
    string str1 = "856-45-6789";
    cout << isValidSSN(str1) << endl;

    // Test Case 2:
    string str2 = "000-45-6789";
    cout << isValidSSN(str2) << endl;

    // Test Case 3:
    string str3 = "856-452-6789";
    cout << isValidSSN(str3) << endl;

    // Test Case 4:
    string str4 = "856-45-0000";
    cout << isValidSSN(str4) << endl;

    return 0;
}

// This code is contributed by yuvraj_chandra
```

**Output**

```
true
false
false
false

```