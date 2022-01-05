# 通过交换不相等的元素对来检查一个数组是否可以转换成另一个给定的数组

> 原文:[https://www . geesforgeks . org/check-如果一个数组可以通过交换成对的不相等元素来转换成另一个给定的数组/](https://www.geeksforgeeks.org/check-if-an-array-can-be-converted-to-another-given-array-by-swapping-pairs-of-unequal-elements/)

给定两个由二进制整数组成的大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr 1【】**和**arr 2【】**，任务是通过交换任意一对数组元素 **(arr1[i]，arr1[j])** 来检查**arr 1【】**是否可以转换为**arr 2【】**，使得 **i < j** 和 **arr1[i]如果可以，则打印**“是”**。否则，打印**“否”**。**

**示例:**

> **输入:** arr1[] = {0，1，1，0}，arr2[] = {0，0 1，1}
> **输出:**是
> **解释:**
> 通过交换 arr1[1]和 arr1[3]可以使数组 arr1[]等于 arr2[]。
> 
> **输入:** arr1[] = {1，0，1}，arr2[] = {0，1，0}
> **输出:**否

**方法:**解决这个问题的思路基于以下观察:

*   该操作不改变数组**arr 1【】**中 1 和 0 的个数出现的频率，所以如果数组之间 **0s** 或 **1s** 的个数不同时，就永远无法与上述操作相等。
*   如果 **arr2[]** 的某些前缀包含的 **1s** 比相同长度的 **arr1[]** 的前缀多，则不可能使 **arr1[]** 和 **arr2[]** 相等，因为 **1** 只能向右移动。
*   否则，在所有其他情况下，可以使数组相等。

按照以下步骤解决问题:

*   初始化一个变量，用 **0** 表示**计数**，存储 **arr1[]** 和 **arr2[]** 的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的差值。
*   [统计两个数组中 **1s**](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/) 和 **0s** 的个数，检查**arr 1【】**中 **1s** 和 **0s** 的个数是否与**arr 2【】**中 **1s** 和 **0s** 的个数不相等，然后打印**“否”**。
*   使用变量 **i** 迭代范围**【1，N–1】**，并执行以下操作:
    *   将值**(arr 1[I]–arr 2[I])**添加到变量**计数**中。
    *   如果计数值小于 **0** ，则打印**“否”**否则[继续下一对元素](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   完成上述步骤后，如果任何一步计数都不是负数，则打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if arr1[] can be
// converted to arr2[] by swapping pair
// (i, j) such that i < j and arr[i] is
// 1 and arr[j] is 0
void canMakeEqual(int arr1[], int arr2[], int N)
{
    // Stores the differences of prefix
    // sum of arr1 and arr2
    int count = 0;

    // Stores the count of 1 and
    // zero of arr1
    int arr1_one = 0, arr1_zero = 0;

    // Stores the count of 1 and
    // zero of arr2
    int arr2_one = 0, arr2_zero = 0;

    // Iterate in the range [0, N - 1]
    for (int i = 0; i < N; i++) {

        // If arr1[i] is 1, then
        // increment arr1_one by one
        if (arr1[i] == 1) {
            arr1_one++;
        }

        // Otherwise increment
        // arr1_zero by one
        else if (arr1[i] == 0) {
            arr1_zero++;
        }

        // If arr2[i] is 1, then
        // increment arr2_one by one
        if (arr2[i] == 1) {
            arr2_one++;
        }

        // Otherwise increment
        // arr2_zero by one
        else if (arr2[i] == 0) {
            arr2_zero++;
        }
    }

    // Check if number of 1s and 0s
    // of arr1 is equal to number of
    // 1s and 0s of arr2 respectievly
    if (arr1_one != arr2_one || arr1_zero != arr2_zero) {
        cout << "No";
        return;
    }

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {

        // Increment count by differences
        // arr1[i] and arr2[i]
        count = count + (arr1[i] - arr2[i]);

        // Check if number of 1's in
        // arr2 are more than arr1 and
        // then print "No"
        if (count < 0) {
            cout << "No";
            return;
        }
    }

    // Finally, print "Yes"
    cout << "Yes";
}

// Driver Code
int main()
{
    // Given input arrays
    int arr1[] = { 0, 1, 1, 0 };
    int arr2[] = { 0, 0, 1, 1 };

    // Size of the array
    int N = sizeof(arr1) / sizeof(arr1[0]);

    // Function Call
    canMakeEqual(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to check if arr1[] can be
  // converted to arr2[] by swapping pair
  // (i, j) such that i < j and arr[i] is
  // 1 and arr[j] is 0
  static void canMakeEqual(int []arr1, int []arr2, int N)
  {

    // Stores the differences of prefix
    // sum of arr1 and arr2
    int count = 0;

    // Stores the count of 1 and
    // zero of arr1
    int arr1_one = 0, arr1_zero = 0;

    // Stores the count of 1 and
    // zero of arr2
    int arr2_one = 0, arr2_zero = 0;

    // Iterate in the range [0, N - 1]
    for (int i = 0; i < N; i++) {

      // If arr1[i] is 1, then
      // increment arr1_one by one
      if (arr1[i] == 1) {
        arr1_one++;
      }

      // Otherwise increment
      // arr1_zero by one
      else if (arr1[i] == 0) {
        arr1_zero++;
      }

      // If arr2[i] is 1, then
      // increment arr2_one by one
      if (arr2[i] == 1) {
        arr2_one++;
      }

      // Otherwise increment
      // arr2_zero by one
      else if (arr2[i] == 0) {
        arr2_zero++;
      }
    }

    // Check if number of 1s and 0s
    // of arr1 is equal to number of
    // 1s and 0s of arr2 respectievly
    if (arr1_one != arr2_one || arr1_zero != arr2_zero) {
      System.out.print("No");
      return;
    }

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {

      // Increment count by differences
      // arr1[i] and arr2[i]
      count = count + (arr1[i] - arr2[i]);

      // Check if number of 1's in
      // arr2 are more than arr1 and
      // then print "No"
      if (count < 0) {
        System.out.print("No");
        return;
      }
    }

    // Finally, print "Yes"
    System.out.print("Yes");
  }

// Driver Code
public static void main(String[] args)
{

    // Given input arrays
    int []arr1 = { 0, 1, 1, 0 };
    int []arr2 = { 0, 0, 1, 1 };

    // Size of the array
    int N = arr1.length;

    // Function Call
    canMakeEqual(arr1, arr2, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if arr1[] can be
# converted to arr2[] by swapping pair
# (i, j) such that i < j and arr[i] is
# 1 and arr[j] is 0
def canMakeEqual(arr1, arr2, N):

    # Stores the differences of prefix
    # sum of arr1 and arr2
    count = 0

    # Stores the count of 1 and
    # zero of arr1
    arr1_one = 0
    arr1_zero = 0

    # Stores the count of 1 and
    # zero of arr2
    arr2_one = 0
    arr2_zero = 0

    # Iterate in the range [0, N - 1]
    for i in range(N):

        # If arr1[i] is 1, then
        # increment arr1_one by one
        if (arr1[i] == 1):
            arr1_one += 1

        # Otherwise increment
        # arr1_zero by one
        elif(arr1[i] == 0):
            arr1_zero += 1

        # If arr2[i] is 1, then
        # increment arr2_one by one
        if (arr2[i] == 1):
            arr2_one += 1

        # Otherwise increment
        # arr2_zero by one
        elif (arr2[i] == 0):
            arr2_zero += 1

    # Check if number of 1s and 0s
    # of arr1 is equal to number of
    # 1s and 0s of arr2 respectievly
    if (arr1_one != arr2_one or arr1_zero != arr2_zero):
        print("No")
        return

    # Iterate over the range [0, N-1]
    for i in range(N):

        # Increment count by differences
        # arr1[i] and arr2[i]
        count = count + (arr1[i] - arr2[i])

        # Check if number of 1's in
        # arr2 are more than arr1 and
        # then print "No"
        if (count < 0):
            print("No")
            return

    # Finally, print "Yes"
    print("Yes")

# Driver Code
if __name__ == '__main__':

    # Given input a
    arr1 =  [0, 1, 1, 0]
    arr2 =  [0, 0, 1, 1]

    # Size of the array
    N = len(arr1)

    # Function Call
    canMakeEqual(arr1, arr2, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to check if arr1[] can be
  // converted to arr2[] by swapping pair
  // (i, j) such that i < j and arr[i] is
  // 1 and arr[j] is 0
  static void canMakeEqual(int []arr1, int []arr2, int N)
  {

    // Stores the differences of prefix
    // sum of arr1 and arr2
    int count = 0;

    // Stores the count of 1 and
    // zero of arr1
    int arr1_one = 0, arr1_zero = 0;

    // Stores the count of 1 and
    // zero of arr2
    int arr2_one = 0, arr2_zero = 0;

    // Iterate in the range [0, N - 1]
    for (int i = 0; i < N; i++) {

      // If arr1[i] is 1, then
      // increment arr1_one by one
      if (arr1[i] == 1) {
        arr1_one++;
      }

      // Otherwise increment
      // arr1_zero by one
      else if (arr1[i] == 0) {
        arr1_zero++;
      }

      // If arr2[i] is 1, then
      // increment arr2_one by one
      if (arr2[i] == 1) {
        arr2_one++;
      }

      // Otherwise increment
      // arr2_zero by one
      else if (arr2[i] == 0) {
        arr2_zero++;
      }
    }

    // Check if number of 1s and 0s
    // of arr1 is equal to number of
    // 1s and 0s of arr2 respectievly
    if (arr1_one != arr2_one || arr1_zero != arr2_zero) {
      Console.WriteLine("No");
      return;
    }

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {

      // Increment count by differences
      // arr1[i] and arr2[i]
      count = count + (arr1[i] - arr2[i]);

      // Check if number of 1's in
      // arr2 are more than arr1 and
      // then print "No"
      if (count < 0) {
        Console.WriteLine("No");
        return;
      }
    }

    // Finally, print "Yes"
    Console.WriteLine("Yes");
  }

  // Driver Code
  public static void Main()
  {

    // Given input arrays
    int []arr1 = { 0, 1, 1, 0 };
    int []arr2 = { 0, 0, 1, 1 };

    // Size of the array
    int N = arr1.Length;

    // Function Call
    canMakeEqual(arr1, arr2, N);
  }

}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if arr1[] can be
// converted to arr2[] by swapping pair
// (i, j) such that i < j and arr[i] is
// 1 and arr[j] is 0
function canMakeEqual(arr1, arr2, N)
{

    // Stores the differences of prefix
    // sum of arr1 and arr2
    var count = 0;

    // Stores the count of 1 and
    // zero of arr1
    var arr1_one = 0, arr1_zero = 0;

    // Stores the count of 1 and
    // zero of arr2
    var arr2_one = 0, arr2_zero = 0;

    // Iterate in the range [0, N - 1]
    for(var i = 0; i < N; i++)
    {

        // If arr1[i] is 1, then
        // increment arr1_one by one
        if (arr1[i] == 1)
        {
            arr1_one++;
        }

        // Otherwise increment
        // arr1_zero by one
        else if (arr1[i] == 0)
        {
            arr1_zero++;
        }

        // If arr2[i] is 1, then
        // increment arr2_one by one
        if (arr2[i] == 1)
        {
            arr2_one++;
        }

        // Otherwise increment
        // arr2_zero by one
        else if (arr2[i] == 0)
        {
            arr2_zero++;
        }
    }

    // Check if number of 1s and 0s
    // of arr1 is equal to number of
    // 1s and 0s of arr2 respectievly
    if (arr1_one != arr2_one ||
        arr1_zero != arr2_zero)
    {
        document.write( "No");
        return;
    }

    // Iterate over the range [0, N-1]
    for(var i = 0; i < N; i++)
    {

        // Increment count by differences
        // arr1[i] and arr2[i]
        count = count + (arr1[i] - arr2[i]);

        // Check if number of 1's in
        // arr2 are more than arr1 and
        // then print "No"
        if (count < 0)
        {
            document.write( "No");
            return;
        }
    }

    // Finally, print "Yes"
    document.write("Yes");
}

// Driver Code

// Given input arrays
var arr1 = [ 0, 1, 1, 0 ];
var arr2 = [ 0, 0, 1, 1 ];

// Size of the array
var N = arr1.length;

// Function Call
canMakeEqual(arr1, arr2, N);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)