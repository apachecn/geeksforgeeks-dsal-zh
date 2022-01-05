# 将给定字符串中的元音转换为大写字符

> 原文:[https://www . geeksforgeeks . org/convert-元音-to-大写-给定字符串中的字符/](https://www.geeksforgeeks.org/convert-vowels-into-upper-case-character-in-a-given-string/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是将给定字符串中存在的所有元音转换为给定字符串中的[大写字符](https://www.geeksforgeeks.org/count-uppercase-lowercase-special-character-numeric-values/)。

**示例:**

> **输入:**str = " geesforgeks "
> **输出:**geesforgeks
> **解释:**
> 给定字符串中出现的元音为:{'e '，' o'}
> 将' E '替换为' E '，将' O '替换为' O '。
> 因此，需要的输出是 GEEksfOrGEEks。
> 
> **输入:**str = " EUtOpIA "
> T3】输出: EUtOpIA

**方法:**思路是[迭代给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，检查当前字符是否是小写字符和元音。如果发现为真，则将字符转换为大写。按照以下步骤解决问题:

*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，检查**字符串【I】**是否为小写元音。
*   如果发现属实，将 **str[i]** 替换为**(str[I]–‘A’+‘A’)**。
*   最后，在完成字符串遍历后，打印最后一个字符串。

以下是该方法的实施情况:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to convert vowels
// into uppercase
string conVowUpp(string& str)
{
    // Stores the length
    // of str
    int N = str.length();

    for (int i = 0; i < N; i++) {
        if (str[i] == 'a' || str[i] == 'e'
            || str[i] == 'i' || str[i] == 'o'
            || str[i] == 'u') {
            str[i] = str[i] - 'a' + 'A';
        }
    }
    return str;
}

// Driver Code
int main()
{
    string str = "eutopia";
    cout << conVowUpp(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to convert vowels
// into uppercase
static void conVowUpp(char[] str)
{
  // Stores the length
  // of str
  int N = str.length;

  for (int i = 0; i < N; i++)
  {
    if (str[i] == 'a' || str[i] == 'e' ||
        str[i] == 'i' || str[i] == 'o' ||
        str[i] == 'u')
    {
      char c = Character.toUpperCase(str[i]);
      str[i] = c;
    }
  }
  for(char c : str)
    System.out.print(c);
}

// Driver Code
public static void main(String[] args)
{
  String str = "eutopia";
  conVowUpp(str.toCharArray());
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to convert vowels
# into uppercase
def conVowUpp(str):

    # Stores the length
    # of str
    N = len(str)

    str1 =""

    for i in range(N):
        if (str[i] == 'a' or str[i] == 'e' or
            str[i] == 'i' or str[i] == 'o' or
            str[i] == 'u'):
            c = (str[i]).upper()
            str1 += c
        else:
            str1 += str[i]

    print(str1)

# Driver Code
if __name__ == '__main__':

    str = "eutopia"

    conVowUpp(str)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to convert vowels
// into uppercase
static void conVowUpp(char[] str)
{
  // Stores the length
  // of str
  int N = str.Length;

  for (int i = 0; i < N; i++)
  {
    if (str[i] == 'a' || str[i] == 'e' ||
        str[i] == 'i' || str[i] == 'o' ||
        str[i] == 'u')
    {
      char c = char.ToUpperInvariant(str[i]);
      str[i] = c;
    }
  }
  foreach(char c in str)
    Console.Write(c);
}

// Driver Code
public static void Main(String[] args)
{
  String str = "eutopia";
  conVowUpp(str.ToCharArray());
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach

      // Function to convert vowels
      // into uppercase
      function conVowUpp(str) {
        // Stores the length
        // of str
        var N = str.length;

        for (var i = 0; i < N; i++) {
          if (
            str[i] === "a" ||
            str[i] === "e" ||
            str[i] === "i" ||
            str[i] === "o" ||
            str[i] === "u"
          ) {
            document.write(str[i].toUpperCase());
          } else {
            document.write(str[i]);
          }
        }
      }

      // Driver Code

      var str = "eutopia";
      conVowUpp(str);

</script>
```

**Output:** 

```
EUtOpIA
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)