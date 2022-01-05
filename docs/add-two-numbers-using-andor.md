# 使用++和/或—

添加两个数字

> 原文:[https://www.geeksforgeeks.org/add-two-numbers-using-andor/](https://www.geeksforgeeks.org/add-two-numbers-using-andor/)

给定两个数字，不使用运算符+和/或-，使用++和/或–,返回它们的总和。
示例:

```
Input: x = 10, y = 5
Output: 15

Input: x = 10, y = -5
Output: 10
```

**我们强烈建议你最小化浏览器，先自己试试这个**
想法是做 y 乘以 x++，如果 y 为正，做 y 乘以 x–如果 y 为负。

## C++

```
// C++ program to add two numbers using ++
#include <bits/stdc++.h>
using namespace std;

// Returns value of x+y without using +
int add(int x, int y)
{
    // If y is positive, y times add 1 to x
    while (y > 0 && y--)
        x++;

    // If y is negative, y times subtract 1 from x
    while (y < 0 && y++)
        x--;

    return x;
}

int main()
{
    cout << add(43, 23) << endl;
    cout << add(43, -23) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to add two numbers
// using ++

public class GFG {

    // Returns value of x+y without
    // using +
    static int add(int x, int y)
    {

        // If y is positive, y times
        // add 1 to x
        while (y > 0 && y != 0) {
            x++;
            y--;
        }

        // If y is negative, y times
        // subtract 1 from x
        while (y < 0 && y != 0) {
            x--;
            y++;
        }

        return x;
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.println(add(43, 23));

        System.out.println(add(43, -23));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to add two
# numbers using ++

# Returns value of x + y
# without using + def add(x, y):

    # If y is positive, y
    # times add 1 to x
    while (y > 0 and y):
        x = x + 1
        y = y - 1

    # If y is negative, y
    # times subtract 1
    # from x
    while (y < 0 and y) :
        x = x - 1
        y = y + 1

    return x

# Driver code
print(add(43, 23))
print(add(43, -23))

# This code is contributed
# by Sam007.
```

## C#

```
// C# program to add two numbers
// using ++
using System;

public class GFG {

    // Returns value of x+y without
    // using +
    static int add(int x, int y)
    {

        // If y is positive, y times
        // add 1 to x
        while (y > 0 && y != 0) {
            x++;
            y--;
        }

        // If y is negative, y times
        // subtract 1 from x
        while (y < 0 && y != 0) {
            x--;
            y++;
        }

        return x;
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(add(43, 23));
        Console.WriteLine(add(43, -23));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to add two
// numbers using ++

// Returns value of
// x+y without using +
function add($x, $y)
{

    // If y is positive,
    // y times add 1 to x
    while ($y > 0 && $y--)
       $x++;

    // If y is negative,
    // y times subtract
    // 1 from x
    while ($y < 0 && $y++)
       $x--;

    return $x;
}

    // Driver Code
    echo add(43, 23), "\n";
    echo add(43, -23), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to
    // add two numbers using ++

    // Returns value of x+y without
    // using +
    function add(x, y)
    {

        // If y is positive, y times
        // add 1 to x
        while (y > 0 && y != 0) {
            x++;
            y--;
        }

        // If y is negative, y times
        // subtract 1 from x
        while (y < 0 && y != 0) {
            x--;
            y++;
        }

        return x;
    }

    document.write(add(43, 23) + "</br>");
      document.write(add(43, -23) + "</br>");

</script>
```

**输出:**

```
66
20
```

感谢 Gaurav Ahirwar 提出上述解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息