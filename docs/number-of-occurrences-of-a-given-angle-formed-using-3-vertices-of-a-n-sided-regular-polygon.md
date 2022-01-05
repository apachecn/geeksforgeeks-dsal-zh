# 使用 n 边正多边形的 3 个顶点形成的给定角度的出现次数

> 原文:[https://www . geeksforgeeks . org/给定角度正多边形使用 3 个顶点形成的出现次数/](https://www.geeksforgeeks.org/number-of-occurrences-of-a-given-angle-formed-using-3-vertices-of-a-n-sided-regular-polygon/)

给定一个 n 边正多边形和一个角度θ，任务是在一个顶点标记为 A <sub>1</sub> 、A <sub>2</sub> 、…、A <sub>n</sub> 的正 n 边形(有 n 个顶点的正多边形)中找到角度(A <sub>i</sub> 、A <sub>j</sub> 、A <sub>k</sub> ) = θ ( i < j < k)的出现次数。
**示例:**

```
Input: n = 4, ang = 90
Output: 4

Input: n = 6, ang = 50
Output: 0
```

**进场:**

1.  首先我们检查这样一个角度是否存在。
2.  考虑顶点为 **x** 、 **y** 和 **z** ，要寻找的角度为 xyz。
3.  **x** 与 **y** 之间的边数为 **a** ，而 **y** 与 **z** 之间的边数为 **b** 。
4.  然后**∠XYZ = 180 –( 180 *(a+b))/n**。
5.  因此**≈XYZ * n(mod 180)= 0**。
6.  接下来我们需要找到这些角度的计数。
7.  由于多边形是规则的，我们只需要计算一个顶点的角度，就可以直接将结果乘以 n(顶点的数量)。
8.  在每个顶点处，可以在 **n-1-freq** 次处找到角度，其中 **freq = (n*ang)/180** 并描绘了创建所需角度后剩余的边数，即 z 和 x 之间的边数

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function that calculates occurrences
// of given angle that can be created
// using any 3 sides
int solve(int ang, int n)
{

    // Maximum angle in a regular n-gon
    // is equal to the interior angle
    // If the given angle
    // is greater than the interior angle
    // then the given angle cannot be created
    if ((ang * n) > (180 * (n - 2))) {
        return 0;
    }

    // The given angle times n should be divisible
    // by 180 else it cannot be created
    else if ((ang * n) % 180 != 0) {
        return 0;
    }

    // Initialise answer
    int ans = 1;

    // Calculate the frequency
    // of given angle for each vertex
    int freq = (ang * n) / 180;

    // Multiply answer by frequency.
    ans = ans * (n - 1 - freq);

    // Multiply answer by the number of vertices.
    ans = ans * n;

    return ans;
}

// Driver code
int main()
{
    int ang = 90, n = 4;

    cout << solve(ang, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that calculates occurrences
// of given angle that can be created
// using any 3 sides
static int solve(int ang, int n)
{

    // Maximum angle in a regular n-gon
    // is equal to the interior angle
    // If the given angle
    // is greater than the interior angle
    // then the given angle cannot be created
    if ((ang * n) > (180 * (n - 2)))
    {
        return 0;
    }

    // The given angle times n should be divisible
    // by 180 else it cannot be created
    else if ((ang * n) % 180 != 0)
    {
        return 0;
    }

    // Initialise answer
    int ans = 1;

    // Calculate the frequency
    // of given angle for each vertex
    int freq = (ang * n) / 180;

    // Multiply answer by frequency.
    ans = ans * (n - 1 - freq);

    // Multiply answer by the number of vertices.
    ans = ans * n;

    return ans;
}

// Driver code
public static void main (String[] args)
{
    int ang = 90, n = 4;
    System.out.println(solve(ang, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that calculates occurrences
# of given angle that can be created
# using any 3 sides
def solve(ang, n):

    # Maximum angle in a regular n-gon
    # is equal to the interior angle
    # If the given angle
    # is greater than the interior angle
    # then the given angle cannot be created
    if ((ang * n) > (180 * (n - 2))):
        return 0

    # The given angle times n should be divisible
    # by 180 else it cannot be created
    elif ((ang * n) % 180 != 0):
        return 0

    # Initialise answer
    ans = 1

    # Calculate the frequency
    # of given angle for each vertex
    freq = (ang * n) // 180

    # Multiply answer by frequency.
    ans = ans * (n - 1 - freq)

    # Multiply answer by the number of vertices.
    ans = ans * n

    return ans

# Driver code
ang = 90
n = 4

print(solve(ang, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that calculates occurrences
// of given angle that can be created
// using any 3 sides
static int solve(int ang, int n)
{

    // Maximum angle in a regular n-gon
    // is equal to the interior angle
    // If the given angle
    // is greater than the interior angle
    // then the given angle cannot be created
    if ((ang * n) > (180 * (n - 2)))
    {
        return 0;
    }

    // The given angle times n should be divisible
    // by 180 else it cannot be created
    else if ((ang * n) % 180 != 0)
    {
        return 0;
    }

    // Initialise answer
    int ans = 1;

    // Calculate the frequency
    // of given angle for each vertex
    int freq = (ang * n) / 180;

    // Multiply answer by frequency.
    ans = ans * (n - 1 - freq);

    // Multiply answer by the
    // number of vertices.
    ans = ans * n;

    return ans;
}

// Driver code
public static void Main (String[] args)
{
    int ang = 90, n = 4;
    Console.WriteLine(solve(ang, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
// Function that calculates occurrences
// of given angle that can be created
// using any 3 sides
function solve(ang , n)
{

    // Maximum angle in a regular n-gon
    // is equal to the interior angle
    // If the given angle
    // is greater than the interior angle
    // then the given angle cannot be created
    if ((ang * n) > (180 * (n - 2)))
    {
        return 0;
    }

    // The given angle times n should be divisible
    // by 180 else it cannot be created
    else if ((ang * n) % 180 != 0)
    {
        return 0;
    }

    // Initialise answer
    var ans = 1;

    // Calculate the frequency
    // of given angle for each vertex
    var freq = (ang * n) / 180;

    // Multiply answer by frequency.
    ans = ans * (n - 1 - freq);

    // Multiply answer by the number of vertices.
    ans = ans * n;

    return ans;
}

// Driver code
var ang = 90, n = 4;
document.write(solve(ang, n));

// This code contributed by shikhasingrajput 

</script>
```

**Output:** 

```
4
```