# 用于切换字符串中所有字符的程序

> 原文:[https://www . geesforgeks . org/program-toggle-characters-string/](https://www.geeksforgeeks.org/program-toggle-characters-string/)

给定一个字符串，任务是切换该字符串的所有字符，即将大写转换为小写，反之亦然。

**示例:**

```
Input  : gfg
Output : GFG

Input  : aBc12#
Output : AbC12#

Input  : tu@kmiNi
Output : TU@KMInI
```

遍历给定的字符串，如果出现大写字符，转换成小写，小写字母转换成大写。

## C++

```
// C++ program to toggle all characters
#include<bits/stdc++.h>
using namespace std;

void toggleChars(char str[])
{
    for (int i=0; str[i]!='\0'; i++)
    {
        if (str[i]>='A' && str[i]<='Z')
            str[i] = str[i] + 'a' - 'A';
        else if (str[i]>='a' && str[i]<='z')
            str[i] = str[i] + 'A' - 'a';
    }
}

// Driver code
int main()
{
    char str[] = "GeKf@rGeek{content}quot;;
    toggleChars(str);
    cout << "String after toggle " << endl;
    cout << str << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle all characters

class GFG
{

static void toggleChars(char str[])
{
    for (int i=0; i<str.length; i++)
    {
        if (str[i]>='A' && str[i]<='Z')
            str[i] = (char) (str[i] + 'a' - 'A');
        else if (str[i]>='a' && str[i]<='z')
            str[i] = (char) (str[i] + 'A' - 'a');
    }
}

// Driver code
public static void main(String[] args)
{
    char str[] = "GeKf@rGeek{content}quot;.toCharArray();
    toggleChars(str);
    System.out.println("String after toggle ");
    System.out.println(String.valueOf(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to toggle all characters
def toggleChars(str):

    for i in range(len(str)):
        if (str[i] >= 'A' and str[i] <= 'Z'):
            str = str[:i] + chr(ord(str[i]) + \
                     ord('a') - ord('A')) + str[i + 1:];
        elif (str[i] >= 'a' and str[i] <= 'z'):
            str = str[:i] + chr(ord(str[i]) + \
                     ord('A') - ord('a')) + str[i + 1:];
    return str;

# Driver code
str = "GeKf@rGeek{content}quot;;
str = toggleChars(str);
print(str);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to toggle all characters
using System;

class GFG
{

static void toggleChars(char []str)
{
    for (int i = 0; i < str.Length; i++)
    {
        if (str[i] >= 'A' && str[i] <= 'Z')
            str[i] = (char) (str[i] + 'a' - 'A');
        else if (str[i] >= 'a' && str[i] <= 'z')
            str[i] = (char) (str[i] + 'A' - 'a');
    }
}

// Driver code
public static void Main(String[] args)
{
    char []str = "GeKf@rGeek{content}quot;.ToCharArray();
    toggleChars(str);
    Console.WriteLine("String after toggle ");
    Console.WriteLine(String.Join("",str));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

function toggleChars(str)
{
    for (let i = 0; i < str.length; i++)
    {
        if (str[i] >= 'A' && str[i] <= 'Z')
            str[i] =  String.fromCharCode(str[i].charCodeAt(0) + 'a'.charCodeAt(0) - 'A'.charCodeAt(0));
        else if (str[i] >= 'a' && str[i] <= 'z')
            str[i] =  String.fromCharCode(str[i].charCodeAt(0) + 'A'.charCodeAt(0) - 'a'.charCodeAt(0));
    }
}

let str = "GeKf@rGeek{content}quot;.split("");
toggleChars(str);
document.write("String after toggle ");
document.write((str).join(""));

// This code is contributed by rag2127.
</script>
```

**输出:**

```
gEkF@RgEEK$
```

本文由 **MATHE_KA_BANDA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。