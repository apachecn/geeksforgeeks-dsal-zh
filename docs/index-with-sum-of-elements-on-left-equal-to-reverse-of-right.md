# 找出左边元素和等于右边元素和的倒数的索引

> 原文:[https://www . geesforgeks . org/index-with-sum-of-elements-on-left-equal-to-reverse-of-right/](https://www.geeksforgeeks.org/index-with-sum-of-elements-on-left-equal-to-reverse-of-right/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)， **arr[]** 大小 **N** ，任务是找到数组的最小索引，使得索引左侧所有数组元素的总和等于该索引右侧所有数组元素总和的位数的倒数。如果没有找到这样的索引，则打印 **-1** 。

**示例:**

> **输入:** arr[] = { 5，7，3，6，4，9，2 }
> **输出:** 2
> **解释:**
> 索引 2 左侧数组元素之和= (5 + 7) = 12
> 索引 2 右侧数组元素之和= (6 + 4 + 9 + 2) = 21
> 因为索引 2 左侧数组元素之和等于右侧元素之和位数的倒数因此，所需的输出为 2。
> 
> **输入:** arr[] = { 1，3，6，8，9，2 }
> **输出:** -1

**天真法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个索引，检查索引左侧的元素之和是否等于该索引右侧的数组元素之和[的位数的倒数](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。如果发现是真的，那么打印索引。否则，如果没有找到这样的索引，打印 **-1** 。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用[前缀和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。按照以下步骤解决问题:

*   初始化一个变量，比如 **rightSum** ，将数组元素的[和存储在每个索引的右侧。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   初始化一个变量，比如 **leftSum** ，将数组元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)存储在每个索引的左侧。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，更新 **rightSum -= arr[i]，leftSum += arr[i]** 的值，检查 **leftSum** 是否等于 **rightSum** 的倒数。如果发现为真，则打印 **i** 。
*   否则，打印 **-1** 。

下面是上述方法的实现。

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is equal
// to the reverse of digits of other number
bool checkReverse(int leftSum, int rightSum)
{
    // Stores reverse of
    // digits of rightSum
    int rev = 0;

    // Stores rightSum
    int temp = rightSum;

    // Calculate reverse of
    // digits of temp
    while (temp != 0) {

        // Update rev
        rev = (rev * 10) + (temp % 10);

        // Update temp
        temp /= 10;
    }

    // If reverse of digits of
    // rightSum equal to leftSum
    if (rev == leftSum) {
        return true;
    }

    return false;
}

// Function to find the index
// that satisfies the condition
int findIndex(int arr[], int N)
{

    // Stores sum of array elements
    // on right side of each index
    int rightSum = 0;

    // Stores sum of array elements
    // on left side of each index
    int leftSum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update rightSum
        rightSum += arr[i];
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update rightSum
        rightSum -= arr[i];

        // If leftSum equal to
        // reverse of digits
        // of rightSum
        if (checkReverse(leftSum,
                         rightSum)) {
            return i;
        }

        // Update leftSum
        leftSum += arr[i];
    }

    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 5, 7, 3, 6, 4, 9, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findIndex(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

  // Function to check if a number is equal
  // to the reverse of digits of other number
  static boolean checkReverse(int leftSum, int rightSum)
  {
    // Stores reverse of
    // digits of rightSum
    int rev = 0;

    // Stores rightSum
    int temp = rightSum;

    // Calculate reverse of
    // digits of temp
    while (temp != 0) {

      // Update rev
      rev = (rev * 10) + (temp % 10);

      // Update temp
      temp /= 10;
    }

    // If reverse of digits of
    // rightSum equal to leftSum
    if (rev == leftSum) {
      return true;
    }

    return false;
  }

  // Function to find the index
  // that satisfies the condition
  static int findIndex(int[] arr, int N)
  {

    // Stores sum of array elements
    // on right side of each index
    int rightSum = 0;

    // Stores sum of array elements
    // on left side of each index
    int leftSum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Update rightSum
      rightSum += arr[i];
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Update rightSum
      rightSum -= arr[i];

      // If leftSum equal to
      // reverse of digits
      // of rightSum
      if (checkReverse(leftSum,
                       rightSum)) {
        return i;
      }

      // Update leftSum
      leftSum += arr[i];
    }

    return -1;
  }

  // Driver code
  public static void main(String[] args)
  {

    int[] arr = { 5, 7, 3, 6, 4, 9, 2 };
    int N = arr.length;
    System.out.print(findIndex(arr, N));
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to check if a number is equal
# to the reverse of digits of other number
def checkReverse(leftSum, rightSum):

    # Stores reverse of
    # digits of rightSum
    rev = 0

    # Stores rightSum
    temp = rightSum

    # Calculate reverse of
    # digits of temp
    while (temp != 0):

        # Update rev
        rev = (rev * 10) + (temp % 10)

        # Update temp
        temp //= 10

    # If reverse of digits of
    # rightSum equal to leftSum
    if (rev == leftSum):
        return True

    return False

# Function to find the index
# that satisfies the condition
def findIndex(arr, N):

    # Stores sum of array elements
    # on right side of each index
    rightSum = 0

    # Stores sum of array elements
    # on left side of each index
    leftSum = 0

    # Traverse the array
    for i in range(N):

        # Update rightSum
        rightSum += arr[i]

    # Traverse the array
    for i in range(N):

        # Update rightSum
        rightSum -= arr[i]

        # If leftSum equal to
        # reverse of digits
        # of rightSum
        if (checkReverse(leftSum, rightSum)):
            return i

        # Update leftSum
        leftSum += arr[i]
    return -1

# Driver Code
if __name__ == '__main__':
    arr = [5, 7, 3, 6, 4, 9, 2]
    N =  len(arr)
    print(findIndex(arr, N))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

    // Function to check if a number is equal
    // to the reverse of digits of other number
    static bool checkReverse(int leftSum, int rightSum)
    {
        // Stores reverse of
        // digits of rightSum
        int rev = 0;

        // Stores rightSum
        int temp = rightSum;

        // Calculate reverse of
        // digits of temp
        while (temp != 0) {

            // Update rev
            rev = (rev * 10) + (temp % 10);

            // Update temp
            temp /= 10;
        }

        // If reverse of digits of
        // rightSum equal to leftSum
        if (rev == leftSum) {
            return true;
        }

        return false;
    }

    // Function to find the index
    // that satisfies the condition
    static int findIndex(int[] arr, int N)
    {

        // Stores sum of array elements
        // on right side of each index
        int rightSum = 0;

        // Stores sum of array elements
        // on left side of each index
        int leftSum = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update rightSum
            rightSum += arr[i];
        }

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update rightSum
            rightSum -= arr[i];

            // If leftSum equal to
            // reverse of digits
            // of rightSum
            if (checkReverse(leftSum,
                             rightSum)) {
                return i;
            }

            // Update leftSum
            leftSum += arr[i];
        }

        return -1;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 5, 7, 3, 6, 4, 9, 2 };
    int N = arr.Length;
    Console.Write(findIndex(arr, N));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to check if a number is equal
    // to the reverse of digits of other number
    function checkReverse(leftSum , rightSum) {
        // Stores reverse of
        // digits of rightSum
        var rev = 0;

        // Stores rightSum
        var temp = rightSum;

        // Calculate reverse of
        // digits of temp
        while (temp != 0) {

            // Update rev
            rev = (rev * 10) + (temp % 10);

            // Update temp
            temp = parseInt(temp/10);
        }

        // If reverse of digits of
        // rightSum equal to leftSum
        if (rev == leftSum) {
            return true;
        }

        return false;
    }

    // Function to find the index
    // that satisfies the condition
    function findIndex(arr , N) {

        // Stores sum of array elements
        // on right side of each index
        var rightSum = 0;

        // Stores sum of array elements
        // on left side of each index
        var leftSum = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Update rightSum
            rightSum += arr[i];
        }

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Update rightSum
            rightSum -= arr[i];

            // If leftSum equal to
            // reverse of digits
            // of rightSum
            if (checkReverse(leftSum, rightSum)) {
                return i;
            }

            // Update leftSum
            leftSum += arr[i];
        }

        return -1;
    }

    // Driver code

        var arr = [ 5, 7, 3, 6, 4, 9, 2 ];
        var N = arr.length;
        document.write(findIndex(arr, N));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)