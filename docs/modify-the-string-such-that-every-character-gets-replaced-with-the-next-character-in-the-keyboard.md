# 修改字符串，使每个字符都被替换为键盘中的下一个字符

> 原文:[https://www . geeksforgeeks . org/修改字符串，使每个字符都被替换为键盘中的下一个字符/](https://www.geeksforgeeks.org/modify-the-string-such-that-every-character-gets-replaced-with-the-next-character-in-the-keyboard/)

给定一个由小写英文字母组成的字符串。任务是用键盘上的下一个字母(以圆形方式)键改变字符串的每个字符。例如，**‘a’**替换为**‘T5’，**‘b’**替换为**‘n’**，…..，**‘l’**替换为**‘z’**，…..，**‘m’**替换为**‘q’**。
**例:**** 

> **输入:** str = "极客"
> **输出:** hrrld
> **输入:** str = "plmabc"
> **输出:** azqsnv

**方法:**对于英语字母表中的每个小写字符，在[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中将其旁边的字符插入键盘。现在逐个字符遍历给定的字符串，并用之前创建的映射更新每个字符。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const string CHARS = "qwertyuiopasdfghjklzxcvbnm";
const int MAX = 26;

// Function to return the modified string
string getString(string str, int n)
{

    // Map to store the next character
    // on the keyboard for every
    // possible lowercase character
    unordered_map<char, char> uMap;
    for (int i = 0; i < MAX; i++) {
        uMap[CHARS[i]] = CHARS[(i + 1) % MAX];
    }

    // Update the string
    for (int i = 0; i < n; i++) {
        str[i] = uMap[str[i]];
    }

    return str;
}

// Driver code
int main()
{
    string str = "geeks";
    int n = str.length();

    cout << getString(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static String CHARS = "qwertyuiopasdfghjklzxcvbnm";
static int MAX = 26;

// Function to return the modified String
static String getString(char[] str, int n)
{

    // Map to store the next character
    // on the keyboard for every
    // possible lowercase character
    Map<Character, Character> uMap = new HashMap<>();
    for (int i = 0; i < MAX; i++)
    {
        uMap. put(CHARS.charAt(i),
                  CHARS.charAt((i + 1) % MAX));
    }

    // Update the String
    for (int i = 0; i < n; i++)
    {
        str[i] = uMap.get(str[i]);
    }
    return String.valueOf(str);
}

// Driver code
public static void main(String []args)
{
    String str = "geeks";
    int n = str.length();

    System.out.println(getString(str.toCharArray(), n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

CHARS = "qwertyuiopasdfghjklzxcvbnm";
MAX = 26;

# Function to return the modified string
def getString(string, n) :

    string = list(string);

    # Map to store the next character
    # on the keyboard for every
    # possible lowercase character
    uMap = {};

    for i in range(MAX) :
        uMap[CHARS[i]] = CHARS[(i + 1) % MAX];

    # Update the string
    for i in range(n) :
        string[i] = uMap[string[i]];

    return "".join(string);

# Driver code
if __name__ == "__main__" :

    string = "geeks";
    n = len(string);

    print(getString(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static String CHARS = "qwertyuiopasdfghjklzxcvbnm";
static int MAX = 26;

// Function to return the modified String
static String getString(char[] str, int n)
{

    // Map to store the next character
    // on the keyboard for every
    // possible lowercase character
    Dictionary<char,
               char> uMap = new Dictionary<char,   
                                           char>();
    for (int i = 0; i < MAX; i++)
    {
        if(!uMap.ContainsKey(CHARS[i]))
            uMap.Add(CHARS[i], CHARS[(i + 1) % MAX]);
        else
            uMap[CHARS[i]] = CHARS[(i + 1) % MAX];
    }

    // Update the String
    for (int i = 0; i < n; i++)
    {
        str[i] = uMap[str[i]];
    }
    return String.Join("", str);
}

// Driver code
public static void Main(String []args)
{
    String str = "geeks";
    int n = str.Length;

    Console.WriteLine(getString(str.ToCharArray(), n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      var CHARS = "qwertyuiopasdfghjklzxcvbnm";
      var MAX = 26;

      // Function to return the modified string
      function getString(string, n) {
        var string = string.split("");

        // Map to store the next character
        // on the keyboard for every
        // possible lowercase character
        uMap = [];

        for (let i = 0; i < MAX; i++) {
          uMap[CHARS[i]] = CHARS[(i + 1) % MAX];
        }
        // Update the string
        for (let i = 0; i < n; i++) {
          string[i] = uMap[string[i]];
        }
        return string.join("");
      }
      // Driver code
      var string = "geeks";
      var n = string.length;

      document.write(getString(string, n));
    </script>
```

**Output:** 

```
hrrld
```