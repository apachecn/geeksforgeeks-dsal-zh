# 从棋盘

中的主教那里拯救

> 原文:[https://www.geeksforgeeks.org/save-bishop-chessboard/](https://www.geeksforgeeks.org/save-bishop-chessboard/)

给你一个 8*8 的棋盘。除了棋盘，棋盘上还有一个主教，他的位置是已知的。Bishop 的位置以两位整数的形式给出，其中两位数字都大于 0 且小于 9(如 67 表示第 6 行和第 7 列)。现在你的任务是找到一些方法，你可以把一枚棋子安全地放在棋盘上。
示例:

```
Input : Bishop's Position = 11
Output : Safe Positions = 56

Input : Bishop's Position = 44 
Output : Safe Positions = 50
```

**蛮力法:**基本方法之一是迭代棋盘上所有 64 个可能的位置，检查那个位置是否安全。这种方法需要更多的时间。
**更好的方法:**正如我们所知，毕肖普的移动是以对角线的方式进行的，因此从棋盘上的任何位置，毕肖普都可以在两条对角线的两个方向上移动。所以，所有不在给定主教对角线运动路线上的位置都是安全位置。
现在我们的任务是从 Bishop 的位置找到所有可能的四个方向上的最大长度。

![](img/8f15fd801924112cb20a842190a4ae7e.png)

->主教可以从任何位置向四个角移动，即(11，18，81，88)。因此，我们将试图找到主教能向这些角落移动的最大距离。
让主教的位置为 ij，然后:

1.  朝向 11 的距离=最小值(mod(1-i)，mod(1-j))。
2.  朝向 18 的距离=最小值(mod(1-i)，mod(8-j))。
3.  朝向 81 的距离=最小值(mod(8-i)，mod(1-j))。
4.  朝向 88 的距离=最小值(mod(8-i)，mod(8-j))。

除了这四个位置之外，一个已经放置了 Bishop 的位置也是不安全的，因此不安全位置的总数是上述结果的总和+ 1。安全位置总数为 64 -(和+1)。

## C++

```
// CPP program to find total safe position
// to place your Bishop
#include<bits/stdc++.h>
using namespace std;

// function to calc total safe position
int calcSafe(int pos)
{
    // i,j denotes row and column of position of bishop
    int j = pos % 10;
    int i = pos /10;

    // calc distance in four direction
    int dis_11 = min ( abs(1-i), abs (1-j));
    int dis_18 = min ( abs(1-i), abs (8-j));
    int dis_81 = min ( abs(8-i), abs (1-j));
    int dis_88 = min ( abs(8-i), abs (8-j));

    // calc total sum of distance  + 1 for unsafe positions
    int sum = dis_11 + dis_18 + dis_81 + dis_88 + 1;

    // return total safe positions
    return (64- sum);
}

// driver function
int main()
{
    int pos = 34;
    cout << "Safe Positions = " << calcSafe(pos);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total safe position
// to place your Bishop
class GFG
{

    // function to calc total safe position
    static int calcSafe(int pos)
    {

        // i,j denotes row and column of position of bishop
        int j = pos % 10;
        int i = pos /10;

        // calc distance in four direction
        int dis_11 = Math.min ( Math.abs(1-i), Math.abs (1-j));
        int dis_18 = Math.min ( Math.abs(1-i), Math.abs (8-j));
        int dis_81 = Math.min ( Math.abs(8-i), Math.abs (1-j));
        int dis_88 = Math.min ( Math.abs(8-i), Math.abs (8-j));

        // calc total sum of distance + 1 for unsafe positions
        int sum = dis_11 + dis_18 + dis_81 + dis_88 + 1;

        // return total safe positions
        return (64- sum);
    }

    // Driver function
    public static void main (String[] args)
    {
        int pos = 34;

        System.out.print("Safe Positions = "+calcSafe(pos));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python program to find total safe
# position to place your Bishop
import math

# function to calc total safe position
def calcSafe(pos):

    # i,j denotes row and column of
    # position of bishop
    j = pos % 10
    i = pos /10

    # calc distance in four direction
    dis_11 = min ( abs(1-i), abs (1-j))
    dis_18 = min ( abs(1-i), abs (8-j))
    dis_81 = min ( abs(8-i), abs (1-j))
    dis_88 = min ( abs(8-i), abs (8-j))

    # calc total sum of distance + 1
    # for unsafe positions
    sum = (dis_11 + dis_18 + dis_81
                        + dis_88 + 1)

    # return total safe positions
    return (64- sum)

# driver function
pos = 34
print("Safe Positions = " ,
            math.ceil(calcSafe(pos)))

# This code is contributed by Sam007
```

## C#

```
// Program to find the total safe
// positions to place your Bishop
using System;

class GFG {

    // function to calc total safe position
    static int calcSafe(int pos)
    {

        // i, j denotes row and column of
        // position of bishop
        int j = pos % 10;
        int i = pos / 10;

        // calc distance in four direction
        int dis_11 = Math.Min(Math.Abs(1 - i), Math.Abs(1 - j));
        int dis_18 = Math.Min(Math.Abs(1 - i), Math.Abs(8 - j));
        int dis_81 = Math.Min(Math.Abs(8 - i), Math.Abs(1 - j));
        int dis_88 = Math.Min(Math.Abs(8 - i), Math.Abs(8 - j));

        // calc total sum of distance + 1
        // for unsafe positions
        int sum = dis_11 + dis_18 + dis_81 + dis_88 + 1;

        // return total safe positions
        return (64 - sum);
    }

    // Driver function
    public static void Main()
    {
        int pos = 34;

        Console.WriteLine("Safe Positions = " + calcSafe(pos));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// total safe position
// to place your Bishop

// function to calculate
// total safe position
function calcSafe( $pos)
{

    // i,j denotes row and
    // column of position
    // of bishop
    $j = $pos % 10;
    $i = $pos /10;

    // calc distance in four direction
    $dis_11 = min(abs(1 - $i),
                  abs (1 - $j));
    $dis_18 = min(abs(1 - $i),
                  abs (8 - $j));
    $dis_81 = min(abs(8 - $i),
                  abs (1 - $j));
    $dis_88 = min(abs(8 - $i),
                  abs (8 - $j));

    // calc total sum of
    // distance + 1 for
    // unsafe positions
    $sum = $dis_11 + $dis_18 +
           $dis_81 + $dis_88 + 1;

    // return total safe positions
    return ceil(64- $sum);
}

    // Driver Code
    $pos = 34;
    echo "Safe Positions = " ,calcSafe($pos);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program to find total safe position
// to place your Bishop

// function to calc total safe position
function calcSafe( pos)
{
    // i,j denotes row and column of position of bishop
    let j = pos % 10;
    let i = Math.floor(pos /10);

    // calc distance in four direction
    let dis_11 = Math.min( Math.abs(1-i), Math.abs(1-j));
    let dis_18 = Math.min( Math.abs(1-i), Math.abs(8-j));
    let dis_81 = Math.min( Math.abs(8-i), Math.abs(1-j));
    let dis_88 = Math.min( Math.abs(8-i), Math.abs(8-j));

    // calc total sum of distance  + 1 for unsafe positions
    let sum = dis_11 + dis_18 + dis_81 + dis_88 + 1;

    // return total safe positions
    return (64- sum);
}

// driver code

    let pos = 34;
    document.write("Safe Positions = " + calcSafe(pos));

</script>
```

**输出:**

```
Safe Positions = 52
```