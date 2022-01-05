# 打印一个数组中的所有完全数，该数组的数字总和也是一个完全数

> 原文:[https://www . geeksforgeeks . org/print-all-perfect-numbers-from-from-a-array-其数字总和也是-perfect-number/](https://www.geeksforgeeks.org/print-all-perfect-numbers-from-an-array-whose-sum-of-digits-is-also-a-perfect-number/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从一个数组中打印所有的[完全数](https://www.geeksforgeeks.org/perfect-number/)，该数组的[位数总和](https://www.geeksforgeeks.org/how-can-we-sum-the-digits-of-a-given-number-in-single-statement/)也是一个[完全数](https://www.geeksforgeeks.org/perfect-number/)。

**示例:**

> ***输入:** arr[] = { 3，8，12，28，6 }*
> ***输出:** 6*
> ***说明:**数组元素 arr[4] ( **=** 6)是一个完全数。数组元素 arr[3] (= 28)是一个完全数，但它的位数之和(= 10)不是一个完全数。*
> 
> ***输入:** arr[] = { 1，2，3 }*
> ***输出:** 1*

**方法:**按照以下步骤解决问题:

1.  声明一个函数， **isPerfect()** 检查[这个数字是不是一个完全数。](https://www.geeksforgeeks.org/perfect-number/)
2.  声明另一个函数， **sumOfDigits()** 来计算一个数的所有数字的[和。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)
3.  [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】:
    *   如果 **arr[i]** 是一个[完全数](https://www.geeksforgeeks.org/perfect-number/):
        *   初始化一个变量，比如 **digitSum，**来存储当前数组元素的位数总和。
        *   如果 **digitSum** 也是一个完美的数字，打印那个数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is perfect number or not
int isPerfect(int N)
{
    // Stores sum of proper divisors
    int sumOfDivisors = 1;
    for (int i = 2; i <= N / 2; ++i) {

        if (N % i == 0) {
            sumOfDivisors += i;
        }
    }

    // If sum of digits is equal to N,
    // then it's a perfect number
    if (sumOfDivisors == N) {
        return 1;
    }

    // Otherwise, not a perfect number
    else
        return 0;
}

// Function to find the
// sum of digits of a number
int sumOfDigits(int N)
{
    // Stores sum of digits
    int sum = 0;

    while (N != 0) {
        sum += (N % 10);
        N = N / 10;
    }

    // Return sum of digits
    return sum;
}

// Function to count perfect numbers from
// an array whose sum of digits is also perfect
void countPerfectNumbers(int arr[], int N)
{
    // Traverse the array
    for (int i = 0; i < N; ++i) {

        // If number is perfect
        if (isPerfect(arr[i])) {

            // Stores sum of digits
            // of the number
            int sum = sumOfDigits(arr[i]);

            // If that is also perfect number
            if (isPerfect(sum)) {

                // Print that number
                cout << arr[i] << " ";
            }
        }
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 3, 8, 12, 28, 6 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to count perfect numbers
    // having sum of digits also perfect
    countPerfectNumbers(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

  // Function to check if a number
  // is perfect number or not
  static boolean isPerfect(int N)
  {
    // Stores sum of proper divisors
    int sumOfDivisors = 1;
    for (int i = 2; i <= N / 2; ++i) {

      if (N % i == 0) {
        sumOfDivisors += i;
      }
    }

    // If sum of digits is equal to N,
    // then it's a perfect number
    if (sumOfDivisors == N) {
      return true;
    }

    // Otherwise, not a perfect number
    else
      return false;
  }

  // Function to find the
  // sum of digits of a number
  static int sumOfDigits(int N)
  {
    // Stores sum of digits
    int sum = 0;

    while (N != 0) {
      sum += (N % 10);
      N = N / 10;
    }

    // Return sum of digits
    return sum;
  }

  // Function to count perfect numbers from
  // an array whose sum of digits is also perfect
  static void countPerfectNumbers(int arr[], int N)
  {
    // Traverse the array
    for (int i = 0; i < N; ++i) {

      // If number is perfect
      if (isPerfect(arr[i])) {

        // Stores sum of digits
        // of the number
        int sum = sumOfDigits(arr[i]);

        // If that is also perfect number
        if (isPerfect(sum)) {

          // Print that number
          System.out.print(arr[i] + " ");
        }
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 3, 8, 12, 28, 6 };

    // Size of the array
    int N = arr.length;

    // Function call to count perfect numbers
    // having sum of digits also perfect
    countPerfectNumbers(arr, N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to check if a number
# is perfect number or not
def isPerfect(N):

    # Stores sum of proper divisors
    sumOfDivisors = 1;
    for i in range(2, int(N / 2) + 1):

        if (N % i == 0):
            sumOfDivisors += i;

    # If sum of digits is equal to N,
    # then it's a perfect number
    if (sumOfDivisors == N):
        return True;

    # Otherwise, not a perfect number
    else:
        return False;

# Function to find the
# sum of digits of a number
def sumOfDigits(N):

    # Stores sum of digits
    sum = 0;

    while (N != 0):
        sum += (N % 10);
        N = N // 10;

    # Return sum of digits
    return sum;

# Function to count perfect numbers from
# an array whose sum of digits is also perfect
def countPerfectNumbers(arr, N):

    # Traverse the array
    for i in range(N):

        # If number is perfect
        if (isPerfect(arr[i])):

            # Stores sum of digits
            # of the number
            sum = sumOfDigits(arr[i]);

            # If that is also perfect number
            if (isPerfect(sum)):

                # Print that number
                print(arr[i], end=" ");

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [3, 8, 12, 28, 6];

    # Size of the array
    N = len(arr);

    # Function call to count perfect numbers
    # having sum of digits also perfect
    countPerfectNumbers(arr, N);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to check if a number
  // is perfect number or not
  static bool isPerfect(int N)
  {

    // Stores sum of proper divisors
    int sumOfDivisors = 1;
    for (int i = 2; i <= N / 2; ++i) {

      if (N % i == 0) {
        sumOfDivisors += i;
      }
    }

    // If sum of digits is equal to N,
    // then it's a perfect number
    if (sumOfDivisors == N) {
      return true;
    }

    // Otherwise, not a perfect number
    else
      return false;
  }

  // Function to find the
  // sum of digits of a number
  static int sumOfDigits(int N)
  {

    // Stores sum of digits
    int sum = 0;

    while (N != 0) {
      sum += (N % 10);
      N = N / 10;
    }

    // Return sum of digits
    return sum;
  }

  // Function to count perfect numbers from
  // an array whose sum of digits is also perfect
  static void countPerfectNumbers(int []arr, int N)
  {

    // Traverse the array
    for (int i = 0; i < N; ++i) {

      // If number is perfect
      if (isPerfect(arr[i])) {

        // Stores sum of digits
        // of the number
        int sum = sumOfDigits(arr[i]);

        // If that is also perfect number
        if (isPerfect(sum)) {

          // Print that number
          Console.Write(arr[i] + " ");
        }
      }
    }
  }

// Driver Code
static public void Main()
{

    // Given array
    int []arr = { 3, 8, 12, 28, 6 };

    // Size of the array
    int N = arr.Length;

    // Function call to count perfect numbers
    // having sum of digits also perfect
    countPerfectNumbers(arr, N);
}
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to check if a number
// is perfect number or not
function isPerfect(N)
{

    // Stores sum of proper divisors
    let sumOfDivisors = 1;
    for (let i = 2; i <= Math.floor(N / 2); ++i)
    {

        if (N % i === 0)
        {
            sumOfDivisors += i;
        }
    }

    // If sum of digits is equal to N,
    // then it's a perfect number
    if (sumOfDivisors === N) {
        return 1;
    }

    // Otherwise, not a perfect number
    else
        return 0;
}

// Function to find the
// sum of digits of a number
function sumOfDigits(N)
{
    // Stores sum of digits
    let sum = 0;

    while (N != 0) {
        sum += (N % 10);
        N = Math.floor(N / 10);
    }

    // Return sum of digits
    return sum;
}

// Function to count perfect numbers from
// an array whose sum of digits is also perfect
function countPerfectNumbers(arr, N)
{
    // Traverse the array
    for (let i = 0; i < N; ++i) {

        // If number is perfect
        if (isPerfect(arr[i])) {

            // Stores sum of digits
            // of the number
            let sum = sumOfDigits(arr[i]);

            // If that is also perfect number
            if (isPerfect(sum)) {

                // Print that number
                document.write(arr[i] + " ");
            }
        }
    }
}

// Driver Code

    // Given array
    let arr = [ 3, 8, 12, 28, 6 ];

    // Size of the array
    let N = arr.length;

    // Function call to count perfect numbers
    // having sum of digits also perfect
    countPerfectNumbers(arr, N);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>3</sup>* log N)*
***辅助空间:** O(1)*