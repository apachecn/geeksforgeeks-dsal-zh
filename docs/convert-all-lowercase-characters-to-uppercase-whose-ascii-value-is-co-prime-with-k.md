# 将所有小写字符转换为 ASCII 值与 k 同素的大写字符

> 原文:[https://www . geesforgeks . org/convert-all-小写-characters-to-大写-what-ascii-value-is-co-prime-with-k/](https://www.geeksforgeeks.org/convert-all-lowercase-characters-to-uppercase-whose-ascii-value-is-co-prime-with-k/)

给定一个整数“k”和一个由英文字母组成的字符串“str”。任务是将所有小写字符转换为 ASCII 值与 k 同素的大写字符。
**示例:**

> **输入:** str = "geeksforgeeks "，k = 4
> **输出:**GEEKSfOrGEEKS
> “f”和“r”是 ASCII 值不与 4 同素的唯一字符。
> **输入:** str = "Ac "，k = 2
> **输出:** AC
> 唯一的小写字符是' c '，ASCII 值' c '是 99，与 2 同素。

**进场:**

*   遍历给定字符串中的所有字符，检查当前字符是否为小写，以及它的 ASCII 值是否与“k”同素
*   要检查同素，请检查 k 值的 gcd 是否为“1”。
*   如果满足上述条件，那么将小写字母转换为大写字母。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// function to modify the string
void convert_str(string s, int k)
{
    // length of the string
    int l = s.length();

    for (int i = 0; i < l; i++) {
        int ascii = (int)s[i];

        // check if the character is
        // lowercase and co-prime with k
        if (ascii >= 'a' && ascii <= 'z'
            && __gcd(ascii, k) == 1) {

            // change the character
            // to upper-case
            char c = s[i] - 32;
            s[i] = c;
        }
    }

    cout << s << "\n";
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    int k = 4;

    convert_str(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// function to modify the string
    static void convert_str(String str, int k)
    {
        // length of the string
        char[] s = str.toCharArray();
        int l = s.length;

        for (int i = 0; i < l; i++)
        {
            int ascii = (int) s[i];

            // check if the character is
            // lowercase and co-prime with k
            if (ascii >= 'a' && ascii <= 'z'
                    && __gcd(ascii, k) == 1)
            {

                // change the character
                // to upper-case
                char c = (char) (s[i] - 32);
                s[i] = c;
            }
        }
        System.out.println(String.valueOf(s));
    }

    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0) 
        {
            return b;
        }
        if (b == 0)
        {
            return a;
        }

        // base case
        if (a == b)
        {
            return a;
        }

        // a is greater
        if (a > b)
        {
            return __gcd(a - b, b);
        }
        return __gcd(a, b - a);
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeksforgeeks";
        int k = 4;
        convert_str(s, k);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# function to modify the string
def convert_str(s, k):

    modified_string = ""
    for i in range(0, len(s)):
        ascii = ord(s[i])

        # check if the character is
        # lowercase and co-prime with k
        if (ascii >= ord('a') and
            ascii <= ord('z') and
            gcd(ascii, k) == 1):

            # change the character to upper-case
            modified_string += chr(ascii - 32)

        else:
            modified_string += s[i]

    print(modified_string)

# Driver code
if __name__ == "__main__":

    s = "geeksforgeeks"
    k = 4

    convert_str(s, k)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // function to modify the string
    static void convert_str(String str, int k)
    {

        // length of the string
        char[] s = str.ToCharArray();
        int l = s.Length;

        for (int i = 0; i < l; i++)
        {
            int ascii = (int) s[i];

            // check if the character is
            // lowercase and co-prime with k
            if (ascii >= 'a' && ascii <= 'z'
                    && __gcd(ascii, k) == 1)
            {

                // change the character
                // to upper-case
                char c = (char) (s[i] - 32);
                s[i] = c;
            }
        }
        Console.WriteLine(String.Join("", s));
    }

    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
        {
            return b;
        }
        if (b == 0)
        {
            return a;
        }

        // base case
        if (a == b)
        {
            return a;
        }

        // a is greater
        if (a > b)
        {
            return __gcd(a - b, b);
        }
        return __gcd(a, b - a);
    }

    // Driver code
    public static void Main()
    {
        String s = "geeksforgeeks";
        int k = 4;
        convert_str(s, k);
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// function to modify the string
function convert_str($str, $k)
{
    // length of the string
    $l = strlen($str);
    $modified_string = "";

    for ($i = 0; $i < $l; $i++)
    {
        $ascii = ord($str[$i]);

        // check if the character is
        // lowercase and co-prime with k
        if ($ascii >= ord('a') &&
            $ascii <= ord('z') &&
            __gcd($ascii, $k) == 1)
        {

            // change the character to upper-case
            $modified_string = $modified_string.chr($ascii - 32);
        }
        else
        {
            $modified_string = $modified_string.$str[$i];
        }
    }
    echo ($modified_string);
}

function __gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0)
    {
        return $b;
    }
    if ($b == 0)
    {
        return $a;
    }

    // base case
    if ($a == $b)
    {
        return $a;
    }

    // a is greater
    if ($a > $b)
    {
        return __gcd($a - $b, $b);
    }
    return __gcd($a, $b - $a);
}

// Driver code
$s = "geeksforgeeks";
$k = 4;
convert_str($s, $k);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // function to modify the string
      function convert_str(s, k) {
        // length of the string
        var l = s.length;
        var newStr = "";

        for (var i = 0; i < l; i++) {
          var ascii = s[i].charCodeAt(0);

          // check if the character is
          // lowercase and co-prime with k
          if (
            ascii >= "a".charCodeAt(0) &&
            ascii <= "z".charCodeAt(0) &&
            __gcd(ascii, k) === 1
          ) {
            // change the character
            // to upper-case
            var c = String.fromCharCode(s[i].charCodeAt(0) - 32);
            newStr += c;
          } else {
            newStr += s[i];
          }
        }
        document.write(newStr);
      }

      function __gcd(a, b) {
        // Everything divides 0
        if (a === 0) {
          return b;
        }
        if (b === 0) {
          return a;
        }

        // base case
        if (a === b) {
          return a;
        }

        // a is greater
        if (a > b) {
          return __gcd(a - b, b);
        }
        return __gcd(a, b - a);
      }

      // Driver code

      var s = "geeksforgeeks";
      var k = 4;
      convert_str(s, k);
    </script>
```

**Output:** 

```
GEEKSfOrGEEKS
```