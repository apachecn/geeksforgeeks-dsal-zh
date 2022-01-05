# 四面体中长度为 N 的不同循环路径的数量

> 原文:[https://www . geeksforgeeks . org/不同长度的 n 进四面体循环路径数/](https://www.geeksforgeeks.org/number-of-different-cyclic-paths-of-length-n-in-a-tetrahedron/)

给定一个四面体(顶点为 A、B、C、D)，任务是从一个顶点寻找长度为 n 的不同循环路径的个数。
**注:**只考虑单个顶点 B，即求从 B 到自身的长度为 N 的不同循环路径的个数。

**示例:**

```
Input: 2
Output: 3
The paths of length 2 which starts and ends at D are:
B-A-B
B-D-B
B-C-B

Input: 3
Output: 6
```

**方法:**动态规划可用于跟踪 n 的先前值的路径数量。检查剩余的移动数量，以及当我们在路径中移动时我们在哪里。那就是 4n 个州，每个州有 3 个选项。观察所有的顶点 A，B，C 都是等价的。让 **zB** 最初为 1，0 步时，我们只能到达 B 本身。让 **zACD** 为 1，因为到达其他顶点 A、C 和 D 的路径为 0。因此，形成的循环关系将是:

> N 步到达 b 的路径为= zADC*3

在每一步中， *zADC* 乘以 2 (2 个状态)，再加上 zB，因为 zB 是包含剩余 2 个状态的步骤 n-1 的路径数。

下面是上述方法的实现:

## C++

```
// C++ program count total number of
// paths to reach B from B
#include <bits/stdc++.h>
#include <math.h>
using namespace std;

// Function to count the number of
// steps in a tetrahedron
int countPaths(int n)
{
    // initially coming to B is B->B
    int zB = 1;

    // cannot reach A, D or C
    int zADC = 0;

    // iterate for all steps
    for (int i = 1; i <= n; i++) {

        // recurrence relation
        int nzB = zADC * 3;

        int nzADC = (zADC * 2 + zB);

        // memoize previous values
        zB = nzB;
        zADC = nzADC;
    }

    // returns steps
    return zB;
}

// Driver Code
int main()
{
    int n = 3;
    cout << countPaths(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program count total
// number of paths to reach
// B from B
import java.io.*;

class GFG
{

// Function to count the
// number of steps in a
// tetrahedron
static int countPaths(int n)
{
    // initially coming
    // to B is B->B
    int zB = 1;

    // cannot reach A, D or C
    int zADC = 0;

    // iterate for all steps
    for (int i = 1; i <= n; i++)
    {

        // recurrence relation
        int nzB = zADC * 3;

        int nzADC = (zADC * 2 + zB);

        // memoize previous values
        zB = nzB;
        zADC = nzADC;
    }

    // returns steps
    return zB;
}

// Driver Code
public static void main (String[] args)
{
    int n = 3;
    System.out.println(countPaths(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 program count total number of
# paths to reach B from B

# Function to count the number of
# steps in a tetrahedron
def countPaths(n):

    # initially coming to B is B->B
    zB = 1

    # cannot reach A, D or C
    zADC = 0

    # iterate for all steps
    for i in range(1, n + 1):

        # recurrence relation
        nzB = zADC * 3

        nzADC = (zADC * 2 + zB)

        # memoize previous values
        zB = nzB
        zADC = nzADC

    # returns steps
    return zB

# Driver code
n = 3
print(countPaths(n))

# This code is contributed by ashutosh450
```

## C#

```
// C# program count total
// number of paths to reach
// B from B
using System;

class GFG{

// Function to count the
// number of steps in a
// tetrahedron
static int countPaths(int n)
{

    // initially coming
    // to B is B->B
    int zB = 1;

    // cannot reach A, D or C
    int zADC = 0;

    // iterate for all steps
    for (int i = 1; i <= n; i++)
    {

        // recurrence relation
        int nzB = zADC * 3;

        int nzADC = (zADC * 2 + zB);

        // memoize previous values
        zB = nzB;
        zADC = nzADC;
    }

    // returns steps
    return zB;
}

    // Driver Code
    static public void Main ()
    {
        int n = 3;
        Console.WriteLine(countPaths(n));
    }
}

// This code is contributed by Sach
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program count total number
// of paths to reach B from B

// Function to count the number 
// of steps in a tetrahedron
function countPaths($n)
{
    // initially coming to B is B->B
    $zB = 1;

    // cannot reach A, D or C
    $zADC = 0;

    // iterate for all steps
    for ($i = 1; $i <= $n; $i++)
    {

        // recurrence relation
        $nzB = $zADC * 3;

        $nzADC = ($zADC * 2 + $zB);

        // memoize previous values
        $zB = $nzB;
        $zADC = $nzADC;
    }

    // returns steps
    return $zB;
}

// Driver Code
$n = 3;
echo countPaths($n);

// This code is contributed
// by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript program count total
// number of paths to reach
// B from B

// Function to count the
// number of steps in a
// tetrahedron
function countPaths(n)
{

    // Initially coming
    // to B is B->B
    let zB = 1;

    // Cannot reach A, D or C
    let zADC = 0;

    // Iterate for all steps
    for(let i = 1; i <= n; i++)
    {

        // recurrence relation
        let nzB = zADC * 3;

        let nzADC = (zADC * 2 + zB);

        // Memoize previous values
        zB = nzB;
        zADC = nzADC;
    }

    // Returns steps
    return zB;
}

// Driver code
let n = 3;
document.write(countPaths(n));

// This code is contributed by mukesh07      

</script>
```

**Output:** 

```
6
```