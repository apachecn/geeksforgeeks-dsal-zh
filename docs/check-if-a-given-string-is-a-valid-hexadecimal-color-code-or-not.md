# 检查给定的字符串是否是有效的十六进制颜色代码

> 原文:[https://www . geesforgeks . org/check-如果给定的字符串是有效的十六进制颜色代码或不是/](https://www.geeksforgeeks.org/check-if-a-given-string-is-a-valid-hexadecimal-color-code-or-not/)

给定一个字符串 **str** ，任务是检查给定的字符串是否为 [HTML 十六进制色码](https://www.geeksforgeeks.org/html-hex-color-codes/)。如果是打印**是**，否则打印**否**。

**示例:**

> **输入:**str = " 1 affa 1 "
> T3】输出:是
> 
> **输入:**str = " # F00 "
> T3】输出:是
> 
> **输入:**str = " 123456 "
> T3】输出:否

**方法:**一个 HTML 十六进制颜色代码遵循下面提到的一组规则:

1.  它以 **'#'** 符号开始。
2.  然后是来自 **a-f** 、 **A-F** 的字母和/或来自 **0-9** 的数字。
3.  十六进制颜色代码的长度应为 6 或 3，不包括 **'#'** 符号。
4.  例如:#abc、#ABC、#000、#FFF、#000000、#FF0000、#00FF00、#0000FF、#FFFFFF 都是有效的十六进制颜色代码。

现在，要解决上述问题，请遵循以下步骤:

1.  检查弦线**弦线**是否存在以下情况:
    *   如果第一个字符不是 **#** ，则返回**假**。
    *   如果长度不是 **3** 或 **6** 。否则，返回**假**。
    *   现在，检查除第一个字符之外的所有字符，即 **0-9** 、 **A-F** 或 **a-f** 。
2.  如果满足上述所有条件，则返回**真**。
3.  根据以上观察打印答案。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to validate
// the HTML hexadecimal color code.
bool isValidHexaCode(string str)
{
    if (str[0] != '#')
        return false;

    if (!(str.length() == 4 or str.length() == 7))
        return false;

    for (int i = 1; i < str.length(); i++)
        if (!((str[i] >= '0' && str[i] <= 9)
              || (str[i] >= 'a' && str[i] <= 'f')
              || (str[i] >= 'A' || str[i] <= 'F')))
            return false;

    return true;
}

// Driver Code
int main()
{
    string str = "#1AFFa1";

    if (isValidHexaCode(str)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

    // Function to validate
    // the HTML hexadecimal color code.
    static boolean isValidHexaCode(String str)
    {
        if (str.charAt(0) != '#')
            return false;

        if (!(str.length() == 4 || str.length() == 7))
            return false;

        for (int i = 1; i < str.length(); i++)
            if (!((str.charAt(i) >= '0' && str.charAt(i) <= 9)
                || (str.charAt(i) >= 'a' && str.charAt(i) <= 'f')
                || (str.charAt(i) >= 'A' || str.charAt(i) <= 'F')))
                return false;

        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "#1AFFa1";

        if (isValidHexaCode(str)) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to validate
# the HTML hexadecimal color code.
def isValidHexaCode(str):

    if (str[0] != '#'):
        return False

    if (not(len(str) == 4 or len(str) == 7)):
        return False

    for i in range(1, len(str)):
        if (not((str[i] >= '0' and str[i] <= '9') or (str[i] >= 'a' and str[i] <= 'f') or (str[i] >= 'A' or str[i] <= 'F'))):
            return False

    return True

# Driver Code
if __name__ == "__main__":

    str = "#1AFFa1"

    if (isValidHexaCode(str)):
        print("Yes")

    else:
        print("No")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG{

    // Function to validate
    // the HTML hexadecimal color code.
    static bool isValidHexaCode(string str)
    {
        if (str[0] != '#')
            return false;

        if (!(str.Length == 4 || str.Length == 7))
            return false;

        for (int i = 1; i < str.Length; i++)
            if (!((str[i] >= '0' && str[i] <= 9)
                || (str[i] >= 'a' && str[i] <= 'f')
                || (str[i] >= 'A' || str[i] <= 'F')))
                return false;

        return true;
    }

    // Driver code
    public static void Main()
    {
        string str = "#1AFFa1";

        if (isValidHexaCode(str)) {
            Console.Write("Yes");
        }
        else {
            Console.Write("No");
        }
    }
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to validate
       // the HTML hexadecimal color code.
       function isValidHexaCode(str) {
           if (str[0] != '#')
               return false;

           if (!(str.length == 4 || str.length == 7))
               return false;

           for (let i = 1; i < str.length; i++)
               if (!((str[i].charCodeAt(0) <= '0'.charCodeAt(0) && str[i].charCodeAt(0) <= 9)
                   || (str[i].charCodeAt(0) >= 'a'.charCodeAt(0) && str[i].charCodeAt(0) <= 'f'.charCodeAt(0))
                   || (str[i].charCodeAt(0) >= 'A'.charCodeAt(0) || str[i].charCodeAt(0) <= 'F'.charCodeAt(0))))
                   return false;

           return true;
       }

       // Driver Code
       let str = "#1AFFa1";

       if (isValidHexaCode(str)) {
           document.write("Yes" + '<br>');
       }
       else {
           document.write("No" + '<br>');
       }

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)