# 检查是否可以重新分配数组

> 原文:[https://www . geeksforgeeks . org/check-如果有可能重新分发阵列/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-redistribute-the-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是检查是否有可能重新分配数组，使得对于每个 **1 ≤ i ≤ N** (基于 1 的索引) **arr[i] = i** 。重新分配数组意味着数组中的所有元素都可以转换为任何其他元素，但是结果数组的总和必须等于原始数组的总和。
**举例:**

> **输入:** arr[] = {7，4，1，1，2}
> **输出:**是
> 7+4+1+1+2 = 15
> 1+2+3+4+5 = 15
> **输入:** arr[] = {1，1，1，1}
> **输出:**否
> 1+1+1+1 = 4
> 1+2+3+4 = 0

**方法:**给出修改后数组的和一定不变。因此，计算给定数组的和，为了使数组具有 **1，2，3，…，N** 的形式，数组元素的和必须是 **(N * (N + 1)) / 2** 。否则，是不可能的。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the
// array can be redistributed to
// the form 1, 2, 3, ..., N
bool canRedistribute(int* a, int n)
{

    // Calculate the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    // If can be redistributed
    if (sum == (n * (n + 1)) / 2)
        return true;

    return false;
}

// Driver code
int main()
{
    int a[] = { 7, 4, 1, 1, 2 };
    int n = sizeof(a) / sizeof(int);

    if (canRedistribute(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that returns true if the
// array can be redistributed to
// the form 1, 2, 3, ..., N
static boolean canRedistribute(int []a, int n)
{

    // Calculate the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    // If can be redistributed
    if (sum == (n * (n + 1)) / 2)
        return true;

    return false;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 7, 4, 1, 1, 2 };
    int n = a.length;

    if (canRedistribute(a, n))
        System.out.print( "Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if the
# array can be redistributed to
# the form 1, 2, 3, ..., N
def canRedistribute(a, n):

    # Calculate the sum of the array elements
    sum = 0;
    for i in range(n):
        sum += a[i];

    # If can be redistributed
    if (sum == (n * (n + 1)) / 2):
        return True;

    return False;

# Driver code

a = [7, 4, 1, 1, 2 ];
n = len(a);

if (canRedistribute(a, n)):
    print("Yes");
else:
    print("No");

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the
// array can be redistributed to
// the form 1, 2, 3, ..., N
static Boolean canRedistribute(int []a, int n)
{

    // Calculate the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    // If can be redistributed
    if (sum == (n * (n + 1)) / 2)
        return true;

    return false;
}

// Driver code
public static void Main (String[] args)
{
    int []a = { 7, 4, 1, 1, 2 };
    int n = a.Length;

    if (canRedistribute(a, n))
        Console.WriteLine( "Yes");
    else
        Console.WriteLine("No");
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
 //Javascript implementation of the approach

// Function that returns true if the
// array can be redistributed to
// the form 1, 2, 3, ..., N
function canRedistribute(a, n)
{

    // Calculate the sum of the array elements
    var sum = 0;
    for (var i = 0; i < n; i++)
        sum += a[i];

    // If can be redistributed
    if (sum == (n * (n + 1)) / 2)
        return true;

    return false;
}

var a = [ 7, 4, 1, 1, 2 ];
var n = a.length;

    if (canRedistribute(a, n))
        document.write("Yes");
    else
       document.write( "No");

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```