# 找到数字 K 最大频率的数组元素

> 原文:[https://www . geeksforgeeks . org/find-the-array-element-having-the-frequency-the-digit-k/](https://www.geeksforgeeks.org/find-the-array-element-having-maximum-frequency-of-the-digit-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K** ，任务是找到一个包含数字 **K** 最大次数的数组元素。如果存在多个解决方案，则打印其中任何一个。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，77，343，456}，K = 3
> **输出:** 343
> **解释:**
> 数组元素中 3 的频率:1，0，2，0
> 343 有最大频率即 2。
> 
> **输入:** arr[] = {1，1111，111，11}，K = 1
> **输出:** 1111
> **解释:**
> 数组元素中 1 的频率:1，4，3，2
> 1111 有最大频率即 4。

**方法:**想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个单独的数组元素，计算数字 **K** 在其中的出现次数。按照以下步骤解决问题:

1.  初始化数字 **K** 的最大频率，说 **maxfreq** ，为 **0** 。
2.  [从开始元素到结束遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
3.  对于每个遍历的元素，求该元素中数字 **K** 的频率。如果大于 **maxfreq** ，则更新 **maxfreq** 并存储该元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// digits, k in the given number n
int countFreq(int N, int K)
{

    // Stores count of occurrence
    // of digit K in N
    int count = 0;

    // Iterate over digits of N
    while (N > 0) {

        // If current digit is k
        if (N % 10 == K) {

            // Update count
            count++;
        }

        // Update N
        N = N / 10;
    }
    return count;
}

// Utility function to find an array element
// having maximum frequency of digit k
int findElementUtil(int arr[], int N, int K)
{

    // Stores frequency of
    // digit K in arr[i]
    int c;

    // Stores maximum frequency of
    // digit K in the array
    int max;

    // Stores an array element having
    // maximum frequency of digit k
    int ele;

    // Initialize max
    max = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Count the frequency of
        // digit k in arr[i]
        c = countFreq(arr[i], K);

        // Update max with maximum
        // frequency found so far
        if (c > max) {
            max = c;

            // Update ele
            ele = arr[i];
        }
    }

    // If there is no array element
    // having digit k in it
    if (max == 0)
        return -1;
    else
        return ele;
}

// Function to find an array element
// having maximum frequency of digit k
void findElement(int arr[], int N, int K)
{

    // Stores an array element having
    // maximum frequency of digit k
    int ele = findElementUtil(arr, N, K);

    // If there is no element found
    // having digit k in it
    if (ele == -1)
        cout << "-1";

    else

        // Print the element having max
        // frequency of digit k
        cout << ele;
}

// Driver Code
int main()
{

    // The digit whose max
    // occurrence has to be found
    int K = 3;

    // Given array
    int arr[] = { 3, 77, 343, 456 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findElement(arr, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the count of
    // digits, k in the given number n
    static int countFreq(int N, int K)
    {

        // Stores count of occurrence
        // of digit K in N
        int count = 0;

        // Iterate over digits of N
        while (N > 0)
        {

            // If current digit is k
            if (N % 10 == K)
            {

                // Update count
                count++;
            }

            // Update N
            N = N / 10;
        }
        return count;
    }

    // Utility function to find an array element
    // having maximum frequency of digit k
    static int findElementUtil(int arr[], int N, int K)
    {

        // Stores frequency of
        // digit K in arr[i]
        int c;

        // Stores maximum frequency of
        // digit K in the array
        int max;

        // Stores an array element having
        // maximum frequency of digit k
        int ele = 0;

        // Initialize max
        max = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Count the frequency of
            // digit k in arr[i]
            c = countFreq(arr[i], K);

            // Update max with maximum
            // frequency found so far
            if (c > max)
            {
                max = c;

                // Update ele
                ele = arr[i];
            }
        }

        // If there is no array element
        // having digit k in it
        if (max == 0)
            return -1;
        else
            return ele;
    }

    // Function to find an array element
    // having maximum frequency of digit k
    static void findElement(int arr[], int N, int K)
    {

        // Stores an array element having
        // maximum frequency of digit k
        int ele = findElementUtil(arr, N, K);

        // If there is no element found
        // having digit k in it
        if (ele == -1)
            System.out.print("-1");

        else

            // Print the element having max
            // frequency of digit k
            System.out.print(ele);
    }

    // Driver Code
    public static void main (String[] args)
    {

        // The digit whose max
        // occurrence has to be found
        int K = 3;

        // Given array
        int arr[] = { 3, 77, 343, 456 };

        // Size of array
        int N = arr.length;

        // Function Call
        findElement(arr, K, N);  
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the count of
# digits, k in the given number n
def countFreq(N, K):

    # Stores count of occurrence
    # of digit K in N
    count = 0

    # Iterate over digits of N
    while (N > 0):

        # If current digit is k
        if (N % 10 == K):

            # Update count
            count += 1

        # Update N
        N = N // 10
    return count

# Utility function to find an array element
# having maximum frequency of digit k
def findElementUtil(arr, N, K):

    # Stores frequency of
    # digit K in arr[i]
    c  = 0

    # Stores maximum frequency of
    # digit K in the array
    max = 0

    # Stores an array element having
    # maximum frequency of digit k
    ele = 0

    # Initialize max
    # max = 0

    # Traverse the array
    for i in range(N):

        # Count the frequency of
        # digit k in arr[i]
        c = countFreq(arr[i], K)

        # Update max with maximum
        # frequency found so far
        if (c > max):
            max = c

            # Update ele
            ele = arr[i]

    # If there is no array element
    # having digit k in it
    if (max == 0):
        return -1
    else:
        return ele

# Function to find an array element
# having maximum frequency of digit k
def findElement(arr, N, K):

    # Stores an array element having
    # maximum frequency of digit k
    ele = findElementUtil(arr, N, K)

    # If there is no element found
    # having digit k in it
    if (ele == -1):
        print("-1", end = "")

    else:

        # Print element having max
        # frequency of digit k
        print(ele)

# Driver Code
if __name__ == '__main__':

    # The digit whose max
    # occurrence has to be found
    K = 3

    # Given array
    arr = [3, 77, 343, 456]

    # Size of array
    N = len(arr)

    # Function Call
    findElement(arr, K, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG {

  // Function to find the count of
  // digits, k in the given number n
  static int countFreq(int N, int K)
  {

    // Stores count of occurrence
    // of digit K in N
    int count = 0;

    // Iterate over digits of N
    while (N > 0)
    {

      // If current digit is k
      if (N % 10 == K)
      {

        // Update count
        count++;
      }

      // Update N
      N = N / 10;
    }
    return count;
  }

  // Utility function to find an array element
  // having maximum frequency of digit k
  static int findElementUtil(int []arr, int N, int K)
  {

    // Stores frequency of
    // digit K in arr[i]
    int c;

    // Stores maximum frequency of
    // digit K in the array
    int max;

    // Stores an array element having
    // maximum frequency of digit k
    int ele = 0;

    // Initialize max
    max = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Count the frequency of
      // digit k in arr[i]
      c = countFreq(arr[i], K);

      // Update max with maximum
      // frequency found so far
      if (c > max)
      {
        max = c;

        // Update ele
        ele = arr[i];
      }
    }

    // If there is no array element
    // having digit k in it
    if (max == 0)
      return -1;
    else
      return ele;
  }

  // Function to find an array element
  // having maximum frequency of digit k
  static void findElement(int []arr, int N, int K)
  {

    // Stores an array element having
    // maximum frequency of digit k
    int ele = findElementUtil(arr, N, K);

    // If there is no element found
    // having digit k in it
    if (ele == -1)
      Console.Write("-1");

    else

      // Print the element having max
      // frequency of digit k
      Console.Write(ele);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // The digit whose max
    // occurrence has to be found
    int K = 3;

    // Given array
    int []arr = { 3, 77, 343, 456 };

    // Size of array
    int N = arr.Length;

    // Function Call
    findElement(arr, K, N);  
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

   // Function to find the count of
    // digits, k in the given number n
    function countFreq(N, K)
    {

        // Stores count of occurrence
        // of digit K in N
        let count = 0;

        // Iterate over digits of N
        while (N > 0)
        {

            // If current digit is k
            if (N % 10 == K)
            {

                // Update count
                count++;
            }

            // Update N
            N = Math.floor(N / 10);
        }
        return count;
    }

    // Utility function to find an array element
    // having maximum frequency of digit k
    function findElementUtil(arr, N, K)
    {

        // Stores frequency of
        // digit K in arr[i]
        let c;

        // Stores maximum frequency of
        // digit K in the array
        let max;

        // Stores an array element having
        // maximum frequency of digit k
        let ele = 0;

        // Initialize max
        max = 0;

        // Traverse the array
        for (let i = 0; i < N; i++)
        {

            // Count the frequency of
            // digit k in arr[i]
            c = countFreq(arr[i], K);

            // Update max with maximum
            // frequency found so far
            if (c > max)
            {
                max = c;

                // Update ele
                ele = arr[i];
            }
        }

        // If there is no array element
        // having digit k in it
        if (max == 0)
            return -1;
        else
            return ele;
    }

    // Function to find an array element
    // having maximum frequency of digit k
    function findElement(arr, N, K)
    {

        // Stores an array element having
        // maximum frequency of digit k
        let ele = findElementUtil(arr, N, K);

        // If there is no element found
        // having digit k in it
        if (ele == -1)
            document.write("-1");

        else

            // Prlet the element having max
            // frequency of digit k
            document.write(ele);
    }

// Driver Code

     // The digit whose max
        // occurrence has to be found
        let K = 3;

        // Given array
        let arr = [ 3, 77, 343, 456 ];

        // Size of array
        let N = arr.length;

        // Function Call
        findElement(arr, K, N); 

    // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
343
```

***时间复杂度:**O(N * log<sub>10</sub>(N))*
***辅助空间:** O(1)*