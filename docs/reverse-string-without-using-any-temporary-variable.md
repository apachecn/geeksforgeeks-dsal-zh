# 不使用任何临时变量反转字符串

> 原文:[https://www . geesforgeks . org/reverse-string-不带任何临时变量/](https://www.geeksforgeeks.org/reverse-string-without-using-any-temporary-variable/)

我们有一根绳子。我们还获得了字符串中第一个和最后一个字符的索引。任务是在不使用任何额外变量的情况下反转字符串。

**示例:**

```
Input  : str = "abc"
Output : str = "cba" 

Input :  str = "GeeksforGeeks"
Output : str = "skeeGrofskeeG"
```

如果我们看一下[程序反转一个字符串或者数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)，我们需要做的就是交换两个字符。这个想法是用[异或来交换变量](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)。下面是这个想法的实现。

## C++

```
// C++ Program to reverse a string without
// using temp variable
#include <bits/stdc++.h>
using namespace std;

// Function to reverse string and return revesed string
string reversingString(string str, int start, int end)
{
    // Iterate loop upto start not equal to end
    while (start < end)
    {
        // XOR for swapping the variable
        str[start] ^= str[end];
        str[end] ^= str[start];
        str[start] ^= str[end];

        ++start;
        --end;
    }
    return str;
}

// Driver Code
int main()
{
    string s = "GeeksforGeeks";
    cout << reversingString(s, 0, 12);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to reverse a string without
// using temp variable
import java.util.*;

class GFG
{

// Function to reverse string and
// return revesed string
static String reversingString(char []str,
                               int start,
                               int end)
{
    // Iterate loop upto start not equal to end
    while (start < end)
    {
        // XOR for swapping the variable
        str[start] ^= str[end];
        str[end] ^= str[start];
        str[start] ^= str[end];

        ++start;
        --end;
    }
    return String.valueOf(str);
}

// Driver Code
public static void main(String[] args)
{
    String s = "GeeksforGeeks";
    System.out.println(reversingString
                      (s.toCharArray(), 0, 12));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to reverse a string
# without using temp variable

# Function to reverse string and
# return reversed string
def reversingString(str, start, end):

    # Iterate loop upto start not equal to end
    while (start < end):

        # XOR for swapping the variable
        str = (str[:start] + chr(ord(str[start]) ^
                                 ord(str[end])) +
                                 str[start + 1:]);
        str = (str[:end] + chr(ord(str[start]) ^
                               ord(str[end])) +
                               str[end + 1:]);
        str = (str[:start] + chr(ord(str[start]) ^
                                 ord(str[end])) +
                                 str[start + 1:]);

        start += 1;
        end -= 1;
    return str;

# Driver Code
s = "GeeksforGeeks";
print(reversingString(s, 0, 12));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# Program to reverse a string without
// using temp variable
using System;

class GFG
{

// Function to reverse string and
// return revesed string
static String reversingString(char []str,
                              int start,
                              int end)
{
    // Iterate loop upto start
    // not equal to end
    while (start < end)
    {
        // XOR for swapping the variable
        str[start] ^= str[end];
        str[end] ^= str[start];
        str[start] ^= str[end];

        ++start;
        --end;
    }
    return String.Join("", str);
}

// Driver Code
public static void Main(String[] args)
{
    String s = "GeeksforGeeks";
    Console.WriteLine(reversingString
                     (s.ToCharArray(), 0, 12));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to reverse a string
// without using temp variable

// Function to reverse string and
// return revesed string
function reversingString(str, start, end)
{

    // Iterate loop upto start not
    // equal to end
    while (start < end)
    {

        // XOR for swapping the variable
        str[start] = String.fromCharCode(
            str[start].charCodeAt(0) ^
            str[end].charCodeAt(0));
        str[end] = String.fromCharCode(
            str[end].charCodeAt(0) ^
            str[start].charCodeAt(0));
        str[start] = String.fromCharCode(
            str[start].charCodeAt(0) ^
            str[end].charCodeAt(0));

        ++start;
        --end;
    }
    return(str).join("");
}

// Driver Code
let s = "GeeksforGeeks";
document.write(reversingString(
    s.split(""), 0, 12));

// This code is contributed by rag2127

</script>
```

**输出:**

```
skeeGrofskeeG
```

如果允许我们库函数，我们也可以用[中讨论的思路在 C++中快速反转一个字符串](https://www.geeksforgeeks.org/quickly-reverse-string-c/)。我们甚至不需要第一个和最后一个字符的索引。

## C++

```
// Reversing a string using reverse()
#include<bits/stdc++.h>
using namespace std;

int main()
{
   string str = "geeksforgeeks";

   // Reverse str[begin..end]
   reverse(str.begin(), str.end());

   cout << str;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Reversing a string using reverse()
class GFG
{
public static void main(String[] args)
{
    StringBuilder str = new StringBuilder("geeksforgeeks");

    // Reverse str[begin..end]
    str.reverse();
    System.out.println(str);
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Reversing a string using reverse()
str = "geeksforgeeks";

# Reverse str[begin..end]
str = "".join(reversed(str))

print(str);

# This code is contributed by 29AjayKumar
```

## C#

```
// Reversing a string using reverse()
using System;
using System.Linq;                

class GFG
{
public static void Main(String[] args)
{
    String str = "geeksforgeeks";

    // Reverse str[begin..end]
    str = new string(str.Reverse().ToArray());
    Console.WriteLine(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Reversing a string using reverse()

    function reverseString(str) {
        return str.split("").reverse().join("");
    }

        var str = ("geeksforgeeks");

        document.write(reverseString(str));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
skeegrofskeeg

```

https://www.youtube.com/watch?v=Y

-UR3ravjRE

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。