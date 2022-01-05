# 如何使用正则表达式

验证维萨卡号

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证签证卡号/](https://www.geeksforgeeks.org/how-to-validate-visa-card-number-using-regular-expression/)

给定一个字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定的字符串是否为有效的维萨卡号。
有效的维萨卡号码必须满足以下条件:

1.  长度应该是 13 或 16 位，新卡 16 位，旧卡 13 位。
2.  应该是 4 开头。
3.  如果卡片有 13 位数字，接下来的 12 位数字应该是 0-9 之间的任何数字。
4.  如果卡片有 16 位数字，接下来的 15 位数字应该是 0-9 之间的任何数字。
5.  它不应该包含任何字母和特殊字符。

**例:**

> **输入:**str = " 4155279860457 "；
> **输出:**真
> **说明:**给定的字符串满足上述所有条件。因此，这是一个有效的维萨卡号码。
> **输入:**str = " 4155279 "；
> **输出:**为假。
> **说明:**给定字符串有 7 位数字。因此它不是有效的维萨卡号码。
> **输入:**str = " 6155279860457 "；
> T21【输出:假。
> **解释:**给定的字符串不以 4 开头。因此它不是有效的维萨卡号码。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案。

1.  获取字符串。
2.  创建一个正则表达式来检查有效的维萨卡号，如下所述:

```
regex = "^4[0-9]{12}(?:[0-9]{3})?{content}quot;;
```

1.  其中:
    *   **^** 代表弦的起点。
    *   **4** 代表字符串应以 4 开头。
    *   **[0-9]{12}** 代表接下来的十二位数字应该是 0-9 之间的任意数字。
    *   **(** 代表组的开始。
    *   **？**代表 0 或 1 的时间。
    *   **[0-9]{3}** 代表接下来的三个数字应该是 0-9 之间的任意数字。
    *   **)** 代表团体结束。
    *   **？**代表 0 或 1 的时间。
    *   **$** 代表字符串的结尾。
2.  将给定的字符串与正则表达式匹配。
    在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
    在 C++中，这可以通过使用 [regex_match()](https://www.geeksforgeeks.org/regex-regular-expression-in-c/) 来完成。
3.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate
// Visa Card number
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate Visa Card number
bool isValidVisaCardNo(string str)
{

  // Regex to check valid Visa Card number
  const regex pattern("^4[0-9]{12}(?:[0-9]{3})?{content}quot;);

  // If the Visa Card number
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the Visa Card number
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
  string str1 = "4155279860457";
  cout << isValidVisaCardNo(str1) << endl;

  // Test Case 2:
  string str2 = "4155279860457201";
  cout << isValidVisaCardNo(str2) << endl;

  // Test Case 3:
  string str3 = "4155279";
  cout << isValidVisaCardNo(str3) << endl;

  // Test Case 4:
  string str4 = "6155279860457";
  cout << isValidVisaCardNo(str4) << endl;

  // Test Case 5:
  string str5 = "415a27##60457";
  cout << isValidVisaCardNo(str5) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// Visa Card number
// using regular expression
import java.util.regex.*;
class GFG {

    // Function to validate
    // Visa Card number.
    // using regular expression.
    public static boolean
    isValidVisaCardNo(String str)
    {
        // Regex to check valid.
        // Visa Card number
        String regex = "^4[0-9]{12}(?:[0-9]{3})?{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

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
        String str1 = "4155279860457";
        System.out.println(
            isValidVisaCardNo(str1));

        // Test Case 2:
        String str2 = "4155279860457201";
        System.out.println(
            isValidVisaCardNo(str2));

        // Test Case 3:
        String str3 = "4155279";
        System.out.println(
            isValidVisaCardNo(str3));

        // Test Case 4:
        String str4 = "6155279860457";
        System.out.println(
            isValidVisaCardNo(str4));

        // Test Case 5:
        String str5 = "415a27##60457";
        System.out.println(
            isValidVisaCardNo(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate Visa
# Card number using regular expression
import re

# Function to validate Visa Card
# number using regular expression.
def isValidVisaCardNo(string):

    # Regex to check valid Visa
    # Card number
    regex = "^4[0-9]{12}(?:[0-9]{3})?{content}quot;;

    # Compile the ReGex
    p = re.compile(regex);

    # If the string is empty
    # return false
    if (string == ''):
        return False;

    # Pattern class contains matcher()
    # method to find matching between
    # given string and regular expression.
    m = re.match(p, string);

    # Return True if the string
    # matched the ReGex else False
    if m is None:
        return False
    else:
        return True

# Driver code
if __name__ == "__main__":

    # Test Case 1
    str1 = "4155279860457";
    print(isValidVisaCardNo(str1));

    # Test Case 2
    str2 = "4155279860457201";
    print(isValidVisaCardNo(str2));

    # Test Case 3
    str3 = "4155279";
    print(isValidVisaCardNo(str3));

    # Test Case 4
    str4 = "6155279860457";
    print(isValidVisaCardNo(str4));

    # Test Case 5
    str5 = "415a27##60457";
    print(isValidVisaCardNo(str5));

# This code is contributed by AnkitRai01
```

**Output:** 

```
true
true
false
false
false
```