# 将罗马数字转换为 1 到 3999 之间的十进制数

> 原文:[https://www . geesforgeks . org/converting-Roman-numbers-decimal-lied-1-3999/](https://www.geeksforgeeks.org/converting-roman-numerals-decimal-lying-1-3999/)

给定一个罗马数字，任务是找到它对应的十进制值。

**示例:**

```
Input: IX
Output: 9
IX is a Roman symbol which represents 9 

Input: XL
Output: 40
XL is a Roman symbol which represents 40

Input: MCMIV
Output: 1904
M is a thousand, 
CM is nine hundred and 
IV is four
```

**罗马数字基于以下符号。**

```
SYMBOL       VALUE
  I            1
  IV           4
  V            5
  IX           9
  X            10
  XL           40
  L            50
  XC           90
  C            100
  CD           400
  D            500
  CM           900 
  M            1000
```

**Approach:** 罗马数字中的数字是这些符号按降序书写的字符串(例如 M 的第一个，然后是 D 的，等等)。).但是，在少数特定情况下，为了避免四个字符连续重复(如 IIII 或 XXXX)，通常使用**减法符号**，如下所示:

*   **I** 放在 **V** 或 **X** 前面表示少一个，所以四是 **IV** (少一个 5)，九是 IX(少一个 10)。
*   **X** 放在 **L** 或 **C** 前面表示少了十个，所以四十是 **XL** (少了 10 个 50 个)而 90 是 **XC** (少了 10 个 100 个)。
*   **C** 放在 **D** 或 **M** 前面表示少一百，所以四百是 **CD** (少一百五百)九百是 **CM** (少一百一千)。

**罗马数字转换为整数的算法:**

1.  将罗马数字字符串拆分为罗马符号(字符)。
2.  将罗马数字的每个符号转换成它所代表的值。
3.  从索引 0 开始，逐个获取符号:
    1.  如果符号的当前值大于或等于下一个符号的值，则将该值添加到运行总数中。
    2.  否则，通过将下一个符号的值与累计值相加来减去该值。

以下是上述算法的实现:

## C++

```
// Program to convert Roman
// Numerals to Numbers
#include <bits/stdc++.h>
using namespace std;

// This function returns value
// of a Roman symbol
int value(char r)
{
    if (r == 'I')
        return 1;
    if (r == 'V')
        return 5;
    if (r == 'X')
        return 10;
    if (r == 'L')
        return 50;
    if (r == 'C')
        return 100;
    if (r == 'D')
        return 500;
    if (r == 'M')
        return 1000;

    return -1;
}

// Returns decimal value of
// roman numaral
int romanToDecimal(string& str)
{
    // Initialize result
    int res = 0;

    // Traverse given input
    for (int i = 0; i < str.length(); i++)
    {
        // Getting value of symbol s[i]
        int s1 = value(str[i]);

        if (i + 1 < str.length())
        {
            // Getting value of symbol s[i+1]
            int s2 = value(str[i + 1]);

            // Comparing both values
            if (s1 >= s2)
            {
                // Value of current symbol
                // is greater or equal to
                // the next symbol
                res = res + s1;
            }
            else
            {
                // Value of current symbol is
                // less than the next symbol
                res = res + s2 - s1;
                i++;
            }
        }
        else {
            res = res + s1;
        }
    }
    return res;
}

// Driver Code
int main()
{
    // Considering inputs given are valid
    string str = "MCMIV";
    cout << "Integer form of Roman Numeral is "
        << romanToDecimal(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to convert Roman
// Numerals to Numbers
import java.util.*;

public class RomanToNumber
{
    // This function returns
    // value of a Roman symbol
    int value(char r)
    {
        if (r == 'I')
            return 1;
        if (r == 'V')
            return 5;
        if (r == 'X')
            return 10;
        if (r == 'L')
            return 50;
        if (r == 'C')
            return 100;
        if (r == 'D')
            return 500;
        if (r == 'M')
            return 1000;
        return -1;
    }

    // Finds decimal value of a
    // given romal numeral
    int romanToDecimal(String str)
    {
        // Initialize result
        int res = 0;

        for (int i = 0; i < str.length(); i++)
        {
            // Getting value of symbol s[i]
            int s1 = value(str.charAt(i));

            // Getting value of symbol s[i+1]
            if (i + 1 < str.length())
            {
                int s2 = value(str.charAt(i + 1));

                // Comparing both values
                if (s1 >= s2)
                {
                    // Value of current symbol
                    // is greater or equalto
                    // the next symbol
                    res = res + s1;
                }
                else
                {
                    // Value of current symbol is
                    // less than the next symbol
                    res = res + s2 - s1;
                    i++;
                }
            }
            else {
                res = res + s1;
            }
        }

        return res;
    }

    // Driver Code
    public static void main(String args[])
    {
        RomanToNumber ob = new RomanToNumber();

        // Considering inputs given are valid
        String str = "MCMIV";
        System.out.println("Integer form of Roman Numeral"
                           + " is "
                           + ob.romanToDecimal(str));
    }
}
```

## 计算机编程语言

```
# Python program to convert Roman Numerals
# to Numbers

# This function returns value of each Roman symbol

def value(r):
    if (r == 'I'):
        return 1
    if (r == 'V'):
        return 5
    if (r == 'X'):
        return 10
    if (r == 'L'):
        return 50
    if (r == 'C'):
        return 100
    if (r == 'D'):
        return 500
    if (r == 'M'):
        return 1000
    return -1

def romanToDecimal(str):
    res = 0
    i = 0

    while (i < len(str)):

        # Getting value of symbol s[i]
        s1 = value(str[i])

        if (i + 1 < len(str)):

            # Getting value of symbol s[i + 1]
            s2 = value(str[i + 1])

            # Comparing both values
            if (s1 >= s2):

                # Value of current symbol is greater
                # or equal to the next symbol
                res = res + s1
                i = i + 1
            else:

                # Value of current symbol is greater
                # or equal to the next symbol
                res = res + s2 - s1
                i = i + 2
        else:
            res = res + s1
            i = i + 1

    return res

# Driver code
print("Integer form of Roman Numeral is"),
print(romanToDecimal("MCMIV"))
```

## C#

```
// C# Program to convert Roman
// Numerals to Numbers
using System;

class GFG {
    // This function returns value
    // of a Roman symbol
    public virtual int value(char r)
    {
        if (r == 'I')
            return 1;
        if (r == 'V')
            return 5;
        if (r == 'X')
            return 10;
        if (r == 'L')
            return 50;
        if (r == 'C')
            return 100;
        if (r == 'D')
            return 500;
        if (r == 'M')
            return 1000;
        return -1;
    }

    // Finds decimal value of a
    // given romal numeral
    public virtual int romanToDecimal(string str)
    {
        // Initialize result
        int res = 0;

        for (int i = 0; i < str.Length; i++)
        {
            // Getting value of symbol s[i]
            int s1 = value(str[i]);

            // Getting value of symbol s[i+1]
            if (i + 1 < str.Length)
            {
                int s2 = value(str[i + 1]);

                // Comparing both values
                if (s1 >= s2)
                {
                    // Value of current symbol is greater
                    // or equalto the next symbol
                    res = res + s1;
                }
                else
                {
                    res = res + s2 - s1;
                    i++; // Value of current symbol is
                    // less than the next symbol
                }
            }
            else {
                res = res + s1;
                i++;
            }
        }

        return res;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        GFG ob = new GFG();

        // Considering inputs given are valid
        string str = "MCMIV";
        Console.WriteLine("Integer form of Roman Numeral"
                          + " is "
                          + ob.romanToDecimal(str));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to convert Roman
// Numerals to Numbers

// This function returns
// value of a Roman symbol
function value($r)
{
    if ($r == 'I')
        return 1;
    if ($r == 'V')
        return 5;
    if ($r == 'X')
        return 10;
    if ($r == 'L')
        return 50;
    if ($r == 'C')
        return 100;
    if ($r == 'D')
        return 500;
    if ($r == 'M')
        return 1000;

    return -1;
}

// Returns decimal value
// of roman numeral
function romanToDecimal(&$str)
{
    // Initialize result
    $res = 0;

    // Traverse given input
    for ($i = 0; $i < strlen($str); $i++)
    {
        // Getting value of
        // symbol s[i]
        $s1 = value($str[$i]);

        if ($i+1 < strlen($str))
        {
            // Getting value of
            // symbol s[i+1]
            $s2 = value($str[$i + 1]);

            // Comparing both values
            if ($s1 >= $s2)
            {
                // Value of current symbol
                // is greater or equal to
                // the next symbol
                $res = $res + $s1;
            }
            else
            {
                $res = $res + $s2 - $s1;
                $i++; // Value of current symbol is
                      // less than the next symbol
            }
        }
        else
        {
            $res = $res + $s1;
            $i++;
        }
    }
    return $res;
}

// Driver Code

// Considering inputs
// given are valid
$str ="MCMIV";
echo "Integer form of Roman Numeral is ",
              romanToDecimal($str), "\n";

// This code is contributed by ajit
?>
```

## 蟒蛇 3

```
def romanToInt(rom):
    value = {
        'M': 1000,
        'D': 500,
        'C': 100,
        'L': 50,
        'X': 10,
        'V': 5,
        'I': 1
    }

    # Initialize previous character and answer
    p = 0
    ans = 0

    # Traverse through all characters
    n = len(rom)
    for i in range(n-1, -1, -1):

        # If greater than or equal to previous,
        # add to answer
        if value[rom[i]] >= p:
            ans += value[rom[i]]

        # If smaller than previous
        else:
            ans -= value[rom[i]]

        # Update previous
        p = value[rom[i]]

    print(ans)

romanToInt('MCMIV')
```

## java 描述语言

```
<script>
// Program to convert Roman
// Numerals to Numberspublic
    // This function returns
    // value of a Roman symbol
    function value(r) {
        if (r == 'I')
            return 1;
        if (r == 'V')
            return 5;
        if (r == 'X')
            return 10;
        if (r == 'L')
            return 50;
        if (r == 'C')
            return 100;
        if (r == 'D')
            return 500;
        if (r == 'M')
            return 1000;
        return -1;
    }

    // Finds decimal value of a
    // given romal numeral
    function romanToDecimal( str) {
        // Initialize result
        var res = 0;

        for (i = 0; i < str.length; i++) {
            // Getting value of symbol s[i]
            var s1 = value(str.charAt(i));

            // Getting value of symbol s[i+1]
            if (i + 1 < str.length) {
                var s2 = value(str.charAt(i + 1));

                // Comparing both values
                if (s1 >= s2) {
                    // Value of current symbol
                    // is greater or equalto
                    // the next symbol
                    res = res + s1;
                } else {
                    // Value of current symbol is
                    // less than the next symbol
                    res = res + s2 - s1;
                    i++;
                }
            } else {
                res = res + s1;
            }
        }

        return res;
    }

    // Driver Code

        // Considering inputs given are valid
        var str = "MCMIV";
        document.write("Integer form of Roman Numeral"
        + " is " + romanToDecimal(str));

// This code contributed by umadevi9616
</script>
```

**Output**

```
Integer form of Roman Numeral is 1904
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为字符串的长度。
    只需要遍历字符串一次。
*   **空间复杂度:** O(1)。
    因为不需要额外的空间。

另一个解决方案–

## C++

```
// Program to convert Roman
// Numerals to Numbers
#include <bits/stdc++.h>
using namespace std;

// This function returns value
// of a Roman symbol
int romanToDecimal(string& str)
{
    map<char, int> m;
    m.insert({ 'I', 1 });
    m.insert({ 'V', 5 });
    m.insert({ 'X', 10 });
    m.insert({ 'L', 50 });
    m.insert({ 'C', 100 });
    m.insert({ 'D', 500 });
    m.insert({ 'M', 1000 });
    int sum = 0;
    for (int i = 0; i < str.length(); i++)
    {
        /*If present value is less than next value,
          subtract present from next value and add the
          resultant to the sum variable.*/
        if (m[str[i]] < m[str[i + 1]])
        {
            sum+=m[str[i+1]]-m[str[i]];
            i++;
            continue;
        }
        sum += m[str[i]];
    }
    return sum;
}

// Driver Code
int main()
{
    // Considering inputs given are valid
    string str = "MCMIV";
    cout << "Integer form of Roman Numeral is "
         << romanToDecimal(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to convert Roman
// Numerals to Numbers
import java.util.Map;
import java.util.HashMap;

class GFG{

private static final Map<Character,
                         Integer> roman = new HashMap<Character,
                                                      Integer>()
{{
    put('I', 1);
    put('V', 5);
    put('X', 10);
    put('L', 50);
    put('C', 100);
    put('D', 500);
    put('M', 1000);
}};

// This function returns value
// of a Roman symbol
private static int romanToInt(String s)
{
    int sum = 0;
    int n = s.length();

    for(int i = 0; i < n; i++)
    {

        // If present value is less than next value,
        // subtract present from next value and add the
        // resultant to the sum variable.
        if (i != n - 1 && roman.get(s.charAt(i)) <
                          roman.get(s.charAt(i + 1)))
        {
            sum += roman.get(s.charAt(i + 1)) -
                   roman.get(s.charAt(i));
            i++;
        }
        else
        {
            sum += roman.get(s.charAt(i));
        }
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{

      // Considering inputs given are valid
    String input = "MCMIV";

    System.out.print("Integer form of Roman Numeral is " +
                     romanToInt(input));
}
}

// This code is contributed by rahuldevgarg
```

**Output**

```
Integer form of Roman Numeral is 1904
```

***时间复杂度**–O(N)*
***辅助空间**–O(1)*

**另一种解决方案:**使用 python 的较短代码

## 蟒蛇 3

```
def romanToInt(s):
        translations = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }
        number = 0
        s = s.replace("IV", "IIII").replace("IX", "VIIII")
        s = s.replace("XL", "XXXX").replace("XC", "LXXXX")
        s = s.replace("CD", "CCCC").replace("CM", "DCCCC")
        for char in s:
            number += translations[char]
        print(number)

romanToInt('MCMIV')
```

**Output**

```
1904
```

**时间复杂度**–O(N)

**辅助空间**–O(1)

参考文献:[https://en.wikipedia.org/wiki/Roman_numerals](https://en.wikipedia.org/wiki/Roman_numerals)
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。