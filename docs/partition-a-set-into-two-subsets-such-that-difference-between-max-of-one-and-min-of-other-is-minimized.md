# 将一个集合划分为两个子集，使得一个子集的最大值和另一个子集的最小值之间的差异最小

> 原文:[https://www . geesforgeks . org/partition-a-set-in-two-subset-so-max-of-one 和 min-of-other-min-之间的差异被最小化/](https://www.geeksforgeeks.org/partition-a-set-into-two-subsets-such-that-difference-between-max-of-one-and-min-of-other-is-minimized/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是将数组分成两个子集，使得第一个子集的最大值和第二个子集的最小值之间的绝对差值最小。
**举例:**

> **输入:** arr[] = {3，1，2，6，4}
> **输出:** 1
> **解释:**
> 将给定数组拆分为两个子集，A = [1，2，4]，B = [3，6]。第一组的最大值差为 4，第二组的最小值差为 3，它们的差为 1。
> **输入:** arr[] = {2，1，3，2，4，3}
> **输出:** 0
> **解释:**
> 将给定数组拆分为两个子集，A = [1，2，2，3]，B = [3，4]。第一组的最大值差为 3，第二组的最小值差为 3，它们的差为 0。

**方法:**为了解决上述问题，我们必须找到两个整数，使得 **m** 和 **n** 使得第一组的最大值为 **m** ，第二组的最小值为 **n** 。其思想是[按照给定的数组升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，在对数组进行排序后，连续元素之间的最小差就是将数组元素划分为子集后所需的最小差。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to split the array
int splitArray(int arr[], int N)
{
    // Sort the array in increasing order
    sort(arr, arr + N);

    int result = INT_MAX;

    // Calculating the max difference
    // between consecutive elements
    for (int i = 1; i < N; i++) {
        result = min(result,
                     arr[i] - arr[i - 1]);
    }

    // Return the final minimum difference
    return result;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 1, 2, 6, 4 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << splitArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.util.*;
class GFG{

// Function to split the array
static int splitArray(int arr[], int N)
{
    // Sort the array in increasing order
    Arrays.sort(arr);

    int result = Integer.MAX_VALUE;

    // Calculating the max difference
    // between consecutive elements
    for (int i = 1; i < N; i++)
    {
        result = Math.min(result,
                          arr[i] - arr[i - 1]);
    }

    // Return the final minimum difference
    return result;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 3, 1, 2, 6, 4 };

    // Size of array
    int N = arr.length;

    // Function Call
    System.out.print(splitArray(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to split the array
def splitArray(arr, N):

    # Sort the array in increasing
    # order
    arr = sorted(arr)

    result = 10 ** 9

    # Calculating the max difference
    # between consecutive elements
    for i in range(1, N):
        result = min(result, arr[i] - arr[i - 1])

    # Return the final minimum difference
    return result

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 3, 1, 2, 6, 4 ]

    # Size of array
    N = len(arr)

    # Function Call
    print(splitArray(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to split the array
static int splitArray(int []arr, int N)
{
    // Sort the array in increasing order
    Array.Sort(arr);

    int result = Int32.MaxValue;

    // Calculating the max difference
    // between consecutive elements
    for (int i = 1; i < N; i++)
    {
        result = Math.Min(result,
                          arr[i] - arr[i - 1]);
    }

    // Return the final minimum difference
    return result;
}

// Driver Code
public static void Main()
{
    // Given array arr[]
    int []arr = { 3, 1, 2, 6, 4 };

    // Size of array
    int N = arr.Length;

    // Function Call
    Console.Write(splitArray(arr, N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to split the array
    function splitArray(arr, N)
    {
        // Sort the array in increasing order
        arr.sort();

        let result = Number.MAX_VALUE;

        // Calculating the max difference
        // between consecutive elements
        for (let i = 1; i < N; i++) {
            result = Math.min(result,
                         arr[i] - arr[i - 1]);
        }

        // Return the final minimum difference
        return result;
    }

    // Given array arr[]
    let arr = [ 3, 1, 2, 6, 4 ];

    // Size of array
    let N = arr.length;

    // Function Call
    document.write(splitArray(arr, N));

</script>
```

**Output:** 

```
1
```

**时间复杂度:**T2【O(N * log N)T4】