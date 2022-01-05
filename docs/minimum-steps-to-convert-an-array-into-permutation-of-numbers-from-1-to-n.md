# 将数组转换为从 1 到 N 的数字排列的最小步骤

> 原文:[https://www . geesforgeks . org/将数组转换为从 1 到 n 的数字排列的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-convert-an-array-into-permutation-of-numbers-from-1-to-n/)

给定一个长度为 **N** 的数组 **arr** ，任务是计算将给定序列转换为第一个 **N** 自然数 **(1，2，…)的排列的最小操作数。，N)** 。在每个操作中，将一个元素递增或递减一。
**举例:**

> **输入:** arr[] = {4，1，3，6，5}
> **输出:** 4
> 在 6
> **上应用四次减量操作输入:** arr[] = {0，2，3，4，1，6，8，9}
> **输出:** 7

**方法**:一种有效的方法是[对给定的数组进行排序](https://www.geeksforgeeks.org/sort-c-stl/)，对于每个元素，找出**arr【I】**和 **i** 之间的差异(基于 1 的索引)。找出所有这些差异的总和，这将是所需的最少步骤。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find minimum number of steps to
// convert a given sequence into a permutation

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of steps to
// convert a given sequence into a permutation
int get_permutation(int arr[], int n)
{
    // Sort the given array
    sort(arr, arr + n);

    // To store the required minimum
    // number of operations
    int result = 0;

    // Find the operations on each step
    for (int i = 0; i < n; i++) {
        result += abs(arr[i] - (i + 1));
    }

    // Return the answer
    return result;
}

// Driver code
int main()
{
    int arr[] = { 0, 2, 3, 4, 1, 6, 8, 9 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << get_permutation(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of steps to
// convert a given sequence into a permutation
import java.util.*;

class GFG{

// Function to find minimum number of steps to
// convert a given sequence into a permutation
static int get_permutation(int arr[], int n)
{
    // Sort the given array
    Arrays.sort(arr);

    // To store the required minimum
    // number of operations
    int result = 0;

    // Find the operations on each step
    for (int i = 0; i < n; i++) {
        result += Math.abs(arr[i] - (i + 1));
    }

    // Return the answer
    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 0, 2, 3, 4, 1, 6, 8, 9 };

    int n = arr.length;

    // Function call
    System.out.print(get_permutation(arr, n));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find minimum number of steps to
# convert a given sequence into a permutation

# Function to find minimum number of steps to
# convert a given sequence into a permutation
def get_permutation(arr, n):

    # Sort the given array
    arr = sorted(arr)

    # To store the required minimum
    # number of operations
    result = 0

    # Find the operations on each step
    for i in range(n):
        result += abs(arr[i] - (i + 1))

    # Return the answer
    return result

# Driver code
if __name__ == '__main__':
    arr=[0, 2, 3, 4, 1, 6, 8, 9]
    n = len(arr)

    # Function call
    print(get_permutation(arr, n))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to find minimum number of steps to
// convert a given sequence into a permutation
using System;

class GFG{

// Function to find minimum number of steps to
// convert a given sequence into a permutation
static int get_permutation(int []arr, int n)
{
    // Sort the given array
    Array.Sort(arr);

    // To store the required minimum
    // number of operations
    int result = 0;

    // Find the operations on each step
    for (int i = 0; i < n; i++) {
        result += Math.Abs(arr[i] - (i + 1));
    }

    // Return the answer
    return result;
}

// Driver Code
public static void Main()
{
    int []arr = { 0, 2, 3, 4, 1, 6, 8, 9 };

    int n = arr.Length;

    // Function call
    Console.Write(get_permutation(arr, n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// javascript program to find minimum number of steps to
// convert a given sequence into a permutation

// Function to find minimum number of steps to
// convert a given sequence into a permutation
function get_permutation(arr , n)
{

    // Sort the given array
    arr.sort();

    // To store the required minimum
    // number of operations
    var result = 0;

    // Find the operations on each step
    for (i = 0; i < n; i++) {
        result += Math.abs(arr[i] - (i + 1));
    }

    // Return the answer
    return result;
}

// Driver code
var arr = [ 0, 2, 3, 4, 1, 6, 8, 9 ];
var n = arr.length;

// Function call
document.write(get_permutation(arr, n));

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
7
```