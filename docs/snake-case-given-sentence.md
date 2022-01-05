# 给定句子的蛇格

> 原文:[https://www.geeksforgeeks.org/snake-case-given-sentence/](https://www.geeksforgeeks.org/snake-case-given-sentence/)

给定一个句子，任务是删除句子中的空格，并在 [Snake case](https://en.wikipedia.org/wiki/Snake_case) 中重写。这是一种写作风格，我们用下划线代替空格，所有单词都以小写字母开头。
**例:**

```
Input :  I got intern at geeksforgeeks
Output : i_got_intern_at_geeksforgeeks

Input : Here comes the garden
Output : here_comes_the_garden
```

**简单解决方法:**第一种方法是遍历句子，用下划线逐个替换空格，将第一个字符的大小写改为小写字母。需要 **O(n*n)** 时间。
**高效解决方案:**我们遍历给定的字符串，遍历时我们用下划线替换空格字符，每当遇到非空格字母时，我们就将该字母改为小写。
下面是代码实现:

## C++

```
// CPP program to convert given sentence
/// to snake case
#include <bits/stdc++.h>
using namespace std;

// Function to replace spaces and convert
// into snake case
void convert(string str)
{
    int n = str.length();

    for (int i = 0; i < n; i++)
    {
        // Converting space to underscore
        if (str.at(i) == ' ')
            str.at(i) = '_';
        else
            // If not space, convert into lower character
            str.at(i) = tolower(str.at(i));
    }

    cout << str;
}

// Driver program
int main()
{
    string str = "I got intern at geeksforgeeks";
    // Calling function
    convert(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert
// given sentence to
// snake case
import java.io.*;

class GFG
{

// Function to replace
// spaces and convert
// into snake case
static void convert(String str)
{
    int n = str.length();
    String str1 = "";

    for (int i = 0; i < n; i++)
    {
        // Converting space
        // to underscore
        if (str.charAt(i) == ' ')
            str1 = str1 + '_';
        else

            // If not space, convert
            // into lower character
            str1 = str1 +
                   Character.toLowerCase(str.charAt(i));
    }

    System.out.print(str1);
}    

// Driver Code
public static void main(String args[])
{
    String str = "I got intern at geeksforgeeks";

    // Calling function
    convert(str);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to convert given sentence
# to snake case

# Function to replace spaces and convert
# into snake case
def convert(string) :

    n = len(string);
    string = list(string);

    for i in range(n) :

        # Converting space to underscore
        if (string[i] == ' ') :
            string[i] = '_';
        else :
            # If not space, convert
            # into lower character
            string[i] = string[i].lower();

    string = "".join(string)
    print(string);

# Driver program
if __name__ == "__main__" :

    string = "I got intern at geeksforgeeks";

    # Calling function
    convert(string);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to convert
// given sentence to
// snake case
using System;

class GFG
{
    // Function to replace
    // spaces and convert
    // into snake case
    static void convert(string str)
    {
        int n = str.Length;
        string str1 = "";

        for (int i = 0; i < n; i++)
        {
            // Converting space
            // to underscore
            if (str[i] == ' ')
                str1 = str1 + '_';
            else

                // If not space, convert
                // into lower character
                str1 = str1 +
                       Char.ToLower(str[i]);
        }        
        Console.Write(str1);
    }    

    // Driver Code
    static void Main()
    {
        string str = "I got intern at geeksforgeeks";

        // Calling function
        convert(str);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert given
// sentence to snake case

// Function to replace spaces
// and convert into snake case
function convert($str)
{
    $n = strlen($str);

    for ($i = 0; $i < $n; $i++)
    {
        // Converting space
        // to underscore
        if ($str[$i] == ' ')
            $str[$i] = '_';
        else
            // If not space, convert
            // into lower character
            $str[$i] = strtolower($str[$i]);
    }
    echo $str;
}

// Driver Code
$str = "I got intern at geeksforgeeks";

// Calling function
convert($str);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// Javascript program to convert
// given sentence to
// snake case

    // Function to replace
    // spaces and convert
    // into snake case
    function convert (str) {
        let n = str.length;
        let str1 = "";

        for ( i = 0; i < n; i++)
        {

            // Converting space
            // to underscore
            if (str[i] == ' ')
                str1 = str1 + '_';
            else

                // If not space, convert
                // into lower letacter
                str1 = str1 + (str[i]).toLowerCase();
        }

        document.write(str1);
    }

    // Driver Code
    let str = "I got letern at geeksforgeeks";

    // Calling function
    convert(str);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
i_got_intern_at_geeksforgeeks
```