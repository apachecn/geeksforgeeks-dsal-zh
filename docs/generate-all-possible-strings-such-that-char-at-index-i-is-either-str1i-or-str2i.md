# 生成所有可能的字符串，使得索引 I 处的字符为 str1[i]或 str2[i]

> 原文:[https://www . geeksforgeeks . org/generate-all-everything-string-so-char-at-index-I-is-非-str1i-or-str2i/](https://www.geeksforgeeks.org/generate-all-possible-strings-such-that-char-at-index-i-is-either-str1i-or-str2i/)

给定两个长度分别为 **N** 的字符串 **str1** 和 **str2** ，任务是生成并打印所有可能的长度为 **N** 的字符串，使得生成的字符串的索引 **i** 处的字符为 **str1[i]** 或 **str2[i]**
**示例:**

> **输入:**【str 1 = " ABC "，【str 2 = " def】
> **输出:**
> ABC
> 【abf】
> 【AEC】AEF
> 【DBC】
> DBF
> dec【dec】

**方法:**这个问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决，在每次递归调用时，我们需要选择位于 **str1[i]** 的字符或位于 **str2[i]** 的字符，并将其附加到结果字符串中。终止条件是当结果字符串的长度等于给定字符串的长度时。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to generate
// the required strings
void generateStr(char* a, char* b, string s,
                 int count, int len)
{

    // If length of the current string is
    // equal to the length of the given
    // strings then the current string
    // is part of the result
    if (count == len) {
        cout << s << endl;
        return;
    }

    // Choosing the current character
    // from the string a
    generateStr(a + 1, b + 1, s + (*a),
                count + 1, len);

    // Choosing the current character
    // from the string b
    generateStr(a + 1, b + 1, s + (*b),
                count + 1, len);
}

// Driver code
int main()
{
    char *a = "abc", *b = "def";
    int n = strlen(a);

    // Third argument is an empty
    // string that we will be appended
    // in the recursion calls
    // Fourth arguments is the length of
    // the resultant string so far
    generateStr(a, b, "", 0, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Recursive function to generate
    // the required strings
    public static void generateStr(String a, String b,
                                String s, int count, int len)
    {

        // If length of the current string is
        // equal to the length of the given
        // strings then the current string
        // is part of the result
        if (count == len)
        {
            System.out.println(s);
            return;
        }

        // Choosing the current character
        // from the string a
        generateStr(a.substring(1), b.substring(1),
                      s + a.charAt(0), count + 1, len);

        // Choosing the current character
        // from the string b
        generateStr(a.substring(1), b.substring(1),
                    s + b.charAt(0), count + 1, len);
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "abc", b = "def";
        int n = a.length();

        // Third argument is an empty
        // string that we will be appended
        // in the recursion calls
        // Fourth arguments is the length of
        // the resultant string so far
        generateStr(a, b, "", 0, n);

    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to generate
# the required strings
def generateStr(a, b, s, count, len):

    # If length of the current string is
    # equal to the length of the given
    # strings then the current string
    # is part of the result
    if (count == len):
        print(s);
        return;

    # Choosing the current character
    # from the string a
    generateStr(a[1:], b[1:],
                s + a[0], count + 1, len);

    # Choosing the current character
    # from the string b
    generateStr(a[1:], b[1:],
                s + b[0], count + 1, len);

# Driver code
a = "abc"; b = "def";
n = len(a);

# Third argument is an empty
# string that we will be appended
# in the recursion calls
# Fourth arguments is the length of
# the resultant string so far
generateStr(a, b, "", 0, n);

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to generate
    // the required strings
    public static void generateStr(String a, String b,
                                     String s, int count,
                                               int len)
    {

        // If length of the current string is
        // equal to the length of the given
        // strings then the current string
        // is part of the result
        if (count == len)
        {
            Console.WriteLine(s);
            return;
        }

        // Choosing the current character
        // from the string a
        generateStr(a.Substring(1), b.Substring(1),
                    s + a[0], count + 1, len);

        // Choosing the current character
        // from the string b
        generateStr(a.Substring(1), b.Substring(1),
                    s + b[0], count + 1, len);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String a = "abc", b = "def";
        int n = a.Length;

        // Third argument is an empty
        // string that we will be appended
        // in the recursion calls
        // Fourth arguments is the length of
        // the resultant string so far
        generateStr(a, b, "", 0, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

//javascript implementation of the approach

    // Recursive function to generate
    // the required strings
    function generateStr( a, b, s, count, len )
    {

        // If length of the current string is
        // equal to the length of the given
        // strings then the current string
        // is part of the result
        if (count == len)
        {
            document.write(s + "<br>");
            return;
        }

        // Choosing the current character
        // from the string a
        generateStr(a.substring(1), b.substring(1),
                    s + a[0], count + 1, len);

        // Choosing the current character
        // from the string b
        generateStr(a.substring(1), b.substring(1),
                    s + b[0], count + 1, len);
    }

    // Driver code

        var a = "abc", b = "def";
        var n = a.length;

        // Third argument is an empty
        // string that we will be appended
        // in the recursion calls
        // Fourth arguments is the length of
        // the resultant string so far

        generateStr(a, b, "", 0, n);

</script>
```

**Output:** 

```
abc
abf
aec
aef
dbc
dbf
dec
def
```