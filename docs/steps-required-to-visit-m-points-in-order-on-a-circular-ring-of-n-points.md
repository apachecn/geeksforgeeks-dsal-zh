# 在 N 个点的圆环上按顺序访问 M 个点所需的步骤

> 原文:[https://www . geeksforgeeks . org/steps-需要访问的步骤-n 点圆环上的有序 m 点/](https://www.geeksforgeeks.org/steps-required-to-visit-m-points-in-order-on-a-circular-ring-of-n-points/)

给定一个整数“n”，考虑一个包含从“1”到“n”的“n”个点的圆环，这样你可以按以下方式移动:

> 1 -> 2 -> 3 -> …..-> n -> 1 -> 2 -> 3 -> ……

此外，给定一个整数数组(大小为“m”)，任务是找到从“1”
**开始按顺序到达数组中每个点所需的步数。示例:**

```
Input: n = 3, m = 3, arr[] = {2, 1, 2}
Output: 4
The sequence followed is 1->2->3->1->2

Input: n = 2, m = 1, arr[] = {2}
Output: 1
The sequence followed is 1->2
```

**方式:**我们用**曲线**表示当前位置，用 **nxt** 表示下一个位置。这给了我们两个例子:

1.  如果 **cur** 小于 **nxt** ，可以在**NXT–cur**步移至该处。
2.  否则，首先需要在**n–cur**步到达 n 点，然后可以在 **cur** 步移动到 nxt。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the steps required
int findSteps(int n, int m, int a[])
{

    // Start at 1
    int cur = 1;

    // Initialize steps
    int steps = 0;
    for (int i = 0; i < m; i++) {

        // If nxt is greater than cur
        if (a[i] >= cur)
            steps += (a[i] - cur);
        else
            steps += (n - cur + a[i]);

        // Now we are at a[i]
        cur = a[i];
    }
    return steps;
}

// Driver code
int main()
{
    int n = 3, m = 3;
    int a[] = { 2, 1, 2 };
    cout << findSteps(n, m, a);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to count the steps required
static int findSteps(int n, int m,
                     int a[])
{

    // Start at 1
    int cur = 1;

    // Initialize steps
    int steps = 0;
    for (int i = 0; i < m; i++)
    {

        // If nxt is greater than cur
        if (a[i] >= cur)
            steps += (a[i] - cur);
        else
            steps += (n - cur + a[i]);

        // Now we are at a[i]
        cur = a[i];
    }
    return steps;
}

// Driver code
public static void main(String []args)
{
    int n = 3, m = 3;
    int a[] = { 2, 1, 2 };
    System.out.println(findSteps(n, m, a));
}
}

// This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function to count the
// steps required
static int findSteps(int n,
                     int m, int []a)
{

    // Start at 1
    int cur = 1;

    // Initialize steps
    int steps = 0;
    for (int i = 0; i < m; i++)
    {

        // If nxt is greater than cur
        if (a[i] >= cur)
            steps += (a[i] - cur);
        else
            steps += (n - cur + a[i]);

        // Now we are at a[i]
        cur = a[i];
    }
    return steps;
}

// Driver code
public static void Main()
{
    int n = 3, m = 3;
    int []a = { 2, 1, 2 };
    Console.WriteLine(findSteps(n, m, a));
}
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to count the steps required
def findSteps(n, m, a):

    # Start at 1
    cur = 1

    # Initialize steps
    steps = 0
    for i in range(0, m):

        # If nxt is greater than cur
        if (a[i] >= cur):
            steps += (a[i] - cur)
        else:
            steps += (n - cur + a[i])

        # Now we are at a[i]
        cur = a[i]

    return steps

# Driver code
n = 3
m = 3
a = [2, 1, 2 ]
print(findSteps(n, m, a))

# This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to count the steps required
function findSteps($n, $m, $a)
{

    // Start at 1
    $cur = 1;

    // Initialize steps
    $steps = 0;
    for ($i = 0; $i < $m; $i++)
    {

        // If nxt is greater than cur
        if ($a[$i] >= $cur)
            $steps += ($a[$i] - $cur);
        else
            $steps += ($n - $cur + $a[$i]);

        // Now we are at a[i]
        $cur = $a[$i];
    }
    return $steps;
}

// Driver code
$n = 3;
$m = 3;
$a = array(2, 1, 2 );
echo findSteps($n, $m, $a);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to count the steps required
function findSteps(n, m, a)
{

    // Start at 1
    var cur = 1;

    // Initialize steps
    var steps = 0;
    for (var i = 0; i < m; i++) {

        // If nxt is greater than cur
        if (a[i] >= cur)
            steps += (a[i] - cur);
        else
            steps += (n - cur + a[i]);

        // Now we are at a[i]
        cur = a[i];
    }
    return steps;
}

// Driver code
var n = 3, m = 3;
var a = [ 2, 1, 2 ];
document.write( findSteps(n, m, a));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(M)

**辅助空间:** O(1)