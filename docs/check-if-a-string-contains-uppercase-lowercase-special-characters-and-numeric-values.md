# 检查字符串是否包含大写、小写、特殊字符和数值

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-大写-小写-特殊字符-数字-值/](https://www.geeksforgeeks.org/check-if-a-string-contains-uppercase-lowercase-special-characters-and-numeric-values/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是检查给定的字符串是否包含大写字母、小写字母、特殊字符和数值。如果字符串包含全部，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**str = " # geeksforgeecks 123 @ "
> **输出:**是
> **解释:**
> 给定字符串包含大写字符(' G '，' F ')、小写字符(' e '，' k '，' s '，' o '，' r ')、特殊字符(' # '，' @ ')和数值(' 1 '，' 2 '，' 3 ')。因此，输出为是。
> 
> **输入:** str = "GeeksForGeeks"
> **输出:**否
> **说明:**
> 给定字符串只包含大写字符和小写字符。因此，输出为否。

**天真方法:**最简单的方法是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，检查给定的字符串是否包含大写、小写、数字和特殊字符。以下是步骤:

1.  从头到尾逐字符遍历字符串。
2.  检查每个字符的 ASCII 值是否符合以下条件:
    *   如果 ASCII 值在**【65，90】**范围内，则为大写字母。
    *   如果 ASCII 值在**【97，122】**范围内，则为小写字母。
    *   如果 ASCII 值在**【48，57】**的范围内，那么它就是一个数字。
    *   如果 ASCII 值位于范围**【32，47】**、**【58，64】**、**【91，96】**或**【123，126】**内，则它是一个特殊字符
3.  如果字符串包含以上所有内容，打印**是**。否则，打印**否**。

***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**正则表达式方法:**的思路是以一个[正则表达式的概念](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。以下是步骤:

*   创建一个[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来检查给定的字符串是否包含大写、小写、特殊字符和数值，如下所述:

> regex = "^(？=.*[a-z])(？=.*[A-Z])(？=.*\\d)" +"(？=.*[-+_!@#$%^&*., ?]).+{ content } # x201；
> 在哪里，
> 
> *   **^** 代表弦的起点。
> *   **(？=.*[a-z])** 代表至少一个小写字符。
> *   **(？=.*[A-Z])** 代表至少一个大写字符。
> *   **(？=.*\\d)** 至少代表一个数值。
> *   **(？=.*[-+_!@#$%^ & *。, ?])** 代表至少一个特殊字符。
> *   **。**表示除换行符以外的任何字符。
> *   **+** 代表一次或多次。

*   使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 将给定字符串与正则表达式匹配。
*   如果字符串与给定的正则表达式匹配，则打印**是**。否则，打印**否**。

以下是上述方法的实现:

## C++

```
// C++ program to check if the string
// contains uppercase, lowercase
// special character & numeric value
#include <iostream>
#include <regex>
using namespace std;
void isAllPresent(string str)
{

  // Regex to check if a string
  // contains uppercase, lowercase
  // special character & numeric value
  const regex pattern("^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[-+_!@#$%^&*.,?]).+{content}quot;);

  // If the string is empty
  // then print No
  if (str.empty())
  {
    cout<<"No"<<endl;
    return ;
  }

  // Print Yes If the string matches
  // with the Regex
  if(regex_match(str, pattern))
  {
    cout << "Yes" << endl;
  }
  else
  {
    cout << "No" << endl;
  }
  return;
}

// Driver Code
int main()
{
  string str = "#GeeksForGeeks123@";
  isAllPresent(str);
  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.regex.*;

class GFG {

    // Function that checks if a string
    // contains uppercase, lowercase
    // special character & numeric value
    public static void
    isAllPresent(String str)
    {
        // ReGex to check if a string
        // contains uppercase, lowercase
        // special character & numeric value
        String regex = "^(?=.*[a-z])(?=."
                       + "*[A-Z])(?=.*\\d)"
                       + "(?=.*[-+_!@#$%^&*., ?]).+{content}quot;;

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // then print No
        if (str == null) {
            System.out.println("No");
            return;
        }

        // Find match between given string
        // & regular expression
        Matcher m = p.matcher(str);

        // Print Yes if string
        // matches ReGex
        if (m.matches())
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given string
        String str = "#GeeksForGeeks123@";

        // Function Call
        isAllPresent(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import re

# Function that checks if a string
# contains uppercase, lowercase
# special character & numeric value
def isAllPresent(str):

    # ReGex to check if a string
    # contains uppercase, lowercase
    # special character & numeric value
    regex = ("^(?=.*[a-z])(?=." +
             "*[A-Z])(?=.*\\d)" +
             "(?=.*[-+_!@#$%^&*., ?]).+{content}quot;)

    # Compile the ReGex
    p = re.compile(regex)

    # If the string is empty
    # return false
    if (str == None):
        print("No")
        return

    # Print Yes if string
    # matches ReGex
    if(re.search(p, str)):
        print("Yes")
    else:
        print("No")

# Driver code

# Given string
str = "#GeeksForGeeks123@"

#Function Call
isAllPresent(str)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Text.RegularExpressions;

class GFG {

    // Function that checks if a string
    // contains uppercase, lowercase
    // special character & numeric value
    static void
    isAllPresent(string str)
    {
        // ReGex to check if a string
        // contains uppercase, lowercase
        // special character & numeric value
        string regex = "^(?=.*[a-z])(?=."
                    + "*[A-Z])(?=.*\\d)"
                    + "(?=.*[-+_!@#$%^&*., ?]).+{content}quot;;

        // Compile the ReGex
        Regex p = new Regex(regex);

        // If the string is empty
        // then print No
        if (str == null) {
            Console.Write("No");
            return;
        }

        // Find match between given string
        // & regular expression
        Match m = p.Match(str);

        // Print Yes if string
        // matches ReGex
        if (m.Success)
            Console.Write("Yes");
        else
            Console.Write("No");
    }

    // Driver Code
    public static void Main()
    {
        // Given string
        string str = "#GeeksForGeeks123@";

        // Function Call
        isAllPresent(str);
    }
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
      // JavaScript program to check if the string
      // contains uppercase, lowercase
      // special character & numeric value

      function isAllPresent(str) {
        // Regex to check if a string
        // contains uppercase, lowercase
        // special character & numeric value
        var pattern = new RegExp(
          "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[-+_!@#$%^&*.,?]).+{content}quot;
        );

        // If the string is empty
        // then print No
        if (!str || str.length === 0) {
          document.write("No" + "<br>");
          return;
        }

        // Print Yes If the string matches
        // with the Regex
        if (pattern.test(str)) {
          document.write("Yes" + "<br>");
        } else {
          document.write("No" + "<br>");
        }
        return;
      }

      // Driver Code
      var str = "#GeeksForGeeks123@";
      isAllPresent(str);
    </script>
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)