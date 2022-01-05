# 给定数组无限拼接形成的数组前 M 个元素之和

> 原文:[https://www . geeksforgeeks . org/由无限连接给定数组形成的数组的前 m 个元素之和/](https://www.geeksforgeeks.org/sum-of-the-first-m-elements-of-array-formed-by-infinitely-concatenating-given-array/)

给定一个由 **N** 个整数和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出由给定数组**arr【】**无限级联而成的数组的前 **M** 个元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {1，2，3}，M = 5
> **输出:** 9
> **解释:**
> 给定数组 arr[]无限级联形成的数组的形式为{1，2，3，1，2，3，1，2，3，1，2，3，1，2，3，… }。
> 数组前 M(= 5)个元素之和为 1 + 2 + 3 + 1 + 2 = 9。
> 
> **输入:** arr[] = {1}，M = 7
> T3】输出: 7

**方法:**给定的问题可以通过使用 [**模算符(%)**](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/) 求解，将给定的数组视为[圆形数组](https://www.geeksforgeeks.org/circular-array/)，并据此求出第一个 **M** 元素的和。按照以下步骤解决此问题:

*   初始化一个变量，将 **sum** 设为 **0** 来存储新数组的第一个 **M** 元素的合成和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M–1】**，并将**和**的值增加**arr【I % N】**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of first
// M numbers formed by the infinite
// concatenation of the array A[]
int sumOfFirstM(int A[], int N, int M)
{
    // Stores the resultant sum
    int sum = 0;

    // Iterate over the range [0, M - 1]
    for (int i = 0; i < M; i++) {

        // Add the value A[i%N] to sum
        sum = sum + A[i % N];
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3 };
    int M = 5;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << sumOfFirstM(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.lang.*;

class GFG {

  // Function to find the sum of first
  // M numbers formed by the infinite
  // concatenation of the array A[]
  public static int sumOfFirstM(int A[], int N, int M)
  {

    // Stores the resultant sum
    int sum = 0;

    // Iterate over the range [0, M - 1]
    for (int i = 0; i < M; i++) {

      // Add the value A[i%N] to sum
      sum = sum + A[i % N];
    }

    // Return the resultant sum
    return sum;
  }

  // Driver Code
  public static void main(String[] args) {
    int arr[] = { 1, 2, 3 };
    int M = 5;
    int N = arr.length;
    System.out.println(sumOfFirstM(arr, N, M));

  }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of first
# M numbers formed by the infinite
# concatenation of the array A[]
def sumOfFirstM(A, N, M):

    # Stores the resultant sum
    sum = 0

    # Iterate over the range [0, M - 1]
    for i in range(M):

        # Add the value A[i%N] to sum
        sum = sum + A[i % N]

    # Return the resultant sum
    return sum

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3 ]
    M = 5
    N = len(arr)

    print(sumOfFirstM(arr, N, M))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the sum of first
    // M numbers formed by the infinite
    // concatenation of the array A[]
    static int sumOfFirstM(int[] A, int N, int M)
    {

        // Stores the resultant sum
        int sum = 0;

        // Iterate over the range [0, M - 1]
        for (int i = 0; i < M; i++) {

            // Add the value A[i%N] to sum
            sum = sum + A[i % N];
        }

        // Return the resultant sum
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 3 };
        int M = 5;
        int N = arr.Length;
        Console.WriteLine(sumOfFirstM(arr, N, M));
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the sum of first
        // M numbers formed by the infinite
        // concatenation of the array A[]
        function sumOfFirstM(A, N, M) {
            // Stores the resultant sum
            let sum = 0;
            // Iterate over the range [0, M - 1]
            for (let i = 0; i < M; i++) {

                // Add the value A[i%N] to sum
                sum = sum + A[i % N];
            }

            // Return the resultant sum
            return sum;
        }

        // Driver Code

        let arr = [1, 2, 3];
        let M = 5;
        let N = arr.length;
        document.write(sumOfFirstM(arr, N, M));

  // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(M)*
T5**辅助空间:** O(1)