# K 次操作后打印数组

> 原文:[https://www . geeksforgeeks . org/k-operations 后打印阵列/](https://www.geeksforgeeks.org/print-the-array-after-k-operations/)

给定一个大小为 **N** 的数组 **arr[]** 和一个数字 **K** 。任务是在 **K** 操作后打印数组 **arr[]** ，以便在每次操作时，将数组中的每个元素 **arr[i]** 替换为**max–arr[I]**，其中 max 是数组中的最大元素。
**举例:**

> **输入:** arr[] = {4，8，12，16}，K = 4
> **输出:** 0 4 8 12
> **解释:**
> 对于给定的数组 arr[] = {4，8，12，16 }。对于每个操作 K，数组的变化如下:
> { 12，8，4，0 }–K = 1
> { 0，4，8，12 }–K = 2
> { 12，8，4，0 }–K = 3
> { 0，4，8，12 }–K = 4
> **输入:** arr[] = {8，0，3，5}，K = 3
> **输出:** 0 每个操作 K 的数组变化如下:
> { 0，8，5，3 }–K = 1
> { 8，0，3，5 }–K = 2
> { 0，8，5，3 }–K = 3

**进场:**思路是每走一步后清晰观察阵面。

1.  最初，因为我们从数组中减去最大元素，所以我们可以确定数组中至少有一个元素的值为零。这发生在第一步 **K = 1** 之后。让这一步后的阵为 **A[]** 带最大元素 **M** 。
2.  在此第一步之后，阵列变得停滞，并且值交替地从其值 **A[i]** 变为**M–A[I]**。
3.  例如，让我们取数组 **arr[]** = {4，8，12，16}。在这个数组中，最大值是 16，让我们假设 **K** = 4。
    *   第一步，(即)对于 **K = 1** ，数组简化为 **{12，8，4，0}** 。也就是说，每个元素 arr[i]都被替换为 16–arr[I]。设这个数组是 A[]，这个数组 M 的最大元素是 12。
    *   第一步后，该数组中的每个元素 **A[i]** 在 **A[i]** 和**12–A[I]**之间交替变化。也就是说，对于 **K = 2** ，数组现在变成 **{0，4，8，12}** 。
    *   同样，对于第三步，(即) **K = 3** ，数组再次变为 **{12，8，4，0}** ，与 **K = 1** 相同。
    *   而对于第四步，(即) **K = 4** ，数组变为 **{0，4，8，12}** ，与 **K = 2** 等相同。

所以可以得出结论，我们只需要检查 K 是奇数还是偶数:

*   如果 K 是**奇数**:将每个元素**arr【I】**替换为**arr【I】–min**，其中 min 是数组中的最小元素。
*   如果 K 是**偶数**:将每个元素**arr【I】**替换为**max–arr【I】**，其中 max 是数组中最大的元素。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print the array
// after K operations
#include <bits/stdc++.h>
using namespace std;

// Function to print the array
// after K operations
void printArray(int A[], int n, int K)
{
    // Variables to store the minimum and
    // the maximum elements of the array
    int minEle = INT_MAX,
        maxEle = INT_MIN;

    // Loop to find the minimum and the
    // maximum elements of the array
    for (int i = 0; i < n; i++) {
        minEle = min(minEle, A[i]);
        maxEle = max(maxEle, A[i]);
    }

    // If K is not equal to 0
    if (K != 0) {

        // If K is odd
        if (K % 2 == 1) {

            // Replace every element with
            // max - arr[i]
            for (int i = 0; i < n; i++)
                A[i] = maxEle - A[i];
        }

        // If K is even
        else {

            // Replace every element with
            // A[i] - min
            for (int i = 0; i < n; i++)
                A[i] = A[i] - minEle;
        }
    }

    // Printing the array after K operations
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 12, 16 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    printArray(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the array
// after K operations
import java.io.*;

class GFG {

    // Function to print the array
    // after K operations
    static void printArray(int[] A, int n, int K)
    {
        // Variables to store the minimum and
        // the maximum elements of the array
        int minEle = Integer.MAX_VALUE,
            maxEle = Integer.MAX_VALUE;

        // Loop to find the minimum and the
        // maximum elements of the array
        for (int i = 0; i < n; i++) {
            minEle = Math.min(minEle, A[i]);
            maxEle = Math.max(maxEle, A[i]);
        }

        // If K is not equal to 0
        if (K != 0) {

            // If K is odd
            if (K % 2 == 1) {

                // Replace every element with
                // max - arr[i]
                for (int i = 0; i < n; i++)
                    A[i] = maxEle - A[i];
            }

            // If K is even
            else {

                // Replace every element with
                // A[i] - min
                for (int i = 0; i < n; i++)
                    A[i] = A[i] - minEle;
            }
        }

        // Printing the array after K operations
        for (int i = 0; i < n; i++)
            System.out.print(A[i] + " ");
    }

    // Driver Code
    public static void main (String[] args)
    {

        int[] arr = { 4, 8, 12, 16 };
        int K = 4;
        int N = arr.length;

        printArray(arr, N, K);
    }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to print the array
# after K operations

# Function to print the array
# after K operations
def printArray(A, n, K):

    # Variables to store the minimum and
    # the maximum elements of the array
    minEle = 10**9
    maxEle = -10**9

    # Loop to find the minimum and the
    # maximum elements of the array
    for i in range(n):
        minEle = min(minEle, A[i])
        maxEle = max(maxEle, A[i])

    # If K is not equal to 0
    if (K != 0):

        # If K is odd
        if (K % 2 == 1):

            # Replace every element with
            # max - arr[i]
            for i in range(n):
                A[i] = maxEle - A[i]

        # If K is even
        else:

            # Replace every element with
            # A[i] - min
            for i in range(n):
                A[i] = A[i] - minEle

    # Printing the array after K operations
    for i in A:
        print(i, end=" ")

# Driver code
if __name__ == '__main__':
    arr=[4, 8, 12, 16]
    K = 4
    N = len(arr)

    printArray(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print the array
// after K operations
using System;

class GFG{

    // Function to print the array
    // after K operations
    static void printArray(int[] A, int n, int K)
    {
        // Variables to store the minimum and
        // the maximum elements of the array
        int minEle = Int32.MaxValue,
            maxEle = Int32.MinValue;

        // Loop to find the minimum and the
        // maximum elements of the array
        for (int i = 0; i < n; i++) {
            minEle = Math.Min(minEle, A[i]);
            maxEle = Math.Max(maxEle, A[i]);
        }

        // If K is not equal to 0
        if (K != 0) {

            // If K is odd
            if (K % 2 == 1) {

                // Replace every element with
                // max - arr[i]
                for (int i = 0; i < n; i++)
                    A[i] = maxEle - A[i];
            }

            // If K is even
            else {

                // Replace every element with
                // A[i] - min
                for (int i = 0; i < n; i++)
                    A[i] = A[i] - minEle;
            }
        }

        // Printing the array after K operations
        for (int i = 0; i < n; i++)
            Console.Write(A[i] + " ");
    }

    // Driver code
    static public void Main ()
    {
        int[] arr = { 4, 8, 12, 16 };
        int K = 4;
        int N = arr.Length;

        printArray(arr, N, K);
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// Javascript program to print the array
// after K operations

// Function to print the array
// after K operations
function printArray(A, n, K)
{
    // Variables to store the minimum and
    // the maximum elements of the array
    var minEle = 100000000, maxEle = -100000000;

    // Loop to find the minimum and the
    // maximum elements of the array
    for (var i = 0; i < n; i++) {
        minEle = Math.min(minEle, A[i]);
        maxEle = Math.max(maxEle, A[i]);
    }

    // If K is not equal to 0
    if (K != 0) {

        // If K is odd
        if (K % 2 == 1) {

            // Replace every element with
            // max - arr[i]
            for (var i = 0; i < n; i++)
                A[i] = maxEle - A[i];
        }

        // If K is even
        else {

            // Replace every element with
            // A[i] - min
            for (var i = 0; i < n; i++)
                A[i] = A[i] - minEle;
        }
    }

    // Printing the array after K operations
    for (var i = 0; i < n; i++)
        document.write(A[i] + " ");
}

// Driver code
arr = [ 4, 8, 12, 16 ];
var K = 4;
var N = arr.length;
printArray(arr, N, K);

</script>
```

**Output:** 

```
0 4 8 12
```

**时间复杂度:** O(N)，其中 N 是数组的大小。