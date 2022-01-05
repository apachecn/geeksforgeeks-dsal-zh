# 给定句子的骆驼格

> 原文:[https://www.geeksforgeeks.org/camel-case-given-sentence/](https://www.geeksforgeeks.org/camel-case-given-sentence/)

给定一个句子，任务是删除句子中的空格，并在 [Camel case](https://en.wikipedia.org/wiki/Camel_case) 中重写。这是一种写作风格，我们没有空格，所有的单词都以大写字母开头。
**例:**

```
Input  : I got intern at geeksforgeeks
Output : IGotInternAtGeeksforgeeks

Input :  Here comes the garden
Output : HereComesTheGarden
```

**简单解决方法:**第一种方法是遍历句子，通过将后面的字符向后移动一个位置，并将第一个字符的大小写改为大写，一个接一个地删除空格。需要 **O(n*n)** 时间。
**高效解决方案:**我们遍历给定的字符串，遍历时我们将非空格字符复制到结果中，每当遇到空格时，我们都会忽略它，并将下一个字母改为大写。
下面是代码实现

## C++

```
// CPP program to convert given sentence
/// to camel case.
#include <bits/stdc++.h>
using namespace std;

// Function to remove spaces and convert
// into camel case
string convert(string s)
{
    int n = s.length();

    int res_ind = 0;

    for (int i = 0; i < n; i++) {

        // check for spaces in the sentence
        if (s[i] == ' ') {

            // conversion into upper case
            s[i + 1] = toupper(s[i + 1]);
            continue;
        }

        // If not space, copy character
        else
            s[res_ind++] = s[i];        
    }

    // return string to main
    return s.substr(0, res_ind);
}

// Driver program
int main()
{
    string str = "I get intern at geeksforgeeks";
    cout << convert(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert given sentence
/// to camel case.
class GFG
{

    // Function to remove spaces and convert
    // into camel case
    static String convert(String s)
    {

        // to count spaces
        int cnt= 0;
        int n = s.length();
        char ch[] = s.toCharArray();
        int res_ind = 0;

        for (int i = 0; i < n; i++)
        {

            // check for spaces in the sentence
            if (ch[i] == ' ')
            {
                cnt++;
                // conversion into upper case
                ch[i + 1] = Character.toUpperCase(ch[i + 1]);
                continue;
            }

            // If not space, copy character
            else
                ch[res_ind++] = ch[i];
        }

        // new string will be resuced by the
        // size of spaces in the original string
        return String.valueOf(ch, 0, n - cnt);
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "I get intern at geeksforgeeks";
        System.out.println(convert(str));
    }
}

// This code is contributed by gp6.
```

## 计算机编程语言

```
# Python program to convert
# given sentence to camel case.

# Function to remove spaces
# and convert into camel case
def convert(s):
    if(len(s) == 0):
        return
    s1 = ''
    s1 += s[0].upper()
    for i in range(1, len(s)):
        if (s[i] == ' '):
            s1 += s[i + 1].upper()
            i += 1
        elif(s[i - 1] != ' '):
            s1 += s[i]
    print(s1)    

# Driver Code
def main():
    s = "I get intern at geeksforgeeks"
    convert(s)

if __name__=="__main__":
    main()

# This code is contributed
# prabhat kumar singh

```

## C#

```
// C# program to convert given sentence
// to camel case.
using System;

class GFG
{

    // Function to remove spaces and convert
    // into camel case
    static void convert(String s)
    {

        // to count spaces
        int cnt= 0;
        int n = s.Length;
        char []ch = s.ToCharArray();
        int res_ind = 0;

        for (int i = 0; i < n; i++)
        {

            // check for spaces in the sentence
            if (ch[i] == ' ')
            {
                cnt++;

                // conversion into upper case
                ch[i + 1] = char.ToUpper(ch[i + 1]);
                continue;
            }

            // If not space, copy character
            else
                ch[res_ind++] = ch[i];
        }

        // new string will be resuced by the
        // size of spaces in the original string
        for(int i = 0; i < n - cnt; i++)
            Console.Write(ch[i]);
    }

    // Driver code
    public static void Main(String []args)
    {
        String str = "I get intern at geeksforgeeks";
        convert(str);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Function to remove spaces and convert
// into camel case
function convert( s)
{
    var n = s.length;

    var str="";
    for (var i = 0; i < n; i++)
    {

        // check for spaces in the sentence
        if (s[i] == ' ')
        {
            // conversion into upper case
            str+= s[i+1].toUpperCase();
            i++;

        }

        // If not space, copy character
        else{

            str+= s[i];
            }
    }

    // return string to main
    return str;
}

var str = "I get intern at geeksforgeeks";
    document.write(convert(str));

</script>
```

**Output**

```
IGetInternAtGeeksforgeeks
```

本文由**喜马拉雅冉冉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。