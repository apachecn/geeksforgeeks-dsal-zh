# 检查是否可以用给定的单词组成两个字符串

> 原文:[https://www . geesforgeks . org/check-string-can-make-contain-given-temporal-string/](https://www.geeksforgeeks.org/check-string-can-made-containing-given-temporary-string/)

给定一个由两个字符组成的字符串和 n 个由两个字符组成的不同单词。任务是找出是否有可能以这样一种方式排列给定的单词，即串联的字符串将给定的两个字符串作为子字符串。我们可以多次追加一个单词。
示例:

```
Input : str = "ya"
        words[] = {"ah", "oy", "to", "ha"} 
Output : YES
We can join "oy" and then "ah", and
then "ha" to form the string "oyahha" 
which contains the string "ya".
 So, the answer is "YES"

Input : str[] = "ha"
        words[] = "ah"
Output :YES
The string "ahah" contains "ha" 
as a substring.

Input : str = "hp"
       words[] = {"ht", "tp"|
Output :NO
We can't produce a string containing
"hp" as a sub-string. Note that we
can join "ht" and then "tp" producing
"http", but it doesn't contain the 
"hp" as a sub-string.
```

如果我们仔细看给定的例子，我们可以看到，如果以下任何一个条件为真，我们的答案将是“是”，

1.  字符串等于 N 个单词中的任何一个
2.  str 等于任何单词的反义词。
3.  字符串的第一个字母等于任意给定 N 个字符串的最后一个字母，最后一个字母等于任意给定 N 个字符串的第一个字母。

否则我们的输出永远是 NO.
下面是上面方法的实现。

## C++

```
// CPP code to check if a two character string can
// be made using given strings
#include <bits/stdc++.h>
using namespace std;

// Function to check if str can be made using
// given words
bool makeAndCheckString(vector<string> words, string str)
{
    int n = words.size();
    bool first = false, second = false;

    for (int i = 0; i < n; i++) {

        // If str itself is present
        if (words[i] == str)
            return true;

        // Match first character of str
        // with second of word and vice versa
        if (str[0] == words[i][1])
            first = true;           
        if (str[1] == words[i][0])
            second = true;

        // If both characters found.
        if (first && second)
            return true;
    }

    return false;
}

// Driver Code
int main()
{
    string str = "ya";        
    vector<string> words = { "ah", "oy", "to", "ha"};    
    if (makeAndCheckString(words, str))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a two character string can
// be made using given strings
import java.util.*;

class GFG
{

// Function to check if str can be made using
// given words
static boolean makeAndCheckString(Vector<String> words,
                                            String str)
{
    int n = words.size();
    boolean first = false, second = false;

    for (int i = 0; i < n; i++)
    {

        // If str itself is present
        if (words.get(i) == str)
            return true;

        // Match first character of str
        // with second of word and vice versa
        if (str.charAt(0) == words.get(i).charAt(1))
            first = true;        
        if (str.charAt(1) == words.get(i).charAt(0))
            second = true;

        // If both characters found.
        if (first && second)
            return true;
    }

    return false;
}

// Driver Code
public static void main(String[] args)
{
    String str = "ya";
    String[] array = { "ah", "oy", "to", "ha"};
    Vector<String> words = new Vector<String>(Arrays.asList(array));    
    if (makeAndCheckString(words, str))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to check if a two character string can 
# be made using given strings

# Function to check if str can be made using
# given words
def makeAndCheckString(words, str):
    n = len(words)
    first = second = False

    for i in range(n):
        # If str itself is present
        if words[i]==str:
            return True

        # Match first character of str
        # with second of word and vice versa
        if str[0] == words[i][1]:
            first = True
        if str[1] == words[i][0]:
            second = True

        # If both characters found.
        if first and second:
            return True

    return False

# Driver Code
str = 'ya'
words = ['ah', 'oy', 'to', 'ha']
if makeAndCheckString(words, str):
    print('YES')
else:
    print('NO')

# This code is contributed 
# by SamyuktaSHegde
```

## C#

```
// C# code to check if a two character string can
// be made using given strings
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if str can be made using
// given words
static bool makeAndCheckString(List<String> words,
                                            String str)
{
    int n = words.Count;
    bool first = false, second = false;

    for (int i = 0; i < n; i++)
    {

        // If str itself is present
        if (words[i] == str)
            return true;

        // Match first character of str
        // with second of word and vice versa
        if (str[0] == words[i][1])
            first = true;        
        if (str[1] == words[i][0])
            second = true;

        // If both characters found.
        if (first && second)
            return true;
    }

    return false;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "ya";
    String[] array = { "ah", "oy", "to", "ha"};
    List<String> words = new List<String>(array);    
    if (makeAndCheckString(words, str))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if a two character string can
// be made using given strings

// Function to check if str can be made using
// given words
function makeAndCheckString($words, $str)
{
    $n = sizeof($words) ;
    $first = false ;
    $second = false;

    for ($i = 0; $i < $n; $i++) {

        // If str itself is present
        if ($words[$i] == $str)
            return true;

        // Match first character of str
        // with second of word and vice versa
        if ($str[0] == $words[$i][1])
            $first = true;            
        if ($str[1] == $words[$i][0])
            $second = true;

        // If both characters found.
        if ($first && $second)
            return true;
    }

    return false;
}

    // Driver Code 
    $str = "ya";        
    $words = array( "ah", "oy", "to", "ha") ;
    if (makeAndCheckString($words, $str))
        echo "Yes";
    else
        echo "No";

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript code to check if a two character string can
    // be made using given strings

    // Function to check if str can be made using
    // given words
    function makeAndCheckString(words, str)
    {
        let n = words.length;
        let first = false, second = false;

        for (let i = 0; i < n; i++)
        {

            // If str itself is present
            if (words[i] == str)
                return true;

            // Match first character of str
            // with second of word and vice versa
            if (str[0] == words[i][1])
                first = true;        
            if (str[1] == words[i][0])
                second = true;

            // If both characters found.
            if (first && second)
                return true;
        }

        return false;
    }

    let str = "ya";
    let words = [ "ah", "oy", "to", "ha"];   
    if (makeAndCheckString(words, str))
        document.write("YES");
    else
        document.write("NO");

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
YES
```

本文由**萨尔特哈克·科利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。