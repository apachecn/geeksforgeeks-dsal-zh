# 检查两个凸正多边形是否有相同的中心

> 原文:[https://www . geeksforgeeks . org/check-two-凸-正多边形-是否有同中心/](https://www.geeksforgeeks.org/check-whether-two-convex-regular-polygon-have-same-center-or-not/)

给定两个正整数 N 和 M，表示凸正多边形的边，其中 N < M, the task is to check whether polygons have the same center or not if N-sided polygon was inscribed in an M-sided polygon.
**多边形的中心:**点在多边形内，与多边形的每个顶点等距。
**示例:**

> **输入:** N = 9，M = 3
> **输出:** YES
> **说明:**
> 边 3 的多边形当内接在边 9 的多边形中时，则两个多边形具有相同的中心。
> **输入:** N = 10，M = 3
> **输出:**否
> **说明:**
> 边 3 的多边形当内接在边 10 的多边形中时，则两个多边形没有相同的中心。

**逼近:**这个问题的关键观察是当 **M % N == 0** 时，意味着 N 边多边形的边相等地覆盖了 M 边多边形的边，也就是说两个多边形有相同的中心。
**算法:**

*   检查 M 是否能被 N 整除，如果能，则两个多边形的中心相同。
*   否则两个多边形有不同的中心。

以下是上述方法的实现:

## C++

```
// C++ implementation to check whether
// two convex polygons have same center

#include<bits/stdc++.h>
using namespace std;

// Function to check whether two convex
// polygons have the same center or not
int check(int n, int m){
    if (m % n == 0){
        cout << "YES";
    }
    else{
        cout << "NO";
    }
    return 0;
}

// Driver Code
int main()
{
    int n = 5;
    int m = 10;

    check(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// two convex polygons have same center
class GFG{

// Function to check whether two convex
// polygons have the same center or not
static int check(int n, int m){
    if (m % n == 0){
        System.out.print("YES");
    }
    else{
        System.out.print("NO");
    }
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    int m = 10;

    check(n, m);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to check whether
# two convex polygons have same center

# Function to check whether two convex
# polygons have the same center or not
def check(n, m):
    if (m % n == 0):
        print("YES")
    else:
        print("NO")

# Driver Code
n = 5
m = 10

check(n, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to check whether
// two convex polygons have same center
using System;

class GFG{

// Function to check whether two convex
// polygons have the same center or not
static int check(int n, int m){
    if (m % n == 0){
        Console.Write("YES");
    }
    else{
        Console.Write("NO");
    }
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    int m = 10;

    check(n, m);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to check whether
// two convex polygons have same center

// Function to check whether two convex
// polygons have the same center or not
function check(n, m)
{
    if (m % n == 0)
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }
    return 0;
}

// Driver code
var n = 5;
var m = 10;

check(n, m);

// This code is contributed by Kirti

</script>
```

**Output:** 

```
YES
```

**业绩分析:**

*   **时间复杂度:** O(1)。
*   **辅助空间:** O(1)。