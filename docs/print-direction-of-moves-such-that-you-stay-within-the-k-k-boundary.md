# 打印移动方向，使您停留在[-k，+k]边界内

> 原文:[https://www . geeksforgeeks . org/print-移动方向-这样-你就可以停留在-k-k-边界内/](https://www.geeksforgeeks.org/print-direction-of-moves-such-that-you-stay-within-the-k-k-boundary/)

给定一个由正整数 **N** 和整数 **K** 组成的数组 **arr[]** 。假设你从位置 0 开始，你可以从**arr【0】**开始通过**a【I】**位置向左或向右移动。任务是打印移动方向，通过向右或向左移动，您可以完成 **N** 步，而不超过 **[-K，+K]** 边界。如果不能执行步骤，打印 **-1** 。如果有多个答案，打印任意一个。
**举例:**

> **输入:** arr[] = {40，50，60，40}，K = 120
> **输出:**
> 右
> 右
> 左
> 右
> 说明:
> 由于 N = 4(数组中的元素个数)
> 我们需要从 arr[0]开始进行 4 次移动，使得
> 值不会超出[-120， 120]
> 移动 1:位置= 0 + 40 = 40
> 移动 2:位置= 40 + 50 = 90
> 移动 3:位置= 90–60 = 30
> 移动 4:位置= 30 + 50 = 80
> **输入:** arr[] = {40，50，60，40}，K = 20
> **输出:** -1

**方法:**可以按照以下步骤解决上述问题:

*   开始时将位置初始化为 0。
*   开始遍历所有的数组元素，
    *   如果 **a[i] +位置**没有超过左右边界，那么移动将是**“右”**。
    *   如果**位置-a[I]**没有超过左右边界，那么移动将是**“左”**。
*   如果在任何阶段两个条件都失败，则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print steps such that
// they do not cross the boundary
void printSteps(int a[], int n, int k)
{

    // To store the resultant string
    string res = "";

    // Initially at zero-th position
    int position = 0;
    int steps = 1;

    // Iterate for every i-th move
    for (int i = 0; i < n; i++) {

        // Check for right move condition
        if (position + a[i] <= k
            && position + a[i] >= (-k)) {
            position += a[i];
            res += "Right\n";
        }

        // Check for left move condition
        else if (position - a[i] >= -k
                 && position - a[i] <= k) {
            position -= a[i];
            res += "Left\n";
        }

        // No move is possible
        else {
            cout << -1;
            return;
        }
    }

    // Print the steps
    cout << res;
}

// Driver code
int main()
{
    int a[] = { 40, 50, 60, 40 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 120;
    printSteps(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print steps such that
// they do not cross the boundary
static void printSteps(int []a, int n, int k)
{

    // To store the resultant string
    String res = "";

    // Initially at zero-th position
    int position = 0;
    //int steps = 1;

    // Iterate for every i-th move
    for (int i = 0; i < n; i++)
    {

        // Check for right move condition
        if (position + a[i] <= k
            && position + a[i] >= (-k))
        {
            position += a[i];
            res += "Right\n";
        }

        // Check for left move condition
        else if (position - a[i] >= -k
                && position - a[i] <= k)
        {
            position -= a[i];
            res += "Left\n";
        }

        // No move is possible
        else
        {
            System.out.println(-1);
            return;
        }
    }

    // Print the steps
    System.out.println(res);
}

// Driver code
public static void main (String[] args)
{

    int []a = { 40, 50, 60, 40 };
    int n = a.length;
    int k = 120;
    printSteps(a, n, k);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print steps such that
# they do not cross the boundary
def printSteps(a, n, k):

    # To store the resultant string
    res = ""

    # Initially at zero-th position
    position = 0
    steps = 1

    # Iterate for every i-th move
    for i in range(n):

        # Check for right move condition
        if (position + a[i] <= k and
            position + a[i] >= -k):
            position += a[i]
            res += "Right\n"

        # Check for left move condition
        elif (position-a[i] >= -k and
              position-a[i] <= k):
            position -= a[i]
            res += "Left\n"

        # No move is possible
        else:
            print(-1)
            return
    print(res)

# Driver code
a = [40, 50, 60, 40]
n = len(a)
k = 120
printSteps(a, n, k)

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print steps such that
// they do not cross the boundary
static void printSteps(int []a, int n, int k)
{

    // To store the resultant string
    String res = "";

    // Initially at zero-th position
    int position = 0;
    //int steps = 1;

    // Iterate for every i-th move
    for (int i = 0; i < n; i++)
    {

        // Check for right move condition
        if (position + a[i] <= k
            && position + a[i] >= (-k))
        {
            position += a[i];
            res += "Right\n";
        }

        // Check for left move condition
        else if (position - a[i] >= -k
                && position - a[i] <= k)
        {
            position -= a[i];
            res += "Left\n";
        }

        // No move is possible
        else
        {
            Console.WriteLine(-1);
            return;
        }
    }

    // Print the steps
    Console.Write(res);
}

// Driver code
static void Main()
{
    int []a = { 40, 50, 60, 40 };
    int n = a.Length;
    int k = 120;
    printSteps(a, n, k);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print steps such that
// they do not cross the boundary
function printSteps($a, $n, $k)
{

    // To store the resultant string
    $res = "";

    // Initially at zero-th position
    $position = 0;
    $steps = 1;

    // Iterate for every i-th move
    for ($i = 0; $i < $n; $i++)
    {

        // Check for right move condition
        if ($position + $a[$i] <= $k
            && $position + $a[$i] >= (-$k))
            {
            $position += $a[$i];
            $res .= "Right\n";
        }

        // Check for left move condition
        else if ($position - $a[$i] >= -$k &&
                 $position - $a[$i] <= $k)
        {
            $position -= $a[$i];
            $res .= "Left\n";
        }

        // No move is possible
        else
        {
            echo -1;
            return;
        }
    }

    // Print the steps
    echo $res;
}

// Driver code
$a = array( 40, 50, 60, 40 );
$n = count($a);
$k = 120;
printSteps($a, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to print steps such that
    // they do not cross the boundary
    function printSteps(a , n , k) {

        // To store the resultant string
        var res = "";

        // Initially at zero-th position
        var position = 0;
        // var steps = 1;

        // Iterate for every i-th move
        for (i = 0; i < n; i++) {

            // Check for right move condition
            if (position + a[i] <= k && position + a[i] >= (-k)) {
                position += a[i];
                res += "Right<br/>";
            }

            // Check for left move condition
            else if (position - a[i] >= -k && position - a[i] <= k) {
                position -= a[i];
                res += "Left<br/>";
            }

            // No move is possible
            else {
                document.write(-1);
                return;
            }
        }

        // Print the steps
        document.write(res);
    }

    // Driver code

        var a = [ 40, 50, 60, 40 ];
        var n = a.length;
        var k = 120;
        printSteps(a, n, k);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Right
Right
Left
Right
```