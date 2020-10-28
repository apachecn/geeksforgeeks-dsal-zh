# 计数阵列中的四倍（i，j，k，l），使得 i < j < k < l 和 arr [i] = arr [k]和 arr [j] = arr [ l]

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是计算元组**（i，j，k，l）的数量 给定数组中的**，使得 **i < j < k < l** 和 **arr [i] = arr [k]** 和 **arr [ j] ＝ arr [1]** 。

**示例**：

> **输入**：arr [] = {1、2、1、2、2、2}
> **输出**：4
> **说明**：]满足给定条件的元组为：
> 1）（0，1，2，3）因为 arr [0] = arr [2] = 1 且 arr [1] = arr [3] = 2
> 2）（0，1，2，4），因为 arr [0] = arr [2] = 1 且 arr [1] = arr [4] = 2
> 3）（0，1，2，5） 因为 arr [0] = arr [2] = 1 且 arr [1] = arr [5] = 2
> 4）（1、3、4、5）因为 arr [1] = arr [4] = 2 并且 arr [3] = arr [5] = 2
> 
> **输入**：arr [] = {2，5，2，2，5，4}。
> **输出**：2

**天真的方法**：最简单的方法是生成所有可能的四倍体，并检查给定条件是否成立。 如果发现是真的，则增加最终计数。 打印获得的最终计数。

***时间复杂度**：O（N <sup>4</sup> ）*

***辅助空间**：O（1）*

**高效方法**：为了优化上述方法，其思想是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)。 步骤如下：

1.  对于每个索引 **j** 重复查找一对索引**（j，l）**，使得 **arr [j] = arr [l]** 和 **j < l** 。

2.  使用[哈希表](https://www.geeksforgeeks.org/hash-table-vs-stl-map/)保留索引 **[0，j – 1]** 中存在的所有数组元素的[频率计数。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

3.  在遍历索引 **j** 到 **l** 时，只需将 **j** 和 **l** 之间的每个元素的频率相加即可。

4.  对每个这样可能的索引对**（j，l）**重复此过程。

5.  完成上述步骤后，打印四倍的总数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count total number
// of required tuples
int countTuples(int arr[], int N)
{
    int ans = 0, val = 0;

    // Initialize unordered map
    unordered_map<int, int> freq;

    for (int j = 0; j < N - 2; j++) {
        val = 0;

        // Find the pairs (j, l) such
        // that arr[j] = arr[l] and j < l
        for (int l = j + 1; l < N; l++) {

            // elements are equal
            if (arr[j] == arr[l]) {

                // Update the count
                ans += val;
            }

            // Add the frequency of
            // arr[l] to val
            val += freq[arr[l]];
        }

        // Update the frequency of
        // element arr[j]
        freq[arr[j]]++;
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 1, 2, 2, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countTuples(arr, N);

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG{

// Function to count total number
// of required tuples
static int countTuples(int arr[], 
                       int N)
{
  int ans = 0, val = 0;

  // Initialize unordered map
  HashMap<Integer,
          Integer> freq = new HashMap<Integer,
                                      Integer>();

  for (int j = 0; j < N - 2; j++) 
  {
    val = 0;

    // Find the pairs (j, l) such
    // that arr[j] = arr[l] and j < l
    for (int l = j + 1; l < N; l++) 
    {
      // elements are equal
      if (arr[j] == arr[l]) 
      {
        // Update the count
        ans += val;
      }

      // Add the frequency of
      // arr[l] to val
      if(freq.containsKey(arr[l]))
        val += freq.get(arr[l]);
    }

    // Update the frequency of
    // element arr[j]
    if(freq.containsKey(arr[j]))
    {
      freq.put(arr[j], freq.get(arr[j]) + 1);
    }
    else
    {
      freq.put(arr[j], 1);
    }
  }

  // Return the answer
  return ans;
}

// Driver code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 2, 1, 2, 2, 2};
  int N = arr.length;

  // Function Call
  System.out.print(countTuples(arr, N));
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program for the above approach

# Function to count total number
# of required tuples
def countTuples(arr, N):

    ans = 0
    val = 0

    # Initialize unordered map
    freq = {}

    for j in range(N - 2):
        val = 0

        # Find the pairs (j, l) such
        # that arr[j] = arr[l] and j < l
        for l in range(j + 1, N):

            # Elements are equal
            if (arr[j] == arr[l]):

                # Update the count
                ans += val

            # Add the frequency of
            # arr[l] to val
            if arr[l] in freq:
                val += freq[arr[l]]

        # Update the frequency of
        # element arr[j]
        freq[arr[j]] = freq.get(arr[j], 0) + 1

    # Return the answer
    return ans

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 1, 2, 2, 2 ]

    N = len(arr)

    # Function call
    print(countTuples(arr, N))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count total number
// of required tuples
static int countTuples(int []arr, 
                       int N)
{
    int ans = 0, val = 0;

    // Initialize unordered map
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    for(int j = 0; j < N - 2; j++) 
    {
        val = 0;

        // Find the pairs (j, l) such
        // that arr[j] = arr[l] and j < l
        for(int l = j + 1; l < N; l++) 
        {

            // Elements are equal
            if (arr[j] == arr[l]) 
            {

                // Update the count
                ans += val;
            }

            // Add the frequency of
            // arr[l] to val
            if (freq.ContainsKey(arr[l]))
                val += freq[arr[l]];
        }

        // Update the frequency of
        // element arr[j]
        if (freq.ContainsKey(arr[j]))
        {
            freq[arr[j]] = freq[arr[j]] + 1;
        }
        else
        {
            freq.Add(arr[j], 1);
        }
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 2, 1, 2, 2, 2 };
    int N = arr.Length;

    // Function call
    Console.Write(countTuples(arr, N));
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
4

```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N）*



* * *

* * *



