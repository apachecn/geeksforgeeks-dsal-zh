# 检查字符串是否仅由特殊字符组成

> 原文:[https://www . geesforgeks . org/check-if-a-string-only-由特殊字符组成/](https://www.geeksforgeeks.org/check-if-a-string-consists-only-of-special-characters/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是检查给定字符串是否只包含特殊字符。如果字符串仅包含特殊字符，则打印“**是”**。否则，打印“**否”**。

**示例:**

> **输入:**str = " @ # { content } amp；%!~"
> **输出:**是
> **说明:**
> 给定字符串只包含特殊字符。
> 因此，输出为是。
> 
> **输入:** str = "Geeks4Geeks@#"
> **输出:**否
> **说明:**
> 给定字符串包含字母、数字和特殊字符。
> 因此，输出为否

**天真方法:** [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并检查字符串是否只包含特殊字符。按照以下步骤解决问题:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，检查每个字符的 ASCII 值是否在范围**【32，47】****【58，64】****【91，96】**或**【123，126】**内。如果发现是真的，那就是特殊人物。
*   如果所有字符都在上述范围内，打印**是**。否则，打印**号**

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**节省空间的方法:**思路是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)对上述方法进行优化。请遵循以下步骤:

*   创建以下[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来检查给定字符串是否只包含特殊字符。

> regex =[^ a-za-z0-9]+"
> 
> 哪里，
> 
> *   **【^a-za-z0-9】**仅代表特殊字符。
> *   ***+*** 代表一次或多次。

*   使用 Java 中的[<u>pattern . matcher()</u>](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/)<u>将给定的字符串与正则表达式进行匹配</u>
*   <u>如果字符串与给定的正则表达式匹配，则打印**是**。否则，打印**否**。</u>

<u>下面是上述方法的实现:</u>

## <u>C++</u>

```
// C++ program to check if the string
// contains only special characters
#include <iostream>
#include <regex>
using namespace std;

// Function to check if the string contains only special characters.
void onlySpecialCharacters(string str)
{

  // Regex to check if the string contains only special characters.
  const regex pattern("[^a-zA-Z0-9]+");

  // If the string
  // is empty then print "No"
  if (str.empty())
  {
     cout<< "No";
     return ;
  }

  // Print "Yes" if the the string contains only special characters
  // matched the ReGex
  if(regex_match(str, pattern))
  {
    cout<< "Yes";
  }
  else
  {
    cout<< "No";
  }
}

// Driver Code
int main()
{

  // Given string str
  string str = "@#{content}amp;%!~";
  onlySpecialCharacters(str) ;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to check if the string
// contains only special characters

import java.util.regex.*;
class GFG {

    // Function to check if a string
    // contains only special characters
    public static void onlySpecialCharacters(
        String str)
    {

        // Regex to check if a string contains
        // only special characters
        String regex = "[^a-zA-Z0-9]+";

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

        // Print Yes If the string matches
        // with the Regex
        if (m.matches())
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given string str
        String str = "@#{content}amp;%!~";

        // Function Call
        onlySpecialCharacters(str);
    }
}
```

## <u>蟒蛇 3</u>

```
# Python program to check if the string
# contains only special characters
import re

# Function to check if a string
# contains only special characters
def onlySpecialCharacters(Str):

    # Regex to check if a string contains
    # only special characters
    regex = "[^a-zA-Z0-9]+"

    # Compile the ReGex
    p=re.compile(regex)

    # If the string is empty
    # then print No
    if(len(Str) == 0):
        print("No")
        return

    # Print Yes If the string matches
    # with the Regex
    if(re.search(p, Str)):
        print("Yes")
    else:
        print("No")

# Driver Code

# Given string str
Str = "@#{content}amp;%!~"

# Function Call
onlySpecialCharacters(Str)

# This code is contributed by avanitrachhadiya2155
```

## <u>C#</u>

```
// C# program to check if
// the string contains only
// special characters
using System;
using System.Text.RegularExpressions; 
class GFG{

// Function to check if a string
// contains only special characters
public static void onlySpecialchars(String str)
{
  // Regex to check if a string
  // contains only special
  // characters
  String regex = "[^a-zA-Z0-9]+";

  // Compile the ReGex
  Regex rgex = new Regex(regex); 

  // If the string is empty
  // then print No
  if (str == null)
  {
    Console.WriteLine("No");
    return;
  }

  // Find match between given
  // string & regular expression
  MatchCollection matchedAuthors =
                  rgex.Matches(str);   

  // Print Yes If the string matches
  // with the Regex
  if (matchedAuthors.Count != 0)
    Console.WriteLine("Yes");
  else
    Console.WriteLine("No");
}

// Driver Code
public static void Main(String []args)
{
  // Given string str
  String str = "@#{content}amp;%!~";

  // Function Call
  onlySpecialchars(str);
}
}

// This code is contributed by Princi Singh
```

## <u>java 描述语言</u>

```
<script>

      // JavaScript program to check if
      // the string contains only
      // special characters

      // Function to check if a string
      // contains only special characters
      function onlySpecialchars(str)
      {
        // Regex to check if a string
        // contains only special
        // characters
        var regex = /^[^a-zA-Z0-9]+$/;

        // If the string is empty
        // then print No
        if (str.length < 1) {
          document.write("No");
          return;
        }

        // Find match between given
        // string & regular expression
        var matchedAuthors = regex.test(str);

        // Print Yes If the string matches
        // with the Regex
        if (matchedAuthors) document.write("Yes");
        else document.write("No");
      }

      // Driver Code

     // Given string str
      var str = "@#{content}amp;%!~";

     // Function Call
      onlySpecialchars(str);

 </script>
```

<u>**Output:** 

```
Yes
```</u> 

<u>**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*</u>