# 删除字符串中出现的所有字符|递归方法

> 原文:[https://www . geeksforgeeks . org/remove-字符串中出现的所有字符-递归方法/](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-in-a-string-recursive-approach/)

给定字符串 **str** ，任务是编写一个递归程序来删除字符串中出现的所有字符 **X** 。

**示例:**

> **输入:** str = "geeksforgeeks "，c = ' e '
> T3】输出:gksforks
> T6】输入: str = "geeksforgeeks "，c = ' g '
> T9】输出: eeksforeeks

**迭代方法:**这个问题的迭代方法可以在[这个](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-in-a-string/)帖子里找到。
**递归方法:**以下是步骤:

1.  获取要删除字符 **X** 的字符串**字符串**和字符 **X** 。
2.  递归迭代字符串中的所有字符:
    *   **基本情况:**如果递归调用的字符串 **str** 的长度为 0，则从函数返回空字符串。

```
if(str.length()==0) {
   return "";
}
```

*   **递归调用:**如果不满足基本大小写，则在**第 0 个**索引处检查字符，如果是 X，则递归迭代子串，删除第一个字符。

```
if (str[0] == X) {
        return recursive_function(str.substr(1), X);
}
```

*   **Return 语句:**每次递归调用时(基本情况和上述条件除外)，返回下一次迭代的递归函数，包括**第 0 个索引**处的字符。

```
return str[0] + recursive_function(str.substr(1), X)
```

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove all occurrences
// of a character in the string
string removeCharRecursive(string str,
                           char X)
{
    // Base Case
    if (str.length() == 0) {
        return "";
    }

    // Check the first character
    // of the given string
    if (str[0] == X) {

        // Pass the rest of the string
        // to recursion Function call
        return removeCharRecursive(str.substr(1), X);
    }

    // Add the first character of str
    // and string from recursion
    return str[0]
           + removeCharRecursive(str.substr(1), X);
}

// Driver Code
int main()
{
    // Given String
    string str = "geeksforgeeks";

    // Given character
    char X = 'e';

    // Function Call
    str = removeCharRecursive(str, X);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to remove all occurrences
// of a character in the string
static String removeCharRecursive(String str,
                                  char X)
{

    // Base Case
    if (str.length() == 0)
    {
        return "";
    }

    // Check the first character
    // of the given string
    if (str.charAt(0) == X)
    {

        // Pass the rest of the string
        // to recursion Function call
        return removeCharRecursive(
               str.substring(1), X);
    }

    // Add the first character of str
    // and string from recursion
    return str.charAt(0) +
           removeCharRecursive(
           str.substring(1), X);
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String str = "geeksforgeeks";

    // Given character
    char X = 'e';

    // Function call
    str = removeCharRecursive(str, X);

    System.out.println(str);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to remove all occurrences
# of a character in the string
def removeCharRecursive(str, X):

    # Base Case
    if (len(str) == 0):
        return ""

    # Check the first character
    # of the given string
    if (str[0] == X):

        # Pass the rest of the string
        # to recursion Function call
        return removeCharRecursive(str[1:], X)

    # Add the first character of str
    # and string from recursion
    return str[0] + removeCharRecursive(str[1:], X)

# Driver Code

# Given String
str = "geeksforgeeks"

# Given character
X = 'e'

# Function call
str = removeCharRecursive(str, X)

print(str)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to remove all occurrences
// of a character in the string
static String removeCharRecursive(String str,
                                  char X)
{

    // Base Case
    if (str.Length == 0)
    {
        return "";
    }

    // Check the first character
    // of the given string
    if (str[0] == X)
    {

        // Pass the rest of the string
        // to recursion Function call
        return removeCharRecursive(
            str.Substring(1), X);
    }

    // Add the first character of str
    // and string from recursion
    return str[0] + removeCharRecursive(
                    str.Substring(1), X);
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String str = "geeksforgeeks";

    // Given character
    char X = 'e';

    // Function call
    str = removeCharRecursive(str, X);

    Console.WriteLine(str);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to remove all occurrences
// of a character in the string
function removeCharRecursive(str,X)
{

    // Base Case
    if (str.length == 0)
    {
        return "";
    }

    // Check the first character
    // of the given string
    if (str.charAt(0) == X)
    {

        // Pass the rest of the string
        // to recursion Function call
        return removeCharRecursive(
               str.substring(1), X);
    }

    // Add the first character of str
    // and string from recursion
    return str.charAt(0) +
           removeCharRecursive(
           str.substring(1), X);
}

// Driver Code
//Given String
var str = "geeksforgeeks";

// Given character
var X = 'e';

// Function call
str = removeCharRecursive(str, X);

document.write(str);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
gksforgks
```

***时间复杂度:** O(N)，其中 N 是字符串的长度*
***辅助空间:** O(1)*