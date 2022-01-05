# 找到最终的颜色组合

> 原文:[https://www . geeksforgeeks . org/find-结果-颜色组合/](https://www.geeksforgeeks.org/find-the-resulting-colour-combination/)

给定三种颜色(G、B、Y)的字符串作为输入，任务是打印根据下面给出的规则形成的合成颜色:

```
// Rules for colour combination

Blue(B) * Green(G) = Yellow(Y)
Yellow(Y) * Blue(B) = Green(G)
Green(G) * Yellow(Y) = Blue(B)
```

**示例:**

```
Input: str = "GBYGB"
Output B

Input: str = "BYB"
Output Y
```

**进场:**这个问题可以通过以下方式解决:

1.  获取输入字符串。
2.  将每个字母与其相邻的字符进行比较。
3.  使用上述条件确定组合。
4.  打印输出组合。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// resultant colour combination

#include <iostream>
using namespace std;

// Function to return Colour Combination
char Colour_Combination(string s)
{
    char temp = s[0];

    for (int i = 1; i < s.length(); i++) {
        if (temp != s[i]) {

            // Check for B * G = Y
            if ((temp == 'B' || temp == 'G')
                && (s[i] == 'G' || s[i] == 'B'))
                temp = 'Y';

            // Check for B * Y = G
            else if ((temp == 'B' || temp == 'Y')
                     && (s[i] == 'Y' || s[i] == 'B'))
                temp = 'G';

            // Check for Y * G = B
            else
                temp = 'B';
        }
    }
    return temp;
}

// Driver Code
int main(int argc, char** argv)
{
    string s = "GBYGB";

    cout << Colour_Combination(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// resultant colour combination
class GfG
{

    // Function to return Colour Combination
    static char Colour_Combination(String s)
    {
        char temp = s.charAt(0);

        for (int i = 1; i < s.length(); i++)
        {
            if (temp != s.charAt(i))
            {

                // Check for B * G = Y
                if ((temp == 'B' || temp == 'G')
                            && (s.charAt(i) == 'G'
                            || s.charAt(i) == 'B'))
                    temp = 'Y';

                // Check for B * Y = G
                else if ((temp == 'B' || temp == 'Y')
                                && (s.charAt(i) == 'Y'
                                || s.charAt(i) == 'B'))
                    temp = 'G';

                // Check for Y * G = B
                else
                    temp = 'B';
            }
        }
        return temp;
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "GBYGB";
        System.out.println(Colour_Combination(s));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 program to find the
# resultant colour combination

# Function to return Colour Combination
def Colour_Combination(s):
    temp = s[0]

    for i in range(1, len(s), 1):
        if (temp != s[i]):

            # Check for B * G = Y
            if ((temp == 'B' or temp == 'G') and
                (s[i] == 'G' or s[i] == 'B')):
                temp = 'Y'

            # Check for B * Y = G
            elif ((temp == 'B' or temp == 'Y') and
                  (s[i] == 'Y' or s[i] == 'B')):
                temp = 'G'

            # Check for Y * G = B
            else:
                temp = 'B'
    return temp

# Driver Code
if __name__ == '__main__':
    s = "GBYGB"

    print(Colour_Combination(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the
// resultant colour combination

using System;

class GFG
{

    // Function to return Colour Combination
    static char Colour_Combination(string s)
    {
        char temp = s[0];

        for (int i = 1; i < s.Length; i++)
        {
            if (temp != s[i])
            {

                // Check for B * G = Y
                if ((temp == 'B' || temp == 'G')
                    && (s[i] == 'G' || s[i] == 'B'))
                    temp = 'Y';

                // Check for B * Y = G
                else if ((temp == 'B' || temp == 'Y')
                        && (s[i] == 'Y' || s[i] == 'B'))
                    temp = 'G';

                // Check for Y * G = B
                else
                    temp = 'B';
            }
        }
        return temp;
    }

    // Driver Code
    static void Main()
    {
        string s = "GBYGB";

        Console.WriteLine(Colour_Combination(s));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// resultant colour combination

// Function to return Colour Combination
function Colour_Combination($s)
{
    $temp = $s[0];

    for ($i = 1; $i < strlen($s); $i++)
    {
        if ($temp != $s[$i])
        {

            // Check for B * G = Y
            if (($temp == 'B' || $temp == 'G') &&
                ($s[$i] == 'G' || $s[$i] == 'B'))
                $temp = 'Y';

            // Check for B * Y = G
            else if (($temp == 'B' || $temp == 'Y') &&
                     ($s[$i] == 'Y' || $s[$i] == 'B'))
                $temp = 'G';

            // Check for Y * G = B
            else
                $temp = 'B';
        }
    }
    return $temp;
}

// Driver Code
$s = "GBYGB";

echo Colour_Combination($s);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// resultant colour combination

// Function to return Colour Combination
function Colour_Combination(s)
{
    let temp = s[0];

    for(let i = 1; i < s.length; i++)
    {
        if (temp != s[i])
        {

            // Check for B * G = Y
            if ((temp == 'B' || temp == 'G') &&
                (s[i] == 'G' || s[i] == 'B'))
                temp = 'Y';

            // Check for B * Y = G
            else if ((temp == 'B' || temp == 'Y') &&
                     (s[i] == 'Y' || s[i] == 'B'))
                temp = 'G';

            // Check for Y * G = B
            else
                temp = 'B';
        }
    }
    return temp;
}

// Driver Code
let s = "GBYGB";

document.write(Colour_Combination(s));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
B
```