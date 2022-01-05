# 重新排列数组元素，使所有前缀数组的 MEX 之和最大化

> 原文:[https://www . geesforgeks . org/重排数组元素以最大化所有前缀数组的 mex 总和/](https://www.geeksforgeeks.org/rearrange-array-elements-to-maximize-the-sum-of-mex-of-all-prefix-arrays/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是重新排列数组元素，使得所有前缀数组的 [MEX](https://www.geeksforgeeks.org/construct-mex-array-from-the-given-array/) 之和最大。

***注:**序列的 MEX 是序列中不存在的最小非负数。*

**示例:**

> **输入:** arr[] = {2，0，1}
> **输出:** 0，1，2
> **解释:**
> 给定数组所有可能排列的所有前缀数组的 Mex 之和:
> arr[] = {0，1，2}，Mex(0) + Mex(0，1) + Mex(0，1，2) = 1 + 2 + 3 = 6
> arr[] = {1，0，2}，MEX 2) = 0 + 2 + 3 = 5
> arr[] = {2，0，1}，Mex(2) + Mex(2，0) + Mex(2，0，1) = 0 + 1 + 3 = 4
> arr[] = {0，2，1}，Mex(0) + Mex(0，2) + Mex(0，2，1) = 1 + 1 + 3 = 5
> arr[] = {1，2，0}，Mex(1)+Mex(0，2，1) Mex(2) + Mex(2，1) + Mex(2，1，0) = 0 + 0 + 3 = 3
> 因此，最大可能和为 6。
> 
> **输入:** arr[] = {1，0，0}
> **输出:** 0，1，0
> **解释:**
> 给定数组所有可能排列的所有前缀数组的 Mex 之和:
> arr[]={1，0，0}，Mex(1) + Mex(1，0) + Mex(1，0，0) = 0 + 2 + 2 = 4
> arr[]={0，1，0}，MEX Mex(0) + Mex(0，0) + Mex(0，0，1) = 1 + 1 + 2 = 4
> 因此，排列的最大值为 5，arr[]={0，1，0}。

**天真方法:**最简单的方法是[生成给定数组的所有可能排列](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)**arr【】**然后对于每个排列，找到所有前缀数组的 [MEX](https://www.geeksforgeeks.org/construct-mex-array-from-the-given-array/) 的值，同时跟踪整体最大值。迭代所有可能的排列后，打印具有最大值的排列。

***时间复杂度:** O(N <sup>2</sup> * N！)*
***辅助空间:** O(N)*

**高效方法:**最优思想是基于这样的观察:当所有不同的元素以递增的顺序排列并且重复出现在数组的末尾时，前缀数组的 MEX 之和将最大。
按照以下步骤解决问题:

*   [初始化一个整数向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **ans，**来存储需要的排列。
*   [按递增顺序排列数组**arr[]**](https://www.geeksforgeeks.org/sort-c-stl/)。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**将所有[异元素](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)推入阵**ans【】**。
*   再次[遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将剩余的[复制元素](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)全部推入阵**ans【】**。
*   完成以上步骤后，打印数组 **ans[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// MEX of prefix arrays for any
// arrangement of the given array
void maximumMex(int arr[], int N)
{

    // Stores the final arrangement
    vector<int> ans;

    // Sort the array in increasing order
    sort(arr, arr + N);

    // Iterate over the array arr[]
    for (int i = 0; i < N; i++) {
        if (i == 0 || arr[i] != arr[i - 1])
            ans.push_back(arr[i]);
    }

    // Iterate over the array, arr[]
    // and push the remaining occurrences
    // of the elements into ans[]
    for (int i = 0; i < N; i++) {
        if (i > 0 && arr[i] == arr[i - 1])
            ans.push_back(arr[i]);
    }

    // Print the array, ans[]
    for (int i = 0; i < N; i++)
        cout << ans[i] << " ";
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 0, 0 };

    // Store the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumMex(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;  

class GFG{

// Function to find the maximum sum of
// MEX of prefix arrays for any
// arrangement of the given array
static void maximumMex(int arr[], int N)
{

    // Stores the final arrangement
    int ans[] = new int[2 * N];

    // Sort the array in increasing order
    Arrays.sort(ans);
    int j = 0;

    // Iterate over the array arr[]
    for(int i = 0; i < N; i++)
    {
        if (i == 0 || arr[i] != arr[i - 1])
        {
            j += 1;
            ans[j] = arr[i];
        }
    }

    // Iterate over the array, arr[]
    // and push the remaining occurrences
    // of the elements into ans[]
    for(int i = 0; i < N; i++)
    {
        if (i > 0 && arr[i] == arr[i - 1])
        {
            j += 1;
            ans[j] = arr[i];
        }
    }

    // Print the array, ans[]
    for(int i = 0; i < N; i++)
        System.out.print(ans[i] + " ");
}

// Driver Code
public static void main (String[] args)
{

    // Given array
    int arr[] = { 1, 0, 0 };

    // Store the size of the array
    int N = arr.length;

    // Function Call
    maximumMex(arr, N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# MEX of prefix arrays for any
# arrangement of the given array
def maximumMex(arr, N):

    # Stores the final arrangement
    ans = []

    # Sort the array in increasing order
    arr = sorted(arr)

    # Iterate over the array arr[]
    for i in range(N):
        if (i == 0 or arr[i] != arr[i - 1]):
            ans.append(arr[i])

    # Iterate over the array, arr[]
    # and push the remaining occurrences
    # of the elements into ans[]
    for i in range(N):
        if (i > 0 and arr[i] == arr[i - 1]):
            ans.append(arr[i])

    # Prthe array, ans[]
    for i in range(N):
        print(ans[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 0, 0 ]

    # Store the size of the array
    N = len(arr)

    # Function Call
    maximumMex(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// MEX of prefix arrays for any
// arrangement of the given array
static void maximumMex(int []arr, int N)
{

    // Stores the final arrangement
    int []ans = new int[2 * N];

    // Sort the array in increasing order
    Array.Sort(ans);
    int j = 0;

    // Iterate over the array arr[]
    for(int i = 0; i < N; i++)
    {
        if (i == 0 || arr[i] != arr[i - 1])
        {
            j += 1;
            ans[j] = arr[i];
        }
    }

    // Iterate over the array, arr[]
    // and push the remaining occurrences
    // of the elements into ans[]
    for(int i = 0; i < N; i++)
    {
        if (i > 0 && arr[i] == arr[i - 1])
        {
            j += 1;
            ans[j] = arr[i];
        }
    }

    // Print the array, ans[]
    for(int i = 0; i < N; i++)
        Console.Write(ans[i] + " ");
}

// Driver Code
public static void Main (string[] args)
{

    // Given array
    int []arr = { 1, 0, 0 };

    // Store the size of the array
    int N = arr.Length;

    // Function Call
    maximumMex(arr, N);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum sum of
// MEX of prefix arrays for any
// arrangement of the given array
function maximumMex(arr, N)
{

    // Stores the final arrangement
    var ans = [];

    // Sort the array in increasing order
    arr.sort();
    var i;
    // Iterate over the array arr[]
    for (i = 0; i < N; i++) {
        if (i == 0 || arr[i] != arr[i - 1])
            ans.push(arr[i]);
    }

    // Iterate over the array, arr[]
    // and push the remaining occurrences
    // of the elements into ans[]
    for (i = 0; i < N; i++) {
        if (i > 0 && arr[i] == arr[i - 1])
            ans.push(arr[i]);
    }

    // Print the array, ans[]
    for (i = 0; i < N; i++)
        document.write(ans[i] + " ");
}

// Driver Code
    // Given array
    var arr = [1, 0, 0];

    // Store the size of the array
    var N = arr.length;

    // Function Call
    maximumMex(arr, N);

</script>
```

**Output:** 

```
0 1 0
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*