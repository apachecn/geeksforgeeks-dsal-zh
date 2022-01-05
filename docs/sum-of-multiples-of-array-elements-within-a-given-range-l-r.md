# 给定范围内数组元素的倍数之和[L，R]

> 原文:[https://www . geesforgeks . org/给定范围内数组元素的倍数之和-l-r/](https://www.geeksforgeeks.org/sum-of-multiples-of-array-elements-within-a-given-range-l-r/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和两个整数 **L** 和 **R** ，任务是找出范围**【L，R】**内所有数组元素的倍数之和。

**示例:**

> **输入:** arr[] = {2，7，3，8}，L = 7， R = 20
> **输出:** 197
> **说明:**
> 在 7 到 20 范围内:
> 2:8+10+12+14+16+18+20 的倍数之和= 98
> 7:7+14 的倍数之和= 21
> 3:9+12+15+18 的倍数之和= 54
> 8:8+16 的倍数之和= 21
> 
> **输入:** arr[] = {5，6，7，8，9}，L = 39，R = 100
> **输出:** 3278

**天真方法:**天真的想法是对于给定数组中的每个元素**arr【】**找到该元素在范围**【L，R】**内的倍数，并打印所有倍数的总和。

***时间复杂度:** O(N*(L-R))*
***辅助空间:** O(1)*

**高效方法:**为了优化上述简单方法，我们将使用下面讨论的概念:

1.  对于任意整数 **X** ，从 **X** 到任意整数 **Y** 的倍数由 **Y/X** 给出。
2.  设 **N = Y/X**
    那么，以上所有倍数之和由 **X*N*(N-1)/2** 给出。

**例如:**

> 对于 X = 2 和 Y = 12
> 倍数之和为:
> =>2+4+6+8+10+12
> =>2 *(1+2+3+4+5+6)
> =>2 *(6 * 5)/2
> =>20。

使用上述概念，可以通过以下步骤解决问题:

1.  使用上述公式计算**arr【I】**到 **R** 的所有倍数之和。
2.  使用上述公式计算 **arr[i]** 到**L–1**的所有倍数之和。
3.  将上述步骤中的上述两个值相减，得到范围**【L，R】**之间的所有倍数之和。
4.  对所有元素重复上述过程，并打印总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all
// multiples of N up to K
int calcSum(int k, int n)
{
    // Calculate the sum
    int value = (k * n * (n
                          + 1))
                / 2;
    // Return the sum
    return value;
}

// Function to find the total sum
int findSum(int* a, int n, int L, int R)
{
    int sum = 0;
    for (int i = 0; i < n; i++) {

        // Calculating sum of multiples
        // for each element

        // If L is divisible by a[i]
        if (L % a[i] == 0 && L != 0) {
            sum += calcSum(a[i], R / a[i])
                   - calcSum(a[i],
                             (L - 1) / a[i]);
        }

        // Otherwise
        else {
            sum += calcSum(a[i], R / a[i])
                   - calcSum(a[i], L / a[i]);
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 7, 3, 8 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Given range
    int L = 7;
    int R = 20;

    // Function Call
    cout << findSum(arr, N, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the sum of
// all multiples of N up to K
static int calcSum(int k, int n)
{

    // Calculate the sum
    int value = (k * n * (n + 1)) / 2;

    // Return the sum
    return value;
}

// Function to find the total sum
static int findSum(int[] a, int n,
                   int L, int R)
{
    int sum = 0;
    for(int i = 0; i < n; i++)
    {

       // Calculating sum of multiples
       // for each element

       // If L is divisible by a[i]
       if (L % a[i] == 0 && L != 0)
       {
           sum += calcSum(a[i], R / a[i]) -
                  calcSum(a[i], (L - 1) / a[i]);
       }

       // Otherwise
       else
       {
           sum += calcSum(a[i], R / a[i]) -
                  calcSum(a[i], L / a[i]);
       }
    }

    // Return the final sum
    return sum;
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 7, 3, 8 };

    int N = arr.length;

    // Given range
    int L = 7;
    int R = 20;

    // Function Call
    System.out.println(findSum(arr, N, L, R));
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of
# all multiples of N up to K
def calcSum(k, n):

    # Calculate the sum
    value = (k * n * (n + 1)) // 2

    # Return the sum
    return value

# Function to find the total sum
def findSum(a, n, L, R):

    sum = 0
    for i in range(n):

        # Calculating sum of multiples
        # for each element

        # If L is divisible by a[i]
        if (L % a[i] == 0 and L != 0):
            sum += (calcSum(a[i], R // a[i]) -
                    calcSum(a[i], (L - 1) // a[i]))

        # Otherwise
        else:
            sum += (calcSum(a[i], R // a[i]) -
                    calcSum(a[i], L // a[i]))

    # Return the final sum
    return sum;

# Driver code
if __name__=="__main__":

    # Given array arr[]
    arr = [ 2, 7, 3, 8 ]

    N = len(arr)

    # Given range
    L = 7
    R = 20

    # Function call
    print(findSum(arr, N, L, R))    

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the sum of
// all multiples of N up to K
static int calcSum(int k, int n)
{

    // Calculate the sum
    int value = (k * n * (n + 1)) / 2;

    // Return the sum
    return value;
}

// Function to find the total sum
static int findSum(int[] a, int n,
                   int L, int R)
{
    int sum = 0;
    for(int i = 0; i < n; i++)
    {

       // Calculating sum of multiples
       // for each element

       // If L is divisible by a[i]
       if (L % a[i] == 0 && L != 0)
       {
           sum += calcSum(a[i], R / a[i]) -
                  calcSum(a[i], (L - 1) / a[i]);
       }

       // Otherwise
       else
       {
           sum += calcSum(a[i], R / a[i]) -
                  calcSum(a[i], L / a[i]);
       }
    }

    // Return the final sum
    return sum;
}

// Driver Code
public static void Main (string[] args)
{

    // Given array arr[]
    int []arr = new int[]{ 2, 7, 3, 8 };

    int N = arr.Length;

    // Given range
    int L = 7;
    int R = 20;

    // Function Call
    Console.Write(findSum(arr, N, L, R));
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to find the sum of
// all multiples of N up to K
function calcSum(k, n)
{

    // Calculate the sum
    let value = (k * n * (n + 1)) / 2;

    // Return the sum
    return value;
}

// Function to find the total sum
function findSum(a, n, L, R)
{
    let sum = 0;
    for(let i = 0; i < n; i++)
    {

       // Calculating sum of multiples
       // for each element

       // If L is divisible by a[i]
       if (L % a[i] == 0 && L != 0)
       {
           sum += calcSum(a[i], Math.floor(R / a[i])) -
                  calcSum(a[i], Math.floor((L - 1) / a[i]));
       }

       // Otherwise
       else
       {
           sum += calcSum(a[i], Math.floor(R / a[i])) -
                  calcSum(a[i], Math.floor(L / a[i]));
       }
    }

    // Return the final sum
    return sum;
}

    // Driver Code

    // Given array arr[]
    let arr = [ 2, 7, 3, 8 ];

    let N = arr.length;

    // Given range
    let L = 7;
    let R = 20;

    // Function Call
   document.write(findSum(arr, N, L, R));

</script>
```

**Output:** 

```
197
```

***时间复杂度:** O(N)，其中 N 是给定数组中元素的个数。*
***辅助空间:** O(1)*