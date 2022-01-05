# 在具有给定字符错误按钮的键盘上输入给定字符串生成的字符串

> 原文:[https://www . geesforgeks . org/通过在键盘中键入给定字符串生成的字符串-具有给定字符的按钮-有故障/](https://www.geeksforgeeks.org/string-generated-by-typing-given-string-in-a-keyboard-having-the-button-of-given-character-faulty/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**和一个[字符](https://www.geeksforgeeks.org/character-class-java/) **ch** ，其中字符 **ch** 的按钮工作不正常。按下该键后，会切换**大写锁定**而不是该字母。任务是在这样一个有故障的键盘上打印出**字符串**后生成的字符串。
***注意:**字符串可以同时包含大写和小写字符。*

**示例:**

> **输入:** str = "此键盘有故障。"，ch = 'a'
> **输出:**此键盘有故障。
> **解释:**
> 【a】在位置 10(基于 0 的索引)遇到，这将打开大写锁定，导致进一步的字符大写，直到在位置 18 遇到下一个“a”，这将关闭它。
> 因此，结果字符串是“此键盘有故障。”。
> 
> **输入:** str =“阅读短语。”，ch = 'z'
> **输出:**读短语。
> **说明:**由于字符串中没有出现‘z’，所以字符串字符串打印正确。

**方法:**按照以下步骤解决上述问题:

*   将布尔变量 **CapsLockOn** 初始化为 **false** ，该变量将存储 **Caps Lock** 是否打开。
*   [逐个字符遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，并执行以下操作:
    *   如果字符串中的任何字符与 **ch** 相同，则删除当前字符并反转**caplock on**的值，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)至[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。
    *   如果**大写**为**真**，则将当前字符更新为大写，反之亦然。
    *   如果**caplock on**为 **False** ，则保持当前角色不变。
*   完成字符串遍历后，打印结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the updated string
// after typing on faulty keyboard
string faultyKeyboard(string str, char ch)
{
    // Stores the status of Caps Lock
    bool CapsLockOn = false;

    int i = 0;

    // Traverse over the string
    while (i < str.length()) {

        // If ch is lower case
        if (str[i] == ch
            || str[i] == char(ch + 32)) {

            // Toggle the caps lock
            CapsLockOn = !CapsLockOn;

            // Delete i-th character
            str.erase(i, 1);

            continue;
        }

        // If ch is upper case
        else if (str[i] == ch
                 || str[i] == char(ch + 32)) {

            // Toggle the caps lock
            CapsLockOn = !CapsLockOn;

            // Delete i-th character
            str.erase(i, 1);

            continue;
        }

        // If CapsLockOn is true
        else if (CapsLockOn) {

            if (islower(str[i])) {

                // Convert the lower case
                // character to upper case
                str[i] = toupper(str[i]);
            }
            else {

                // Convert the upper case
                // character to lower case
                str[i] = tolower(str[i]);
            }
        }

        // Increment for next iteration
        i++;
    }

    // Return the resultant string
    return str;
}

// Driver Code
int main()
{
    // Given string str
    string str = "This keyboard is faulty.";

    char ch = 'a';

    // Function Call
    cout << faultyKeyboard(str, ch);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the updated string
// after typing on faulty keyboard
static String faultyKeyboard(String str, char ch)
{

    // Stores the status of Caps Lock
    boolean CapsLockOn = false;

    int i = 0;

    // Traverse over the string
    while (i < str.length())
    {

        // If ch is lower case
        if (str.charAt(i) == ch ||
            str.charAt(i) == (char)((int)ch + 32))
        {

            // Toggle the caps lock
            CapsLockOn = !CapsLockOn;

            // Delete i-th character
            str = str.substring(0, i) +
                  str.substring(i + 1);

           // str.replace(str.charAt(i),'');

            continue;
        }

        // If ch is upper case
        else if (str.charAt(i) == ch ||
                 str.charAt(i) == (char)((int)ch + 32))
        {

            // Toggle the caps lock
            CapsLockOn = !CapsLockOn;

            // Delete i-th character
           str = str.substring(0, i) +
                 str.substring(i + 1); 
           // str.replace(str.charAt(i),'');

            continue;
        }

        // If CapsLockOn is true
        else if (CapsLockOn)
        {
            if (str.charAt(i) >='a' &&
                str.charAt(i) <= 'z')
            {

                // Convert the lower case
                // character to upper case
                char c = Character.toUpperCase(
                         str.charAt(i));
                str = str.substring(0, i) + c +
                      str.substring(i + 1);

                // str = str.replace(str.charAt(i),
                // Character.toUpperCase(str.charAt(i)));
            }
            else
            {

                // Convert the upper case
                // character to lower case
                char c = Character.toLowerCase(
                         str.charAt(i));
                str = str.substring(0, i) + c +
                      str.substring(i + 1);

               // str = str.replace(str.charAt(i),
               // Character.toLowerCase(str.charAt(i)));
            }
        }

        // Increment for next iteration
        i++;
    }

    // Return the resultant string
    return str;
}

// Driver Code
public static void main(String args[])
{

    // Given string str
    String str = "This keyboard is faulty.";

    char ch = 'a';

    // Function Call
    System.out.print(faultyKeyboard(str, ch));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to return the updated string
# after typing on faulty keyboard
def faultyKeyboard(str, ch):

    # Stores the status of Caps Lock
    CapsLockOn = False
    i = 0

    # Traverse over the string
    while (i < len(str)):

        # If ch is lower case
        if (str[i] == ch or str[i] == chr(ord(ch) + 32)):

            # Toggle the caps lock
            if(CapsLockOn == False):
                CapsLockOn = True
            else:
                CapsLockOn = False

            # Delete i-th character
            str = str.replace(str[i],'', 1)

            continue

        # If ch is upper case
        elif(str[i] == ch or str[i] == chr(ord(ch) + 32)):

            # Toggle the caps lock
            if(CapsLockOn==False):
                CapsLockOn = True
            else:
                CapsLockOn = False

            # Delete i-th character
            str = str.replace(str[i],'', 1)
            continue

        # If CapsLockOn is true
        elif (CapsLockOn):
            if (ord(str[i]) >= 97 and ord(str[i]) <= 122):

                # Convert the lower case
                # character to upper case
                #indexes = set((i))
                chars = list(str)
                chars[i] = chars[i].upper()

                str = ''.join(chars)
            else:

                #indexes = set((i))
                chars = list(str)
                chars[i] = chars[i].lower()

                str = ''.join(chars)

        # Increment for next iteration
        i += 1

    # Return the resultant string
    return str

# Driver Code
if __name__ == '__main__':

    # Given string str
    str = "This keyboard is faulty."
    ch = 'a'

    # Function Call
    print(faultyKeyboard(str, ch))

# This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to return the updated
// string after typing on faulty
// keyboard
static string faultyKeyboard(string str,
                             char ch)
{

  // Stores the status of
  // Caps Lock
  bool CapsLockOn = false;

  int i = 0;
  // Traverse over the string
  while (i < str.Length)
  {
    // If ch is lower case
    if (str[i] == ch ||
        str[i] == (char)(ch + 32))
    {
      // Toggle the caps lock
      CapsLockOn = !CapsLockOn;

      // Delete i-th character
      str = str.Substring(0, i) +
            str.Substring(i + 1);

      continue;
    }

    // If ch is upper case
    else if (str[i] == ch ||
             str[i] == (char)(ch + 32))
    {
      // Toggle the caps lock
      CapsLockOn = !CapsLockOn;

      // Delete i-th character
      str = str.Substring(0, i) +
            str.Substring(i + 1);

      continue;
    }

    // If CapsLockOn is true
    else if (CapsLockOn)
    {
      if (str[i] >= 'a' &&
          str[i] <= 'z')
      {
        // Convert the lower case
        // character to upper case
        char c = (char)(str[i] - 32);
        str = str.Substring(0, i) + c +
              str.Substring(i + 1);
      }
      else if (str[i] >= 'A' &&
               str[i] <= 'Z')
      {
        // Convert the upper case
        // character to lower case
        char c = (char)(str[i] + 32);
        str = str.Substring(0, i) + c +
              str.Substring(i + 1);
      }
    }

    // Increment for next
    // iteration
    i++;
  }

  // Return the resultant
  // string
  return str;
}

// Driver Code
public static void Main()
{
  // Given string str
  string str = "This keyboard is faulty.";

  char ch = 'a';

  // Function Call
  Console.Write(faultyKeyboard(str, ch));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to return the updated string
// after typing on faulty keyboard
function faultyKeyboard(str,ch)
{

    // Stores the status of Caps Lock
    let CapsLockOn = false;
    let i = 0;

    // Traverse over the string
    while (i < str.length)
    {

        // If ch is lower case
        if (str[i] == ch ||
            str[i] == String.fromCharCode(ch.charCodeAt(0) + 32))
        {

            // Toggle the caps lock
            CapsLockOn = !CapsLockOn;

            // Delete i-th character
            str = str.substring(0, i) +
                  str.substring(i + 1);

           // str.replace(str.charAt(i),'');

            continue;
        }

        // If ch is upper case
        else if (str[i] == ch ||
                 str[i] == String.fromCharCode(ch.charCodeAt(0) + 32))
        {

            // Toggle the caps lock
            CapsLockOn = !CapsLockOn;

            // Delete i-th character
           str = str.substring(0, i) +
                 str.substring(i + 1);
           // str.replace(str.charAt(i),'');

            continue;
        }

        // If CapsLockOn is true
        else if (CapsLockOn)
        {
            if (str[i] >='a' &&
                str[i] <= 'z')
            {

                // Convert the lower case
                // character to upper case
                let c = str[i].toUpperCase();
                str = str.substring(0, i) + c +
                      str.substring(i + 1);

                // str = str.replace(str.charAt(i),
                // Character.toUpperCase(str.charAt(i)));
            }
            else
            {

                // Convert the upper case
                // character to lower case
                let c = str[i].toLowerCase();
                str = str.substring(0, i) + c +
                      str.substring(i + 1);

               // str = str.replace(str.charAt(i),
               // Character.toLowerCase(str.charAt(i)));
            }
        }

        // Increment for next iteration
        i++;
    }

    // Return the resultant string
    return str;
}

// Driver Code

// Given string str
let str = "This keyboard is faulty.";
let ch = 'a';

// Function Call
document.write(faultyKeyboard(str, ch));

// This code is contributed by rag2127
</script>
```

**Output**

```
This keyboRD IS Fulty.
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)