# 重新排列数组以获得前缀 GCDs 连接的最大可能值

> 原文:[https://www . geesforgeks . org/重排-数组-获取-最大可能值-前缀串联-gcds/](https://www.geeksforgeeks.org/rearrange-array-to-obtain-maximum-possible-value-of-concatenation-of-prefix-gcds/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是重新排列数组元素，使得对于每个索引 **i** 将数组元素的 [GCD 从索引 **0** 到 **i** 连接起来所形成的数量是最大可能的。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

**示例:**

> **输入:** arr[] = {4，2，5}
> **输出:** 5 4 2
> **说明:**
> X = 511 是 arr[]的所有重排中可以得到的 X 的最大值。
> arr[]的可能排列为:
> arr[] = [2，4，5] → X = 221
> arr[] = [2，5，4] → X = 211
> arr[] = [4，2，5] → X = 421
> arr[] = [4，5，2] → X = 411
> arr[] = [5，4，2] → X = 511
> arr[] = [5，2，4] →
> 
> **输入:** arr[] = {2，4，6，8}
> **输出:** 8 4 6 2
> **说明:**
> X = 842 是 arr[]的所有重排中能得到的 X 的最大值。
> arr[]的可能排列为:
> arr[] = [4，6，8] → X = 422
> arr[] = [4，8，6] → X = 442
> arr[] = [6，4，8] → X = 622
> arr[] = [6，8，4] → X = 622
> arr[] = [8，4，6] → X = 842
> arr[] = [8，6，4] →

**方法:**单个数字的 GCD 就是数字本身，因此 **X** 的第一位数字，即**X【0】**将始终等于**arr【0】**。因此，为了确保 **X** 在所有可获得的数字中是最大的， **arr[0]** 需要是最大的。然后继续跟踪已经排列好的 **arr[]** 的最长前缀的 GCD，并找到要放在该前缀之后的连续元素的值。按照以下步骤解决上述问题:

1.  数组的[最大元素被设置为第一个元素，因此第一个前缀在数组 **arr[]中正确排列。**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
2.  现在找到前缀最后一个元素的连续元素，即 **arr[1]** 。
3.  这里最长前缀的GCD(说 **G** )等于**arr【0】**，这样[遍历剩余数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到与 **G** 给出最大 GCD 的元素。
4.  现在，将元素 **arr[1]** 与给出最大 GCD 的元素交换值 **G** ，将 **G** 的值更新为获得的最大 GCD，即 **G = GCD(G，arr[1])** 。
5.  现在最长的固定前缀变成了 **arr[0]** 、 **arr[1]** ，继续这个寻找 **arr[2]** 、 **arr[3]** 、…、**arr[N–1]**的过程，获得需要的数组。
6.  经过以上步骤，打印重排数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// obtainable from prefix GCDs
void prefixGCD(int arr[], int N)
{
    // Stores the GCD of the
    // longest prefix
    int gcc;

    // Sort the array
    sort(arr, arr + N);

    // Reverse the array
    reverse(arr, arr + N);

    // GCD of a[0] is a[0]
    gcc = arr[0];
    int start = 0;

    // Iterate to place the arr[start + 1]
    // element at it's correct position
    while (start < N - 1) {

        int g = 0, s1;

        for (int i = start + 1; i < N; i++) {

            // Find the element with
            // maximum GCD
            int gc = __gcd(gcc, arr[i]);

            // Update the value of g
            if (gc > g) {
                g = gc;
                s1 = i;
            }
        }

        // Update GCD of prefix
        gcc = g;

        // Place arr[s1] to it's
        // correct position
        swap(arr[s1], arr[start + 1]);

        // Increment start for the
        // remaining elements
        start++;
    }

    // Print the rearranged array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    prefixGCD(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program for
// the above approach
import java.util.*;
class GFG{

//Function to find the maximum number
//obtainable from prefix GCDs
static void prefixGCD(int arr[], int N)
{
  // Stores the GCD of the
  // longest prefix
  int gcc;

  // Sort the array
  Arrays.sort(arr);

  // Reverse the array
  arr = reverse(arr);

  // GCD of a[0] is a[0]
  gcc = arr[0];
  int start = 0;

  // Iterate to place
  // the arr[start + 1]
  // element at it's
  // correct position
  while (start < N - 1)
  {
    int g = 0, s1 = 0;

    for (int i = start + 1; i < N; i++)
    {
      // Find the element with
      // maximum GCD
      int gc = __gcd(gcc, arr[i]);

      // Update the value of g
      if (gc > g)
      {
        g = gc;
        s1 = i;
      }
    }

    // Update GCD of prefix
    gcc = g;

    // Place arr[s1] to it's
    // correct position
    arr = swap(arr, s1, start + 1);

    // Increment start for the
    // remaining elements
    start++;
  }

  // Print the rearranged array
  for (int i = 0; i < N; i++)
  {
    System.out.print(arr[i] + " ");
  }
}

static int __gcd(int a, int b) 
{ 
  return b == 0 ? a : __gcd(b, a % b);    
}

static int[] reverse(int a[])
{
  int i, n = a.length, t;
  for (i = 0; i < n / 2; i++)
  {
    t = a[i];
    a[i] = a[n - i - 1];
    a[n - i - 1] = t;
  }
  return a;
}

static int[] swap(int []arr,
                  int i, int j)
{
  int temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
  return arr;
}

//Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 2, 3, 4};

  int N = arr.length;

  // Function Call
  prefixGCD(arr, N);
}
}

//This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import gcd

# Function to find the maximum number
# obtainable from prefix GCDs
def prefixGCD(arr, N):

    # Stores the GCD of the
    # longest prefix
    gcc = 0

    # Sort the array
    arr = sorted(arr)

    # Reverse the array
    arr = arr[::-1]

    # GCD of a[0] is a[0]
    gcc = arr[0]
    start = 0

    # Iterate to place the arr[start + 1]
    # element at it's correct position
    while (start < N - 1):
        g = 0
        s1 = 0

        for i in range(start + 1, N):

            # Find the element with
            # maximum GCD
            gc = gcd(gcc, arr[i])

            # Update the value of g
            if (gc > g):
                g = gc
                s1 = i

        # Update GCD of prefix
        gcc = g

        # Place arr[s1] to it's
        # correct position
        arr[s1], arr[start + 1] = arr[start + 1], arr[s1]

        # Increment start for the
        # remaining elements
        start += 1

    # Print the rearranged array
    for i in range(N):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3, 4 ]

    N = len(arr)

    # Function Call
    prefixGCD(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach 
using System;
class GFG{

// Function to find the maximum number
// obtainable from prefix GCDs
static void prefixGCD(int[] arr, int N)
{

  // Stores the GCD of the
  // longest prefix
  int gcc;

  // Sort the array
  Array.Sort(arr);

  // Reverse the array
  arr = reverse(arr);

  // GCD of a[0] is a[0]
  gcc = arr[0];
  int start = 0;

  // Iterate to place the
  // arr[start + 1] element
  // at it's correct position
  while (start < N - 1)
  {
    int g = 0, s1 = 0;

    for(int i = start + 1; i < N; i++)
    {

      // Find the element with
      // maximum GCD
      int gc = __gcd(gcc, arr[i]);

      // Update the value of g
      if (gc > g)
      {
        g = gc;
        s1 = i;
      }
    }

    // Update GCD of prefix
    gcc = g;

    // Place arr[s1] to it's
    // correct position
    arr = swap(arr, s1, start + 1);

    // Increment start for the
    // remaining elements
    start++;
  }

  // Print the rearranged array
  for(int i = 0; i < N; i++)
  {
    Console.Write(arr[i] + " ");
  }
}

static int __gcd(int a, int b) 
{ 
  return b == 0 ? a : __gcd(b, a % b);    
}

static int[] reverse(int[] a)
{
  int i, n = a.Length, t;

  for(i = 0; i < n / 2; i++)
  {
    t = a[i];
    a[i] = a[n - i - 1];
    a[n - i - 1] = t;
  }
  return a;
}

static int[] swap(int []arr, int i,
                             int j)
{
  int temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
  return arr;
}

//Driver Code
public static void Main()
{

  // Given array arr[]
  int[] arr = { 1, 2, 3, 4 };

  int N = arr.Length;

  // Function call
  prefixGCD(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

//Function to find the maximum number
//obtainable from prefix GCDs
function prefixGCD(arr, N)
{
  // Stores the GCD of the
  // longest prefix
  let gcc;

  // Sort the array
  arr.sort();

  // Reverse the array
  arr = reverse(arr);

  // GCD of a[0] is a[0]
  gcc = arr[0];
  let start = 0;

  // Iterate to place
  // the arr[start + 1]
  // element at it's
  // correct position
  while (start < N - 1)
  {
    let g = 0, s1 = 0;

    for (let i = start + 1; i < N; i++)
    {
      // Find the element with
      // maximum GCD
      let gc = __gcd(gcc, arr[i]);

      // Update the value of g
      if (gc > g)
      {
        g = gc;
        s1 = i;
      }
    }

    // Update GCD of prefix
    gcc = g;

    // Place arr[s1] to it's
    // correct position
    arr = swap(arr, s1, start + 1);

    // Increment start for the
    // remaining elements
    start++;
  }

  // Prlet the rearranged array
  for (let i = 0; i < N; i++)
  {
    document.write(arr[i] + " ");
  }
}

function __gcd(a, b) 
{ 
  return b == 0 ? a : __gcd(b, a % b);    
}

function reverse(a)
{
  let i, n = a.length, t;
  for (i = 0; i < n / 2; i++)
  {
    t = a[i];
    a[i] = a[n - i - 1];
    a[n - i - 1] = t;
  }
  return a;
}

function swap(arr, i, j)
{
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
  return arr;
}

// Driver Code

    // Given array arr[]
  let arr = [1, 2, 3, 4];

  let N = arr.length;

  // Function Call
  prefixGCD(arr, N);

</script>
```

**Output:** 

```
4 2 3 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*