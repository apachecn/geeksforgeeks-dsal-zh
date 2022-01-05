# 检查给定范围内的子阵列之和是否为完美平方

> 原文:[https://www . geesforgeks . org/check-如果给定范围内的子阵列之和不是完美平方/](https://www.geeksforgeeks.org/check-if-the-sum-of-a-subarray-within-a-given-range-is-a-perfect-square-or-not/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数组**range【】**，任务是检查子阵列**的和是否{range[0]，..，范围[1]}** 是不是一个[完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果和是一个完美的平方，那么打印和的平方根。否则，打印 **-1。**

**示例:**

> **输入:** arr[] = {2，19，33，48，90，100}，范围= [1，3]
> **输出:** 10
> **说明:**
> 从位置 1 到位置 3 的元素之和为 19 + 33 + 48 = 100，是 10 的完美平方。
> 
> **输入:** arr[] = {13，15，30，55，87}，范围= [0，1]
> **输出:** -1

**天真方法:**最简单的方法是迭代子阵，检查子阵的和是否是完美平方。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效法:**对上述方法进行优化，思路是用 [**【二分搜索法】**](https://www.geeksforgeeks.org/binary-search/) 计算子阵之和的平方根。请遵循以下步骤:

1.  计算给定**范围[]** 内子阵列的总和。
2.  现在，用二分搜索法求 0 到 sum 范围内和的平方根。
3.  从开始和最后一个值找到中间元素，并将**中间<sup>2</sup>T3】的值与**总和**进行比较。**
4.  如果**中间<sup>2</sup>T5】的值等于**的和，**找到一个完美的正方形，然后返回中间。**
5.  如果**中间<sup>2</sup>T3】的值大于**之和，**则答案只能位于中间元素之后的范围右侧。所以向右重复，将搜索空间缩小到 **0** 到**中-1**。**
6.  如果**中间<sup>2</sup>T3】的值小于**和**的值，则将搜索空间缩小到**中间+ 1** 到**和。****

下面是上述方法的实现。

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the square
// root of the sum of a subarray in
// a given range
int checkForPerfectSquare(vector<int> arr,
                          int i, int j)
{
    int mid, sum = 0;

    // Calculate the sum of array
    // elements within a given range
    for (int m = i; m <= j; m++) {
        sum += arr[m];
    }

    // Finding the square root
    int low = 0, high = sum / 2;
    while (low <= high) {
        mid = low + (high - low) / 2;

        // If a perfect square is found
        if (mid * mid == sum) {
            return mid;
        }

        // Reduce the search space if
        // the value is greater than sum
        else if (mid * mid > sum) {
            high = mid - 1;
        }

        // Reduce the search space if
        // the value if smaller than sum
        else {
            low = mid + 1;
        }
    }
    return -1;
}

// Driver Code
int main()
{
    // Given Array
    vector<int> arr;
    arr = { 2, 19, 33, 48, 90, 100 };

    // Given range
    int L = 1, R = 3;

    // Function Call
    cout << checkForPerfectSquare(arr, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to calculate the square
// root of the sum of a subarray in
// a given range
static int checkForPerfectSquare(int []arr,
                                 int i, int j)
{
  int mid, sum = 0;

  // Calculate the sum of array
  // elements within a given range
  for (int m = i; m <= j; m++)
  {
    sum += arr[m];
  }

  // Finding the square root
  int low = 0, high = sum / 2;
  while (low <= high)
  {
    mid = low + (high - low) / 2;

    // If a perfect square
    // is found
    if (mid * mid == sum)
    {
      return mid;
    }

    // Reduce the search space
    // if the value is greater
    // than sum
    else if (mid * mid > sum)
    {
      high = mid - 1;
    }

    // Reduce the search space
    // if the value if smaller
    // than sum
    else
    {
      low = mid + 1;
    }
  }
  return -1;
}

// Driver Code
public static void main(String[] args)
{
  // Given Array
  int []arr = {2, 19, 33,
               48, 90, 100};

  // Given range
  int L = 1, R = 3;

  // Function Call
  System.out.print(
         checkForPerfectSquare(arr, L, R));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to calculate the square
# root of the sum of a subarray in
# a given range
def checkForPerfectSquare(arr, i, j):

    mid, sum = 0, 0

    # Calculate the sum of array
    # elements within a given range
    for m in range(i, j + 1):
        sum += arr[m]

    # Finding the square root
    low = 0
    high = sum // 2

    while (low <= high):
        mid = low + (high - low) // 2

        # If a perfect square is found
        if (mid * mid == sum):
            return mid

        # Reduce the search space if
        # the value is greater than sum
        elif (mid * mid > sum):
            high = mid - 1

        # Reduce the search space if
        # the value if smaller than sum
        else:
            low = mid + 1

    return -1

# Driver Code
if __name__ == '__main__':

    # Given Array
    arr = [ 2, 19, 33, 48, 90, 100 ]

    # Given range
    L = 1
    R = 3

    # Function call
    print(checkForPerfectSquare(arr, L, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to calculate the square
// root of the sum of a subarray in
// a given range
static int checkForPerfectSquare(int []arr,
                                 int i, int j)
{
  int mid, sum = 0;

  // Calculate the sum of array
  // elements within a given range
  for (int m = i; m <= j; m++)
  {
    sum += arr[m];
  }

  // Finding the square root
  int low = 0, high = sum / 2;
  while (low <= high)
  {
    mid = low + (high - low) / 2;

    // If a perfect square
    // is found
    if (mid * mid == sum)
    {
      return mid;
    }

    // Reduce the search space
    // if the value is greater
    // than sum
    else if (mid * mid > sum)
    {
      high = mid - 1;
    }

    // Reduce the search space
    // if the value if smaller
    // than sum
    else
    {
      low = mid + 1;
    }
  }
  return -1;
}

// Driver Code
public static void Main(String[] args)
{
  // Given Array
  int []arr = {2, 19, 33,
               48, 90, 100};

  // Given range
  int L = 1, R = 3;

  // Function Call
  Console.Write(checkForPerfectSquare(arr,
                                      L, R));}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to calculate the square
// root of the sum of a subarray in
// a given range
function checkForPerfectSquare(arr, i, j)
{
    let mid, sum = 0;

    // Calculate the sum of array
    // elements within a given range
    for(let m = i; m <= j; m++)
    {
        sum += arr[m];
    }

    // Finding the square root
    let low = 0, high = parseInt(sum / 2);

    while (low <= high)
    {
        mid = low + parseInt((high - low) / 2);

        // If a perfect square is found
        if (mid * mid == sum)
        {
            return mid;
        }

        // Reduce the search space if
        // the value is greater than sum
        else if (mid * mid > sum)
        {
            high = mid - 1;
        }

        // Reduce the search space if
        // the value if smaller than sum
        else
        {
            low = mid + 1;
        }
    }
    return -1;
}

// Driver Code

// Given Array
let arr = [ 2, 19, 33, 48, 90, 100 ];

// Given range
let L = 1, R = 3;

// Function Call
document.write(checkForPerfectSquare(arr, L, R));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(max(log(sum)，N))*
***辅助空间:** O(1)*