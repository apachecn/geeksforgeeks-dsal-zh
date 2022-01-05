# 先前数字的二进制表示

> 原文:[https://www . geesforgeks . org/binary-presentation-previous-number/](https://www.geeksforgeeks.org/binary-representation-previous-number/)

给定一个表示正数 n 的二进制表示的二进制输入，求 n-1 的二进制表示。可以假设输入二进制数大于 0。
二进制输入可能适合也可能不适合无符号长整型。
**例:**

```
Input : 10110
Output : 10101
Here n  = (22)10 = (10110)2
Previous number = (21)10 = (10101)2

Input : 11000011111000000
Output : 11000011110111111
```

我们将输入存储为字符串，这样就可以处理大量的数字。我们从最右边的字符开始遍历字符串，并将所有 0 转换为 1，直到找到 1。最后将找到的 1 转换为 0。这个过程之后形成的数字就是所需的数字。如果输入的是“1”，那么之前的数字将是“0”。如果整个字符串中只有第一个字符是“1”，那么我们将丢弃这个字符，并将所有的 0 更改为 1。

## C++

```
// C++ implementation to find the binary
// representation of previous number
#include <bits/stdc++.h>
using namespace std;

// function to find the required
// binary representation
string previousNumber(string num)
{
    int n = num.size();

    // if the number is '1'
    if (num.compare("1") == 0)
        return "0";

    // examine bits from right to left
    int i;
    for (i = n - 1; i >= 0; i--) {

        // if '1' is encountered, convert
        // it to '0' and then break
        if (num.at(i) == '1') {
            num.at(i) = '0';
            break;
        }

        // else convert '0' to '1'
        else
            num.at(i) = '1';
    }

    // if only the 1st bit in the
    // binary representation was '1'
    if (i == 0)
        return num.substr(1, n - 1);

    // final binary representation
    // of the required number
    return num;
}

// Driver program to test above
int main()
{
    string num = "10110";
    cout << "Binary representation of previous number = "
         << previousNumber(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the binary
// representation of previous number
class GFG
{

    // function to find the required
    // binary representation
    static String previousNumber(String num)
    {
        int n = num.length();

        // if the number is '1'
        if (num.compareTo("1") == 0)
        {
            return "0";
        }

        // examine bits from right to left
        int i;
        for (i = n - 1; i >= 0; i--)
        {

            // if '1' is encountered, convert
            // it to '0' and then break
            if (num.charAt(i) == '1')
            {
                num = num.substring(0, i) + '0' +
                            num.substring(i + 1);

                // num.charAt(i) = '0';
                break;
            }

            // else convert '0' to '1'
            else
            {
                num = num.substring(0, i) + '1' +
                            num.substring(i + 1);
            }
            //num.at(i) = '1';
        }

        // if only the 1st bit in the
        // binary representation was '1'
        if (i == 0)
        {
            return num.substring(1, n - 1);
        }

        // final binary representation
        // of the required number
        return num;
    }

    // Driver code
    public static void main(String[] args)
    {
        String num = "10110";
        System.out.print("Binary representation of previous number = "
                + previousNumber(num));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation to find the binary
# representation of previous number

# function to find the required
# binary representation
def previousNumber(num1):
    n = len(num1);
    num = list(num1);

    # if the number is '1'
    if (num1 == "1"):
        return "0";
    i = n - 1;

    # examine bits from right to left
    while (i >= 0):

        # if '1' is encountered, convert
        # it to '0' and then break
        if (num[i] == '1'):
            num[i] = '0';
            break;

        # else convert '0' to '1'
        else:
            num[i] = '1';
        i -= 1;

    # if only the 1st bit in the
    # binary representation was '1'
    if (i == 0):
        return num[1:n];

    # final binary representation
    # of the required number
    return '' . join(num);

# Driver code
num = "10110";
print("Binary representation of previous number =",
                              previousNumber(num));

# This code is contributed by mits
```

## C#

```
// C# implementation to find the binary
// representation of previous number
using System;

class GFG
{

    // function to find the required
    // binary representation
    static String previousNumber(String num)
    {
        int n = num.Length;

        // if the number is '1'
        if (num.CompareTo("1") == 0)
        {
            return "0";
        }

        // examine bits from right to left
        int i;
        for (i = n - 1; i >= 0; i--)
        {

            // if '1' is encountered, convert
            // it to '0' and then break
            if (num[i] == '1')
            {
                num = num.Substring(0, i) + '0' +
                            num.Substring(i + 1);

                // num.charAt(i) = '0';
                break;
            }

            // else convert '0' to '1'
            else
            {
                num = num.Substring(0, i) + '1' +
                            num.Substring(i + 1);
            }
            //num.at(i) = '1';
        }

        // if only the 1st bit in the
        // binary representation was '1'
        if (i == 0)
        {
            return num.Substring(1, n - 1);
        }

        // final binary representation
        // of the required number
        return num;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String num = "10110";
        Console.Write("Binary representation of previous number = "
                + previousNumber(num));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the binary
// representation of previous number

// function to find the required
// binary representation
function previousNumber($num)
{
    $n = strlen($num);

    // if the number is '1'
    if ($num == "1")
        return "0";
    $i = $n - 1;

    // examine bits from right to left
    for (; $i >= 0; $i--)
    {

        // if '1' is encountered, convert
        // it to '0' and then break
        if ($num[$i] == '1')
        {
            $num[$i] = '0';
            break;
        }

        // else convert '0' to '1'
        else
            $num[$i] = '1';
    }

    // if only the 1st bit in the
    // binary representation was '1'
    if ($i == 0)
        return substr($num,1, $n - 1);

    // final binary representation
    // of the required number
    return $num;
}

    // Driver code
    $num = "10110";
    echo "Binary representation of previous number = ".previousNumber($num);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the binary
// representation of previous number
// function to find the required
// binary representation
function previousNumber(num)
{
    var n = num.length;

    // if the number is '1'
    if (num == "1")
        return "0";

    // examine bits from right to left
    var i;
    for (i = n - 1; i >= 0; i--) {

        // if '1' is encountered, convert
        // it to '0' and then break
        if (num[i] == '1') {
            num[i] = '0';
            break;
        }

        // else convert '0' to '1'
        else
            num[i] = '1';
    }

    // if only the 1st bit in the
    // binary representation was '1'
    if (i == 0)
        return num.substring(1, n);

    // final binary representation
    // of the required number
    return num.join('');
}

// Driver program to test above
var num = "10110".split('');
document.write( "Binary representation of previous number = "
     + previousNumber(num));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Binary representation of previous number = 10101
```

**时间复杂度:**O(n)**n**为输入的位数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。