# 如何使用正则表达式

验证域名

> 原文:[https://www . geesforgeks . org/如何使用正则表达式验证域名/](https://www.geeksforgeeks.org/how-to-validate-a-domain-name-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效域名。
有效域名必须满足以下条件:

1.  域名应该是 a-z 或 A-Z 或 0-9 和连字符(-)。
2.  域名长度应该在 1 到 63 个字符之间。
3.  域名不能以连字符(-)开头或结尾(例如-geeksforgeeks.org 或 geeksforgeeks.org-)。
4.  最后一个 TLD(顶级域)必须至少包含两个字符，最多包含 6 个字符。
5.  域名可以是一个子域(例如 contribute . geeksforgeks . org)。

**示例:**

> **输入:**str = " contribute . geeksforgeeks . org "
> **输出:**真
> **说明:**
> 给定的字符串满足上述所有条件。因此，它是一个有效的域名。
> **输入:**str = "-geeksforgeeks . org "
> **输出:** false
> **解释:**
> 给定字符串以连字符(-)开头。因此，它不是有效的域名。
> **输入:**str = " geeksforgeeks . o "
> **输出:** false
> **解释:**
> 给定字符串的最后一个 TLD 长度为 1 个字符，最后一个 TLD 长度必须在 2 到 6 个字符之间。因此，它不是有效的域名。
> **输入:** str =。org"
> **输出:**假
> **解释:**
> 给定字符串不以 a-z 或 A-Z 或 0-9 开头。因此，它不是有效的域名。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算答案:

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效域名:

> regex = "^(？！-[a-za-z0-9-]{ 1.63 }(？

*   其中:
    *   **^** 代表弦的起点。
    *   **(** 代表组的开始。
    *   **(？！-)** 表示字符串不应以连字符(-)开头。
    *   **[a-za-z0-9-]{1，63}** 代表域名长度应为 a-z 或 A-Z 或 0-9 和 1 到 63 个字符之间的连字符(-)。
    *   **(？<！-)** 表示字符串不应该以连字符(-)结尾。
    *   **\\。**表示后跟点的字符串。
    *   **)+** 代表该组的结束，该组至少要出现 1 次，但对于子域允许出现多次。
    *   **【a-za-Z】{ 2，6}** 代表 TLD 必须是 2 到 6 个字符长的 A-Z 或 A-Z。
    *   **$** 代表字符串的结尾。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
*   如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate the
// domain name using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the domain name.
bool isValidDomain(string str)
{

  // Regex to check valid domain name.
  const regex pattern("^(?!-)[A-Za-z0-9-]+([\\-\\.]{1}[a-z0-9]+)*\\.[A-Za-z]{2,6}{content}quot;);

  // If the domain name
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the domain name
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
  string str1 = "geeksforgeeks.org";
  cout << isValidDomain(str1) << endl;

  // Test Case 2:
  string str2 = "contribute.geeksforgeeks.org";
  cout << isValidDomain(str2) << endl;

  // Test Case 3:
  string str3 = "-geeksforgeeks.org";
  cout << isValidDomain(str3) << endl;

  // Test Case 4:
  string str4 = "geeksforgeeks.o";
  cout << isValidDomain(str4) << endl;

  // Test Case 5:
  string str5 = ".org";
  cout << isValidDomain(str5) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate domain name.
// using regular expression.

import java.util.regex.*;
class GFG {

    // Function to validate domain name.
    public static boolean isValidDomain(String str)
    {
        // Regex to check valid domain name.
        String regex = "^((?!-)[A-Za-z0-9-]"
                       + "{1,63}(?<!-)\\.)"
                       + "+[A-Za-z]{2,6}";

        // Compile the ReGex
        Pattern p
            = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null) {
            return false;
        }

        // Pattern class contains matcher()
        // method to find the matching
        // between the given string and
        // regular expression.
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver Code
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "geeksforgeeks.org";
        System.out.println(isValidDomain(str1));

        // Test Case 2:
        String str2 = "contribute.geeksforgeeks.org";
        System.out.println(isValidDomain(str2));

        // Test Case 3:
        String str3 = "-geeksforgeeks.org";
        System.out.println(isValidDomain(str3));

        // Test Case 4:
        String str4 = "geeksforgeeks.o";
        System.out.println(isValidDomain(str4));

        // Test Case 5:
        String str5 = ".org";
        System.out.println(isValidDomain(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# domain name
# using regular expression
import re

# Function to validate
# domain name.
def isValidDomain(str):

    # Regex to check valid
    # domain name. 
    regex = "^((?!-)[A-Za-z0-9-]" +
            "{1,63}(?<!-)\\.)" +
            "+[A-Za-z]{2,6}"

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
str1 = "geeksforgeeks.org"
print(isValidDomain(str1))

# Test Case 2:
str2 = "contribute.geeksforgeeks.org"
print(isValidDomain(str2))

# Test Case 3:
str3 = "-geeksforgeeks.org"
print(isValidDomain(str3))

# Test Case 4:
str4 = "geeksforgeeks.o"
print(isValidDomain(str4))

# Test Case 5:
str5 = ".org"
print(isValidDomain(str5))

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