# 计数第一个和最后一个数字相同的非回文数组元素

> 原文:[https://www . geesforgeks . org/count-非回文-数组-元素-具有相同的第一个和最后一个数字/](https://www.geeksforgeeks.org/count-non-palindromic-array-elements-having-same-first-and-last-digit/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是打印给定数组中第一个和最后一个数字相同的非回文数字的计数。

**示例:**

> **输入:** arr[]={121，134，2342，4514}
> **输出:** 2
> **说明:** 2342 和 4514 是前后数字相同的非回文数字。因此，所需的输出为 2。
> 
> **输入:** arr[]={1，22，4545 }
> T3】输出: 0

**方法:**通过检查每个数组元素，不管是不是[回文](https://www.geeksforgeeks.org/program-to-check-the-number-is-palindrome-or-not/)都可以解决这个问题。按照步骤解决问题。

1.  [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。
2.  对于每个数组元素**arr【I】**，检查它是否是回文。
3.  对于每个发现为非回文的数组元素，在反转数字之前和之后提取最后一位数字。提取后，检查数字是否相等。
4.  如果发现是真的，增加计数。
5.  最后，打印此类数字的计数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to reverse a number
int revNum(int N)
{
    // Store the reverse of N
    int x = 0;
    while (N) {
        x = x * 10 + N % 10;
        N = N / 10;
    }

    // Return reverse of N
    return x;
}

// Function to get the count of non-palindromic
// numbers having same first and last digit
int ctNonPalin(int arr[], int N)
{

    // Store the required count
    int Res = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Store reverse of arr[i]
        int x = revNum(arr[i]);

        // Check for palindrome
        if (x == arr[i]) {
            continue;
        }

        // IF non-palindromic
        else {
            // Check if first and last
            // digits are equal
            Res += (arr[i] % 10 == N % 10);
        }
    }
    return Res;
}

// Driver Code
int main()
{
    int arr[] = { 121, 134, 2342, 4514 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << ctNonPalin(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to reverse a number
static int revNum(int N)
{

    // Store the reverse of N
    int x = 0;

    while (N != 0)
    {
        x = x * 10 + N % 10;
        N = N / 10;
    }

    // Return reverse of N
    return x;
}

// Function to get the count of non-palindromic
// numbers having same first and last digit
static int ctNonPalin(int arr[], int N)
{

    // Store the required count
    int Res = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Store reverse of arr[i]
        int x = revNum(arr[i]);

        // Check for palindrome
        if (x == arr[i])
        {
            continue;
        }

        // IF non-palindromic
        else
        {

            // Check if first and last
            // digits are equal
            if(arr[i] % 10 == x % 10)
                Res += 1;
        }
    }
    return Res;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 121, 134, 2342, 4514 };
    int N = arr.length;

    System.out.println(ctNonPalin(arr, N));
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to reverse a number
def revNum(N):

    # Store the reverse of N
    x = 0
    while (N):
        x = x * 10 + N % 10
        N = N // 10

    # Return reverse of N
    return x

# Function to get the count of non-palindromic
# numbers having same first and last digit
def ctNonPalin(arr, N):

    # Store the required count
    Res = 0

    # Traverse the array
    for i in range(N):

        # Store reverse of arr[i]
        x = revNum(arr[i])

        # Check for palindrome
        if (x == arr[i]):
            continue

        # IF non-palindromic
        else:

            # Check if first and last
            # digits are equal
            Res += (arr[i] % 10 == N % 10)

    return Res

# Driver Code
if __name__ == '__main__':

    arr = [ 121, 134, 2342, 4514 ]
    N = len(arr)

    print(ctNonPalin(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to reverse a number
static int revNum(int N)
{

    // Store the reverse of N
    int x = 0;

    while (N != 0)
    {
        x = x * 10 + N % 10;
        N = N / 10;
    }

    // Return reverse of N
    return x;
}

// Function to get the count of non-palindromic
// numbers having same first and last digit
static int ctNonPalin(int[] arr, int N)
{

    // Store the required count
    int Res = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Store reverse of arr[i]
        int x = revNum(arr[i]);

        // Check for palindrome
        if (x == arr[i])
        {
            continue;
        }

        // IF non-palindromic
        else
        {

            // Check if first and last
            // digits are equal
            if(arr[i] % 10 == x % 10)
                Res += 1;
        }
    }
    return Res;
}

// Driver code
public static void Main ()
{
    int[] arr = new int[]{ 121, 134, 2342, 4514 };
    int N = arr.Length;

    Console.WriteLine(ctNonPalin(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach

      // Function to reverse a number
      function revNum(N) {
        // Store the reverse of N
        var x = 0;
        while (N) {
          x = x * 10 + (N % 10);
          N = N / 10;
        }

        // Return reverse of N
        return x;
      }

      // Function to get the count of non-palindromic
      // numbers having same first and last digit
      function ctNonPalin(arr, N) {
        // Store the required count
        var Res = 0;

        // Traverse the array
        for (var i = 0; i < N; i++) {
          // Store reverse of arr[i]
          var x = revNum(arr[i]);

          // Check for palindrome
          if (x == arr[i]) {
            continue;
          }

          // IF non-palindromic
          else {
            // Check if first and last
            // digits are equal
            Res += arr[i] % 10 == N % 10;
          }
        }
        return Res;
      }

      // Driver Code
      var arr = [121, 134, 2342, 4514];
      var N = arr.length;
      document.write(ctNonPalin(arr, N));
    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * D)其中 D 是数组中最大数的长度。*
***辅助空间:** O(D)*