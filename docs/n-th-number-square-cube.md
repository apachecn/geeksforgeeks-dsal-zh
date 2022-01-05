# 既是正方形又是立方体的第 N 个数

> 原文:[https://www.geeksforgeeks.org/n-th-number-square-cube/](https://www.geeksforgeeks.org/n-th-number-square-cube/)

给定一个数 n，求第 n 个数，它既是正方形又是立方体。前几个这样的数字是 1，64，729…

**示例:**

```
Input : 3
Output :729
        729 is square of 27 and cube of 3.
Input :5
Output :15625
```

想法很简单，第 n 个这样的数字是 n <sup>6</sup>

## C++

```
// C++ program to find n-th number which is both
// square and cube.
#include <bits/stdc++.h>
using namespace std;

int nthSquareCube(int n)
{
   return n*n*n*n*n*n;
}

// Driver code
int main()
{
    int n = 5;
    cout << nthSquareCube(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number
// which is both square and cube.
class GFG {

    static int nthSquareCube(int n)
    {
        return n * n * n * n * n * n;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;

        System.out.println(nthSquareCube(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# program to find n-th number
# which is both square and cube.

def nthSquareCube(n):

    return n * n * n * n * n * n

# Driver code
n = 5
print(nthSquareCube(n))
# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find n-th number
// which is both square and cube.
using System;

class GFG
{

    static int nthSquareCube(int n)
    {
        return n * n * n * n * n * n;
    }

    // Driver code
    static public void Main ()
    {
        int n = 5;

        Console.WriteLine(nthSquareCube(n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th
// number which is both
// square and cube.

function nthSquareCube($n)
{
    return $n * $n * $n *
           $n * $n * $n;
}

// Driver code
$n = 5;
echo(nthSquareCube($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find n-th number
// which is bothsquare and cube.
function nthSquareCube(n)
{
    return n * n * n * n * n * n;
}

// Driver code
let n = 5;

document.write(nthSquareCube(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
15625
```