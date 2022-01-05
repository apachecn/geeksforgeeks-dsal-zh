# 使用字符串中两个数字之间的“+”或“*”符号计算最大值

> 原文:[https://www . geesforgeks . org/compute-maximum-value-use-sign-two-numbers-string/](https://www.geeksforgeeks.org/calculate-maximum-value-using-sign-two-numbers-string/)

给定一个数字字符串，任务是从字符串中找到最大值，可以在任意两个数字之间添加一个“+”或“*”符号。
**例:**

```
Input : 01231
Output : 
((((0 + 1) + 2) * 3) + 1) = 10
In above manner, we get the maximum value i.e. 10

Input : 891
Output :73
As 8*9*1 = 72 and 8*9+1 = 73.So, 73 is maximum.
```

问于:脸书

任务非常简单，因为我们可以在乘以所有值时获得最大值，但重点是处理 0 和 1 的情况，即在乘以 0 和 1 时，我们获得的值比加上 0 和 1 时的值低。
因此，在任意两个数字之间使用“*”符号(包含 0 和 1 的数字除外)，如果其中任何一个数字是 0 和 1，则使用“+”。

## C++

```
// C++ program to find maximum value
#include <bits/stdc++.h>

using namespace std;

// Function to calculate the value
int calcMaxValue(string str)
{
    // Store first character as integer
    // in result
    int res = str[0] -'0';

    // Start traversing the string
    for (int i = 1; i < str.length(); i++)
    {
        // Check if any of the two numbers
        // is 0 or 1, If yes then add current
        // element
        if (str[i] == '0' || str[i] == '1' ||
            res < 2 )
            res += (str[i]-'0');

        // Else multiply
        else
            res *= (str[i]-'0');
    }

    // Return maximum value
    return res;
}

// Drivers code
int main()
{
    string str = "01891";
    cout << calcMaxValue(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum value

public class GFG
{
    // Method to calculate the value
    static int calcMaxValue(String str)
    {
        // Store first character as integer
        // in result
        int res = str.charAt(0) -'0';

        // Start traversing the string
        for (int i = 1; i < str.length(); i++)
        {
            // Check if any of the two numbers
            // is 0 or 1, If yes then add current
            // element
            if (str.charAt(i) == '0' || str.charAt(i) == '1' ||
                res < 2 )
                res += (str.charAt(i)-'0');

            // Else multiply
            else
                res *= (str.charAt(i)-'0');
        }

        // Return maximum value
        return res;
    }

    // Driver Method
    public static void main(String[] args)
    {
        String str = "01891";
        System.out.println(calcMaxValue(str));
    }
}
```

## 蟒蛇 3

```
# Python program to find maximum value

# Function to calculate the value
def calcMaxValue(str):

    # Store first character as integer
    # in result
    res = ord(str[0]) - 48

    # Start traversing the string
    for i in range(1, len(str)):

        # Check if any of the two numbers
        # is 0 or 1, If yes then add current
        # element
        if(str[i] == '0' or
           str[i] == '1' or res < 2):
            res += ord(str[i]) - 48
        else:
            res *= ord(str[i]) - 48

    return res        

# Driver code
if __name__== "__main__":
    str = "01891";
    print(calcMaxValue(str));

# This code is contributed by Sairahul Jella
```

## C#

```
//C# program to find maximum value
using System;

class GFG
{

    // Method to calculate the value
    static int calcMaxValue(String str)
    {
        // Store first character as integer
        // in result
        int res = str[0] -'0';

        // Start traversing the string
        for (int i = 1; i < str.Length; i++)
        {
            // Check if any of the two numbers
            // is 0 or 1, If yes then add current
            // element
            if (str[i] == '0' ||
                str[i] == '1' || res < 2 )
                res += (str[i] - '0');

            // Else multiply
            else
                res *= (str[i] - '0');
        }

        // Return maximum value
        return res;
    }

    // Driver Code
    static public void Main ()
    {
        String str = "01891";
        Console.Write(calcMaxValue(str));
    }
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// maximum value

// Function to calculate
// the value
function calcMaxValue($str)
{
    // Store first character
    // as integer in result
    $res = $str[0] - '0';

    // Start traversing
    // the string
    for ($i = 1; $i < strlen($str); $i++)
    {
        // Check if any of the
        // two numbers is 0 or
        // 1, If yes then add
        // current element
        if ($str[$i] == '0' || $str[$i] == '1' ||
                           $res < 2  )
            $res += ($str[$i] - '0');

        // Else multiply
        else
            $res *= ($str[$i] - '0');
    }

    // Return maximum value
    return $res;
}

// Driver code
$str = "01891";
echo calcMaxValue($str);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to
    // find maximum value

    // Method to calculate the value
    function calcMaxValue(str)
    {
        // Store first character as integer
        // in result
        let res = str[0].charCodeAt() -
        '0'.charCodeAt();

        // Start traversing the string
        for (let i = 1; i < str.length; i++)
        {
            // Check if any of the two numbers
            // is 0 or 1, If yes then add current
            // element
            if (str[i] == '0' ||
                str[i] == '1' || res < 2 )
                res += (str[i].charCodeAt() -
                '0'.charCodeAt());

            // Else multiply
            else
                res *= (str[i].charCodeAt() -
                '0'.charCodeAt());
        }

        // Return maximum value
        return res;
    }

    let str = "01891";
      document.write(calcMaxValue(str));

</script>
```

**输出:**

```
82
```

上面的程序考虑了小输入的情况，即 C/C++最多可以处理最大值的范围。
参考:
[【https://www.careercup.com/question?id=5745795300065280】](https://www.careercup.com/question?id=5745795300065280)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。