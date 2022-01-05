# 将囚犯放入牢房，使任意两个之间的最小差异最大化

> 原文:[https://www . geeksforgeeks . org/将囚犯放入牢房，以最大化或最小化任意两人之间的差异/](https://www.geeksforgeeks.org/place-the-prisoners-into-cells-to-maximize-the-minimum-difference-between-any-two/)

给定一个由 **N** 个元素组成的数组**个单元【】**，这些元素代表监狱中各个单元的位置。此外，给定一个整数 **P** ，即囚犯的数量，任务是以有序的方式将所有囚犯放入牢房，使得任何两个囚犯之间的最小距离尽可能大。最后，打印最大距离。
**示例:**

> **输入:**牢房[] = {1，2，8，4，9}，P = 3
> **输出:** 3
> 三名囚犯将被安置在编号为 1，4 和 8 的牢房
> ，最小距离为 3
> ，这是最大可能。
> **输入:**单元格[] = {10，12，18}，P = 2
> **输出:** 8
> 三种可能的放置方式为{10，12}、 **{10，18}** 和{12，18}。

**进场:**这个问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。由于关押囚犯的两个牢房之间的最小距离必须最大化，搜索空间将是一定距离的，从 **0** (如果两个囚犯被关押在同一个牢房中)开始，到**牢房【N–1】–牢房【0】**(如果一个囚犯被关押在第一个牢房中，另一个被关押在最后一个牢房中)结束。
初始化 **L = 0** 和 **R =单元格[N–1]–单元格[0]** ，然后应用二分搜索法。每隔**中间**，检查囚犯是否可以被放置，使得任意两个囚犯之间的最小距离至少为**中间**

*   如果是，那么尝试增加这个距离，以便最大化答案，并再次检查。
*   如果没有，那么尽量缩短距离。
*   最后，打印最大距离。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the prisoners
// can be placed such that the minimum distance
// between any two prisoners is at least sep
bool canPlace(int a[], int n, int p, int sep)
{
    // Considering the first prisoner
    // is placed at 1st cell
    int prisoners_placed = 1;

    // If the first prisoner is placed at
    // the first cell then the last_prisoner_placed
    // will be the first prisoner placed
    // and that will be in cell[0]
    int last_prisoner_placed = a[0];

    for (int i = 1; i < n; i++) {
        int current_cell = a[i];

        // Checking if the prisoner can be
        // placed at ith cell or not
        if (current_cell - last_prisoner_placed >= sep) {
            prisoners_placed++;
            last_prisoner_placed = current_cell;

            // If all the prisoners got placed
            // then return true
            if (prisoners_placed == p) {
                return true;
            }
        }
    }

    return false;
}

// Function to return the maximized distance
int maxDistance(int cell[], int n, int p)
{

    // Sort the array so that binary
    // search can be applied on it
    sort(cell, cell + n);

    // Minimum possible distance
    // for the search space
    int start = 0;

    // Maximum possible distance
    // for the search space
    int end = cell[n - 1] - cell[0];

    // To store the result
    int ans = 0;

    // Binary search
    while (start <= end) {
        int mid = start + ((end - start) / 2);

        // If the prisoners can be placed such that
        // the minimum distance between any two
        // prisoners is at least mid
        if (canPlace(cell, n, p, mid)) {

            // Update the answer
            ans = mid;
            start = mid + 1;
        }
        else {
            end = mid - 1;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int cell[] = { 1, 2, 8, 4, 9 };
    int n = sizeof(cell) / sizeof(int);
    int p = 3;

    cout << maxDistance(cell, n, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true if the prisoners
    // can be placed such that the minimum distance
    // between any two prisoners is at least sep
    static boolean canPlace(int a[], int n, int p, int sep)
    {
        // Considering the first prisoner
        // is placed at 1st cell
        int prisoners_placed = 1;

        // If the first prisoner is placed at
        // the first cell then the last_prisoner_placed
        // will be the first prisoner placed
        // and that will be in cell[0]
        int last_prisoner_placed = a[0];

        for (int i = 1; i < n; i++)
        {
            int current_cell = a[i];

            // Checking if the prisoner can be
            // placed at ith cell or not
            if (current_cell - last_prisoner_placed >= sep)
            {
                prisoners_placed++;
                last_prisoner_placed = current_cell;

                // If all the prisoners got placed
                // then return true
                if (prisoners_placed == p)
                {
                    return true;
                }
            }
        }

        return false;
    }

    // Function to return the maximized distance
    static int maxDistance(int cell[], int n, int p)
    {

        // Sort the array so that binary
        // search can be applied on it
        Arrays.sort(cell);

        // Minimum possible distance
        // for the search space
        int start = 0;

        // Maximum possible distance
        // for the search space
        int end = cell[n - 1] - cell[0];

        // To store the result
        int ans = 0;

        // Binary search
        while (start <= end)
        {
            int mid = start + ((end - start) / 2);

            // If the prisoners can be placed such that
            // the minimum distance between any two
            // prisoners is at least mid
            if (canPlace(cell, n, p, mid))
            {

                // Update the answer
                ans = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int cell[] = { 1, 2, 8, 4, 9 };
        int n = cell.length;
        int p = 3;

        System.out.println(maxDistance(cell, n, p));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the prisoners
# can be placed such that the minimum distance
# between any two prisoners is at least sep
def canPlace(a, n, p, sep):

    # Considering the first prisoner
    # is placed at 1st cell
    prisoners_placed = 1

    # If the first prisoner is placed at
    # the first cell then the last_prisoner_placed
    # will be the first prisoner placed
    # and that will be in cell[0]
    last_prisoner_placed = a[0]

    for i in range(1, n):
        current_cell = a[i]

        # Checking if the prisoner can be
        # placed at ith cell or not
        if (current_cell - last_prisoner_placed >= sep):
            prisoners_placed += 1
            last_prisoner_placed = current_cell

            # If all the prisoners got placed
            # then return true
            if (prisoners_placed == p):
                return True

    return False

# Function to return the maximized distance
def maxDistance(cell, n, p):

    # Sort the array so that binary
    # search can be applied on it
    cell = sorted(cell)

    # Minimum possible distance
    # for the search space
    start = 0

    # Maximum possible distance
    # for the search space
    end = cell[n - 1] - cell[0]

    # To store the result
    ans = 0

    # Binary search
    while (start <= end):
        mid = start + ((end - start) // 2)

        # If the prisoners can be placed such that
        # the minimum distance between any two
        # prisoners is at least mid
        if (canPlace(cell, n, p, mid)):

            # Update the answer
            ans = mid
            start = mid + 1
        else :
            end = mid - 1

    return ans

# Driver code
cell= [1, 2, 8, 4, 9]
n = len(cell)
p = 3

print(maxDistance(cell, n, p))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{

    // Function that returns true if the prisoners
    // can be placed such that the minimum distance
    // between any two prisoners is at least sep
    static bool canPlace(int []a, int n,
                         int p, int sep)
    {
        // Considering the first prisoner
        // is placed at 1st cell
        int prisoners_placed = 1;

        // If the first prisoner is placed at
        // the first cell then the last_prisoner_placed
        // will be the first prisoner placed
        // and that will be in cell[0]
        int last_prisoner_placed = a[0];

        for (int i = 1; i < n; i++)
        {
            int current_cell = a[i];

            // Checking if the prisoner can be
            // placed at ith cell or not
            if (current_cell - last_prisoner_placed >= sep)
            {
                prisoners_placed++;
                last_prisoner_placed = current_cell;

                // If all the prisoners got placed
                // then return true
                if (prisoners_placed == p)
                {
                    return true;
                }
            }
        }
        return false;
    }

    // Function to return the maximized distance
    static int maxDistance(int []cell, int n, int p)
    {

        // Sort the array so that binary
        // search can be applied on it
        Array.Sort(cell);

        // Minimum possible distance
        // for the search space
        int start = 0;

        // Maximum possible distance
        // for the search space
        int end = cell[n - 1] - cell[0];

        // To store the result
        int ans = 0;

        // Binary search
        while (start <= end)
        {
            int mid = start + ((end - start) / 2);

            // If the prisoners can be placed such that
            // the minimum distance between any two
            // prisoners is at least mid
            if (canPlace(cell, n, p, mid))
            {

                // Update the answer
                ans = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []cell = { 1, 2, 8, 4, 9 };
        int n = cell.Length;
        int p = 3;

        Console.WriteLine(maxDistance(cell, n, p));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function that returns true if the prisoners
    // can be placed such that the minimum distance
    // between any two prisoners is at least sep
    function canPlace(a , n , p , sep)
    {

        // Considering the first prisoner
        // is placed at 1st cell
        var prisoners_placed = 1;

        // If the first prisoner is placed at
        // the first cell then the last_prisoner_placed
        // will be the first prisoner placed
        // and that will be in cell[0]
        var last_prisoner_placed = a[0];

        for (i = 1; i < n; i++)
        {
            var current_cell = a[i];

            // Checking if the prisoner can be
            // placed at ith cell or not
            if (current_cell - last_prisoner_placed >= sep)
            {
                prisoners_placed++;
                last_prisoner_placed = current_cell;

                // If all the prisoners got placed
                // then return true
                if (prisoners_placed == p)
                {
                    return true;
                }
            }
        }

        return false;
    }

    // Function to return the maximized distance
    function maxDistance(cell , n , p)
    {

        // Sort the array so that binary
        // search can be applied on it
        cell.sort();

        // Minimum possible distance
        // for the search space
        var start = 0;

        // Maximum possible distance
        // for the search space
        var end = cell[n - 1] - cell[0];

        // To store the result
        var ans = 0;

        // Binary search
        while (start <= end)
        {
            var mid = start + parseInt(((end - start) / 2));

            // If the prisoners can be placed such that
            // the minimum distance between any two
            // prisoners is at least mid
            if (canPlace(cell, n, p, mid))
            {

                // Update the answer
                ans = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
        var cell = [ 1, 2, 8, 4, 9 ];
        var n = cell.length;
        var p = 3;

        document.write(maxDistance(cell, n, p));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```