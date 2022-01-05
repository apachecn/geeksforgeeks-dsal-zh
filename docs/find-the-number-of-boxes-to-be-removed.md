# 找到需要拆除的箱子数量

> 原文:[https://www . geesforgeks . org/find-要移除的箱子数量/](https://www.geeksforgeeks.org/find-the-number-of-boxes-to-be-removed/)

给定一个数组 arr[]表示一系列的盒子堆，其中每个盒子都有 1 个单位的相同高度。假设你在第一堆的顶部，需要从最左边到最右边从每一堆开始移动到达地面。
**约束** :

*   当下一堆箱子的高度等于或小于他们站立的那堆箱子的高度时，可以从当前的箱子堆移动到下一个箱子堆。
*   人们也可能会遇到一些桩的高度大于他们所站的桩。因此，他们需要从那堆箱子中取出一些箱子才能继续前进。因此，任务是告诉在到达地面的过程中需要从每一堆中移走的箱子的总数(如果需要的话)。

给出了所有桩的高度。假设你站在第一堆上。打印要移除的盒子总数。
**例** :

> **输入** : arr[] = {3，3，2，4，1}
> **输出** : 2
> **说明**:拆箱后桩的高度将为{3，3，2，2，1}
> 我们目前站在高度 3 的第一桩。
> **第一步**:我们可以移动到第二堆，因为它的高度等于当前堆的高度。
> **第二步**:我们可以移动到高度 2 的第三堆，因为它不到 3。
> **第三步**:我们不能从第三堆到第四堆(高度 4)，所以我们需要从第四堆移走 2 个盒子，使其高度等于 2。
> **第四步**:我们可以轻松移动到最后一堆，因为它的高度是 1，比高度 2 的第四堆的高度要小(通过上一步移除 2 个盒子)。
> **输入** : arr[] = {5，6，7，1}
> **输出** : 3
> **说明**:拆箱后桩的高度将为{5，5，5，1}
> 我们目前站在第一桩的高度为 5。
> **第一步**:因为第二堆的高度比较大，所以不能移动到第二堆。所以，我们去掉 1 个盒子，使它的高度等于 5，然后我们向前移动。
> **第二步**:我们无法移动到 7 高度的第三堆，所以我们从里面拿走了 2 个箱子。
> **第三步**:我们可以轻松移动到最后一堆，因为它的高度是 1，比高度 5 的第三堆的高度要小。

想法是从左边开始遍历数组，每次向前移动之前，比较当前堆和前一堆的高度。如果当前堆的高度大于前一堆，则按两个高度之差递增计数，否则在数组中向前移动。
以下是上述方法的实现:

## C++

```
// C++ program to find the number of
// boxes to be removed
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// boxes to be removed
int totalBoxesRemoved(int arr[], int n)
{
    int count = 0;

    // Store height of previous pile
    int prev = arr[0];

    // Start traversing the array
    for (int i = 1; i < n; i++) {
        // if height of current pile is greater
        // than previous pile
        if (arr[i] > prev) {
            // Increment count by difference
            // of two heights
            count += (arr[i] - prev);

            // Update current height
            arr[i] = prev;

            // Update prev for next iteration
            prev = arr[i];
        }
        else {
            // Update prev for next iteration
            prev = arr[i];
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 7, 3, 2, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << totalBoxesRemoved(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of
// boxes to be removed
import java.io.*;

class GFG {

// Function to find the number of
// boxes to be removed
static int totalBoxesRemoved(int arr[], int n)
{
    int count = 0;

    // Store height of previous pile
    int prev = arr[0];

    // Start traversing the array
    for (int i = 1; i < n; i++) {
        // if height of current pile is greater
        // than previous pile
        if (arr[i] > prev) {
            // Increment count by difference
            // of two heights
            count += (arr[i] - prev);

            // Update current height
            arr[i] = prev;

            // Update prev for next iteration
            prev = arr[i];
        }
        else {
            // Update prev for next iteration
            prev = arr[i];
        }
    }

    return count;
}

    // Driver code
    public static void main (String[] args) {
            int arr[] = { 5, 4, 7, 3, 2, 1 };

    int n = arr.length;

    System.out.println(totalBoxesRemoved(arr, n));
    }
}

// This code is contributed
// by inder_verma..
```

## 蟒蛇 3

```
# Python3 program to find the
# number of boxes to be removed

# Function to find the number
# of boxes to be removed
def totalBoxesRemoved(arr, n):

    count = 0

    # Store height of previous pile
    prev = arr[0]

    # Start traversing the array
    for i in range(1, n):

        # if height of current pile
        # is greater than previous pile
        if (arr[i] > prev) :

            # Increment count by
            # difference of two heights
            count += (arr[i] - prev)

            # Update current height
            arr[i] = prev

            # Update prev for next
            # iteration
            prev = arr[i]

        else :
            # Update prev for next
            # iteration
            prev = arr[i]

    return count

# Driver code
arr = [ 5, 4, 7, 3, 2, 1 ]

n = len(arr)

print(totalBoxesRemoved(arr, n))

# This code is contributed
# by Yatin Gupta
```

## C#

```
// C# program to find the number of
// boxes to be removed
using System;

class GFG {

// Function to find the number of
// boxes to be removed
static int totalBoxesRemoved(int []arr, int n)
{
    int count = 0;

    // Store height of previous pile
    int prev = arr[0];

    // Start traversing the array
    for (int i = 1; i < n; i++) {
        // if height of current pile is greater
        // than previous pile
        if (arr[i] > prev) {
            // Increment count by difference
            // of two heights
            count += (arr[i] - prev);

            // Update current height
            arr[i] = prev;

            // Update prev for next iteration
            prev = arr[i];
        }
        else {
            // Update prev for next iteration
            prev = arr[i];
        }
    }

    return count;
}

        // Driver code
    public static void Main () {
            int []arr = { 5, 4, 7, 3, 2, 1 };

    int n = arr.Length;

    Console.WriteLine(totalBoxesRemoved(arr, n));
    }
}

// This code is contributed
// by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number
// of boxes to be removed

// Function to find the number
// of boxes to be removed
function totalBoxesRemoved($arr, $n)
{
    $count = 0;

    // Store height of previous pile
    $prev = $arr[0];

    // Start traversing the array
    for ($i = 1; $i <$n; $i++)
    {
        // if height of current pile is
        // greater than previous pile
        if ($arr[$i] > $prev)
        {
            // Increment count by difference
            // of two heights
            $count += ($arr[$i] - $prev);

            // Update current height
            $arr[$i] = $prev;

            // Update prev for next iteration
            $prev = $arr[$i];
        }
        else
        {
            // Update prev for next iteration
            $prev = $arr[$i];
        }
    }

    return $count;
}

// Driver code
$arr = array( 5, 4, 7, 3, 2, 1 );

$n = count($arr);

echo totalBoxesRemoved($arr, $n);

// This code is contributed
// by shs
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number of
// boxes to be removed

// Function to find the number of
// boxes to be removed
function totalBoxesRemoved(arr, n)
{
    var count = 0;

    // Store height of previous pile
    var prev = arr[0];

    // Start traversing the array
    for (var i = 1; i < n; i++) {
        // if height of current pile is greater
        // than previous pile
        if (arr[i] > prev) {
            // Increment count by difference
            // of two heights
            count += (arr[i] - prev);

            // Update current height
            arr[i] = prev;

            // Update prev for next iteration
            prev = arr[i];
        }
        else {
            // Update prev for next iteration
            prev = arr[i];
        }
    }

    return count;
}

// Driver code
var arr = [5, 4, 7, 3, 2, 1 ];
var n = arr.length;
document.write( totalBoxesRemoved(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(N)，其中 N 为桩总数。
**辅助空间:** O(1)