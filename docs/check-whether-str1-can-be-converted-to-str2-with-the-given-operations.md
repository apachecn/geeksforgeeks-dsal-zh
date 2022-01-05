# 用给定的操作

检查 str1 是否可以转换成 str2

> 原文:[https://www . geeksforgeeks . org/check-str 1-是否可以通过给定的操作转换为 str 2/](https://www.geeksforgeeks.org/check-whether-str1-can-be-converted-to-str2-with-the-given-operations/)

给定两个二进制字符串 **str1** 和 **str2** 。任务是通过在 str1 上任意多次应用以下操作，检查是否可以将 **str1** 转换为 **str2** 。
在每次操作中，可以将两个连续的**0**合并为一个 **1** 。
**举例:**

> **输入:**str 1 =“00100”，str 2 =“111”
> **输出:**是
> 将前两个 0 合 1，将后两个 0 合 1。
> **输入:**str1 =“00”，str2 =“000”
> **输出:**否
> 无法将 str 1 转换为 str 2。

**方法:**让我们从左到右逐个字符并行处理 str1 和 str2。让我们使用两个指数 I 和 j:指数 I 代表 str1，指数 j 代表 str2。现在有两种情况:

1.  如果 **str1[i] = str2[j]** ，则增加 **i** 和 **j** 。
2.  如果 **str1[i]！= str2[j]** 然后，
    *   如果 str1 中有两个连续的 0，即 **str1[i] = 0** 和 **str1[i + 1] = 0** 和 **str2[j] = 1** ，这意味着这两个零可以组合起来与 **str2** 中的 **1** 相匹配。所以，将 **i** 增加 **2** ，将 **j** 增加 **1** 。
    *   否则 **str1** 不能转换为 **str2** 。
3.  如果最终 **i** 和 **j** 都在各自的弦的末端，即 **str1** 和 **str2** ，那么答案是**是**，否则答案是**否**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if str1 can be
// converted to str2 with the given operations
bool canConvert(string str1, string str2)
{
    int i = 0, j = 0;

    // Traverse from left to right
    while (i < str1.size() && j < str2.size()) {

        // If the two characters do not match
        if (str1[i] != str2[j]) {

            // If possible to combine
            if (str1[i] == '0' && str2[j] == '1'
                && i + 1 < str1.size()
                && str1[i + 1] == '0') {
                i += 2;
                j++;
            }

            // If not possible to combine
            else {
                return false;
            }
        }

        // If the two characters match
        else {
            i++;
            j++;
        }
    }

    // If possible to convert one string to another
    if (i == str1.size() && j == str2.size())
        return true;
    return false;
}

// Driver code
int main()
{
    string str1 = "00100", str2 = "111";

    if (canConvert(str1, str2))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if str1 can be
    // converted to str2 with the given operations
    static boolean canConvert(String str1, String str2)
    {
        int i = 0, j = 0;

        // Traverse from left to right
        while (i < str1.length() && j < str2.length())
        {

            // If the two characters do not match
            if (str1.charAt(i) != str2.charAt(j))
            {

                // If possible to combine
                if (str1.charAt(i) == '0' && str2.charAt(j) == '1'
                    && i + 1 < str1.length() && str1.charAt(i+1) == '0')
                {
                    i += 2;
                    j++;
                }

                // If not possible to combine
                else
                {
                    return false;
                }
            }

            // If the two characters match
            else
            {
                i++;
                j++;
            }
        }

        // If possible to convert one string to another
        if (i == str1.length() && j == str2.length())
            return true;
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {

        String str1 = "00100", str2 = "111";

        if (canConvert(str1, str2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if str1 can be
# converted to str2 with the given operations
def canConvert(str1, str2):
    i, j = 0, 0;

    # Traverse from left to right
    while (i < len(str1) and j < len(str2)):

        # If the two characters do not match
        if (str1[i] != str2[j]):

            # If possible to combine
            if (str1[i] == '0' and str2[j] == '1'
                and i + 1 < len(str1)
                and str1[i + 1] == '0'):
                i += 2;
                j+=1;

            # If not possible to combine
            else:
                return False;
        # If the two characters match
        else:
            i += 1;
            j += 1;

    # If possible to convert one string to another
    if (i == len(str1) and j == len(str2)):
        return True;
    return False;

# Driver code
str1 = "00100";
str2 = "111";

if (canConvert(str1, str2)):
    print("Yes");
else:
    print("No");

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if str1 can be
    // converted to str2 with the given operations
    static bool canConvert(string str1, string str2)
    {
        int i = 0, j = 0;

        // Traverse from left to right
        while (i < str1.Length && j < str2.Length)
        {

            // If the two characters do not match
            if (str1[i] != str2[j])
            {

                // If possible to combine
                if (str1[i] == '0' && str2[j] == '1'
                    && i + 1 < str1.Length && str1[i+1] == '0')
                {
                    i += 2;
                    j++;
                }

                // If not possible to combine
                else
                {
                    return false;
                }
            }

            // If the two characters match
            else
            {
                i++;
                j++;
            }
        }

        // If possible to convert one string to another
        if (i == str1.Length && j == str2.Length)
            return true;
        return false;
    }

    // Driver code
    public static void Main()
    {

        string str1 = "00100", str2 = "111";

        if (canConvert(str1, str2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function that returns true if str1 can be
      // converted to str2 with the given operations
      function canConvert(str1, str2) {
        var i = 0,
          j = 0;

        // Traverse from left to right
        while (i < str1.length && j < str2.length) {
          // If the two characters do not match
          if (str1[i] !== str2[j]) {
            // If possible to combine
            if (
              str1[i] === "0" &&
              str2[j] === "1" &&
              i + 1 < str1.length &&
              str1[i + 1] === "0"
            ) {
              i += 2;
              j++;
            }

            // If not possible to combine
            else {
              return false;
            }
          }

          // If the two characters match
          else {
            i++;
            j++;
          }
        }

        // If possible to convert one string to another
        if (i === str1.length && j === str2.length) return true;
        return false;
      }

      // Driver code
      var str1 = "00100",
        str2 = "111";

      if (canConvert(str1, str2)) document.write("Yes");
      else document.write("No");
    </script>
```

**Output:** 

```
Yes
```