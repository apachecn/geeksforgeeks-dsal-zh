# 将数组拆分为两个子序列，子序列对的最小计数和等于 X

> 原文:[https://www . geesforgeks . org/split-array-in-two-subseries-with-count-of-with-sum-equal-x/](https://www.geeksforgeeks.org/split-array-into-two-subsequences-having-minimum-count-of-pairs-with-sum-equal-to-x/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是将该数组拆分为两个子序列，使得两个数组中总和等于 **X** 的对的数量最小。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，X = 7
> **输出:**
> 第一个数组是–1 2 3
> 第二个数组是–4 5 6
> **解释:**
> 第一个数组中可能的 3 对是{(1，2)，(2，3)，(1，3)}。这些对的和都不等于 X (= 7)。
> 第二个数组中可能的 3 对是{(4，5)，(5，6)，(4，6)}。这些对的和都不等于 X (= 7)。
> 
> **输入** : arr[] = {3，3，3}，X = 6
> **输出:**
> 第一个数组是–3
> 第二个数组是–3 3

**方法:**按照以下步骤解决问题:

*   创建两个数组来存储两个分开的子序列。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   **如果 arr[i] * 2 < X:** 将其插入第一个数组。
    *   由于第一个数组当前包含所有小于 **X / 2** 的数字，因此当前数组中没有任何对的和等于 **X** 。
    *   **如果 arr[i] * 2 > X:** 将其插入第二个数组。
    *   由于第二个数组当前包含所有大于 **X / 2** 的数字，因此当前数组中没有一对的和等于 **X** 。
    *   **如果 arr[i] * 2 < X:** 交替地将元素分别插入到第一个和第二个数组中，以获得最小对。
*   最后，在完成数组遍历后，打印两个数组。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split the array
// into two subsequences
void solve(int arr[], int N, int X)
{
    // Stores the two subsequences
    vector<int> A, B;

    // Flag to set/reset to split
    // arrays elements alternately
    // into two arrays
    int c = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // If 2 * arr[i] is less than X
        if ((2 * arr[i]) < X) {

            // Push element into
            // the first array
            A.push_back(arr[i]);
        }

        // If 2 * arr[i] is greater than X
        else if ((2 * arr[i]) > X) {

            // Push element into
            // the second array
            B.push_back(arr[i]);
        }

        // If 2 * arr[i] is equal to X
        else {

            // Alternatively place the
            // elements into the two arrays
            if (c % 2 == 0) {

                A.push_back(arr[i]);
            }
            else {

                B.push_back(arr[i]);
            }
            c++;
        }
    }

    // Print both the arrays
    cout << "The First Array is - ";
    for (int i = 0; i < A.size(); i++) {

        cout << A[i] << " ";
    }
    cout << endl;
    cout << "The Second Array is - ";
    for (int i = 0; i < B.size(); i++) {

        cout << B[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 4, 3,
                  6, 2, 4, 3 };
    int X = 7;

    // Size of the array
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function Call
    solve(arr, N, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to split the array
// into two subsequences
static void solve(int arr[],
                  int N, int X)
{
  // Stores the two subsequences
  Vector<Integer> A =
         new Vector<Integer>(),
   B = new Vector<Integer>();

  // Flag to set/reset to split
  // arrays elements alternately
  // into two arrays
  int c = 0;

  // Traverse the given array
  for (int i = 0; i < N; i++)
  {
    // If 2 * arr[i] is
    // less than X
    if ((2 * arr[i]) < X)
    {
      // Push element into
      // the first array
      A.add(arr[i]);
    }

    // If 2 * arr[i] is greater
    // than X
    else if ((2 * arr[i]) > X)
    {
      // Push element into
      // the second array
      B.add(arr[i]);
    }

    // If 2 * arr[i] is
    // equal to X
    else
    {
      // Alternatively place the
      // elements into the two arrays
      if (c % 2 == 0)
      {
        A.add(arr[i]);
      }
      else
      {
        B.add(arr[i]);
      }
      c++;
    }
  }

  // Print both the arrays
  System.out.print("The First Array is - ");
  for (int i = 0; i < A.size(); i++)
  {
    System.out.print(A.get(i) + " ");
  }

  System.out.println();

  System.out.print("The Second Array is - "); 
  for (int i = 0; i < B.size(); i++)
  {
    System.out.print(B.get(i) + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 5, 4, 3,
               6, 2, 4, 3};
  int X = 7;

  // Size of the array
  int N = arr.length;

  // Function Call
  solve(arr, N, X);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to split the array
# into two subsequences
def solve(arr, N, X):

    # Stores the two subsequences
    A = []
    B = []

    # Flag to set/reset to split
    # arrays elements alternately
    # into two arrays
    c = 0

    # Traverse the given array
    for i in range(N):

        # If 2 * arr[i] is less than X
        if ((2 * arr[i]) < X):

            # Push element into
            # the first array
            A.append(arr[i])

        # If 2 * arr[i] is greater than X
        elif ((2 * arr[i]) > X):

            # Push element into
            # the second array
            B.append(arr[i])

        # If 2 * arr[i] is equal to X
        else:

            # Alternatively place the
            # elements into the two arrays
            if (c % 2 == 0):
                A.append(arr[i])
            else:
                B.append(arr[i])

            c += 1

    # Print both the arrays
    print("The First Array is - ", end = " ")
    for i in range(len(A)):
        print(A[i], end = " ")

    print()

    print("The Second Array is - ", end = " ")
    for i in range(len(B)):
        print(B[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 5, 4, 3, 6, 2, 4, 3 ]
    X = 7

    # Size of the array
    N = len(arr)

    # Function Call
    solve(arr, N, X)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to split the array
// into two subsequences
static void solve(int []arr,
                  int N, int X)
{
  // Stores the two subsequences
  List<int> A =
       new List<int>(),
   B = new List<int>();

  // Flag to set/reset to
  // split arrays elements
  // alternately into two
  // arrays
  int c = 0;

  // Traverse the given array
  for (int i = 0; i < N; i++)
  {
    // If 2 * arr[i] is
    // less than X
    if ((2 * arr[i]) < X)
    {
      // Push element into
      // the first array
      A.Add(arr[i]);
    }

    // If 2 * arr[i] is greater
    // than X
    else if ((2 * arr[i]) > X)
    {
      // Push element into
      // the second array
      B.Add(arr[i]);
    }

    // If 2 * arr[i] is
    // equal to X
    else
    {
      // Alternatively place the
      // elements into the two arrays
      if (c % 2 == 0)
      {
        A.Add(arr[i]);
      }
      else
      {
        B.Add(arr[i]);
      }
      c++;
    }
  }

  // Print both the arrays
  Console.Write("The First Array is - ");
  for (int i = 0; i < A.Count; i++)
  {
    Console.Write(A[i] + " ");
  }

  Console.WriteLine();

  Console.Write("The Second Array is - "); 
  for (int i = 0; i < B.Count; i++)
  {
    Console.Write(B[i] + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {1, 5, 4, 3,
               6, 2, 4, 3};
  int X = 7;

  // Size of the array
  int N = arr.Length;

  // Function Call
  solve(arr, N, X);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to split the array
// into two subsequences
function solve(arr, N, X)
{

    // Stores the two subsequences
    var A = [], B = [];

    // Flag to set/reset to split
    // arrays elements alternately
    // into two arrays
    var c = 0;

    // Traverse the given array
    for(var i = 0; i < N; i++)
    {

        // If 2 * arr[i] is less than X
        if ((2 * arr[i]) < X)
        {

            // Push element into
            // the first array
            A.push(arr[i]);
        }

        // If 2 * arr[i] is greater than X
        else if ((2 * arr[i]) > X)
        {

            // Push element into
            // the second array
            B.push(arr[i]);
        }

        // If 2 * arr[i] is equal to X
        else
        {

            // Alternatively place the
            // elements into the two arrays
            if (c % 2 == 0)
            {
                A.push(arr[i]);
            }
            else
            {
                B.push(arr[i]);
            }
            c++;
        }
    }

    // Print both the arrays
    document.write( "The First Array is - ");
    for(var i = 0; i < A.length; i++)
    {
        document.write( A[i] + " ");
    }
    document.write("<br>");
    document.write( "The Second Array is - ");
    for(var i = 0; i < B.length; i++)
    {
        document.write( B[i] + " ");
    }
}

// Driver Code
var arr = [ 1, 5, 4, 3, 6, 2, 4, 3 ];
var X = 7;

// Size of the array
var N = arr.length;

// Function Call
solve(arr, N, X);

// This code is contributed by noob2000

</script>
```

**Output**

```
The First Array is - 1 3 2 3 
The Second Array is - 5 4 6 4 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)