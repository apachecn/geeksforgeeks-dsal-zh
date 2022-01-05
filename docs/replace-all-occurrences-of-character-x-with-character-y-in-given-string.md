# 将给定字符串中出现的所有字符 X 替换为字符 Y

> 原文:[https://www . geesforgeks . org/将所有出现的字符 x 替换为给定字符串中的字符 y/](https://www.geeksforgeeks.org/replace-all-occurrences-of-character-x-with-character-y-in-given-string/)

给定一个字符串 **str** 和两个字符 **X** 和 **Y** ，任务是编写一个递归函数，用字符 **Y** 替换所有出现的字符 **X** 。

**示例:**

> **输入:** str = abacd，X = a，Y = X
> T3】输出: xbxcd
> 
> **输入:** str = abacd，X = e，Y = Y
> T3】输出: abacd

**迭代方法:**思想是迭代给定的字符串，如果找到任何字符 **X** ，则用 **Y** 替换该字符。

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*

**递归方法:**思想是递归遍历给定的字符串，用值 **X** 替换字符为 **Y** 。以下是步骤:

1.  获取字符串**字符串**，字符 **X** ，以及 **Y** 。
2.  递归地从索引 **0** 迭代到**字符串长度**。
    *   **基本情况:**如果我们到达字符串的末尾，函数的出口。

```
if(str[0]=='\0')
   return ;
```

*   **递归调用:**如果不满足基本大小写，则检查**第 0 个**索引处的字符，如果是 **X** ，则用 **Y** 替换该字符，并递归迭代下一个字符。

```
if(str[0]==X) 
  str[0] = Y
```

*   **Return 语句:**每次递归调用时(基本情况除外)，返回下一次迭代的递归函数。

```
return recursive_function(str + 1, X, Y)
```

下面是递归实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace all occurrences
// of character c1 with character c2
void replaceCharacter(char input[],
                    char c1, char c2)
{
    // Base Case
    // If the string is empty
    if (input[0] == '\0') {
        return;
    }

    // If the character at starting
    // of the given string is equal
    // to c1, replace it with c2
    if (input[0] == c1) {
        input[0] = c2;
    }

    // Getting the answer from recursion
    // for the smaller problem
    return replaceCharacter(input + 1,
                            c1, c2);
}

// Driver Code
int main()
{
    // Given string
    char str[] = "abacd";
    char c1 = 'a';
    char c2 = 'x';

    // Function call
    replaceCharacter(str, c1, c2);

    // Print the string
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to replace all occurrences
// of character c1 with character c2
static String replaceCharacter(String str,
                             char c1, char c2)
{
    // Base Case
    // If the string is empty
    if (str.length() == 1)
    {
        return str;
    }
    char x=str.charAt(0);
    // If the character at starting
    // of the given string is equal
    // to c1, replace it with c2
    if (str.charAt(0) == c1)
    {
        x=c2;
        str = c2+str.substring(1);
    }

    // Getting the answer from recursion
    // for the smaller problem
    return x+replaceCharacter(str.substring(1),
                            c1, c2);
}

// Driver Code
public static void main(String[] args)
{

    // Given string
    String str = "abacd";
    char c1 = 'a';
    char c2 = 'x';

    // Function call
    System.out.println(replaceCharacter(str, c1, c2));
}
}

// This code is contributed by cyrus18
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to replace all occurrences
# of character c1 with character c2
def replaceCharacter(input, c1, c2):

    input = list(str)

    # If the character at starting
    # of the given string is equal
    # to c1, replace it with c2
    for i in range(0, len(str)):
        if (input[i] == c1):
            input[i] = c2;

        # Print the string
        print(input[i], end = "")

# Driver Code

# Given string
str = "abacd"
c1 = 'a'
c2 = 'x'

# Function call
replaceCharacter(str, c1, c2);

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to replace all occurrences
// of character c1 with character c2
static void replaceCharacter(string str,
                             char c1, char c2)
{
    char[] input = str.ToCharArray();

    // If the character at starting
    // of the given string is equal
    // to c1, replace it with c2
    for(int i = 0; i < str.Length; i++)
    {
        if (input[i] == c1)
        {
            input[i] = c2;
        }

        // Print the string
        Console.Write(input[i]);
    }
}

// Driver Code
public static void Main()
{

    // Given string
    string str = "abacd";
    char c1 = 'a';
    char c2 = 'x';

    // Function call
    replaceCharacter(str, c1, c2);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to replace all occurrences
// of character c1 with character c2
function replaceCharacter(str,c1, c2)
{
    // Base Case
    // If the string is empty
    if (str.length == 1)
    {
        return str;
    }
    var x=str.charAt(0);
    // If the character at starting
    // of the given string is equal
    // to c1, replace it with c2
    if (str.charAt(0) == c1)
    {
        x=c2;
        str = c2+str.substring(1);
    }

    // Getting the answer from recursion
    // for the smaller problem
    return x+replaceCharacter(str.substring(1),
                            c1, c2);
}

// Driver Code
//Given string
var str = "abacd";
var c1 = 'a';
var c2 = 'x';

// Function call
document.write(replaceCharacter(str, c1, c2));

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
xbxcd
```

**时间复杂度:** *O(N)，其中 N 是字符串的长度*
**辅助空间:** *O(1)*