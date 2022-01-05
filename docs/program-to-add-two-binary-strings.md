# 程序添加两个二进制字符串

> 原文:[https://www . geesforgeks . org/program-to-add-two-binary-strings/](https://www.geeksforgeeks.org/program-to-add-two-binary-strings/)

给定两个二进制字符串，返回它们的和(也是二进制字符串)。
**例:**

```
Input:  a = "11", b = "1"
Output: "100" 
```

**强烈建议你尽量减少浏览器，先自己试试**
思路是从两个字符串的最后一个字符开始，逐个计算数字和。如果总和大于 1，则存储下一位数的进位。

## C++

```
// C++ program to add two binary strings
#include<bits/stdc++.h>
using namespace std;

// This function adds two binary strings and return
// result as a third string
string addBinary(string a, string b)
{
    string result = ""; // Initialize result
    int s = 0;          // Initialize digit sum

    // Traverse both strings starting from last
    // characters
    int i = a.size() - 1, j = b.size() - 1;
    while (i >= 0 || j >= 0 || s == 1)
    {
        // Comput sum of last digits and carry
        s += ((i >= 0)? a[i] - '0': 0);
        s += ((j >= 0)? b[j] - '0': 0);

        // If current digit sum is 1 or 3, add 1 to result
        result = char(s % 2 + '0') + result;

        // Compute carry
        s /= 2;

        // Move to next digits
        i--; j--;
    }
    return result;
}

// Driver program
int main()
{
    string a = "1101", b="100";
    cout << addBinary(a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to add
// two binary strings

public class GFG {

    // This function adds two
    // binary strings and return
    // result as a third string
    static String addBinary(String a, String b)
    {

        // Initialize result
        String result = "";

        // Initialize digit sum
        int s = 0;        

        // Traverse both strings starting
        // from last characters
        int i = a.length() - 1, j = b.length() - 1;
        while (i >= 0 || j >= 0 || s == 1)
        {

            // Comput sum of last
            // digits and carry
            s += ((i >= 0)? a.charAt(i) - '0': 0);
            s += ((j >= 0)? b.charAt(j) - '0': 0);

            // If current digit sum is
            // 1 or 3, add 1 to result
            result = (char)(s % 2 + '0') + result;

            // Compute carry
            s /= 2;

            // Move to next digits
            i--; j--;
        }

    return result;
    }

    //Driver code
    public static void main(String args[])
    {
        String a = "1101", b="100";

        System.out.print(addBinary(a, b));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python Solution for above problem:

# This function adds two binary
# strings return the resulting string
def add_binary_nums(x, y):
        max_len = max(len(x), len(y))

        x = x.zfill(max_len)
        y = y.zfill(max_len)

        # initialize the result
        result = ''

        # initialize the carry
        carry = 0

        # Traverse the string
        for i in range(max_len - 1, -1, -1):
            r = carry
            r += 1 if x[i] == '1' else 0
            r += 1 if y[i] == '1' else 0
            result = ('1' if r % 2 == 1 else '0') + result
            carry = 0 if r < 2 else 1     # Compute the carry.

        if carry !=0 : result = '1' + result

        return result.zfill(max_len)

# Driver code
print(add_binary_nums('1101', '100'))

# This code is contributed
# by Anand Khatri
```

## C#

```
// C# program to add
// two binary strings
using System;

class GFG {

    // This function adds two
    // binary strings and return
    // result as a third string
    static string addBinary(string a,
                            string b)
    {

        // Initialize result
        string result = "";

        // Initialize digit sum
        int s = 0;        

        // Traverse both strings starting
        // from last characters
        int i = a.Length - 1, j = b.Length - 1;
        while (i >= 0 || j >= 0 || s == 1)
        {

            // Comput sum of last
            // digits and carry
            s += ((i >= 0)? a[i] - '0': 0);
            s += ((j >= 0)? b[j] - '0': 0);

            // If current digit sum is
            // 1 or 3, add 1 to result
            result = (char)(s % 2 + '0') + result;

            // Compute carry
            s /= 2;

            // Move to next digits
            i--; j--;
        }
    return result;
    }

// Driver Code   
public static void Main()
{
    string a = "1101", b="100";
    Console.Write( addBinary(a, b));
}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to add two binary strings

// This function adds two binary strings
// and return result as a third string
function addBinary($a, $b)
{
    $result = ""; // Initialize result
    $s = 0;     // Initialize digit sum

    // Traverse both strings starting
    // from last characters
    $i = strlen($a) - 1;
    $j = strlen($b) - 1;
    while ($i >= 0 || $j >= 0 || $s == 1)
    {
        // Comput sum of last digits and carry
        $s += (($i >= 0)? ord($a[$i]) -
                          ord('0'): 0);
        $s += (($j >= 0)? ord($b[$j]) -
                          ord('0'): 0);

        // If current digit sum is 1 or 3,
        // add 1 to result
        $result = chr($s % 2 + ord('0')) . $result;

        // Compute carry
        $s = (int)($s / 2);

        // Move to next digits
        $i--; $j--;
    }
    return $result;
}

// Driver Code
$a = "1101";
$b = "100";
echo addBinary($a, $b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to add
// two binary strings

// This function adds two
// binary strings and return
// result as a third string
function addBinary(a, b)
{

    // Initialize result
    var result = "";

    // Initialize digit sum
    var s = 0;        

    // Traverse both strings starting
    // from last characters
    var i = a.length - 1, j = b.length - 1;
    while (i >= 0 || j >= 0 || s == 1)
    {

        // Comput sum of last
        // digits and carry
        s += ((i >= 0)? a.charAt(i).charCodeAt(0) -
        '0'.charCodeAt(0): 0);
        s += ((j >= 0)? b.charAt(j).charCodeAt(0) -
        '0'.charCodeAt(0): 0);

        // If current digit sum is
        // 1 or 3, add 1 to result
        result = String.fromCharCode(parseInt(s % 2) +
        '0'.charCodeAt(0)) + result;

        // Compute carry
        s = parseInt(s/2);

        // Move to next digits
        i--; j--;
    }

return result;
}

//Driver code
var a = "1101", b="100";

document.write(addBinary(a, b));

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
10001
```

感谢 Gaurav Ahirwar 提出上述解决方案。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息