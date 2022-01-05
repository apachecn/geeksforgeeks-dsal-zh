# 从给定数组中找到原始数组，其中第 I 个元素是前 I 个元素的平均值

> 原文:[https://www . geesforgeks . org/find-原始数组-从给定数组-其中-with-element-是第一个 i-elements 的平均值/](https://www.geeksforgeeks.org/find-the-original-array-from-given-array-where-ith-element-is-the-average-of-first-i-elements/)

给定一个长度为 **N、**的[数组](https://www.geeksforgeeks.org/array-class-c/) **arr[]** ，任务是找到原始数组，使得给定数组中的每个**和**元素( **arr[i]** )都是原始数组中第一个 **i** 元素的[平均值](https://www.geeksforgeeks.org/calculate-the-average-variance-and-standard-deviation-in-r-programming/)。

**示例:**

> **输入:**arr = { 4 3 3 3 }
> T3】输出:4 2 3 3
> T6】解释: (4) / 1 = 1，(4+2) / 2 = 3，(4+2+3) / 3 = 3，(4+2+3+3) / 4 = 3
> 
> **输入:**arr = { 2 6 8 10 }
> T3】输出:2 10 12 16
> T6】解释: (2) / 1 = 2，(2+10) / 2 = 6，(2+10+12) / 3 = 8，(2+10+12+16) / 4 = 10

**方法:**给定的问题可以使用[数学](https://www.geeksforgeeks.org/mathematical-algorithms/)方法来解决。请遵循以下步骤:

*   初始化一个变量**和**到数组的第一个元素 **arr**
*   [从第二个索引到最后迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** ，每次迭代:
    *   将当前元素**arr【I】**乘以当前索引+ 1 **(i + 1)** ，并从中减去 **sum** 的值
    *   将得到的当前元素添加到变量**和**中
*   修改后返回结果数组，因为它将是原始数组

## C++

```
// C++ implementation for the above approach

#include <iostream>
using namespace std;

// Function to find the original
// array from the modified array
void findOriginal(int arr[], int N)
{

    // Initialize the variable sum
    // with the first element of array
    int sum = arr[0];

    for (int i = 1; i < N; i++) {

        // Calculate original element
        // from average of first i elements
        arr[i] = (i + 1) * arr[i] - sum;

        // Add current element to sum
        sum += arr[i];
    }

    // Print the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver function
int main()
{

    int arr[] = { 2, 6, 8, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Call the function
    findOriginal(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
class GFG
{

  // Function to find the original
  // array from the modified array
  static void findOriginal(int arr[], int N)
  {

      // Initialize the variable sum
      // with the first element of array
      int sum = arr[0];

      for (int i = 1; i < N; i++) {

          // Calculate original element
          // from average of first i elements
          arr[i] = (i + 1) * arr[i] - sum;

          // Add current element to sum
          sum += arr[i];
      }

      // Print the array
      for (int i = 0; i < N; i++) {
          System.out.print(arr[i] + " ");
      }
  }

  // Driver function
  public static void main(String [] args)
  {

      int [] arr = new int [] { 2, 6, 8, 10 };
      int N = arr.length;

      // Call the function
      findOriginal(arr, N);
  }   
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to find the original
# array from the modified array
def findOriginal(arr, N):

    # Initialize the variable sum
    # with the first element of array
    sum = arr[0]

    for i in range(1, N):

        # Calculate original element
        # from average of first i elements
        arr[i] = (i + 1) * arr[i] - sum

        # Add current element to sum
        sum = sum + arr[i]

    # Print the array
    for i in range (0, N):
        print(arr[i], end=" ")

# Driver function

arr= [ 2, 6, 8, 10 ]
N = len(arr)

# Call the function
findOriginal(arr, N)

# This code is contributed by ihritik
```

## C#

```
// C# program for above approach
using System;

class GFG {

    // Function to find the original
    // array from the modified array
    static void findOriginal(int[] arr, int N)
    {

        // Initialize the variable sum
        // with the first element of array
        int sum = arr[0];

        for (int i = 1; i < N; i++) {

            // Calculate original element
            // from average of first i elements
            arr[i] = (i + 1) * arr[i] - sum;

            // Add current element to sum
            sum += arr[i];
        }

        // Print the array
        for (int i = 0; i < N; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 4;
        int[] arr = { 2, 6, 8, 10 };
        findOriginal(arr, N);
    }
}
// This code is contributed by dwivediyash
```

## java 描述语言

```
<script>
// JavaScript implementation for the above approach

// Function to find the original
// array from the modified array
function findOriginal(arr, N)
{

    // Initialize the variable sum
    // with the first element of array
    var sum = arr[0];

    for (var i = 1; i < N; i++) {

        // Calculate original element
        // from average of first i elements
        arr[i] = (i + 1) * arr[i] - sum;

        // Add current element to sum
        sum += arr[i];
    }

    // Print the array
    for (var i = 0; i < N; i++) {
           document.write(arr[i] + " ");
    }
}

// Driver code
var arr = [ 2, 6, 8, 10 ];
var N = arr.length;

// Call the function
findOriginal(arr, N);

// This code is contributed by AnkThon

</script>
```

**Output**

```
2 10 12 16 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)