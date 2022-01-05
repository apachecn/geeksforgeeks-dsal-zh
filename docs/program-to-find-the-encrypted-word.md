# 查找加密单词的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-encrypted-word/](https://www.geeksforgeeks.org/program-to-find-the-encrypted-word/)

给定一个字符串，给定的字符串是一个加密的单词，任务是解密给定的字符串得到原始单词。

**示例:**

```
Input: str = "abcd"
Output: bdee
Explanation:
a -> a + 1 -> b
b -> b + 2 -> d
c -> c + 2 -> e
d -> d + 1 -> e

Input: str = "xyz"
Output: yaa
Explanation:
x -> x + 1 -> y
y -> y + 2 -> a
z -> z + 1 -> a

```

**进场:**

*   让字符串的长度为 n。
*   那么加密后的字符串将是:
    [![](img/2ce61cf9ed7d9889e207597f120ca44e.png)](https://media.geeksforgeeks.org/wp-content/uploads/20190730174651/CodeCogsEqn-31.png)
*   找到加密的单词后打印字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement 
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the encrypted string
void findWord(string c, int n)
{
    int co = 0, i;

    // to store the encrypted string
    string s(n, ' ');

    for (i = 0; i < n; i++) {
        if (i < n / 2)
            co++;
        else
            co = n - i;

        // after 'z', it should go to a.
        if (c[i] + co <= 122)
            s[i] = (char)((int)c[i] + co);
        else
            s[i] = (char)((int)c[i] + co - 26);
    }
    cout << s;
}

// Driver code
int main()
{
    string s = "abcd";
    findWord(s, s.length());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.*;
import java.io.*;

class GFG
{

// Static function declared to find
// the encrypted string
public static void findWord(String c, int n)
{
    int co = 0, i;

    // Character array to store
    //the encrypted string
    char s[] = new char[n];

    for (i = 0; i < n ; i++)
    {
        if (i < n / 2)
            co++;
        else
            co = n - i;

        // after 'z', it should go to a.
        if ((c.charAt(i) + co) <= 122)
            s[i] = (char)((int)c.charAt(i) + co);
        else
            s[i] = (char)((int)c.charAt(i) + co - 26);
    }

    // storing the character array in the string.
    String str = Arrays.toString(s);
    System.out.println(str);
}

// Driver code
public static void main(String args[])
{
    String s = "abcd";
    findWord(s, s.length());
}
}

// This code is contributed by Animesh_Gupta
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach

# Function to find the encrypted string
def findWord(c, n):
    co = 0

    # to store the encrypted string
    s = [0] * n
    for i in range(n):
        if (i < n / 2):
            co += 1
        else:
            co = n - i

        # after 'z', it should go to a.
        if (ord(c[i]) + co <= 122):
            s[i] = chr(ord(c[i]) + co)
        else:
            s[i] = chr(ord(c[i]) + co - 26)
    print(*s, sep = "")

# Driver code
s = "abcd"
findWord(s, len(s))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to implement the above approach
using System;

class GFG
{

// Static function declared to find
// the encrypted string
public static void findWord(String c, int n)
{
    int co = 0, i;

    // Character array to store
    // the encrypted string
    char []s = new char[n];

    for (i = 0; i < n ; i++)
    {
        if (i < n / 2)
            co++;
        else
            co = n - i;

        // after 'z', it should go to a.
        if ((c[i] + co) <= 122)
            s[i] = (char)((int)c[i] + co);
        else
            s[i] = (char)((int)c[i] + co - 26);
    }

    // storing the character array in the string.
    String str = String.Join("",s);
    Console.WriteLine(str);
}

// Driver code
public static void Main(String []args)
{
    String s = "abcd";
    findWord(s, s.Length);
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
bdee

```

**时间复杂度:** O(N)