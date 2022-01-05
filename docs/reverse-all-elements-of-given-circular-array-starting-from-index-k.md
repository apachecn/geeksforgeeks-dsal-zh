# 从索引 K 开始反转给定圆形数组的所有元素

> 原文:[https://www . geesforgeks . org/reverse-给定循环数组的所有元素-从索引-k 开始/](https://www.geeksforgeeks.org/reverse-all-elements-of-given-circular-array-starting-from-index-k/)

给定一个大小为 **N** 的[圆形数组](https://www.geeksforgeeks.org/circular-array/)**arr【】**和一个索引 **K** ，任务是[从索引 **K** 开始反转圆形数组的所有元素](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)。

**示例:**

> ***输入:** arr[] = {3，5，2，4，1}，K = 2*
> ***输出:*** 4 2 5 3 1
> ***解释:***
> *将数组的元素从索引 K 反转为 K–1 后，修改后的 arr[]为{4，1，2，5，3}* 。
> 
> ***输入:** arr[] = {1，2，3，4，5}，K = 4*
> ***输出:** 3 2 1 5 4*
> ***解释:***
> *将数组的元素从索引 K 反转为 K–1 后，修改后的 arr[]为{3，2，1，5，4}* 。

**逼近:**解决给定问题，思路是用[两点逼近](https://www.geeksforgeeks.org/two-pointers-technique/)。按照以下步骤解决问题:

*   初始化三个变量**开始**为 **K** ，**结束**为**(K–1)**，使用**两个指针**接近来跟踪边界，并且**计数**为 **N / 2** 。
*   迭代直到**计数**的值为正，并执行以下步骤:
    *   [交换](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)元素 **arr【开始% N】**和 **arr【结束% N】**。
    *   通过 **1** 增加**开始**，通过 **1** 减少**结束**。如果 **end** 等于 **-1** ，则更新 **end** 为**(N–1)**。
    *   将**计数**减 1。
*   完成上述步骤后，打印上述步骤后获得的更新数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array arr[]
void printArray(int arr[], int N)
{
    // Print the array
    for (int i = 0; i < N; i++)
    {
        cout << arr[i] << " ";
    }
}

// Function to reverse elements of given
// circular array starting from index k
void reverseCircularArray(int arr[],
                          int N, int K)
{
    // Initialize two variables as
    // start = k and end = k-1
    int start = K, end = K - 1;

    // Initialize count = N/2
    int count = N / 2;

    // Loop while count > 0
    while (count--) {

        // Swap the elements at index
        // (start%N) and (end%N)
        int temp = arr[start % N];
        arr[start % N] = arr[end % N];
        arr[end % N] = temp;

        // Update the start and end
        start++;
        end--;

        // If end equals to -1
        // set end = N-1
        if (end == -1) {
            end = N - 1;
        }
    }

    // Print the circular array
    printArray(arr, N);
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 2, 4, 1 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    reverseCircularArray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

  // Function to print the array arr[]
  static void printArray(int arr[], int N)
  {

    // Print the array
    for (int i = 0; i < N; i++)
    {
      System.out.print(arr[i] + " ");
    }
  }

  // Function to reverse elements of given
  // circular array starting from index k
  static void reverseCircularArray(int arr[],
                                   int N, int K)
  {

    // Initialize two variables as
    // start = k and end = k-1
    int start = K, end = K - 1;

    // Initialize count = N/2
    int count = N / 2;

    // Loop while count > 0
    while (count != 0)
    {

      // Swap the elements at index
      // (start%N) and (end%N)
      int temp = arr[start % N];
      arr[start % N] = arr[end % N];
      arr[end % N] = temp;

      // Update the start and end
      start++;
      end--;

      // If end equals to -1
      // set end = N-1
      if (end == -1)
      {
        end = N - 1;
      }           
      count -= 1;
    }

    // Print the circular array
    printArray(arr, N);
  }

  // Driver Code
  public static void main (String[] args)
  {
    int arr[] = { 3, 5, 2, 4, 1 };
    int K = 2;
    int N = arr.length;

    // Function Call
    reverseCircularArray(arr, N, K);  
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print array arr[]
def printArray(arr, N):

    # Print the array
    for i in range(N):
        print(arr[i], end = " ")

# Function to reverse elements of given
# circular array starting from index k
def reverseCircularArray(arr, N, K):

    # Initialize two variables as
    # start = k and end = k-1
    start, end = K, K - 1

    # Initialize count = N/2
    count = N // 2

    # Loop while count > 0
    while (count):

        # Swap the elements at index
        # (start%N) and (end%N)
        temp = arr[start % N]
        arr[start % N] = arr[end % N]
        arr[end % N] = temp

        # Update the start and end
        start += 1
        end -= 1

        # If end equals to -1
        # set end = N-1
        if (end == -1):
            end = N - 1

        count -= 1

    # Print the circular array
    printArray(arr, N)

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 5, 2, 4, 1 ]
    K = 2
    N = len(arr)

    # Function Call
    reverseCircularArray(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to print the array []arr
  static void printArray(int []arr, int N)
  {

    // Print the array
    for (int i = 0; i < N; i++)
    {
      Console.Write(arr[i] + " ");
    }
  }

  // Function to reverse elements of given
  // circular array starting from index k
  static void reverseCircularArray(int []arr,
                                   int N, int K)
  {

    // Initialize two variables as
    // start = k and end = k-1
    int start = K, end = K - 1;

    // Initialize count = N/2
    int count = N / 2;

    // Loop while count > 0
    while (count != 0)
    {

      // Swap the elements at index
      // (start%N) and (end%N)
      int temp = arr[start % N];
      arr[start % N] = arr[end % N];
      arr[end % N] = temp;

      // Update the start and end
      start++;
      end--;

      // If end equals to -1
      // set end = N-1
      if (end == -1)
      {
        end = N - 1;
      }           
      count -= 1;
    }

    // Print the circular array
    printArray(arr, N);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 3, 5, 2, 4, 1 };
    int K = 2;
    int N = arr.Length;

    // Function Call
    reverseCircularArray(arr, N, K);  
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the array arr[]
function printArray(arr, N)
{
    // Print the array
    for (let i = 0; i < N; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Function to reverse elements of given
// circular array starting from index k
function reverseCircularArray(arr, N, K)
{
    // Initialize two variables as
    // start = k and end = k-1
    let start = K, end = K - 1;

    // Initialize count = N/2
    let count = Math.floor(N / 2);

    // Loop while count > 0
    while (count--) {

        // Swap the elements at index
        // (start%N) and (end%N)
        let temp = arr[start % N];
        arr[start % N] = arr[end % N];
        arr[end % N] = temp;

        // Update the start and end
        start++;
        end--;

        // If end equals to -1
        // set end = N-1
        if (end === -1) {
            end = N - 1;
        }
    }

    // Print the circular array
    printArray(arr, N);
}

// Driver Code
    let arr = [ 3, 5, 2, 4, 1 ];
    let K = 2;
    let N = arr.length;

    // Function Call
    reverseCircularArray(arr, N, K);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
4 2 5 3 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)