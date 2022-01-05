# 检查映射是否可以使第一个数组的和大于第二个数组

> 原文:[https://www . geesforgeks . org/check-if-mapping-make-sum-first-array-大于-second-array/](https://www.geeksforgeeks.org/check-if-mapping-is-possible-to-make-sum-of-first-array-larger-than-second-array/)

给定一个正整数 **K** 和两个大小分别为 **N** 和 **M** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，每个数组包含**【1，K】**范围内的元素。任务是用函数 **f** 将 **1** 到 **K** 的所有数字进行映射，使得**f(1)<f(2)<f(3)<……<f(K)**的 **f(A[i])** 对于 **0≤i < N** 的和是否大于和

**示例:**

> **输入:** A[] = {2，2，2}，B[] = {1，1，3}，K=3
> **输出:** YES
> **解释:**一种可能的方法是为函数 f 赋值如下:
> f(1)= 1
> f(2)= 2
> f(3)= 3
> 每 i = 2+2+2 = 6 和 f(A[i])的和
> 
> **输入:** A[] = {8，2，8，6，9，10}，B[] = {1，2，3，4}，K=10
> **输出:**是

**方法:**按照以下步骤解决问题:

*   如果 **N > M** 的值，则打印**“是”**作为答案，因为分配总是可以使得 **A** 之和大于 **B** 。
*   否则，[对数组](https://www.geeksforgeeks.org/sort-c-stl/) **A[]** 和 **B[]** 进行降序排序。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0】****N-1】**中迭代，如果对于任何指数，**A【I】>B【I】**，则打印**【是】**作为答案，因为为**A【I】**分配足够大的值将使**A【】**之和大于**B【】**
*   否则，打印**“否”**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if mapping is
// possible to make sum of first array
// larger than second array
int isPossible(int A[], int B[], int K, int N, int M)
{
    // If N > M, an assignment is
    // always possible
    if (N > M)
        return 1;

    // Sort A[] in descending order
    sort(A, A + N, greater<int>());

    // Sort B[] in descending order
    sort(B, B + M, greater<int>());

    // Traverse in the arrays
    for (int i = 0; i < N; i++)

        // If A[i] > B[i], assignment
        // is possible
        if (A[i] > B[i])
            return 1;

    return 0;
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 2, 2, 2 };
    int B[] = { 1, 1, 3 };
    int K = 3;
    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function Call
    if (isPossible(A, B, K, N, M))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;
import java.util.Arrays;
import java.util.Collections;

class GFG {
    public static void reverse(int array[])
    {

        // Length of the array
        int n = array.length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = array[i];

            // Assigning the first half to the last half
            array[i] = array[n - i - 1];

            // Assigning the last half to the first half
            array[n - i - 1] = temp;
        }
    }
    // Function to check if mapping is
    // possible to make sum of first array
    // larger than second array
    public static int isPossible(int A[], int B[], int K,
                                 int N, int M)
    {
        // If N > M, an assignment is
        // always possible
        if (N > M)
            return 1;

        // Sort A[] in descending order
        Arrays.sort(A);
        reverse(A);

        // Sort B[] in descending order
        Arrays.sort(B);
        reverse(B);

        // Traverse in the arrays
        for (int i = 0; i < N; i++)

            // If A[i] > B[i], assignment
            // is possible
            if (A[i] > B[i])
                return 1;

        return 0;
    }

    public static void main(String[] args)
    {
        int A[] = { 2, 2, 2 };
        int B[] = { 1, 1, 3 };
        int K = 3;
        int N = A.length;
        int M = B.length;

        // Function Call
        if (isPossible(A, B, K, N, M) == 1)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by lokeshpotta20
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if mapping is
# possible to make sum of first array
# larger than second array
def isPossible(A, B, K, N, M):

    # If N > M, an assignment is
    # always possible
    if (N > M):
        return 1

    # Sort A[] in descending order
    A.sort(reverse = True)

    # Sort B[] in descending order
    B.sort(reverse = True)

    # Traverse in the arrays
    for i in range(N):

        # If A[i] > B[i], assignment
        # is possible
        if (A[i] > B[i]):
            return 1

    return 0

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [ 2, 2, 2 ]
    B = [ 1, 1, 3 ]
    K = 3
    N = len(A)
    M = len(B)

    # Function Call
    if (isPossible(A, B, K, N, M)):
        print("YES")
    else:
        print("NO")

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if mapping is
// possible to make sum of first array
// larger than second array
static int isPossible(int []A, int []B, int K,
                      int N, int M)
{

    // If N > M, an assignment is
    // always possible
    if (N > M)
        return 1;

    // Sort A[] in descending order
    Array.Sort(A);
    Array.Reverse(A);

    // Sort B[] in descending order
    Array.Sort(B);
    Array.Reverse(B);

    // Traverse in the arrays
    for(int i = 0; i < N; i++)

        // If A[i] > B[i], assignment
        // is possible
        if (A[i] > B[i])
            return 1;

    return 0;
}

// Driver Code
public static void Main()
{

    // Given Input
    int []A = { 2, 2, 2 };
    int []B = { 1, 1, 3 };
    int K = 3;
    int N = A.Length;
    int M = B.Length;

    // Function Call
    if (isPossible(A, B, K, N, M) == 1)
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to check if mapping is
        // possible to make sum of first array
        // larger than second array
        function isPossible(A, B, K, N, M) {
            // If N > M, an assignment is
            // always possible
            if (N > M)
                return 1;

            // Sort A[] in descending order
            A.sort(function (a,b) {return b - a })

            // Sort B[] in descending order
            B.sort(function (a,b) {return b - a })
            // Traverse in the arrays
            for (let i = 0; i < N; i++)

                // If A[i] > B[i], assignment
                // is possible
                if (A[i] > B[i])
                    return 1;

            return 0;
        }

        // Driver Code

        // Given Input
        var A = [2, 2, 2];
        var B = [1, 1, 3];
        var K = 3;
        var N = A.length;
        var M = B.length;

        // Function Call
        if (isPossible(A, B, K, N, M))
            document.write("YES");
        else
            document.write("NO");

    </script>
```

**Output**

```
YES
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*