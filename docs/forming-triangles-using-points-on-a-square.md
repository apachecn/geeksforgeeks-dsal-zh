# 利用正方形上的点形成三角形

> 原文:[https://www . geesforgeks . org/forming-三角形-使用正方形上的点/](https://www.geeksforgeeks.org/forming-triangles-using-points-on-a-square/)

给定一个正方形，正方形的每一边都有 **N** 个点，这些点都不与正方形的角重合。任务是计算使用这些 **4 * N** 点(正方形每侧的 N 个点)作为三角形顶点可以形成的三角形总数。
**例:**

> **输入:**N = 1
> T3】输出: 4
> 每边一个点。因此，我们可以通过留下一个点，然后从四个点中选择另外三个点来制作三个矩形。
> **输入:** N = 2
> **输出:** 56

**途径:**在 **4 * N** 点中选择 **3** 点的途径数为**<sup>(4 * N)</sup>C<sub>3</sub>**。然而，其中一些并不形成三角形。当所有三个选定的点都在正方形的同一侧时，就会发生这种情况。这些三胞胎的总数为每侧**<sup>N</sup>C<sub>3</sub>**，即**4 *<sup>N</sup>C<sub>3</sub>**。因此，所需的三角形数将为**(<sup>(4 * N)</sup>C<sub>3</sub>)–(4 *<sup>N</sup>C<sub>3</sub>)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of possible triangles
int noOfTriangles(int n)
{
    int y = 4 * n;
    return ((y * (y - 2) * (y - 1))
            - (4 * n * (n - 2) * (n - 1)))
           / 6;
}

// Driver code
int main()
{
    int n = 1;

    cout << noOfTriangles(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the count
    // of possible triangles
    static int noOfTriangles(int n)
    {
        int y = 4 * n;
        return ((y * (y - 2) * (y - 1)) -
                (4 * n * (n - 2) * (n - 1))) / 6;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 1;

        System.out.println(noOfTriangles(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of possible triangles
def noOfTriangles(n):
    y = 4 * n
    return ((y * (y - 2) * (y - 1)) -
            (4 * n * (n - 2) * (n - 1)))// 6

# Driver code
n = 1

print(noOfTriangles(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the count
    // of possible triangles
    static int noOfTriangles(int n)
    {
        int y = 4 * n;
        return ((y * (y - 2) * (y - 1)) -
                (4 * n * (n - 2) * (n - 1))) / 6;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 1;

        Console.WriteLine(noOfTriangles(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the count
// of possible triangles
function noOfTriangles(n)
{
    var y = 4 * n;
    return ((y * (y - 2) * (y - 1))
            - (4 * n * (n - 2) * (n - 1)))
           / 6;
}

// Driver code
var n = 1;
document.write(noOfTriangles(n));

</script>
```

**Output:** 

```
4
```