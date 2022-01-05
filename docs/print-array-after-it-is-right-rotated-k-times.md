# 右旋转 K 次后打印数组

> 原文:[https://www . geesforgeks . org/print-array-it-right-rotated-k-times/](https://www.geeksforgeeks.org/print-array-after-it-is-right-rotated-k-times/)

给定一个大小为 N 的**数组**和一个值为 **K** ，我们需要围绕它右旋转数组。如何快速打印右旋转数组？
**例:**

```
Input: Array[] = {1, 3, 5, 7, 9}, K = 2.
Output: 7 9 1 3 5
Explanation:
After 1st rotation - {9, 1, 3, 5, 7}
After 2nd rotation - {7, 9, 1, 3, 5}

Input: Array[] = {1, 2, 3, 4, 5}, K = 4.
Output: 2 3 4 5 1      
```

**进场:**

1.  我们将首先取 K 乘以 N (K = K % N)的 mod，因为在每 N 次旋转之后，数组将变得与初始数组相同。

2.  现在，我们将数组从 i = 0 迭代到 i = N-1 并检查，
    *   如果 **i < K** ，打印最右边的第 Kth 个元素(a[N + i -K])。否则，

    *   在“K”元素后打印数组(a[I–K])。

下面是上述方法的实现。

## C++

```
// C++ implementation of right rotation
// of an array K number of times
#include<bits/stdc++.h>
using namespace std;

// Function to rightRotate array
void RightRotate(int a[], int n, int k)
{

    // If rotation is greater
    // than size of array
    k = k % n;

    for(int i = 0; i < n; i++)
    {
       if(i < k)
       {

           // Printing rightmost
           // kth elements
           cout << a[n + i - k] << " ";
       }
       else
       {

           // Prints array after
           // 'k' elements
           cout << (a[i - k]) << " ";
       }
    }
    cout << "\n";
}

// Driver code
int main()
{
    int Array[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(Array) / sizeof(Array[0]);
    int K = 2;

    RightRotate(Array, N, K);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of Right Rotation
// of an Array K number of times
import java.util.*;
import java.lang.*;
import java.io.*;

class Array_Rotation
{

// Function to rightRotate array
static void RightRotate(int a[],
                        int n, int k)
{

    // If rotation is greater
    // than size of array
    k=k%n;

    for(int i = 0; i < n; i++)
    {
        if(i<k)
        {
            // Printing rightmost
            // kth elements
            System.out.print(a[n + i - k]
                             + " ");
        }
        else
        {
            // Prints array after
            // 'k' elements
            System.out.print(a[i - k]
                             + " ");
        }
    }
    System.out.println();
}

// Driver program
public static void main(String args[])
{
    int Array[] = {1, 2, 3, 4, 5};
    int N = Array.length;

    int K = 2;
    RightRotate(Array, N, K);

}
}
// This code is contributed by M Vamshi Krishna
```

## 蟒蛇 3

```
# Python3 implementation of right rotation
# of an array K number of times

# Function to rightRotate array
def RightRotate(a, n, k):

    # If rotation is greater
    # than size of array
    k = k % n;

    for i in range(0, n):

        if(i < k):

            # Printing rightmost
            # kth elements
            print(a[n + i - k], end = " ");

        else:

            # Prints array after
            # 'k' elements
            print(a[i - k], end = " ");

    print("\n");

# Driver code
Array = [ 1, 2, 3, 4, 5 ];
N = len(Array);
K = 2;

RightRotate(Array, N, K);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation of right rotation
// of an array K number of times
using System;
class GFG{

// Function to rightRotate array
static void RightRotate(int []a,
                        int n, int k)
{

    // If rotation is greater
    // than size of array
    k = k % n;

    for(int i = 0; i < n; i++)
    {
       if(i < k)
       {

           // Printing rightmost
           // kth elements
           Console.Write(a[n + i - k] + " ");
       }
       else
       {

           // Prints array after
           // 'k' elements
           Console.Write(a[i - k] + " ");
       }
    }
    Console.WriteLine();
}

// Driver code
public static void Main(String []args)
{
    int []Array = { 1, 2, 3, 4, 5 };
    int N = Array.Length;
    int K = 2;

    RightRotate(Array, N, K);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
// Javascript implementation of right rotation
// of an array K number of times

// Function to rightRotate array
function RightRotate(a, n, k)
{

    // If rotation is greater
    // than size of array
    k = k % n;

    for (let i = 0; i < n; i++) {
        if (i < k) {

            // Printing rightmost
            // kth elements
            document.write(a[n + i - k] + " ");
        }
        else {

            // Prints array after
            // 'k' elements
            document.write((a[i - k]) + " ");
        }
    }
    document.write("<br>");
}

// Driver code
let Array = [1, 2, 3, 4, 5];
let N = Array.length;
let K = 2;

RightRotate(Array, N, K);

// This code is contributed by gfgking.
```

**Output:** 

```
4 5 1 2 3
```

**时间复杂度**:O(n)
T3】辅助空间 : O(1)

请参阅以下帖子了解阵列旋转的其他方法:

[https://www . geesforgeks . org/print-array-it-right-rotated-k-times-set-2/](https://www.geeksforgeeks.org/print-array-after-it-is-right-rotated-k-times-set-2/)