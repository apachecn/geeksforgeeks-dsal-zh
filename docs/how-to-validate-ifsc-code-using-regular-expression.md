# 如何使用正则表达式

验证 IFSC 码

> 原文:[https://www . geesforgeks . org/how-validate-ifsc-code-use-正则表达式/](https://www.geeksforgeeks.org/how-to-validate-ifsc-code-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的 IFSC(印度金融系统)代码。
有效的 IFSC(印度金融系统)代码必须满足以下条件:

1.  它应该有 11 个字符长。
2.  前四个字符应该是大写字母。
3.  第五个字符应为 0。
4.  最后六个字符通常是数字，但也可以是字母。

**示例:**

> **输入:**str = " sbin 0125620 "；
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，这是一个有效的 IFSC(印度金融系统)代码。
> **输入:**str = " SBIN 0125 "；
> **输出:**假
> **说明:**
> 给定字符串有 8 个字符。因此，它不是有效的 IFSC(印度金融系统)代码。
> **输入:**str = " 1234 sbin 012 "；
> **输出:**假
> **解释:**
> 给定字符串不以字母开头。因此，它不是有效的 IFSC(印度金融系统)代码。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案。

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的 IFSC(印度金融系统)代码:

```
regex = "^[A-Z]{4}0[A-Z0-9]{6}{content}quot;;
```

*   其中:
    *   **^** 代表弦的起点。
    *   **【A-Z】{ 4 }**代表前四个字符应为大写字母。
    *   **0** 代表第五个字符应为 0。
    *   **[A-Z0-9]{6}** 代表接下来的六个字符，通常是数字，但也可以是字母。
    *   **$** 代表字符串的结尾。

以下是上述方法的实现:

## C++

```
// C++ program to validate the
// IFSC (Indian Financial System) Code using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the IFSC (Indian Financial System) Code.
bool isValidIFSCode(string str)
{

  // Regex to check valid IFSC (Indian Financial System) Code.
  const regex pattern("^[A-Z]{4}0[A-Z0-9]{6}{content}quot;);

  // If the IFSC (Indian Financial System) Code
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the IFSC (Indian Financial System) Code
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
  string str1 = "SBIN0125620";
  cout << boolalpha << isValidIFSCode(str1) << endl;

  // Test Case 2:
  string str2 = "SBIN0125";
  cout << boolalpha << isValidIFSCode(str2) << endl;

  // Test Case 3:
  string str3 = "1234SBIN012";
  cout << boolalpha << isValidIFSCode(str3) << endl;

  // Test Case 4:
  string str4 = "SBIN7125620";
  cout << boolalpha <<isValidIFSCode(str4) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// IFSC (Indian Financial System) Code
// using regular expression.
import java.util.regex.*;
class GFG {

    // Function to validate
    // IFSC (Indian Financial System) Code
    // using regular expression.
    public static boolean isValidIFSCode(String str)
    {
        // Regex to check valid IFSC Code.
        String regex = "^[A-Z]{4}0[A-Z0-9]{6}{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null) {
            return false;
        }

        // Pattern class contains matcher()
        // method to find matching between
        // the given string and
        // the regular expression.
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "SBIN0125620";
        System.out.println(isValidIFSCode(str1));

        // Test Case 2:
        String str2 = "SBIN0125";
        System.out.println(isValidIFSCode(str2));

        // Test Case 3:
        String str3 = "1234SBIN012";
        System.out.println(isValidIFSCode(str3));

        // Test Case 4:
        String str4 = "SBIN7125620";
        System.out.println(isValidIFSCode(str4));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# IFSC (Indian Financial System) Code 
# using regular expression
import re

# Function to validate
# IFSC (Indian Financial System) Code
# using regular expression.
def  isValidIFSCode(str):

    # Regex to check valid IFSC Code.
    regex = "^[A-Z]{4}0[A-Z0-9]{6}{content}quot;

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
str1 = "SBIN0125620"
print(isValidIFSCode(str1))

# Test Case 2:
str2 = "SBIN0125"
print(isValidIFSCode(str2))

# Test Case 3:
str3 = "1234SBIN012"
print(isValidIFSCode(str3))

# Test Case 4:
str4 = "SBIN7125620"
print(isValidIFSCode(str4))

# This code is contributed by avanitrachhadiya2155
```

**Output**

```
true
false
false
false

```

**使用 String.matches()方法**

这个方法告诉这个字符串是否匹配给定的正则表达式。调用这种形式的方法[字符串匹配(正则表达式)](https://www.geeksforgeeks.org/java-lang-string-matches-java/)会产生与表达式**模式匹配(正则表达式，字符串)完全相同的结果。** Pattern.compile(regex)编译该模式，这样当您执行 matcher . matches()时，模式不会一次又一次地被重新编译。Pattern.compile 预编译它。但是，如果您使用 string.matches，它会在您每次执行该行时编译模式。所以，最好使用 Pattern.compile()。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate
// IFSC (Indian Financial System) Code
// using regular expression.
class GFG {

    // Function to validate
    // IFSC (Indian Financial System) Code
    // using regular expression.
    public static boolean isValidIFSCode(String str)
    {
        // Regex to check valid IFSC Code.
        String regex = "^[A-Z]{4}0[A-Z0-9]{6}{content}quot;;
        return str.trim().matches(regex);
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "SBIN0125620";
        System.out.println(isValidIFSCode(str1));

        // Test Case 2:
        String str2 = "SBIN0125";
        System.out.println(isValidIFSCode(str2));

        // Test Case 3:
        String str3 = "1234SBIN012";
        System.out.println(isValidIFSCode(str3));

        // Test Case 4:
        String str4 = "SBIN7125620";
        System.out.println(isValidIFSCode(str4));
    }
}
```

**Output**

```
true
false
false
false

```