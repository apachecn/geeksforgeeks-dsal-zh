# 从阵列中拾取点，使最小距离最大化

> 原文:[https://www . geeksforgeeks . org/从阵列中拾取点，以使最小距离最大化/](https://www.geeksforgeeks.org/pick-points-from-array-such-that-minimum-distance-is-maximized/)

给定 **C** 磁体和代表 **N** 索引位置的阵列**arr【】**，其中 **C ≤ N** 。任务是将这些磁体放置在这些可用的索引处，使得两个最近的磁体之间的距离尽可能大。
**举例:**

> **输入:** C = 4，arr[] = {1，2，5，8，10，18}
> **输出:** 4
> 我们可以将 4 个磁铁放置到位置 1，5，10，18，因此最大距离最小为(dist(1，5)，dist(5，10)，dist(10，18) ) = dist(1，5) = 4。
> 这将是两个最近的磁铁之间的最大可能距离。
> **输入:** C = 3，arr[] = {5，7，11，20，23}
> **输出:** 6
> 我们可以在位置 5，11，23 放置 3 块磁铁，这样答案将是(dist(5，11)，dist(11，23) ) = dist(5，11) = 6 的最小值。

**天真的做法:**找到磁铁所有可能的位置也就是 C(n，C)个可能的方式，找到一个最大化两个磁铁之间距离的方式，其中 C(n，C)就是从 n 个给定的物体中选择 C 个物体。
**有效方法:**让 mx 为最大可能距离，因此所有大于 0 且小于 mx 的 x 也将允许放置磁体，但是对于所有大于 mx 的 y，将不可能放置磁体。因此，我们可以利用二分搜索法来寻找最大可能的距离。
因为我们的答案总是在 0 和给定的 N 个指数中的最大指数之间。因此，应用二分搜索法，找到最低值和最高值之间的中间值，比如“中间”，做一个函数，检查是否有可能放置 C 磁体，假设“中间”是最大可能距离。
整体时间复杂度为 O(nlog(n))，因为二分搜索法将采用 O(log(n))和 O(n)来检查是否可以放置所有的 C 磁体。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to place C magnets assuming mid as
// maximum possible distance
bool isPossible(int arr[], int n, int C, int mid)
{
    // Variable magnet will store count of magnets
    // that got placed and currPosition will store
    // the position of last placed magnet
    int magnet = 1, currPosition = arr[0];

    for (int i = 1; i < n; i++) {

        // If difference between current index and
        // last placed index is greater than or equal to mid
        // it will allow placing magnet to this index
        if (arr[i] - currPosition >= mid) {

            magnet++;

            // Now this index will become
            // last placed index
            currPosition = arr[i];

            // If count of magnets placed becomes C
            if (magnet == C)
                return true;
        }
    }

    // If count of placed magnet is
    // less than C then return false
    return false;
}

// Function for modified binary search
int binarySearch(int n, int C, int arr[])
{
    int lo, hi, mid, ans;

    // Sort the indices in ascending order
    sort(arr, arr + n);

    // Minimum possible distance
    lo = 0;

    // Maximum possible distance
    hi = arr[n - 1];

    ans = 0;

    // Run the loop until lo becomes
    // greater than hi
    while (lo <= hi) {

        mid = (lo + hi) / 2;

        // If not possible, decrease value of hi
        if (!isPossible(arr, n, C, mid))
            hi = mid - 1;
        else {

            // Update the answer
            ans = max(ans, mid);
            lo = mid + 1;
        }
    }

    // Return maximum possible distance
    return ans;
}

// Driver code
int main()
{
    int C = 4;
    int arr[] = { 1, 2, 5, 8, 10, 18 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << binarySearch(n, C, arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to check if it is possible
// to place C magnets assuming mid as
// maximum possible distance
static boolean isPossible(int []arr, int n,
                        int C, int mid)
{
    // Variable magnet will store count of magnets
    // that got placed and currPosition will store
    // the position of last placed magnet
    int magnet = 1, currPosition = arr[0];

    for (int i = 1; i < n; i++)
    {

        // If difference between current index and
        // last placed index is greater than or equal to mid
        // it will allow placing magnet to this index
        if (arr[i] - currPosition >= mid)
        {

            magnet++;

            // Now this index will become
            // last placed index
            currPosition = arr[i];

            // If count of magnets placed becomes C
            if (magnet == C)
                return true;
        }
    }

    // If count of placed magnet is
    // less than C then return false
    return false;
}

// Function for modified binary search
static int binarySearch(int n, int C, int []arr)
{
    int lo, hi, mid, ans;

    // Sort the indices in ascending order
    Arrays.sort(arr);

    // Minimum possible distance
    lo = 0;

    // Maximum possible distance
    hi = arr[n - 1];

    ans = 0;

    // Run the loop until lo becomes
    // greater than hi
    while (lo <= hi)
    {

        mid = (lo + hi) / 2;

        // If not possible, decrease value of hi
        if (!isPossible(arr, n, C, mid))
            hi = mid - 1;
        else
        {

            // Update the answer
            ans = Math.max(ans, mid);
            lo = mid + 1;
        }
    }

    // Return maximum possible distance
    return ans;
}

// Driver code
public static void main(String args[])
{
    int C = 4;
    int []arr = { 1, 2, 5, 8, 10, 18 };
    int n = arr.length;
    System.out.println(binarySearch(n, C, arr));
}
}

// This code is contributed by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to check if it is possible
# to place C magnets assuming mid as
# maximum possible distance
def isPossible(arr, n, C, mid):

    # Variable magnet will store count of
    # magnets that got placed and
    # currPosition will store the position
    # of last placed magnet
    magnet = 1
    currPosition = arr[0]

    for i in range(1, n):

        # If difference between current index
        # and last placed index is greater than
        # or equal to mid it will allow placing
        # magnet to this index
        if (arr[i] - currPosition >= mid):
            magnet += 1

            # Now this index will become
            # last placed index
            currPosition = arr[i]

            # If count of magnets placed becomes C
            if (magnet == C):
                return True

    # If count of placed magnet is
    # less than C then return false
    return False

# Function for modified binary search
def binarySearch(n, C, arr):

    # Sort the indices in ascending order
    arr.sort(reverse = False)

    # Minimum possible distance
    lo = 0

    # Maximum possible distance
    hi = arr[n - 1]
    ans = 0

    # Run the loop until lo becomes
    # greater than hi
    while (lo <= hi):
        mid = int((lo + hi) / 2)

        # If not possible, decrease value of hi
        if (isPossible(arr, n, C, mid) == False):
            hi = mid - 1
        else:

            # Update the answer
            ans = max(ans, mid)
            lo = mid + 1

    # Return maximum possible distance
    return ans

# Driver code
if __name__ == '__main__':
    C = 4
    arr = [1, 2, 5, 8, 10, 18]
    n = len(arr)
    print(binarySearch(n, C, arr))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function to check if it is possible
// to place C magnets assuming mid as
// maximum possible distance
static bool isPossible(int []arr, int n,
                        int C, int mid)
{
    // Variable magnet will store count of magnets
    // that got placed and currPosition will store
    // the position of last placed magnet
    int magnet = 1, currPosition = arr[0];

    for (int i = 1; i < n; i++)
    {

        // If difference between current index and
        // last placed index is greater than or equal to mid
        // it will allow placing magnet to this index
        if (arr[i] - currPosition >= mid)
        {

            magnet++;

            // Now this index will become
            // last placed index
            currPosition = arr[i];

            // If count of magnets placed becomes C
            if (magnet == C)
                return true;
        }
    }

    // If count of placed magnet is
    // less than C then return false
    return false;
}

// Function for modified binary search
static int binarySearch(int n, int C, int []arr)
{
    int lo, hi, mid, ans;

    // Sort the indices in ascending order
    Array.Sort(arr);

    // Minimum possible distance
    lo = 0;

    // Maximum possible distance
    hi = arr[n - 1];

    ans = 0;

    // Run the loop until lo becomes
    // greater than hi
    while (lo <= hi)
    {

        mid = (lo + hi) / 2;

        // If not possible, decrease value of hi
        if (!isPossible(arr, n, C, mid))
            hi = mid - 1;
        else
        {

            // Update the answer
            ans = Math.Max(ans, mid);
            lo = mid + 1;
        }
    }

    // Return maximum possible distance
    return ans;
}

// Driver code
static void Main()
{
    int C = 4;
    int []arr = { 1, 2, 5, 8, 10, 18 };
    int n = arr.Length;
    Console.WriteLine(binarySearch(n, C, arr));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to check if it is possible
// to place C magnets assuming mid as
// maximum possible distance
function isPossible($arr, $n, $C, $mid)
{
    // Variable magnet will store count of magnets
    // that got placed and currPosition will store
    // the position of last placed magnet
    $magnet = 1; $currPosition = $arr[0];

    for ($i = 1; $i < $n; $i++)
    {

        // If difference between current index and
        // last placed index is greater than or equal to mid
        // it will allow placing magnet to this index
        if ($arr[$i] - $currPosition >= $mid)
        {
            $magnet++;

            // Now this index will become
            // last placed index
            $currPosition = $arr[$i];

            // If count of magnets placed becomes C
            if ($magnet == $C)
                return true;
        }
    }

    // If count of placed magnet is
    // less than C then return false
    return false;
}

// Function for modified binary search
function binarySearch($n, $C, $arr)
{

    // Sort the indices in ascending order
    sort($arr, 0);

    // Minimum possible distance
    $lo = 0;

    // Maximum possible distance
    $hi = $arr[$n - 1];

    $ans = 0;

    // Run the loop until lo becomes
    // greater than hi
    while ($lo <= $hi)
    {
        $mid = ($lo + $hi) / 2;

        // If not possible, decrease value of hi
        if (!isPossible($arr, $n, $C, $mid))
            $hi = $mid - 1;
        else
        {

            // Update the answer
            $ans = max($ans, $mid);
            $lo = $mid + 1;
        }
    }

    // Return maximum possible distance
    return $ans;
}

// Driver code
$C = 4;
$arr = array(1, 2, 5, 8, 10, 18);
$n = sizeof($arr);
echo binarySearch($n, $C, $arr) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to check if it is possible
// to place C magnets assuming mid as
// maximum possible distance
function isPossible(arr, n, C, mid)
{
    // Variable magnet will store count of magnets
    // that got placed and currPosition will store
    // the position of last placed magnet
    let magnet = 1; currPosition = arr[0];

    for (let i = 1; i < n; i++)
    {

        // If difference between current index and
        // last placed index is greater than or equal to mid
        // it will allow placing magnet to this index
        if (arr[i] - currPosition >= mid)
        {
            magnet++;

            // Now this index will become
            // last placed index
            currPosition = arr[i];

            // If count of magnets placed becomes C
            if (magnet == C)
                return true;
        }
    }

    // If count of placed magnet is
    // less than C then return false
    return false;
}

// Function for modified binary search
function binarySearch(n, C, arr)
{

    // Sort the indices in ascending order
    arr.sort((a, b) => a - b);

    // Minimum possible distance
    let lo = 0;

    // Maximum possible distance
    let hi = arr[n - 1];

    let ans = 0;

    // Run the loop until lo becomes
    // greater than hi
    while (lo <= hi)
    {
        mid = Math.floor((lo + hi) / 2);

        // If not possible, decrease value of hi
        if (!isPossible(arr, n, C, mid))
            hi = mid - 1;
        else
        {

            // Update the answer
            ans = Math.max(ans, mid);
            lo = mid + 1;
        }
    }

    // Return maximum possible distance
    return ans;
}

// Driver code
let C = 4;
let arr = new Array(1, 2, 5, 8, 10, 18);
let n = arr.length;

document.write(binarySearch(n, C, arr) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n * log(n))
**辅助空间:** O(1)