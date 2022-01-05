# 重复删除二进制字符串的第一个字符并翻转字符后的最后一个剩余字符

> 原文:[https://www . geeksforgeeks . org/重复删除二进制字符串的第一个字符并翻转字符后的最后一个剩余字符/](https://www.geeksforgeeks.org/last-remaining-character-after-repeated-removal-of-the-first-character-and-flipping-of-characters-of-a-binary-string/)

给定长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是通过重复删除字符串的第一个字符并翻转字符串的所有字符(如果删除的字符是**‘0’**)来找到从字符串中删除的最后一个字符。

**示例:**

> **输入:** str = "1001"
> **输出:** '0'
> **解释:**
> 从字符串中移除 str[0]会将 str 修改为“001”。
> 从字符串中删除字符串[0]会将字符串修改为“10”。
> 从字符串中删除字符串[0]会将字符串修改为“0”。
> 由于删除的最后一个字符是“0”，因此所需的输出是“0”。
> 
> **输入:** str = "10010"
> **输出:** '0 '

**天真方法:**解决这个问题最简单的方法是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符。对于遇到的每个字符，删除字符串的第一个字符，并检查删除的字符是否为**“0”**。如果发现是真的，则[翻转字符串的所有字符](https://www.geeksforgeeks.org/queries-to-flip-characters-of-a-binary-string-in-given-range/)。最后，打印上次迭代中删除的字符。按照以下步骤解决问题:

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> **情况 1:**
> 假设 str =“XXXXXXX0X”，其中 X 不是‘0’就是‘1’。
> 如果字符串[N–2]被翻转，那么字符串[N–1]必须被翻转。
> 因此，如果字符串[N–2]是“0”，那么最后删除的字符将是(‘1’–字符串[N–1]+‘0’)。
> **情况 2:**
> 假设 str =“XXXXXXX1X”，其中 X 不是‘0’就是‘1’。
> 如果字符串[N–2]被翻转，那么字符串[N–1]必须被翻转。
> 因此，如果字符串[N–2]为“1”，那么最后删除的字符将是字符串[N–1]。

按照以下步骤解决问题:

*   如果 N 等于 1，则答案是 **str[0]** 本身，否则。
*   检查**字符串【N–2】**(对于 N > =2)是否为**‘1’**。如果发现为真，则打印**字符串【N–1】。**
*   否则，打印**(' 1 '–str[N–1]+' 0 ')**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the last removed
// character from the string
char lastRemovedCharacter(string str)
{
    // Stores length of the string
    int n = str.length();

    // Base Case:
    if (n == 1)
        return str[0];

    // If the second last
    // character is '0'
    if (str[n - 2] == '0') {

        return ('1' - str[n - 1] + '0');
    }

    // If the second last
    // character is '1'
    else
        return str[n - 1];
}

// Driver Code
int main()
{
    string str = "10010";
    cout << lastRemovedCharacter(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the last removed
// character from the String
static char lastRemovedCharacter(char []str)
{
    // Stores length of the String
    int n = str.length;

    // Base Case:
    if (n == 1)
        return str[0];

    // If the second last
    // character is '0'
    if (str[n - 2] == '0') {

        return (char)('1' - str[n - 1] + '0');
    }

    // If the second last
    // character is '1'
    else
        return str[n - 1];
}

// Driver Code
public static void main(String[] args)
{
    String str = "10010";
    System.out.print(lastRemovedCharacter(str.toCharArray()));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the last removed
# character from the string
def lastRemovedCharacter(str):

    # Stores length of the string
    n = len(str)

    # Base Case:
    if (n == 1):
        return ord(str[0])

    # If the second last
    # character is '0'
    if (str[n - 2] == '0'):
        return (ord('1') -
                ord(str[n - 1]) +
                ord('0'))

    # If the second last
    # character is '1'
    else:
        return ord(str[n - 1])

# Driver Code
if __name__ == '__main__':

    str = "10010"

    print(chr(lastRemovedCharacter(str)))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the last removed
// character from the String
static char lastRemovedCharacter(char []str)
{

    // Stores length of the String
    int n = str.Length;

    // Base Case:
    if (n == 1)
        return str[0];

    // If the second last
    // character is '0'
    if (str[n - 2] == '0')
    {
        return (char)('1' - str[n - 1] + '0');
    }

    // If the second last
    // character is '1'
    else
        return str[n - 1];
}

// Driver Code
public static void Main()
{
    string str = "10010";

    Console.Write(lastRemovedCharacter(
        str.ToCharArray()));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach

      // Function to find the last removed
      // character from the string
      function lastRemovedCharacter(str) {
        // Stores length of the string
        var n = str.length;

        // Base Case:
        if (n == 1) return str[0];

        // If the second last
        // character is '0'
        if (str[n - 2] == "0") {
          return "1" - str[n - 1] + "0";
        }

        // If the second last
        // character is '1'
        else return str[n - 1];
      }

      // Driver Code
      var str = "10010";
      document.write(lastRemovedCharacter(str));
    </script>
```

**Output:** 

```
0
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)