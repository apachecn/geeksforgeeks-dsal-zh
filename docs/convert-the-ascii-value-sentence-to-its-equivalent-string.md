# 将 ASCII 值句子转换为其等价字符串

> 原文:[https://www . geeksforgeeks . org/convert-the-ascii-value-句子到它的等价字符串/](https://www.geeksforgeeks.org/convert-the-ascii-value-sentence-to-its-equivalent-string/)

给定一个代表 [ASCII 句子](https://www.geeksforgeeks.org/print-given-sentence-equivalent-ascii-form/)的字符串 **str** ，任务是将这个字符串转换成它的等价字符序列。
**例:**

> **输入:** str = "71101101107115"
> **输出:**极客
> 71、101、101、107 分别是“G”、“e”、“e”、“k”和“s”字符的 unicode 值
> 。
> **输入:**str = " 10410110810811144321191111410810033 "
> **输出:**你好，世界！

**方法:**逐字符遍历整个字符串，并连接每个数字。一旦连接的值在范围**【32，122】**内，我们在 ASCII 表中打印与该数值对应的字符值。我们取范围[32，122]，因为空格，大写字母，小写字母都在这个范围内。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the character sequence
// for the given ASCII sentence
void asciiToSentence(string str, int len)
{
    int num = 0;
    for (int i = 0; i < len; i++) {

        // Append the current digit
        num = num * 10 + (str[i] - '0');

        // If num is within the required range
        if (num >= 32 && num <= 122) {

            // Convert num to char
            char ch = (char)num;
            cout << ch;

            // Reset num to 0
            num = 0;
        }
    }
}

// Driver code
int main()
{
    string str = "7110110110711510211111471101101107115";
    int len = str.length();
    asciiToSentence(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the character sequence
    // for the given ASCII sentence
    static void asciiToSentence(String str, int len)
    {
        int num = 0;
        for (int i = 0; i < len; i++) {

            // Append the current digit
            num = num * 10 + (str.charAt(i) - '0');

            // If num is within the required range
            if (num >= 32 && num <= 122) {

                // Convert num to char
                char ch = (char)num;
                System.out.print(ch);

                // Reset num to 0
                num = 0;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "7110110110711510211111471101101107115";
        int len = str.length();
        asciiToSentence(str, len);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the character sequence
# for the given ASCII sentence
def asciiToSentence(string, length) :

    num = 0;
    for i in range(length) :

        # Append the current digit
        num = num * 10 + (ord(string[i]) -
                          ord('0'));

        # If num is within the required range
        if (num >= 32 and num <= 122) :

            # Convert num to char
            ch = chr(num);
            print(ch, end = "");

            # Reset num to 0
            num = 0;

# Driver code
if __name__ == "__main__" :
    string = "7110110110711510211111471101101107115";
    length = len(string);

    asciiToSentence(string, length);

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to print the character sequence
    // for the given ASCII sentence
    static void asciiToSentence(String str, int len)
    {
        int num = 0;
        for (int i = 0; i < len; i++) {

            // Append the current digit
            num = num * 10 + (str[i] - '0');

            // If num is within the required range
            if (num >= 32 && num <= 122) {

                // Convert num to char
                char ch = (char)num;
                Console.Write(ch);

                // Reset num to 0
                num = 0;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        String str = "7110110110711510211111471101101107115";
        int len = str.Length;
        asciiToSentence(str, len);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the character sequence
// for the given ASCII sentence
function asciiToSentence($string, $length)
{
    $num = 0;
    for($i = 0; $i < $length; $i++)
    {

        // Append the current digit
        $num = $num * 10 + (ord($string[$i]) - ord('0'));

        // If num is within the required range
        if ($num >= 32 && $num <= 122)
        {

            // Convert num to char
            $ch = chr($num);
            print($ch);

            // Reset num to 0
            $num = 0;
            }
        }
}

    // Driver code
    $string = "7110110110711510211111471101101107115";
    $length = strlen($string);

    asciiToSentence($string, $length);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the character sequence
// for the given ASCII sentence
function asciiToSentence(str, len)
{
    var num = 0;
    for (var i = 0; i < len; i++) {

        // Append the current digit
        num = num * 10 + (str[i] - '0');

        // If num is within the required range
        if (num >= 32 && num <= 122) {

            // Convert num to char
            var ch = String.fromCharCode(num);
            document.write(ch);

            // Reset num to 0
            num = 0;
        }
    }
}

// Driver code
var str = "7110110110711510211111471101101107115";
var len = str.length;
asciiToSentence(str, len);

</script>
```

**Output:** 

```
GeeksforGeeks
```

**时间复杂度:** O(N)，其中 N 是给定字符串的长度。