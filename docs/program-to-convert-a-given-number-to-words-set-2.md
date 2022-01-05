# 将给定数字转换为单词的程序|设置 2

> 原文:[https://www . geesforgeks . org/program-to-convert-a-给定数字转单词-set-2/](https://www.geeksforgeeks.org/program-to-convert-a-given-number-to-words-set-2/)

编写代码将给定的数字转换成单词。
**例:**

```
Input: 438237764
Output: forty three crore eighty two lakh 
thirty seven thousand seven hundred and 
sixty four 

Input: 999999
Output: nine lakh ninety nine thousand nine
hundred and ninety nine

Input: 1000
Output: one thousand 
Explanation:1000 in words is "one thousand"
```

在[之前的](https://www.geeksforgeeks.org/convert-number-to-words/)帖子中，我们已经讨论了一种处理从 0 到 9999 的数字的方法。
**<u>解决方案:</u>** 这种方法可以处理长度小于 ULLONG_MAX(无符号长整型对象的最大值)的 20 位数字。ULLONG_MAX 在十进制中等于 18446744073709551615，假设编译器取 8 个字节存储无符号长整型。
下图显示了任意 9 位正整数的位置值图表:

```
4  3  8  2  3  7  7  6  4
|  |  |  |  |  |  |  |  |__ ones' place
|  |  |  |  |  |  |  |__ __ tens' place
|  |  |  |  |  |  |__ __ __ hundreds' place
|  |  |  |  |  |__ __ __ __ thousands' place
|  |  |  |  |__ __ __ __ __ tens thousands' place
|  |  |  |__ __ __ __ __ __ hundred thousands' place
|  |  |__ __ __ __ __ __ __ one millions' place
|  |__ __ __ __ __ __ __ __ ten millions' place
|__ __ __ __ __ __ __ __ __ hundred millions' place
```

其思想是根据上面的位置值图表将数字分成单个数字，并从最高有效数字开始处理。这里有一个简单的实现，支持最多 9 位数的数字。该程序可以很容易地扩展到支持任何 20 位数字。

## C++

```
/* C++ program to print a given number in words.
   The program handles till 9 digits numbers and
   can be easily extended to 20 digit number */
#include <iostream>
using namespace std;

// strings at index 0 is not used, it is to make array
// indexing simple
string one[] = { "", "one ", "two ", "three ", "four ",
                 "five ", "six ", "seven ", "eight ",
                 "nine ", "ten ", "eleven ", "twelve ",
                 "thirteen ", "fourteen ", "fifteen ",
                 "sixteen ", "seventeen ", "eighteen ",
                 "nineteen " };

// strings at index 0 and 1 are not used, they is to
// make array indexing simple
string ten[] = { "", "", "twenty ", "thirty ", "forty ",
                 "fifty ", "sixty ", "seventy ", "eighty ",
                 "ninety " };

// n is 1- or 2-digit number
string numToWords(int n, string s)
{
    string str = "";
    // if n is more than 19, divide it
    if (n > 19)
        str += ten[n / 10] + one[n % 10];
    else
        str += one[n];

    // if n is non-zero
    if (n)
        str += s;

    return str;
}

// Function to print a given number in words
string convertToWords(long n)
{
    // stores word representation of given number n
    string out;

    // handles digits at ten millions and hundred
    // millions places (if any)
    out += numToWords((n / 10000000), "crore ");

    // handles digits at hundred thousands and one
    // millions places (if any)
    out += numToWords(((n / 100000) % 100), "lakh ");

    // handles digits at thousands and tens thousands
    // places (if any)
    out += numToWords(((n / 1000) % 100), "thousand ");

    // handles digit at hundreds places (if any)
    out += numToWords(((n / 100) % 10), "hundred ");

    if (n > 100 && n % 100)
        out += "and ";

    // handles digits at ones and tens places (if any)
    out += numToWords((n % 100), "");

    return out;
}

// Driver code
int main()
{
    // long handles upto 9 digit no
    // change to unsigned long long int to
    // handle more digit number
    long n = 438237764;

    // convert given number in words
    cout << convertToWords(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to print a given number in words.
The program handles till 9 digits numbers and
can be easily extended to 20 digit number */
class GFG {

    // Strings at index 0 is not used, it is to make array
    // indexing simple
    static String one[] = { "", "one ", "two ", "three ", "four ",
                            "five ", "six ", "seven ", "eight ",
                            "nine ", "ten ", "eleven ", "twelve ",
                            "thirteen ", "fourteen ", "fifteen ",
                            "sixteen ", "seventeen ", "eighteen ",
                            "nineteen " };

    // Strings at index 0 and 1 are not used, they is to
    // make array indexing simple
    static String ten[] = { "", "", "twenty ", "thirty ", "forty ",
                            "fifty ", "sixty ", "seventy ", "eighty ",
                            "ninety " };

    // n is 1- or 2-digit number
    static String numToWords(int n, String s)
    {
        String str = "";
        // if n is more than 19, divide it
        if (n > 19) {
            str += ten[n / 10] + one[n % 10];
        }
        else {
            str += one[n];
        }

        // if n is non-zero
        if (n != 0) {
            str += s;
        }

        return str;
    }

    // Function to print a given number in words
    static String convertToWords(long n)
    {
        // stores word representation of given number n
        String out = "";

        // handles digits at ten millions and hundred
        // millions places (if any)
        out += numToWords((int)(n / 10000000), "crore ");

        // handles digits at hundred thousands and one
        // millions places (if any)
        out += numToWords((int)((n / 100000) % 100), "lakh ");

        // handles digits at thousands and tens thousands
        // places (if any)
        out += numToWords((int)((n / 1000) % 100), "thousand ");

        // handles digit at hundreds places (if any)
        out += numToWords((int)((n / 100) % 10), "hundred ");

        if (n > 100 && n % 100 > 0) {
            out += "and ";
        }

        // handles digits at ones and tens places (if any)
        out += numToWords((int)(n % 100), "");

        return out;
    }

    // Driver code
    public static void main(String[] args)
    {
        // long handles upto 9 digit no
        // change to unsigned long long int to
        // handle more digit number
        long n = 438237764;

        // convert given number in words
        System.out.printf(convertToWords(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to print a given number in words.
# The program handles till 9 digits numbers and
# can be easily extended to 20 digit number

# strings at index 0 is not used, it
# is to make array indexing simple
one = [ "", "one ", "two ", "three ", "four ",
        "five ", "six ", "seven ", "eight ",
        "nine ", "ten ", "eleven ", "twelve ",
        "thirteen ", "fourteen ", "fifteen ",
        "sixteen ", "seventeen ", "eighteen ",
        "nineteen "];

# strings at index 0 and 1 are not used,
# they is to make array indexing simple
ten = [ "", "", "twenty ", "thirty ", "forty ",
        "fifty ", "sixty ", "seventy ", "eighty ",
        "ninety "];

# n is 1- or 2-digit number
def numToWords(n, s):

    str = "";

    # if n is more than 19, divide it
    if (n > 19):
        str += ten[n // 10] + one[n % 10];
    else:
        str += one[n];

    # if n is non-zero
    if (n):
        str += s;

    return str;

# Function to print a given number in words
def convertToWords(n):

    # stores word representation of given
    # number n
    out = "";

    # handles digits at ten millions and
    # hundred millions places (if any)
    out += numToWords((n // 10000000),
                            "crore ");

    # handles digits at hundred thousands
    # and one millions places (if any)
    out += numToWords(((n // 100000) % 100),
                                   "lakh ");

    # handles digits at thousands and tens
    # thousands places (if any)
    out += numToWords(((n // 1000) % 100),
                             "thousand ");

    # handles digit at hundreds places (if any)
    out += numToWords(((n // 100) % 10),
                            "hundred ");

    if (n > 100 and n % 100):
        out += "and ";

    # handles digits at ones and tens
    # places (if any)
    out += numToWords((n % 100), "");

    return out;

# Driver code

# long handles upto 9 digit no
# change to unsigned long long
# int to handle more digit number
n = 438237764;

# convert given number in words
print(convertToWords(n));

# This code is contributed by mits
```

## C#

```
/* C# program to print a given number in words.
The program handles till 9 digits numbers and
can be easily extended to 20 digit number */
using System;
class GFG {

    // strings at index 0 is not used, it is
    // to make array indexing simple
    static string[] one = { "", "one ", "two ", "three ", "four ",
                            "five ", "six ", "seven ", "eight ",
                            "nine ", "ten ", "eleven ", "twelve ",
                            "thirteen ", "fourteen ", "fifteen ",
                            "sixteen ", "seventeen ", "eighteen ",
                            "nineteen " };

    // strings at index 0 and 1 are not used,
    // they is to make array indexing simple
    static string[] ten = { "", "", "twenty ", "thirty ", "forty ",
                            "fifty ", "sixty ", "seventy ", "eighty ",
                            "ninety " };

    // n is 1- or 2-digit number
    static string numToWords(int n, string s)
    {
        string str = "";

        // if n is more than 19, divide it
        if (n > 19) {
            str += ten[n / 10] + one[n % 10];
        }
        else {
            str += one[n];
        }

        // if n is non-zero
        if (n != 0) {
            str += s;
        }

        return str;
    }

    // Function to print a given number in words
    static string convertToWords(long n)
    {

        // stores word representation of
        // given number n
        string out1 = "";

        // handles digits at ten millions and
        // hundred millions places (if any)
        out1 += numToWords((int)(n / 10000000),
                           "crore ");

        // handles digits at hundred thousands
        // and one millions places (if any)
        out1 += numToWords((int)((n / 100000) % 100),
                           "lakh ");

        // handles digits at thousands and tens
        // thousands places (if any)
        out1 += numToWords((int)((n / 1000) % 100),
                           "thousand ");

        // handles digit at hundreds places (if any)
        out1 += numToWords((int)((n / 100) % 10),
                           "hundred ");

        if (n > 100 && n % 100 > 0) {
            out1 += "and ";
        }

        // handles digits at ones and tens
        // places (if any)
        out1 += numToWords((int)(n % 100), "");

        return out1;
    }

    // Driver code
    static void Main()
    {
        // long handles upto 9 digit no
        // change to unsigned long long int to
        // handle more digit number
        long n = 438237764;

        // convert given number in words
        Console.WriteLine(convertToWords(n));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP program to print a given number in words.
The program handles till 9 digits numbers and
can be easily extended to 20 digit number */

// strings at index 0 is not used, it is
// to make array indexing simple
$one = array("", "one ", "two ", "three ", "four ",
             "five ", "six ", "seven ", "eight ",
             "nine ", "ten ", "eleven ", "twelve ",
             "thirteen ", "fourteen ", "fifteen ",
             "sixteen ", "seventeen ", "eighteen ",
             "nineteen ");

// strings at index 0 and 1 are not used,
// they is to make array indexing simple
$ten = array("", "", "twenty ", "thirty ", "forty ",
             "fifty ", "sixty ", "seventy ", "eighty ",
             "ninety ");

// n is 1- or 2-digit number
function numToWords($n, $s)
{
    global $one, $ten;
    $str = "";

    // if n is more than 19, divide it
    if ($n > 19)
        {
            $str .= $ten[(int)($n / 10)];
            $str .= $one[$n % 10];
        }
    else
        $str .= $one[$n];

    // if n is non-zero
    if ($n != 0 )
        $str .= $s;

    return $str;
}

// Function to print a given number in words
function convertToWords($n)
{
    // stores word representation of
    // given number n
    $out = "";

    // handles digits at ten millions and
    // hundred millions places (if any)
    $out .= numToWords((int)($n / 10000000), "crore ");

    // handles digits at hundred thousands
    // and one millions places (if any)
    $out .= numToWords(((int)($n / 100000) % 100), "lakh ");

    // handles digits at thousands and tens
    // thousands places (if any)
    $out .= numToWords(((int)($n / 1000) % 100), "thousand ");

    // handles digit at hundreds places (if any)
    $out .= numToWords(((int)($n / 100) % 10), "hundred ");

    if ($n > 100 && $n % 100)
        $out .= "and ";

    // handles digits at ones and tens
    // places (if any)
    $out .= numToWords(($n % 100), "");

    return $out;
}

// Driver code

// long handles upto 9 digit no
// change to unsigned long long int to
// handle more digit number
$n = 438237764;

// convert given number in words
echo convertToWords($n) . "\n";

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

/* Javascript program to
 print a given number in words.
 The program handles till 9
 digits numbers and
can be easily extended to
20 digit number */  

// Strings at index 0 is not used, it is to make array
 // indexing simple
    var one = [ "", "one ", "two ", "three ", "four ",
                   "five ", "six ", "seven ", "eight ",
                    "nine ", "ten ", "eleven ", "twelve ",
                     "thirteen ", "fourteen ", "fifteen ",
                      "sixteen ", "seventeen ", "eighteen ",
                       "nineteen " ];

    // Strings at index 0 and 1 are not used, they is to
    // make array indexing simple
    var ten = [ "", "", "twenty ", "thirty ", "forty ",
              "fifty ", "sixty ", "seventy ", "eighty ",
                          "ninety " ];

    // n is 1- or 2-digit number
    function numToWords(n, s)
    {
        var str = "";
        // if n is more than 19, divide it
        if (n > 19) {
            str += ten[parseInt(n / 10)] + one[n % 10];
        }
        else {
            str += one[n];
        }

        // if n is non-zero
        if (n != 0) {
            str += s;
        }

        return str;
    }

    // Function to print a given number in words
    function convertToWords(n)
    {
        // stores word representation of given number n
        var out = "";

        // handles digits at ten millions and hundred
        // millions places (if any)
        out += numToWords(parseInt(n / 10000000),
        "crore ");

        // handles digits at hundred thousands and one
        // millions places (if any)
        out += numToWords(parseInt((n / 100000) % 100),
        "lakh ");

        // handles digits at thousands and tens thousands
        // places (if any)
        out += numToWords(parseInt((n / 1000) % 100),
        "thousand ");

        // handles digit at hundreds places (if any)
        out += numToWords(parseInt((n / 100) % 10),
        "hundred ");

        if (n > 100 && n % 100 > 0) {
            out += "and ";
        }

        // handles digits at ones and tens places (if any)
        out += numToWords(parseInt(n % 100), "");

        return out;
    }

    // Driver code
 // var handles upto 9 digit no
    // change to unsigned var var var to
    // handle more digit number
    var n = 438237764;

    // convert given number in words
    document.write(convertToWords(n));

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
forty three crore eighty two lakh thirty seven 
thousand seven hundred and sixty four 
```

**复杂度分析:**

*   **时间复杂度:** O(1)。
    循环运行的时间是恒定的。
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。