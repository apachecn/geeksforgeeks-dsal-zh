# 给定字符串字符的 ASCII 值的平均值

> 原文:[https://www . geesforgeks . org/给定字符串的 ascii 字符值平均值/](https://www.geeksforgeeks.org/average-of-ascii-values-of-characters-of-a-given-string/)

给定一个字符串，任务是找到字符串中字符的 ASCII 值的平均值。

**示例:**

```
Input: str =  "for"
Output: 109
'f'= 102, 'o' = 111, 'r' = 114
(102 + 111 + 114)/3 = 109 

Input: str = "geeks" 
Output: 105
```

**来源:**T2】微软实习经历 T4】

**方法:**开始迭代字符串的字符，并将它们的 ASCII 值添加到变量中。最后，将字符的 ASCII 值之和除以字符串长度，即字符串中的字符总数。

## C++

```
// C++ code to find average
// of ASCII characters
#include <bits/stdc++.h>
using namespace std;

// Function to find average
// of ASCII value of chars
int averageValue(string s)
{
    int sum_char = 0;

    // loop to sum the ascii
    // value of chars
    for (int i = 0; i < s.length(); i++)
    {
        sum_char += (int)s[i];
    }

    // Returning average of chars
    return sum_char / s.length();
}

// Driver code
int main()
{
    string s = "GeeksforGeeks";

    cout << averageValue(s);
    return 0;
}

// This code is contributed
// by Subhadeep
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find average of ASCII characters
import java.io.*;

class GFG {

    // Function to find average of ASCII value of chars
    public static int averageValue(String s)
    {
        int sum_char = 0;

        // loop to sum the ascii value of chars
        for (int i = 0; i < s.length(); i++) {
            sum_char += (int)s.charAt(i);
        }

        // Returning average of chars
        return sum_char / s.length();
    }

    // Driver code
    public static void main(String[] args)
    {

        String s = "GeeksforGeeks";

        System.out.println(averageValue(s));
    }
}
```

## 蟒蛇 3

```
# Python 3 code to find average
# of ASCII characters

# Function to find average
# of ASCII value of chars
def averageValue(s):
    sum_char = 0

    # loop to sum the ascii
    # value of chars
    for i in range(len(s)):
        sum_char += ord(s[i])

    # Returning average of chars
    return sum_char // len(s)

# Driver code
if __name__ == "__main__":

    s = "GeeksforGeeks"

    print(averageValue(s))

# This code is contributed by ita_c
```

## C#

```
// C# code to find average of
// ASCII characters
using System;

class GFG
{

// Function to find average of
// ASCII value of chars
public static int averageValue(String s)
{
    int sum_char = 0;

    // loop to sum the ascii value of chars
    for (int i = 0; i < s.Length; i++)
    {
        sum_char += (int)s[i];
    }

    // Returning average of chars
    return sum_char / s.Length;
}

// Driver code
public static void Main()
{
    String s = "GeeksforGeeks";

    Console.Write(averageValue(s));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find average
// of ASCII characters

// Function to find average
// of ASCII value of chars
function averageValue( $s)
{
    $sum_char = 0;

    // loop to sum the ascii
    // value of chars
    for ( $i = 0; $i < strlen($s); $i++)

    {

        $sum_char += ord($s[$i]);
    }

    // Returning average of chars
    return (int)($sum_char / strlen($s));
}

// Driver code
$s = "GeeksforGeeks";

echo averageValue($s);

// This code is contributed
// by 29AjayKumar
?>
```

## java 描述语言

```
<script>
// Javascript code to find average of ASCII characters

    // Function to find average of ASCII value of chars
    function averageValue(s)
    {
        let sum_char = 0;

        // loop to sum the ascii value of chars
        for (let i = 0; i < s.length; i++) {
            sum_char +=(s[i]).charCodeAt(0);

        }

        // Returning average of chars
        return Math.floor(sum_char / s.length);   
    }

    // Driver code
    let s = "GeeksforGeeks";
    document.write(averageValue(s));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
101
```

**时间复杂度:** O(l)，其中 l 为字符串的长度。
**辅助空间:** O(1)