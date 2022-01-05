# 通过增加每个字符与单词末尾的距离来修改字符串

> 原文:[https://www . geesforgeks . org/modify-string-by-递增-每个字符与其单词末尾的距离/](https://www.geeksforgeeks.org/modify-string-by-increasing-each-character-by-its-distance-from-the-end-of-the-word/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过用一个新字符替换每个字符 **S[i]** 来修改给定的字符串，该新字符的值为( **S[i] +它在单词**末尾的位置)

**示例:**

> **输入:**S =“ACM fkz”
> **输出:**“CDM hlz”
> **解释:**
> 给定字符串中有 2 个单词{“ACM”、“fkz”}
> 对于“ACM”:
> a 变成‘a’+2 =‘c’
> c 变成‘c’+1 =‘d’
> m 变成‘m’+0 =‘m’
> “ACM”
> 同样，“fkz”变成“hlz”。
> 因此，需要的答案是“cdm hlz”
> 
> **输入:**“极客换极客”
> **输出:**“khgls HPR khgls”

**方法:**思路是[把给定的字符串拆分成单词](https://www.geeksforgeeks.org/split-a-sentence-into-words-in-cpp/)并单独修改每个单词。以下是步骤:

1.  首先，将给定的字符串 **S** 标记为单个单词。
2.  [迭代单词](https://www.geeksforgeeks.org/iterate-over-words-of-a-string-in-python/)并为单词中的每个字符添加其从末尾到它的位置。
3.  然后，将结果单词添加到最后一个字符串中，说 **res** 。
4.  继续重复以上两个步骤，直到字符串中的每个单词都被转换。

以下是上述方法的程序:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to transform and return
// the transformed word
string util(string sub)
{
    int n = sub.length();
    int i = 0;

    // Stores resulting word
    string ret = "";

    // Iterate over the word
    while (i < n)
    {

        // Add the position
        // value to the letter
        int t = (sub[i] - 'a') +
                  n - 1 - i;

        // Convert it back to character
        char ch = (char)(t % 26 + 97);

        // Add it to the string
        ret = ret + ch;

        i++;
    }
    return ret;
}

// Function to transform the
// given string
void manipulate(string s)
{

    // Size of string
    int n = s.length();
    int i = 0, j = 0;

    // Stores resultant string
    string res = "";

    // Iterate over given string
    while (i < n)
    {

        // End of word is reached
        if (s[i] == ' ')
        {

            // Append the word
            res += util(s.substr(j, i));
            res = res + " ";
            j = i + 1;
            i = j + 1;
        }
        else
        {
            i++;
        }
    }

    // For the last word
    res = res + util(s.substr(j, i));

    cout << res << endl;
}

// Driver code
int main()
{

    // Given string
    string s = "acm fkz";

    // Function call
    manipulate(s);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // Function to transform the given string
    public static void manipulate(String s)
    {
        // Size of string
        int n = s.length();
        int i = 0, j = 0;

        // Stores resultant string
        String res = "";

        // Iterate over given string
        while (i < n) {

            // End of word is reached
            if (s.charAt(i) == ' ') {

                // Append the word
                res += util(s.substring(j, i));
                res = res + " ";
                j = i + 1;
                i = j + 1;
            }

            else {
                i++;
            }
        }

        // For the last word
        res = res + util(s.substring(j, i));

        System.out.println(res);
    }

    // Function to transform and return
    // the transformed word
    public static String util(String sub)
    {
        int n = sub.length();
        int i = 0;

        // Stores resulting word
        String ret = "";

        // Iterate over the word
        while (i < n) {

            // Add the position
            // value to the letter
            int t = (sub.charAt(i) - 'a')
                    + n - 1 - i;

            // Convert it back to character
            char ch = (char)(t % 26 + 97);

            // Add it to the string
            ret = ret + String.valueOf(ch);

            i++;
        }

        return ret;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string
        String s = "acm fkz";

        // Function Call
        manipulate(s);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to transform and return
# the transformed word
def util(sub):

    n = len(sub)
    i = 0

    # Stores resulting word
    ret = ""

    # Iterate over the word
    while i < n:

        # Add the position
        # value to the letter
        t = (ord(sub[i]) - 97) + n - 1 - i

        # Convert it back to character
        ch = chr(t % 26 + 97)

        # Add it to the string
        ret = ret + ch

        i = i + 1

    return ret

# Function to transform the
# given string
def manipulate(s):

    # Size of string
    n = len(s)
    i = 0
    j = 0

    # Stores resultant string
    res = ""

    # Iterate over given string
    while i < n:

        # End of word is reached
        if s[i] == ' ':

            # print(s[j:j+i])
            # Append the word
            res += util(s[j : j + i])
            res = res + " "
            j = i + 1
            i = j + 1
        else:
            i = i + 1

    # For the last word
    res = res + util(s[j : j + i])

    print(res)

# Driver code
if __name__ == "__main__":

    # Given string
    s = "acm fkz"

    # Function call
    manipulate(s)

# This code is contributed by akhilsaini
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to transform the given string
public static void manipulate(String s)
{
  // Size of string
  int n = s.Length;
  int i = 0, j = 0;

  // Stores resultant string
  String res = "";

  // Iterate over given string
  while (i < n)
  {
    // End of word is reached
    if (s[i] == ' ')
    {
      // Append the word
      res += util(s.Substring(j, i - j));
      res = res + " ";
      j = i + 1;
      i = j + 1;
    }
    else
    {
      i++;
    }
  }

  // For the last word
  res = res + util(s.Substring(j, i - j));

  Console.WriteLine(res);
}

// Function to transform and return
// the transformed word
public static String util(String sub)
{
  int n = sub.Length;
  int i = 0;

  // Stores resulting word
  String ret = "";

  // Iterate over the word
  while (i < n)
  {
    // Add the position
    // value to the letter
    int t = (sub[i] - 'a') +
             n - 1 - i;

    // Convert it back to character
    char ch = (char)(t % 26 + 97);

    // Add it to the string
    ret = ret + String.Join("", ch);

    i++;
  }

  return ret;
}

// Driver Code
public static void Main(String[] args)
{
  // Given string
  String s = "acm fkz";

  // Function Call
  manipulate(s);
}
}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
cdm hlz

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)