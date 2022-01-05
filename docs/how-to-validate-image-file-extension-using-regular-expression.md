# 如何使用正则表达式

验证图像文件扩展名

> 原文:[https://www . geesforgeks . org/如何验证-图像-文件-扩展名-使用-正则表达式/](https://www.geeksforgeeks.org/how-to-validate-image-file-extension-using-regular-expression/)

给定字符串 **str** ，任务是使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查给定字符串是否为有效的图像文件扩展名。

> 有效的图像文件扩展名必须指定以下条件:
> 
> 1.  它应该以至少一个字符的字符串开头。
> 2.  它不应该有任何空白。
> 3.  它后面应该跟一个点(。).
> 4.  它应该以下列任何一种扩展名结尾:jpg、jpeg、png、gif、bmp。

**例:**

> **输入:** str = "abc.png"
> **输出:**真
> **解释:**
> 给定字符串满足上述所有条件。
> **输入:** str = "im.jpg"
> **输出:**真
> **解释:**
> 给定字符串满足上述所有条件。
> **输入:** str =。gif"
> **输出:**假
> **说明:**
> 给定字符串不以图像文件名开头(至少需要一个字符)。因此，它不是有效的图像文件扩展名。

**方法:**这个问题可以通过使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决。

*   获取字符串。
*   如下所述，创建一个正则表达式来检查有效的图像文件扩展名:

> regex = "([^\\s]+(\\)。(？i)(jpe？g | png | gif | BMP)]$ "；

*   其中:
    *   **(** 代表第 1 组开始。
    *   **【^\\s]+】**表示字符串必须包含至少一个字符。
    *   **(** 代表第 2 组开始。
    *   **\\。**表示字符串后面应该跟一个点(。).
    *   **(？i)** 表示字符串忽略区分大小写。
    *   **(** 代表组 3 的开始。
    *   **jpe？g|png|gif|bmp** 代表以 jpg 或 jpeg 或 png 或 gif 或 bmp 扩展名结尾的字符串。
    *   **)** 代表第三组的结束。
    *   **)** 代表第二组结束。
    *   **$** 代表字符串的结尾。
    *   **)** 代表第 1 组的结束。
*   用正则表达式匹配给定的字符串。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   如果给定字符串与正则表达式匹配，则返回 true，否则返回 false。

下面是上述方法的实现:

## C++

```
// C++ program to validate the
// image file extension using Regular Expression
#include <iostream>
#include <regex>
using namespace std;

// Function to validate the image file extension.
bool imageFile(string str)
{

  // Regex to check valid image file extension.
  const regex pattern("[^\\s]+(.*?)\\.(jpg|jpeg|png|gif|JPG|JPEG|PNG|GIF){content}quot;);

  // If the image file extension
  // is empty return false
  if (str.empty())
  {
     return false;
  }

  // Return true if the image file extension
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
  string str1 = "abc.png";
  cout << imageFile(str1) << endl;

  // Test Case 2:
  string str2 = "im.jpg";
  cout << imageFile(str2) << endl;

  // Test Case 3:
  string str3 = ".gif";
  cout << imageFile(str3) << endl;

  // Test Case 4:
  string str4 = "abc.mp3";
  cout << imageFile(str4) << endl;

  // Test Case 5:
  string str5 = " .jpg";
  cout << imageFile(str5) << endl;

  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check valid
// image file extension using regex

import java.util.regex.*;
class GFG {

    // Function to validate image file extension .
    public static boolean imageFile(String str)
    {
        // Regex to check valid image file extension.
        String regex
            = "([^\\s]+(\\.(?i)(jpe?g|png|gif|bmp))$)";

        // Compile the ReGex
        Pattern p = Pattern.compile(regex);

        // If the string is empty
        // return false
        if (str == null) {
            return false;
        }

        // Pattern class contains matcher() method
        // to find matching between given string
        // and regular expression.
        Matcher m = p.matcher(str);

        // Return if the string
        // matched the ReGex
        return m.matches();
    }

    // Driver code
    public static void main(String args[])
    {

        // Test Case 1:
        String str1 = "abc.png";
        System.out.println(imageFile(str1));

        // Test Case 2:
        String str2 = "im.jpg";
        System.out.println(imageFile(str2));

        // Test Case 3:
        String str3 = ".gif";
        System.out.println(imageFile(str3));

        // Test Case 4:
        String str4 = "abc.mp3";
        System.out.println(imageFile(str4));

        // Test Case 5:
        String str5 = " .jpg";
        System.out.println(imageFile(str5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to validate
# image file extension using regex
import re

# Function to validate
# image file extension . 
def imageFile(str):

    # Regex to check valid image file extension.
    regex = "([^\\s]+(\\.(?i)(jpe?g|png|gif|bmp))$)"

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
str1 = "abc.png"
print(imageFile(str1))

# Test Case 2:
str2 = "im.jpg"
print(imageFile(str2))

# Test Case 3:
str3 = ".gif"
print(imageFile(str3))

# Test Case 4:
str4 = "abc.mp3"
print(imageFile(str4))

# Test Case 5:
str5 = " .jpg"
print(imageFile(str5))

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