# 打印所有数字乘积等于 K 的 N 以内的数字

> 原文:[https://www . geesforgeks . org/print-all-numbers-up-n-having-of-product-of-digits-equal-k/](https://www.geeksforgeeks.org/print-all-numbers-up-to-n-having-product-of-digits-equal-to-k/)

给定两个整数 **N** 和 **K** ，任务是打印范围**【1，N】**中的所有数字，数字的[积等于 **K** 。如果没有找到这样的号码，则打印**-1”**。](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)

**示例:**

> **输入:** N =100，K = 25
> **输出:** 55
> **说明:**只有一个数字 55 的位数乘积等于 K
> 
> **输入:** N = 500，K = 10
> T3】输出: 25 52 125 152 215 251

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如**标志，**来存储是否存在满足给定条件的数字。
*   声明一个函数， **productOfDigits()，**求数字位数的乘积。
*   迭代范围**【1，N】**:
    *   如果**arr【I】**的数字乘积等于 **K** ，则打印该数字并设置**标志= 1** 。
*   如果**标志**等于 **0** ，则表示在**【1，N】**范围内找不到这样的数字。因此，打印 **"-1"** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the product
// of digits of a number
int productOfDigits(int N)
{
    // Stores the product of
    // digits of a number
    int product = 1;

    while (N != 0) {
        product = product * (N % 10);
        N = N / 10;
    }

    // Return the product
    return product;
}

// Function to print all numbers upto
// N having product of digits equal to K
void productOfDigitsK(int N, int K)
{
    // Stores whether any number satisfying
    // the given conditions exists or not
    int flag = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; ++i) {

        // If product of digits of
        // arr[i] is equal to K or not
        if (K == productOfDigits(i)) {

            // Print that number
            cout << i << " ";
            flag = 1;
        }
    }

    // If no numbers are found
    if (flag == 0)
        cout << "-1";
}

// Driver Code
int main()
{
    // Given value of N & K
    int N = 500, K = 10;

    // Function call to print all numbers
    // from [1, N] with product of digits K
    productOfDigitsK(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

  // Function to find the product
  // of digits of a number
  static int productOfDigits(int N)
  {

    // Stores the product of
    // digits of a number
    int product = 1;

    while (N != 0) {
      product = product * (N % 10);
      N = N / 10;
    }

    // Return the product
    return product;
  }

  // Function to print all numbers upto
  // N having product of digits equal to K
  static void productOfDigitsK(int N, int K)
  {
    // Stores whether any number satisfying
    // the given conditions exists or not
    int flag = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; ++i) {

      // If product of digits of
      // arr[i] is equal to K or not
      if (K == productOfDigits(i)) {

        // Print that number
        System.out.print(i + " ");
        flag = 1;
      }
    }

    // If no numbers are found
    if (flag == 0)
      System.out.println(-1);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given value of N & K
    int N = 500, K = 10;

    // Function call to print all numbers
    // from [1, N] with product of digits K
    productOfDigitsK(N, K);
  }
}

// This code is contribute by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the product
# of digits of a number
def productOfDigits(N) :

    # Stores the product of
    # digits of a number
    product = 1;

    while (N != 0) :
        product = product * (N % 10);
        N = N // 10;

    # Return the product
    return product;

# Function to print all numbers upto
# N having product of digits equal to K
def productOfDigitsK(N, K) :

    # Stores whether any number satisfying
    # the given conditions exists or not
    flag = 0;

    # Iterate over the range [1, N]
    for i in range(1, N + 1) :

        # If product of digits of
        # arr[i] is equal to K or not
        if (K == productOfDigits(i)) :

            # Print that number
            print(i, end =" ");
            flag = 1;

    # If no numbers are found
    if (flag == 0) :
        print("-1");

# Driver Code
if __name__ == "__main__" :

    # Given value of N & K
    N = 500; K = 10;

    # Function call to print all numbers
    # from [1, N] with product of digits K
    productOfDigitsK(N, K);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the product
  // of digits of a number
  static int productOfDigits(int N)
  {

    // Stores the product of
    // digits of a number
    int product = 1;

    while (N != 0) {
      product = product * (N % 10);
      N = N / 10;
    }

    // Return the product
    return product;
  }

  // Function to print all numbers upto
  // N having product of digits equal to K
  static void productOfDigitsK(int N, int K)
  {

    // Stores whether any number satisfying
    // the given conditions exists or not
    int flag = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; ++i) {

      // If product of digits of
      // arr[i] is equal to K or not
      if (K == productOfDigits(i)) {

        // Print that number
        Console.Write(i + " ");
        flag = 1;
      }
    }

    // If no numbers are found
    if (flag == 0)
      Console.WriteLine(-1);
  }

  // Driver Code
  static public void Main()
  {

    // Given value of N & K
    int N = 500, K = 10;

    // Function call to print all numbers
    // from [1, N] with product of digits K
    productOfDigitsK(N, K);
  }
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

  // Function to find the product
  // of digits of a number
  function productOfDigits(N)
  {

    // Stores the product of
    // digits of a number
    let product = 1;

    while (N != 0) {
      product = product * (N % 10);
      N = Math.floor(N / 10);
    }

    // Return the product
    return product;
  }

  // Function to print all numbers upto
  // N having product of digits equal to K
  function productOfDigitsK(N, K)
  {
    // Stores whether any number satisfying
    // the given conditions exists or not
    let flag = 0;

    // Iterate over the range [1, N]
    for (let i = 1; i <= N; ++i) {

      // If product of digits of
      // arr[i] is equal to K or not
      if (K == productOfDigits(i)) {

        // Print that number
        document.write(i + " ");
        flag = 1;
      }
    }

    // If no numbers are found
    if (flag == 0)
      document.write(-1);
  }

// Driver Code

     // Given value of N & K
    let N = 500, K = 10;

    // Function call to print all numbers
    // from [1, N] with product of digits K
    productOfDigitsK(N, K);

</script>
```

**Output**

```
25 52 125 152 215 251 
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(1)*