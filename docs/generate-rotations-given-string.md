# 生成给定字符串的所有旋转

> 原文:[https://www . geesforgeks . org/generate-rotations-给定字符串/](https://www.geeksforgeeks.org/generate-rotations-given-string/)

任务是打印给定字符串的所有可能的旋转字符串。

**示例:**

```
Input : S = "geeks"
Output : geeks
         eeksg
         eksge
         ksgee
         sgeek

Input : S = "abc" 
Output : abc
         bca
         cab
```

**方法 1(简单)**
想法是运行从 i = 0 到 n–1(n =字符串长度)的循环，即对于每个旋转点，复制临时字符串中字符串的第二部分，然后将原始字符串的第一部分复制到临时字符串。

以下是该方法的实施:

## C++

```
// A simple C++ program to generate all rotations
// of a given string
#include<bits/stdc++.h>
using namespace std;

// Print all the rotated string.
void printRotatedString(char str[])
{
    int len = strlen(str);

    // Generate all rotations one by one and print
    char temp[len];
    for (int i = 0; i < len; i++)
    {
        int j = i;  // Current index in str
        int k = 0;  // Current index in temp

        // Copying the second part from the point
        // of rotation.
        while (str[j] != '\0')
        {
            temp[k] = str[j];
            k++;
            j++;
        }

        // Copying the first part from the point
        // of rotation.
        j = 0;
        while (j < i)
        {
            temp[k] = str[j];
            j++;
            k++;
        }

        printf("%s\n", temp);
    }
}

// Driven Program
int main()
{
    char str[] = "geeks";
    printRotatedString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to generate all rotations
// of a given string   

class Test
{
    // Print all the rotated string.
    static void printRotatedString(String str)
    {
        int len = str.length();

        // Generate all rotations one by one and print
        StringBuffer sb;

        for (int i = 0; i < len; i++)
        {
            sb = new StringBuffer();

            int j = i;  // Current index in str
            int k = 0;  // Current index in temp

            // Copying the second part from the point
            // of rotation.
            for (int k2 = j; k2 < str.length(); k2++) {
                sb.insert(k, str.charAt(j));
                k++;
                j++;
            }

            // Copying the first part from the point
            // of rotation.
            j = 0;
            while (j < i)
            {
                sb.insert(k, str.charAt(j));
                j++;
                k++;
            }

            System.out.println(sb);
        }
    }

    // Driver method
    public static void main(String[] args)
    {
        String  str = new String("geeks");
        printRotatedString(str);
    }
}
```

## 蟒蛇 3

```
# A simple Python3 program to generate
# all rotations of a given string

# Print all the rotated strings.
def printRotatedString(str):

    lenn = len(str)

    # Generate all rotations
    # one by one and print
    temp = [0] * (lenn)
    for i in range(lenn):    
        j = i # Current index in str
        k = 0 # Current index in temp

        # Copying the second part from
        # the point of rotation.
        while (j < len(str)):

            temp[k] = str[j]
            k += 1
            j += 1

        # Copying the first part from
        # the point of rotation.
        j = 0
        while (j < i) :

            temp[k] = str[j]
            j += 1
            k += 1

        print(*temp, sep = "")

# Driver Code
if __name__ == '__main__':
    str = "geeks"
    printRotatedString(str)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// A simple C# program to generate
// all rotations of a given string    
using System;
using System.Text;

class GFG
{
// Print all the rotated string.
public static void printRotatedString(string str)
{
    int len = str.Length;

    // Generate all rotations one
    // by one and print
    StringBuilder sb;

    for (int i = 0; i < len; i++)
    {
        sb = new StringBuilder();

        int j = i; // Current index in str
        int k = 0; // Current index in temp

        // Copying the second part from
        // the point of rotation.
        for (int k2 = j; k2 < str.Length; k2++)
        {
            sb.Insert(k, str[j]);
            k++;
            j++;
        }

        // Copying the first part from
        // the point of rotation.
        j = 0;
        while (j < i)
        {
            sb.Insert(k, str[j]);
            j++;
            k++;
        }

        Console.WriteLine(sb);
    }
}

// Driver Code
public static void Main(string[] args)
{
    string str = "geeks";
    printRotatedString(str);
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to generate
// all rotations of a given string

// Print all the rotated string.
function printRotatedString($str)
{
    $len = strlen($str);

    // Generate all rotations one
    // by one and print
    $temp = " ";
    for ($i = 0; $i < $len; $i++)
    {
        $j = $i; // Current index in str
        $k = 0;  // Current index in temp

        // Copying the second part from
        // the point of rotation.
        while ($j < $len)
        {
            $temp[$k] = $str[$j];
            $k++;
            $j++;
        }

        // Copying the first part from
        // the point of rotation.
        $j = 0;
        while ($j < $i)
        {
            $temp[$k] = $str[$j];
            $j++;
            $k++;
        }

        echo $temp . "\n";
    }
}

// Driver Code
$str = "geeks";
printRotatedString($str);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// A simple javascript program to generate
// all rotations of a given string   

// Print all the rotated string.
function printRotatedString(str)
{
    var len = str.length;

    // Generate all rotations one
    // by one and print
    var sb;

    for(i = 0; i < len; i++)
    {
        sb = [];

        // Current index in str
        var j = i;

        // Current index in temp
        var k = 0; 

        // Copying the second part from the point
        // of rotation.
        for(k2 = j; k2 < str.length; k2++)
        {
            sb.push(str.charAt(j));
            k++;
            j++;
        }

        // Copying the first part from the point
        // of rotation.
        j = 0;

        while (j < i)
        {
            sb.push(str.charAt(j));
            j++;
            k++;
        }
        document.write(sb.join("") + "<br>");
    }
}

// Driver code
var  str = "geeks";
printRotatedString(str);

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
geeks
eeksg
eksge
ksgee
sgeek
```

**方法 2(棘手且高效)**
这个想法是基于[高效的方法来检查字符串是否是彼此的旋转](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)。我们把 str 和它自己连接起来，也就是说，我们在。是串联运算符。现在，我们遍历从 0 到 n–1 的串联字符串，并打印大小为 n 的所有子字符串。

下面是这种方法的实现:

## C++

```
// An efficient C++ program to print all
// rotations of a string.
#include<bits/stdc++.h>
using namespace std;

// Print all the rotated string.
void printRotatedString(char str[])
{
    int n = strlen(str);

    // Concatenate str with itself
    char temp[2*n + 1];
    strcpy(temp, str);
    strcat(temp, str);

    // Print all substrings of size n.
    // Note that size of temp is 2n
    for (int i = 0; i < n; i++)
    {
        for (int j=0; j != n; j++)
            printf("%c",temp[i + j]);
        printf("\n");
    }
}

// Driven Program
int main()
{
    char str[] = "geeks";
    printRotatedString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to generate all rotations
// of a given string   

class Test
{
    // Print all the rotated string.
    static void printRotatedString(String str)
    {
        int n = str.length();

        StringBuffer sb = new StringBuffer(str);
        // Concatenate str with itself
        sb.append(str);

        // Print all substrings of size n.
        // Note that size of sb is 2n
        for (int i = 0; i < n; i++)
        {
            for (int j=0; j != n; j++)
                System.out.print(sb.charAt(i + j));
            System.out.println();
        }
    }

    // Driver method
    public static void main(String[] args)
    {
        String  str = new String("geeks");
        printRotatedString(str);
    }
}
```

## 蟒蛇 3

```
# An efficient Python3 program to print 
# all rotations of a string.

# Print all the rotated string.
def printRotatedString(string) :

    n = len(string)

    # Concatenate str with itself
    temp = string + string

    # Print all substrings of size n.
    # Note that size of temp is 2n
    for i in range(n) :

        for j in range(n) :
            print(temp[i + j], end = "")

        print()

# Driver Code
if __name__ == "__main__" :

    string = "geeks"
    printRotatedString(string)

# This code is contributed by Ryuga
```

## C#

```
// A simple C# program to generate all rotations
// of a given string
using System;
using System.Text;

class Test
{

    // Print all the rotated string.
    static void printRotatedString(String str)
    {
        int n = str.Length;

        StringBuilder sb = new StringBuilder(str);
        // Concatenate str with itself
        sb.Append(str);

        // Print all substrings of size n.
        // Note that size of sb is 2n
        for (int i = 0; i < n; i++)
        {
            for (int j=0; j != n; j++)
                Console.Write(sb[i + j]);
            Console.WriteLine();
        }
    }

    // Driver method
    public static void Main(String[] args)
    {
        String str = "geeks";
        printRotatedString(str);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program to print all
// rotations of a string.

// Print all the rotated string.
function printRotatedString($str)
{
    $n = strlen($str);

    // Concatenate str with itself
    $temp=$str.$str;

    // Print all substrings of size n.
    // Note that size of temp is 2n
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j != $n; $j++)
            print($temp[$i + $j]);
        print("\n");
    }
}

    // Driver code
    $str = "geeks";
    printRotatedString($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// A simple javascript program to generate all rotations
// of a given string   

    // Print all the rotated string.
    function printRotatedString(str)
    {
        var n = str.length;     
        var sb = str;

        // Concatenate str with itself
        sb += (str);

        // Print all substrings of size n.
        // Note that size of sb is 2n
        for (var i = 0; i < n; i++)
        {
            for (var j = 0; j != n; j++)
                document.write(sb.charAt(i + j));
            document.write('<br>');
        }
    }

    // Driver method
    var  str = "geeks";
    printRotatedString(str);

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
geeks
eeksg
eksge
ksgee
sgeek
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。