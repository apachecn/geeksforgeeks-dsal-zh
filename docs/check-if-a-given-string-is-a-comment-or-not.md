# 检查给定的字符串是否是注释

> 原文:[https://www . geesforgeks . org/check-if-a-给定字符串是注释还是非注释/](https://www.geeksforgeeks.org/check-if-a-given-string-is-a-comment-or-not/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，代表程序中的一行，任务是检查给定的字符串是否是注释。

> 程序中的注释类型:
> 
> *   **单行注释:**以双斜线( **'//'** )开头的注释
> *   **多行注释:**注释以(**'/***)开头，以( **'*/'** )结尾。

**示例:**

> **输入:**line =/* geesforgeeks geesforgeeks */
> T3】输出:多行评论
> 
> **输入:**line =//geesforgeks geesforgeks”
> T3】输出:为单行评论

**方法:**思路是检查输入字符串是否为注释。以下是步骤:

*   检查第一个索引(即索引 0)的值是否为“/”，然后按照以下步骤操作，否则打印“这不是注释”。
*   If 行[0] == '/':
    *   如果行[1] == '/'，则打印“这是单行注释”。
    *   如果第[1] == '* '行，则遍历字符串，如果找到任何相邻的' * & '/'对，则打印“这是多行注释”。
*   否则，打印“这不是评论”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// string is a comment or not
void isComment(string line)
{

    // If two continuous slashes
    // precedes the comment
    if (line[0] == '/' && line[1] == '/'
        && line[2] != '/') {

        cout << "It is a single-line comment";
        return;
    }

    if (line[line.size() - 2] == '*'
        && line[line.size() - 1] == '/' && line[0] == '/' && line[1] == '*') {

        cout << "It is a multi-line comment";
        return;
    }

    cout << "It is not a comment";
}

// Driver Code
int main()
{
    // Given string
    string line = "/*GeeksForGeeks GeeksForGeeks*/";

    // Function call to check whether then
    // given string is a comment or not
    isComment(line);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if the given
// string is a comment or not
static void isComment(String S)
{
    char line[] = S.toCharArray();

    // If two continuous slashes
    // preceeds the comment
    if (line[0] == '/' && line[1] == '/' )
    {
        System.out.println(
            "It is a single-line comment");
        return;
    }

    if (line[0]=='/' && line[1]=='*' && line[line.length - 2] == '*' &&
        line[line.length - 1] == '/')
    {
        System.out.println(
            "It is a multi-line comment");
        return;
    }

    System.out.println("It is not a comment");
}

// Driver Code
public static void main(String[] args)
{

    // Given string
    String line = "/*GeeksForGeeks GeeksForGeeks*/";

    // Function call to check whether then
    // given string is a comment or not
    isComment(line);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given
# string is a comment or not
def isComment(line):

    # If two continuous slashes
    # preceeds the comment
    if (line[0] == '/'  and line[1] == '/' and line[2] != '/'):
        print("It is a single-line comment")
        return

    if (line[len(line) - 2] == '*' and line[len(line) - 1] == '/' and line[0] == '/'  and line[1] == '*'):
        print("It is a multi-line comment")
        return

    print("It is not a comment")

# Driver Code
if __name__ == '__main__':

    # Given string
    line = "/*GeeksForGeeks GeeksForGeeks*/"

    # Function call to check whether then
    # given string is a comment or not
    isComment(line)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if the given
// string is a comment or not
static void isComment(string S)
{
    char[] line = S.ToCharArray();

    // If two continuous slashes
    // preceeds the comment
    if (line[0] == '/' && line[1] == '/' &&
        line[2] != '/')
    {
        Console.WriteLine("It is a single-line comment");
        return;
    }

    if (line[line.Length - 2] == '*' &&
        line[line.Length - 1] == '/' && line[0] == '/' && line[1] == '*')
    {
        Console.WriteLine("It is a multi-line comment");
        return;
    }

    Console.WriteLine("It is not a comment");
}

// Driver Code
static public void Main()
{

    // Given string
    string line = "/*GeeksForGeeks GeeksForGeeks*/";

    // Function call to check whether then
    // given string is a comment or not
    isComment(line);
}
}

// This code is contributed by splevel62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the given
// string is a comment or not
function isComment( line)
{

    // If two continuous slashes
    // preceeds the comment
    var regex = new RegExp("//.*", );
    var rex = regex.test(line);
    if(rex){
        document.write("It is a single-line comment");
        return;
    }
    var regexMul = new RegExp("/\*.*?\*/", );
    var rexmul = regexMul.test(line);
    if (rexmul)
    {
        document.write("It is a multi-line comment");
        return;
    }

    document.write("It is not a comment");
}
// Driver Code

// Given string
var line = "/*GeeksForGeeks GeeksForGeeks*/";

// Function call to check whether then
// given string is a comment or not
isComment(line);

</script>
```

**Output**

```
It is a multi-line comment
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)