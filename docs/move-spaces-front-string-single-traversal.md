# 在单次遍历中将空格移到字符串的前面

> 原文:[https://www . geesforgeks . org/move-spaces-front-string-single-遍历/](https://www.geeksforgeeks.org/move-spaces-front-string-single-traversal/)

给定一个包含单词和空格的字符串，编写一个程序，通过遍历字符串一次，将所有空格移到字符串的前面。

**示例:**

```
Input  : str = "geeks for geeks"
Output : ste = "  geeksforgeeks"

Input  : str = "move these spaces to beginning"
Output : str = "    movethesespacestobeginning"
There were four space characters in input,
all of them should be shifted in front. 
```

**方法 1(使用 Swap)**
思路是从头到尾维护两个索引 I 和 j. Traverse。如果当前索引包含空格，将索引 I 中的字符与索引 j 交换。这将使所有空格都位于数组的开头。

## C++

```
// C++ program to bring all spaces in front of
// string using swapping technique
#include<bits/stdc++.h>
using namespace std;

// Function to find spaces and move to beginning
void moveSpaceInFront(char str[])
{
    // Traverse from end and swap spaces
    int i = strlen(str)-1;
    for (int j = i; j >= 0; j--)
        if (str[j] != ' ')
            swap(str[i--], str[j]);
}

// Driver code
int main()
{
    char str[] = "Hey there, it's GeeksforGeeks";
    moveSpaceInFront(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to bring all spaces in front of
// string using swapping technique
class GFG
{

    // Function to find spaces and move to beginning
    static void moveSpaceInFront(char str[])
    {
        // Traverse from end and swap spaces
        int i = str.length-1;
        for (int j = i; j >= 0; j--)
            if (str[j] != ' ')
            {
                char c = str[i];
                str[i] = str[j];
                str[j] = c;
                i--;
            }
    }   

    // Driver code
    public static void main(String[] args)
    {
        char str[] = "Hey there, it's GeeksforGeeks".toCharArray();
        moveSpaceInFront(str);
        System.out.println(String.valueOf(str));
    }
}

// This code is contributed by
// 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to bring all spaces
# in front of string using swapping technique

# Function to find spaces and move to beginning
def moveSpaceInFront(s):

    # Traverse from end and swap spaces
    i = len(s) - 1;
    for j in range(i, -1, -1):
        if (s[j] != ' '):
            s = swap(s, i, j);
            i -= 1;
    return s;

def swap(c, i, j):
    c = list(c)
    c[i], c[j] = c[j], c[i]
    return ''.join(c)

# Driver code
s = "Hey there, it's GeeksforGeeks";
s = moveSpaceInFront(s);
print(s);

# This code is contributed
# by Princi Singh
```

## C#

```
// C# program to bring all spaces in front of
// string using swapping technique
using System;

class GFG
{

    // Function to find spaces and move to beginning
    static void moveSpaceInFront(char []str)
    {

        // Traverse from end and swap spaces
        int i = str.Length-1;
        for (int j = i; j >= 0; j--)
            if (str[j] != ' ')
            {
                char c = str[i];
                str[i] = str[j];
                str[j] = c;
                i--;
            }
    }

    // Driver code
    public static void Main()
    {
        char []str = "Hey there, it's GeeksforGeeks".ToCharArray();
        moveSpaceInFront(str);
        Console.WriteLine(String.Join("",str));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to bring all spaces
// in front of string using swapping technique

// Function to find spaces and move to beginning
function moveSpaceInFront(str)
{

    // Traverse from end and swap spaces
    let i = str.length-1;
    for(let j = i; j >= 0; j--)
        if (str[j] != ' ')
        {
            let c = str[i];
            str[i] = str[j];
            str[j] = c;
            i--;
        }
}

// Driver code
let str = "Hey there, it's GeeksforGeeks".split("");
moveSpaceInFront(str);

document.write((str).join(""));

// This code is contributed by rag2127

</script>
```

**输出:**

```
   Heythere,it'sGeeksforGeeks
```

**时间复杂度** -: O(n)
**辅助空间** -: O(1)

**方法二(不使用互换)**
思路是复制所有非空格字符到结束。最后复制空格。

## C++

```
// CPP program to bring all spaces in front of
// string using swapping technique
#include<bits/stdc++.h>
using namespace std;

// Function to find spaces and move to beginning
void moveSpaceInFront(char str[])
{
     // Keep copying non-space characters
     int i = strlen(str);
     for (int j=i; j >= 0; j--)
          if (str[j] != ' ')
             str[i--] = str[j];

     // Move spaces to be beginning
     while (i >= 0)
         str[i--] = ' ';
}

// Driver code
int main()
{
    char str[] = "Hey there, it's GeeksforGeeks";
    moveSpaceInFront(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to bring all spaces in front of
// string using swapping technique
class GFG
{

// Function to find spaces and move to beginning
static void moveSpaceInFront(char str[])
{
    // Keep copying non-space characters
    int i = str.length-1;

    for (int j = i; j >= 0; j--)
        if (str[j] != ' ')
            str[i--] = str[j];

    // Move spaces to be beginning
    while (i >= 0)
        str[i--] = ' ';
}

// Driver code
public static void main(String[] args)
{
    char str[] = "Hey there, it's GeeksforGeeks".toCharArray();
    moveSpaceInFront(str);
    System.out.println(String.valueOf(str));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to bring all spaces
# in front of sing using swapping technique

# Function to find spaces and
# move to beginning
def moveSpaceInFront(s):

    # Keep copying non-space characters
    i = len(s) - 1;

    for j in range(i, -1, -1):
        if (s[j] != ' '):
            s = s[:i] + s[j] + s[i + 1:]
            i -= 1;

    # Move spaces to be beginning
    while (i >= 0):
        s = s[:i] + ' ' + s[i + 1:]
        i -= 1
    return s;

# Driver code
s = "Hey there, it's GeeksforGeeks";
s = moveSpaceInFront(s);
print(s);

# This code is contributed
# by Princi Singh
```

## C#

```
// C# program to bring all spaces in front of
// string using swapping technique
using System;

class GFG
{

// Function to find spaces and move to beginning
static void moveSpaceInFront(char []str)
{
    // Keep copying non-space characters
    int i = str.Length-1;

    for (int j = i; j >= 0; j--)
        if (str[j] != ' ')
            str[i--] = str[j];

    // Move spaces to be beginning
    while (i >= 0)
        str[i--] = ' ';
}

// Driver code
public static void Main(String[] args)
{
    char []str = "Hey there, it's GeeksforGeeks".
                                    ToCharArray();
    moveSpaceInFront(str);
    Console.WriteLine(String.Join("",str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to bring all spaces
// in front of string using swapping technique

// Function to find spaces and move to beginning
function moveSpaceInFront(str)
{

    // Keep copying non-space characters
    var i = str.length - 1;

    for(var j = i; j >= 0; j--)
        if (str[j] !== " ")
            str[i--] = str[j];

    // Move spaces to be beginning
    while (i >= 0) str[i--] = " ";
}

// Driver code
var str = "Hey there, it's GeeksforGeeks".split("");
moveSpaceInFront(str);
document.write(str.join(""));

// This code is contributed by rdtank

</script>
```

**输出:**

```
   Heythere,it'sGeeksforGeeks
```

**时间复杂度**-:O(n)
T3】辅助空间 -:O(1)

本文由 **SAKSHI TIWARI** 供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。