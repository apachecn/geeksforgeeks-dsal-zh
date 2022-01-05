# 分别找出最近的奇、偶数组元素的奇、偶完美平方

> 原文:[https://www . geeksforgeeks . org/分别查找奇数和偶数数组元素的最近奇数和偶数完美平方/](https://www.geeksforgeeks.org/find-the-nearest-odd-and-even-perfect-squares-of-odd-and-even-array-elements-respectively/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，每个数组元素的任务是打印具有相同奇偶性的[最近的完美正方形](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)。

**示例:**

> **输入** : arr[ ] = {6，3，2，15}
> **输出** : 4 1 4 9
> **解释**:
> arr[0](= 6)最近的偶完美平方是 4。
> arr[1](= 3)最近的奇完美平方是 1。
> arr[2](= 2)的最近偶完美平方是 4
> arr[3](= 15)的最近奇完美平方是 9。
> 
> **输入** : arr[ ] = {31，18，64}
> 输出 : 25 16 64

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   找到当前数组元素的[平方根](https://www.geeksforgeeks.org/square-root-of-an-integer/)并将其存储在一个变量中，比如 **sr** 。
    *   如果 **sr** 与**arr【I】**相同，那么 **sr*sr** 就是[最近的完美方块](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)。
    *   否则， **(sr + 1) <sup>2</sup>** 就是[最近的完美方块](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)。
    *   打印上一步中获得的最近的完美正方形。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest even and odd
// perfect squares for even and odd array elements
void nearestPerfectSquare(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Calculate square root of
        // current array element
        int sr = sqrt(arr[i]);

        // If both are of same parity
        if ((sr & 1) == (arr[i] & 1))
            cout << sr * sr << " ";

      // Otherwise
        else {
            sr++;
            cout << sr * sr << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 6, 3, 2, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    nearestPerfectSquare(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to find the nearest even and odd
// perfect squares for even and odd array elements
static void nearestPerfectSquare(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Calculate square root of
        // current array element
        int sr = (int)Math.sqrt(arr[i]);

        // If both are of same parity
        if ((sr & 1) == (arr[i] & 1))
            System.out.print((sr * sr) + " ");

      // Otherwise
        else {
            sr++;
            System.out.print((sr * sr) + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 6, 3, 2, 15 };
    int N = arr.length;
    nearestPerfectSquare(arr, N);
}
}

// This code is contributed by souravghosh0416.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the nearest even and odd
# perfect squares for even and odd array elements
def nearestPerfectSquare(arr, N) :

    # Traverse the array
    for i in range(N):

        # Calculate square root of
        # current array element
        sr = int(math.sqrt(arr[i]))

        # If both are of same parity
        if ((sr & 1) == (arr[i] & 1)) :
            print(sr * sr, end = " ")

      # Otherwise
        else :
            sr += 1
            print(sr * sr, end = " ")

# Driver Code
arr = [ 6, 3, 2, 15 ]
N = len(arr)
nearestPerfectSquare(arr, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find the nearest even and odd
  // perfect squares for even and odd array elements
  static void nearestPerfectSquare(int[] arr, int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Calculate square root of
      // current array element
      int sr = (int)Math.Sqrt(arr[i]);

      // If both are of same parity
      if ((sr & 1) == (arr[i] & 1))
        Console.Write((sr * sr) + " ");

      // Otherwise
      else {
        sr++;
        Console.Write((sr * sr) + " ");
      }
    }
  }

  // Driver Code
  static public void Main()
  {
    int[] arr = { 6, 3, 2, 15 };
    int N = arr.Length;
    nearestPerfectSquare(arr, N);
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the nearest even and odd
// perfect squares for even and odd array elements
function nearestPerfectSquare(arr, N)
{

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Calculate square root of
        // current array element
        let sr = Math.floor(Math.sqrt(arr[i]));

        // If both are of same parity
        if ((sr & 1) == (arr[i] & 1))
            document.write((sr * sr) + " ");

        // Otherwise
        else
        {
            sr++;
            document.write((sr * sr) + " ");
        }
    }
}

// Driver code

// Given array
let arr = [ 6, 3, 2, 15 ];
let N = arr.length;

nearestPerfectSquare(arr, N);

// This code is contributed by target_2

</script>
```

**Output:** 

```
4 1 4 9
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*