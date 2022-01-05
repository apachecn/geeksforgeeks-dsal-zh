# 去掉多余的支架后平衡一根绳子

> 原文:[https://www . geesforgeks . org/balance-一个去掉额外括号后的字符串/](https://www.geeksforgeeks.org/balance-a-string-after-removing-extra-brackets/)

给定一个带左括号和右括号的字符串。任务是从字符串中移除额外的括号并平衡它。
**例:**

> **输入:**str = " gau(ra)ra)v(ku(mar(Raj put))"
> **输出:**gau rav(ku(mar(Raj put)))
> **输入:**str = " 1+5)+5+)6+(5+9)* 9 "
> **输出:** 1+5+5+6+(5+9)*9

**进场:**

*   开始从左向右移动。
*   检查当前索引处的元素是否是左括号“(”，然后打印该括号并增加计数。
*   检查当前索引处的元素是否是右括号“)”，如果计数不等于零，则打印它并减少计数。
*   检查字符串中当前索引处是否有括号以外的元素，然后打印出来。
*   最后，如果计数不等于零，则打印')'等于计数的数字，以平衡字符串。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Print balanced and remove
// extra brackets from string
void balancedString(string str)
{
    int count = 0, i;
    int n = str.length();

    // Maintain a count for opening brackets
    // Traversing string
    for (i = 0; i < n; i++) {

        // check if opening bracket
        if (str[i] == '(') {

            // print str[i] and increment count by 1
            cout << str[i];
            count++;
        }

        // check if closing bracket and count != 0
        else if (str[i] == ')' && count != 0) {
            cout << str[i];

            // decrement count by 1
            count--;
        }

        // if str[i] not a closing brackets
        // print it
        else if (str[i] != ')')
            cout << str[i];
    }

    // balanced brackets if opening brackets
    // are more then closing brackets
    if (count != 0)
        // print remaining closing brackets
        for (i = 0; i < count; i++)
           cout << ")";
}

// Driver code
int main()
{

    string str = "gau)ra)v(ku(mar(rajput))";
     balancedString(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG {

// Print balanced and remove
// extra brackets from string
public static void balancedString(String str)
{
    int count = 0, i;
    int n = str.length();

    // Maintain a count for opening brackets
    // Traversing string
    for (i = 0; i < n; i++) {

        // check if opening bracket
        if (str.charAt(i) == '(') {

            // print str.charAt(i) and increment count by 1
            System.out.print(str.charAt(i));
            count++;
        }

        // check if closing bracket and count != 0
        else if (str.charAt(i) == ')' && count != 0) {
            System.out.print(str.charAt(i));

            // decrement count by 1
            count--;
        }

        // if str.charAt(i) not a closing brackets
        // print it
        else if (str.charAt(i) != ')')
            System.out.print(str.charAt(i));
    }

    // balanced brackets if opening brackets
    // are more then closing brackets
    if (count != 0)
        // print remaining closing brackets
        for (i = 0; i < count; i++)
            System.out.print(")");
}

// Driver Method
public static void main(String args[])
{
    String str = "gau)ra)v(ku(mar(rajput))";
    balancedString(str);
}
}
```

## 蟒蛇 3

```
# Python implementation of above approach

# Print balanced and remove
# extra brackets from string
def balancedString(str):
    count, i = 0, 0
    n = len(str)

    # Maintain a count for opening
    # brackets Traversing string
    for i in range(n):

        # check if opening bracket
        if (str[i] == '('):

            # print str[i] and increment
            # count by 1
            print(str[i], end = "")
            count += 1

        # check if closing bracket and count != 0
        elif (str[i] == ')' and count != 0):
            print(str[i], end = "")

            # decrement count by 1
            count -= 1

        # if str[i] not a closing brackets
        # print it
        elif (str[i] != ')'):
            print(str[i], end = "")

    # balanced brackets if opening brackets
    # are more then closing brackets
    if (count != 0):

        # print remaining closing brackets
        for i in range(count):
            print(")", end = "")

# Driver code
if __name__ == '__main__':
    str = "gau)ra)v(ku(mar(rajput))"
    balancedString(str)

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Print balanced and remove
// extra brackets from string
public static void balancedString(String str)
{
    int count = 0, i;
    int n = str.Length;

    // Maintain a count for opening
    // brackets Traversing string
    for (i = 0; i < n; i++)
    {

        // check if opening bracket
        if (str[i] == '(')
        {

            // print str[i] and increment
            // count by 1
            Console.Write(str[i]);
            count++;
        }

        // check if closing bracket
        // and count != 0
        else if (str[i] == ')' && count != 0)
        {
            Console.Write(str[i]);

            // decrement count by 1
            count--;
        }

        // if str[i] not a closing
        // brackets print it
        else if (str[i] != ')')
            Console.Write(str[i]);
    }

    // balanced brackets if opening
    // brackets are more then closing
    // brackets
    if (count != 0)

        // print remaining closing brackets
        for (i = 0; i < count; i++)
            Console.Write(")");
}

// Driver Code
public static void Main()
{
    String str = "gau)ra)v(ku(mar(rajput))";
    balancedString(str);
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Print balanced and remove
// extra brackets from string
function balancedString($str)
{
    $count = 0;
    $n = strlen($str);

    // Maintain a count for opening
    // brackets Traversing string
    for ($i = 0; $i < $n; $i++)
    {

        // check if opening bracket
        if ($str[$i] == '(')
        {

            // print str[i] and increment
            // count by 1
            echo $str[$i];
            $count++;
        }

        // check if closing bracket and count != 0
        else if ($str[$i] == ')' && $count != 0)
        {
            echo $str[$i];

            // decrement count by 1
            $count--;
        }

        // if str[i] not a closing brackets
        // print it
        else if ($str[$i] != ')')
            echo $str[$i];
    }

    // balanced brackets if opening brackets
    // are more then closing brackets
    if ($count != 0)

        // print remaining closing brackets
        for ($i = 0; $i < $count; $i++)
        echo ")";
}

// Driver code
$str = "gau)ra)v(ku(mar(rajput))";
balancedString($str);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript implementation of above approach

// Print balanced and remove
// extra brackets from string
function balancedString( str)
{
    var count = 0, i;
    var n = str.length;

    // Maintain a count for opening
    // brackets Traversing string
    for (i = 0; i < n; i++)
    {

        // check if opening bracket
        if (str[i] == '(')
        {

            // print str[i] and increment
            // count by 1
            document.write(str[i]);
            count++;
        }

        // check if closing bracket
        // and count != 0
        else if (str[i] == ')' && count != 0)
        {
            document.write(str[i]);

            // decrement count by 1
            count--;
        }

        // if str[i] not a closing
        // brackets print it
        else if (str[i] != ')')
            document.write(str[i]);
    }

    // balanced brackets if opening
    // brackets are more then closing
    // brackets
    if (count != 0)

        // print remaining closing brackets
        for (i = 0; i < count; i++)
            document.write(")");
}

// Driver Code

    var str = "gau)ra)v(ku(mar(rajput))";
    balancedString(str);

// This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
gaurav(ku(mar(rajput)))
```