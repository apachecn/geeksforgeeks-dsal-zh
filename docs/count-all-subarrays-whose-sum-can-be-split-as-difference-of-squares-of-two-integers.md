# 计算所有子阵列，其和可以被拆分为两个整数的平方差

> 原文:[https://www . geeksforgeeks . org/count-all-subarray-其和可以被拆分为两个整数的平方差/](https://www.geeksforgeeks.org/count-all-subarrays-whose-sum-can-be-split-as-difference-of-squares-of-two-integers/)

给定一个数组 **arr[]** ，任务是计算所有子数组，这些子数组的和可以分解为两个整数的平方差。
**例:**

> **输入:** arr[] = {1，3，5}
> **输出:** 6
> **解释:**
> 有六个子阵列，可以从其和可以拆分为两个整数的平方差的数组中形成。它们是:
> 子阵列{1 } = 1 = 1<sup>2</sup>–0<sup>2</sup>
> 子阵列{ 3 } = 3 = 2<sup>2</sup>–1<sup>2</sup>T19】子阵列{ 5 } = 5 = 3<sup>2</sup>–2<sup>2</sup>
> 子阵列{ 1，3 } = 4 = 2【2 5} = 8 = 3<sup>2</sup>–1<sup>2</sup>T34】子阵列{1，3，5 }之和= 9 = 5<sup>2</sup>–4<sup>2</sup>T39**输入:** arr[] = {1，2，3，4，5}
> **输出:** 11

**方法:**为了解决这个问题，需要进行观察。除了可以用 **((4 * N) + 2)** 形式表示的数字之外，任何数字都可以表示为两个正方形的差，其中 N 是整数。因此，可以按照以下步骤计算答案:

*   遍历数组[找到给定数组的所有可能的子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。
*   如果一个数 K 可以表示为 **((4 * N) + 2)** ，其中 N 是某个整数，那么 **K + 2** 永远是 4 的倍数。
*   因此，对于子阵列 K 的每个和，检查 **(K + 2)** 是否为 4 的倍数。
*   如果是，那么这个特定的值就不能用平方的差来表示。

以下是上述方法的实现:

## C++

```
// C++ program to count all the non-contiguous
// subarrays whose sum can be split
// as the difference of the squares
#include <bits/stdc++.h>
using namespace std;

// Function to count all the non-contiguous
// subarrays whose sum can be split
// as the difference of the squares
int Solve(int arr[], int n)
{
    int temp = 0, count = 0;

    // Loop to iterate over all the possible
    // subsequences of the array
    for (int i = 0; i < n; i++) {
        temp = 0;
        for (int j = i; j < n; j++) {

            // Finding the sum of all the
            // possible subsequences
            temp += arr[j];

            // Condition to check whether
            // the number can be split
            // as difference of squares
            if ((temp + 2) % 4 != 0)
                count++;
        }
    }

    return count;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 };
    int N = sizeof(arr) / sizeof(int);

    cout << Solve(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all the
// non-contiguous subarrays whose
// sum can be split as the
// difference of the squares
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count all the non-contiguous
// subarrays whose sum can be split
// as the difference of the squares
static int Solve(int arr[], int n)
{
    int temp = 0, count = 0;

    // Loop to iterate over all the possible
    // subsequences of the array
    for(int i = 0; i < n; i++)
    {
       temp = 0;
       for(int j = i; j < n; j++)
       {

           // Finding the sum of all the
           // possible subsequences
           temp += arr[j];

           // Condition to check whether
           // the number can be split
           // as difference of squares
           if ((temp + 2) % 4 != 0)
               count++;
       }
    }

    return count;
}

// Driver Code
public static void main(String [] args)
{
    int arr[] = { 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 };
    int N = arr.length;

    System.out.println(Solve(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to count all the non-contiguous
# subarrays whose sum can be split
# as the difference of the squares

# Function to count all the non-contiguous
# subarrays whose sum can be split
# as the difference of the squares
def Solve(arr, n):

    temp = 0; count = 0;

    # Loop to iterate over all the possible
    # subsequences of the array
    for i in range(0, n):
        temp = 0;
        for j in range(i, n):

            # Finding the sum of all the
            # possible subsequences
            temp = temp + arr[j];

            # Condition to check whether
            # the number can be split
            # as difference of squares
            if ((temp + 2) % 4 != 0):
                count += 1;

    return count;

# Driver code
arr = [ 1, 2, 3, 4, 5,
        6, 7, 8, 9, 10 ];
N = len(arr);
print(Solve(arr, N));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to count all the
// non-contiguous subarrays whose
// sum can be split as the
// difference of the squares
using System;

class GFG{

// Function to count all the
// non-contiguous subarrays whose
// sum can be split as the
// difference of the squares
static int Solve(int []arr, int n)
{
    int temp = 0, count = 0;

    // Loop to iterate over all
    // the possible subsequences
    // of the array
    for(int i = 0; i < n; i++)
    {
       temp = 0;
       for(int j = i; j < n; j++)
       {

          // Finding the sum of all the
          // possible subsequences
          temp += arr[j];

          // Condition to check whether
          // the number can be split
          // as difference of squares
          if ((temp + 2) % 4 != 0)
              count++;
       }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 };
    int N = arr.Length;

    Console.Write(Solve(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program to count all the non-contiguous
// subarrays whose sum can be split
// as the difference of the squares

// Function to count all the non-contiguous
// subarrays whose sum can be split
// as the difference of the squares
function Solve(arr, n)
{
    let temp = 0, count = 0;

    // Loop to iterate over all the possible
    // subsequences of the array
    for (let i = 0; i < n; i++) {
        temp = 0;
        for (let j = i; j < n; j++) {

            // Finding the sum of all the
            // possible subsequences
            temp += arr[j];

            // Condition to check whether
            // the number can be split
            // as difference of squares
            if ((temp + 2) % 4 != 0)
                count++;
        }
    }

    return count;
}

// Driver code
    let arr = [ 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 ];
    let N = arr.length;
    document.write(Solve(arr, N));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
40
```

**时间复杂度:** *O(N) <sup>2</sup>* 其中 N 是数组的大小