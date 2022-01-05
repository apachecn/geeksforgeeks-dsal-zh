# 从质心到顶点有直线的多边形的循环数

> 原文:[https://www . geeksforgeeks . org/多边形从质心到顶点的圈数/](https://www.geeksforgeeks.org/number-of-cycles-in-a-polygon-with-lines-from-centroid-to-vertices/)

给定一个数字 **N** ，它表示多边形的质心与所有顶点相连的多边形的边数，任务是找出多边形中的循环数。
**例:**

> **输入:** N = 4
> **输出:** 13
> **输入:** N = 8
> **输出:** 57

**方法:**这个问题遵循一个简单的方法，我们可以使用一个简单的公式来计算多边形中从质心到顶点的圈数。为了推导循环数，我们可以使用这个公式:

> (N)*(N–1)+1

如果 N 的值是 4，我们可以用这个简单的公式求出 13 的循环数。以类似的方式，如果 N 的值是 10，那么周期数将是 91。
以下是上述方法的实现:

## C++

```
// C++ program to find number
// of cycles in a Polygon with
// lines from Centroid to Vertices

#include <bits/stdc++.h>
using namespace std;

// Function to find the Number of Cycles
int nCycle(int N)
{
    return (N) * (N - 1) + 1;
}

// Driver code
int main()
{
    int N = 4;
    cout << nCycle(N)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of cycles in a Polygon with
// lines from Centroid to Vertices
class GFG{

// Function to find the Number of Cycles
static int nCycle(int N)
{
    return (N) * (N - 1) + 1;
}

// Driver code
public static void main (String[] args)
{
    int N = 4;
    System.out.println(nCycle(N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to find number
# of cycles in a Polygon with
# lines from Centroid to Vertices

# Function to find the Number of Cycles
def nCycle(N):

    return (N) * (N - 1) + 1

# Driver code
N = 4
print(nCycle(N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find number
// of cycles in a Polygon with
// lines from Centroid to Vertices
using System;
class GFG{

// Function to find the Number of Cycles
static int nCycle(int N)
{
    return (N) * (N - 1) + 1;
}

// Driver code
public static void Main (String[] args)
{
    int N = 4;
    Console.Write(nCycle(N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to find number
    // of cycles in a Polygon with
    // lines from Centroid to Vertices

    // Function to find the Number of Cycles
    function nCycle(N)
    {
        return (N) * (N - 1) + 1;
    }

    let N = 4;
    document.write(nCycle(N));

</script>
```

**Output:**

```
13
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)