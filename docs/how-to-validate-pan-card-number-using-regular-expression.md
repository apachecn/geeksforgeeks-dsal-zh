# 如何使用正则表达式

验证 PAN 卡号

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证 pan-card-number/](https://www.geeksforgeeks.org/how-to-validate-pan-card-number-using-regular-expression/)

给定由字母数字字符组成的字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查该字符串是否为有效的 **PAN(永久账号)卡**号。
有效的 PAN 卡号必须满足以下条件:

1.  应该有十个字符长。
2.  前五个字符应该是任何大写字母。
3.  接下来的四个字符应该是 0 到 9 之间的任何数字。
4.  最后(第十个)字符应该是任何大写字母。
5.  它不应该包含任何空格。

**示例:**

> **输入:** str = "BNZAA2318J"
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。
> 
> **输入:** str = "23ZAABN18J"
> **输出:**假
> **说明:**
> 给定字符串不以大写字母开头，因此不是有效的 PAN 卡号。
> 
> **输入:** str = "BNZAA2318JM"
> **输出:**假
> **说明:**
> 给定字符串包含 11 个字符，因此不是有效的 PAN 卡号。
> 
> **输入:** str = "BNZAA23184"
> **输出:**真
> **说明:**
> 该字符串的最后(第十)个字符为数字(0-9)字符，因此不是有效的 PAN 卡号。
> 
> **输入:** str = "BNZAA 23184"
> **输出:**真
> **说明:**
> 给定字符串包含空格，因此不是有效的 PAN 卡号。

**方法:**这个问题可以用正则表达式来解决。

*   去拿绳子。
*   如下所述，创建一个正则表达式来验证 PAN 卡号:

```
regex = "[A-Z]{5}[0-9]{4}[A-Z]{1}";
```

*   其中:
    *   **【A-Z】{ 5 }**代表前五个大写字母，可以是 A 到 Z
    *   **[0-9]{4}** 代表可以是 0-9 的四个数字。
    *   **【A-Z】{ 1 }**代表一个大写字母，可以是 A 到 Z
*   用正则表达式匹配给定的字符串，在 Java 中，这可以使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate the
// PAN Card number using Regular Expression

import java.util.regex.*;

class GFG
{

    // Function to validate the PAN Card number.
    public static boolean isValidPanCardNo(String panCardNo)
    {

        // Regex to check valid PAN Card number.
        String regex = "[A-Z]{5}[0-9]{4}[A-Z]{1}";

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the PAN Card number
        // is empty return false
        if (panCardNo == null)
        {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given
        // PAN Card number using regular expression.
        Matcher m = p.matcher(panCardNo);

        // Return if the PAN Card number
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "BNZAA2318J";
        System.out.println(isValidPanCardNo(str1));

        // Test Case 2:
        String str2 = "23ZAABN18J";
        System.out.println(isValidPanCardNo(str2));

        // Test Case 3:
        String str3 = "BNZAA2318JM";
        System.out.println(isValidPanCardNo(str3));

        // Test Case 4:
        String str4 = "BNZAA23184";
        System.out.println(isValidPanCardNo(str4));

        // Test Case 5:
        String str5 = "BNZAA 23184";
        System.out.println(isValidPanCardNo(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate the
# PAN Card number using Regular
# Expression
import re

# Function to validate the
# PAN Card number.

def isValidPanCardNo(panCardNo):

    # Regex to check valid
    # PAN Card number
    regex = "[A-Z]{5}[0-9]{4}[A-Z]{1}"

    # Compile the ReGex
    p = re.compile(regex)

    # If the PAN Card number
    # is empty return false
    if(panCardNo == None):
        return False

    # Return if the PAN Card number
    # matched the ReGex
    if(re.search(p, panCardNo) and
       len(panCardNo) == 10):
        return True
    else:
        return False

# Driver Code.

# Test Case 1:
str1 = "BNZAA2318J"
print(isValidPanCardNo(str1))

# Test Case 2:
str2 = "23ZAABN18J"
print(isValidPanCardNo(str2))

# Test Case 3:
str3 = "BNZAA2318JM"
print(isValidPanCardNo(str3))

# Test Case 4:
str4 = "BNZAA23184"
print(isValidPanCardNo(str4))

# Test Case 5:
str5 = "BNZAA 23184"
print(isValidPanCardNo(str5))

# This code is contributed by avanitrachhadiya2155
```

## C++

```
// C++ program to validate the
// PAN Card number using Regular
//  Expression

#include <iostream>
#include <regex>
using namespace std;

// Function to validate the
// PAN Card number.
bool isValidPanCardNo(string panCardNo)
{

    // Regex to check valid
    // PAN Card number.
    const regex pattern("[A-Z]{5}[0-9]{4}[A-Z]{1}");

    // If the PAN Card number
    // is empty return false
    if (panCardNo.empty()) {
        return false;
    }

    // Return true if the PAN Card number
    // matched the ReGex
    if (regex_match(panCardNo, pattern))
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
    string str1 = "BNZAA2318J";
    cout << isValidPanCardNo(str1) << endl;

    // Test Case 2:
    string str2 = "23ZAABN18J";
    cout << isValidPanCardNo(str2) << endl;

    // Test Case 3:
    string str3 = "BNZAA2318JM";
    cout << isValidPanCardNo(str3) << endl;

    // Test Case 4:
    string str4 = "BNZAA23184";
    cout << isValidPanCardNo(str4) << endl;

    // Test Case 5:
    string str5 = "BNZAA 23184";
    cout << isValidPanCardNo(str5) << endl;

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