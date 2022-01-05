# 统计同时停车的最大车数

> 原文:[https://www . geesforgeks . org/count-最多同时停放的汽车数量/](https://www.geeksforgeeks.org/count-maximum-number-of-cars-parked-at-the-same-time/)

给定一个 [2d 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **arr[][]** ，每行代表一对代表停车场中一辆车的进出时间，任务是计算可以同时停放的最大汽车数量。

**示例:**

> **输入:** arr[][] = {{1012，1136}，{1317，1417}，{1015，1020}}
> **输出:** 2
> **说明:**
> 1 <sup>st</sup> 车 10:12 进入，11:36 退出，3 <sup>rd</sup> 车 10:15 进入，10:20 退出
> 因此，1 <sup>st</sup> 和 3 <sup>rd</sup> 车同时出现。
> 
> **输入:** arr[][] = {{1120，1159}、{1508，1529}、{1508，1527}、{1503，1600}、{1458，1629}、{1224，1313}}
> **输出:** 4
> **解释:** 2 <sup>nd</sup> ，3 <sup>rd 【T11</sup>

**方法:**思路是用[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来解决这个问题。按照以下步骤解决问题:

*   初始化[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，将进入或退出时间存储为一对中的第一个元素，如果存储的相应时间是进入时间，则将 true 存储为一对中的第二个元素。否则，存储为假。
*   [按照时间的非递减顺序对向量进行排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。
*   初始化两个变量，比如说 **curMax** ，以寻找数组中所有的真实连续段，以及 **maxFinal** ，以跟踪所有真实段中最长的真实连续段。
*   迭代范围 **[0，2 * N–1]:**
    *   如果有车进入，将 **curMax** 增加 **1。**
    *   否则:
        *   如果**课程大纲** > **课程大纲**课程大纲，更新**课程大纲** = **课程大纲**。
        *   每当一辆车退出时，用 **1** 减去 **curMax** 。
*   打印 **maxFinal** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of cars parked at the same
int maxCars(int arr[][2], int N)
{
    // Stores info about
    // entry and exit times
    pair<int, bool> a[2 * N];

    // Convert given array to new array
    for (int i = 0; i < N; i++) {
        a[2 * i] = { arr[i][0], true };
        a[2 * i + 1] = { arr[i][1], false };
    }

    // Sort array in ascending
    // order of time
    sort(a, a + 2 * N);

    // Stores current maximum
    // at every iteration
    int curMax = 0;

    // Stores final maximum number
    // of cars parked at any time
    int maxFinal = 0;

    // Traverse the array
    for (int i = 0; i < 2 * N; ++i) {

        // When car entered
        if (a[i].second) {
            curMax++;
        }

        // When car exits
        else {
            if (curMax > maxFinal) {
                maxFinal = curMax;
            }
            curMax--;
        }
    }

    // Print the answer
    cout << maxFinal;
}

// Driver Code
int main()
{
    // Given array
    int arr[][2] = { { 1012, 1136 },
                     { 1317, 1412 },
                     { 1015, 1020 } };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxCars(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Pair class
static class pair
{
    int first;
    boolean second;

    pair(int first, boolean second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to count maximum number
// of cars parked at the same
static void maxCars(int arr[][], int N)
{

    // Stores info about
    // entry and exit times
    pair a[] = new pair[2 * N];

    // Convert given array to new array
    for(int i = 0; i < N; i++)
    {
        a[2 * i] = new pair(arr[i][0], true);
        a[2 * i + 1] = new pair(arr[i][1], false);
    }

    // Sort array in ascending
    // order of time
    Arrays.sort(a, (p1, p2) -> p1.first - p2.first);

    // Stores current maximum
    // at every iteration
    int curMax = 0;

    // Stores final maximum number
    // of cars parked at any time
    int maxFinal = 0;

    // Traverse the array
    for(int i = 0; i < 2 * N; ++i)
    {

        // When car entered
        if (a[i].second)
        {
            curMax++;
        }

        // When car exits
        else
        {
            if (curMax > maxFinal)
            {
                maxFinal = curMax;
            }
            curMax--;
        }
    }

    // Print the answer
    System.out.println(maxFinal);
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[][] = { { 1012, 1136 },
                    { 1317, 1412 },
                    { 1015, 1020 } };

    // Size of the array
    int N = arr.length;

    // Function Call
    maxCars(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count maximum number
# of cars parked at the same
def maxCars(arr, N):

    # Stores info about
    # entry and exit times
    a = [[0,True] for i in range(2 * N)]

    # Convert given array to new array
    for i in range(N):
        a[2 * i] = [arr[i][0], True]
        a[2 * i + 1] = [arr[i][1], False]

    # Sort array in ascending
    # order of time
    a = sorted(a)

    # Stores current maximum
    # at every iteration
    curMax = 0

    # Stores final maximum number
    # of cars parked at any time
    maxFinal = 0

    # Traverse the array
    for i in range(2*N):

        # When car entered
        if (a[i][1]):
            curMax += 1
        # When car exits
        else:
            if (curMax > maxFinal):
                maxFinal = curMax
            curMax -= 1

    # Print answer
    print (maxFinal)

# Driver Code
if __name__ == '__main__':
    # Given array
    arr= [ [ 1012, 1136 ],
         [ 1317, 1412 ],
         [ 1015, 1020 ]]

    # Size of the array
    N = len(arr)

    # Function Call
    maxCars(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
    // Function to count maximum number
    // of cars parked at the same
    static void maxCars(int[,] arr, int N)
    {

        // Stores info about
        // entry and exit times
        Tuple<int, bool>[] a = new Tuple<int, bool>[2 * N];

        // Convert given array to new array
        for (int i = 0; i < N; i++) {
            a[2 * i] = new Tuple<int, bool>(arr[i,0], true);
            a[2 * i + 1] = new Tuple<int, bool>(arr[i,1], false);
        }

        // Stores current maximum
        // at every iteration
        int curMax = 1;

        // Stores final maximum number
        // of cars parked at any time
        int maxFinal = 0;

        // Traverse the array
        for (int i = 0; i < 2 * N; ++i) {

            // When car entered
            if (a[i].Item2) {
                curMax++;
            }

            // When car exits
            else {
                if (curMax > maxFinal) {
                    maxFinal = curMax;
                }
                curMax--;
            }
        }

        // Print the answer
        Console.WriteLine(maxFinal);
    }

  static void Main ()
  {
    // Given array
    int[,] arr = { { 1012, 1136 },
                    { 1317, 1412 },
                    { 1015, 1020 } };

    // Size of the array
    int N = 2;

    // Function Call
    maxCars(arr, N);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Pair class
class pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to count maximum number
// of cars parked at the same
function maxCars(arr,N)
{
    // Stores info about
    // entry and exit times
    let a = new Array(2 * N);

    // Convert given array to new array
    for(let i = 0; i < N; i++)
    {
        a[2 * i] = new pair(arr[i][0], true);
        a[2 * i + 1] = new pair(arr[i][1], false);
    }

    // Sort array in ascending
    // order of time
    a.sort(function(p1, p2){return p1.first - p2.first});

    // Stores current maximum
    // at every iteration
    let curMax = 0;

    // Stores final maximum number
    // of cars parked at any time
    let maxFinal = 0;

    // Traverse the array
    for(let i = 0; i < 2 * N; ++i)
    {

        // When car entered
        if (a[i].second)
        {
            curMax++;
        }

        // When car exits
        else
        {
            if (curMax > maxFinal)
            {
                maxFinal = curMax;
            }
            curMax--;
        }
    }

    // Print the answer
    document.write(maxFinal+"<br>");
}

// Driver Code
let arr=[[ 1012, 1136 ],
                    [ 1317, 1412 ],
                    [ 1015, 1020 ]];
// Size of the array
let N = arr.length;

// Function Call
maxCars(arr, N);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)