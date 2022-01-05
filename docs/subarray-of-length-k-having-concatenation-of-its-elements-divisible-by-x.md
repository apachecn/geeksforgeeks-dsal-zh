# 长度为 K 的子阵列，其元素的连接可被 X 整除

> 原文:[https://www . geeksforgeeks . org/长度为 k 的子数组，其元素可被 x 整除/](https://www.geeksforgeeks.org/subarray-of-length-k-having-concatenation-of-its-elements-divisible-by-x/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到一个长度为 **K** 的[子数组](https://www.geeksforgeeks.org/tag/subarray/)，这样子数组的每个元素的连接可以被 **X** 整除。如果不存在这样的子阵列，则打印**-1”**。如果存在多个这样的子阵列，打印其中任何一个。

**示例:**

> **输入:** arr[] = {1，2，4，5，9，6，4，3，7，8}，K = 4，X = 4
> **输出:** 4 5 9 6
> **解释:**
> 子阵列{4，5，9，6}的元素串联形成 4 5 9 6，可被 4 整除。
> 
> **输入:** arr[] = {2，3，5，1，3}，K = 3，X = 6
> **输出:** -1

**天真方法:**解决问题最简单的方法是[生成所有可能的长度为 **K** 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并打印该子阵列，其元素的连接可被 **X** 整除。如果没有这样的子阵列，打印【T8 "-" 1 "。否则，打印这些子阵列中的任何一个。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化。按照以下步骤解决问题:

1.  通过连接第一个 **K** 数组元素生成一个数字。将其存储在变量中，例如 **num** 。
2.  检查生成的数字是否能被 **X** 整除。如果发现为真，则打印当前子阵列。
3.  否则，[在范围**【K，N】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，请遵循以下步骤:
    *   将元素**arr【I】**的数字添加到变量 **num** 中。
    *   从**号**的前面去掉元素**的数字。**
    *   现在检查当前形成的数是否能被 **X** 整除。如果发现为真，则打印当前子阵列范围内的**【I–K，I】**。
    *   否则，检查下一个子阵列。
4.  如果不存在这样的子阵列，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the starting
// index of the subarray whose
// concatenation is divisible by X
int findSubarray(vector<int> arr,
                 int K, int X)
{
    int i, num = 0;

    // Generate the concatenation
    // of first K length subarray
    for (i = 0; i < K; i++) {
        num = num * 10 + arr[i];
    }

    // If num is divisible by X
    if (num % X == 0) {
        return 0;
    }

    // Traverse the remaining array
    for (int j = i; j < arr.size(); j++) {

        // Append the digits of arr[i]
        num = (num % (int)pow(10, j - 1))
                  * 10
              + arr[j];

        // If num is divisible by X
        if (num % X == 0) {
            return j - i + 1;
        }
    }

    // No subarray exists
    return -1;
}

// Function to print the subarray in
// the range [answer, answer + K]
void print(vector<int> arr, int answer,
           int K)
{
    // No such subarray exists
    if (answer == -1) {
        cout << answer;
    }

    // Otherwise
    else {

        // Print the subarray in the
        // range [answer, answer + K]
        for (int i = answer;
             i < answer + K; i++) {
            cout << arr[i] << " ";
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 1, 2, 4, 5, 9,
                        6, 4, 3, 7, 8 };

    int K = 4, X = 4;

    // Function Call
    int answer = findSubarray(arr, K, X);

    // Function Call to print subarray
    print(arr, answer, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to return the starting
// index of the subarray whose
// concatenation is divisible by X
static int findSubarray(ArrayList<Integer> arr, int K,
                                                int X)
{
    int i, num = 0;

    // Generate the concatenation
    // of first K length subarray
    for(i = 0; i < K; i++)
    {
        num = num * 10 + arr.get(i);
    }

    // If num is divisible by X
    if (num % X == 0)
    {
        return 0;
    }

    // Traverse the remaining array
    for(int j = i; j < arr.size(); j++)
    {

        // Append the digits of arr[i]
        num = (num % (int)Math.pow(10, j - 1)) *
                10 + arr.get(j);

        // If num is divisible by X
        if (num % X == 0)
        {
            return j - i + 1;
        }
    }

    // No subarray exists
    return -1;
}

// Function to print the subarray in
// the range [answer, answer + K]
static void print(ArrayList<Integer> arr, int answer,
                                          int K)
{

    // No such subarray exists
    if (answer == -1)
    {
        System.out.println(answer);
    }

    // Otherwise
    else
    {

        // Print the subarray in the
        // range [answer, answer + K]
        for(int i = answer; i < answer + K; i++)
        {
            System.out.print(arr.get(i) + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    ArrayList<Integer> arr = new ArrayList<Integer>(
        Arrays.asList(1, 2, 4, 5, 9, 6, 4, 3, 7, 8));

    int K = 4, X = 4;

    // Function call
    int answer = findSubarray(arr, K, X);

    // Function call to print subarray
    print(arr, answer, K);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the starting
# index of the subarray whose
# concatenation is divisible by X
def findSubarray(arr, K, X):

    num = 0

    # Generate the concatenation
    # of first K length subarray
    for i in range(0, K):
        num = num * 10 + arr[i]

    # If num is divisible by X
    if num % X == 0:
        return 0

    i = K

    # Traverse the remaining array
    for j in range(i, len(arr)):

        # Append the digits of arr[i]
        num = ((num % int(pow(10, j - 1))) *
                10 + arr[j])

        # If num is divisible by X
        if num % X == 0:
            return j - i + 1

    # No subarray exists
    return -1

# Function to print the subarray in
# the range [answer, answer + K]
def print_subarray(arr, answer, K):

    # No such subarray exists
    if answer == -1:
        print(answer)

    # Otherwise
    else:

        # Print the subarray in the
        # range [answer, answer + K]
        for i in range(answer, answer + K):
            print(arr[i], end = " ")

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [ 1, 2, 4, 5, 9,
            6, 4, 3, 7, 8 ]

    K = 4
    X = 4

    # Function call
    answer = findSubarray(arr, K, X)

    # Function call to print subarray
    print_subarray(arr, answer, K)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the starting
// index of the subarray whose
// concatenation is divisible by X
static int findSubarray(List<int> arr, int K,
                                       int X)
{
    int i, num = 0;

    // Generate the concatenation
    // of first K length subarray
    for(i = 0; i < K; i++)
    {
        num = num * 10 + arr[i];
    }

    // If num is divisible by X
    if (num % X == 0)
    {
        return 0;
    }

    // Traverse the remaining array
    for(int j = i; j < arr.Count; j++)
    {

        // Append the digits of arr[i]
        num = (num % (int)Math.Pow(10, j - 1)) *
                10 + arr[j];

        // If num is divisible by X
        if (num % X == 0)
        {
            return j - i + 1;
        }
    }

    // No subarray exists
    return -1;
}

// Function to print the subarray in
// the range [answer, answer + K]
static void print(List<int> arr, int answer,
                                 int K)
{

    // No such subarray exists
    if (answer == -1)
    {
        Console.WriteLine(answer);
    }

    // Otherwise
    else
    {

        // Print the subarray in the
        // range [answer, answer + K]
        for(int i = answer; i < answer + K; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// Driver Code
static public void Main()
{

    // Given array arr[]
    List<int> arr = new List<int>(){ 1, 2, 4, 5, 9,
                                     6, 4, 3, 7, 8 };

    int K = 4, X = 4;

    // Function call
    int answer = findSubarray(arr, K, X);

    // Function call to print subarray
    print(arr, answer, K);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the starting
// index of the subarray whose
// concatenation is divisible by X
function findSubarray(arr, K, X)
{
    var i, num = 0;

    // Generate the concatenation
    // of first K length subarray
    for(i = 0; i < K; i++)
    {
        num = num * 10 + arr[i];
    }

    // If num is divisible by X
    if (num % X == 0)
    {
        return 0;
    }

    // Traverse the remaining array
    for(var j = i; j < arr.length; j++)
    {

        // Append the digits of arr[i]
        num = (num % parseInt(Math.pow(10, j - 1))) *
                10 + arr[j];

        // If num is divisible by X
        if (num % X == 0)
        {
            return j - i + 1;
        }
    }

    // No subarray exists
    return -1;
}

// Function to print the subarray in
// the range [answer, answer + K]
function print(arr, answer, K)
{

    // No such subarray exists
    if (answer == -1)
    {
        document.write(answer);
    }

    // Otherwise
    else
    {

        // Print the subarray in the
        // range [answer, answer + K]
        for(var i = answer;
                i < answer + K; i++)
        {
            document.write( arr[i] + " ");
        }
    }
}

// Driver Code

// Given array arr[]
var arr = [ 1, 2, 4, 5, 9,
            6, 4, 3, 7, 8 ];
var K = 4, X = 4;

// Function Call
var answer = findSubarray(arr, K, X);

// Function Call to print subarray
print(arr, answer, K);

// This code is contributed by itsok

</script>
```

**Output:** 

```
4 5 9 6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)