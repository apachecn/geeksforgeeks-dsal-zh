# 用正位“与”找到最大子集的大小

> 原文:[https://www . geeksforgeeks . org/find-最大子集大小的正位与/](https://www.geeksforgeeks.org/find-the-size-of-largest-subset-with-positive-bitwise-and/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到数组 **arr[]** 的最大大小的[子集，数组中有正的](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = [7，13，8，2，3]
> **输出:** 3
> **解释:**
> 具有按位 AND 正的子集是{13，7，3}长度为 3，这是所有可能的子集中最大的长度。
> 
> **输入:**arr[]=【1，2，4，8】
> **输出:** 1

**方法:**给定的问题可以通过[计算所有数组元素的每个对应位位置的设置位数量](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)来解决，然后任何位置的设置位最大数量的计数就是所需子集的最大数量，因为所有这些元素的按位“与”总是正的。按照以下步骤解决给定的问题:

*   初始化一个数组，比如大小为 **32** 的**位[]** ，它存储每个第 I 位位置的设置位的计数。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，说 **arr[i]** 如果在 **arr[i]** 中设置了 **ith 位**，则增加数组**位**中的 **ith 位的频率。**
*   经过以上步骤，[打印数组的最大值](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **位【】**打印子集的最大尺寸。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest possible
// subset having Bitwise AND positive
void largestSubset(int a[], int N)
{
    // Stores the number of set bits
    // at each bit position
    int bit[32] = { 0 };

    // Traverse the given array arr[]
    for (int i = 0; i < N; i++) {

        // Current bit position
        int x = 31;

        // Loop till array element
        // becomes zero
        while (a[i] > 0) {

            // If the last bit is set
            if (a[i] & 1 == 1) {

                // Increment frequency
                bit[x]++;
            }

            // Divide array element by 2
            a[i] = a[i] >> 1;

            // Decrease the bit position
            x--;
        }
    }

    // Size of the largest possible subset
    cout << *max_element(bit, bit + 32);
}

// Driver Code
int main()
{
    int arr[] = { 7, 13, 8, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    largestSubset(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

      static void largestSubset(int a[], int N)
    {

        // Stores the number of set bits
        // at each bit position
        int bit[] = new int[32];

        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Current bit position
            int x = 31;

            // Loop till array element
            // becomes zero
            while (a[i] > 0) {

                // If the last bit is set
                if ((int)(a[i] & 1) == (int)1) {

                    // Increment frequency
                    bit[x]++;
                }

                // Divide array element by 2
                a[i] = a[i] >> 1;

                // Decrease the bit position
                x--;
            }
        }

        // Size of the largest possible subset
        int max = Integer.MIN_VALUE;

        for (int i = 0; i < 32; i++) {
            max = Math.max(max, bit[i]);
        }

        System.out.println(max);
    }

  // Driver code
    public static void main (String[] args)
    {
        int arr[] = {7, 13, 8, 2, 3};
        int N = arr.length;
        largestSubset(arr, N);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the largest possible
# subset having Bitwise AND positive
def largestSubset(a, N):
    # Stores the number of set bits
    # at each bit position
    bit = [0 for i in range(32)]

    # Traverse the given array arr[]
    for i in range(N):
        # Current bit position
        x = 31

        # Loop till array element
        # becomes zero
        while(a[i] > 0):
            # If the last bit is set
            if (a[i] & 1 == 1):

                # Increment frequency
                bit[x] += 1

            # Divide array element by 2
            a[i] = a[i] >> 1

            # Decrease the bit position
            x -= 1

    # Size of the largest possible subset
    print(max(bit))

# Driver Code
if __name__ == '__main__':
    arr = [7, 13, 8, 2, 3]
    N = len(arr)
    largestSubset(arr, N)

    # This code is contributed by ipg016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static void largestSubset(int[] a, int N)
    {

        // Stores the number of set bits
        // at each bit position
        int[] bit = new int[32];

        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Current bit position
            int x = 31;

            // Loop till array element
            // becomes zero
            while (a[i] > 0) {

                // If the last bit is set
                if ((int)(a[i] & 1) == (int)1) {

                    // Increment frequency
                    bit[x]++;
                }

                // Divide array element by 2
                a[i] = a[i] >> 1;

                // Decrease the bit position
                x--;
            }
        }

        // Size of the largest possible subset
        int max = Int32.MinValue;

        for (int i = 0; i < 32; i++) {
            max = Math.Max(max, bit[i]);
        }

        Console.WriteLine(max);
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] arr = { 7, 13, 8, 2, 3 };
        int N = arr.Length;
        largestSubset(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the largest possible
       // subset having Bitwise AND positive
       function largestSubset(a, N)
       {

           // Stores the number of set bits
           // at each bit position
           let bit = new Array(32).fill(0);

           // Traverse the given array arr[]
           for (let i = 0; i < N; i++) {

               // Current bit position
               let x = 31;

               // Loop till array element
               // becomes zero
               while (a[i] > 0) {

                   // If the last bit is set
                   if (a[i] & 1 == 1) {

                       // Increment frequency
                       bit[x]++;
                   }

                   // Divide array element by 2
                   a[i] = a[i] >> 1;

                   // Decrease the bit position
                   x--;
               }
           }

           // Size of the largest possible subset
           let max = Number.MIN_VALUE;

           for (let i = 0; i < 32; i++) {
               max = Math.max(max, bit[i]);
           }

           document.write(max);
       }

       // Driver Code
       let arr = [7, 13, 8, 2, 3];
       let N = arr.length;
       largestSubset(arr, N);

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)