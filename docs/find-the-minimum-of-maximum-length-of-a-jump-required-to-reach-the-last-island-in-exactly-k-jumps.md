# 精确地在 k 次跳跃中找到到达最后一个岛所需的最大跳跃长度的最小值

> 原文:[https://www . geeksforgeeks . org/find-到达最后一个岛所需的最小最大跳跃长度-精确 k-跳跃/](https://www.geeksforgeeks.org/find-the-minimum-of-maximum-length-of-a-jump-required-to-reach-the-last-island-in-exactly-k-jumps/)

给定整数数组**arr【】**，其中**I<sup>th</sup>T5【整数】表示存在岛屿的位置，以及整数 **k** (1 ≤ k < N)。一个人站在 **0 <sup>th</sup>** 岛上，必须到达最后一个岛，通过准确地 **k** 跳跃从一个岛跳到另一个岛，任务是找到一个人在旅程中最大跳跃长度的最小值。**注意**所有岛屿的位置是按升序给出的。
**举例:**** 

> **输入:** arr[] = {2，15，36，43}，k = 1
> **输出:** 41
> 到达终点只有一条路
> 2->43
> T8】输入: arr[] = {2，15，36，43}，k = 2
> **输出:** 28
> 到达最后一个岛
> 2-
> 有两条路
> 2 - > 36 - > 43
> 这里任何两个连续岛屿之间的最大距离在 36 和 2 之间，即 34。
> 因此 28 和 34 的最小值是 28。

**方法:**想法是使用二分搜索法，对于距离**中间**，计算是否有可能在恰好 k 个跳跃中到达阵列的末端，其中选择用于跳跃的任意两个岛之间的最大距离小于或等于距离**中间**，然后检查是否存在小于**中间**的距离，对于该距离，有可能在恰好 k 个跳跃中到达末端。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is possible
// to reach end of the array in exactly k jumps
bool isPossible(int arr[], int n, int dist, int k)
{

    // Variable to store the number of
    // steps required to reach the end
    int req = 0;

    int curr = 0;
    int prev = 0;

    for (int i = 0; i < n; i++) {
        while (curr != n && arr[curr] - arr[prev] <= dist)
            curr++;
        req++;

        if (curr == n)
            break;
        prev = curr - 1;
    }

    if (curr != n)
        return false;

    // If it is possible to reach the
    // end in exactly k jumps
    if (req <= k)
        return true;

    return false;
}

// Returns the minimum maximum distance required
// to reach the end of the array in exactly k jumps
int minDistance(int arr[], int n, int k)
{
    int l = 0;
    int h = arr[n - 1];

    // Stores the answer
    int ans = 0;

    // Binary search to calculate the result
    while (l <= h) {
        int m = (l + h) / 2;
        if (isPossible(arr, n, m, k)) {
            ans = m;
            h = m - 1;
        }
        else
            l = m + 1;
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 15, 36, 43 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    cout << minDistance(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function that returns true if it is possible
    // to reach end of the array in exactly k jumps
    static boolean isPossible(int arr[], int n, int dist, int k)
    {

        // Variable to store the number of
        // steps required to reach the end
        int req = 0;

        int curr = 0;
        int prev = 0;

        for (int i = 0; i < n; i++)
        {
            while (curr != n && arr[curr] - arr[prev] <= dist)
            {
                curr++;
            }
            req++;

            if (curr == n)
            {
                break;
            }
            prev = curr - 1;
        }

        if (curr != n)
        {
            return false;
        }

        // If it is possible to reach the
        // end in exactly k jumps
        if (req <= k)
        {
            return true;
        }

        return false;
    }

    // Returns the minimum maximum distance required
    // to reach the end of the array in exactly k jumps
    static int minDistance(int arr[], int n, int k)
    {
        int l = 0;
        int h = arr[n - 1];

        // Stores the answer
        int ans = 0;

        // Binary search to calculate the result
        while (l <= h)
        {
            int m = (l + h) / 2;
            if (isPossible(arr, n, m, k))
            {
                ans = m;
                h = m - 1;
            }
            else
            {
                l = m + 1;
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 15, 36, 43};
        int n = arr.length;
        int k = 2;

        System.out.println(minDistance(arr, n, k));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is possible
# to reach end of the array in exactly k jumps
def isPossible(arr, n, dist, k) :

    # Variable to store the number of
    # steps required to reach the end
    req = 0

    curr = 0
    prev = 0

    for i in range(0, n):
        while (curr != n and (arr[curr] - arr[prev]) <= dist):
            curr = curr + 1
        req = req + 1

        if (curr == n):
            break
        prev = curr - 1

    if (curr != n):
        return False

    # If it is possible to reach the
    # end in exactly k jumps
    if (req <= k):
        return True

    return False

# Returns the minimum maximum distance required
# to reach the end of the array in exactly k jumps
def minDistance(arr, n, k):

    l = 0
    h = arr[n - 1]

    # Stores the answer
    ans = 0

    # Binary search to calculate the result
    while (l <= h):
        m = (l + h) // 2;
        if (isPossible(arr, n, m, k)):
            ans = m
            h = m - 1

        else:
            l = m + 1

    return ans

# Driver code

arr = [ 2, 15, 36, 43 ]
n =  len(arr)
k = 2

print(minDistance(arr, n, k))

# This code is contributed by ihritik
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

    // Function that returns true if it is possible
    // to reach end of the array in exactly k jumps
    static bool isPossible(int []arr, int n, int dist, int k)
    {

        // Variable to store the number of
        // steps required to reach the end
        int req = 0;

        int curr = 0;
        int prev = 0;

        for (int i = 0; i < n; i++)
        {
            while (curr != n && arr[curr] - arr[prev] <= dist)
            {
                curr++;
            }
            req++;

            if (curr == n)
            {
                break;
            }
            prev = curr - 1;
        }

        if (curr != n)
        {
            return false;
        }

        // If it is possible to reach the
        // end in exactly k jumps
        if (req <= k)
        {
            return true;
        }

        return false;
    }

    // Returns the minimum maximum distance required
    // to reach the end of the array in exactly k jumps
    static int minDistance(int []arr, int n, int k)
    {
        int l = 0;
        int h = arr[n - 1];

        // Stores the answer
        int ans = 0;

        // Binary search to calculate the result
        while (l <= h)
        {
            int m = (l + h) / 2;
            if (isPossible(arr, n, m, k))
            {
                ans = m;
                h = m - 1;
            }
            else
            {
                l = m + 1;
            }
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 15, 36, 43};
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(minDistance(arr, n, k));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function that returns true if it is possible
// to reach end of the array in exactly k jumps
function isPossible($arr, $n, $dist, $k)
{

    // Variable to store the number of
    // steps required to reach the end
    $req = 0;

    $curr = 0;
    $prev = 0;

    for ($i = 0; $i < $n; $i++)
    {
        while ($curr != $n && $arr[$curr] - $arr[$prev] <= $dist)
            $curr++;
        $req++;

        if ($curr == $n)
            break;
        $prev = $curr - 1;
    }

    if ($curr != $n)
        return false;

    // If it is possible to reach the
    // end in exactly k jumps
    if ($req <= $k)
        return true;

    return false;
}

// Returns the minimum maximum distance required
// to reach the end of the array in exactly k jumps
function minDistance($arr, $n, $k)
{
    $l = 0;
    $h = $arr[$n - 1];

    // Stores the answer
    $ans = 0;

    // Binary search to calculate the result
    while ($l <= $h)
    {
        $m = floor(($l + $h) / 2);
        if (isPossible($arr, $n, $m, $k))
        {
            $ans = $m;
            $h = $m - 1;
        }
        else
            $l = $m + 1;
    }

    return $ans;
}

    // Driver code
    $arr = array( 2, 15, 36, 43 );
    $n = count($arr);
    $k = 2;

    echo minDistance($arr, $n, $k);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function that returns true if it is possible
    // to reach end of the array in exactly k jumps
    function isPossible(arr, n, dist, k)
    {

        // Variable to store the number of
        // steps required to reach the end
        let req = 0;

        let curr = 0;
        let prev = 0;

        for (let i = 0; i < n; i++)
        {
            while (curr != n && arr[curr] - arr[prev] <= dist)
            {
                curr++;
            }
            req++;

            if (curr == n)
            {
                break;
            }
            prev = curr - 1;
        }

        if (curr != n)
        {
            return false;
        }

        // If it is possible to reach the
        // end in exactly k jumps
        if (req <= k)
        {
            return true;
        }

        return false;
    }

    // Returns the minimum maximum distance required
    // to reach the end of the array in exactly k jumps
    function minDistance(arr, n, k)
    {
        let l = 0;
        let h = arr[n - 1];

        // Stores the answer
        let ans = 0;

        // Binary search to calculate the result
        while (l <= h)
        {
            let m = Math.floor((l + h) / 2);
            if (isPossible(arr, n, m, k))
            {
                ans = m;
                h = m - 1;
            }
            else
            {
                l = m + 1;
            }
        }

        return ans;
    }

// Driver Code

        let arr = [2, 15, 36, 43];
        let n = arr.length;
        let k = 2;

         document.write(minDistance(arr, n, k));

</script>
```

**Output:** 

```
28
```