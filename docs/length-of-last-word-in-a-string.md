# 字符串中最后一个单词的长度

> 原文:[https://www . geesforgeks . org/字符串中最后一个单词的长度/](https://www.geeksforgeeks.org/length-of-last-word-in-a-string/)

给定一个由大写/小写字母和空格组成的字符串，返回字符串中最后一个单词的长度。如果最后一个字不存在，则返回 0。

**示例:**

```
Input  : str = "Geeks For Geeks"
Output : 5
length(Geeks)= 5

Input : str = "Start Coding Here"
Output : 4
length(Here) = 4

Input  :  **
Output : 0
```

**方法 1:从索引 0 迭代字符串**
如果我们从左到右迭代字符串，我们必须小心最后一个单词后面的空格。第一个单词前的空格很容易被忽略。但是，如果字符串末尾有空格，则很难检测到最后一个单词的长度。这可以通过[修剪弦](https://www.geeksforgeeks.org/trim-remove-leading-trailing-spaces-string-java/)之前或末端的空间来处理。如果修改给定的字符串受到限制，我们需要创建一个字符串的副本，并从中删除空格。

## C++

```
// C++ program for implementation of simple
// approach to find length of last word
#include<bits/stdc++.h>
#include <boost/algorithm/string.hpp>
using namespace std;

int lengthOfLastWord(string a)
{
    int len = 0;

    /* String a is 'final'-- can not be modified
    So, create a copy and trim the spaces from
    both sides */
    string str(a);
    boost::trim_right(str);
    for (int i = 0; i < str.length(); i++)
    {
        if (str.at(i) == ' ')
            len = 0;
        else
            len++;
    }
    return len;
}

// Driver code
int main()
{
    string input = "Geeks For Geeks ";
    cout << "The length of last word is "
        << lengthOfLastWord(input);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of simple
// approach to find length of last word
public class GFG {
    public int lengthOfLastWord(final String a)
    {
        int len = 0;

        /* String a is 'final'-- can not be modified
           So, create a copy and trim the spaces from
           both sides */
        String x = a.trim();

        for (int i = 0; i < x.length(); i++) {
            if (x.charAt(i) == ' ')
                len = 0;
            else
                len++;
        }

        return len;
    }

    // Driver code
    public static void main(String[] args)
    {
        String input = "Geeks For Geeks  ";
        GFG gfg = new GFG();
        System.out.println("The length of last word is " + gfg.lengthOfLastWord(input));
    }
}
```

## 蟒蛇 3

```
# Python3 program for implementation of simple
# approach to find length of last word
def lengthOfLastWord(a):
    l = 0

    # String a is 'final'-- can not be modified
    # So, create a copy and trim the spaces from
    # both sides
    x = a.strip()

    for i in range(len(x)):
        if x[i] == " ":
            l = 0
        else:
            l += 1
    return l

# Driver code
if __name__ == "__main__":
    inp = "Geeks For Geeks "
    print("The length of last word is",
                 lengthOfLastWord(inp))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for implementation of simple
// approach to find length of last word
using System;

class GFG {

    public virtual int lengthOfLastWord(string a)
    {
        int len = 0;

        // String a is 'final'-- can
        // not be modified So, create
        // a copy and trim the
        // spaces from both sides
        string x = a.Trim();

        for (int i = 0; i < x.Length; i++) {
            if (x[i] == ' ') {
                len = 0;
            }
            else {
                len++;
            }
        }

        return len;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string input = "Geeks For Geeks ";
        GFG gfg = new GFG();
        Console.WriteLine("The length of last word is "
                          + gfg.lengthOfLastWord(input));
    }
}

// This code is contributed by shrikanth13
```

## java 描述语言

```
<script>

// js program for implementation of simple
// approach to find length of last word

function lengthOfLastWord(a)
{
    let len = 0;

    // String a is 'final'-- can
    // not be modified So, create
    // a copy and trim the
    // spaces from both sides
    x = a.trim();

    for (let i = 0; i < x.length; i++) {
        if (x[i] == ' ') {
            len = 0;
        }
        else {
            len++;
        }
    }

    return len;
}

// Driver code

input = "Geeks For Geeks ";
document.write("The length of last word is "+ lengthOfLastWord(input));

</script>
```

**输出:**

```
Length of the last word is 5
```

**方法 2:从最后一个索引开始迭代字符串。**这个想法更有效，因为我们可以很容易地忽略最后一个的空格。这个想法是当你遇到从最后一个字母开始的第一个字母时开始增加计数，当你遇到这些字母后面的空格时停止计数。

## C++

```
// CPP program for implementation of efficient
// approach to find length of last word
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

int length(string str)
{
    int count = 0;
    bool flag = false;
    for (int i = str.length() - 1; i >= 0; i--) {
        // Once the first character from last
        // is encountered, set char_flag to true.
        if ((str[i] >= 'a' && str[i] <= 'z') || (str[i] >= 'A' && str[i] <= 'Z')) {
            flag = true;
            count++;
        }
        // When the first space after the
        // characters (from the last) is
        // encountered, return the length
        // of the last word
        else {
            if (flag == true)
                return count;
        }
    }
    return count;
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";
    cout << "The length of last word is " << length(str);
    return 0;
}

// This code is contributed by rahulkumawat2107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of efficient
// approach to find length of last word
public class GFG {
    public int lengthOfLastWord(final String a)
    {
        boolean char_flag = false;
        int len = 0;
        for (int i = a.length() - 1; i >= 0; i--) {
            if (Character.isLetter(a.charAt(i))) {
                // Once the first character from last
                // is encountered, set char_flag to true.
                char_flag = true;
                len++;
            }
            else {
                // When the first space after the characters
                // (from the last) is encountered, return the
                // length of the last word
                if (char_flag == true)
                    return len;
            }
        }
        return len;
    }

    // Driver code
    public static void main(String[] args)
    {
        String input = "Geeks For Geeks  ";
        GFG gfg = new GFG();
        System.out.println("The length of last word is " + gfg.lengthOfLastWord(input));
    }
}
```

## 蟒蛇 3

```
# Python3 program for implementation of efficient
# approach to find length of last word
def length(str):

    count = 0;
    flag = False;
    length = len(str)-1;
    while(length != 0):
        if(str[length] == ' '):
            return count;
        else:
            count += 1;
        length -= 1;
    return count;

# Driver code
str = "Geeks for Geeks";
print("The length of last word is",
                      length(str));

# This code is contributed by Rajput Ji
```

## C#

```
// C# program for implementation of efficient
// approach to find length of last word
using System;

class GFG {

    public virtual int lengthOfLastWord(string a)
    {
        bool char_flag = false;
        int len = 0;
        for (int i = a.Length - 1; i >= 0; i--) {
            if (char.IsLetter(a[i])) {
                // Once the first character from last
                // is encountered, set char_flag to true.
                char_flag = true;
                len++;
            }
            else {
                // When the first space after the
                // characters (from the last) is
                // encountered, return the length
                // of the last word
                if (char_flag == true) {
                    return len;
                }
            }
        }
        return len;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string input = "Geeks For Geeks ";
        GFG gfg = new GFG();
        Console.WriteLine("The length of last word is " + gfg.lengthOfLastWord(input));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for implementation of efficient
// approach to find length of last word

function length($str)
{
    $count = 0;
    $flag = false;
    for($i = strlen($str)-1 ; $i>=0 ; $i--)
    {
        // Once the first character from last
        // is encountered, set char_flag to true.
        if( ($str[$i] >='a' && $str[$i]<='z') ||
            ($str[$i] >='A' && $str[$i]<='Z'))
        {
            $flag = true;
            $count++;
        }

        // When the first space after the
        // characters (from the last) is
        // encountered, return the length
        // of the last word
        else
        {
            if($flag == true)
                return $count;
        }

    }
    return $count;
}

// Driver code
$str = "Geeks for Geeks";
echo "The length of last word is ", length($str);

// This code is contributed by ajit.
?>
```

**输出:**

```
Length of the last word is 5
```

本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。

#### 方法 3:使用 split()和 list

*   因为一个句子中的所有单词都用空格隔开。
*   我们必须使用 [**split()通过空格来分割句子。**T3】](https://www.geeksforgeeks.org/python-string-split/)
*   我们将所有的单词用空格分开，并存储在一个列表中。
*   打印列表最后一个单词的长度。

下面是实现:

## 蟒蛇 3

```
# Python3 program for implementation of efficient
# approach to find length of last word

def length(str):
  # Split by space and converting
    # String to list and
    lis = list(str.split(" "))
    return len(lis[-1])

# Driver code
str = "Geeks for Geeks"
print("The length of last word is",
      length(str))

# This code is contributed by vikkycirus
```

## java 描述语言

```
<script>

// Javascript program for implementation
// of efficient approach to find length
// of last word
function length(str)
{

    // Split by space and converting
    // String to list and
    var lis = str.split(" ")
    return lis[lis.length - 1].length;
}

// Driver code
var str = "Geeks for Geeks"
document.write("The length of last word is " +
               length(str));

// This code is contributed by bunnyram19

</script>
```

**输出:**

```
Length of the last word is 5
```