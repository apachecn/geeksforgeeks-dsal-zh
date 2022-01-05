# 第一个子串，其反义词是字符串中的一个单词

> 原文:[https://www . geeksforgeeks . org/first-substring-with-reverse-is-a-word-in-string/](https://www.geeksforgeeks.org/first-substring-whose-reverse-is-a-word-in-the-string/)

给定一个用空格分隔的字符串 **str** ，任务是找到第一个子字符串，其反义词是字符串中的一个单词。字符串的所有字符都是**小写**英文字母。弦以 **#** 结束。如果不存在这样的子串，返回 **-1**

**示例:**

> **输入:**str = " nan en 尝芒果甜#"
> **输出:** man
> **说明:**子串“man”反过来为“nam”，是给定串中的一个词
> 
> **输入:**str = " hello world # "
> T3】输出: -1

**进场:**

1.  将字符串的所有单词存储在地图上。
2.  查找字符串的所有子字符串。
3.  对于每个子串，检查子串的反向是否是该串的一个单词。如果不存在这样的子串，打印-1。

下面是上述方法的实现。

## C++

```
// C++ program to find first substring
#include <bits/stdc++.h>
using namespace std;

// Function to find first substring
string first_substring(string s)
{
    int n = s.length(), c = 0;
    string s1, s2;
    map<string, int> mpp;

    // Storing the words present in string
    for (int i = 0; i < n; i++) {
        if (s[i] == ' ' || s[i] == '#') {
            s1 = s.substr(c, i - c);
            mpp[s1] = 1;
            c = i + 1;
        }
    }

    // Calculating for all
    // possible valid substring.
    for (int i = 0; i < n; i++) {
        if (s[i] == ' ') {
            continue;
        }
        for (int j = 0; j < n; j++) {
            if (s[j] == ' ') {
                break;
            }
            s1 = s.substr(i, j - i + 1);
            s2 = s1;
            reverse(s1.begin(), s1.end());
            if (mpp[s1]) {
                return s2;
            }
        }
    }
    return "-1";
}
// Driver code
int main()
{
    string s, s1;
    s = "mango is sweet when nam en tastes it#";
    s1 = first_substring(s);
    cout << s1 << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first subString
import java.util.*;

class GFG
{

// Function to find first subString
static String first_subString(String s)
{
    int n = s.length(), c = 0;
    String s1, s2;
    HashMap<String, Integer> mpp =
        new HashMap<String, Integer>();

    // Storing the words present in String
    for (int i = 0; i < n; i++)
    {
        if (s.charAt(i) == ' ' || s.charAt(i) == '#')
        {
            s1 = s.substring(c, i);
            mpp.put(s1, 1);
            c = i + 1;
        }
    }

    // Calculating for all
    // possible valid subString.
    for (int i = 0; i < n; i++)
    {
        if (s.charAt(i) == ' ')
        {
            continue;
        }
        for (int j = 0; j < n; j++)
        {
            if (s.charAt(i) == ' ')
            {
                break;
            }
            s1 = s.substring(i, j - i + 1);
            s2 = s1;
            s1 = reverse(s1);
            if (mpp.containsKey(s1))
            {
                return s2;
            }
        }
    }
    return "-1";
}
static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver code
public static void main(String[] args)
{
    String s, s1;
    s = "mango is sweet when nam en tastes it#";
    s1 = first_subString(s);
    System.out.print(s1+ "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find first substring

# Function to find first substring
def first_substring(s) :

    n = len(s); c = 0;
    mpp = {};

    # Storing the words present in string
    for i in range(n) :
        if (s[i] == ' ' or s[i] == '#') :
            s1 = s[c: i];
            mpp[s1] = 1;
            c = i + 1;

    # Calculating for all
    # possible valid substring.
    for i in range(n) :
        if (s[i] == ' ') :
            continue;

        for j in range(n) :
            if (s[j] == ' ') :
                break;

            s1 = s[i : j + 1];
            s2 = s1;
            s1 = s1[::-1];

            if s1 in mpp :
                if mpp[s1] :
                    return s2;

    return "-1";

# Driver code
if __name__ == "__main__" :

    s = "mango is sweet when nam en tastes it#";
    s1 = first_substring(s);
    print(s1);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find first subString
using System;
using System.Collections.Generic;

class GFG
{

// Function to find first subString
static String first_subString(String s)
{
    int n = s.Length, c = 0;
    String s1, s2;
    Dictionary<String, int> mpp =
        new Dictionary<String, int>();

    // Storing the words present in String
    for (int i = 0; i < n; i++)
    {
        if (s[i] == ' ' || s[i] == '#')
        {
            s1 = s.Substring(c, i - c);
            mpp.Add(s1, 1);
            c = i + 1;
        }
    }

    // Calculating for all
    // possible valid subString.
    for (int i = 0; i < n; i++)
    {
        if (s[i] == ' ')
        {
            continue;
        }
        for (int j = 0; j < n; j++)
        {
            if (s[i] == ' ')
            {
                break;
            }
            s1 = s.Substring(i, j - i + 1);
            s2 = s1;
            s1 = reverse(s1);
            if (mpp.ContainsKey(s1))
            {
                return s2;
            }
        }
    }
    return "-1";
}
static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("", a);
}

// Driver code
public static void Main(String[] args)
{
    String s, s1;
    s = "mango is sweet when nam en tastes it#";
    s1 = first_subString(s);
    Console.Write(s1 + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find first substring

// Function to find first substring
function first_substring(s)
{
    var n = s.length, c = 0;
    var s1, s2;
    var mpp = new Map();

    // Storing the words present in string
    for (var i = 0; i < n; i++) {
        if (s[i] == ' ' || s[i] == '#') {
            s1 = s.substring(c, i);
            mpp.set(s1, 1);
            c = i + 1;
        }
    }

    // Calculating for all
    // possible valid substring.
    for (var i = 0; i < n; i++) {
        if (s[i] == ' ') {
            continue;
        }
        for (var j = 0; j < n; j++) {
            if (s[j] == ' ') {
                break;
            }
            s1 = s.substring(i, j + 1);
            s2 = s1;
            s1 = s1.split('').reverse().join('');

            if (mpp.has(s1)) {
                return s2;
            }
        }
    }
    return "-1";
}
// Driver code
var s, s1;
s = "mango is sweet when nam en tastes it#";
s1 = first_substring(s);
document.write( s1 );

</script>
```

**Output:** 

```
man
```