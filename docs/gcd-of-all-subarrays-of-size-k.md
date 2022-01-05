# 大小为 K 的所有子阵列的 GCD

> 原文:[https://www . geesforgeks . org/gcd-of-all-size-k 子阵列/](https://www.geeksforgeeks.org/gcd-of-all-subarrays-of-size-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr[]**，任务是打印所有大小为 **K** 的子数组的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

**示例:**

> **输入:** arr[] = {2，4，3，9，14，20，25，17}，K = 2
> **输出:** 2 1 3 1 2 5 1
> **解释:**T8】gcd(2，4}) = 2
> gcd(4，3) = 1
> gcd(3，9) = 3
> gcd(9，14) = 1
> gcd(14
> 
> **输入:** arr[] = {2，4，8，24，14，20，25，35，7，49，7}，K = 3
> **输出:【4 2 2 1 5 1 7 7**

**方式:**思路是[生成大小为 **K** 的所有子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，打印每个子阵的 [GCD。为了有效地计算每个子阵列的 GCD，想法是使用 GCD 的以下属性。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

> GCD(A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，…，A <sub>K</sub> ) = GCD(A <sub>1</sub> ，GCD(A <sub>2</sub> ，A <sub>3</sub> ，A <sub>4</sub> ，…。，A <sub>K</sub> )

按照以下步骤解决问题:

1.  初始化一个变量，比如 **gcd** ，来存储当前子阵列的 **GCD** 。
2.  从给定阵列生成 **K** 长度的子阵列。
3.  应用 GCD 的上述性质，计算每个子阵列的 GCD，并打印得到的结果。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the gcd
// of each subarray of length K
void printSub(int arr[], int N,
              int K)
{
    for (int i = 0; i <= N - K; i++) {

        // Store GCD of subarray
        int gcd = arr[i];

        for (int j = i + 1; j < i + K;
             j++) {

            // Update GCD of subarray
            gcd = __gcd(gcd, arr[j]);
        }

        // Print GCD of subarray
        cout << gcd << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 3, 9, 14,
                  20, 25, 17 };
    int K = 2;
    int N = sizeof(arr)
            / sizeof(arr[0]);

    printSub(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

static int __gcd(int a, int b)
{
  if (b == 0)
    return a;
  return __gcd(b, a % b);
}

// Function to print the gcd
// of each subarray of length K
static void printSub(int arr[],
                     int N, int K)
{
  for (int i = 0; i <= N - K; i++)
  {
    // Store GCD of subarray
    int gcd = arr[i];

    for (int j = i + 1; j < i + K; j++)
    {
      // Update GCD of subarray
      gcd = __gcd(gcd, arr[j]);
    }

    // Print GCD of subarray
    System.out.print(gcd + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {2, 4, 3, 9,
               14, 20, 25, 17};
  int K = 2;
  int N = arr.length;
  printSub(arr, N, K);
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import gcd

# Function to print the gcd
# of each subarray of length K
def printSub(arr, N, K):

    for i in range(N - K + 1):

        # Store GCD of subarray
        g = arr[i]

        for j in range(i + 1, i + K):

            # Update GCD of subarray
            g = gcd(g, arr[j])

        # Print GCD of subarray
        print(g, end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 4, 3, 9, 14,
            20, 25, 17 ]
    K = 2
    N = len(arr)

    printSub(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static int __gcd(int a, int b)
{
  if (b == 0)
    return a;
  return __gcd(b, a % b);
}

// Function to print the gcd
// of each subarray of length K
static void printSub(int []arr,
                     int N, int K)
{
  for (int i = 0; i <= N - K; i++)
  {
    // Store GCD of subarray
    int gcd = arr[i];

    for (int j = i + 1; j < i + K; j++)
    {
      // Update GCD of subarray
      gcd = __gcd(gcd, arr[j]);
    }

    // Print GCD of subarray
    Console.Write(gcd + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {2, 4, 3, 9,
               14, 20, 25, 17};
  int K = 2;
  int N = arr.Length;
  printSub(arr, N, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

function __gcd(a, b)
{
  if (b == 0)
    return a;
  return __gcd(b, a % b);
}

// Function to print the gcd
// of each subarray of length K
function prletSub(arr, N, K)
{
  for (let i = 0; i <= N - K; i++)
  {
    // Store GCD of subarray
    let gcd = arr[i];

    for (let j = i + 1; j < i + K; j++)
    {
      // Update GCD of subarray
      gcd = __gcd(gcd, arr[j]);
    }

    // Print GCD of subarray
    document.write(gcd + " ");
  }
}

// Driver Code

    let arr = [2, 4, 3, 9,
               14, 20, 25, 17];
  let K = 2;
  let N = arr.length;
  prletSub(arr, N, K);

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
2 1 3 1 2 5 1
```

***时间复杂度:**O((N–K+1)* K)*
***辅助空间:** O(1)*