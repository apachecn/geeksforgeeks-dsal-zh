# 计算所需的顺时针数组旋转，以最大化索引与其值相同的数组元素的数量

> 原文:[https://www . geeksforgeeks . org/count-顺时针-数组-旋转-需要最大化数组元素的计数-出现在索引处-与它们的值相同/](https://www.geeksforgeeks.org/count-clockwise-array-rotations-required-to-maximize-count-of-array-elements-present-at-indices-same-as-their-value/)

给定一个由第一个 **N 个**自然数的[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到数组中最少数量的[顺时针圆周旋转](https://www.geeksforgeeks.org/array-rotation/)，以最大化满足条件 **arr[i] = i** ( *基于 1 的索引*)的元素数量，其中 **1 ≤ i ≤ N** 。

**示例:**

> **输入:** arr[] = {4，5，1，2，3}
> **输出:** 3
> **解释:**旋转数组三次，数组修改为{1，2，3，4，5}。所有数组元素都满足条件 arr[i] = i。
> 
> **输入:** arr[] = {3，4，1，5，2}
> **输出:** 2
> **解释:**旋转数组两次，数组修改为{5，2，3，4，1}。三个数组元素满足条件 arr[i] = i，这是给定数组的最大可能值。

**方法:**按照以下步骤解决问题:

*   初始化两个整数 **maxi** 和 **ans** ，以及两个数组 **new_arr[]** 和 **freq[]** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**对于每个元素，计算将其与其正确位置分开的索引数，即**|(arr[I]–I+N)% N |**。
*   将每个数组元素的计数存储在新数组 **new_arr[]** 中。
*   将**new _ arr【】**中各元素的[频率计数存储在数组**freq【】**中。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   打印最大频率的元素作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// clockwise array rotations required
// to maximize count of array elements
// present at indices same as their value
void find_min_rot(int arr[], int n)
{
    // Stores count of indices separating
    // elements from its correct position
    int new_arr[n + 1];
    int maxi = 1, ans = 0;

    // Stores frequencies of counts of
    // indices separating
    int freq[n + 1];
    for (int i = 1; i <= n; i++) {
        freq[i] = 0;
    }

    // Count indices separating each
    // element from its correct position
    for (int i = 1; i <= n; i++) {

        new_arr[i] = (arr[i] - i + n) % n;
    }

    // Update frequencies of counts obtained
    for (int i = 1; i <= n; i++) {

        freq[new_arr[i]]++;
    }

    // Find the count with maximum frequency
    for (int i = 1; i <= n; i++) {
        if (freq[i] > maxi) {
            maxi = freq[i];
            ans = i;
        }
    }

    // Print the answer
    cout << ans << endl;
}

// Driver Code
int main()
{

    int N = 5;
    int arr[] = { -1, 3, 4, 1, 5, 2 };

    // Find minimum number of
    // array rotations required
    find_min_rot(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number of
// clockwise array rotations required
// to maximize count of array elements
// present at indices same as their value
static void find_min_rot(int arr[], int n)
{

    // Stores count of indices separating
    // elements from its correct position
    int[] new_arr = new int[n + 1];
    int maxi = 1, ans = 0;

    // Stores frequencies of counts of
    // indices separating
    int[] freq = new int[n + 1];
    for(int i = 1; i <= n; i++)
    {
        freq[i] = 0;
    }

    // Count indices separating each
    // element from its correct position
    for(int i = 1; i <= n; i++)
    {
        new_arr[i] = (arr[i] - i + n) % n;
    }

    // Update frequencies of counts obtained
    for(int i = 1; i <= n; i++)
    {
        freq[new_arr[i]]++;
    }

    // Find the count with maximum frequency
    for(int i = 1; i <= n; i++)
    {
        if (freq[i] > maxi)
        {
            maxi = freq[i];
            ans = i;
        }
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int[] arr = { -1, 3, 4, 1, 5, 2 };

    // Find minimum number of
    // array rotations required
    find_min_rot(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# clockwise array rotations required
# to maximize count of array elements
# present at indices same as their value
def find_min_rot(arr, n):

    # Stores count of indices separating
    # elements from its correct position
    new_arr = [0] * (n + 1)
    maxi = 1
    ans = 0

    # Stores frequencies of counts of
    # indices separating
    freq = [0] * (n + 1)
    for i in range(1, n + 1):
        freq[i] = 0

    # Count indices separating each
    # element from its correct position
    for i in range(1, n + 1):
         new_arr[i] = (arr[i] - i + n) % n

    # Update frequencies of counts obtained
    for i in range(1, n + 1):
        freq[new_arr[i]] += 1

    # Find the count with maximum frequency
    for i in range(1, n + 1):
        if (freq[i] > maxi):
            maxi = freq[i]
            ans = i

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    N = 5
    arr = [ -1, 3, 4, 1, 5, 2 ]

    # Find minimum number of
    # array rotations required
    find_min_rot(arr, N)

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to count the number of
// clockwise array rotations required
// to maximize count of array elements
// present at indices same as their value
static void find_min_rot(int []arr, int n)
{

    // Stores count of indices separating
    // elements from its correct position
    int[] new_arr = new int[n + 1];
    int maxi = 1, ans = 0;

    // Stores frequencies of counts of
    // indices separating
    int[] freq = new int[n + 1];
    for(int i = 1; i <= n; i++)
    {
        freq[i] = 0;
    }

    // Count indices separating each
    // element from its correct position
    for(int i = 1; i <= n; i++)
    {
        new_arr[i] = (arr[i] - i + n) % n;
    }

    // Update frequencies of counts obtained
    for(int i = 1; i <= n; i++)
    {
        freq[new_arr[i]]++;
    }

    // Find the count with maximum frequency
    for(int i = 1; i <= n; i++)
    {
        if (freq[i] > maxi)
        {
            maxi = freq[i];
            ans = i;
        }
    }

    // Print the answer
    Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;
    int[] arr = { -1, 3, 4, 1, 5, 2 };

    // Find minimum number of
    // array rotations required
    find_min_rot(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to count the number of
// clockwise array rotations required
// to maximize count of array elements
// present at indices same as their value
function find_min_rot(arr, n)
{

    // Stores count of indices separating
    // elements from its correct position
    let new_arr = [];
    let maxi = 1, ans = 0;

    // Stores frequencies of counts of
    // indices separating
    let freq = [];
    for(let i = 1; i <= n; i++)
    {
        freq[i] = 0;
    }

    // Count indices separating each
    // element from its correct position
    for(let i = 1; i <= n; i++)
    {
        new_arr[i] = (arr[i] - i + n) % n;
    }

    // Update frequencies of counts obtained
    for(let i = 1; i <= n; i++)
    {
        freq[new_arr[i]]++;
    }

    // Find the count with maximum frequency
    for(let i = 1; i <= n; i++)
    {
        if (freq[i] > maxi)
        {
            maxi = freq[i];
            ans = i;
        }
    }

    // Prlet the answer
    document.write(ans);
}

// Driver code
    let N = 5;
    let arr = [ -1, 3, 4, 1, 5, 2 ];

    // Find minimum number of
    // array rotations required
    find_min_rot(arr, N);

     // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)
**辅助空间:** O(N)