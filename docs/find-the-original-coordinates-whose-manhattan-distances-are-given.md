# 找到给出曼哈顿距离的原始坐标

> 原文:[https://www . geeksforgeeks . org/find-原始坐标-给出了谁的曼哈顿距离/](https://www.geeksforgeeks.org/find-the-original-coordinates-whose-manhattan-distances-are-given/)

给定二维平面上三个坐标的曼哈顿距离，任务是找到原始坐标。如果可能有多个解决方案，打印任何解决方案，否则打印 **-1** 。

> **输入:** d1 = 3，d2 = 4，d3 = 5
> **输出:** (0，0)、(3，0)和(1，3)
> 曼哈顿距离(0，0)到(3，0)为 3，
> (3，0)到(1，3)为 5，而(0，0)到(1，3)为 4
> **输入:** d1 = 5，d2 = 10，d3 = 12

****进场:**我们来分析一下什么时候没有解。首先，三角形不等式必须成立，即最大距离不应超过其他两个的总和。第二，所有曼哈顿距离的总和应该是偶数。
这就是为什么，如果我们有三个点，它们的 x 坐标是 **x1** 、 **x2** 和 **x3** ，这样 **x1 < x2 < x3** 。它们将构成总和**(x2–x1)+(x3–x1)+(x3–x2)= 2 *(x3–x1)**。同样的逻辑适用于 y 坐标。
在所有其他情况下，我们都有解决方案。让 **d1** 、 **d2** 和 **d3** 为给定的曼哈顿距离。将两点固定为 **(0，0)** 和 **(d1，0)** 。现在由于两点是固定的，我们很容易找到第三点为**x3 =(D1+D2–D3)/2**和**y3 =(D2–x3)**。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the original coordinated
void solve(int d1, int d2, int d3)
{

    // Maximum of the given distances
    int maxx = max(d1, max(d2, d3));

    // Sum of the given distances
    int sum = (d1 + d2 + d3);

    // Conditions when the
    // solution doesn't exist
    if (2 * maxx > sum or sum % 2 == 1) {
        cout << "-1";
        return;
    }

    // First coordinate
    int x1 = 0, y1 = 0;

    // Second coordinate
    int x2 = d1, y2 = 0;

    // Third coordinate
    int x3 = (d1 + d2 - d3) / 2;
    int y3 = (d2 + d3 - d1) / 2;
    cout << "(" << x1 << ", " << y1 << "), ("
         << x2 << ", " << y2 << ") and ("
         << x3 << ", " << y3 << ")";
}

// Driver code
int main()
{
    int d1 = 3, d2 = 4, d3 = 5;
    solve(d1, d2, d3);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java .io.*;

class GFG
{

// Function to find the original coordinated
static void solve(int d1, int d2, int d3)
{

    // Maximum of the given distances
    int maxx = Math.max(d1, Math.max(d2, d3));

    // Sum of the given distances
    int sum = (d1 + d2 + d3);

    // Conditions when the
    // solution doesn't exist
    if (2 * maxx > sum || sum % 2 == 1)
    {
        System.out.print("-1");
        return;
    }

    // First coordinate
    int x1 = 0, y1 = 0;

    // Second coordinate
    int x2 = d1, y2 = 0;

    // Third coordinate
    int x3 = (d1 + d2 - d3) / 2;
    int y3 = (d2 + d3 - d1) / 2;
    System.out.print("("+x1+", "+y1+"), ("+x2+", "+y2+") and ("+x3+", "+y3+")");
}

// Driver code
public static void main(String[] args)
{
    int d1 = 3, d2 = 4, d3 = 5;
    solve(d1, d2, d3);

}
}

// This code is contributed by anuj_67..
```

**<gfg-tab role="tab" slot="tab" id="gfg-tab-2">蟒 3</gfg-tab>T3**

```
 `# Python3 implementation of the approach

# Function to find the original coordinated
def solve(d1, d2, d3) :

    # Maximum of the given distances
    maxx = max(d1, max(d2, d3))

    # Sum of the given distances
    sum = (d1 + d2 + d3)

    # Conditions when the
    # solution doesn't exist
    if (2 * maxx > sum or sum % 2 == 1) :
        print("-1")
        return

    # First coordinate
    x1 = 0
    y1 = 0

    # Second coordinate
    x2 = d1 
    y2 = 0

    # Third coordinate
    x3 = (d1 + d2 - d3) // 2
    y3 = (d2 + d3 - d1) // 2
    print("(" , x1 , "," , y1 , "), ("
        , x2 , "," , y2 , ") and ("
        , x3 , "," , y3 , ")")

# Driver code
d1 = 3
d2 = 4
d3 = 5
solve(d1, d2, d3)

# This code is contributed by ihritik` 
```

**T4** 

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the original coordinated
static void solve(int d1, int d2, int d3)
{

    // Maximum of the given distances
    int maxx = Math.Max(d1, Math.Max(d2, d3));

    // Sum of the given distances
    int sum = (d1 + d2 + d3);

    // Conditions when the
    // solution doesn't exist
    if (2 * maxx > sum || sum % 2 == 1)
    {
        Console.WriteLine("-1");
        return;
    }

    // First coordinate
    int x1 = 0, y1 = 0;

    // Second coordinate
    int x2 = d1, y2 = 0;

    // Third coordinate
    int x3 = (d1 + d2 - d3) / 2;
    int y3 = (d2 + d3 - d1) / 2;
    Console.WriteLine("("+x1+", "+y1+"), ("+x2+", "+y2+") and ("+x3+", "+y3+")");
}

// Driver code
static void Main()
{
    int d1 = 3, d2 = 4, d3 = 5;
    solve(d1, d2, d3);

}
}

// This code is contributed by mits
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

// Function to find the original coordinated
function solve(d1, d2, d3)
{

    // Maximum of the given distances
    let maxx = Math.max(d1, Math.max(d2, d3));

    // Sum of the given distances
    let sum = (d1 + d2 + d3);

    // Conditions when the
    // solution doesn't exist
    if (2 * maxx > sum || sum % 2 == 1) {
        document.write("-1");
        return;
    }

    // First coordinate
    let x1 = 0, y1 = 0;

    // Second coordinate
    let x2 = d1, y2 = 0;

    // Third coordinate
    let x3 = parseInt((d1 + d2 - d3) / 2);
    let y3 = parseInt((d2 + d3 - d1) / 2);
    document.write("(" + x1 + ", " + y1 + "), ("
         + x2 + ", " + y2 + ") and ("
         + x3 + ", " + y3 + ")");
}

// Driver code
    let d1 = 3, d2 = 4, d3 = 5;
    solve(d1, d2, d3);

</script>
```

****Output:** 

```
(0, 0), (3, 0) and (1, 3)
```**