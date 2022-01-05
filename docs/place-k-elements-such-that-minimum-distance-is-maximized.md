# 放置 k 个元素，使最小距离最大化

> 原文:[https://www . geesforgeks . org/place-k-elements-so-最小距离最大化/](https://www.geeksforgeeks.org/place-k-elements-such-that-minimum-distance-is-maximized/)

给定一个代表直线上 n 个位置的数组。从数组中找出 k(其中 k <= n)个元素，使得任意两个(k 个点中的连续点)之间的最小距离最大化。

**示例:**

```
Input : arr[] = {1, 2, 8, 4, 9}
            k = 3
Output : 3
Largest minimum distance = 3
3 elements arranged at positions 1, 4 and 8, 
Resulting in a minimum distance of 3

Input  : arr[] = {1, 2, 7, 5, 11, 12}
             k = 3
Output : 5
Largest minimum distance = 5
3 elements arranged at positions 1, 7 and 12, 
resulting in a minimum distance of 5 (between
7 and 12)
```

一个**天真的解决方案**是考虑大小为 3 的所有子集，找到每个子集的最小距离。最后，返回所有最小距离中最大的一个。

一个**高效的解决方案**基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。我们首先对数组进行排序。现在我们知道最大可能值结果是 arr[n-1]–arr[0](对于 k = 2)。对于给定的 k，我们对最大结果做一个二分搜索法，我们从最大可能结果的中间开始。如果中间是可行解，我们在中间的右半部分搜索。否则我们搜索的是左半部分。为了检查可行性，我们在给定的中间距离下放置 k 个元素。

## C++

```
// C++ program to find largest minimum distance
// among k points.
#include <bits/stdc++.h>

using namespace std;

// Returns true if it is possible to arrange
// k elements of arr[0..n-1] with minimum distance
// given as mid.
bool isFeasible(int mid, int arr[], int n, int k)
{
    // Place first element at arr[0] position
    int pos = arr[0];

    // Initialize count of elements placed.
    int elements = 1;

    // Try placing k elements with minimum
    // distance mid.
    for (int i = 1; i < n; i++) {
        if (arr[i] - pos >= mid) {
            // Place next element if its
            // distance from the previously
            // placed element is greater
            // than current mid
            pos = arr[i];
            elements++;

            // Return if all elements are placed
            // successfully
            if (elements == k)
                return true;
        }
    }
    return 0;
}

// Returns largest minimum distance for k elements
// in arr[0..n-1]. If elements can't be placed,
// returns -1.
int largestMinDist(int arr[], int n, int k)
{
    // Sort the positions
    sort(arr, arr + n);

    // Initialize result.
    int res = -1;

    // Consider the maximum possible distance
    //here we are using right value as highest distance difference,
      //so we remove some extra checks
    int left = 1, right = arr[n - 1];

    // left is initialized with 1 and not with arr[0]
    // because, minimum distance between each element
    // can be one and not arr[0]. consider this example:
    // arr[] = {9,12} and you have to place 2 element
    // then left = arr[0] will force the function to
    // look the answer between range arr[0] to arr[n-1],
    // i.e 9 to 12, but the answer is 3 so It is required
    // that you initialize the left with 1

    // Do binary search for largest minimum distance
    while (left < right) {
        int mid = (left + right) / 2;

        // If it is possible to place k elements
        // with minimum distance mid, search for
        // higher distance.
        if (isFeasible(mid, arr, n, k)) {
            // Change value of variable max to mid iff
            // all elements can be successfully placed
            res = max(res, mid);
            left = mid + 1;
        }

        // If not possible to place k elements, search
        // for lower distance
        else
            right = mid;
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 8, 4, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    cout << largestMinDist(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest
// minimum distance among k points.
import java.util.Arrays;

class GFG {
    // Returns true if it is possible to
    // arrange k elements of arr[0..n-1]
    // with minimum distance given as mid.
    static boolean isFeasible(int mid, int arr[], int n,
                              int k)
    {
        // Place first element at arr[0] position
        int pos = arr[0];

        // Initialize count of elements placed.
        int elements = 1;

        // Try placing k elements with minimum
        // distance mid.
        for (int i = 1; i < n; i++) {
            if (arr[i] - pos >= mid) {
                // Place next element if its
                // distance from the previously
                // placed element is greater
                // than current mid
                pos = arr[i];
                elements++;

                // Return if all elements are
                // placed successfully
                if (elements == k)
                    return true;
            }
        }
        return false;
    }

    // Returns largest minimum distance for
    // k elements in arr[0..n-1]. If elements
    // can't be placed, returns -1.
    static int largestMinDist(int arr[], int n, int k)
    {
        // Sort the positions
        Arrays.sort(arr);

        // Initialize result.
        int res = -1;

        // Consider the maximum possible distance
        int left = 1, right = arr[n - 1];

        // left is initialized with 1 and not with arr[0]
        // because, minimum distance between each element
        // can be one and not arr[0]. consider this example:
        // arr[] = {9,12} and you have to place 2 element
        // then left = arr[0] will force the function to
        // look the answer between range arr[0] to arr[n-1],
        // i.e 9 to 12, but the answer is 3 so It is
        // required that you initialize the left with 1

        // Do binary search for largest
        // minimum distance
        while (left < right) {
            int mid = (left + right) / 2;

            // If it is possible to place k
            // elements with minimum distance mid,
            // search for higher distance.
            if (isFeasible(mid, arr, n, k)) {
                // Change value of variable max to
                // mid if all elements can be
                // successfully placed
                res = Math.max(res, mid);
                left = mid + 1;
            }

            // If not possible to place k elements,
            // search for lower distance
            else
                right = mid;
        }

        return res;
    }

    // driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 8, 4, 9 };
        int n = arr.length;
        int k = 3;
        System.out.print(largestMinDist(arr, n, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to find largest minimum
# distance among k points.

# Returns true if it is possible to arrange
# k elements of arr[0..n-1] with minimum
# distance given as mid.

def isFeasible(mid, arr, n, k):

    # Place first element at arr[0] position
    pos = arr[0]

    # Initialize count of elements placed.
    elements = 1

    # Try placing k elements with minimum
    # distance mid.
    for i in range(1, n, 1):
        if (arr[i] - pos >= mid):

            # Place next element if its distance
            # from the previously placed element
            # is greater than current mid
            pos = arr[i]
            elements += 1

            # Return if all elements are placed
            # successfully
            if (elements == k):
                return True
    return 0

# Returns largest minimum distance for k elements
# in arr[0..n-1]. If elements can't be placed,
# returns -1.

def largestMinDist(arr, n, k):

    # Sort the positions
    arr.sort(reverse=False)

    # Initialize result.
    res = -1

    # Consider the maximum possible distance
    left = 1
    right = arr[n - 1]

    # left is initialized with 1 and not with arr[0]
    # because, minimum distance between each element
    # can be one and not arr[0]. consider this example:
    # arr[] = {9,12} and you have to place 2 element
    # then left = arr[0] will force the function to
    # look the answer between range arr[0] to arr[n-1],
    # i.e 9 to 12, but the answer is 3 so It is required
    # that you initialize the left with 1

    # Do binary search for largest
    # minimum distance
    while (left < right):
        mid = (left + right) / 2

        # If it is possible to place k elements
        # with minimum distance mid, search for
        # higher distance.
        if (isFeasible(mid, arr, n, k)):

            # Change value of variable max to mid iff
            # all elements can be successfully placed
            res = max(res, mid)
            left = mid + 1

        # If not possible to place k elements,
        # search for lower distance
        else:
            right = mid

    return res

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 8, 4, 9]
    n = len(arr)
    k = 3
    print(largestMinDist(arr, n, k))

# This code is contributed by
# Sanjit_prasad
```

## C#

```
// C# program to find largest
// minimum distance among k points.
using System;

public class GFG {

    // Returns true if it is possible to
    // arrange k elements of arr[0..n-1]
    // with minimum distance given as mid.
    static bool isFeasible(int mid, int[] arr, int n, int k)
    {

        // Place first element at arr[0]
        // position
        int pos = arr[0];

        // Initialize count of elements placed.
        int elements = 1;

        // Try placing k elements with minimum
        // distance mid.
        for (int i = 1; i < n; i++) {
            if (arr[i] - pos >= mid) {

                // Place next element if its
                // distance from the previously
                // placed element is greater
                // than current mid
                pos = arr[i];
                elements++;

                // Return if all elements are
                // placed successfully
                if (elements == k)
                    return true;
            }
        }

        return false;
    }

    // Returns largest minimum distance for
    // k elements in arr[0..n-1]. If elements
    // can't be placed, returns -1.
    static int largestMinDist(int[] arr, int n, int k)
    {

        // Sort the positions
        Array.Sort(arr);

        // Initialize result.
        int res = -1;

        // Consider the maximum possible
        // distance
        int left = 1, right = arr[n - 1];

        // left is initialized with 1 and not with arr[0]
        // because, minimum distance between each element
        // can be one and not arr[0]. consider this example:
        // arr[] = {9,12} and you have to place 2 element
        // then left = arr[0] will force the function to
        // look the answer between range arr[0] to arr[n-1],
        // i.e 9 to 12, but the answer is 3 so It is
        // required that you initialize the left with 1

        // Do binary search for largest
        // minimum distance
        while (left < right) {
            int mid = (left + right) / 2;

            // If it is possible to place k
            // elements with minimum distance
            // mid, search for higher distance.
            if (isFeasible(mid, arr, n, k)) {
                // Change value of variable
                // max to mid if all elements
                // can be successfully placed
                res = Math.Max(res, mid);
                left = mid + 1;
            }

            // If not possible to place k
            // elements, search for lower
            // distance
            else
                right = mid;
        }

        return res;
    }

    // driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 8, 4, 9 };
        int n = arr.Length;
        int k = 3;

        Console.WriteLine(largestMinDist(arr, n, k));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest
// minimum distance among k points.

// Returns true if it is possible
// to arrange k elements of
// arr[0..n-1] with minimum
// distance given as mid.
function isFeasible($mid, $arr,
                    $n, $k)
{
    // Place first element
    // at arr[0] position
    $pos = $arr[0];

    // Initialize count of
    // elements placed.
    $elements = 1;

    // Try placing k elements
    // with minimum distance mid.
    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i] - $pos >= $mid)
        {
            // Place next element if
            // its distance from the
            // previously placed
            // element is greater
            // than current mid
            $pos = $arr[$i];
            $elements++;

            // Return if all elements
            // are placed successfully
            if ($elements == $k)
            return true;
        }
    }
    return 0;
}

// Returns largest minimum
// distance for k elements
// in arr[0..n-1]. If elements
// can't be placed, returns -1.
function largestMinDist($arr, $n, $k)
{
    // Sort the positions
    sort($arr);

    // Initialize result.
    $res = -1;

    // Consider the maximum
    // possible distance
    $left = 1;
    $right = $arr[$n - 1];

    // left is initialized with 1 and not with arr[0]
    // because, minimum distance between each element
    // can be one and not arr[0]. consider this example:
    // arr[] = {9,12} and you have to place 2 element
    // then left = arr[0] will force the function to
    // look the answer between range arr[0] to arr[n-1],
    // i.e 9 to 12, but the answer is 3 so It is required
    // that you initialize the left with 1

    // Do binary search for
    // largest minimum distance
    while ($left < $right)
    {
        $mid = ($left + $right) / 2;

        // If it is possible to place
        // k elements with minimum
        // distance mid, search for
        // higher distance.
        if (isFeasible($mid, $arr,
                       $n, $k))
        {
            // Change value of variable
            // max to mid iff all elements
            // can be successfully placed
            $res = max($res, $mid);
            $left = $mid + 1;
        }

        // If not possible to place
        // k elements, search for
        // lower distance
        else
            $right = $mid;
    }

    return $res;
}

// Driver Code
$arr = array(1, 2, 8, 4, 9);
$n = sizeof($arr);
$k = 3;
echo largestMinDist($arr, $n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript program to find largest
    // minimum distance among k points.

    // Returns true if it is possible to
    // arrange k elements of arr[0..n-1]
    // with minimum distance given as mid.
    function isFeasible(mid, arr, n, k)
    {

        // Place first element at arr[0]
        // position
        let pos = arr[0];

        // Initialize count of elements placed.
        let elements = 1;

        // Try placing k elements with minimum
        // distance mid.
        for (let i = 1; i < n; i++) {
            if (arr[i] - pos >= mid) {

                // Place next element if its
                // distance from the previously
                // placed element is greater
                // than current mid
                pos = arr[i];
                elements++;

                // Return if all elements are
                // placed successfully
                if (elements == k)
                    return true;
            }
        }

        return false;
    }

    // Returns largest minimum distance for
    // k elements in arr[0..n-1]. If elements
    // can't be placed, returns -1.
    function largestMinDist(arr, n, k)
    {

        // Sort the positions
        arr.sort(function(a, b){return a - b});

        // Initialize result.
        let res = -1;

        // Consider the maximum possible
        // distance
        let left = 1, right = arr[n - 1];

        // left is initialized with 1 and not with arr[0]
        // because, minimum distance between each element
        // can be one and not arr[0]. consider this example:
        // arr[] = {9,12} and you have to place 2 element
        // then left = arr[0] will force the function to
        // look the answer between range arr[0] to arr[n-1],
        // i.e 9 to 12, but the answer is 3 so It is
        // required that you initialize the left with 1

        // Do binary search for largest
        // minimum distance
        while (left < right) {
            let mid = parseInt((left + right) / 2, 10);

            // If it is possible to place k
            // elements with minimum distance
            // mid, search for higher distance.
            if (isFeasible(mid, arr, n, k)) {
                // Change value of variable
                // max to mid if all elements
                // can be successfully placed
                res = Math.max(res, mid);
                left = mid + 1;
            }

            // If not possible to place k
            // elements, search for lower
            // distance
            else
                right = mid;
        }

        return res;
    }

    let arr = [ 1, 2, 8, 4, 9 ];
    let n = arr.length;
    let k = 3;

    document.write(largestMinDist(arr, n, k));

</script>
```

**Output**

```
3
```

时间复杂度:O(nlog n)，其中 n 为数组长度。

空间竞争力:0(1)

本文由 [**Raghav Jajodia**](https://github.com/jajodiaraghav/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。