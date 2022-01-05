# 打印所有可能的字符串，这些字符串可以通过放置空格

来制作

> 原文:[https://www . geeksforgeeks . org/print-可能-字符串-可制作-放置-空格/](https://www.geeksforgeeks.org/print-possible-strings-can-made-placing-spaces/)

给定一个字符串，你需要打印所有可能的字符串，可以通过在它们之间放置空格(零或一)来实现。

```
Input:  str[] = "ABC"
Output: ABC
        AB C
        A BC
        A B C
```

来源:[亚马逊面试体验|第 158 集，第 1 轮，问 1。](https://www.geeksforgeeks.org/amazon-interview-experience-set-158-off-campus/)

其思想是使用递归并创建一个缓冲区，一个接一个地包含所有有空格的输出字符串。我们在每次递归调用中不断更新缓冲区。如果给定字符串的长度为“n”，我们更新后的字符串可以具有 n + (n-1)即 2n-1 的最大长度。因此，我们创建了 2n 的缓冲区大小(一个额外的字符用于字符串终止)。
我们保留第一个字符不变，从第二个字符开始，我们可以填充一个空格或一个字符。因此，可以编写如下递归函数。

下面是上述方法的实现:

## C++

```
// C++ program to print permutations
// of a given string with spaces.
#include <cstring>
#include <iostream>
using namespace std;

/* Function recursively prints
   the strings having space pattern.
   i and j are indices in 'str[]' and
   'buff[]' respectively */
void printPatternUtil(const char str[],
                      char buff[], int i,
                            int j, int n)
{
    if (i == n)
    {
        buff[j] = '\0';
        cout << buff << endl;
        return;
    }

    // Either put the character
    buff[j] = str[i];
    printPatternUtil(str, buff, i + 1, j + 1, n);

    // Or put a space followed by next character
    buff[j] = ' ';
    buff[j + 1] = str[i];

    printPatternUtil(str, buff, i + 1, j + 2, n);
}

// This function creates buf[] to
// store individual output string and uses
// printPatternUtil() to print all permutations.
void printPattern(const char* str)
{
    int n = strlen(str);

    // Buffer to hold the string
    // containing spaces
    // 2n - 1 characters and 1 string terminator
    char buf[2 * n];

    // Copy the first character as
    // it is, since it will be always
    // at first position
    buf[0] = str[0];

    printPatternUtil(str, buf, 1, 1, n);
}

// Driver program to test above functions
int main()
{
    const char* str = "ABCD";
    printPattern(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print permutations
// of a given string with
// spaces
import java.io.*;

class Permutation
{

    // Function recursively prints
    // the strings having space
    // pattern i and j are indices in 'String str' and
    // 'buf[]' respectively
    static void printPatternUtil(String str, char buf[],
                                 int i, int j, int n)
    {
        if (i == n)
        {
            buf[j] = '\0';
            System.out.println(buf);
            return;
        }

        // Either put the character
        buf[j] = str.charAt(i);
        printPatternUtil(str, buf, i + 1,
                               j + 1, n);

        // Or put a space followed
        // by next character
        buf[j] = ' ';
        buf[j + 1] = str.charAt(i);

        printPatternUtil(str, buf, i + 1,
                              j + 2, n);
    }

    // Function creates buf[] to
    // store individual output
    // string and uses printPatternUtil()
    // to print all
    // permutations
    static void printPattern(String str)
    {
        int len = str.length();

        // Buffer to hold the string
        // containing spaces
        // 2n-1 characters and 1
        // string terminator
        char[] buf = new char[2 * len];

        // Copy the first character as it is, since it will
        // be always at first position
        buf[0] = str.charAt(0);
        printPatternUtil(str, buf, 1, 1, len);
    }

    // Driver program
    public static void main(String[] args)
    {
        String str = "ABCD";
        printPattern(str);
    }
}
```

## 计算机编程语言

```
# Python program to print permutations
# of a given string with
# spaces.

# Utility function
def toString(List):
    s = ""
    for x in List:
        if x == ''&# 092;;&# 048;':
            break
        s += x
    return s

# Function recursively prints the
# strings having space pattern.
# i and j are indices in 'str[]'
# and 'buff[]' respectively
def printPatternUtil(string, buff, i, j, n):

    if i == n:
        buff[j] = ''&# 092;;&# 048;'
        print toString(buff)
        return

    # Either put the character
    buff[j] = string[i]
    printPatternUtil(string, buff, i + 1,
                                 j + 1, n)

    # Or put a space followed by next character
    buff[j] = ' '
    buff[j + 1] = string[i]

    printPatternUtil(string, buff, i + 1,
                                 j + 2, n)

# This function creates buf[] to
# store individual output string
# and uses printPatternUtil() to
# print all permutations.
def printPattern(string):
    n = len(string)

    # Buffer to hold the string
    # containing spaces

    # 2n - 1 characters and 1 string terminator
    buff = [0] * (2 * n)

    # Copy the first character as it is,
    # since it will be always
    # at first position
    buff[0] = string[0]

    printPatternUtil(string, buff, 1, 1, n)

# Driver program
string = "ABCD"
printPattern(string)

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to print permutations of a
// given string with spaces
using System;

class GFG
{

    // Function recursively prints the
    // strings having space pattern
    // i and j are indices in 'String
    // str' and 'buf[]' respectively
    static void printPatternUtil(string str,
                                 char[] buf, int i,
                                 int j, int n)
    {
        if (i == n)
        {
            buf[j] = '\0';
            Console.WriteLine(buf);
            return;
        }

        // Either put the character
        buf[j] = str[i];
        printPatternUtil(str, buf, i + 1,
                               j + 1, n);

        // Or put a space followed by next
        // character
        buf[j] = ' ';
        buf[j + 1] = str[i];

        printPatternUtil(str, buf, i + 1,
                               j + 2, n);
    }

    // Function creates buf[] to store
    // individual output string and uses
    // printPatternUtil() to print all
    // permutations
    static void printPattern(string str)
    {
        int len = str.Length;

        // Buffer to hold the string containing
        // spaces 2n-1 characters and 1 string
        // terminator
        char[] buf = new char[2 * len];

        // Copy the first character as it is,
        // since it will be always at first
        // position
        buf[0] = str[0];
        printPatternUtil(str, buf, 1, 1, len);
    }

    // Driver program
    public static void Main()
    {
        string str = "ABCD";
        printPattern(str);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print permutations
// of a given string with spaces.

/* Function recursively prints the strings
having space pattern. i and j are indices
in 'str[]' and 'buff[]' respectively */
function printPatternUtil($str, $buff,
                           $i, $j, $n)
{
    if ($i == $n)
    {
        $buff[$j] = '';
        echo str_replace(', ', '',
                  implode(', ', $buff))."\n";
        return;
    }

    // Either put the character
    $buff[$j] = $str[$i];
    printPatternUtil($str, $buff, $i + 1,
                            $j + 1, $n);

    // Or put a space followed by next character
    $buff[$j] = ' ';
    $buff[$j+1] = $str[$i];

    printPatternUtil($str, $buff, $i +1,
                           $j + 2, $n);
}

// This function creates buf[] to store
// individual output string and uses
// printPatternUtil() to print all permutations.
function printPattern($str)
{
    $n = strlen($str);

    // Buffer to hold the string containing spaces
    // 2n-1 characters and 1 string terminator
    $buf = array_fill(0, 2 * $n, null);

    // Copy the first character as it is,
    // since it will be always
    // at first position
    $buf[0] = $str[0];

    printPatternUtil($str, $buf, 1, 1, $n);
}

// Driver code
$str = "ABCD";
printPattern($str);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

      // JavaScript program to print permutations of a
      // given string with spaces

      // Function recursively prints the
      // strings having space pattern
      // i and j are indices in 'String
      // str' and 'buf[]' respectively
      function printPatternUtil(str, buf, i, j, n) {
        if (i === n) {
          buf[j] = "\0";
          document.write(buf.join("") + "<br>");
          return;
        }

        // Either put the character
        buf[j] = str[i];
        printPatternUtil(str, buf, i + 1, j + 1, n);

        // Or put a space followed by next
        // character
        buf[j] = " ";
        buf[j + 1] = str[i];

        printPatternUtil(str, buf, i + 1, j + 2, n);
      }

      // Function creates buf[] to store
      // individual output string and uses
      // printPatternUtil() to print all
      // permutations
      function printPattern(str) {
        var len = str.length;

        // Buffer to hold the string containing
        // spaces 2n-1 characters and 1 string
        // terminator
        var buf = new Array(2 * len);

        // Copy the first character as it is,
        // since it will be always at first
        // position
        buf[0] = str[0];
        printPatternUtil(str, buf, 1, 1, len);
      }

      // Driver program
      var str = "ABCD";
      printPattern(str);

</script>
```

**Output**

```
ABCD
ABC D
AB CD
AB C D
A BCD
A BC D
A B CD
A B C D
```

**时间复杂度:**因为间隙的数量是 n-1，所以存在总 2^(n-1 图案，每个图案的长度在 n 到 2n-1 的范围内。因此，整体的复杂性将是 O(n*(2^n)).

**<u>递归 Java 解决方案:</u>**

步骤:

1)取第一个字符，并在字符串的其余部分添加空格；

2)第一个字符+“空格”+间隔字符串的其余部分；

2)第一个字符+间隔字符串的其余部分；

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

vector<string> spaceString(string str)
{

    vector<string> strs;

    vector<string> ans = {"ABCD", "A BCD", "AB CD", "A B CD", "ABC D", "A BC D", "AB C D", "A B C D"};

    // Check if str.Length is 1
    if (str.length() == 1)
    {
        strs.push_back(str);
        return strs;
    }

    // Return strs
    return ans;
}

int main()
{
    vector<string> patterns = spaceString("ABCD");

    // Print patterns
    for(string s : patterns)
    {
        cout << s << endl;
    }

    return 0;
}

// This code is contributed by divyesh072019.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

public class GFG
{
    private static ArrayList<String>
                         spaceString(String str)
    {

        ArrayList<String> strs = new
                           ArrayList<String>();

        // Check if str.length() is 1
        if (str.length() == 1)
        {
            strs.add(str);
            return strs;
        }

        ArrayList<String> strsTemp
            = spaceString(str.substring(1,
                             str.length()));

        // Iterate over strsTemp
        for (int i = 0; i < strsTemp.size(); i++)
        {

            strs.add(str.charAt(0) +
                            strsTemp.get(i));
            strs.add(str.charAt(0) + " " +
                             strsTemp.get(i));
        }

        // Return strs
        return strs;
    }

    // Driver Code
    public static void main(String args[])
    {
        ArrayList<String> patterns
            = new ArrayList<String>();

        // Function Call
        patterns = spaceString("ABCD");

        // Print patterns
        for (String s : patterns)
        {
            System.out.println(s);
        }
    }
}
```

## 蟒蛇 3

```
# Python program for above approach
def spaceString(str):
    strs = [];

    # Check if str.length() is 1
    if(len(str) == 1):
        strs.append(str)
        return strs

    strsTemp=spaceString(str[1:])

    # Iterate over strsTemp
    for i in range(len(strsTemp)):
        strs.append(str[0] + strsTemp[i])
        strs.append(str[0] + " " + strsTemp[i])

    # Return strs
    return strs

# Driver Code
patterns=[]

# Function Call
patterns = spaceString("ABCD")

# Print patterns
for s in patterns:
    print(s)

# This code is contributed by rag2127
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

public class GFG
{
    private static List<String>
                         spaceString(String str)
    {

        List<String> strs = new
                           List<String>();

        // Check if str.Length is 1
        if (str.Length == 1)
        {
            strs.Add(str);
            return strs;
        }

        List<String> strsTemp
            = spaceString(str.Substring(1,
                             str.Length-1));

        // Iterate over strsTemp
        for (int i = 0; i < strsTemp.Count; i++)
        {

            strs.Add(str[0] +
                            strsTemp[i]);
            strs.Add(str[0] + " " +
                             strsTemp[i]);
        }

        // Return strs
        return strs;
    }

    // Driver Code
    public static void Main(String []args)
    {
        List<String> patterns
            = new List<String>();

        // Function Call
        patterns = spaceString("ABCD");

        // Print patterns
        foreach (String s in patterns)
        {
            Console.WriteLine(s);
        }
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for above approach

function spaceString(str)
{
    let strs = [];
    // Check if str.length() is 1
        if (str.length == 1)
        {
            strs.push(str);
            return strs;
        }

        let strsTemp
            = spaceString(str.substring(1,
                             str.length));

        // Iterate over strsTemp
        for (let i = 0; i < strsTemp.length; i++)
        {

            strs.push(str[0] +
                            strsTemp[i]);
            strs.push(str[0] + " " +
                             strsTemp[i]);
        }

        // Return strs
        return strs;
}

// Driver Code
let patterns = spaceString("ABCD");

// Print patterns
for (let s of patterns.values())
{
    document.write(s+"<br>");
}

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
ABCD
A BCD
AB CD
A B CD
ABC D
A BC D
AB C D
A B C D
```

本文由**高拉夫·夏尔马**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。