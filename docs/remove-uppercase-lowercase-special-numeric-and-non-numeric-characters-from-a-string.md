# 从字符串中删除大写、小写、特殊、数字和非数字字符

> 原文:[https://www . geesforgeks . org/remove-大写-小写-特殊-数字和非数字-字符-从字符串中/](https://www.geeksforgeeks.org/remove-uppercase-lowercase-special-numeric-and-non-numeric-characters-from-a-string/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是从该字符串中删除大写、小写、特殊、数字和非数字字符，并在同时修改后打印该字符串。

**示例:**

> **输入:**str = " gfg fg 123 美元% "
> 
> **输出:**去掉大写字符后 **:** gfg123$%
> 
> 删除小写字符后:GFG123$%
> 
> 删除特殊字符后:GFGgfg123
> 
> 删除数字字符后:GFGgfg$%
> 
> 删除非数字字符后:123
> 
> **输入:** str = "J@va12 "
> 
> **输出:**去掉大写字符后 **:** @va12
> 
> 删除小写字符后:J@12
> 
> 去掉特殊字符后:金刚 12
> 
> 删除数字字符后:J@va
> 
> 删除非数字字符后:12

**天真方法:**最简单的方法是遍历字符串，删除大写、小写、特殊、数字和非数字字符。以下是步骤:

1.从头到尾逐字符遍历字符串。

2.检查每个字符的 ASCII 值是否符合以下条件:

*   如果 ASCII 值在**【65，90】**范围内，则为大写字符。因此，跳过这些字符，将其余字符添加到另一个字符串中并打印出来。
*   如果 ASCII 值在**【97，122】**范围内，则为小写字符。因此，跳过这些字符，将其余字符添加到另一个字符串中并打印出来。
*   如果 ASCII 值在**【32，47】**、**【58，64】**、**【91，96】**或**【123，126】**的范围内，则为特殊字符。因此，跳过这些字符，将其余字符添加到另一个字符串中并打印出来。
*   如果 ASCII 值在**【48，57】**的范围内，则它是一个数字字符。因此，跳过这些字符，将其余字符添加到另一个字符串中并打印出来。
*   否则该字符是非数字字符。因此，跳过这些字符，将其余字符添加到另一个字符串中并打印出来。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**正则表达式方法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。以下是步骤:

1.创建[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)从字符串中删除大写、小写、特殊、数字和非数字字符，如下所述:

> *   【regecontextremoveupper 字符】【a-z】
> *   【管理外向性格】【a-z】
> *   【regextremovespecialcharacters = "[^ a-za-z0-9]"
> *   【regextremovenumeric characters = "[0-0-9]

2.使用 [Pattern.compile()](https://www.geeksforgeeks.org/pattern-compilestring-method-in-java-with-examples/) 方法编译给定的正则表达式以创建模式。

3.使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 将给定的字符串与上述所有正则表达式进行匹配。

4.使用 [Matcher.replaceAll()](https://www.geeksforgeeks.org/matcher-replaceallstring-method-in-java-with-examples/) 方法将每个匹配的模式替换为目标字符串。

下面是上述方法的实现:

## C++

```
// C++ program to remove uppercase, lowercase
// special, numeric, and non-numeric characters
#include <iostream>
#include <regex>
using namespace std;

// Function to remove uppercase characters
string removingUpperCaseCharacters(string str)
{
  // Create a regular expression
  const regex pattern("[A-Z]");

  // Replace every matched pattern with the
  // target string using regex_replace() method
  return regex_replace(str, pattern, "");
}

// Function to remove lowercase characters
string removingLowerCaseCharacters(string str)
{
  // Create a regular expression
  const regex pattern("[a-z]");

  // Replace every matched pattern with the
  // target string using regex_replace() method
  return regex_replace(str, pattern, "");
}

// Function to remove special characters
string removingSpecialCharacters(string str)
{
  // Create a regular expression
  const regex pattern("[^A-Za-z0-9]");

  // Replace every matched pattern with the
  // target string using regex_replace() method
  return regex_replace(str, pattern, "");
}

// Function to remove numeric characters
string removingNumericCharacters(string str)
{
  // Create a regular expression
  const regex pattern("[0-9]");

  // Replace every matched pattern with the
  // target string using regex_replace() method
  return regex_replace(str, pattern, "");
}

// Function to remove non-numeric characters
string removingNonNumericCharacters(string str)
{
  // Create a regular expression
  const regex pattern("[^0-9]");

  // Replace every matched pattern with the
  // target string using regex_replace() method
  return regex_replace(str, pattern, "");
}

int main()
{
  // Given String str
  string str = "GFGgfg123$%";

  // Print the strings after the simultaneous
  // modifications
  cout << "After removing uppercase characters: "
       << removingUpperCaseCharacters(str) << endl;
  cout << "After removing lowercase characters: "
       << removingLowerCaseCharacters(str) << endl;
  cout << "After removing special characters: "
       << removingSpecialCharacters(str) << endl;
  cout << "After removing numeric characters: "
       << removingNumericCharacters(str) << endl;
  cout << "After removing non-numeric characters: "
       << removingNonNumericCharacters(str) << endl;

  return 0;
}

// This article is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove uppercase, lowercase
// special, numeric, and non-numeric characters
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class GFG
{

    // Function to remove uppercase characters
    public static String
    removingUpperCaseCharacters(String str)
    {

        // Create a regular expression
        String regex = "[A-Z]";

        // Compile the regex to create pattern
        // using compile() method
        Pattern pattern = Pattern.compile(regex);

        // Get a matcher object from pattern
        Matcher matcher = pattern.matcher(str);

        // Replace every matched pattern with the
        // target string using replaceAll() method
        return matcher.replaceAll("");
    }

    // Function to remove lowercase characters
    public static String
    removingLowerCaseCharacters(String str)
    {

        // Create a regular expression
        String regex = "[a-z]";

        // Compile the regex to create pattern
        // using compile() method
        Pattern pattern = Pattern.compile(regex);

        // Get a matcher object from pattern
        Matcher matcher = pattern.matcher(str);

        // Replace every matched pattern with the
        // target string using replaceAll() method
        return matcher.replaceAll("");
    }

    // Function to remove special characters
    public static String
    removingSpecialCharacters(String str)
    {

        // Create a regular expression
        String regex = "[^A-Za-z0-9]";

        // Compile the regex to create pattern
        // using compile() method
        Pattern pattern = Pattern.compile(regex);

        // Get a matcher object from pattern
        Matcher matcher = pattern.matcher(str);

        // Replace every matched pattern with the
        // target string using replaceAll() method
        return matcher.replaceAll("");
    }

    // Function to remove numeric characters
    public static String
    removingNumericCharacters(String str)
    {

        // Create a regular expression
        String regex = "[0-9]";

        // Compile the regex to create pattern
        // using compile() method
        Pattern pattern = Pattern.compile(regex);

        // Get a matcher object from pattern
        Matcher matcher = pattern.matcher(str);

        // Replace every matched pattern with the
        // target string using replaceAll() method
        return matcher.replaceAll("");
    }

    // Function to remove non-numeric characters
    public static String
    removingNonNumericCharacters(String str)
    {

        // Create a regular expression
        String regex = "[^0-9]";

        // Compile the regex to create pattern
        // using compile() method
        Pattern pattern = Pattern.compile(regex);

        // Get a matcher object from pattern
        Matcher matcher = pattern.matcher(str);

        // Replace every matched pattern with the
        // target string using replaceAll() method
        return matcher.replaceAll("");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given String str
        String str = "GFGgfg123$%";

        // Print the strings after the simultaneous
        // modifications
        System.out.println(
            "After removing uppercase characters: "
            + removingUpperCaseCharacters(str));
        System.out.println(
            "After removing lowercase characters: "
            + removingLowerCaseCharacters(str));
        System.out.println(
            "After removing special characters: "
            + removingSpecialCharacters(str));
        System.out.println(
            "After removing numeric characters: "
            + removingNumericCharacters(str));
        System.out.println(
            "After removing non-numeric characters: "
            + removingNonNumericCharacters(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program to remove
# uppercase, lowercase special,
# numeric, and non-numeric characters
import re

# Function to remove
# uppercase characters
def removingUpperCaseCharacters(str):

    # Create a regular expression
    regex = "[A-Z]"

    # Replace every matched pattern 
    # with the target string using
    # sub() method
    return (re.sub(regex, "", str))

# Function to remove lowercase
# characters
def removingLowerCaseCharacters(str):

    # Create a regular expression
    regex = "[a-z]"

    # Replace every matched
    # pattern with the target
    # string using sub() method
    return (re.sub(regex, "", str))

def removingSpecialCharacters(str):

    # Create a regular expression
    regex = "[^A-Za-z0-9]"

    # Replace every matched pattern
    # with the target string using
    # sub() method
    return (re.sub(regex, "", str))

def removingNumericCharacters(str):

    # Create a regular expression
    regex = "[0-9]"

    # Replace every matched
    # pattern with the target
    # string using sub() method
    return (re.sub(regex, "", str))

def  removingNonNumericCharacters(str):

    # Create a regular expression
    regex = "[^0-9]"

    # Replace every matched pattern
    # with the target string using
    # sub() method
    return (re.sub(regex, "", str))

str = "GFGgfg123$%"
print("After removing uppercase characters:",
       removingUpperCaseCharacters(str))
print("After removing lowercase characters:",
       removingLowerCaseCharacters(str))
print("After removing special characters:",
       removingSpecialCharacters(str))
print("After removing numeric characters:",
       removingNumericCharacters(str))
print("After removing non-numeric characters:",
       removingNonNumericCharacters(str))

# This code is contributed by avanitrachhadiya2155
```

**Output**

```
After removing uppercase characters: gfg123$%
After removing lowercase characters: GFG123$%
After removing special characters: GFGgfg123
After removing numeric characters: GFGgfg$%
After removing non-numeric characters: 123
```

**时间复杂度:** O(N)

**辅助空间:** O(1)