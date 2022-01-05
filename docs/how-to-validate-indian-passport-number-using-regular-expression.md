# 如何使用正则表达式

验证印度护照号码

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证印度护照号码/](https://www.geeksforgeeks.org/how-to-validate-indian-passport-number-using-regular-expression/)

给定一个由字母数字字符组成的字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定的字符串是否有效**护照号码**。
印度有效护照号必须满足以下条件:

1.  应该是八个字符长。
2.  第一个字符应该是大写字母。
3.  接下来的两个字符应该是数字，但是第一个字符应该是 1-9 之间的任何数字，第二个字符应该是 0-9 之间的任何数字。
4.  它应该是零或一个空白字符。
5.  接下来的四个字符应该是 0-9 之间的任何数字。
6.  最后一个字符应该是 1-9 之间的任意数字。

**示例:**

> **输入:**str = " a 2096457 "；
> **输出:**真
> **说明:**给定的字符串满足上述所有条件。因此它是印度的有效护照号码。
> 
> **输入:**str = " 12096457 "；
> **输出:**假
> **解释:**给定字符串不以大写字母开头。因此它不是印度的有效护照号码。
> 
> **输入:**str = " a 209645704 "；
> **输出:**假
> **说明:**给定字符串包含 10 个字符。因此它不是印度的有效护照号码。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案。

1.  获取字符串。
2.  如下所述，创建一个正则表达式来检查印度的有效护照号码:

> regex = " ^[a-pr-wya-pr-wy][1-9]\ \ d \ \ s？\ \ d { 4 }[1-9]{内容} # x201 d；；

1.  其中:
    *   **^** 代表弦的起点。
    *   **【A-PR-WYa-PR-wy】**代表字符串应该以 A-Z 开头，不包括 Q、X 和 Z
    *   **【1-9】**代表第二个字符应该是 1-9 之间的任意数字。
    *   **\\d** 代表第三个字符应该是 0-9 之间的任意数字。
    *   **\\s？**表示字符串应该是零或一个空格字符。
    *   **\\d{4}** 代表接下来的四个字符应该是 0-9 之间的任意数字。
    *   **【1-9】**代表最后一个字符应该是 1-9 之间的任意数字。
    *   **$** 代表字符串的结尾。
2.  将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
3.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// passport number of India
// using regular expression

import java.util.regex.*;

class GFG {

    // Function to validate
    // passport number of India
    // using regular expression
    public static boolean isValidPassportNo(String str)
    {
        // Regex to check valid.
        // passport number of India
        String regex = "^[A-PR-WYa-pr-wy][1-9]\\d"
                       + "\\s?\\d{4}[1-9]{content}quot;;

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
        String str1 = "A21 90457";
        System.out.println(isValidPassportNo(str1));

        // Test Case 2:
        String str2 = "A0296457";
        System.out.println(isValidPassportNo(str2));

        // Test Case 3:
        String str3 = "Q2096453";
        System.out.println(isValidPassportNo(str3));

        // Test Case 4:
        String str4 = "12096457";
        System.out.println(isValidPassportNo(str4));

        // Test Case 5:
        String str5 = "A209645704";
        System.out.println(isValidPassportNo(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate passport
# number of India using regular expression
import re

# Function to validate the pin code
# of India.

def isValidPassportNo(string):

    # Regex to check valid pin code
    # of India.
    regex = "^[A-PR-WYa-pr-wy][1-9]\\d" +\
            "\\s?\\d{4}[1-9]{content}quot;

    # Compile the ReGex
    p = re.compile(regex)

    # If the string is empty
    # return false
    if (string == ''):
        return False

    # Pattern class contains matcher()
    # method to find matching between
    # given string and regular expression.
    m = re.match(p, string)

    # Return True if the string
    # matched the ReGex else False
    if m is None:
        return False
    else:
        return True

# Driver code.
if __name__ == "__main__":

    # Test Case 1
    str1 = "A21 90457"
    print(isValidPassportNo(str1))

    # Test Case 2:
    str2 = "A0296457"
    print(isValidPassportNo(str2))

    # Test Case 3:
    str3 = "Q2096453"
    print(isValidPassportNo(str3))

    # Test Case 4:
    str4 = "12096457"
    print(isValidPassportNo(str4))

    # Test Case 5:
    str5 = "A209645704"
    print(isValidPassportNo(str5))

# This code is contributed by AnkitRai01
```

## C++

```
// C++ program to validate the
// passport number
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the passport number
bool isValidPassportNo(string str)
{

    // Regex to check valid passport number
    const regex pattern(
        "^[A-PR-WYa-pr-wy][1-9]"
         "\\d\\s?\\d{4}[1-9]{content}quot;);

    // If the passport number
    // is empty return false
    if (str.empty()) {
        return false;
    }

    // Return true if the passport number
    // matched the ReGex
    if (regex_match(str, pattern)) {
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
    string str1 = "A21 90457";
    cout << isValidPassportNo(str1) << endl;

    // Test Case 2:
    string str2 = "A0296457";
    cout << isValidPassportNo(str2) << endl;

    // Test Case 3:
    string str3 = "Q2096453";
    cout << isValidPassportNo(str3) << endl;

    // Test Case 4:
    string str4 = "12096457";
    cout << isValidPassportNo(str4) << endl;

    // Test Case 5:
    string str5 = "A209645704";
    cout << isValidPassportNo(str5) << endl;

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
false

```