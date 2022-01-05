# 通过将另一个给定字符串中相同索引字符的整数值相加来修改字符串中的字符

> 原文:[https://www . geesforgeks . org/通过从另一个给定字符串中添加相同索引字符的整数值来修改字符串字符/](https://www.geeksforgeeks.org/modify-characters-of-a-string-by-adding-integer-values-of-same-indexed-characters-from-another-given-string/)

给定两个相同长度的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **N** ，分别由字母和数字字符组成，任务是通过将字符串 **N** 的每个字符的整数值与字符串 **S** 的相同索引字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)相加，生成一个新的字符串。最后，打印结果字符串。
***注意:**如果总和超过 122，则从总和中减去 26，并打印结果字符。*

**示例:**

> **输入:** S = "sun "，N = "966"
> **输出:**【蝙蝠】
> **解释:**
> 的 ASCII 值为' s' = 115。
> 因此，115+9 = 124–26 = 98。因此，等价字符是' b '。
> ASCII 值‘u’= 117。
> 因此，117+6 = 123–26 = 97。因此，等价字符是“a”。
> ASCII 值‘n’= 110。
> 因此，110 + 6 = 116。因此，等价字符是' t '。
> 
> **输入:** S = "苹果"，N = " 12580 "
> T3】输出:【蛮力】

**方法:**按照以下步骤解决问题:

*   [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)T2【S:
    *   [将字符串 **N** 的当前字符转换为其等效整数值。](https://www.geeksforgeeks.org/converting-strings-numbers-cc/)
    *   将得到的整数值与字符串 **S** 中当前字符的等效 ASCII 值相加。
    *   如果该值超过 **122** ，即最后一个字母 **'z'** 的 ASCII 值，则用 **26 减去该值。**
    *   通过用 ASCII 值等于获得的值的字符替换当前字符来更新字符串 **S** 。
*   完成上述步骤后，打印结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify a given string
// by adding ASCII value of characters
// from a string S to integer values of
// same indexed characters in string N
void addASCII(string S, string N)
{
    // Traverse the string
    for (int i = 0; i < S.size(); i++) {

        // Stores integer value of
        // character in string N
        int a = int(N[i]) - '0';

        // Stores ASCII value of
        // character in string S
        int b = int(S[i]) + a;

        // If b exceeds 122
        if (b > 122)
            b -= 26;

        // Replace the character
        S[i] = char(b);
    }

    // Print resultant string
    cout << S;
}

// Driver Code
int main()
{
    // Given strings
    string S = "sun", N = "966";

    // Function call to modify
    // string S by given operations
    addASCII(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to modify a given String
// by adding ASCII value of characters
// from a String S to integer values of
// same indexed characters in String N
static void addASCII(char []S, char []N)
{

    // Traverse the String
    for (int i = 0; i < S.length; i++)
    {

        // Stores integer value of
        // character in String N
        int a = (int)(N[i]) - '0';

        // Stores ASCII value of
        // character in String S
        int b = (int)(S[i]) + a;

        // If b exceeds 122
        if (b > 122)
            b -= 26;

        // Replace the character
        S[i] = (char)(b);
    }

    // Print resultant String
    System.out.print(S);
}

// Driver Code
public static void main(String[] args)
{

    // Given Strings
    String S = "sun", N = "966";

    // Function call to modify
    // String S by given operations
    addASCII(S.toCharArray(), N.toCharArray());
}
}

// This code is contributed by shikhasingrajput.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to modify a given string
# by adding ASCII value of characters
# from a string S to integer values of
# same indexed characters in string N
def addASCII(S, N):

    # Traverse the string
    for i in range(len(S)):

        # Stores integer value of
        # character in string N
        a = ord(N[i]) - ord('0')

        # Stores ASCII value of
        # character in string S
        b = ord(S[i]) + a

        # If b exceeds 122
        if (b > 122):
            b -= 26

        # Replace the character
        S = S.replace(S[i], chr(b))

    # Print resultant string
    print(S)

# Driver Code
if __name__ == "__main__":

    # Given strings
    S = "sun"
    N = "966"

    # Function call to modify
    # string S by given operations
    addASCII(S, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to modify a given String
// by adding ASCII value of characters
// from a String S to integer values of
// same indexed characters in String N
static void addASCII(char []S, char []N)
{

    // Traverse the String
    for (int i = 0; i < S.Length; i++)
    {

        // Stores integer value of
        // character in String N
        int a = (int)(N[i]) - '0';

        // Stores ASCII value of
        // character in String S
        int b = (int)(S[i]) + a;

        // If b exceeds 122
        if (b > 122)
            b -= 26;

        // Replace the character
        S[i] = (char)(b);
    }

    // Print resultant String
    Console.Write(S);
}

// Driver Code
public static void Main(String[] args)
{

    // Given Strings
    String S = "sun", N = "966";

    // Function call to modify
    // String S by given operations
    addASCII(S.ToCharArray(), N.ToCharArray());
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to modify a given string
      // by adding ASCII value of characters
      // from a string S to integer values of
      // same indexed characters in string N
      function addASCII(S, N) {
        var newStr = new Array(S.length);
        // Traverse the string
        for (var i = 0; i < S.length; i++) {
          // Stores integer value of
          // character in string N
          var a = N[i].charCodeAt(0) - "0".charCodeAt(0);

          // Stores ASCII value of
          // character in string S
          var b = S[i].charCodeAt(0) + a;

          // If b exceeds 122
          if (b > 122) b -= 26;

          // Replace the character
          newStr[i] = String.fromCharCode(b);
        }

        // Print resultant string
        document.write(newStr.join(""));
      }

      // Driver Code
      // Given strings
      var S = "sun",
        N = "966";

      // Function call to modify
      // string S by given operations
      addASCII(S, N);
    </script>
```

**Output:** 

```
bat
```

***时间复杂度:** O(|S|)*
***辅助空间:** O(1)*