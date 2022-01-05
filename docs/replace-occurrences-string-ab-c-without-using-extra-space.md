# 在不使用额外空间的情况下，用 C 替换所有出现的字符串 AB

> 原文:[https://www . geeksforgeeks . org/replace-occurs-string-ab-c-不使用-extra-space/](https://www.geeksforgeeks.org/replace-occurrences-string-ab-c-without-using-extra-space/)

给定一个字符串**字符串**，该字符串可能包含一个或多个出现的“AB”。将字符串中出现的所有“AB”替换为“C”。

**示例:**

```
Input  : str = "helloABworld"
Output : str = "helloCworld"

Input  : str = "fghABsdfABysu"
Output : str = "fghCsdfCysu"
```

一个**简单的解决方法**就是找到所有出现的“AB”。每次出现时，用 C 替换它，并将所有字符向后移动一个位置。

## C++

```
// C++ program to replace all occurrences of "AB"
// with "C"
#include <bits/stdc++.h>

void translate(char* str)
{
    if (str[0] == '')
        return;

    // Start traversing from second character
    for (int i=1; str[i] != ''; i++)
    {
        // If previous character is 'A' and
        // current character is 'B"
        if (str[i-1]=='A' && str[i]=='B')
        {
            // Replace previous character with
            // 'C' and move all subsequent
            // characters one position back
            str[i-1] = 'C';
            for (int j=i; str[j]!=''; j++)
                str[j] = str[j+1];
        }
    }
    return;
}

// Driver code
int main()
{
    char str[] = "helloABworldABGfG";
    translate(str);
    printf("The modified string is :\n");
    printf("%s", str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace all
// occurrences of "AB" with "C"
import java.io.*;

class GFG {

    static void translate(char str[])
    {
        // Start traversing from second character
        for (int i = 1; i < str.length; i++)
        {
            // If previous character is 'A' and
            // current character is 'B"
            if (str[i - 1] == 'A' && str[i] == 'B')
            {
                // Replace previous character with
                // 'C' and move all subsequent
                // characters one position back
                str[i - 1] = 'C';
                int j;
                for (j = i; j < str.length - 1; j++)
                    str[j] = str[j + 1];
                str[j] = ' ';

            }
        }
        return;
    }

    // Driver code
    public static void main(String args[])
    {
        String st = "helloABworldABGfG";
        char str[] = st.toCharArray();
        translate(str);
        System.out.println("The modified string is :");
        System.out.println(str);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to replace all
# occurrences of "AB" with "C"

def translate(st) :

    # Start traversing from second character
    for i in range(1, len(st)) :

        # If previous character is 'A'
        # and current character is 'B"
        if (st[i - 1] == 'A' and st[i] == 'B') :

            # Replace previous character with
            # 'C' and move all subsequent
            # characters one position back
            st[i - 1] = 'C'

            for j in range(i, len(st) - 1) :
                st[j] = st[j + 1]

            st[len(st) - 1] = ' '

    return

# Driver code
st = list("helloABworldABGfG")
translate(st)

print("The modified string is :")
print(''.join(st))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to replace all
// occurrences of "AB" with "C"
using System;

class GFG {

    static void translate(char []str)
    {

        // Start traversing from second character
        for (int i = 1; i < str.Length; i++)
        {
            // If previous character is 'A' and
            // current character is 'B"
            if (str[i - 1] == 'A' && str[i] == 'B')
            {
                // Replace previous character with
                // 'C' and move all subsequent
                // characters one position back
                str[i - 1] = 'C';
                int j;
                for (j = i; j < str.Length - 1; j++)
                    str[j] = str[j + 1];
                str[j] = ' ';

            }
        }
        return;
    }

    // Driver code
    public static void Main()
    {
        String st = "helloABworldABGfG";
        char []str = st.ToCharArray();
        translate(str);
        Console.WriteLine("The modified string is :");
        Console.Write(str);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace all
// occurrences of "AB" with "C"

function translate(&$str)
{
    if ($str[0] == '')
        return;

    // Start traversing from second character
    for ($i = 1; $i < strlen($str); $i++)
    {
        // If previous character is 'A' and
        // current character is 'B"
        if ($str[$i - 1] == 'A' && $str[$i] == 'B')
        {
            // Replace previous character with
            // 'C' and move all subsequent
            // characters one position back
            $str[$i - 1] = 'C';
            for ($j = $i; $j < strlen($str) ; $j++)
                $str[$j] = $str[$j + 1];
        }
    }
    return;
}

// Driver code
$str = "helloABworldABGfG";
translate($str);
echo "The modified string is :\n";
echo $str;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to replace all
// occurrences of "AB" with "C"
function translate(str)
{

    // Start traversing from second character
    for(let i = 1; i < str.length; i++)
    {

        // If previous character is 'A' and
        // current character is 'B"
        if (str[i - 1] == 'A' && str[i] == 'B')
        {

            // Replace previous character with
            // 'C' and move all subsequent
            // characters one position back
            str[i - 1] = 'C';
            let j;

            for(j = i; j < str.length - 1; j++)
                str[j] = str[j + 1];

            str[j] = ' ';
        }
    }
    return;
}

// Driver code
let st = "helloABworldABGfG";
let str = st.split("");
translate(str);

document.write("The modified string is :<br>");
document.write(str.join(""));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
The modified string is :
helloCworldCGfG
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)

一个**有效的解决方案**是跟踪两个索引，一个用于修改后的字符串( **i【下面代码中的 T3】)另一个用于原始字符串( **j【下面代码中的 T5】)。如果我们在当前指数 j 处找到“AB”，我们将 j 增加 2，I 增加 1。否则，我们将两者都递增，并将字符从 j 复制到 I。****

下面是上述想法的实现。

## C++

```
// Efficient C++ program to replace all occurrences
// of "AB" with "C"
#include <bits/stdc++.h>

void translate(char* str)
{
    int len = strlen(str);
    if (len < 2)
       return;

    int i = 0;  // Index in modified string
    int j = 0; // Index in original string

    // Traverse string
    while (j < len-1)
    {
        // Replace occurrence of "AB" with "C"
        if (str[j] == 'A' && str[j+1] == 'B')
        {
            // Increment j by 2
            j = j + 2;
            str[i++] = 'C';
            continue;
        }
        str[i++] = str[j++];
    }

    if (j == len-1)
      str[i++] = str[j];

    // add a null character to terminate string
    str[i] = '';
}

// Driver code
int main()
{
    char str[] = "helloABworldABGfG";
    translate(str);
    printf("The modified string is :\n");
    printf("%s", str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to replace
// all occurrences of "AB" with "C"
import java.io.*;

class GFG {

    static void translate(char str[])
    {
        int len = str.length;
        if (len < 2)
        return;

        // Index in modified string
        int i = 0;

        // Index in original string
        int j = 0;

        // Traverse string
        while (j < len - 1)
        {
            // Replace occurrence of "AB" with "C"
            if (str[j] == 'A' && str[j + 1] == 'B')
            {
                // Increment j by 2
                j = j + 2;
                str[i++] = 'C';
                continue;
            }
            str[i++] = str[j++];
        }

        if (j == len - 1)
        str[i++] = str[j];

        // add a null character to terminate string
        str[i] = ' ';
        str[len - 1]=' ';
    }

    // Driver code
    public static void main(String args[])
    {
        String st="helloABworldABGfG";
        char str[] = st.toCharArray();
        translate(str);
        System.out.println("The modified string is :");
        System.out.println(str);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to replace all
# occurrences of "AB" with "C"

def translate(st) :
    l = len(st)

    if (l < 2) :
        return

    i = 0 # Index in modified string
    j = 0 # Index in original string

    # Traverse string
    while (j < l - 1) :

        # Replace occurrence of "AB" with "C"
        if (st[j] == 'A' and st[j + 1] == 'B') :

            # Increment j by 2
            j += 2
            st[i] = 'C'
            i += 1
            continue

        st[i] = st[j]
        i += 1
        j += 1

    if (j == l - 1) :
        st[i] = st[j]
        i += 1

    # add a null character to
    # terminate string
    st[i] = ' '
    st[l-1] = ' '

# Driver code
st = list("helloABworldABGfG")
translate(st)

print("The modified string is :")
print(''.join(st))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Efficient C# program to replace
// all occurrences of "AB" with "C"
using System;

class GFG {

    static void translate(char []str)
    {
        int len = str.Length;
        if (len < 2)
            return;

        // Index in modified string
        int i = 0;

        // Index in original string
        int j = 0;

        // Traverse string
        while (j < len - 1)
        {

            // Replace occurrence of "AB" with "C"
            if (str[j] == 'A' && str[j + 1] == 'B')
            {
                // Increment j by 2
                j = j + 2;
                str[i++] = 'C';
                continue;
            }
            str[i++] = str[j++];
        }

        if (j == len - 1)
            str[i++] = str[j];

        // add a null character to
        // terminate string
        str[i] = ' ';
        str[len - 1]=' ';
    }

    // Driver code
    public static void Main()
    {
        String st="helloABworldABGfG";
        char []str = st.ToCharArray();
        translate(str);
        Console.Write("The modified string is :");
        Console.Write(str);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// Efficient javascript program to replace
// all occurrences of "AB" with "C"
function translate(str)
{
    var len = str.length;
    if (len < 2)
       return;

    // Index in modified string
    var i = 0; 

    // Index in original string
    var j = 0;

    // Traverse string
    while (j < len - 1)
    {

        // Replace occurrence of "AB" with "C"
        if (str[j] == 'A' && str[j + 1] == 'B')
        {

            // Increment j by 2
            j = j + 2;
            let firstPart = str.substr(0, i);
            let lastPart =  str.substr(i + 1);
            str = firstPart + 'C' + lastPart;
            i += 1;
            continue;
        }
        let firstPart = str.substr(0, i);
        let lastPart =  str.substr(i + 1);
        str = firstPart + str[j] + lastPart;
        i += 1;
        j += 1;
    }

    if (j == len - 1)
    {
        let firstPart = str.substr(0, i);
        let lastPart =  str.substr(i + 1);
        str = firstPart + str[j] + lastPart;
        i += 1;
    }

    // Add a null character to terminate string
    let firstPart = str.substr(0, i);
    let lastPart =  str.substr(i + 1);
    str = firstPart + ' ' + lastPart;
    firstPart = str.substr(0, len - 1);
    lastPart =  str.substr(len);
    str = firstPart + ' ' + lastPart;

    // str[len - 1]=' ';
    return str;
}

// Driver code
var str = "helloABworldABGfG";
document.write("The modified string is :" +
               "<br>" + translate(str));

// This code is contributed by ipg2016107

</script>
```

输出:

```
The modified string is :
helloCworldCGfG
```

时间复杂度:O(n)
辅助空间:O(1)

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。