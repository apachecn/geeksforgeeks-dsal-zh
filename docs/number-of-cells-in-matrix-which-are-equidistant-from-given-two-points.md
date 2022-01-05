# 矩阵中与给定两点等距的单元数

> 原文:[https://www . geeksforgeeks . org/距给定两点等距的矩阵单元数/](https://www.geeksforgeeks.org/number-of-cells-in-matrix-which-are-equidistant-from-given-two-points/)

给定一个 **N** 行 **M** 列的矩阵，给定矩阵上的**两点**；任务是计算与给定两点等距的像元数量。水平方向或垂直方向或两个方向的任何遍历都被认为是有效的，但对角线路径无效。
**举例:**

> **输入**:5 5
> 2 4
> 5 3
> T5】输出: 5
> **说明:**
> 在所有单元格中，这些是点(3，1)；(3, 2);(3, 3);(4, 4);(4，5)
> 满足给定条件。
> **输入:** 4 3
> 2 3
> 4 1
> **输出:** 4
> **解释:**
> 在所有单元格中，这些是点(1，1)；(2, 1);(3, 2);(4，3)
> 满足给定条件。

**接近** :

1.  矩阵的每个单元都被遍历。
2.  假设“A”是当前单元格和第一个点之间的距离，同样“B”是当前单元格和第二个点之间的距离。
3.  使用曼哈顿距离计算两点之间的距离。如果 A & B 相等，则计数递增。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
int numberOfPoints(int N, int M, int x1,
                   int y1, int x2, int y2)
{

    // Initializing count
    int count = 0;

    // Traversing through rows.
    for (int i = 1; i <= N; i++) {

        // Traversing through columns.
        for (int j = 1; j <= M; j++) {

            // By using Manhattan Distance, the distance between
            // the current point to given two points is calculated.

            // If distances are equal
            // the count is incremented by 1.
            if (abs(i - x1) + abs(j - y1)
                == abs(i - x2) + abs(j - y2))
                count++;
        }
    }

    return count;
}

// Driver Code
int main()
{
    int n = 5;
    int m = 5;
    int x1 = 2;
    int y1 = 4;
    int x2 = 5;
    int y2 = 3;

    cout << numberOfPoints(n, m, x1, y1, x2, y2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the above approach
import java.util.*;
import java.lang.Math;
public class GFG {
    public static int numberOfPoints(int N, int M, int x1,
                                     int y1, int x2, int y2)
    {
        int count = 0, i, j;

        // Traversing through rows.
        for (i = 1; i <= N; i++) {

            // Traversing through columns.
            for (j = 1; j <= M; j++) {

                // By using Manhattan Distance, distance between
                // current point to given two points is calculated

                // If distances are equal
                // the count is incremented by 1.
                if (Math.abs(i - x1) + Math.abs(j - y1)
                    == Math.abs(i - x2) + Math.abs(j - y2))
                    count += 1;
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        int m = 5;
        int x1 = 2;
        int y1 = 4;
        int x2 = 5;
        int y2 = 3;

        System.out.println(numberOfPoints(n, m, x1, y1, x2, y2));
    }
}
```

## 计算机编程语言

```
# Python implementation of the above approach
def numberPoints(N, M, x1, y1, x2, y2):

    # Initializing count = 0
    count = 0

    # Traversing through rows.
    for i in range(1, N + 1):

        # Traversing through columns.
        for j in range(1, M + 1):

            # By using Manhattan Distance,
            # distance between current point to
            # given two points is calculated

            # If distances are equal the
            # count is incremented by 1.
            if (abs(i - x1)+abs(j - y1)) == (abs(i - x2)+abs(j - y2)):
                count += 1

    return count

# Driver Code
N = 5
M = 5
x1 = 2
y1 = 4
x2 = 5
y2 = 3
print(numberPoints(N, M, x1, y1, x2, y2))
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int numberOfPoints(int N, int M, int x1,
                                    int y1, int x2, int y2)
    {
        int count = 0, i, j;

        // Traversing through rows.
        for (i = 1; i <= N; i++)
        {

            // Traversing through columns.
            for (j = 1; j <= M; j++)
            {

                // By using Manhattan Distance, distance between
                // current point to given two points is calculated

                // If distances are equal
                // the count is incremented by 1.
                if (Math.Abs(i - x1) + Math.Abs(j - y1)
                    == Math.Abs(i - x2) + Math.Abs(j - y2))

                    count += 1;
            }
        }
        return count;
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        int m = 5;
        int x1 = 2;
        int y1 = 4;
        int x2 = 5;
        int y2 = 3;

        Console.WriteLine(numberOfPoints(n, m, x1, y1, x2, y2));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    function numberOfPoints(N , M , x1 , y1 , x2 , y2)
    {
        var count = 0, i, j;

        // Traversing through rows.
        for (i = 1; i <= N; i++) {

            // Traversing through columns.
            for (j = 1; j <= M; j++) {

                // By using Manhattan Distance, distance between
                // current point to given two points is calculated

                // If distances are equal
                // the count is incremented by 1.
                if (Math.abs(i - x1) + Math.abs(j - y1) == Math.abs(i - x2) + Math.abs(j - y2))
                    count += 1;
            }
        }
        return count;
    }

    // Driver Code
        var n = 5;
        var m = 5;
        var x1 = 2;
        var y1 = 4;
        var x2 = 5;
        var y2 = 3;

        document.write(numberOfPoints(n, m, x1, y1, x2, y2));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
5
```