# 求面积= (S / 2)

的三角形的坐标

> 原文:[https://www . geeksforgeeks . org/find-一个三角形的坐标-其面积-s-2/](https://www.geeksforgeeks.org/find-the-coordinates-of-a-triangle-whose-area-s-2/)

给定一个整数 **S** ，任务是找到面积为 **(S / 2)** 的三角形的坐标。

**示例:**

> **输入:** S = 4
> **输出:**
> (0，0)
> (100000000，1)
> (999999996，1)
> 
> **输入:** S = 15
> **输出:**
> (0，0)
> (1000000000，1)
> (999999985，1)

**进场:**

*   已知坐标为 **(X1，Y1)** 、 **(X2，Y2)** 、 **(X3，Y3)** 的三角形面积由**A =((X1 * Y2)+(X2 * Y3)+(X3 * Y1)–(X1 * Y3)–(X2 * Y1)–(X3 * Y2))/2**给出。
*   现在将 **(X1，Y1)** 固定到 **(0，0)** 给出**A =((X2 * Y3)–(X3 * Y2))/2**。
*   给出了 **A = S / 2** 这意味着**S =(X2 * Y3)–(X3 * Y2)**。
*   现在将 **(X2，Y2)** 固定为 **(10 <sup>9</sup> ，1)** ，等式变为**S = 10<sup>9</sup>* Y3–X3**，可以通过取给定另一个变量整数值的变量的整数值来求解。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const long MAX = 1000000000;

// Function to find the triangle
// with area = (S / 2)
void findTriangle(long S)
{

    // Fix the two pairs of coordinates
    long X1 = 0, Y1 = 0;
    long X2 = MAX, Y2 = 1;

    // Find (X3, Y3) with integer coordinates
    long X3 = (MAX - S % MAX) % MAX;
    long Y3 = (S + X3) / MAX;

    cout << "(" << X1 << ", " << Y1 << ")\n";
    cout << "(" << X2 << ", " << Y2 << ")\n";
    cout << "(" << X3 << ", " << Y3 << ")";
}

// Driver code
int main()
{

    long S = 4;

    findTriangle(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final long MAX = 1000000000;

    // Function to find the triangle
    // with area = (S / 2)
    static void findTriangle(long S)
    {

        // Fix the two pairs of coordinates
        long X1 = 0, Y1 = 0;
        long X2 = MAX, Y2 = 1;

        // Find (X3, Y3) with integer coordinates
        long X3 = (MAX - S % MAX) % MAX;
        long Y3 = (S + X3) / MAX;

        System.out.println("(" + X1 +
                           ", " + Y1 + ")");
        System.out.println("(" + X2 +
                           ", " + Y2 + ")");
        System.out.println("(" + X3 +
                           ", " + Y3 + ")");
    }

    // Driver code
    public static void main (String[] args)
    {
        long S = 4;

        findTriangle(S);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 1000000000;

# Function to find the triangle
# with area = (S / 2)
def findTriangle(S) :

    # Fix the two pairs of coordinates
    X1 = 0; Y1 = 0;
    X2 = MAX; Y2 = 1;

    # Find (X3, Y3) with integer coordinates
    X3 = (MAX - S % MAX) % MAX;
    Y3 = (S + X3) / MAX;

    print("(", X1, ",", Y1, ")");
    print("(", X2, ",", Y2, ")");
    print("(", X3, ",", Y3, ")");

# Driver code
if __name__ == "__main__" :

    S = 4;

    findTriangle(S);

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static readonly long MAX = 1000000000;

    // Function to find the triangle
    // with area = (S / 2)
    static void findTriangle(long S)
    {

        // Fix the two pairs of coordinates
        long X1 = 0, Y1 = 0;
        long X2 = MAX, Y2 = 1;

        // Find (X3, Y3) with integer coordinates
        long X3 = (MAX - S % MAX) % MAX;
        long Y3 = (S + X3) / MAX;

        Console.WriteLine("(" + X1 +
                         ", " + Y1 + ")");
        Console.WriteLine("(" + X2 +
                         ", " + Y2 + ")");
        Console.WriteLine("(" + X3 +
                         ", " + Y3 + ")");
    }

    // Driver code
    public static void Main (String[] args)
    {
        long S = 4;

        findTriangle(S);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

let MAX = 1000000000;

// Function to find the triangle
// with area = (S / 2)
function findTriangle( S)
{

    // Fix the two pairs of coordinates
    let X1 = 0, Y1 = 0;
    let X2 = MAX, Y2 = 1;

    // Find (X3, Y3) with integer coordinates
    let X3 = (MAX - S % MAX) % MAX;
    let Y3 = (S + X3) / MAX;

    document.write( "(" + X1 + ", " + Y1 + ")<br/>");
    document.write( "(" + X2 + ", " + Y2 + ")<br/>");
    document.write( "(" + X3 + ", " + Y3 + ")<br/>")
    }

// Driver code

    let S = 4;

    findTriangle(S);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
(0, 0)
(1000000000, 1)
(999999996, 1)
```

**时间复杂度:** O(1)