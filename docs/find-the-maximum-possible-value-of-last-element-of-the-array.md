# 求数组最后一个元素的最大可能值

> 原文:[https://www . geesforgeks . org/find-数组最后一个元素的最大可能值/](https://www.geeksforgeeks.org/find-the-maximum-possible-value-of-last-element-of-the-array/)

给定一个大小为 **N** 的非负数组 **arr** 和一个表示移动次数的整数 **M** ，这样在一次移动中，数组中任何一个元素的值减少 1，其右边相邻元素的值增加 1。任务是在给定的 **M** 移动次数下，找到数组最后一个元素的最大可能值。
**举例:**

> **输入:** arr[] = {2，3，0，1}，M = 5
> **输出:** 3
> 移动 1:处理索引 1，第一个索引处的元素 3 减少为 2，第二个索引处的元素 0 增加为 1。因此，一次移动后得到的数组= {2，2，1，1}
> 移动 2:处理索引 2 时，第二个索引处的元素 1 减少为 0，第三个索引处的元素 1 增加为 2。因此，两次移动后得到的数组= {2，2，0，2}
> 移动 3:处理索引 1 时，第一个索引处的元素 2 减少为 1，第二个索引处的元素 0 增加为 1。因此，经过三次移动{2，1，1，2}
> 移动 4 后得到的数组:在索引 2 上，第二个索引处的元素 1 减少为 0，第三个索引处的元素 2 增加为 3。因此，经过四次移动后得到的数组{2，1，0，3}
> 移动 5:处理索引 1 时，第一个索引处的元素 1 减少为 0，第二个索引处的元素 0 增加为 1。因此五次移动后的结果为{2，0，1，3}
> 所以五次移动后最后一个元素的最大值为 3
> **输入:** arr[] = {1，100}，M = 2
> **输出:** 101

**方法:**
将一个值从一个元素移动到最后一个元素所需的移动次数由它们之间的[距离](https://www.geeksforgeeks.org/find-the-minimum-distance-between-two-numbers/)计算。对于数组中的每个元素，如果这个元素和最后一个元素之间的距离小于等于 M，那么这个元素可以移动到最后一个。所以为了移动它，随着距离增加最后一个元素，随着距离减少左边的移动次数。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the maximum possible
// value of last element of the array

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible
// value of last element of the array
int maxValue(int arr[], int n, int moves)
{

    // Traverse for all element
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] > 0) {
            // Find the distance
            int distance = n - 1 - i;

            // If moves less than distance then
            // we can not move this number to end
            if (moves < distance)
                break;

            // How many number we can move to end
            int can_take = moves / distance;

            // Take the minimum of both of them
            int take = min(arr[i], can_take);

            // Increment in the end
            arr[n - 1] += take;

            // Remove taken moves
            moves -= take * distance;
        }
    }

    // Return the last element
    return arr[n - 1];
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 0, 1 };
    int M = 5;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << maxValue(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum possible
// value of last element of the array
import java.util.*;

class GFG{

// Function to find the maximum possible
// value of last element of the array
static int maxValue(int arr[], int n, int moves)
{

    // Traverse for all element
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] > 0) {
            // Find the distance
            int distance = n - 1 - i;

            // If moves less than distance then
            // we can not move this number to end
            if (moves < distance)
                break;

            // How many number we can move to end
            int can_take = moves / distance;

            // Take the minimum of both of them
            int take = Math.min(arr[i], can_take);

            // Increment in the end
            arr[n - 1] += take;

            // Remove taken moves
            moves -= take * distance;
        }
    }

    // Return the last element
    return arr[n - 1];
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 0, 1 };
    int M = 5;
    int N = arr.length;

    // Function call
    System.out.print(maxValue(arr, N, M));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the maximum possible
# value of last element of the array

# Function to find the maximum possible
# value of last element of the array
def maxValue(arr, n, moves):

    # Traverse for all element
    for i in range(n - 2, -1, -1):
        if (arr[i] > 0):

            # Find the distance
            distance = n - 1 - i

            # If moves less than distance then
            # we can not move this number to end
            if (moves < distance):
                break

            # How many number we can move to end
            can_take = moves // distance

            # Take the minimum of both of them
            take = min(arr[i], can_take)

            # Increment in the end
            arr[n - 1] += take

            # Remove taken moves
            moves -= take * distance

    # Return the last element
    return arr[n - 1]

# Driver code
if __name__ == '__main__':
    arr= [2, 3, 0, 1]
    M = 5
    N = len(arr)

    # Function call
    print(maxValue(arr, N, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the maximum possible
// value of last element of the array
using System;

class GFG{

// Function to find the maximum possible
// value of last element of the array
static int maxValue(int []arr, int n, int moves)
{

    // Traverse for all element
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] > 0) {
            // Find the distance
            int distance = n - 1 - i;

            // If moves less than distance then
            // we can not move this number to end
            if (moves < distance)
                break;

            // How many number we can move to end
            int can_take = moves / distance;

            // Take the minimum of both of them
            int take = Math.Min(arr[i], can_take);

            // Increment in the end
            arr[n - 1] += take;

            // Remove taken moves
            moves -= take * distance;
        }
    }

    // Return the last element
    return arr[n - 1];
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 0, 1 };
    int M = 5;
    int N = arr.Length;

    // Function call
    Console.Write(maxValue(arr, N, M));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the maximum possible
// value of last element of the array

// Function to find the maximum possible
// value of last element of the array
function maxValue(arr, n, moves)
{

    // Traverse for all element
    for (var i = n - 2; i >= 0; i--)
    {
        if (arr[i] > 0)
        {

            // Find the distance
            var distance = n - 1 - i;

            // If moves less than distance then
            // we can not move this number to end
            if (moves < distance)
                break;

            // How many number we can move to end
            var can_take = parseInt(moves / distance);

            // Take the minimum of both of them
            var take = Math.min(arr[i], can_take);

            // Increment in the end
            arr[n - 1] += take;

            // Remove taken moves
            moves -= take * distance;
        }
    }

    // Return the last element
    return arr[n - 1];
}

// Driver code
var arr = [2, 3, 0, 1];
var M = 5;
var N = arr.length;

// Function call
document.write( maxValue(arr, N, M));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3
```