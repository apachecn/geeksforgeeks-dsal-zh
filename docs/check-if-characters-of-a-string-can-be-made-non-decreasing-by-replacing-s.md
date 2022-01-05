# 检查字符串的字符是否可以通过替换“？”而不减少 s

> 原文:[https://www . geesforgeks . org/check-if-characters-of-string-can-non-reduced-by-replacement-s/](https://www.geeksforgeeks.org/check-if-characters-of-a-string-can-be-made-non-decreasing-by-replacing-s/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，由小写英文字母和**“？”**，任务是检查是否有可能通过更换所有**“？”**带英文字母的字符。如果发现是真的，打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S =“abb？xy？”
> **输出:**是
> **解释:**
> 替换“？”索引 3 和 6 中的 S 带有“b”和“z”，将字符串 S 修改为“abbbxyz”，这是不递减的。
> 
> **输入:** S =？？z？一个？”
> T3】输出:否

**天真方法:**解决问题最简单的方法是使用**英文字母**生成所有可能的字符串，并检查结果字符串是否不递减。如果发现属实，打印**“是”**，否则打印**“否”。**

***时间复杂度:**O(N * 26<sup>N</sup>)*
***辅助空间:** O(N)*

**有效方法:** 给定的问题可以基于以下观察来解决:

> *   It can be observed that the only important position is the position of **s [i]! = '?'** , as an alternative to **"?"** The character at the nearest index is not **'?'** 。
> *   Therefore, the task is simplified to check whether the character in the string that does not belong to **is "?"** , whether it is arranged in non-decreasing order.

按照以下步骤解决问题:

*   初始化一个变量，最后说**，**存储最后一个字符，这个不是**'？'。**
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) 并针对每一个 **i** <sup>th</sup> 字符，检查 **S[i]！= '?'**和 **S[i] <最后，**再打印**“否”**。
*   否则，如果 **S[i]，则将**最后一个**更新为**最后一个= S[i]** ！='?'。**
*   如果以上情况都不满足，则打印**“是”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it's possible
// to make the string s non decreasing
int nonDecreasing(string s)
{
    // Stores length of string
    int size = s.length();

    // Stores the last character
    // that is not '?'
    char c = 'a';

    // Traverse the string S
    for (int i = 0; i < size; i++) {

        // If current character
        // of the string is '?'
        if (s[i] == '?') {
            continue;
        }

        // If s[i] is not '?'
        // and is less than C
        else if ((s[i] != '?')
                 && (s[i] < c)) {

            return 0;
        }

        // Otherwise
        else {

            // Update C
            c = s[i];
        }
    }

    // Return 1
    return 1;
}

// Driver Code
int main()
{
    string S = "abb?xy?";

    if (nonDecreasing(S))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to check if it's possible
// to make the String s non decreasing
static int nonDecreasing(char []s)
{

    // Stores length of String
    int size = s.length;

    // Stores the last character
    // that is not '?'
    char c = 'a';

    // Traverse the String S
    for (int i = 0; i < size; i++)
    {

        // If current character
        // of the String is '?'
        if (s[i] == '?')
        {
            continue;
        }

        // If s[i] is not '?'
        // and is less than C
        else if ((s[i] != '?')
                 && (s[i] < c))
        {

            return 0;
        }

        // Otherwise
        else {

            // Update C
            c = s[i];
        }
    }

    // Return 1
    return 1;
}

// Driver Code
public static void main(String[] args)
{
    String S = "abb?xy?";

    if (nonDecreasing(S.toCharArray())==1)
        System.out.print("Yes" +"\n");
    else
        System.out.print("No" +"\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to check if it's possible
# to make the string s non decreasing
def nonDecreasing(s):

    # Stores length of string
    size = len(s)

    # Stores the last character
    # that is not '?'
    c = 'a'

    # Traverse the string S
    for i in range(size):

        # If current character
        # of the string is '?'
        if (s[i] == '?'):
            continue

        # If s[i] is not '?'
        # and is less than C
        elif((s[i] != '?') and (s[i] < c)):
            return 0

        # Otherwise
        else:

            # Update C
            c = s[i]

    # Return 1
    return 1

# Driver Code
if __name__ == '__main__':
    S = "abb?xy?"

    if(nonDecreasing(S)):
        print("Yes")
    else:
        print("No")

        # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to check if it's possible
  // to make the String s non decreasing
  static int nonDecreasing(char []s)
  {

    // Stores length of String
    int size = s.Length;

    // Stores the last character
    // that is not '?'
    char c = 'a';

    // Traverse the String S
    for (int i = 0; i < size; i++)
    {

      // If current character
      // of the String is '?'
      if (s[i] == '?')
      {
        continue;
      }

      // If s[i] is not '?'
      // and is less than C
      else if ((s[i] != '?')
               && (s[i] < c))
      {

        return 0;
      }

      // Otherwise
      else {

        // Update C
        c = s[i];
      }
    }

    // Return 1
    return 1;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String S = "abb?xy?";

    if (nonDecreasing(S.ToCharArray())==1)
      Console.Write("Yes" +"\n");
    else
      Console.Write("No" +"\n");

  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if it's possible
// to make the String s non decreasing
function nonDecreasing(s)
{

    // Stores length of String
    let size = s.length;

    // Stores the last character
    // that is not '?'
    var c = 'a';

    // Traverse the String S
    for(let i = 0; i < size; i++)
    {

        // If current character
        // of the String is '?'
        if (s[i] == '?')
        {
            continue;
        }

        // If s[i] is not '?'
        // and is less than C
        else if ((s[i] != '?') &&
                 (s[i] < c))
        {
            return 0;
        }

        // Otherwise
        else
        {

            // Update C
            c = s[i];
        }
    }

    // Return 1
    return 1;
}

// Driver Code
let S = "abb?xy?";

if (nonDecreasing(S.split('')))
    document.write("Yes" + "\n");
else
    document.write("No" + "\n");

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)