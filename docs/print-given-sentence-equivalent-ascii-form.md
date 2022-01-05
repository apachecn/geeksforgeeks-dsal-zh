# 将给定句子打印成其等效的 ASCII 形式

> 原文:[https://www . geesforgeks . org/print-给定句子-等效-ascii-form/](https://www.geeksforgeeks.org/print-given-sentence-equivalent-ascii-form/)

给定一个包含构成句子的单词的字符串(属于英语)。任务是输出输入句子的等价 ASCII 句子。
*一个句子的 ASCII 形式是输入字符串的每个字符的转换，并将它们与字符串中出现的字符位置对齐*
**示例:**

```
Input : hello, world!
Output : ASCII Sentence:
         104101108108111443211911111410810033

Input : GeeksforGeeks
Output : ASCII Sentence:
         7110110110711510211111471101101107115
```

**说明:**
要完成任务，我们需要将每个字符转换成它的等价 [ASCII 值](https://www.geeksforgeeks.org/understanding-character-encoding/)。我们执行以下步骤来获得给定句子的等效 ASCII 形式-

*   遍历整个句子/字符串的长度
*   一次取句子的每个字符，减去空字符，并显式地键入结果
*   打印结果

按照上面的步骤，我们可以实现给定句子/字符串的等效 ASCII 形式。

## C++

```
// C++ implementation for converting
// a string into it's ASCII equivalent sentence
#include <bits/stdc++.h>
using namespace std;

// Function to compute the ASCII value of each
// character one by one
void ASCIISentence(std::string str)
{
    int l = str.length();
    int convert;
    for (int i = 0; i < l; i++) {
        convert = str[i] - NULL;
        cout << convert;
    }
}

// Driver function
int main()
{
    string str = "GeeksforGeeks";
    cout << "ASCII Sentence:" << std::endl;
    ASCIISentence(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for converting
// a string into it's ASCII equivalent sentence
import java.util.*;
import java.lang.*;

class GeeksforGeeks {

    // Function to compute the ASCII value of each
    // character one by one
    static void ASCIISentence(String str)
    {
        int l = str.length();
        int convert;
        for (int i = 0; i < l; i++) {
            convert = str.charAt(i);
            System.out.print(convert);
        }
    }

    // Driver function
    public static void main(String args[])
    {
        String str = "GeeksforGeeks";
        System.out.println("ASCII Sentence:");
        ASCIISentence(str);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation for
# converting a string into it's
# ASCII equivalent sentence

# Function to compute the ASCII
# value of each character one by one
def ASCIISentence( str ):

    for i in str:
        print(ord(i), end = '')
    print('\n', end = '')

# Driver code
str = "GeeksforGeeks"
print("ASCII Sentence:")
ASCIISentence(str)

# This code iss contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# implementation for converting
// a string into it's ASCII equivalent sentence
using System;

class GeeksforGeeks {

    // Function to compute the ASCII value
    //  of each character one by one
    static void ASCIISentence(string str)
    {
        int l = str.Length;
        int convert;
        for (int i = 0; i < l; i++)
        {
            convert = str[i];
            Console.Write(convert);
        }
    }

    // Driver function
    public static void Main()
    {
        string str = "GeeksforGeeks";
        Console.WriteLine("ASCII Sentence:");
        ASCIISentence(str);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation for converting a
// string into it's ASCII equivalent sentence

// Function to compute the ASCII
// value of each character one by one
function ASCIISentence($str)
{
    for ($i = 0; $i< strlen($str); $i++)
        echo ord($str[$i]);
}

// Driver code
$str = "GeeksforGeeks";
echo "ASCII Sentence:"."\n";
ASCIISentence($str);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript implementation for converting
// a string into it's ASCII equivalent sentence   

    // Function to compute the ASCII value of each
    // character one by one
    function ASCIISentence(str)
    {
        let l = str.length;
        let convert;
        for (let i = 0; i < l; i++) {
            convert = str[i].charCodeAt(0);
            document.write(convert);
        }
    }

    // Driver function
    let str = "GeeksforGeeks";
    document.write("ASCII Sentence:<br>");
    ASCIISentence(str);

    // This code is contributed by rag2127
</script>
```

**输出:**

```
ASCII Sentence:
7110110110711510211111471101101107115
```

转换成等价 ASCII 句子的时间复杂度是![O(len) ](img/1c59098a0c69a4ae477ffac8ac813cd6.png "Rendered by QuickLaTeX.com")，其中 len 是字符串的长度。
**应用:**

*   英语中的句子可以被编码/解码成这种形式，例如，将一个句子转换成它的等效 ASCII 形式，并在每个数字上加 5，然后从编码器端发送出去。稍后，解码器可以从每个数字中减去 5，并将其解码为原始形式。这样，只有发送方和接收方能够解码句子。
*   ASCII 形式也用于将数据从一台计算机传输到另一台计算机。

https://youtu.be/J8WGtK7I

-我们是 T0