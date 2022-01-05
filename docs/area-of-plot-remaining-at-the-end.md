# 终点剩余地块面积

> 原文:[https://www . geesforgeks . org/绘图区域-剩余在末端/](https://www.geeksforgeeks.org/area-of-plot-remaining-at-the-end/)

给定两个整数 **N** 和 **M** 表示矩形地块的长度和宽度，另一个整数 **K** 表示人数。每个人将把情节分成两部分，这样它将是情节中最大的可能的正方形，并将第二部分留给其他人，它一直持续到情节结束或每个人都得到情节。现在，任务是确定最后留下的地块面积。
**举例:**

> **输入:** N = 5，M = 3，K = 2
> **输出:** 2
> 第一人称将 5×3 的地块分为 2 部分，即 3×3 和 2×3
> ，将得到尺寸为 3×3 的地块。另一个人再次将 2×3 的图分成
> 两部分，即 2×2 和 1×2，将得到尺寸为 2×2 的图。现在地块剩下的
> 部分是 1×2 的尺寸，面积为 2 个单位。
> **输入:** N = 4，M = 8，K = 4
> **输出:** 0

**进场:**

1.  如果长度大于宽度，则从长度中减去宽度。
2.  如果宽度大于长度，那么从宽度中减去长度。
3.  对所有人重复上述步骤，同时扩大图的面积大于 0。
4.  打印最后剩余地块的面积，即长度*宽度。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the area
// of the remaining plot
int remainingArea(int N, int M, int K)
{

    // Continue while plot has positive area
    // and there are persons left
    while (K-- && N && M) {

        // If length > breadth
        // then subtract breadth from length
        if (N > M)
            N = N - M;

        // Else subtract length from breadth
        else
            M = M - N;
    }

    if (N > 0 && M > 0)
        return N * M;
    else
        return 0;
}

// Driver code
int main()
{
    int N = 5, M = 3, K = 2;

    cout << remainingArea(N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the area
    // of the remaining plot
    static int remainingArea(int N, int M, int K)
    {

        // Continue while plot has positive area
        // and there are persons left
        while (K-- > 0 && N > 0 && M > 0) {

            // If length > breadth
            // then subtract breadth from length
            if (N > M)
                N = N - M;

            // Else subtract length from breadth
            else
                M = M - N;
        }

        if (N > 0 && M > 0)
            return N * M;
        else
            return 0;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 5, M = 3, K = 2;

        System.out.println(remainingArea(N, M, K));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the area
# of the remaining plot
def remainingArea(N, M, K):

    # Continue while plot has positive area
    # and there are persons left
    while (K > 0 and N > 0 and M > 0):

        # If length > breadth
        # then subtract breadth from length
        if (N > M):
            N = N - M;

        # Else subtract length from breadth
        else:
            M = M - N;
        K = K - 1;
    if (N > 0 and M > 0):
        return N * M;
    else:
        return 0;

# Driver code
N = 5;
M = 3;
K = 2;

print(remainingArea(N, M, K));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the area
    // of the remaining plot
    static int remainingArea(int N, int M, int K)
    {

        // Continue while plot has positive area
        // and there are persons left
        while (K-- > 0 && N > 0 && M > 0) {

            // If length > breadth
            // then subtract breadth from length
            if (N > M)
                N = N - M;

            // Else subtract length from breadth
            else
                M = M - N;
        }

        if (N > 0 && M > 0)
            return N * M;
        else
            return 0;
    }

    // Driver code
    static public void Main()
    {
        int N = 5, M = 3, K = 2;

        Console.WriteLine(remainingArea(N, M, K));
    }
}

/* This code contributed by ajit */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the area
// of the remaining plot
function remainingArea($N, $M, $K)
{

    // Continue while plot has positive area
    // and there are persons left
    while ($K-- && $N && $M)
    {

        // If length > breadth
        // then subtract breadth from length
        if ($N > $M)
            $N = $N - $M;

        // Else subtract length from breadth
        else
            $M = $M - $N;
    }

    if ($N > 0 && $M > 0)
        return $N * $M;
    else
        return 0;
}

// Driver code
$N = 5;
$M = 3;
$K = 2;

echo remainingArea($N, $M, $K);

// This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the area
// of the remaining plot
function remainingArea(N, M, K)
{

    // Continue while plot has positive area
    // and there are persons left
    while (K-- && N && M) {

        // If length > breadth
        // then subtract breadth from length
        if (N > M)
            N = N - M;

        // Else subtract length from breadth
        else
            M = M - N;
    }

    if (N > 0 && M > 0)
        return N * M;
    else
        return 0;
}

// Driver code
var N = 5, M = 3, K = 2;
document.write( remainingArea(N, M, K));

</script>
```

**Output:** 

```
2
```