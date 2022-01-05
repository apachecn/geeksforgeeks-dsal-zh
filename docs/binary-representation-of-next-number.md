# 下一个数字的二进制表示

> 原文:[https://www . geeksforgeeks . org/下一个数字的二进制表示/](https://www.geeksforgeeks.org/binary-representation-of-next-number/)

给定一个表示正数 n 的二进制表示的二进制输入，求 n+1 的二进制表示。
二进制输入可能适合也可能不适合无符号长整型。
**例:**

```
Input : 10011
Output : 10100
Here n = (19)10 = (10011)2
next greater integer = (20)10 = (10100)2 

Input : 111011101001111111
Output : 111011101010000000 
```

我们将输入存储为字符串，这样就可以处理大量的数字。我们从最右边的字符开始遍历字符串，并将所有 1 转换为 0，直到找到 0。最后，将找到的 0 转换为 1。如果找不到 0，我们会在整个字符串中添加 1。

```
string nextGreater(num)
  l = num.length

  // Find first 0 from right side. While
  // searching, convert 1s to 0s
  for i = l-1 to 0
    if num[i] == '0'
       num[i] = '1'
       break
    else
       num[i] = '0'

  // If there was no 0  
  if i < 0
      num = '1' + num
  return num        
```

以下是上述想法的实现。

## C++

```
// C++ implementation to find the binary
// representation of next greater integer
#include <bits/stdc++.h>
using namespace std;

// function to find the required
// binary representation
string nextGreater(string num)
{
    int l = num.size();

    // examine bits from the right
    for (int i=l-1; i>=0; i--)
    {
        // if '0' is encountered, convert
        // it to '1' and then break
        if (num.at(i) == '0')
        {
            num.at(i) = '1';
            break;
        }

        // else convert '1' to '0'
        else
            num.at(i) = '0';
    }

    // if the binary representation
    // contains only the set bits
    if (i < 0)
        num = "1" + num;

    // final binary representation
    // of the required integer
    return num;
}

// Driver program to test above
int main()
{
    string num = "10011";
    cout << "Binary representation of next number = "
         << nextGreater(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the binary
// representation of next greater integer

class GFG {

// function to find the required
// binary representation
    static String nextGreater(String num) {

        int l = num.length();
        int i;
        // examine bits from the right
        for (i = l - 1; i >= 0; i--) {
            // if '0' is encountered, convert
            // it to '1' and then break
            if (num.charAt(i) == '0') {
                num = num.substring(0, i) + '1' + num.substring(i+1);
                break;
            } // else convert '1' to '0'
            else {
                num = num.substring(0, i) + '0' + num.substring(i + 1);
            }
            // num[i] = '0';
        }

        // if the binary representation
        // contains only the set bits
        if (i < 0) {
            num = "1" + num;
        }

        // final binary representation
        // of the required integer
        return num;
    }

// Driver program to test above
    public static void main(String[] args) {
        String num = "10011";
        System.out.println("Binary representation of next number = "
                + nextGreater(num));
    }
}
//this code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the binary
# representation of next greater integer

# function to find the required
# binary representation
def nextGreater(num1):

    l = len(num1);
    num = list(num1);

    # examine bits from the right
    i = l-1;
    while(i >= 0):
        # if '0' is encountered, convert
        # it to '1' and then break
        if (num[i] == '0'):
            num[i] = '1';
            break;

        # else convert '1' to '0'
        else:
            num[i] = '0';
        i-=1;

    # if the binary representation
    # contains only the set bits
    num1 = ''.join(num);
    if (i < 0):
        num1 = '1' + num1;

    # final binary representation
    # of the required integer
    return num1;

# Driver Code
num = "10011";
print("Binary representation of next number = ",nextGreater(num));

# This code is contributed by mits
```

## C#

```

// C# implementation to find the binary
// representation of next greater integer
 using System;
public class GFG {

// function to find the required
// binary representation
    static String nextGreater(String num) {

        int l = num.Length;
        int i;
        // examine bits from the right
        for (i = l - 1; i >= 0; i--) {
            // if '0' is encountered, convert
            // it to '1' and then break
            if (num[i] == '0') {
                num = num.Substring(0, i) + '1' + num.Substring(i+1);
                break;
            } // else convert '1' to '0'
            else {
                num = num.Substring(0, i) + '0' + num.Substring(i + 1);
            }
            // num[i] = '0';
        }

        // if the binary representation
        // contains only the set bits
        if (i < 0) {
            num = "1" + num;
        }

        // final binary representation
        // of the required integer
        return num;
    }

// Driver program to test above
    public static void Main() {
        String num = "10011";
        Console.WriteLine("Binary representation of next number = "
                + nextGreater(num));
    }
}
//this code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the binary
// representation of next greater integer

// function to find the required
// binary representation
function nextGreater($num)
{
    $l = strlen($num);

    // examine bits from the right
    for ($i = $l - 1; $i >= 0; $i--)
    {
        // if '0' is encountered, convert
        // it to '1' and then break
        if ($num[$i] == '0')
        {
            $num[$i] = '1';
            break;
        }

        // else convert '1' to '0'
        else
            $num[$i] = '0';
    }

    // if the binary representation
    // contains only the set bits
    if ($i < 0)
        $num = "1" . $num;

    // final binary representation
    // of the required integer
    return $num;
}

// Driver Code
$num = "10011";
echo "Binary representation of next number = " .
                              nextGreater($num);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the binary
// representation of next greater integer

    // function to find the required
    // binary representation
    function nextGreater(num)
    {
        let l = num.length;
        let i;
        // examine bits from the right
        for (i = l - 1; i >= 0; i--) {
            // if '0' is encountered, convert
            // it to '1' and then break
            if (num[i] == '0') {
                num = num.substring(0, i) + '1'
                + num.substring(i+1);
                break;
            } // else convert '1' to '0'
            else {
                num = num.substring(0, i) + '0'
                + num.substring(i + 1);
            }
            // num[i] = '0';
        }

        // if the binary representation
        // contains only the set bits
        if (i < 0) {
            num = "1" + num;
        }

        // final binary representation
        // of the required integer
        return num;
    }

    // Driver program to test above
    let num = "10011";
    document.write(
    "Binary representation of next number = "
                            + nextGreater(num)
    );

    // This code is contributed by rag2127

</script>
```

**输出:**

```
Binary representation of next number = 10100
```

**时间复杂度:** O(n)，其中 n 为输入中的位数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。