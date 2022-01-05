# 所有点对之间的曼哈顿距离之和

> 原文:[https://www . geesforgeks . org/sum-Manhattan-distants-pairs-points/](https://www.geeksforgeeks.org/sum-manhattan-distances-pairs-points/)

给定 **n** 个整数坐标。任务是找出所有坐标对之间的曼哈顿距离之和。
两个点之间的曼哈顿距离(x <sub>1</sub> ，y <sub>1</sub> )和(x <sub>2</sub> ，y <sub>2</sub> )为:
**| x<sub>1</sub>–x<sub>2</sub>|+| y<sub>1</sub>–y<sub>2</sub>|****示例:**

```
Input : n = 4
        point1 = { -1, 5 }
        point2 = { 1, 6 }
        point3 = { 3, 5 }
        point4 = { 2, 3 }
Output : 22
Distance of { 1, 6 }, { 3, 5 }, { 2, 3 } from 
{ -1, 5 } are 3, 4, 5 respectively.
Therefore, sum = 3 + 4 + 5 = 12

Distance of { 3, 5 }, { 2, 3 } from { 1, 6 } 
are 3, 4 respectively.
Therefore, sum = 12 + 3 + 4 = 19

Distance of { 2, 3 } from { 3, 5 } is 3.
Therefore, sum = 19 + 3 = 22.
```

**方法一:(蛮力)**

**时间复杂度:O(n2)**
这个想法是运行两个嵌套循环，即对于每个点，找到所有其他点的曼哈顿距离。

```
for (i = 1; i < n; i++)

  for (j = i + 1; j < n; j++)

    sum += ((xi - xj) + (yi - yj))
```

下面是该方法的实现:

## C++

```
// CPP Program to find sum of Manhattan distance
// between all the pairs of given points
#include <bits/stdc++.h>
using namespace std;

// Return the sum of distance between all
// the pair of points.
int distancesum(int x[], int y[], int n)
{
    int sum = 0;

    // for each point, finding distance to
    // rest of the point
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            sum += (abs(x[i] - x[j]) +
                    abs(y[i] - y[j]));
    return sum;
}

// Driven Program
int main()
{
    int x[] = { -1, 1, 3, 2 };
    int y[] = { 5, 6, 5, 3 };
    int n = sizeof(x) / sizeof(x[0]);
    cout << distancesum(x, y, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of Manhattan distance
// between all the pairs of given points

import java.io.*;

class GFG {

    // Return the sum of distance between all
    // the pair of points.
    static int distancesum(int x[], int y[], int n)
    {
        int sum = 0;

        // for each point, finding distance to
        // rest of the point
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                sum += (Math.abs(x[i] - x[j]) +
                            Math.abs(y[i] - y[j]));
        return sum;
    }

    // Driven Program
    public static void main(String[] args)
    {
        int x[] = { -1, 1, 3, 2 };
        int y[] = { 5, 6, 5, 3 };
        int n = x.length;

        System.out.println(distancesum(x, y, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find sum of
# Manhattan distance between all
# the pairs of given points

# Return the sum of distance
# between all the pair of points.
def distancesum (x, y, n):
    sum = 0

    # for each point, finding distance
    # to rest of the point
    for i in range(n):
        for j in range(i+1,n):
            sum += (abs(x[i] - x[j]) +
                        abs(y[i] - y[j]))

    return sum

# Driven Code
x = [ -1, 1, 3, 2 ]
y = [ 5, 6, 5, 3 ]
n = len(x)
print(distancesum(x, y, n) )

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Program to find sum of Manhattan distance
// between all the pairs of given points
using System;

class GFG {

    // Return the sum of distance between all
    // the pair of points.
    static int distancesum(int []x, int []y, int n)
    {
        int sum = 0;

        // for each point, finding distance to
        // rest of the point
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                sum += (Math.Abs(x[i] - x[j]) +
                            Math.Abs(y[i] - y[j]));
        return sum;
    }

    // Driven Program
    public static void Main()
    {
        int []x = { -1, 1, 3, 2 };
        int []y = { 5, 6, 5, 3 };
        int n = x.Length;

        Console.WriteLine(distancesum(x, y, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum
// of Manhattan distance
// between all the pairs
// of given points

// Return the sum of distance
// between all the pair of points.
function distancesum( $x, $y, $n)
{
    $sum = 0;

    // for each point, finding
    // distance to rest of
    // the point
    for($i = 0; $i < $n; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            $sum += (abs($x[$i] - $x[$j]) +
                     abs($y[$i] - $y[$j]));
    return $sum;
}

    // Driver Code
    $x = array(-1, 1, 3, 2);
    $y = array(5, 6, 5, 3);
    $n = count($x);
    echo distancesum($x, $y, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find sum of Manhattan distance
// between all the pairs of given points

    // Return the sum of distance between all
    // the pair of points.
    function distancesum(x, y, n)
    {
        let sum = 0;

        // for each point, finding distance to
        // rest of the point
        for (let i = 0; i < n; i++)
            for (let j = i + 1; j < n; j++)
                sum += (Math.abs(x[i] - x[j]) +
                            Math.abs(y[i] - y[j]));
        return sum;
    }

// Driver code
        let x = [ -1, 1, 3, 2 ];
        let y = [ 5, 6, 5, 3 ];
        let n = x.length;

        document.write(distancesum(x, y, n));

         // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
22
```

**方法 2:(有效方法)**

1.  这个想法是使用贪婪方法。首先观察，曼哈顿公式可以分解成两个独立的和，一个是 **x** 坐标之间的差，第二个是 **y** 坐标之间的差。如果我们知道如何计算其中一个，我们可以用同样的方法计算另一个。所以现在我们继续计算 **x** 坐标距离之和。
2.  假设我们已经计算了任意两点之间的距离之和，直到某一点**x<sub>I-1</sub>****x**小于**x<sub>I-1</sub>T9】的所有值，让这个和为 **res** ，现在我们必须计算任意两点之间的距离，包括**x<sub>I</sub>T15】，其中 **x <sub>i 【T18 为了计算每个点与下一个更大的点 **x <sub>i</sub>** 的距离，我们可以将现有的差之和 **res** 与所有小于 **x <sub>i</sub>** 的点 **x <sub>k</sub>** 的距离相加。 因此，任何两点之间的总和现在将等于**RES**+**∑**(**x<sub>I</sub>**T46】–</sub>**T48】x<sub>k</sub>T51】，其中**x<sub>I</sub>T55】是测量差异的当前点，而**x<sub>k</sub>T59】是所有的********
3.  因为每次计算**x<sub>I</sub>T3】保持不变，我们可以将求和简化为:**

> **RES = RES+(x<sub>I</sub>–x<sub>1</sub>+【x<sub>I</sub>–x<sub>2</sub>)+【x<sub>I</sub>–x**
> 
> **RES = RES+(x<sub>I</sub>)* I –( x<sub>1</sub>+x<sub>2</sub>+……x<sub>I-1</sub>)**，因为在排序数组中，有 I 个元素小于当前索引 I。
> 
> **RES = RES+(x<sub>I</sub>)* I–S<sub>I-1</sub>**，其中 **S <sub>i-1</sub>** 是所有先前点的总和，直到索引**I–1**

4.对于新的指数 I，我们需要加上当前指数**x<sub>I</sub>T3】与之前所有指数**x<sub>k</sub>****<x<sub>I</sub>**的差值**

5.如果我们按非递减顺序对所有点进行排序，我们可以很容易地计算出 O(N)时间内每对坐标之间沿一个轴的期望距离之和，从左到右处理点，并使用上述方法。
同样，我们不必担心两个点是否是相等的坐标，在按非递减顺序对点进行排序后，我们说一个点 **x <sub>i-1</sub>** 小于 **x <sub>i</sub>** 如果且仅当它在排序后的数组中出现得更早。
以下是本办法的实施情况:

## C++

```
// CPP Program to find sum of Manhattan
// distances between all the pairs of
// given points
#include <bits/stdc++.h>
using namespace std;

// Return the sum of distance of one axis.
int distancesum(int arr[], int n)
{
    // sorting the array.
    sort(arr, arr + n);

    // for each point, finding the distance.
    int res = 0, sum = 0;
    for (int i = 0; i < n; i++) {
        res += (arr[i] * i - sum);
        sum += arr[i];
    }

    return res;
}

int totaldistancesum(int x[], int y[], int n)
{
    return distancesum(x, n) + distancesum(y, n);
}

// Driven Program
int main()
{
    int x[] = { -1, 1, 3, 2 };
    int y[] = { 5, 6, 5, 3 };
    int n = sizeof(x) / sizeof(x[0]);
    cout << totaldistancesum(x, y, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of Manhattan
// distances between all the pairs of
// given points

import java.io.*;
import java.util.*;

class GFG {

    // Return the sum of distance of one axis.
    static int distancesum(int arr[], int n)
    {

        // sorting the array.
        Arrays.sort(arr);

        // for each point, finding the distance.
        int res = 0, sum = 0;
        for (int i = 0; i < n; i++) {
            res += (arr[i] * i - sum);
            sum += arr[i];
        }

        return res;
    }

    static int totaldistancesum(int x[],
                            int y[], int n)
    {
        return distancesum(x, n) +
                        distancesum(y, n);
    }

    // Driven Program
    public static void main(String[] args)
    {

        int x[] = { -1, 1, 3, 2 };
        int y[] = { 5, 6, 5, 3 };
        int n = x.length;
        System.out.println(totaldistancesum(x,
                                        y, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find sum of Manhattan
# distances between all the pairs of
# given points

# Return the sum of distance of one axis.
def distancesum (arr, n):

    # sorting the array.
    arr.sort()

    # for each point, finding
    # the distance.
    res = 0
    sum = 0
    for i in range(n):
        res += (arr[i] * i - sum)
        sum += arr[i]

    return res

def totaldistancesum( x , y , n ):
    return distancesum(x, n) + distancesum(y, n)

# Driven Code
x = [ -1, 1, 3, 2 ]
y = [ 5, 6, 5, 3 ]
n = len(x)
print(totaldistancesum(x, y, n) )

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Program to find sum of Manhattan
// distances between all the pairs of
// given points

using System;

class GFG {

    // Return the sum of distance of one axis.
    static int distancesum(int []arr, int n)
    {

        // sorting the array.
        Array.Sort(arr);

        // for each point, finding the distance.
        int res = 0, sum = 0;
        for (int i = 0; i < n; i++) {
            res += (arr[i] * i - sum);
            sum += arr[i];
        }

        return res;
    }

    static int totaldistancesum(int []x,
                            int []y, int n)
    {
        return distancesum(x, n) +
                        distancesum(y, n);
    }

    // Driven Program
    public static void Main()
    {

        int []x = { -1, 1, 3, 2 };
        int []y = { 5, 6, 5, 3 };
        int n = x.Length;
        Console.WriteLine(totaldistancesum(x,
                                        y, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// Manhattan distances between
// all the pairs of given points

// Return the sum of
// distance of one axis.
function distancesum($arr, $n)
{
    // sorting the array.
    sort($arr);

    // for each point,
    // finding the distance.
    $res = 0; $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $res += ($arr[$i] * $i - $sum);
        $sum += $arr[$i];
    }

    return $res;
}

function totaldistancesum($x, $y, $n)
{
    return distancesum($x, $n) +
           distancesum($y, $n);
}

// Driver Code
$x = array(-1, 1, 3, 2);
$y = array(5, 6, 5, 3);
$n = sizeof($x);
echo totaldistancesum($x, $y, $n), "\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find sum of Manhattan
// distances between all the pairs of
// given points

    // Return the sum of distance of one axis.
    function distancesum(arr, n)
    {

        // sorting the array.
        arr.sort();

        // for each point, finding the distance.
        let res = 0, sum = 0;
        for (let i = 0; i < n; i++) {
            res += (arr[i] * i - sum);
            sum += arr[i];
        }

        return res;
    }

    function totaldistancesum(x,
                            y, n)
    {
        return distancesum(x, n) +
                        distancesum(y, n);
    }

// Driver code

        let x = [ -1, 1, 3, 2 ];
        let y = [ 5, 6, 5, 3 ];
        let n = x.length;
        document.write(totaldistancesum(x,
                                        y, n));

</script>
```

**输出:**

```
22
```

**时间复杂度:** O(nlogn)