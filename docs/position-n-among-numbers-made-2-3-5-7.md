# n 在由 2、3、5 组成的数字中的位置& 7

> 原文:[https://www . geesforgeks . org/position-n-in-numbers-made-2-3-5-7/](https://www.geeksforgeeks.org/position-n-among-numbers-made-2-3-5-7/)

考虑一系列仅由数字 2、3、5、7(素数)组成的数字。数列中的前几个数字是 2、3、5、7、22、23、25、27、32、33、35、37、52、53、55、57..等等。给定一个仅由 2，3，5，7 位数字构成的数，我们需要找到这个数在这个数列中的位置。
示例:

```
Input : 22
Output : 5
22 is 5th number in series 2, 3, 5, 7, 22, ...

Input : 777
Output : 84
```

与以下文章相反:
[只求质数(2、3、5、7)组成的第 n 个数](https://www.geeksforgeeks.org/finding-n-th-number-made-prime-digits/)

```
                                                    ""
             /                           |                            |                            \
          1(2)                          2(3)                         3(5)                          4(7)
   /    |     |   \           /   |      |  \             /     |       |    \           /     |     |     \ 
5(22) 6(23) 7(25) 8(27)    9(32)10(33)11(35)12(37)    13(52) 14(53) 15(55) 16(57)    17(72) 18(73) 19(75) 20(77)
/||\  /||\ /||\ /||\        /||\  /||\   /||\  /||\     /||\   /||\   /||\   /||\      /||\   /||\   /||\   /||\
```

如果数字为 2，则位于位置*2+1
上；如果数字为 3，则位于位置*2+2
上；如果数字为 5，则位于位置*2+3
上；如果数字为 7，则位于位置*2+4
上；这里，位置是大于或等于 0 的整数。

## C++

```
#include <algorithm>
#include <iostream>
using namespace std;

int findpos(string n)
{
    int pos = 0;
    for (int i = 0; n[i] != '\0'; i++) {
        switch (n[i]) {

        // If number is 2 then it is
        // on the position pos*2+1
        case '2':
            pos = pos * 4 + 1;
            break;

        // If number is 3 then it is
        // on the position pos*2+2
        case '3':
            pos = pos * 4 + 2;
            break;

        // If number is 5 then it is
        // on the position pos*2+3
        case '5':
            pos = pos * 4 + 3;
            break;

        // If number is 7 then it is
        // on the position pos*2+4
        case '7':
            pos = pos * 4 + 4;
            break;
        }
    }
    return pos;
}

// Driver code
int main()
{
    string n = "777";
    cout << findpos(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program position of n among
// the numbers made of 2, 3, 5 & 7
class GFG
{
static int findpos(String n)
{
    int pos = 0;
    for (int i = 0; i < n.length(); i++)
    {
        switch (n.charAt(i))
        {

        // If number is 2 then it is
        // on the position pos*2+1
        case '2':
            pos = pos * 4 + 1;
            break;

        // If number is 3 then it is
        // on the position pos*2+2
        case '3':
            pos = pos * 4 + 2;
            break;

        // If number is 5 then it is
        // on the position pos*2+3
        case '5':
            pos = pos * 4 + 3;
            break;

        // If number is 7 then it is
        // on the position pos*2+4
        case '7':
            pos = pos * 4 + 4;
            break;
        }
    }
    return pos;
}

// Driver code
public static void main(String args[])
{
    String n = "777";
    System.out.println( findpos(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
def findpos(n):
    pos = 0
    for i in n:

        # If number is 2 then it is
        # on the position pos*2+1
        if i == '2':
            pos = pos * 4 + 1

        # If number is 3 then it is
        # on the position pos*2+2
        elif i == '3':
            pos = pos * 4 + 2

        # If number is 5 then it is
        # on the position pos*2+3
        elif i == '5':
            pos = pos * 4 + 3

        # If number is 7 then it is
        # on the position pos*2+4
        elif i == '7':
            pos = pos * 4 + 4

    return pos

# Driver code
n = "777"
print (findpos(n))

# This code is contributed by vishal.
```

## C#

```
// C# Program position of n among
// the numbers made of 2, 3, 5 & 7
using System;

class GFG
{

static int findpos(String n)
{
    int pos = 0;
    for (int i = 0; i < n.Length; i++)
    {
        switch (n[i])
        {

        // If number is 2 then it is
        // on the position pos*2+1
        case '2':
            pos = pos * 4 + 1;
            break;

        // If number is 3 then it is
        // on the position pos*2+2
        case '3':
            pos = pos * 4 + 2;
            break;

        // If number is 5 then it is
        // on the position pos*2+3
        case '5':
            pos = pos * 4 + 3;
            break;

        // If number is 7 then it is
        // on the position pos*2+4
        case '7':
            pos = pos * 4 + 4;
            break;
        }
    }
    return pos;
}

// Driver code
public static void Main(String[] args)
{
    String n = "777";
    Console.WriteLine( findpos(n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program position of n among
// the numbers made of 2, 3, 5 & 7

function findpos($n)
{
    $pos = 0;
    for ($i = 0; isset($n[$i]) != NULL; $i++)
    {
        switch ($n[$i])
        {

            // If number is 2 then it is
            // on the position pos*2+1
            case '2':
                $pos = $pos * 4 + 1;
                break;

            // If number is 3 then it is
            // on the position pos*2+2
            case '3':
                $pos = $pos * 4 + 2;
                break;

            // If number is 5 then it is
            // on the position pos*2+3
            case '5':
                $pos = $pos * 4 + 3;
                break;

            // If number is 7 then it is
            // on the position pos*2+4
            case '7':
                $pos = $pos * 4 + 4;
                break;
        }
    }
    return $pos;
}

// Driver Code
$n = "777";
echo findpos($n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript Program position of n among
// the numbers made of 2, 3, 5 & 7

function findpos(n)
{
    var pos = 0;
    for (i = 0; i < n.length; i++)
    {
        switch (n.charAt(i))
        {

        // If number is 2 then it is
        // on the position pos*2+1
        case '2':
            pos = pos * 4 + 1;
            break;

        // If number is 3 then it is
        // on the position pos*2+2
        case '3':
            pos = pos * 4 + 2;
            break;

        // If number is 5 then it is
        // on the position pos*2+3
        case '5':
            pos = pos * 4 + 3;
            break;

        // If number is 7 then it is
        // on the position pos*2+4
        case '7':
            pos = pos * 4 + 4;
            break;
        }
    }
    return pos;
}

// Driver code
var n = "777";
document.write( findpos(n));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
84
```