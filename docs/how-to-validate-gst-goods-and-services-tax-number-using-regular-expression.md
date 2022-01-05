# 如何使用正则表达式

验证商品及服务税号

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证商品及服务税号/](https://www.geeksforgeeks.org/how-to-validate-gst-goods-and-services-tax-number-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的商品及服务税(GST)号。
有效的商品及服务税号码必须满足以下条件:

1.  它应该有 15 个字符长。
2.  前 2 个字符应该是一个数字。
3.  接下来的 10 个字符应该是纳税人的 PAN 号。
4.  第 13 个字符(实体代码)应该是 1-9 之间的数字或字母表。
5.  第 14 个字符应该是 z。
6.  第 15 个字符应该是字母或数字。

**示例:**

> **输入:**str = " 06bzahm6385 p6z 2 "；
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，这是一个有效的商品及服务税号码。
> 
> **输入:**str = " 06bzaf 67 "；
> **输出:**假
> **说明:**
> 给定字符串长度不超过 15 个字符。因此，它不是有效的商品及服务税号码。
> 
> **输入:**str = " azbzahm6385 p6z 2 "；
> **输出:**假
> **解释:**
> 给定字符串以字母开头。因此，它不是有效的商品及服务税号码。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)的概念来解决这个问题。可以按照以下步骤计算答案:

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的商品及服务税号:

> regex = " ^[0-9]{2}[a-z]{5}[0-9]{4}[a-z]{1}[1-9a-z]{1}z[0-9a-z]{1}{content}#x201d；；

*   其中:
    *   **^** 代表弦的起点。
    *   **[0-9]{2}** 代表前两个字符应该是数字。
    *   **[A-Z]{5}** 代表接下来的五个字符应该是任意大写字母。
    *   **[0-9]{4}** 代表接下来的四个字符应该是任意数字。
    *   **[A-Z]{1}** 代表下一个字符应该是任意大写字母。
    *   **[1-9A-Z]{1}** 代表第 13 个字符应该是 1-9 之间的数字或字母表。
    *   **Z** 代表第 14 个字符应该是 Z。
    *   **[0-9A-Z]{1}** 代表第 15 个字符应该是字母或数字。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate the
// GST (Goods and Services Tax) number
// using regular expression.

import java.util.regex.*;

class GFG {

    // Function to validate
    // GST (Goods and Services Tax) number.
    public static boolean isValidGSTNo(String str)
    {
        // Regex to check valid
        // GST (Goods and Services Tax) number
        String regex = "^[0-9]{2}[A-Z]{5}[0-9]{4}"
                       + "[A-Z]{1}[1-9A-Z]{1}"
                       + "Z[0-9A-Z]{1}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null)
        {
            return false;
        }

        // Pattern class contains matcher()
        // method to find the matching
        // between the given string
        // and the regular expression.
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "06BZAHM6385P6Z2";
        System.out.println(isValidGSTNo(str1));

        // Test Case 2:
        String str2 = "06BZAF67";
        System.out.println(isValidGSTNo(str2));

        // Test Case 3:
        String str3 = "AZBZAHM6385P6Z2";
        System.out.println(isValidGSTNo(str3));

        // Test Case 4:
        String str4 = "06BZ63AHM85P6Z2";
        System.out.println(isValidGSTNo(str4));

        // Test Case 5:
        String str5 = "06BZAHM6385P6F2";
        System.out.println(isValidGSTNo(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# GST (Goods and Services Tax) number 
# using regular expression
import re

# Function to validate GST
# (Goods and Services Tax) number.
def isValidMasterCardNo(str):

    # Regex to check valid
    # GST (Goods and Services Tax) number
    regex = "^[0-9]{2}[A-Z]{5}[0-9]{4}" +
            "[A-Z]{1}[1-9A-Z]{1}" +
            "Z[0-9A-Z]{1}{content}quot;

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
str1 = "06BZAHM6385P6Z2"
print(isValidMasterCardNo(str1))

# Test Case 2:
str2 = "06BZAF67"
print(isValidMasterCardNo(str2))

# Test Case 3:
str3 = "AZBZAHM6385P6Z2"
print(isValidMasterCardNo(str3))

# Test Case 4:
str4 = "06BZ63AHM85P6Z2"
print(isValidMasterCardNo(str4))

# Test Case 5:
str5 = "06BZAHM6385P6F2"
print(isValidMasterCardNo(str5))

# This code is contributed by avanitrachhadiya2155
```

## C++

```
// C++ program to validate the
// GST (Goods and Services Tax) number
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the GST
// (Goods and Services Tax) number
bool isValidGSTNo(string str)
{

    // Regex to check valid GST
    // (Goods and Services Tax) number
    const regex pattern("^[0-9]{2}[A-Z]{5}"
                        "[0-9]{4}[A-Z]{1}["
                        "1-9A-Z]{1}Z[0-9A-Z]{1}{content}quot;);

    // If the GST (Goods and Services Tax)
    // number is empty return false
    if (str.empty())
    {
        return false;
    }

    // Return true if the GST number
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
    string str1 = "06BZAHM6385P6Z2";
    cout << isValidGSTNo(str1) << endl;

    // Test Case 2:
    string str2 = "06BZAF67";
    cout << isValidGSTNo(str2) << endl;

    // Test Case 3:
    string str3 = "AZBZAHM6385P6Z2";
    cout << isValidGSTNo(str3) << endl;

    // Test Case 4:
    string str4 = "06BZ63AHM85P6Z2";
    cout << isValidGSTNo(str4) << endl;

    // Test Case 5:
    string str5 = "06BZAHM6385P6F2";
    cout << isValidGSTNo(str5) << endl;

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