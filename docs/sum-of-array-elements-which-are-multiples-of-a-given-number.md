# 给定数量倍数的数组元素之和

> 原文:[https://www . geesforgeks . org/给定数字的倍数数组元素之和/](https://www.geeksforgeeks.org/sum-of-array-elements-which-are-multiples-of-a-given-number/)

给定一个由正整数和整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出所有数组元素的[和，这些元素是 **N** 的倍数](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例**:

> **输入:** arr[] = {1，2，3，5，6}，N = 3
> **输出:** 9
> **解释:**从给定数组来看，3 和 6 是 3 的倍数。因此，sum = 3 + 6 = 9。
> 
> **输入:** arr[] = {1，2，3，5，7，11，13}，N = 5
> **输出:** 5

**逼近**:思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，检查是否是 **N** 的倍数，并将这些元素相加。按照以下步骤解决问题:

1.  初始化一个变量，比如**和**，来存储需要的和。
2.  [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，执行以下操作。
3.  检查数组元素是否为 **N** 的倍数。
4.  如果元素是 **N** 的倍数，则将元素添加到**和**中。
5.  最后，打印**和**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of array
// elements which are multiples of N
void mulsum(int arr[], int n, int N)
{

    // Stores the sum
    int sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If current element
        // is a multiple of N
        if (arr[i] % N == 0) {
            sum = sum + arr[i];
        }
    }

    // Print total sum
    cout << sum;
}

// Driver Code
int main()
{

    // Given arr[]
    int arr[] = { 1, 2, 3, 5, 6 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int N = 3;

    mulsum(arr, n, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG{

// Function to find the sum of array
// elements which are multiples of N
static void mulsum(int arr[], int n, int N)
{

    // Stores the sum
    int sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++)
    {

        // If current element
        // is a multiple of N
        if (arr[i] % N == 0)
        {
            sum = sum + arr[i];
        }
    }

    // Print total sum
    System.out.println(sum);
}

// Driver Code
public static void main(String[] args)
{

    // Given arr[]
    int arr[] = { 1, 2, 3, 5, 6 };
    int n = arr.length;
    int N = 3;
    mulsum(arr, n, N);
}
}

// This code is contributed by jana_sayantan.
```

## 计算机编程语言

```
# Python3 program for the above approach

# Function to find the sum of array
# elements which are multiples of N
def mulsum(arr, n, N):

    # Stores the sum
    sums = 0

    # Traverse the array
    for i in range(0, n):
        if arr[i] % N == 0:
              sums = sums + arr[i]

    # Print total sum
    print(sums)

# Driver Code
if __name__ == "__main__":

    # Given arr[]
    arr = [ 1, 2, 3, 5, 6 ]

    n = len(arr)

    N = 3

    # Function call
    mulsum(arr, n, N)
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to find the sum of array
// elements which are multiples of N
static void mulsum(int[] arr, int n, int N)
{

    // Stores the sum
    int sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++)
    {

        // If current element
        // is a multiple of N
        if (arr[i] % N == 0)
        {
            sum = sum + arr[i];
        }
    }

    // Print total sum
    Console.Write(sum);
}

// Driver Code
static public void Main ()
{
    // Given arr[]
    int[] arr = { 1, 2, 3, 5, 6 };
    int n = arr.Length;
    int N = 3;
    mulsum(arr, n, N);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the sum of array
// elements which are multiples of N
function mulsum(arr, n, N)
{

    // Stores the sum
    var sum = 0;

    // Traverse the given array
    for(var i = 0; i < n; i++)
    {

        // If current element
        // is a multiple of N
        if (arr[i] % N == 0)
        {
            sum = sum + arr[i];
        }
    }

    // Print total sum
    document.write(sum);
}

// Driver Code

// Given arr[]
var arr = [ 1, 2, 3, 5, 6 ];
var n = arr.length;
var N = 3;

mulsum(arr, n, N);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)