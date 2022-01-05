# x<y 的解的个数，其中 a < = x < = b 和 c < = y < = d 和 x，y 是整数

> 原文:[https://www . geeksforgeeks . org/number-of-x-y-where-a-x-B-和-c-y-d-和-x-y-都是整数/](https://www.geeksforgeeks.org/number-of-solutions-for-x-y-where-a-x-b-and-c-y-d-and-x-y-are-integers/)

给定四个整数 a，b，c，d(直到 10^6)。任务是找到 x 的解的个数< y, where a <= x <= b and c <= y <= d and x, y integers. 
**例** :

```
Input: a = 2, b = 3, c = 3, d = 4
Output: 3

Input: a = 3, b = 5, c = 6, d = 7
Output: 6
```

**方法:**让我们显式迭代 x 的所有可能值，对于 x 的一个这样的固定值，问题简化为有多少个 y 值使得 **c < = y < = d** 和 **x = max(c，x + 1)** 和 **y < = d** 。假设 **c < = d** ，否则当然没有 y 的有效值。因此，对于一个固定的 x，有**d–max(c，x+1)+1**y 的有效值，因为一个范围[R1，R2]内的整数个数是由**R2–R1+1 给出的。**
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to Find the number of solutions for x < y,
// where a <= x <= b and c <= y <= d and x, y integers.
int NumberOfSolutions(int a, int b, int c, int d)
{
    // to store answer
    int ans = 0;

    // iterate explicitly over all possible values of x
    for (int i = a; i <= b; i++)
        if (d >= max(c, i + 1))
            ans += d - max(c, i + 1) + 1;

    // return answer
    return ans;
}

// Driver code
int main()
{
    int a = 2, b = 3, c = 3, d = 4;

    // function call
    cout << NumberOfSolutions(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

// function to Find the number of
// solutions for x < y, where
// a <= x <= b and c <= y <= d
// and x, y integers.
static int NumberOfSolutions(int a, int b,
                             int c, int d)
{
    // to store answer
    int ans = 0;

    // iterate explicitly over all
    // possible values of x
    for (int i = a; i <= b; i++)
        if (d >= Math.max(c, i + 1))
            ans += d - Math.max(c, i + 1) + 1;

    // return answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int a = 2, b = 3, c = 3, d = 4;

    // function call
    System.out.println(NumberOfSolutions(a, b, c, d));
}
}

// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# function to Find the number of
# solutions for x < y, where
# a <= x <= b and c <= y <= d and
# x, y integers.
def NumberOfSolutions(a, b, c, d) :

    # to store answer
    ans = 0

    # iterate explicitly over all
    # possible values of x
    for i in range(a, b + 1) :

        if d >= max(c, i + 1) :

            ans += d - max(c, i + 1) + 1

    # return answer
    return ans

# Driver code
if __name__ == "__main__" :

    a, b, c, d = 2, 3, 3, 4

    # function call
    print(NumberOfSolutions(a, b, c, d))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// function to Find the number of
// solutions for x < y, where
// a <= x <= b and c <= y <= d
// and x, y integers.
static int NumberOfSolutions(int a, int b,
                              int c, int d)
{
    // to store answer
    int ans = 0;

    // iterate explicitly over all
    // possible values of x
    for (int i = a; i <= b; i++)
        if (d >= Math.Max(c, i + 1))
            ans += d - Math.Max(c, i + 1) + 1;

    // return answer
    return ans;
}

// Driver code
public static void Main()
{
    int a = 2, b = 3, c = 3, d = 4;

    // function call
    Console.WriteLine(NumberOfSolutions(a, b, c, d));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// function to Find the number
// of solutions for x < y, where
// a <= x <= b and c <= y <= d
// and x, y integers.
function NumberOfSolutions($a, $b, $c, $d)
{
    // to store answer
    $ans = 0;

    // iterate explicitly over all
    // possible values of x
    for ($i = $a; $i <= $b; $i++)
        if ($d >= max($c, $i + 1))
            $ans += $d - max($c, $i + 1) + 1;

    // return answer
    return $ans;
}

// Driver code
$a = 2; $b = 3; $c = 3; $d = 4;

// function call
echo NumberOfSolutions($a, $b, $c, $d);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// function to Find the number of
// solutions for x < y, where
// a <= x <= b and c <= y <= d
// and x, y integers.
function NumberOfSolutions(a, b, c, d)
{
    // to store answer
    let ans = 0;

    // iterate explicitly over all
    // possible values of x
    for (let i = a; i <= b; i++)
        if (d >= Math.max(c, i + 1))
            ans += d - Math.max(c, i + 1) + 1;

    // return answer
    return ans;
}

// Driver Code

    let a = 2, b = 3, c = 3, d = 4;

    // function call
    document.write(NumberOfSolutions(a, b, c, d));

</script>
```

**Output:** 

```
3
```