# 程序找出任意两个不同数字的指数之间的最大差值

> 原文:[https://www . geesforgeks . org/program-to-find-任何两个不同数字的索引之间的最大差异/](https://www.geeksforgeeks.org/program-to-find-the-maximum-difference-between-the-index-of-any-two-different-numbers/)

给定一组 **N 个**整数。任务是找出任何两个不同数字的索引之间的最大差异。**注意**至少有两个不同的数字。
**例:**

> **输入:** a[] = {1，2，3，2，3}
> **输出:**4
> 1 和最后 3 的差。
> **输入:** a[] = {1，1，3，1，1}
> **输出:**3
> 3 的指数与最后 1 的差。

**方法:**最初，从末尾开始检查与**a【0】**不同的第一个数字，将它们的指数之差存储为 **ind1** 。此外，从一开始就检查第一个不同于**a【n–1】**的数字，将它们的索引之差存储为 **ind2** 。答案将是 **max(ind1，ind2)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum difference
int findMaximumDiff(int a[], int n)
{
    int ind1 = 0;

    // Iteratively check from back
    for (int i = n - 1; i > 0; i--) {

        // Different numbers
        if (a[0] != a[i]) {
            ind1 = i;
            break;
        }
    }

    int ind2 = 0;

    // Iteratively check from
    // the beginning
    for (int i = 0; i < n - 1; i++) {

        // Different numbers
        if (a[n - 1] != a[i]) {
            ind2 = (n - 1 - i);
            break;
        }
    }

    return max(ind1, ind2);
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << findMaximumDiff(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum difference
static int findMaximumDiff(int []a, int n)
{
    int ind1 = 0;

    // Iteratively check from back
    for (int i = n - 1; i > 0; i--)
    {

        // Different numbers
        if (a[0] != a[i])
        {
            ind1 = i;
            break;
        }
    }

    int ind2 = 0;

    // Iteratively check from
    // the beginning
    for (int i = 0; i < n - 1; i++)
    {

        // Different numbers
        if (a[n - 1] != a[i])
        {
            ind2 = (n - 1 - i);
            break;
        }
    }

    return Math.max(ind1, ind2);
}

// Driver code
public static void main(String args[])
{
    int []a = { 1, 2, 3, 2, 3 };
    int n = a.length;
    System.out.println(findMaximumDiff(a, n));
}
}

// This code is contributed by Akanksha_Rai
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum difference
def findMaximumDiff(a, n):
    ind1 = 0

    # Iteratively check from back
    for i in range(n - 1, -1, -1):

        # Different numbers
        if (a[0] != a[i]):
            ind1 = i
            break

    ind2 = 0

    # Iteratively check from
    # the beginning
    for i in range(n - 1):

        # Different numbers
        if (a[n - 1] != a[i]):
            ind2 = (n - 1 - i)
            break

    return max(ind1, ind2)

# Driver code
a = [1, 2, 3, 2, 3]
n = len(a)
print(findMaximumDiff(a, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum difference
static int findMaximumDiff(int []a, int n)
{
    int ind1 = 0;

    // Iteratively check from back
    for (int i = n - 1; i > 0; i--)
    {

        // Different numbers
        if (a[0] != a[i])
        {
            ind1 = i;
            break;
        }
    }

    int ind2 = 0;

    // Iteratively check from
    // the beginning
    for (int i = 0; i < n - 1; i++)
    {

        // Different numbers
        if (a[n - 1] != a[i])
        {
            ind2 = (n - 1 - i);
            break;
        }
    }

    return Math.Max(ind1, ind2);
}

// Driver code
static void Main()
{
    int []a = { 1, 2, 3, 2, 3 };
    int n = a.Length;
    Console.WriteLine(findMaximumDiff(a, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum difference
function findMaximumDiff($a, $n)
{
    $ind1 = 0;

    // Iteratively check from back
    for ($i = $n - 1; $i > 0; $i--)
    {

        // Different numbers
        if ($a[0] != $a[$i])
        {
            $ind1 = $i;
            break;
        }
    }

    $ind2 = 0;

    // Iteratively check from
    // the beginning
    for ($i = 0; $i < $n - 1; $i++)
    {

        // Different numbers
        if ($a[$n - 1] != $a[$i])
        {
            $ind2 = ($n - 1 - $i);
            break;
        }
    }

    return max($ind1, $ind2);
}

// Driver code
$a = array( 1, 2, 3, 2, 3 );
$n = count($a);

echo findMaximumDiff($a, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the maximum difference
    function findMaximumDiff(a , n) {
        var ind1 = 0;

        // Iteratively check from back
        for (i = n - 1; i > 0; i--) {

            // Different numbers
            if (a[0] != a[i]) {
                ind1 = i;
                break;
            }
        }

        var ind2 = 0;

        // Iteratively check from
        // the beginning
        for (i = 0; i < n - 1; i++) {

            // Different numbers
            if (a[n - 1] != a[i]) {
                ind2 = (n - 1 - i);
                break;
            }
        }

        return Math.max(ind1, ind2);
    }

    // Driver code

        var a = [ 1, 2, 3, 2, 3 ];
        var n = a.length;
        document.write(findMaximumDiff(a, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
4
```