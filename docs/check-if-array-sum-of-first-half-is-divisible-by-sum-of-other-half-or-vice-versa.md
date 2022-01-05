# 检查前半部分的数组和是否能被另一半的和整除，反之亦然

> 原文:[https://www . geesforgeks . org/check-if-array-sum-first-half-被-other-half-sum-整除，反之亦然/](https://www.geeksforgeeks.org/check-if-array-sum-of-first-half-is-divisible-by-sum-of-other-half-or-vice-versa/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查左子阵列的和是否能被右子阵列的和整除，反之亦然。如果是，打印**是**，否则打印**否**。这里，左子阵列将包含从 **0** 到 **mid=(N-1)/2** 的字符串，右子阵列将包含从 **mid+1** 到 **N-1** 的字符串。

**示例:**

> **输入:**arr[]=【1，2，3，4，5】
> **输出:**否
> **说明:**
> 左子阵之和:1+2+3=6
> 右子阵之和:4+5=9
> 所以，两者之和都不能被另一个整除。
> 
> **输入:**arr[]=【4，5，6，1，2，2】
> **输出:**是
> **解释:**
> 左子阵列之和:4+5+6=15
> 右子阵列之和:1+2+2=5
> 所以，左子阵列之和可以被右子阵列之和整除

**方法:**按照以下步骤，解决这个问题:

1.  创建两个变量 **sumL** 和 **sumR** 分别存储左子阵列和右子阵列的总和。用 **0** 初始化它们。
2.  现在，运行一个从 **0** 到 **N-1** 的循环，对于 **0** 到 **(N-1)/2** 范围内的迭代，将元素添加到 **sumL** 中。对于 **(N-1)/2** 之后的迭代，添加 **sumR** 中的元素。
3.  循环结束后，检查 **sumL** 是否可以被 **sumR** 整除，或者 **sumR** 是否可以被 **sumL** 整除。如果这些条件中的任何一个满足，则打印**是**否则打印**否**。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the sum of left subarray
// is divisible by the sum of right or vice - versa
bool isDivisible(int* arr, int N)
{

    // Variables to store the sum of
    // left and right subarrays
    int sumL = 0, sumR = 0;

    for (int i = 0; i < N; ++i) {
        if (i <= (N - 1) / 2) {
            sumL += arr[i];
        }
        else {
            sumR += arr[i];
        }
    }

    // If Divisible
    if (sumL % sumR == 0
        or sumR % sumL == 0) {
        return 1;
    }

    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 4, 5, 6, 1, 2, 2 };
    int N = sizeof(arr) / sizeof(int);

    if (isDivisible(arr, N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to check if the sum of left subarray
    // is divisible by the sum of right or vice - versa
    public static boolean isDivisible(int[] arr, int N)
    {

        // Variables to store the sum of
        // left and right subarrays
        int sumL = 0, sumR = 0;

        for (int i = 0; i < N; ++i) {
            if (i <= (N - 1) / 2) {
                sumL += arr[i];
            } else {
                sumR += arr[i];
            }
        }

        // If Divisible
        if (sumL % sumR == 0 || sumR % sumL == 0) {
            return true;
        }

        return false;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 4, 5, 6, 1, 2, 2 };
        int N = arr.length;

        if (isDivisible(arr, N))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the sum of left subarray
# is divisible by the sum of right or vice - versa
def isDivisible(arr, N) :

    # Variables to store the sum of
    # left and right subarrays
    sumL = 0; sumR = 0;

    for i in range(N) :
        if (i <= (N - 1) // 2) :
            sumL += arr[i];

        else :
            sumR += arr[i];

    # If Divisible
    if (sumL % sumR == 0 or sumR % sumL == 0) :
        return 1;

    return 0;

# Driver Code
if __name__ == "__main__" :

    arr = [ 4, 5, 6, 1, 2, 2 ];
    N = len(arr);

    if (isDivisible(arr, N)) :
        print("Yes");
    else :
        print("No");

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to check if the sum of left subarray
    // is divisible by the sum of right or vice - versa
    public static bool isDivisible(int[] arr, int N)
    {

        // Variables to store the sum of
        // left and right subarrays
        int sumL = 0, sumR = 0;

        for (int i = 0; i < N; ++i) {
            if (i <= (N - 1) / 2) {
                sumL += arr[i];
            } else {
                sumR += arr[i];
            }
        }

        // If Divisible
        if (sumL % sumR == 0 || sumR % sumL == 0) {
            return true;
        }

        return false;
    }

    // Driver Code
    public static void Main() {
        int[] arr = { 4, 5, 6, 1, 2, 2 };
        int N = arr.Length;

        if (isDivisible(arr, N))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check if the sum of left subarray
        // is divisible by the sum of right or vice - versa
        function isDivisible(arr, N) {

            // Variables to store the sum of
            // left and right subarrays
            let sumL = 0, sumR = 0;

            for (let i = 0; i < N; ++i) {
                if (i <= (N - 1) / 2) {
                    sumL += arr[i];
                }
                else {
                    sumR += arr[i];
                }
            }

            // If Divisible
            if (sumL % sumR == 0
                || sumR % sumL == 0) {
                return 1;
            }

            return 0;
        }

        // Driver Code

        let arr = [4, 5, 6, 1, 2, 2];
        let N = arr.length;

        if (isDivisible(arr, N))
            document.write("Yes");
        else
            document.write("No");

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)