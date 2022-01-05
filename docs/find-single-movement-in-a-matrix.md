# 在矩阵中找到单个运动

> 原文:[https://www . geesforgeks . org/find-矩阵中单次移动/](https://www.geeksforgeeks.org/find-single-movement-in-a-matrix/)

给定四个整数 *x1，y1 和 x2，y2* ，它们代表无限 2D 矩阵中的两个位置，任务是找出是否有可能在一次移动中从(x1，y1)移动到(x2，y2)，或者是*向左，向右，向上或向下*。请注意，移动将重复进行，直到到达目的地。如果无法达到(x2，y2)输出 *-1* 。
**举例:**

> **输入:** x1 = 0，y1 = 0，x2 = 1，y2 = 0
> **输出:**下降
> 目的地刚好在起点下方。
> **输入:** x1 = 0，y1 = 0，x2 = 1，y2 = 1
> **输出:** -1
> 单次移动不可能从(0，0)到达(1，1)。

**进近:**检查坐标是在同一行还是同一列，然后只有可能到达最终目的地。然后根据目的地的方向打印移动。
以下是上述办法的实施情况:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function that checks whether it is
// possible to move from
// (x1, y1) to (x2, y2)
void Robot_Grid(int x1, int y1, int x2, int y2)
{
    // Both locations are
    // in the same row
    if (x1 == x2) {

        // Destination is
        // at the right
        if (y1 < y2) {
            cout << "Right";
        }
        // Destination is
        // at the left
        else {
            cout << "Left";
        }
    }

    // Both locations are
    // in the same column
    else if (y1 == y2) {

        // Destination is below
        // the current row
        if (x1 < x2) {
            cout << "Down";
        }

        // Destination is above
        // the current row
        else {
            cout << "Up";
        }
    }

    // Impossible to get
    // to the destination
    else {
        cout << "-1";
    }
}

// Driver code
int main()
{
    int x1, x2, y1, y2;
    x1 = 0;
    y1 = 0;
    x2 = 0;
    y2 = 1;

    Robot_Grid(x1, y1, x2, y2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the given above approach

public class GFG{

    // Function that checks whether it is
    // possible to move from
    // (x1, y1) to (x2, y2)
    static void Robot_Grid(int x1, int y1, int x2, int y2)
    {
        // Both locations are
        // in the same row
        if (x1 == x2) {

            // Destination is
            // at the right
            if (y1 < y2) {
                System.out.print("Right");
            }
            // Destination is
            // at the left
            else {
                System.out.print("Left");
            }
        }

        // Both locations are
        // in the same column
        else if (y1 == y2) {

            // Destination is below
            // the current row
            if (x1 < x2) {
                System.out.print("Down");
            }

            // Destination is above
            // the current row
            else {
                System.out.println("Up");
            }
        }

        // Impossible to get
        // to the destination
        else {
            System.out.print("-1");
        }
    }

    // Driver code
     public static void main(String []args)
    {
        int x1, x2, y1, y2;
        x1 = 0;
        y1 = 0;
        x2 = 0;
        y2 = 1;

        Robot_Grid(x1, y1, x2, y2);
}

// This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Function that checks whether it is
# possible to move from
# (x1, y1) to (x2, y2)

def Robot_Grid(x1, y1, x2, y2):

    # Both locations are in the same row
    if (x1 == x2):

        # Destination is at the right
        if (y1 < y2):
            print("Right")

        # Destination is at the left
        else:
            print("Left")

    # Both locations are in the same column
    elif (y1 == y2):

        # Destination is below the current row
        if (x1 < x2):
            print("Down")

        # Destination is above the current row
        else:
            print("Up")

    # Impossible to get to the destination
    else:
        print("-1")

# Driver code
if __name__ == '__main__':
    x1 = 0
    y1 = 0
    x2 = 0
    y2 = 1

    Robot_Grid(x1, y1, x2, y2)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the given above approach
using System;

class GFG{

    // Function that checks whether it is
    // possible to move from
    // (x1, y1) to (x2, y2)
    static void Robot_Grid(int x1, int y1,
                           int x2, int y2)
    {
        // Both locations are
        // in the same row
        if (x1 == x2)
        {

            // Destination is
            // at the right
            if (y1 < y2)
            {
                Console.Write("Right");
            }
            // Destination is
            // at the left
            else
            {
                Console.Write("Left");
            }
        }

        // Both locations are
        // in the same column
        else if (y1 == y2)
        {

            // Destination is below
            // the current row
            if (x1 < x2)
            {
                Console.Write("Down");
            }

            // Destination is above
            // the current row
            else
            {
                Console.WriteLine("Up");
            }
        }

        // Impossible to get
        // to the destination
        else
        {
            Console.WriteLine("-1");
        }
    }

    // Driver code
    public static void Main()
    {
        int x1, x2, y1, y2;
        x1 = 0;
        y1 = 0;
        x2 = 0;
        y2 = 1;

        Robot_Grid(x1, y1, x2, y2);
    }
}

// This code is contributed by
// Mukul Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function that checks whether it is
// possible to move from
// (x1, y1) to (x2, y2)
function Robot_Grid($x1, $y1, $x2, $y2)
{
    // Both locations are in the same row
    if ($x1 == $x2)
    {

        // Destination is at the right
        if ($y1 < $y2)
        {
            echo "Right";
        }

        // Destination is at the left
        else
        {
            echo "Left";
        }
    }

    // Both locations are in the same column
    else if ($y1 == $y2)
    {

        // Destination is below the
        // current row
        if ($x1 < $x2)
        {
            echo "Down";
        }

        // Destination is above the current row
        else
        {
            echo "Up";
        }
    }

    // Impossible to get to the destination
    else
    {
        echo "-1";
    }
}

// Driver code
$x1 = 0;
$y1 = 0;
$x2 = 0;
$y2 = 1;

Robot_Grid($x1, $y1, $x2, $y2);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the given above approach

    // Function that checks whether it is
    // possible to move from
    // (x1, y1) to (x2, y2)
    function Robot_Grid(x1,y1,x2,y2)
    {
        // Both locations are
        // in the same row
        if (x1 == x2) {

            // Destination is
            // at the right
            if (y1 < y2) {
                document.write("Right");
            }
            // Destination is
            // at the left
            else {
                document.write("Left");
            }
        }

        // Both locations are
        // in the same column
        else if (y1 == y2) {

            // Destination is below
            // the current row
            if (x1 < x2) {
                document.write("Down");
            }

            // Destination is above
            // the current row
            else {
                document.write("Up");
            }
        }

        // Impossible to get
        // to the destination
        else {
            document.write("-1");
        }
    }

    // Driver code
    let x1, x2, y1, y2;
        x1 = 0;
        y1 = 0;
        x2 = 0;
        y2 = 1;

        Robot_Grid(x1, y1, x2, y2);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Right
```