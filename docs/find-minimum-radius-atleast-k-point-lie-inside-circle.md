# 找到最小半径，使得至少 k 个点位于圆内

> 原文:[https://www . geesforgeks . org/find-最小半径-至少-k 点-位于圆内/](https://www.geeksforgeeks.org/find-minimum-radius-atleast-k-point-lie-inside-circle/)

给定正整数 K，圆心在(0，0)的圆和一些点的坐标。任务是找到圆的最小半径，使至少 k 个点位于圆内。输出最小半径的平方。

**示例:**

```
Input : (1, 1), (-1, -1), (1, -1), 
         k = 3
Output : 2
We need a circle of radius at least 2
to include 3 points.

Input : (1, 1), (0, 1), (1, -1), 
         k = 2
Output : 1
We need a circle of radius at least 1
to include 2 points. The circle around
(0, 0) of radius 1 would include (1, 1)
and (0, 1).
```

思路是求各点距离原点(0，0)的[欧氏距离](https://en.wikipedia.org/wiki/Euclidean_distance)的平方。现在，按照递增的顺序排列这些距离。现在距离的第 k <sup>个</sup>元素是所需的最小半径。
以下是本办法的实施情况:

## C++

```
// C++ program to find minimum radius
// such that atleast k point lie inside
// the circle
#include<bits/stdc++.h>
using namespace std;

// Return minimum distance required so that
// aleast k point lie inside the circle.
int minRadius(int k, int x[], int y[], int n)
{
   int dis[n];

   // Finding distance between of each
   // point from origin
   for (int i = 0; i < n; i++)
       dis[i] = x[i] * x[i] + y[i] * y[i];

    // Sorting the distance
    sort(dis, dis + n);

    return dis[k - 1];
}

// Driven Program
int main()
{
  int k = 3;
  int x[] = { 1, -1, 1 };
  int y[] = { 1, -1, -1 };
  int n = sizeof(x)/sizeof(x[0]);

  cout << minRadius(k, x, y, n) << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum radius
// such that atleast k point lie inside
// the circle
import java.util.Arrays;

class GFG
{

    // Return minimum distance required so that
    // aleast k point lie inside the circle.
    static int minRadius(int k, int[] x, int[] y,
                                          int n)
    {
        int[] dis=new int[n];

        // Finding distance between of each
        // point from origin
        for (int i = 0; i < n; i++)
            dis[i] = x[i] * x[i] + y[i] * y[i];

        // Sorting the distance
        Arrays.sort(dis);

        return dis[k - 1];
    }

    // Driven Program
    public static void main (String[] args) {

    int k = 3;
    int[] x = { 1, -1, 1 };
    int[] y = { 1, -1, -1 };
    int n = x.length;

    System.out.println(minRadius(k, x, y, n));

    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python3 program to find minimum radius
# such that atleast k point lie inside
# the circle

# Return minimum distance required so
# that aleast k point lie inside the
# circle.
def minRadius(k, x, y, n):
    dis = [0] * n

    # Finding distance between of each
    # point from origin

    for i in range(0, n):
        dis[i] = x[i] * x[i] + y[i] * y[i]

    # Sorting the distance
    dis.sort()

    return dis[k - 1]

# Driver Program
k = 3
x = [1, -1, 1]
y = [1, -1, -1]
n = len(x)

print(minRadius(k, x, y, n))

# This code is contributed by
# Prasad Kshirsagar
```

## C#

```
// C# program to find minimum radius
// such that atleast k point lie inside
// the circle
using System;

class GFG {

    // Return minimum distance required
    // so that aleast k point lie inside
    // the circle.
    static int minRadius(int k, int []x,
                          int[] y, int n)
    {
        int[] dis = new int[n];

        // Finding distance between of
        // each point from origin
        for (int i = 0; i < n; i++)
            dis[i] = x[i] * x[i] +
                       y[i] * y[i];

        // Sorting the distance
        Array.Sort(dis);

        return dis[k - 1];
    }

    // Driven Program
    public static void Main ()
    {
        int k = 3;
        int[] x = { 1, -1, 1 };
        int[] y = { 1, -1, -1 };
        int n = x.Length;

        Console.WriteLine(
              minRadius(k, x, y, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum radius
// such that atleast k point lie inside
// the circle

// Return minimum distance required
// so that aleast k point lie
// inside the circle.
function minRadius($k, $x, $y, $n)
{
    $dis =array();

    // Finding distance between
    // of each point from origin
    for ($i = 0; $i < $n; $i++)
        $dis[$i] = $x[$i] * $x[$i] +
                   $y[$i] * $y[$i];

        // Sorting the distance
        sort($dis);

        return $dis[$k - 1];
}

// Driver Code
$k = 3;
$x = array(1, -1, 1);
$y = array(1, -1, -1);
$n = count($x);

echo minRadius($k, $x, $y, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum radius
// such that atleast k point lie inside
// the circle

    // Return minimum distance required so that
    // aleast k point lie inside the circle.
    function minRadius(k, x, y, n) {

        let dis = Array.from({length: n}, (_, i) => 0);

        // Finding distance between of each
        // point from origin
        for (let i = 0; i < n; i++)
            dis[i] = x[i] * x[i] + y[i] * y[i];

        // Sorting the distance
        dis.sort();

        return dis[k - 1];
    }

// driver function

    let k = 3;
    let x = [ 1, -1, 1 ];
    let y = [ 1, -1, -1 ];
    let n = x.length;

    document.write(minRadius(k, x, y, n));

 // This code is contributed by code_hunt.
</script>   
```

**输出:**

```
2
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。