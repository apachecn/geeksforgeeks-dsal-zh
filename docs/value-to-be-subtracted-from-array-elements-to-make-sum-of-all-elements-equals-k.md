# 要从数组元素中减去的值，使所有元素的总和等于 K

> 原文:[https://www . geeksforgeeks . org/从数组元素中减去值以得到所有元素的和等于-k/](https://www.geeksforgeeks.org/value-to-be-subtracted-from-array-elements-to-make-sum-of-all-elements-equals-k/)

给定一个整数 **K** 和一个数组，**高度【】**其中**高度【I】**表示森林中 **i <sup>th</sup>** 树的高度。任务是从地面切割高度 **X** ，以便准确收集 **K** 单位木材。如果不可能，则打印 **-1** 否则打印 **X** 。

**示例:**

> **输入:**高度[] = {1，2，1，2}，K = 2
> **输出:** 1
> 在高度 1 进行切割，更新后的数组为{1，1，1，1}，
> 采集的木材为{0，1，0，1}即 0 + 1 + 0 + 1 = 2。
> 
> **输入:**高度= {1，1，2，2}，K = 1
> **输出:** -1

**进场:**这个问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。

*   给树的高度分类。
*   进行砍伐的最低高度为 **0** ，最高为所有树木中的最大高度。因此，设置**低= 0** 和**高=最大(高度[i])** 。
*   当低≤高时，重复以下步骤【T0:
    1.  设置**中间=低+((高–低)/ 2)** 。
    2.  计算在高度**中间**进行切割时可以收集的木材量，并将其储存在变量**收集的**中。
    3.  如果**采集= K** ，那么**中**就是答案。
    4.  如果**采集了> K** ，那么更新 **low = mid + 1** ，因为切割需要在高于当前高度的高度进行。
    5.  否则更新**高=中-1**，因为切割需要在较低的高度进行。
*   如果没有找到**中间**的值，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to return the amount of wood
// collected if the cut is made at height m
int woodCollected(int height[], int n, int m)
{
    int sum = 0;
    for (int i = n - 1; i >= 0; i--) {
        if (height[i] - m <= 0)
            break;
        sum += (height[i] - m);
    }

    return sum;
}

// Function that returns Height at
// which cut should be made
int collectKWood(int height[], int n, int k)
{
    // Sort the heights of the trees
    sort(height, height + n);

    // The minimum and the maximum
    // cut that can be made
    int low = 0, high = height[n - 1];

    // Binary search to find the answer
    while (low <= high) {
        int mid = low + ((high - low) / 2);

        // The amount of wood collected
        // when cut is made at the mid
        int collected = woodCollected(height, n, mid);

        // If the current collected wood is
        // equal to the required amount
        if (collected == k)
            return mid;

        // If it is more than the required amount
        // then the cut needs to be made at a
        // height higher than the current height
        if (collected > k)
            low = mid + 1;

        // Else made the cut at a lower height
        else
            high = mid - 1;
    }

    return -1;
}

// Driver code
int main()
{

    int height[] = { 1, 2, 1, 2 };
    int n = sizeof(height) / sizeof(height[0]);
    int k = 2;

    cout << collectKWood(height, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{
    static int[] height = new int[]{ 1, 2, 1, 2 };

    // Function to return the amount of wood
    // collected if the cut is made at height m
    public static int woodCollected(int n, int m)
    {
        int sum = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            if (height[i] - m <= 0)
                break;
            sum += (height[i] - m);
        }
        return sum;
    }

    // Function that returns Height at
    // which cut should be made
    public static int collectKWood(int n, int k)
    {
        // Sort the heights of the trees
        Arrays.sort(height);

        // The minimum and the maximum
        // cut that can be made
        int low = 0, high = height[n - 1];

        // Binary search to find the answer
        while (low <= high)
        {
            int mid = low + ((high - low) / 2);

            // The amount of wood collected
            // when cut is made at the mid
            int collected = woodCollected(n, mid);

            // If the current collected wood is
            // equal to the required amount
            if (collected == k)
                return mid;

            // If it is more than the required amount
            // then the cut needs to be made at a
            // height higher than the current height
            if (collected > k)
                low = mid + 1;

            // Else made the cut at a lower height
            else
                high = mid - 1;
        }
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int k = 2;
        int n = height.length;
        System.out.print(collectKWood(n,k));
    }
}

// This code is contributed by Sanjit_Prasad
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the amount of wood
# collected if the cut is made at height m
def woodCollected(height, n, m):
    sum = 0
    for i in range(n - 1, -1, -1):
        if (height[i] - m <= 0):
            break
        sum += (height[i] - m)

    return sum

# Function that returns Height at
# which cut should be made
def collectKWood(height, n, k):

    # Sort the heights of the trees
    height = sorted(height)

    # The minimum and the maximum
    # cut that can be made
    low = 0
    high = height[n - 1]

    # Binary search to find the answer
    while (low <= high):
        mid = low + ((high - low) // 2)

        # The amount of wood collected
        # when cut is made at the mid
        collected = woodCollected(height, n, mid)

        # If the current collected wood is
        # equal to the required amount
        if (collected == k):
            return mid

        # If it is more than the required amount
        # then the cut needs to be made at a
        # height higher than the current height
        if (collected > k):
            low = mid + 1

        # Else made the cut at a lower height
        else:
            high = mid - 1

    return -1

# Driver code
height = [1, 2, 1, 2]
n = len(height)
k = 2

print(collectKWood(height, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{
    static int[] height = { 1, 2, 1, 2 };

    // Function to return the amount of wood
    // collected if the cut is made at height m
    public static int woodCollected(int n, int m)
    {
        int sum = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            if (height[i] - m <= 0)
                break;
            sum += (height[i] - m);
        }
        return sum;
    }

    // Function that returns Height at
    // which cut should be made
    public static int collectKWood(int n, int k)
    {
        // Sort the heights of the trees
        Array.Sort(height);

        // The minimum and the maximum
        // cut that can be made
        int low = 0, high = height[n - 1];

        // Binary search to find the answer
        while (low <= high)
        {
            int mid = low + ((high - low) / 2);

            // The amount of wood collected
            // when cut is made at the mid
            int collected = woodCollected(n, mid);

            // If the current collected wood is
            // equal to the required amount
            if (collected == k)
                return mid;

            // If it is more than the required amount
            // then the cut needs to be made at a
            // height higher than the current height
            if (collected > k)
                low = mid + 1;

            // Else made the cut at a lower height
            else
                high = mid - 1;
        }
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int k = 2;
        int n = height.Length;
        Console.WriteLine(collectKWood(n,k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the amount of wood
// collected if the cut is made at height m
function woodCollected(height, n, m) {
    let sum = 0;
    for (let i = n - 1; i >= 0; i--) {
        if (height[i] - m <= 0)
            break;
        sum += (height[i] - m);
    }

    return sum;
}

// Function that returns Height at
// which cut should be made
function collectKWood(height, n, k) {
    // Sort the heights of the trees
    height.sort((a, b) => a - b);

    // The minimum and the maximum
    // cut that can be made
    let low = 0, high = height[n - 1];

    // Binary search to find the answer
    while (low <= high) {
        let mid = low + ((high - low) / 2);

        // The amount of wood collected
        // when cut is made at the mid
        let collected = woodCollected(height, n, mid);

        // If the current collected wood is
        // equal to the required amount
        if (collected == k)
            return mid;

        // If it is more than the required amount
        // then the cut needs to be made at a
        // height higher than the current height
        if (collected > k)
            low = mid + 1;

        // Else made the cut at a lower height
        else
            high = mid - 1;
    }

    return -1;
}

// Driver code

let height = [ 1, 2, 1, 2 ];
let n = height.length;
let k = 2;

document.write(collectKWood(height, n, k));
</script>
```

**Output:** 

```
1
```

时间复杂性

辅助空间:0(1)