# 打印排序数组中的所有唯一元素

> 原文:[https://www . geesforgeks . org/print-all-unique-elements-present-in-a-sorted-array/](https://www.geeksforgeeks.org/print-all-unique-elements-present-in-a-sorted-array/)

给定一个大小为 **N、**的[排序的](https://www.geeksforgeeks.org/sorting-algorithms/) [数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是打印[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)中所有**唯一的**元素。

> 如果数组中某个元素的频率为 **1** ，则称该元素为**唯一**。

**示例:**

> **输入:** arr[ ] = {1，1，2，2，3，4，5，5}
> **输出:** 3 4
> **解释:**由于 1，2，5 在数组中出现不止一次，所以不同的元素是 3 和 4。
> 
> **输入:** arr[ ] = {1，2，3，3，3，4，5，6}
> **输出:** 1 2 4 5 6

**方法:**解决问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**只打印那些频率为 **1** 的元素。按照以下步骤解决问题:

*   [迭代数组](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **arr[]** 并初始化一个变量，比如 **cnt = 0，**来计算当前数组元素的频率。
*   由于[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)已经是[排序的](https://www.geeksforgeeks.org/sorting-algorithms/)，检查当前元素是否与前一个元素相同。如果发现是真的，那么更新 **cnt += 1** 。
*   否则，如果 **cnt = 1，**则**打印**元素。否则，**继续**。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all unique
// elements present in a sorted array
void RemoveDuplicates(int arr[], int n)
{

    int i = 0;

    // Traverse the array
    while (i < n) {

        int cur = arr[i];

        // Stores frequency of
        // the current element
        int cnt = 0;

        // Iterate until end of the
        // array is reached or current
        // element is not the same as the
        // previous element
        while (i < n and cur == arr[i]) {
            cnt++;
            i++;
        }

        // If current element is unique
        if (cnt == 1) {

            cout << cur << " ";
        }
    }
}

// Driver Code
int main()
{

    // Given Input
    int arr[] = { 1, 3, 3, 5, 5, 6, 10 };
    int N = 7;

    // Function Call
    RemoveDuplicates(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG
{

  // Function to print all unique
  // elements present in a sorted array
  static void RemoveDuplicates(int arr[], int n)
  {

    int i = 0;

    // Traverse the array
    while (i < n) {

      int cur = arr[i];

      // Stores frequency of
      // the current element
      int cnt = 0;

      // Iterate until end of the
      // array is reached or current
      // element is not the same as the
      // previous element
      while (i < n && cur == arr[i]) {
        cnt++;
        i++;
      }

      // If current element is unique
      if (cnt == 1) {
        System.out.print(cur +" ");
      }
    }
  }

  // Driver Code

  public static void main (String[] args)
  {

    // Given Input
    int arr[] = { 1, 3, 3, 5, 5, 6, 10 };
    int N = 7;

    // Function Call
    RemoveDuplicates(arr, N);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Function to print all unique
# elements present in a sorted array
def RemoveDuplicates(arr, n):
    i = 0
    while i < n:
        cur = arr[i]

        # Stores frequency of
        # the current element
        cnt = 0

        # Iterate until end of the
        # array is reached or current
        # element is not the same as the
        # previous element
        while i < n and cur == arr[i]:
            cnt += 1
            i += 1
        if cnt == 1:
            print(cur, end=" ")

# Driver code
if __name__ == "__main__":

    # Given Input
    arr = [1, 3, 3, 5, 5, 6, 10]
    N = 7

    # Function Call
    RemoveDuplicates(arr, N)

# This code is contributed by Kushagra Bansal
```

## C#

```
// C# Program for the above approach
using System;

class GFG {

    // Function to print all unique
    // elements present in a sorted array
    static void RemoveDuplicates(int[] arr, int n)
    {

        int i = 0;

        // Traverse the array
        while (i < n) {

            int cur = arr[i];

            // Stores frequency of
            // the current element
            int cnt = 0;

            // Iterate until end of the
            // array is reached or current
            // element is not the same as the
            // previous element
            while (i < n && cur == arr[i]) {
                cnt++;
                i++;
            }

            // If current element is unique
            if (cnt == 1) {
                Console.Write(cur + " ");
            }
        }
    }

    // Driver Code

    public static void Main()
    {

        // Given Input
        int[] arr = { 1, 3, 3, 5, 5, 6, 10 };
        int N = 7;

        // Function Call
        RemoveDuplicates(arr, N);
    }
}

// This code is contributed by rishavmahato348.
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to print all unique
       // elements present in a sorted array
       function RemoveDuplicates(arr, n) {

           let i = 0;

           // Traverse the array
           while (i < n) {

               let cur = arr[i];

               // Stores frequency of
               // the current element
               let cnt = 0;

               // Iterate until end of the
               // array is reached or current
               // element is not the same as the
               // previous element
               while (i < n && cur == arr[i]) {
                   cnt++;
                   i++;
               }

               // If current element is unique
               if (cnt == 1) {

                   document.write(cur + " ");
               }
           }
       }

       // Driver Code

       // Given Input
       let arr = [1, 3, 3, 5, 5, 6, 10];
       let N = 7;

       // Function Call
       RemoveDuplicates(arr, N);

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
1 6 10 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)