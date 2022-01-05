# 根据给定条件通过向左或向右旋转来减少给定的[1，N]数组

> 原文:[https://www . geesforgeks . org/通过基于给定条件向左或向右旋转来减少给定的 1-n 数组/](https://www.geeksforgeeks.org/reduce-the-given-array-of-1-n-by-rotating-left-or-right-based-on-given-conditions/)

给定第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的一个[排序的](https://www.geeksforgeeks.org/sorting-algorithms/) [数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **X** ，任务是在执行以下操作**(N–1)**次后打印最后一个剩余元素:

*   如果 **X** 的值为 **1** ，则[将数组](https://www.geeksforgeeks.org/how-to-left-or-right-rotate-an-array-in-java/)向右旋转 **1** 单位，删除最后一个元素。
*   如果 **X** 的值为 **2** ，则[将数组](https://www.geeksforgeeks.org/how-to-left-or-right-rotate-an-array-in-java/)向左旋转 **1** 单位，删除第一个元素。

**示例:**

> **输入:** N = 5，arr[] = {1，2，3，4，5}，X = 1
> **输出:** 3
> **解释:**
> 操作如下:
> 
> 1.  将数组向右旋转 1 个单位会将数组修改为{5，1，2，3，4}。删除数组元素会将数组修改为{5，1，2，3}。
> 2.  将数组向右旋转 1 个单位会将数组修改为{3，5，1，2}。删除数组元素会将数组修改为{3，5，1}。
> 3.  将数组向右旋转 1 个单位会将数组修改为{1，3，5}。删除数组元素会将数组修改为{1，3}。
> 4.  将数组向右旋转 1 个单位会将数组修改为{3，1}。删除数组元素会将数组修改为{3}。
> 
> 因此，最后剩下的元素是 3。
> 
> **输入:** N = 5，arr[] = {1，2，3，4，5}，X = 2
> **输出:** 3

**天真法:**解决给定问题最简单的方法是将范围**【1，N】**的所有数字推入一个[德格](https://www.geeksforgeeks.org/deque-cpp-stl/)中，根据 **X** 的给定值执行给定操作**(N–1)**次，然后打印最后剩余的元素。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**给定的问题可以基于以下观察进行优化:

1.  如果 **X** 的值是 **1** ，那么最后剩下的元素就是 **2** 的[最小次方大于 **N**](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/) 和 **N** 的差。
2.  如果 **X** 的值是 **2** ，那么最后剩下的元素将是**2 *(N–D)+1，**其中 **D** 代表 **2** 小于或等于 **N** 的[最大幂。](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)

按照以下步骤解决问题:

*   [将大于 **N**](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/) 的 2 次方存储在一个变量中，比如**次方。**
*   如果 **X** 的值为 **1** ，则打印值**(next power–N)**作为结果。
*   否则，打印数值**2 *(N–next power/2)+1**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the last element
// left after performing N - 1 queries
// of type X
int rotate(int arr[], int N, int X)
{
    // Stores the next power of 2
    long long int nextPower = 1;

    // Iterate until nextPower is at most N
    while (nextPower <= N)
        nextPower *= 2;

    // If X is equal to 1
    if (X == 1)
        return nextPower - N;

    // Stores the power of 2 less than or
    // equal to N
    long long int prevPower = nextPower / 2;

    // Return the final value
    return 2 * (N - prevPower) + 1;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int X = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << rotate(arr, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to find the last element
// left after performing N - 1 queries
// of type X
static int rotate(int arr[], int N, int X)
{

    // Stores the next power of 2
    long nextPower = 1;

    // Iterate until nextPower is at most N
    while (nextPower <= N)
        nextPower *= 2;

    // If X is equal to 1
    if (X == 1)
        return (int) nextPower - N;

    // Stores the power of 2 less than or
    // equal to N
    long prevPower = nextPower / 2;

    // Return the final value
    return 2 * (N - (int)prevPower) + 1;
}

// Driver Code
    public static void main (String[] args) {
        int arr[] = { 1, 2, 3, 4, 5 };
    int X = 1;
    int N =arr.length;

   System.out.println(rotate(arr, N, X));

    }
}

    // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the last element
# left after performing N - 1 queries
# of type X
def rotate(arr, N, X):
    # Stores the next power of 2
    nextPower = 1

    # Iterate until nextPower is at most N
    while (nextPower <= N):
        nextPower *= 2

    # If X is equal to 1
    if (X == 1):
        ans = nextPower - N
        return ans

    # Stores the power of 2 less than or
    # equal to N
    prevPower = nextPower // 2

    # Return the final value
    return 2 * (N - prevPower) + 1

# Driver Code
arr = [1, 2, 3, 4, 5]
X = 1
N = len(arr)
print(rotate(arr, N, X))

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the last element
// left after performing N - 1 queries
// of type X
static int rotate(int []arr, int N, int X)
{

    // Stores the next power of 2
    int nextPower = 1;

    // Iterate until nextPower is at most N
    while (nextPower <= N)
        nextPower *= 2;

    // If X is equal to 1
    if (X == 1)
        return nextPower - N;

    // Stores the power of 2 less than or
    // equal to N
    int prevPower = nextPower / 2;

    // Return the final value
    return 2 * (N - prevPower) + 1;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 2, 3, 4, 5 };
    int X = 1;
    int N = arr.Length;

    Console.Write(rotate(arr, N, X));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to find the last element
       // left after performing N - 1 queries
       // of type X
       function rotate(arr, N, X) {
           // Stores the next power of 2
           let nextPower = 1;

           // Iterate until nextPower is at most N
           while (nextPower <= N)
               nextPower *= 2;

           // If X is equal to 1
           if (X == 1)
               return nextPower - N;

           // Stores the power of 2 less than or
           // equal to N
           let prevPower = nextPower / 2;

           // Return the final value
           return 2 * (N - prevPower) + 1;
       }

       // Driver Code
       let arr = [1, 2, 3, 4, 5];
       let X = 1;
       let N = arr.length;

       document.write(rotate(arr, N, X));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
3
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*