# 检查给定的数组是否可以通过给定次数的给定操作减少到零

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数组可以用给定的操作执行给定的次数来降为零/](https://www.geeksforgeeks.org/check-if-the-given-array-can-be-reduced-to-zeros-with-the-given-operation-performed-given-number-of-times/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** ，任务是找出如果给定的运算被精确地应用 **K** 次，给定的数组元素是否可以被置为 0。在一次操作中，将从数组的所有非零元素中减去数组中的最小元素。
**举例:**

> **输入:** arr[] = {1，1，2，3}，K = 3
> **输出:**是
> K = 1 - > arr[] = {0，0，1，2}
> K = 2 - > arr[] = {0，0，0，1}
> K = 3 - > arr[] = {0，0，0，0}
> **输入:** arr[] = {11，2，3

**进场:**

*   这里主要观察的是，最小次数在每次操作中并不重要，假设 **X** 是最小次数，那么当前操作中 **X** 的所有出现次数都将是 **0** ，其他元素将减少 **X** 。
*   我们可以得出结论，在同一操作中，所有相同的元素都将为 0。
*   所以说在 **Q** 运算中整个数组变成了 **0** ，它等于数组中唯一元素的个数。
*   如果 **Q = K** 那么答案是**是**否则打印**否**。
*   使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)可以获得唯一元素的数量。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the array
// can be reduced to 0s with the given
// operation performed given number of times
bool check(int arr[], int N, int K)
{
    // Set to store unique elements
    set<int> unique;

    // Add every element of the array
    // to the set
    for (int i = 0; i < N; i++)
        unique.insert(arr[i]);

    // Count of all the unique elements
    // in the array
    if (unique.size() == K)
        return true;
    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;
    if (check(arr, N, K))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if the array
// can be reduced to 0s with the given
// operation performed given number of times
static boolean check(int arr[], int N, int K)
{
    // Set to store unique elements
    HashSet<Integer> unique = new HashSet<Integer>();

    // Add every element of the array
    // to the set
    for (int i = 0; i < N; i++)
        unique.add(arr[i]);

    // Count of all the unique elements
    // in the array
    if (unique.size() == K)
        return true;
    return false;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 2, 3 };
    int N = arr.length;
    int K = 3;
    if (check(arr, N, K))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the array
# can be reduced to 0s with the given
# operation performed given number of times
def check(arr, N, K):

    # Set to store unique elements
    unique = dict()

    # Add every element of the array
    # to the set
    for i in range(N):
        unique[arr[i]] = 1

    # Count of all the unique elements
    # in the array
    if len(unique) == K:
        return True
    return False

# Driver code
arr = [1, 1, 2, 3]
N = len(arr)
K = 3
if (check(arr, N, K) == True):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns true if the array
// can be reduced to 0s with the given
// operation performed given number of times
public static bool check(int[] arr, int N, int K)
{
    // Set to store unique elements
    HashSet<int> unique = new HashSet<int>();

    // Add every element of the array
    // to the set
    for (int i = 0; i < N; i++)
    {
        unique.Add(arr[i]);
    }

    // Count of all the unique elements
    // in the array
    if (unique.Count == K)
    {
        return true;
    }
    return false;
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = new int[] {1, 1, 2, 3};
    int N = arr.Length;
    int K = 3;
    if (check(arr, N, K))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by shrikanth13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if the array
// can be reduced to 0s with the given
// operation performed given number of times
function check( &$arr, $N, $K)
{

    // Add in Set only unique elements
    $unique = array_unique($arr);

    // Count of all the unique elements
    // in the array
    if (count($unique) == $K)
        return true;
    return false;
}

// Driver code
$arr = array( 1, 1, 2, 3 );
$N = count($arr);
$K = 3;
if (check($arr, $N, $K))
    echo "Yes";
else
    echo "No";

// This code has been contributed
// by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if the array
// can be reduced to 0s with the given
// operation performed given number of times
function check(arr, N, K)
{
    // Set to store unique elements
    var unique = new Set();

    // Add every element of the array
    // to the set
    for (var i = 0; i < N; i++)
        unique.add(arr[i]);

    // Count of all the unique elements
    // in the array
    if (unique.size == K)
        return true;
    return false;
}

// Driver code
var arr = [1, 1, 2, 3];
var N = arr.length;
var K = 3;
if (check(arr, N, K))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```