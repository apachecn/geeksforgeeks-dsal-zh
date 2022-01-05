# 加减 K 后检查 N 是否可以是完美立方体

> 原文:[https://www . geesforgeks . org/check-n-can-a-perfect-cube-after-加减-k/](https://www.geeksforgeeks.org/check-whether-n-can-be-a-perfect-cube-after-adding-or-subtracting-k/)

给定两个整数 **N** 和 **K** ，任务是检查 **N** 与 **K** 相加或相减后是否能做成一个完美的立方体。
**举例:**

> **输入:** N = 7，K = 1
> **输出:**是
> 7 + 1 = 8 这是一个完美立方体(2 <sup>3</sup> = 8)
> **输入:** N = 5，K = 4
> **输出:**是
> 5–4 = 1 这是一个完美立方体(1 <sup>3</sup> = 1)

**方法:**解决这个问题最简单的方法是检查(N + K)或(N–K)是否是完美立方体。

1.  检查(N + K)是否是完美立方体
2.  如果不是，那么检查(N–K)是否是一个完美的立方体。
3.  如果两者都不是完美的立方体，则打印“否”，否则打印“是”。
4.  为了[检查一个数是否是完美立方](https://www.geeksforgeeks.org/perfect-cubes-range/)，最简单的方法就是找到这个数的立方根的楼层值的立方，然后检查这个立方和这个数是否相同。

```
if(N3 == (floor(∛N))3)
Then N is a perfect cube
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is
// a perfect Cube or not
bool isPerfectCube(int x)
{
    int cr = round(cbrt(x));
    return (cr * cr * cr == x);
}

void canBePerfectCube(int N, int K)
{
    if (isPerfectCube(N + K)
        || isPerfectCube(N - K))
        cout << "Yes\n";
    else
        cout << "No\n";
}

// Driver code
int main()
{
    int N = 7, K = 1;
    canBePerfectCube(N, K);

    N = 5, K = 4;
    canBePerfectCube(N, K);

    N = 7, K = 2;
    canBePerfectCube(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // Function to check if a number is
    // a perfect Cube or not
    static boolean isPerfectCube(int x)
    {
        int cr = (int)Math.cbrt(x);
        return (cr * cr * cr == x);
    }

    static void canBePerfectCube(int N, int K)
    {
        if (isPerfectCube(N + K)
            || isPerfectCube(N - K) == true)
            System.out.println("Yes");
        else
             System.out.println("No");
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 7;
        int K = 1;
        canBePerfectCube(N, K);

        N = 5;
        K = 4;
        canBePerfectCube(N, K);

        N = 7; K = 2;
        canBePerfectCube(N, K);

    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check if a number is
# a perfect Cube or not
def isPerfectCube(x) :
    cr = int(x ** (1/3));
    return (cr * cr * cr == x);

def canBePerfectCube(N, K) :
    if (isPerfectCube(N + K) or isPerfectCube(N - K)) :
        print("Yes");
    else :
        print("No");

# Driver code
if __name__ == "__main__" :

    N = 7; K = 1;
    canBePerfectCube(N, K);

    N = 5; K = 4;
    canBePerfectCube(N, K);

    N = 7; K = 2;
    canBePerfectCube(N, K);

# This code is contributed by Yash_R
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Function to check if a number is
    // a perfect Cube or not
    static bool isPerfectCube(int x)
    {
        int cr = (int)Math.Cbrt(x);
        return (cr * cr * cr == x);
    }

    static void canBePerfectCube(int N, int K)
    {
        if (isPerfectCube(N + K)
            || isPerfectCube(N - K) == true)
            Console.WriteLine("Yes");
        else
             Console.WriteLine("No");
    }

    // Driver code
    public static void Main (string[] args)
    {
        int N = 7;
        int K = 1;
        canBePerfectCube(N, K);

        N = 5;
        K = 4;
        canBePerfectCube(N, K);

        N = 7; K = 2;
        canBePerfectCube(N, K);

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check if a number is
// a perfect Cube or not
function isPerfectCube(x)
{
    var cr = Math.round(Math.cbrt(x));
    return (cr * cr * cr == x);
}

function canBePerfectCube(N, K)
{
    if (isPerfectCube(N + K)
        || isPerfectCube(N - K))
        document.write("Yes<br>");
    else
        document.write("No<br>");
}

// Driver code
var N = 7, K = 1;
canBePerfectCube(N, K);
N = 5, K = 4;
canBePerfectCube(N, K);
N = 7, K = 2;
canBePerfectCube(N, K);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Yes
Yes
No
```