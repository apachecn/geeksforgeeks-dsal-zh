# 检查一个字符串的长度是否等于其最后一个

所附加的数字

> 原文:[https://www . geesforgeks . org/check-length-string-equal-number-appended-last/](https://www.geeksforgeeks.org/check-length-string-equal-number-appended-last/)

给定一个最后可以附加数字的字符串。您需要找到除该数字之外的字符串长度是否等于该数字。例如对于“helloworld10”，答案为 True，因为 helloworld 由 10 个字母组成。字符串长度小于 10，000。

**示例:**

```
Input:  str = "geeks5"
Output:  Yes
Explanation : As geeks is of 5 length and at 
              last number is also 5.

Input:  str = "geeksforgeeks15"
Output:  No
Explanation: As geeksforgeeks is of 13 length and
             at last number is 15 i.e. not equal
```

提问时间:[编码面试](https://www.geeksforgeeks.org/codenation-interview-experience-set-2-on-campus-for-internship/)

一种**简单的方法**是从开始遍历并从字符串中检索数字，并检查字符串的长度-数字中的数字是否=数字

一种有效的方法是执行以下步骤

1.  从头到尾遍历字符串，并一直存储该数字，直到它小于整个字符串的长度。
2.  如果该数字等于字符串的长度，但该数字的位数除外，则返回 true。
3.  否则返回 false。

## C++

```
// C++ program to check if size of string is appended
// at the end or not.
#include <bits/stdc++.h>
using namespace std;

// Function to find if given number is equal to
// length or not
bool isequal(string str)
{
    int n = str.length();

    // Traverse string from end and find the number
    // stored at the end.
    // x is used to store power of 10.
    int num = 0, x = 1, i = n - 1;
    for (i = n - 1; i >= 0; i--) {
        if ('0' <= str[i] && str[i] <= '9') {
            num = (str[i] - '0') * x + num;
            x = x * 10;
            if(num>=n)
                return false;
        }
        else
            break;
    }

    // Check if number is equal to string length except
    // that number's digits
    return num == i + 1;
}

// Drivers code
int main()
{
    string str = "geeksforgeeks13";
    isequal(str) ? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if size of
// string is appended at the end or not.
import java.io.*;

class GFG {

    // Function to find if given number is
    // equal to length or not
    static boolean isequal(String str)
    {
        int n = str.length();

        // Traverse string from end and find the number
        // stored at the end.
        // x is used to store power of 10.
        int num = 0, x = 1, i = n - 1;
        for (i = n - 1; i >= 0; i--)
        {
            if ('0' <= str.charAt(i) &&
                str.charAt(i) <= '9')
            {
                num = (str.charAt(i) - '0') * x + num;
                x = x * 10;
                if(num>=n)
                    return false;
            }
            else
                break;
        }

        // Check if number is equal to string
        // length except that number's digits
        return num == i + 1;
    }

    // Drivers code
    static public void main(String[] args)
    {
        String str = "geeksforgeeks13";
        if (isequal(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This Code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to check if size of
# string is appended at the end or not.

# Function to find if given number
# is equal to length or not
def isequal(str):

    n = len(str)

    # Traverse string from end and
    # find the number stored at the end.
    # x is used to store power of 10.
    num = 0
    x = 1
    i = n - 1
    for i in range(n - 1, -1,-1) :
        if ('0' <= str[i] and str[i] <= '9') :
            num = (ord(str[i]) - ord('0')) * x + num
            x = x * 10
            if (num>=n):
                return false

        else:
            break

    # Check if number is equal to string
    # length except that number's digits
    return num == i + 1

# Driver Code
if __name__ == "__main__":

    str = "geeksforgeeks13"
    print("Yes") if isequal(str) else print("No")

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to check if size of
// string is appended at the end or not.
using System;

class GFG {

    // Function to find if given number
    // is equal to length or not
    static bool isequal(string str)
    {
        int n = str.Length;

        // Traverse string from end and find the number
        // stored at the end.
        // x is used to store power of 10.
        int num = 0, x = 1, i = n - 1;
        for (i = n - 1; i >= 0; i--)
        {
            if ('0' <= str[i] && str[i] <= '9') {
                num = (str[i] - '0') * x + num;
                x = x * 10;
                if(num>=n)
                    return false;
            }
            else
                break;
        }

        // Check if number is equal to string
        // length except that number's digits
        return num == i + 1;
    }

    // Drivers code
    static public void Main()
    {
        string str = "geeksforgeeks13";
        if (isequal(str))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if size
// of string is appended at
// the end or not.

// Function to find if given
// number is equal to length or not
function isequal($str)
{
    $n = strlen($str);

    // Traverse string from end
    // and find the number stored
    // at the end. x is used to
    // store power of 10.
    $num = 0; $x = 1; $i = $n - 1;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        if ('0' <= $str[$i] &&
                   $str[$i] <= '9')
        {
            $num = ($str[$i] - '0') *
                           $x + $num;
            $x = $x * 10;
            if($num>=$n)
                return false;
        }
        else
            break;
    }

    // Check if number is equal
    // to string length except
    // that number's digits
    return $num == $i + 1;
}

// Driver code
$str = "geeksforgeeks13";
if(isequal($str))
echo "Yes" ;
else
echo "No";
return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if size of
// string is appended at the end or not.

// Function to find if given number is
// equal to length or not
function isequal(str)
{
    let n = str.length;

    // Traverse string from end and find
    // the number stored at the end.
    // x is used to store power of 10.
    let num = 0, x = 1, i = n - 1;
    for(i = n - 1; i >= 0; i--)
    {
        if ('0' <= str[i] &&
            str[i] <= '9')
        {
            num = (str[i] - '0') * x + num;
            x = x * 10;

            if (num >= n)
                return false;
        }
        else
            break;
    }

    // Check if number is equal to string
    // length except that number's digits
    return num == i + 1;
}

// Driver code
let str = "geeksforgeeks13";

if (isequal(str))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Yes
```

本文由 [**萨希尔·查布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。