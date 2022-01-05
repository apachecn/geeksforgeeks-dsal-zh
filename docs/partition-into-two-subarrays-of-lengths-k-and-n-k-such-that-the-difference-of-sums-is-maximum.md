# 分成长度为 k 和(N–k)的两个子阵列，使得和之差最大

> 原文:[https://www . geesforgeks . org/partition-in-two-length-k-n-k-subarrays-of-sum-is-max/](https://www.geeksforgeeks.org/partition-into-two-subarrays-of-lengths-k-and-n-k-such-that-the-difference-of-sums-is-maximum/)

给定一个长度为 N 的非负整数和一个整数 K 的数组。将给定的数组分成长度为 K 和 N–K 的两个子数组，使两个子数组之和的差值最大。

**示例:**

```
Input : arr[] = {8, 4, 5, 2, 10}
        k = 2
Output : 17
Explanation :
Here, we can make first subarray of length k = {4, 2}
and second subarray of length N - k = {8, 5, 10}. Then,
the max_difference = (8 + 5 + 10) - (4 + 2) = 17.

Input : arr[] = {1, 1, 1, 1, 1, 1, 1, 1}
        k = 3
Output : 2
Explanation :
Here, subarrays would be {1, 1, 1, 1, 1} and {1, 1, 1}.
So, max_difference would be 2
```

选择具有最大可能和的 k 个数字。那么解显然是 k 个最大的数。因此，贪婪算法在这里起作用——在每一步，我们选择最大可能的数字，直到我们得到所有的 K 个数字。
在这个问题中，我们应该把 N 个数的数组分别分成两个子数组 *k* 和*N–k*个数。考虑两种情况–

*   这两个子阵中和最大的子阵是 K 个数的子阵。然后我们希望最大化其中的和，因为只有当第一子阵列中的和增加时，第二子阵列中的和才会减少。所以我们现在在上面考虑的子问题中，应该选择 k 个最大的数。
*   这两个子阵中和最大的子阵是 N–k 个数的子阵。与前面的情况类似，我们必须在所有数字中选择 N–k 个最大的数字。

现在，让我们想想上面两种情况中哪一种实际上给出了答案。我们可以很容易地看到，当更多的数字包含在最大数字组中时，差异会更大。因此，我们可以设置 M = max(k，N–k)，求出 M 个最大数字的和(假设是 S1)，然后答案是 S1 –( S–S1)，其中 S 是所有数字的和。

下面是上述方法的实现:

## C++

```
// C++ program to calculate max_difference between
// the sum of two subarrays of length k and N - k
#include <bits/stdc++.h>
using namespace std;

// Function to calculate max_difference
int maxDifference(int arr[], int N, int k)
{
    int M, S = 0, S1 = 0, max_difference = 0;

    // Sum of the array
    for (int i = 0; i < N; i++)
        S += arr[i];

    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());
    M = max(k, N - k);
    for (int i = 0; i < M; i++)
        S1 += arr[i];

    // Calculating max_difference
    max_difference = S1 - (S - S1);
    return max_difference;
}

// Driver function
int main()
{
    int arr[] = { 8, 4, 5, 2, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << maxDifference(arr, N, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate max_difference between
// the sum of two subarrays of length k and N - k
import java.util.*;

class GFG
{

// Function to calculate max_difference
static int maxDifference(int arr[], int N, int k)
{
    int M, S = 0, S1 = 0, max_difference = 0;

    // Sum of the array
    for (int i = 0; i < N; i++)
        S += arr[i];
    int temp;

    // Sort the array in descending order
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            if (arr[i] < arr[j])
            {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    M = Math.max(k, N - k);
    for (int i = 0; i < M; i++)
        S1 += arr[i];

    // Calculating max_difference
    max_difference = S1 - (S - S1);
    return max_difference;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 8, 4, 5, 2, 10 };
    int N = arr.length;
    int k = 2;
    System.out.println(maxDifference(arr, N, k));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 code to calculate max_difference
# between the sum of two subarrays of
# length k and N - k

# Function to calculate max_difference
def maxDifference(arr, N, k ):
    S = 0
    S1 = 0
    max_difference = 0

    # Sum of the array
    for i in range(N):
        S += arr[i]

    # Sort the array in descending order
    arr.sort(reverse=True)
    M = max(k, N - k)
    for i in range( M):
        S1 += arr[i]

    # Calculating max_difference
    max_difference = S1 - (S - S1)
    return max_difference

# Driver Code
arr = [ 8, 4, 5, 2, 10 ]
N = len(arr)
k = 2
print(maxDifference(arr, N, k))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to calculate max_difference between
// the sum of two subarrays of length k and N - k
using System;

class GFG
{

// Function to calculate max_difference
static int maxDifference(int []arr, int N, int k)
{
    int M, S = 0, S1 = 0, max_difference = 0;

    // Sum of the array
    for (int i = 0; i < N; i++)
        S += arr[i];
    int temp;

    // Sort the array in descending order
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {
            if (arr[i] < arr[j])
            {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    M = Math.Max(k, N - k);
    for (int i = 0; i < M; i++)
        S1 += arr[i];

    // Calculating max_difference
    max_difference = S1 - (S - S1);
    return max_difference;
}

// Driver Code
public static void Main()
{
    int []arr = { 8, 4, 5, 2, 10 };
    int N = arr.Length;
    int k = 2;
    Console.Write(maxDifference(arr, N, k));
}
}

// This code is contributed by mohit kumar 29
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// max_difference between
// the sum of two subarrays
// of length k and N - k

// Function to calculate
// max_difference
function maxDifference($arr, $N, $k)
{
    $M; $S = 0; $S1 = 0;
    $max_difference = 0;

    // Sum of the array
    for ($i = 0; $i < $N; $i++)
        $S += $arr[$i];

    // Sort the array in
    // descending order
    rsort($arr);
    $M = max($k, $N - $k);
    for ($i = 0; $i < $M; $i++)
        $S1 += $arr[$i];

    // Calculating
    // max_difference
    $max_difference = $S1 - ($S - $S1);
    return $max_difference;
}

// Driver Code
$arr = array(8, 4, 5, 2, 10);
$N = count($arr);
$k = 2;
echo maxDifference($arr, $N, $k);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate max_difference
// between the sum of two subarrays of length
// k and N - k

// Function to calculate max_difference
function maxDifference(arr, N, k)
{
    let M, S = 0, S1 = 0, max_difference = 0;

    // Sum of the array
    for(let i = 0; i < N; i++)
        S += arr[i];

    let temp;

    // Sort the array in descending order
    for(let i = 0; i < N; i++)
    {
        for(let j = i + 1; j < N; j++)
        {
            if (arr[i] < arr[j])
            {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    M = Math.max(k, N - k);
    for(let i = 0; i < M; i++)
        S1 += arr[i];

    // Calculating max_difference
    max_difference = S1 - (S - S1);
    return max_difference;
}

// Driver code
let arr = [ 8, 4, 5, 2, 10 ];
let N = arr.length;
let k = 2;

document.write(maxDifference(arr, N, k));

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
17
```

**进一步优化:**我们可以使用 Heap(或优先级队列)高效地找到 M 个最大的元素。详情参见[数组中 k 个最大(或最小)元素](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)。