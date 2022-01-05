# 从给定字符串中移除 HTML 标签的程序

> 原文:[https://www . geeksforgeeks . org/program-to-remove-html-tags-from-给定字符串/](https://www.geeksforgeeks.org/program-to-remove-html-tags-from-a-given-string/)

给定一个包含一些 [HTML 标签](https://www.geeksforgeeks.org/most-commonly-used-tags-in-html/)的字符串 **str** ，任务是移除给定字符串 **str** 中存在的所有标签。
**举例:**

> **输入:**str =<div>T14】b>极客为极客</b></div>"
> **输出:**极客为极客
> **输入:**str =<a href = " https://www . geekesforgeks . org/>GFG</a>
> **输出**

**方法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。可以按照以下步骤计算结果字符串:

1.  去拿绳子。
2.  因为每个 HTML 标签都包含在角括号中( **< >** )。因此在正则表达式中使用 **replaceAll()** 函数，将每个以**“<”**开头，以**“>”**结尾的子字符串替换为空字符串。
3.  该函数用作:

```
String str;
str.replaceAll("\\", "");
```

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <regex>
using namespace std;

// Function to remove the HTML tags
// from the given string
void RemoveHTMLTags(string s)
{
  const regex pattern("\\<.*?\\>");

  // Use regex_replace function in regex
  // to erase every tags enclosed in <>
  s = regex_replace(s, pattern, "");

  // Print string after removing tags
  cout << s;

  return ;
}

// Driver Code
int main()
{

  // Given String
  string str = "<div><b>Geeks for Geeks</b></div>";

  // Function call to print the
  // HTML string after removing tags
  RemoveHTMLTags(str) ;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to remove the HTML tags
    // from the given tags
    static void RemoveHTMLTags(String str)
    {

        // Use replaceAll function in regex
        // to erase every tags enclosed in <>
        str = str.replaceAll("\\<.*?\\>", "");

        // Print string after removing tags
        System.out.println(str);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str;

        // Given String
        str = "<div><b>Geeks for Geeks</b></div>";

        // Function call to print the
        // HTML string after removing tags
        RemoveHTMLTags(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import re

# Function to remove the HTML tags
# from the given tags
def RemoveHTMLTags(strr):

    # Print string after removing tags
    print(re.compile(r'<[^>]+>').sub('', strr))

# Driver code
if __name__=='__main__':

    # Given String
    strr = "<div><b>Geeks for Geeks</b></div>"

    # Function call to print the HTML
    # string after removing tags
    RemoveHTMLTags(strr);

# This code is contributed by vikas_g
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to remove the HTML tags
// from the given tags
static void RemoveHTMLTags(String str)
{

    // Use replaceAll function in regex
    // to erase every tags enclosed in <>
    // str = Regex.Replace(str, "<.*?>", String.Empty)
    System.Text.RegularExpressions.Regex rx =
    new System.Text.RegularExpressions.Regex("<[^>]*>");

    str = rx.Replace(str, "");

    // Print string after removing tags
    Console.WriteLine(str);
}

// Driver code
public static void Main(String []args)
{
    String str;

    // Given String
    str = "<div><b>Geeks for Geeks</b></div>";

    // Function call to print the
    // HTML string after removing tags
    RemoveHTMLTags(str);
}
}

// This code is contributed by vikas_g
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to remove the HTML tags
// from the given string
function RemoveHTMLTags(s) {
    const pattern = new RegExp("\\<.*?\\>");

    // Use regex_replace function in regex
    // to erase every tags enclosed in <>
    s = new String(s).replace(pattern, "");

    // Print string after removing tags
    document.write(s);

    return;
}

// Driver Code

// Given String
let str = "<div><b>Geeks for Geeks</b></div>";

// Function call to print the
// HTML string after removing tags
RemoveHTMLTags(str);

</script>
```

**Output:** 

```
Geeks for Geeks
```