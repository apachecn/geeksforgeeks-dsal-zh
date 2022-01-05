# 使用正则表达式

检查网址是否有效

> 原文:[https://www . geesforgeks . org/check-if-an-URL-valid-or-not-use-正则表达式/](https://www.geeksforgeeks.org/check-if-an-url-is-valid-or-not-using-regular-expression/)

给定一个网址作为大小为 **N** 的字符串**字符串**。任务是检查给定的网址是否有效。
**例:**

> **输入:**str = " https://www . geeksforgeeks . org/"
> **输出:**是
> **说明:**
> 以上网址为有效网址。
> **输入:**str = " https://www.geeksforgeeks.org/"
> **输出:**否
> **说明:**
> 注意 https://后面有空格，因此 URL 无效。

**方法:**
使用 [java.net.url](https://www.geeksforgeeks.org/url-class-java-examples/) 类验证 url 的方法在[之前的](https://www.geeksforgeeks.org/check-if-url-is-valid-or-not-in-java/)帖子中讨论过。
这里的想法是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来验证一个网址。

*   获取网址。
*   如下所述，创建一个正则表达式来检查有效的网址:

> **regex = "(http | https):/)(www .)？"**
> **+[a-za-z0-9 @:%。_ \ \ \+~ #？& //=]{2，256}\。[a-z]"**
> **+{ 2.6 } \ \ b([-a-za-z0-9 @:%。_ \ \ \+~ #？&//=]*)**
> 
> *   网址必须以 http 或 https 开头
> *   然后是 **://** 和
> *   那么它必须包含 **www。**和
> *   然后是长度为(2，256)的子域
> *   最后一部分包含顶级域名，如**。com，。组织**等。

*   将给定的网址与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/pattern-matchercharsequence-method-in-java-with-examples/) 来完成。
*   如果 URL 与给定的正则表达式匹配，则返回 true，否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to validate URL
// using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate URL
// using regular expression
bool isValidURL(string url)
{

  // Regex to check valid URL
  const regex pattern("((http|https)://)(www.)?[a-zA-Z0-9@:%._\\+~#?&//=]{2,256}\\.[a-z]{2,6}\\b([-a-zA-Z0-9@:%._\\+~#?&//=]*)");

  // If the URL
  // is empty return false
  if (url.empty())
  {
     return false;
  }

  // Return true if the URL
  // matched the ReGex
  if(regex_match(url, pattern))
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
  string url = "https://www.geeksforgeeks.org";

  if (isValidURL(url))
  {
    cout << "YES";
  }
  else
  {
    cout << "NO";
  }
  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check URL is valid or not
// using Regular Expression

import java.util.regex.*;

class GFG {

    // Function to validate URL
    // using regular expression
    public static boolean
    isValidURL(String url)
    {
        // Regex to check valid URL
        String regex = "((http|https)://)(www.)?"
              + "[a-zA-Z0-9@:%._\\+~#?&//=]"
              + "{2,256}\\.[a-z]"
              + "{2,6}\\b([-a-zA-Z0-9@:%"
              + "._\\+~#?&//=]*)";

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (url == null) {
            return false;
        }

        // Find match between given string
        // and regular expression
        // using Pattern.matcher()
        Matcher m = p.matcher(url);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver code
    public static void main(String args[])
    {
        String url
            = "https://www.geeksforgeeks.org";
        if (isValidURL(url) == true) {
            System.out.println("Yes");
        }
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check
# URL is valid or not
# using regular expression
import re

# Function to validate URL
# using regular expression
def isValidURL(str):

    # Regex to check valid URL
    regex = ("((http|https)://)(www.)?" +
             "[a-zA-Z0-9@:%._\\+~#?&//=]" +
             "{2,256}\\.[a-z]" +
             "{2,6}\\b([-a-zA-Z0-9@:%" +
             "._\\+~#?&//=]*)")

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
url = "https://www.geeksforgeeks.org"

if(isValidURL(url) == True):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O (1)