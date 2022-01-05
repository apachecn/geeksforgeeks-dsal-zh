# 检查是否可以创建给定 n 条边的多边形

> 原文:[https://www . geeksforgeeks . org/check-如果有可能创建一个给定 n 边的多边形/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-create-a-polygon-with-given-n-sides/)

给定一个数组 **arr[]** ，该数组包含可能形成也可能不形成多边形的 **n** 条边的长度。任务是确定是否有可能形成一个具有所有给定边的多边形。如有可能，打印**是**否则打印**否**。
**举例:**

> **输入:** arr[] = {2，3，4}
> **输出:**是
> **输入:** arr[] = {3，4，9，2}
> **输出:**否

**方法:**为了创建给定 ***n*** 边的多边形，多边形的边必须满足某个属性。

> **属性:**每条给定边的长度必须小于其他剩余边的总和。

在给定的边中找到最大的边。然后，检查它是否小于其他边的总和。如果较小，则打印**是**否则打印**否**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is possible
// to form a polygon with the given sides
bool isPossible(int a[], int n)
{

    // Sum stores the sum of all the sides
    // and maxS stores the length of
    // the largest side
    int sum = 0, maxS = 0;
    for (int i = 0; i < n; i++) {
        sum += a[i];
        maxS = max(a[i], maxS);
    }

    // If the length of the largest side
    // is less than the sum of the
    // other remaining sides
    if ((sum - maxS) > maxS)
        return true;

    return false;
}

// Driver code
int main()
{
    int a[] = { 2, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    if (isPossible(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if it is possible
    // to form a polygon with the given sides
    static boolean isPossible(int a[], int n)
    {
        // Sum stores the sum of all the sides
        // and maxS stores the length of
        // the largest side
        int sum = 0, maxS = 0;
        for (int i = 0; i < n; i++) {
            sum += a[i];
            maxS = Math.max(a[i], maxS);
        }

        // If the length of the largest side
        // is less than the sum of the
        // other remaining sides
        if ((sum - maxS) > maxS)
            return true;

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 3, 4 };
        int n = a.length;

        if (isPossible(a, n))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## 计算机编程语言

```
# Python 3 implementation of the approach

# Function to check whether
# it is possible to create a
# polygon with given sides length
def isPossible(a, n):
    # Sum stores the sum of all the sides
    # and maxS stores the length of
    # the largest side
    sum = 0
    maxS = 0
    for i in range(n):
        sum += a[i]
        maxS = max(a[i], maxS)

    # If the length of the largest side
    # is less than the sum of the
    # other remaining sides
    if ((sum - maxS) > maxS):
        return True

    return False

# Driver code
a =[2, 3, 4]
n = len(a)

if(isPossible(a, n)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function that returns true if it is possible
    // to form a polygon with the given sides
    static bool isPossible(int[] a, int n)
    {
        // Sum stores the sum of all the sides
        // and maxS stores the length of
        // the largest side
        int sum = 0, maxS = 0;
        for (int i = 0; i < n; i++) {
            sum += a[i];
            maxS = Math.Max(a[i], maxS);
        }

        // If the length of the largest side
        // is less than the sum of the
        // other remaining sides
        if ((sum - maxS) > maxS)
            return true;

        return false;
    }

    // Driver code
    static void Main()
    {
        int[] a = { 2, 3, 4 };
        int n = a.Length;

        if (isPossible(a, n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if it is possible
// to form a polygon with the given sides
function isPossible($a, $n)
{
    // Sum stores the sum of all the sides
    // and maxS stores the length of
    // the largest side
    $sum = 0;
    $maxS = 0;
    for ($i = 0; $i < $n; $i++) {
        $sum += $a[$i];
        $maxS = max($a[$i], $maxS);
    }

    // If the length of the largest side
    // is less than the sum of the
    // other remaining sides
    if (($sum - $maxS) > $maxS)
        return true;

    return false;
}

// Driver code
$a = array(2, 3, 4);
$n = count($a);

if(isPossible($a, $n))
    echo "Yes";
else
    echo "No";
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if it is possible
// to form a polygon with the given sides
function isPossible( a, n)
{

    // Sum stores the sum of all the sides
    // and maxS stores the length of
    // the largest side
    let sum = 0, maxS = 0;
    for (let i = 0; i < n; i++) {
        sum += a[i];
        maxS = Math.max(a[i], maxS);
    }

    // If the length of the largest side
    // is less than the sum of the
    // other remaining sides
    if ((sum - maxS) > maxS)
        return true;

    return false;
}

    // Driver Code

    let a = [ 2, 3, 4 ];
    let n = a.length;

    if (isPossible(a, n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```