# 查询给定范围内可被其所有数字整除的数字的计数

> 原文:[https://www . geesforgeks . org/query-to-count-numbers-from-给定范围内可被其所有数字整除的数字/](https://www.geeksforgeeks.org/queries-to-count-numbers-from-given-range-which-are-divisible-by-all-its-digits/)

给定一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【】**每一行的查询形式 **{ L，R }** ，任务是对范围**【L，R】**内的数字进行计数，使得该数字可被其所有非零数字整除。

**示例:**

> **输入:** arr[][] ={ {1，5}，{12，14} }
> **输出:** 5 1
> **解释:**
> 查询 1:范围[1，5]内的所有数字都可以被它们的数字整除。
> 查询 2:范围[12，14]内可被其所有数字整除的数字只有 12。
> 
> **输入:** arr[][] = { {1，20} }
> **输出:** 14
> **解释:**
> 范围内可被其所有非零数字整除的数字为:{1，2，3，4，5，6，7，8，9，10，11，12，15，20}

**天真方法:**解决这个问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[][]** 并且对于数组的每一个 **i <sup>第</sup>T9】行，迭代范围**【L，R】**。对于范围中的每个元素，检查该数字是否能被其所有非零数字整除。如果发现为真，则增加计数。最后，打印获得的计数。
***时间复杂度:**O(N *(R–L))，其中 N 为行数*
***辅助空间:** O(1)***

**高效方法:**上述方法可以通过找到 **arr[i][1]** 的最大可能值并使用[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)预计算可被其非零数字整除的数字计数来优化。按照以下步骤解决问题:

*   初始化一个变量，比如 **Max** ，以存储 **arr[i][1]** 的最大可能值。
*   初始化一个数组，比如说 **prefCntDiv[]** ，其中 **prefCntDiv[i]** 存储范围**【1，I】**中可被非零数字整除的数字计数。
*   迭代范围**【1，最大】**。对于每一次**I<sup>T5】迭代，检查 **i** 是否能被其所有非零数字整除。如果发现为真，则更新**prefntcdiv[I]= prefntcdiv[I–1]+1**。</sup>**
*   否则，更新**prefCntDiv[I]= prefCntDiv[I–1]**。
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。对于数组的第 i <sup>行</sup>行，打印**precntdiv[arr[I][1]]–precntdiv[arr[I][0]–1]。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define Max 1000005

// Function to check if a number is divisible
// by all of its non-zero digits or not
bool CheckDivByAllDigits(int number)
{
    // Stores the number
    int n = number;

    // Iterate over the digits
    // of the numbers
    while (n > 0) {

        // If digit of number
        // is non-zero
        if (n % 10)

            // If number is not divisible
            // by its current digit
            if (number % (n % 10)) {

                return false;
            }

        // Update n
        n /= 10;
    }
    return true;
}

// Function to count of numbers which are
// divisible by all of its non-zero
// digits in the range [1, i]
void cntNumInRang(int arr[][2], int N)
{

    // Stores count of numbers which are
    // divisible by all of its non-zero
    // digits in the range [1, i]
    int prefCntDiv[Max] = { 0 };

    // Iterate over the range [1, Max]
    for (int i = 1; i <= Max; i++) {

        // Update
        prefCntDiv[i] = prefCntDiv[i - 1]
                        + (CheckDivByAllDigits(i));
    }

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++)
        cout << (prefCntDiv[arr[i][1]]
                 - prefCntDiv[arr[i][0] - 1])
             << " ";
}

// Driver Code
int main()
{
    int arr[][2] = { { 1, 5 }, { 12, 14 } };

    int N = sizeof(arr) / sizeof(arr[0]);
    cntNumInRang(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
class GFG
{
  public static int Max = 1000005;

  // Function to check if a number is divisible
  // by all of its non-zero digits or not
  static boolean CheckDivByAllDigits(int number)
  {

    // Stores the number
    int n = number;

    // Iterate over the digits
    // of the numbers
    while (n > 0)
    {

      // If digit of number
      // is non-zero
      if (n % 10 != 0)

        // If number is not divisible
        // by its current digit
        if (number % (n % 10) != 0)
        {
          return false;
        }

      // Update n
      n /= 10;
    }
    return true;
  }

  // Function to count of numbers which are
  // divisible by all of its non-zero
  // digits in the range [1, i]
  static void cntNumInRang(int arr[][], int N)
  {

    // Stores count of numbers which are
    // divisible by all of its non-zero
    // digits in the range [1, i]
    int prefCntDiv[] = new int[Max + 1];

    // Iterate over the range [1, Max]
    for (int i = 1; i <= Max; i++)
    {

      int ans = 0;
      if (CheckDivByAllDigits(i))
        ans = 1;

      // Update
      prefCntDiv[i] = prefCntDiv[i - 1] + ans;
    }

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++)
      System.out.print((prefCntDiv[arr[i][1]]
                        - prefCntDiv[arr[i][0] - 1])
                       + " ");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[][] = { { 1, 5 }, { 12, 14 } };
    int N = arr.length;
    cntNumInRang(arr, N);
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a number is divisible
# by all of its non-zero digits or not
def CheckDivByAllDigits(number):

    # Stores the number
    n = number

    # Iterate over the digits
    # of the numbers
    while (n > 0):

        # If digit of number
        # is non-zero
        if (n % 10):

            # If number is not divisible
            # by its current digit
            if (number % (n % 10)):
                return False

        # Update n
        n //= 10
    return True

# Function to count of numbers which are
# divisible by all of its non-zero
# digits in the range [1, i]
def cntNumInRang(arr, N):
    global Max

    # Stores count of numbers which are
    # divisible by all of its non-zero
    # digits in the range [1, i]
    prefCntDiv = [0]*Max

    # Iterate over the range [1, Max]
    for i in range(1, Max):

        # Update
        prefCntDiv[i] = prefCntDiv[i - 1] + (CheckDivByAllDigits(i))

    # Traverse the array, arr[]
    for i in range(N):
        print(prefCntDiv[arr[i][1]]- prefCntDiv[arr[i][0] - 1], end = " ")

# Driver Code
if __name__ == '__main__':
    arr =[ [ 1, 5 ], [12, 14]]
    Max = 1000005

    N = len(arr)
    cntNumInRang(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{
  public static int Max = 1000005;

  // Function to check if a number is divisible
  // by all of its non-zero digits or not
  static bool CheckDivByAllDigits(int number)
  {

    // Stores the number
    int n = number;

    // Iterate over the digits
    // of the numbers
    while (n > 0) {

      // If digit of number
      // is non-zero
      if (n % 10 != 0)

        // If number is not divisible
        // by its current digit
        if (number % (n % 10) != 0)
        {
          return false;
        }

      // Update n
      n /= 10;
    }
    return true;
  }

  // Function to count of numbers which are
  // divisible by all of its non-zero
  // digits in the range [1, i]
  static void cntNumInRang(int[, ] arr, int N)
  {

    // Stores count of numbers which are
    // divisible by all of its non-zero
    // digits in the range [1, i]
    int[] prefCntDiv = new int[Max + 1];

    // Iterate over the range [1, Max]
    for (int i = 1; i <= Max; i++) {

      int ans = 0;
      if (CheckDivByAllDigits(i))
        ans = 1;

      // Update
      prefCntDiv[i] = prefCntDiv[i - 1] + ans;
    }

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++)
      Console.Write((prefCntDiv[arr[i, 1]]
                     - prefCntDiv[arr[i, 0] - 1])
                    + " ");
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[, ] arr = { { 1, 5 }, { 12, 14 } };
    int N = arr.GetLength(0);
    cntNumInRang(arr, N);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

const Max = 1000005;

// Function to check if a number is divisible
// by all of its non-zero digits or not
function CheckDivByAllDigits(number)
{
    // Stores the number
    let n = number;

    // Iterate over the digits
    // of the numbers
    while (n > 0) {

        // If digit of number
        // is non-zero
        if (n % 10)

            // If number is not divisible
            // by its current digit
            if (number % (n % 10)) {

                return false;
            }

        // Update n
        n = parseInt(n / 10);
    }
    return true;
}

// Function to count of numbers which are
// divisible by all of its non-zero
// digits in the range [1, i]
function cntNumInRang(arr, N)
{

    // Stores count of numbers which are
    // divisible by all of its non-zero
    // digits in the range [1, i]
    let prefCntDiv = new Array(Max).fill(0);

    // Iterate over the range [1, Max]
    for (let i = 1; i <= Max; i++) {

        // Update
        prefCntDiv[i] = prefCntDiv[i - 1]
                        + (CheckDivByAllDigits(i));
    }

    // Traverse the array, arr[]
    for (let i = 0; i < N; i++)
        document.write((prefCntDiv[arr[i][1]]
                 - prefCntDiv[arr[i][0] - 1])
             + " ");
}

// Driver Code
    let arr = [ [ 1, 5 ], [ 12, 14 ] ];

    let N = arr.length;
    cntNumInRang(arr, N);

</script>
```

**Output:** 

```
5 1
```

***时间复杂度:** O(N + Max)，其中 Max 为 arr[i][1]*
***辅助空间:** O(N)*