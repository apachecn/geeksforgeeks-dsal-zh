# 对给定范围内可访问的数量进行计数，从范围[L，R]

移动任意数量的步骤

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-给定范围-可以访问-移动-任意步数-from-l-r/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-that-can-be-visited-moving-any-number-of-steps-from-the-range-l-r/)

给定两个整数 **X** 、 **Y** 和一个范围**【L，R】**，任务是从**X**和 **Y** ( *包括*)开始，从 **X** 开始，在任意数量的步骤中对可以访问的整数进行计数。每一步都可以增加 **L** 到 **R** 。

**示例:**

> **输入:** X = 1，Y = 10，L = 4，R = 6
> **输出:** 6
> **说明:**在【1，10】之间总共可以访问六个点:
> 
> 1.  1:起点
> 2.  5: 1 -> 5
> 3.  6: 1 -> 6
> 4.  7: 1 -> 7
> 5.  9: 1 -> 5 -> 9
> 6.  10: 1 -> 5 -> 10
> 
> **输入:** X = 3，Y = 12，L = 2，R = 3
> T3】输出: 9

**方法:**从索引 I 开始，可以到达[i+L，i+R]之间的任何位置，同样，对于[i+L，i+R]中的每个点 j，可以移动到[j+L，j+R]。对于每个索引 I，可以使用[差异数组](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)来标记这些可达范围。按照以下步骤进行操作。

*   构建一个大尺寸的数组**来标记范围。**
*   **初始化一个变量，比如**计数= 0，**来计算可到达的点。**
*   **首先，使 **diff_arr[x] = 1** 和 **diff_arr[x+1] = -1** 将起点 **X** 标记为已访问。**
*   **从 **X** 迭代到 **Y** ，对于每个 **i** 更新**diff _ arr[I]+= diff _ arr[I-1]**，如果 **diff_arr[i] > = 1** ，则更新 **diff_arr[i+L] = 1** 和 **diff_arr[i + R + 1] = -1** 和**计数=计数+ 1。****
*   **最后，返回**计数**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ code for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count points from the range [X, Y]
// that can be reached by moving by L or R steps
int countReachablePoints(int X, int Y,
                         int L, int R)
{

    // Initialize difference array
    int diff_arr[100000] = { 0 };

    // Initialize Count
    int count = 0;

    // Marking starting point
    diff_arr[X] = 1;
    diff_arr[X + 1] = -1;

    // Iterating from X to Y
    for (int i = X; i <= Y; i++) {

        // Accumulate difference array
        diff_arr[i] += diff_arr[i - 1];

        // If diff_arr[i] is greater
        // than 1
        if (diff_arr[i] >= 1) {
            // Updating difference array
            diff_arr[i + L] += 1;
            diff_arr[i + R + 1] -= 1;

            // Visited point found
            count++;
        }
    }
    return count;
}

// Driver Code
int main()

{
    // Given Input
    int X = 3, Y = 12, L = 2, R = 3;

    // Function Call
    cout << countReachablePoints(X, Y, L, R);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code for above approach

import java.util.*;

class GFG{

// Function to count points from the range [X, Y]
// that can be reached by moving by L or R steps
static int countReachablePoints(int X, int Y,
                         int L, int R)
{

    // Initialize difference array
    int diff_arr[] = new int[100000];

    // Initialize Count
    int count = 0;

    // Marking starting point
    diff_arr[X] = 1;
    diff_arr[X + 1] = -1;

    // Iterating from X to Y
    for (int i = X; i <= Y; i++) {

        // Accumulate difference array
        diff_arr[i] += diff_arr[i - 1];

        // If diff_arr[i] is greater
        // than 1
        if (diff_arr[i] >= 1) {
            // Updating difference array
            diff_arr[i + L] += 1;
            diff_arr[i + R + 1] -= 1;

            // Visited point found
            count++;
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)

{
    // Given Input
    int X = 3, Y = 12, L = 2, R = 3;

    // Function Call
    System.out.print(countReachablePoints(X, Y, L, R));

}
}

// This code contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# Python3 code for above approach

# Function to count points from the range [X, Y]
# that can be reached by moving by L or R steps
def countReachablePoints(X, Y, L, R):

    # Initialize difference array
    diff_arr = [0 for i in range(100000)]

    # Initialize Count
    count = 0

    # Marking starting point
    diff_arr[X] = 1
    diff_arr[X + 1] = -1

    # Iterating from X to Y
    for i in range(X, Y + 1, 1):

        # Accumulate difference array
        diff_arr[i] += diff_arr[i - 1]

        # If diff_arr[i] is greater
        # than 1
        if (diff_arr[i] >= 1):

            # Updating difference array
            diff_arr[i + L] += 1
            diff_arr[i + R + 1] -= 1

            # Visited point found
            count += 1

    return count

# Driver Code
if __name__ == '__main__':

    # Given Input
    X = 3
    Y = 12
    L = 2
    R = 3

    # Function Call
    print(countReachablePoints(X, Y, L, R))

# This code is contributed by ipg2016107
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to count points from the range [X, Y]
// that can be reached by moving by L or R steps
static int countReachablePoints(int X, int Y,
                         int L, int R)
{

    // Initialize difference array
    int[] diff_arr= new int[100000];

    // Initialize Count
    int count = 0;

    // Marking starting point
    diff_arr[X] = 1;
    diff_arr[X + 1] = -1;

    // Iterating from X to Y
    for (int i = X; i <= Y; i++) {

        // Accumulate difference array
        diff_arr[i] += diff_arr[i - 1];

        // If diff_arr[i] is greater
        // than 1
        if (diff_arr[i] >= 1)
        {

            // Updating difference array
            diff_arr[i + L] += 1;
            diff_arr[i + R + 1] -= 1;

            // Visited point found
            count++;
        }
    }
    return count;
}
// Driver Code
public static void Main()
{
        // Given Input
    int X = 3, Y = 12, L = 2, R = 3;

    // Function Call
    Console.Write(countReachablePoints(X, Y, L, R));
}
}

// This code is contributed by splevel62.
```

## **java 描述语言**

```
<script>

// JavaScript code for above approach

// Function to count points from the range [X, Y]
// that can be reached by moving by L or R steps
function countReachablePoints(X, Y, L, R) {
  // Initialize difference array
  let diff_arr = new Array(100000).fill(0);

  // Initialize Count
  let count = 0;

  // Marking starting point
  diff_arr[X] = 1;
  diff_arr[X + 1] = -1;

  // Iterating from X to Y
  for (let i = X; i <= Y; i++) {
    // Accumulate difference array
    diff_arr[i] += diff_arr[i - 1];

    // If diff_arr[i] is greater
    // than 1
    if (diff_arr[i] >= 1) {
      // Updating difference array
      diff_arr[i + L] += 1;
      diff_arr[i + R + 1] -= 1;

      // Visited point found
      count++;
    }
  }
  return count;
}

// Driver Code

// Given Input
let X = 3,
  Y = 12,
  L = 2,
  R = 3;

// Function Call
document.write(countReachablePoints(X, Y, L, R));

</script>
```

****Output:** 

```
9
```** 

*****时间复杂度:**O(Y–X)*
***辅助空间:** O(Y)***