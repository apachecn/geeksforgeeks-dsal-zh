# 和为完美平方的子阵

> 原文:[https://www . geesforgeks . org/subarrays-其和为完美平方/](https://www.geeksforgeeks.org/subarrays-whose-sum-is-a-perfect-square/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是打印所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的开始和结束索引，其和为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。

**示例**:

> **输入:** arr[] = {65，79，81}
> **输出:** (0，1) (0，2) (2，2)
> **解释:**
> 开始和结束索引为(0，1) = 65 + 79 = 144 = 12 <sup>2</sup>
> 开始和结束索引为(0，2} = 65 + 79 + 81 = 225 = 15 的斯巴瑞总和
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** (0，0) (1，3) (3，3) (3，4)

**方法:**这个问题可以使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术来解决。想法是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)找到所有[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的和。对于每个子阵列，检查子阵列之和是否为[完美平方](https://www.geeksforgeeks.org/check-if-a-given-number-is-a-perfect-square-using-binary-search/)。如果发现任何子阵列为真，则打印该子阵列的开始和结束索引。按照以下步骤解决问题。

1.  初始化一个变量，比如**currenolet**来存储当前子数组的和。
2.  [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)到[生成给定数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能的子数组。
3.  计算每个子阵的和，对于每个子阵和，检查是否是[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。
4.  如果发现任何子阵列为真，则打印子阵列的开始和结束索引。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the start and end
// indices of all subarrays whose sum
// is a perfect square
void PrintIndexes(int arr[], int N)
{

    for (int i = 0; i < N; i++) {

        // Stores the current
        // subarray sum
        int currSubSum = 0;

        for (int j = i; j < N; j++) {

            // Update current subarray sum
            currSubSum += arr[j];

            // Stores the square root
            // of currSubSum
            int sq = sqrt(currSubSum);

            // Check if currSubSum is
            // a perfect square or not
            if (sq * sq == currSubSum) {
                cout << "(" << i << ", "
                     << j << ") ";
            }
        }
    }
}

// Driver Code
int main()
{

    int arr[] = { 65, 79, 81 };
    int N = sizeof(arr) / sizeof(arr[0]);
    PrintIndexes(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to print the start and end
// indices of all subarrays whose sum
// is a perfect square
static void PrintIndexes(int arr[], int N)
{
    for(int i = 0; i < N; i++)
    {

        // Stores the current
        // subarray sum
        int currSubSum = 0;

        for(int j = i; j < N; j++)
        {

            // Update current subarray sum
            currSubSum += arr[j];

            // Stores the square root
            // of currSubSum
            int sq = (int)Math.sqrt(currSubSum);

            // Check if currSubSum is
            // a perfect square or not
            if (sq * sq == currSubSum)
            {
                System.out.print("(" + i + "," +
                                 j + ")" + " ");
            }
        }
    }
}

// Driver code
public static void main (String[] args)
throws java.lang.Exception
{
    int arr[] = { 65, 79, 81 };

    PrintIndexes(arr, arr.length);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to print the start and end
# indices of all subarrays whose sum
# is a perfect square
def PrintIndexes(arr, N):

    for i in range(N):

        # Stores the current
        # subarray sum
        currSubSum = 0

        for j in range(i, N, 1):

            # Update current subarray sum
            currSubSum += arr[j]

            # Stores the square root
            # of currSubSum
            sq = int(math.sqrt(currSubSum))

            # Check if currSubSum is
            # a perfect square or not
            if (sq * sq == currSubSum):
                print("(", i, ",",
                           j, ")", end = " ")

# Driver Code
arr = [ 65, 79, 81 ]
N = len(arr)

PrintIndexes(arr, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to print the start
// and end indices of all
// subarrays whose sum
// is a perfect square
static void PrintIndexes(int []arr,
                         int N)
{
  for(int i = 0; i < N; i++)
  {
    // Stores the current
    // subarray sum
    int currSubSum = 0;

    for(int j = i; j < N; j++)
    {
      // Update current subarray sum
      currSubSum += arr[j];

      // Stores the square root
      // of currSubSum
      int sq = (int)Math.Sqrt(currSubSum);

      // Check if currSubSum is
      // a perfect square or not
      if (sq * sq == currSubSum)
      {
        Console.Write("(" + i + "," +
                      j + ")" + " ");
      }
    }
  }
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {65, 79, 81};
  PrintIndexes(arr, arr.Length);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to print the start and end
// indices of all subarrays whose sum
// is a perfect square
function PrintIndexes(arr, N)
{
    for(let i = 0; i < N; i++)
    {

        // Stores the current
        // subarray sum
        let currSubSum = 0;

        for(let j = i; j < N; j++)
        {

            // Update current subarray sum
            currSubSum += arr[j];

            // Stores the square root
            // of currSubSum
            let sq = Math.floor(Math.sqrt(currSubSum));

            // Check if currSubSum is
            // a perfect square or not
            if (sq * sq == currSubSum)
            {
                document.write("(" + i + "," +
                                 j + ")" + " ");
            }
        }
    }
}

// Driver Code

        let arr = [ 65, 79, 81 ];

    PrintIndexes(arr, arr.length);

</script>
```

**Output:** 

```
(0, 1) (0, 2) (2, 2)
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*