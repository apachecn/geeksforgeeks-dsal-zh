# 满足点(A，B)时的抛物线，方程给出

> 原文:[https://www . geeksforgeeks . org/当给定 a-b 点和方程时满足抛物线/](https://www.geeksforgeeks.org/satisfy-the-parabola-when-point-a-b-and-the-equation-is-given/)

给定一个点 **(A，B)** ，使得曲线上每个点的距离 **M.y = N.x <sup>2</sup> + O.x + P** 与 **(A，B)** 等于曲线上该点与 **x 轴**之间的距离。任务是找到 **M，N O，P** 的值。

**注:**方程应为简单形式，即 **gcd( |M|、|N|、|O|、|P| ) = 1** 和 **N** 应始终为正。

**示例:**

> **输入:** A = 1，B = 1
> **输出:** 2 1 -2 2
> M = 2，N = 1，O = -2，P = 2
> 曲线方程为
> T8】2y = x<sup>2</sup>–2x+2
> 
> **输入:** A = -1，B = 1
> T3】输出:2 1 2 2 2

**方法:**从抛物线的性质来看，对于曲线上的每个点，与准线和焦点的距离总是相等的。使用该属性，将 **y = 0** 视为准线， **(A，B)** 视为焦点。
由于在等式**中 N** 被给定为总是正的，抛物线将面向上，抛物线的等式为**(x–h)<sup>2</sup>= 4p(y–k)**，其中 **(h，k)** 是顶点的坐标，p 是焦点与顶点或顶点与准线之间的距离。

由于顶点是焦点垂直距离 **(A，B)** 和准线(A，0)之间的中点，这里是 **B** 。所以顶点的坐标是(A，B/2)**p**也是 **B/2** 。
那么，方程就是**(x–A)<sup>2</sup>= 4 * B/2 *(y–B/2)**。
这个方程可以求解得到结果:

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required values
void solve(int A, int B)
{
    double p = B / 2.0;
    int M = ceil(4 * p);
    int N = 1;
    int O = - 2 * A;
    int Q = ceil(A * A + 4 * p*p);
    cout << M << " " << N << " "
         << O << " " << Q;
}

// Driver code
int main()
{
    int a = 1;
    int b = 1;
    solve(a, b);
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find the required values
    static void solve(int A, int B)
    {
        double p = B / 2.0;
        double M = Math.ceil(4 * p);
        int N = 1;
        int O = - 2 * A;
        double Q = Math.ceil(A * A + 4 * p * p);
        System.out.println(M + " " + N +
                               " " + O + " " + Q);
    }

    // Driver code
    public static void main (String[] args)
    {
        int a = 1;
        int b = 1;
        solve(a, b);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required values
def solve(A, B):
    p = B / 2
    M = int(4 * p)
    N = 1
    O = - 2 * A
    Q = int(A * A + 4 * p*p)
    return [M, N, O, Q]

# Driver code
a = 1
b = 1
print(*solve(a, b))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to find the required values
    static void solve(int A, int B)
    {
        double p = B / 2.0;

        double M = Math.Ceiling(4 * p);

        int N = 1;
        int O = - 2 * A;

        double Q = Math.Ceiling(A * A + 4 * p * p);

        Console.Write(M + " " + N + " " + O + " " + Q);
    }

    // Driver code
    static public void Main ()
    {
        int a = 1;
        int b = 1;
        solve(a, b);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to find the required values
    function solve(A, B)
    {
        let p = B / 2.0;
        let M = Math.ceil(4 * p);
        let N = 1;
        let O = - 2 * A;
        let Q = Math.ceil(A * A + 4 * p * p);
        document.write(M + " " + N + " " + O + " " + Q);
    }

    let a = 1;
    let b = 1;
    solve(a, b);

</script>
```

**Output:** 

```
2 1 -2 2
```