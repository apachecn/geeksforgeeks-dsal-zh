# 如何使用正则表达式

验证 CVV 数

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证-cvv-number/](https://www.geeksforgeeks.org/how-to-validate-cvv-number-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查是否为有效的 CVV(卡验证值)号。
有效的 CVV(卡验证值)号码必须满足以下条件:

1.  它应该有 3 或 4 个数字。
2.  它应该有一个 0-9 之间的数字。
3.  它不应该有任何字母和特殊字符。

**示例:**

> **输入:** str = "561"
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，这是一个有效的 CVV(卡验证值)号码。
> 
> **输入:** str = "50614"
> **输出:**假
> **说明:**
> 给定的字符串有五位数。因此，它不是有效的 CVV(卡验证值)号码。
> 
> **输入:** str = "5a#1"
> **输出:**假
> **说明:**给定字符串有字母和特殊字符。因此，它不是有效的 CVV(卡验证值)号码。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案。

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的 CVV(卡验证值)号码:

```
regex = "^[0-9]{3, 4}{content}quot;;
```

*   其中:
    *   **^** 代表弦的起点。
    *   **【0-9】**代表 0-9 之间的数字。
    *   **{3，4}** 代表字符串有 3 或 4 位数字。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// CVV (Card Verification Value)
// number using regex.
import java.util.regex.*;
class GFG {

    // Function to validate
    // CVV (Card Verification Value) number.
    // using regular expression.
    public static boolean isValidCVVNumber(String str)
    {
        // Regex to check valid CVV number.
        String regex = "^[0-9]{3,4}{content}quot;;

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
        String str1 = "561";
        System.out.println(isValidCVVNumber(str1));

        // Test Case 2:
        String str2 = "5061";
        System.out.println(isValidCVVNumber(str2));

        // Test Case 3:
        String str3 = "50614";
        System.out.println(isValidCVVNumber(str3));

        // Test Case 4:
        String str4 = "5a#1";
        System.out.println(isValidCVVNumber(str4));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# CVV (Card Verification Value)
# number using regex.
import re

# Function to validate
# CVV (Card Verification Value) number.
# using regular expression.

def isValidCVVNumber(str):

    # Regex to check valid
    # CVV number.
    regex = "^[0-9]{3,4}{content}quot;

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

# Driver code

# Test Case 1:
str1 = "561"
print(isValidCVVNumber(str1))

# Test Case 2:
str2 = "5061"
print(isValidCVVNumber(str2))

# Test Case 3:
str3 = "50614"
print(isValidCVVNumber(str3))

# Test Case 4:
str4 = "5a#1"
print(isValidCVVNumber(str4))

# This code is contributed by avanitrachhadiya2155
```

## C++

```
// C++ program to validate the
// CVV (Card Verification Value) number
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the CVV
// (Card Verification Value) number
bool isValidCVVNumber(string str)
{

    // Regex to check valid CVV
    // (Card Verification Value) number
    const regex pattern("^[0-9]{3,4}{content}quot;);

    // If the CVV (Card Verification Value)
    //  number is empty return false
    if (str.empty())
    {
        return false;
    }

    // Return true if the CVV
    // (Card Verification Value) number
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
    string str1 = "561";
    cout << isValidCVVNumber(str1) << endl;

    // Test Case 2:
    string str2 = "5061";
    cout << isValidCVVNumber(str2) << endl;

    // Test Case 3:
    string str3 = "50614";
    cout << isValidCVVNumber(str3) << endl;

    // Test Case 4:
    string str4 = "5a#1";
    cout << isValidCVVNumber(str4) << endl;

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