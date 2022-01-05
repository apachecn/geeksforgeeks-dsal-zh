# 通过将数组的所有元素乘以任意值，将数组的任意子集的和减为 1

> 原文:[https://www . geeksforgeeks . org/通过将其所有元素乘以任意值将数组的任意子集的总和减少为 1/](https://www.geeksforgeeks.org/reduce-sum-of-any-subset-of-an-array-to-1-by-multiplying-all-its-elements-by-any-value/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是检查给定数组的任意[子集](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的元素之和在将其所有元素乘以任意整数后是否可以简化为 **1** 。如果不可能，则打印**“否”**。否则，打印**“是”**。

**示例:**

> ***输入:** arr[] = {29，6，4，10}*
> ***输出:**是*
> ***解释:***
> *选择一个子集{29，6，10}，将每个对应的元素乘以{1，-3，-1}。*
> *因此，子集之和= 29 *(1)+6 *(3)+10 *(1)= 29–18–10 = 1。*
> *故印“是”。*
> 
> ***输入:** arr[] = {6，3，9}*
> ***输出:**否*

**天真方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的所有可能子集，如果数组中存在任何子集，那么它的元素之和在乘以任何整数后等于 1，然后打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效法:**上述方法也可以通过使用[贝祖特的恒等式(贝祖特引理)](https://www.geeksforgeeks.org/bezouts-identity-bezouts-lemma/)进行优化，其中规定如果任意两个整数 **a** 和 **b** 的 [GCD 等于 **d** ，则存在整数 **x** 和 **y** ，使得**a * x+b * y = d【T0**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)

因此，想法是检查给定数组**arr【】**的 [GCD 是否可以做成 **1** 。因此，要满足给定的条件，必须存在任意两个元素的 **GCD** 为 **1** ，那么数组的 GCD 将等于 **1** 。因此，打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    // Base Case
    if (a == 0)
        return b;

    // Find the GCD recursively
    return gcd(b % a, a);
}

// Function to calculate the GCD
// of the array arr[]
int findGCDofArray(int arr[], int N)
{
    // Stores the GCD of array
    int g = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update gcd of the array
        g = gcd(g, arr[i]);

        // If gcd is 1, then return 1
        if (g == 1) {
            return 1;
        }
    }

    // Return the resultant GCD
    return g;
}

// Function to check if a subset satisfying
// the given condition exists or not
void findSubset(int arr[], int N)
{

    // Calculate the gcd of the array
    int gcd = findGCDofArray(arr, N);

    // If gcd is 1, then print Yes
    if (gcd == 1) {
        cout << "Yes";
    }

    // Otherwise, print No
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int arr[] = { 29, 6, 4, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findSubset(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG
{

  // Function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Base Case
    if (a == 0)
      return b;

    // Find the GCD recursively
    return gcd(b % a, a);
  }

  // Function to calculate the GCD
  // of the array arr[]
  static int findGCDofArray(int arr[], int N)
  {

    // Stores the GCD of array
    int g = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

      // Update gcd of the array
      g = gcd(g, arr[i]);

      // If gcd is 1, then return 1
      if (g == 1) {
        return 1;
      }
    }

    // Return the resultant GCD
    return g;
  }

  // Function to check if a subset satisfying
  // the given condition exists or not
  static void findSubset(int arr[], int N)
  {

    // Calculate the gcd of the array
    int gcd = findGCDofArray(arr, N);

    // If gcd is 1, then print Yes
    if (gcd == 1) {
      System.out.println("Yes");
    }

    // Otherwise, print No
    else {
      System.out.println("No");
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 29, 6, 4, 10 };

    // length of the array
    int N = arr.length;

    // function call
    findSubset(arr, N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return gcd of a and b
def gcd(a, b):

    # Base Case
    if (a == 0):
        return b

    # Find the GCD recursively
    return gcd(b % a, a)

# Function to calculate the GCD
# of the array arr[]
def findGCDofArray(arr, N):

    # Stores the GCD of array
    g = 0

    # Traverse the array arr[]
    for i in range(N):

        # Update gcd of the array
        g = gcd(g, arr[i])

        # If gcd is 1, then return 1
        if (g == 1):
            return 1

    # Return the resultant GCD
    return g

# Function to check if a subset satisfying
# the given condition exists or not
def findSubset(arr, N):

    # Calculate the gcd of the array
    gcd = findGCDofArray(arr, N)

    # If gcd is 1, then prYes
    if (gcd == 1):
        print("Yes")

    # Otherwise, prNo
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    arr = [29, 6, 4, 10]

    N = len(arr)

    findSubset(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Base Case
    if (a == 0)
      return b;

    // Find the GCD recursively
    return gcd(b % a, a);
  }

  // Function to calculate the GCD
  // of the array arr[]
  static int findGCDofArray(int[] arr, int N)
  {

    // Stores the GCD of array
    int g = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

      // Update gcd of the array
      g = gcd(g, arr[i]);

      // If gcd is 1, then return 1
      if (g == 1) {
        return 1;
      }
    }

    // Return the resultant GCD
    return g;
  }

  // Function to check if a subset satisfying
  // the given condition exists or not
  static void findSubset(int[] arr, int N)
  {

    // Calculate the gcd of the array
    int gcd = findGCDofArray(arr, N);

    // If gcd is 1, then print Yes
    if (gcd == 1) {
      Console.Write("Yes");
    }

    // Otherwise, print No
    else {
      Console.Write("No");
    }
  }

  // Driver code
  public static void Main(String[] args)
  {
    int[] arr = { 29, 6, 4, 10 };
    int N = arr.Length;
    findSubset(arr, N);
  }
}

// This code is contributed by shivani
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function to return gcd of a and b
    function gcd(a , b) {

        // Base Case
        if (a == 0)
            return b;

        // Find the GCD recursively
        return gcd(b % a, a);
    }

    // Function to calculate the GCD
    // of the array arr
    function findGCDofArray(arr , N) {

        // Stores the GCD of array
        var g = 0;

        // Traverse the array arr
        for (i = 0; i < N; i++) {

            // Update gcd of the array
            g = gcd(g, arr[i]);

            // If gcd is 1, then return 1
            if (g == 1) {
                return 1;
            }
        }

        // Return the resultant GCD
        return g;
    }

    // Function to check if a subset satisfying
    // the given condition exists or not
    function findSubset(arr , N) {

        // Calculate the gcd of the array
        var gcd = findGCDofArray(arr, N);

        // If gcd is 1, then print Yes
        if (gcd == 1) {
            document.write("Yes");
        }

        // Otherwise, print No
        else {
            document.write("No");
        }
    }

    // Driver code

        // Given array
        var arr = [ 29, 6, 4, 10 ];

        // length of the array
        var N = arr.length;

        // function call
        findSubset(arr, N);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N * log(M))，其中 M 是数组* *的* [*最小元素。*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)