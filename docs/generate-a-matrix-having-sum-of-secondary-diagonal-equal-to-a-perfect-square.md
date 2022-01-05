# 生成二次对角线之和等于完美平方的矩阵

> 原文:[https://www . geeksforgeeks . org/generate-a-matrix-having-sum-secondary-对角线等于完美平方/](https://www.geeksforgeeks.org/generate-a-matrix-having-sum-of-secondary-diagonal-equal-to-a-perfect-square/)

给定一个整数 **N** ，任务是使用范围**【1，N】**中的正整数生成维度矩阵 **N x N** ，使得次对角线之和为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。

**示例:**

> **输入:** N = 3
> **输出:**
> 1 2 3
> 2 3 1
> 3 2 1
> **说明:**
> 二次对角线之和= 3 + 3 + 3 = 9(= 3 <sup>2</sup> )。
> 
> **输入:** N = 7
> **输出:**
> 1 2 3 4 5 6 7
> 2 3 4 5 6 7 1
> 3 4 5 6 7 1 2
> 4 5 6 7 1 2 3
> 5 6 7 1 2 3 4 5
> 6 7 1 2 3 4 5
> 7 1 2 3 4 5 6
> **说明:**
> 二次对角线之和= 7 + 7 + 7 + 7 + 7 + 7

**方法:**由于生成的矩阵需要为维度 **N x N** ，因此，为了使次对角线中的元素之和成为完美的正方形，想法是在次对角线的每个索引处分配 **N** 。所以这条对角线上所有 **N** 元素之和为 **N <sup>2</sup>** ，是一个完美的正方形。按照以下步骤解决问题:

1.  初始化一个矩阵 **mat[][]** 的维度 **N x N** 。
2.  将矩阵的第一行初始化为{1 2 3 … N}。
3.  现在对于矩阵的剩余行，用 **1** 将矩阵前一行的排列按[循环左移](https://www.geeksforgeeks.org/array-rotation/)来填充每一行。
4.  完成上述步骤后，打印矩阵。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the matrix whose sum
// of element in secondary diagonal is a
// perfect square
void diagonalSumPerfectSquare(int arr[], int N)
{

    // Iterate for next N - 1 rows
    for(int i = 0; i < N; i++)
    {

        // Print the current row after
        // the left shift
        for(int j = 0; j < N; j++)
        {
            cout << (arr[(j + i) % 7]) << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    // Given N
    int N = 7;

    int arr[N];

    // Fill the array with elements
    // ranging from 1 to N
    for(int i = 0; i < N; i++)
    {
        arr[i] = i + 1;
    }

    // Function Call
    diagonalSumPerfectSquare(arr, N);
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to print the matrix whose sum
    // of element in secondary diagonal is a
    // perfect square
    static void diagonalSumPerfectSquare(int[] arr,
                                         int N)
    {

        // Iterate for next N - 1 rows
        for (int i = 0; i < N; i++)
        {

            // Print the current row after
            // the left shift
            for (int j = 0; j < N; j++)
            {
                System.out.print(arr[(j + i) % 7] + " ");
            }
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] srgs)
    {

        // Given N
        int N = 7;

        int[] arr = new int[N];

        // Fill the array with elements
        // ranging from 1 to N
        for (int i = 0; i < N; i++)
        {
            arr[i] = i + 1;
        }

        // Function Call
        diagonalSumPerfectSquare(arr, N);
    }
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the matrix whose sum
# of element in secondary diagonal is a
# perfect square
def diagonalSumPerfectSquare(arr, N):

    # Print the current row
    print(*arr, sep =" ")

    # Iterate for next N - 1 rows
    for i in range(N-1):

        # Perform left shift by 1
        arr = arr[i::] + arr[:i:]

        # Print the current row after
        # the left shift
        print(*arr, sep =" ")

# Driver Code

# Given N
N = 7

arr = []

# Fill the array with elements
# ranging from 1 to N
for i in range(1, N + 1):
    arr.append(i)

# Function Call
diagonalSumPerfectSquare(arr, N)
```

## C#

```
// C# program for the
// above approach
using System;
class GFG {

    // Function to print the matrix whose sum
    // of element in secondary diagonal is a
    // perfect square
    static void diagonalSumPerfectSquare(int[] arr,
                                         int N)
    {
        // Iterate for next N - 1 rows
        for (int i = 0; i < N; i++)
        {
            // Print the current row after
            // the left shift
            for (int j = 0; j < N; j++)
            {
                Console.Write(arr[(j + i) % 7] + " ");
            }
            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main(String[] srgs)
    {
        // Given N
        int N = 7;

        int[] arr = new int[N];

        // Fill the array with elements
        // ranging from 1 to N
        for (int i = 0; i < N; i++) {
            arr[i] = i + 1;
        }

        // Function Call
        diagonalSumPerfectSquare(arr, N);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

   // Function to print the matrix whose sum
    // of element in secondary diagonal is a
    // perfect square
    function diagonalSumPerfectSquare( arr,N)
    {

        // Iterate for next N - 1 rows
        for (let i = 0; i < N; i++)
        {

            // Print the current row after
            // the left shift
            for (let j = 0; j < N; j++)
            {
                document.write(arr[(j + i) % 7] + " ");
            }
            document.write("<br/>");
        }
    }

// Driver Code

        // Given N
        let N = 7;

        let arr = new Array(N).fill(0);

        // Fill the array with elements
        // ranging from 1 to N
        for (let i = 0; i < N; i++)
        {
            arr[i] = i + 1;
        }

        // Function Call
        diagonalSumPerfectSquare(arr, N);

 // This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
1 2 3 4 5 6 7 
2 3 4 5 6 7 1 
3 4 5 6 7 1 2 
4 5 6 7 1 2 3 
5 6 7 1 2 3 4 
6 7 1 2 3 4 5 
7 1 2 3 4 5 6 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*