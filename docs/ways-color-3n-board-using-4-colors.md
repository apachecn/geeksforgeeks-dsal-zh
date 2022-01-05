# 用 4 种颜色给 3*N 板上色的方法

> 原文:[https://www . geesforgeks . org/way-color-3n-board-using-4-colors/](https://www.geeksforgeeks.org/ways-color-3n-board-using-4-colors/)

给定一个 3 X n 的板，找出最多使用 4 种颜色给它上色的方法，这样就不会有两个相邻的盒子有相同的颜色。对角线邻居不被视为相邻的盒子。
随着答案的快速增长，输出途径%1000000007。
约束:
1 < = n < 100000
**示例:**

```
Input : 1
Output : 36
We can use either a combination of 3 colors
or 2 colors. Now, choosing 3 colors out of 
4 is  and arranging them 

in 3! ways, similarly choosing 2 colors out 

of 4 is  and while arranging

we can only choose which of them could be at 

centre, that would be 2 ways. 

Answer = *3! + *2! = 36
Input : 2

Output : 588
```

我们将使用动态方法来解决这个问题，因为当一个新列添加到板上时，颜色填充的方式仅取决于当前列中的颜色模式。我们一列只能有两种颜色和三种颜色的组合。图像中给出了所有可能生成的新列。请考虑 A、B、C 和 D 四种颜色。

![Image Containing Color Combination Generation](img/d841e9dde01a4fb6750e57474d8977b8.png)

可以从当前列生成的所有可能的颜色组合。

从现在开始，我们将 3*N 板的第 N 列的 3 种颜色组合称为 W(n)，两种颜色称为 Y(n)。
我们可以看到每个 W 可以产生 5Y 和 11W，每个 Y 可以产生 7Y 和 10W。我们从这里得到两个方程
我们现在有两个方程，

```
W(n+1) = 10*Y(n)+11*W(n);
Y(n+1) = 7*Y(n)+5*W(n);
```

## C++

```
// C++ program to find number of ways
// to color a 3 x n grid using 4 colors
// such that no two adjacent have same
// color
#include <iostream>
using namespace std;

int solve(int A)
{

    // When we to fill single column
    long int color3 = 24;
    long int color2 = 12;
    long int temp = 0;

    for (int i = 2; i <= A; i++)
    {
        temp = color3;
        color3 = (11 * color3 + 10 *
              color2 ) % 1000000007;

        color2 = ( 5 * temp + 7 *
              color2 ) % 1000000007;
    }

    long num = (color3 + color2)
                       % 1000000007;

    return (int)num;
}

// Driver code
int main()
{
    int num1 = 1;
    cout << solve(num1) << endl;

    int num2 = 2;
    cout << solve(num2) << endl;

    int num3 = 500;
    cout << solve(num3) << endl;

    int num4 = 10000;
    cout << solve(num4);

    return 0;
}

// This code is contributed by vt_m.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways to color
// a 3 x n grid using 4 colors such that no two
// adjacent have same color.
public class Solution {
    public static int solve(int A) {
        long color3 = 24; // When we to fill single column
        long color2 = 12;
        long temp = 0;
        for (int i = 2; i <= A; i++)       
        {
            long temp = color3;
            color3 = (11 * color3 + 10 * color2 ) % 1000000007;
            color2 = ( 5 * temp + 7 * color2 ) % 1000000007;
        }
        long num = (color3 + color2) % 1000000007;
        return (int)num;
    }

    // Driver code
    public static void main(String[] args)
    {
        int num1 = 1;
        System.out.println(solve(num1));

        int num2 = 2;
        System.out.println(solve(num2));

        int num3 = 500;
        System.out.println(solve(num3));

        int num4 = 10000;
        System.out.println(solve(num4));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find number of ways
# to color a 3 x n grid using 4 colors
# such that no two adjacent have same
# color

def solve(A):

    # When we to fill single column
    color3 = 24
    color2 = 12
    temp = 0

    for i in range(2, A + 1, 1):
        temp = color3
        color3 = (11 * color3 + 10 * color2 ) % 1000000007

        color2 = ( 5 * temp + 7 * color2 ) % 1000000007

    num = (color3 + color2) % 1000000007

    return num

# Driver code
if __name__ == '__main__':
    num1 = 1
    print(solve(num1))

    num2 = 2
    print(solve(num2))

    num3 = 500
    print(solve(num3))

    num4 = 10000
    print(solve(num4))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find number of ways
// to color a 3 x n grid using 4
// colors such that no two adjacent
// have same color.
using System;

public class GFG {

    public static int solve(int A)
    {

        // When we to fill single column
        long color3 = 24;
        long color2 = 12;
        long temp = 0;

        for (int i = 2; i <= A; i++)
        {
            temp = color3;
            color3 = (11 * color3 + 10
                 * color2 ) % 1000000007;

            color2 = ( 5 * temp + 7
                 * color2 ) % 1000000007;
        }
        long num = (color3 + color2)
                            % 1000000007;
        return (int)num;
    }

    // Driver code
    public static void Main()
    {
        int num1 = 1;
        Console.WriteLine(solve(num1));

        int num2 = 2;
        Console.WriteLine(solve(num2));

        int num3 = 500;
        Console.WriteLine(solve(num3));

        int num4 = 10000;
        Console.WriteLine(solve(num4));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of ways
// to color a 3 x n grid using 4 colors
// such that no two adjacent have same
// color
function solve($A)
{

    // When we to fill single column
    $color3 = 24;
    $color2 = 12;
    $temp = 0;

    for ($i = 2; $i <= $A; $i++)
    {
        $temp = $color3;
        $color3 = (11 * $color3 +
                   10 * $color2 ) %
                   1000000007;

        $color2 = ( 5 * $temp +
                    7 * $color2 ) %
                    1000000007;
    }

    $num = ($color3 + $color2) %
                     1000000007;

    return (int)$num;
}

// Driver code
$num1 = 1;
echo solve($num1) ,"\n";

$num2 = 2;
echo solve($num2) ,"\n";

$num3 = 500;
echo solve($num3),"\n";

$num4 = 10000;
echo solve($num4);

// This code is contributed by m_kit.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find number of ways to color
// a 3 x n grid using 4 colors such that no two
// adjacent have same color.

    function solve(A) {
        let color3 = 24; // When we to fill single column
        let color2 = 12;
        let temp = 0;
        for (let i = 2; i <= A; i++)       
        {
            let temp = color3;
            color3 = (11 * color3 + 10 * color2 ) % 1000000007;
            color2 = ( 5 * temp + 7 * color2 ) % 1000000007;
        }
        let num = (color3 + color2) % 1000000007;
        return num;
    }

// Driver Code

        let num1 = 1;
        document.write(solve(num1) + "<br/>");

        let num2 = 2;
        document.write(solve(num2) + "<br/>");

        let num3 = 500;
        document.write(solve(num3) + "<br/>");

        let num4 = 10000;
        document.write(solve(num4));

</script>
```

**输出:**

```
36
588
178599516
540460643
```

本文由**潘舒尔·加尔格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。