# 对给定数组 K 次追加生成的序列中的反转进行计数

> 原文:[https://www . geesforgeks . org/count-inversion-in-a-sequence-通过追加给定数组生成-k-times/](https://www.geeksforgeeks.org/count-inversions-in-a-sequence-generated-by-appending-given-array-k-times/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是将给定数组精确追加**K–1**次到它的末尾，并在结果数组中打印出[的倒排总数](https://www.geeksforgeeks.org/counting-inversions/)。

**示例:**

> **输入:** arr[]= {2，1，3}，K = 3
> **输出:** 12
> **解释:**
> 追加数组 arr[]的 2 个副本将 arr[]修改为{2，1，3，2，1，3，2，2，1，3}
> 对(arr[i]，arr[j])，其中 i < j 和 arr[i] > arr[j]为(2，1)、(2，1)、(2，1)、(2，1)
> 
> **输入:** arr[]= {6，2}，K = 2
> **输出:** 3
> **解释:**
> 追加数组 arr[]= {6，2，6，2}
> 对(arr[i]，arr[j])，其中 i < j 和 arr[i] > arr[j]为(6，2)，(6，2)，(6，2)
> 因此，求逆的总数为 3。

**天真方法:**最简单的方法是将给定数组的 **K** 个副本存储在一个向量中，然后，计算得到的向量的逆序计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(K * N)*

**高效方法:**解决这个问题的思路是先找到给定数组中[的逆序总数](https://www.geeksforgeeks.org/counting-inversions/)，比如 **inv** 。然后，计算单个副本中不同元素对的数量，比如 **X** 。现在，通过以下等式计算追加数组的 **K** 个副本后的求逆总数:

> **(inv*K + ((K*(K-1))/2)*X)。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// inversions in K copies of given array
void totalInversions(int arr[],
                     int K, int N)
{
    // Stores count of inversions
    // in the given array
    int inv = 0;

    // Stores the count of pairs
    // of distinct array elements
    int X = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Generate each pair
        for (int j = 0; j < N; j++) {

            // Check for each pair, if the
            // condition is satisfied or not
            if (arr[i] > arr[j] and i < j)
                inv++;

            // If pairs consist of
            // distinct elements
            if (arr[i] > arr[j])
                X++;
        }
    }

    // Count inversion in the sequence
    int totalInv = X * K * (K - 1) / 2
                   + inv * K;

    // Print the answer
    cout << totalInv << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 1, 3 };

    // Given K
    int K = 3;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    totalInversions(arr, K, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

 // Function to count the number of
// inversions in K copies of given array
static void totalInversions(int arr[],
                     int K, int N)
{

    // Stores count of inversions
    // in the given array
    int inv = 0;

    // Stores the count of pairs
    // of distinct array elements
    int X = 0;
    int i, j;

    // Traverse the array
    for (i = 0; i < N; i++)
    {

        // Generate each pair
        for (j = 0; j < N; j++)
        {

            // Check for each pair, if the
            // condition is satisfied or not
            if(arr[i] > arr[j] && i < j)
                inv++;

            // If pairs consist of
            // distinct elements
            if(arr[i] > arr[j])
                X++;
        }
    }

    // Count inversion in the sequence
    int totalInv = X * K * (K - 1) / 2
                   + inv * K;

    // Print the answer
    System.out.println(totalInv);
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int arr[] = { 2, 1, 3 };

    // Given K
    int K = 3;

    // Size of the array
    int N = arr.length;
    totalInversions(arr, K, N);
}
}

// This code is contributed by bgangwar59.
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to count the number of
# inversions in K copies of given array
def totalInversions(arr, K, N) :

    # Stores count of inversions
    # in the given array
    inv = 0

    # Stores the count of pairs
    # of distinct array elements
    X = 0

    # Traverse the array
    for i in range(N):

        # Generate each pair
        for j in range(N):

            # Check for each pair, if the
            # condition is satisfied or not
            if (arr[i] > arr[j] and i < j) :
                inv += 1

            # If pairs consist of
            # distinct elements
            if (arr[i] > arr[j]) :
                X += 1

    # Count inversion in the sequence
    totalInv = X * K * (K - 1) // 2 + inv * K

    # Prthe answer
    print(totalInv)

# Driver Code

# Given array
arr = [ 2, 1, 3 ]

# Given K
K = 3

# Size of the array
N = len(arr)
totalInversions(arr, K, N)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

  // Function to count the number of
  // inversions in K copies of given array
  static void totalInversions(int []arr,
                              int K, int N)
  {

    // Stores count of inversions
    // in the given array
    int inv = 0;

    // Stores the count of pairs
    // of distinct array elements
    int X = 0;
    int i, j;

    // Traverse the array
    for (i = 0; i < N; i++)
    {

      // Generate each pair
      for (j = 0; j < N; j++)
      {

        // Check for each pair, if the
        // condition is satisfied or not
        if(arr[i] > arr[j] && i < j)
          inv++;

        // If pairs consist of
        // distinct elements
        if(arr[i] > arr[j])
          X++;
      }
    }

    // Count inversion in the sequence
    int totalInv = X * K * (K - 1) / 2
      + inv * K;

    // Print the answer
    Console.WriteLine(totalInv);
  }

  // Driver Code
  public static void  Main()
  {

    // Given array
    int []arr = { 2, 1, 3 };

    // Given K
    int K = 3;

    // Size of the array
    int N = arr.Length;
    totalInversions(arr, K, N);
  }
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

 // Function to count the number of
// inversions in K copies of given array
function totalInversions(arr, K, N)
{

    // Stores count of inversions
    // in the given array
    let inv = 0;

    // Stores the count of pairs
    // of distinct array elements
    let X = 0;
    let i, j;

    // Traverse the array
    for (i = 0; i < N; i++)
    {

        // Generate each pair
        for (j = 0; j < N; j++)
        {

            // Check for each pair, if the
            // condition is satisfied or not
            if(arr[i] > arr[j] && i < j)
                inv++;

            // If pairs consist of
            // distinct elements
            if(arr[i] > arr[j])
                X++;
        }
    }

    // Count inversion in the sequence
    let totalInv = X * K * (K - 1) / 2
                   + inv * K;

    // Print the answer
    document.write(totalInv);
}

// Driver Code

    // Given array
    let arr = [ 2, 1, 3 ];

    // Given K
    let K = 3;

    // Size of the array
    let N = arr.length;
    totalInversions(arr, K, N);

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*