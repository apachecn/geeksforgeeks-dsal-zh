# 反转中间 X 字符

> 原文:[https://www.geeksforgeeks.org/reverse-middle-x-characters/](https://www.geeksforgeeks.org/reverse-middle-x-characters/)

给定一个字符串**字符串**和一个整数 **X** 。任务是反转给定字符串的中间 **X** 字符，然后打印修改后的字符串。**注意****透镜(str)–X**总是均匀的。
**举例:**

> **输入:** str = "geeksforgeeks "，X = 3
> **输出:**geeks forgeeks
> 中间三个字符是【geeks】的**表示** geeks 的
> 因此得到的字符串是【geeks】的 **rof** geeks 的
> **输入:** str =【确认】，X = 7
> **输出:** acknegdelwoment

**进场:**

*   因为我们不需要颠倒前几个和后几个字符。找出我们在开头和结尾不需要反转的字符数，即**n = len(str)–X/2**。
*   按原样打印第一个 **n 个**字符。
*   然后按照相反的顺序从 **n + 1** 开始打印中间的 **x** 字符。
*   最后，最后一个 **n** 字符保持原样。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to reverse the middle x characters in a string
void reverse(string str, int x)
{
    // Find the position from where
    // the characters have to be reversed
    int n = (str.length() - x) / 2;

    // Print the first n characters
    for (int i = 0; i < n; i++)
        cout << str[i];

    // Print the middle x characters in reverse
    for (int i = n + x - 1; i >= n; i--)
        cout << str[i];

    // Print the last n characters
    for (int i = n + x; i < str.length(); i++)
        cout << str[i];
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int x = 3;
    reverse(str, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GfG
{

    // Function to reverse the middle x
    // characters in a string
    static void reverse(String str, int x)
    {
        // Find the position from where
        // the characters have to be reversed
        int n = (str.length() - x) / 2;

        // Print the first n characters
        for (int i = 0; i < n; i++)
            System.out.print(str.charAt(i));

        // Print the middle x characters in reverse
        for (int i = n + x - 1; i >= n; i--)
            System.out.print(str.charAt(i));

        // Print the last n characters
        for (int i = n + x; i < str.length(); i++)
            System.out.print(str.charAt(i));
    }

    // Drived code
    public static void main(String []args)
    {
        String str = "geeksforgeeks";
        int x = 3;
        reverse(str, x);
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to reverse the middle x characters in a str1ing
def reverse(str1, x):

    # Find the position from where
    # the characters have to be reversed
    n = (len(str1) - x) // 2

    # Print the first n characters
    for i in range(n):
        print(str1[i], end="")

    # Print the middle x characters in reverse
    for i in range(n + x - 1, n - 1, -1):
        print(str1[i], end="")

    # Print the last n characters
    for i in range(n + x, len(str1)):
        print(str1[i], end="")

# Driver code
str1 = "geeksforgeeks"
x = 3
reverse(str1, x)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to reverse the middle x
// characters in a string
static void reverse(string str, int x)
{
    // Find the position from where
    // the characters have to be reversed
    int n = (str.Length - x) / 2;

    // Print the first n characters
    for (int i = 0; i < n; i++)
        Console.Write(str[i]);

    // Print the middle x characters in reverse
    for (int i = n + x - 1; i >= n; i--)
        Console.Write(str[i]);

    // Print the last n characters
    for (int i = n + x; i < str.Length; i++)
        Console.Write(str[i]);
}

// Drived code
public static void Main()
{
    string str = "geeksforgeeks";
    int x = 3;
    reverse(str, x);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to reverse the middle x
// characters in a string
function reverse($str, $x)
{
    // Find the position from where
    // the characters have to be reversed
    $n = (strlen($str) - $x) / 2;

    // Print the first n characters
    for ($i = 0; $i < $n; $i++)
        echo($str[$i]);

    // Print the middle x characters in reverse
    for ($i = $n + $x - 1; $i >= $n; $i--)
        echo($str[$i]);

    // Print the last n characters
    for ($i= $n + $x; $i < strlen($str); $i++)
        echo $str[$i];
}

// Driver code
$str = "geeksforgeeks";
$x = 3;
reverse($str, $x);

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

    // Function to reverse the middle x
    // characters in a string
    function reverse( str , x)
    {
        // Find the position from where
        // the characters have to be reversed
        var n = (str.length - x) / 2;

        // Print the first n characters
        for (i = 0; i < n; i++)
            document.write(str.charAt(i));

        // Print the middle x characters in reverse
        for (i = n + x - 1; i >= n; i--)
            document.write(str.charAt(i));

        // Print the last n characters
        for (i = n + x; i < str.length; i++)
            document.write(str.charAt(i));
    }

    // Drived code

        var str = "geeksforgeeks";
        var x = 3;
        reverse(str, x);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
geeksrofgeeks
```