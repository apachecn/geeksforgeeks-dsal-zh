# 找到位置 I 拆分数组，使得前缀和直到 i-1，I 和后缀和直到 i+1 在 GP 中具有共同的比率 K

> 原文:[https://www . geesforgeks . org/find-position-I-to-split-array-so-prefix-sum-til-I-1-I-and-后缀-sum-til-i1-in-gp-common-ratio-k/](https://www.geeksforgeeks.org/find-position-i-to-split-array-such-that-prefix-sum-till-i-1-i-and-suffix-sum-till-i1-are-in-gp-with-common-ratio-k/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** 和一个正整数 **K** 。任务是找到**arr【】**中元素的位置 say **i** ，使得前缀和直到 **i-1** 、 **i** 和后缀和直到 **i+1** 以共同的比例 **K** 呈几何级数。

**示例**:

> **输入** : arr[] = { 5，1，4，20，6，15，9，10 }，K = 2
> **输出** : 4
> **解释**:执行以下操作得到所需的 GP。
> 位置 1 到 3 的元素之和为 5 + 1 + 4 = 10，位置 5 到 8 的元素之和为 6 + 15 + 9 + 10 = 40。
> 位置 4 的元素为 20。
> 因此 10，20，40 是一个具有公比 k 的几何级数
> 
> **输入** : arr[] ={ -3，5，0，2，1，25，25，100 }，K = 5
> **输出** : 6

**逼近**:给定的问题可以通过[线性搜索](https://www.geeksforgeeks.org/linear-search/)和基本[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来解决。按照以下步骤解决给定的问题。

*   如果数组的大小小于 3，那么就不可能有序列，所以只需返回-1。
*   初始化一个变量，比如 **arrSum** 来存储 **arr[]** 的所有元素的和。
*   计算数组 **arr[]** 的和，并存储在 **arrSum** 中。
*   如果 **arrSum % R！= 0** ，然后返回 **0** 。其中 **R = K * K + 1 + K + 1** 。
*   初始化一个变量，比如 **mid = K * (Sum / R)** ，将通用比率 GP 系列的中间元素存储为 **K.**
*   取一个变量，比如 **temp** 来存储临时结果。
*   用变量 **i** 迭代 **arr[]** 从索引 **i** 到(**arr[])的大小–2**。
    *   **有=有+ arr[i-1]**
    *   如果 **arr[i] =中间**
        *   如果 **tem = mid/k** ，则返回 **(i+1)** 作为答案。
        *   否则返回 **0** 。
*   如果循环终止并且 **arr[]** 中没有元素等于 mid，那么只需返回 **0** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if there is
// an element forming G.P. series
// having common ratio k
int checkArray(int arr[], int N, int k)
{

    // If size of array is less than
    // three then return -1
    if (N < 3)
        return -1;

    // Initialize the variables
    int i, Sum = 0, temp = 0;

    // Calculate total sum of array
    for (i = 0; i < N; i++)
        Sum += arr[i];

    int R = (k * k + k + 1);

    if (Sum % R != 0)
        return 0;

    // Calculate Middle element of G.P. series
    int Mid = k * (Sum / R);

    // Iterate over the range
    for (i = 1; i < N - 1; i++) {

        // Store the first element of G.P.
        // series in the variable temp
        temp += arr[i - 1];

        if (arr[i] == Mid) {

            // Return position of middle element
            // of the G.P. series if the first
            // element is in G.P. of common ratio k
            if (temp == Mid / k)
                return i + 1;

            // Else return 0
            else
                return 0;
        }
    }

    // if middle element is not found in arr[]
    return 0;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 5, 1, 4, 20, 6, 15, 9, 10 };

    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 2;

    cout << checkArray(arr, N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

// Function to check if there is
// an element forming G.P. series
// having common ratio k
static int checkArray(int arr[], int N, int k)
{

    // If size of array is less than
    // three then return -1
    if (N < 3)
        return -1;

    // Initialize the variables
    int i, Sum = 0, temp = 0;

    // Calculate total sum of array
    for (i = 0; i < N; i++)
        Sum += arr[i];

    int R = (k * k + k + 1);

    if (Sum % R != 0)
        return 0;

    // Calculate Middle element of G.P. series
    int Mid = k * (Sum / R);

    // Iterate over the range
    for (i = 1; i < N - 1; i++) {

        // Store the first element of G.P.
        // series in the variable temp
        temp += arr[i - 1];

        if (arr[i] == Mid) {

            // Return position of middle element
            // of the G.P. series if the first
            // element is in G.P. of common ratio k
            if (temp == Mid / k)
                return i + 1;

            // Else return 0
            else
                return 0;
        }
    }

    // if middle element is not found in arr[]
    return 0;
}

// Driver Code
public static void main (String[] args) {

    // Given array
    int arr[] = { 5, 1, 4, 20, 6, 15, 9, 10 };

    int N = arr.length;

    int K = 2;

       System.out.println(checkArray(arr, N, K));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to check if there is
# an element forming G.P. series
# having common ratio k
def checkArray(arr, N, k):

        # If size of array is less than
        # three then return -1
    if (N < 3):
        return -1

        # Initialize the variables
    Sum = 0
    temp = 0

    # Calculate total sum of array
    for i in range(0, N):
        Sum += arr[i]

    R = (k * k + k + 1)

    if (Sum % R != 0):
        return 0

        # Calculate Middle element of G.P. series
    Mid = k * (Sum // R)

    # Iterate over the range
    for i in range(1, N-1):

                # Store the first element of G.P.
                # series in the variable temp
        temp += arr[i - 1]

        if (arr[i] == Mid):

                        # Return position of middle element
                        # of the G.P. series if the first
                        # element is in G.P. of common ratio k
            if (temp == Mid // k):
                return i + 1

                # Else return 0
            else:
                return 0

        # if middle element is not found in arr[]
    return 0

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [5, 1, 4, 20, 6, 15, 9, 10]
    N = len(arr)
    K = 2

    print(checkArray(arr, N, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to check if there is
    // an element forming G.P. series
    // having common ratio k
    static int checkArray(int[] arr, int N, int k)
    {

        // If size of array is less than
        // three then return -1
        if (N < 3)
            return -1;

        // Initialize the variables
        int i, Sum = 0, temp = 0;

        // Calculate total sum of array
        for (i = 0; i < N; i++)
            Sum += arr[i];

        int R = (k * k + k + 1);

        if (Sum % R != 0)
            return 0;

        // Calculate Middle element of G.P. series
        int Mid = k * (Sum / R);

        // Iterate over the range
        for (i = 1; i < N - 1; i++) {

            // Store the first element of G.P.
            // series in the variable temp
            temp += arr[i - 1];

            if (arr[i] == Mid) {

                // Return position of middle element
                // of the G.P. series if the first
                // element is in G.P. of common ratio k
                if (temp == Mid / k)
                    return i + 1;

                // Else return 0
                else
                    return 0;
            }
        }

        // if middle element is not found in arr[]
        return 0;
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Given array
        int[] arr = { 5, 1, 4, 20, 6, 15, 9, 10 };

        int N = arr.Length;

        int K = 2;

        Console.WriteLine(checkArray(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check if there is
        // an element forming G.P. series
        // having common ratio k
        function checkArray(arr, N, k) {

            // If size of array is less than
            // three then return -1
            if (N < 3)
                return -1;

            // Initialize the variables
            let i, Sum = 0, temp = 0;

            // Calculate total sum of array
            for (i = 0; i < N; i++)
                Sum += arr[i];

            let R = (k * k + k + 1);

            if (Sum % R != 0)
                return 0;

            // Calculate Middle element of G.P. series
            let Mid = k * (Sum / R);

            // Iterate over the range
            for (i = 1; i < N - 1; i++) {

                // Store the first element of G.P.
                // series in the variable temp
                temp += arr[i - 1];

                if (arr[i] == Mid) {

                    // Return position of middle element
                    // of the G.P. series if the first
                    // element is in G.P. of common ratio k
                    if (temp == Mid / k)
                        return i + 1;

                    // Else return 0
                    else
                        return 0;
                }
            }

            // if middle element is not found in arr[]
            return 0;
        }

        // Driver Code

        // Given array
        let arr = [5, 1, 4, 20, 6, 15, 9, 10];
        let N = arr.length;
        let K = 2;
        document.write(checkArray(arr, N, K) + "<br>");

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

**时间** **复杂度**:O(N)
T5】辅助 **空间** : O(1)