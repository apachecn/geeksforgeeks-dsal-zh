# 打印每次索引后给定数组反转形成的数组

> 原文:[https://www . geesforgeks . org/print-the-array-formed-通过在每个索引后反转给定的数组/](https://www.geeksforgeeks.org/print-the-array-formed-by-reversing-the-given-array-after-each-index/)

给定一个[数组](https://www.geeksforgeeks.org/array-class-c/) **arr[]，**任务是通过在打印每个元素后翻转整个数组来打印从第一个到最后一个索引遍历给定数组形成的数组。

**示例:**

> **输入:** arr = {0，1，2，3，4，5}
> **输出:**0 4 2 4 0
> **解释:**在第一次迭代时，索引 0 - > 0 上的元素被打印，然后整个数组被翻转:{ **0** ，1，2，3，4，5} *- >* {5，4，3，2，1， 0}
> 在第二次迭代中，索引 1 - > 4 上的元素被打印，然后整个数组被翻转::{5， **4** ，3，2，1，0} *- >* {0，1，2，3，4，5}
> 在第三次迭代中，索引 2 - > 2 上的元素被打印，然后整个数组被翻转:{0，1， **2** ，3，4，5} 0}
> 在第二次迭代中，索引 3 - > 2 上的元素被打印，然后整个数组被翻转::{5，4，3， **2** ，1，0} *- >* {0，1，2，3，4，5}
> 在第二次迭代中，索引 4 - > 4 上的元素被打印，然后整个数组被翻转:{0，1，2，3， **4** ，5 0}
> 在第二次迭代中，索引 5 上的元素- > 0 被打印，然后整个数组被翻转::{5，4，3，2，1，**0**}*->*{ 0，1，2，3，4，5}
> 
> **输入:** arr = {0，1，2，3，4}
> **输出:** 0 3 2 1 4

**方法:**给定的问题可以通过使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。思路是[从第一个索引开始从左到右迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，从第二个最后一个索引开始从右到左迭代数组。

可以遵循以下步骤来解决问题:

*   使用指针一从左到右[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，使用指针二从右到左[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
*   同时打印两个指针指向的元素，并将指针 1 增加 2，将指针 2 减少 2

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print array elements at
// every index by flipping whole array
// after printing every element
void printFlip(vector<int> arr)
{

    // Initialize length of the array
    int N = arr.size();

    // Initialize both the pointers
    int p1 = 0, p2 = N - 2;

    // Iterate until both pointers
    // are not out of bounds
    while (p1 < N || p2 >= 0) {

        // Print the elements
        cout << arr[p1] << " ";
        if (p2 > 0)
            cout << arr[p2] << " ";

        // Increment p1 by 2
        p1 += 2;

        // Decrement p2 by 2
        p2 -= 2;
    }
}

// Driver code
int main()
{

    // Initialize the array
    vector<int> arr = { 0, 1, 2, 3, 4 };

    // Call the function
    // and print the array
    printFlip(arr);
    return 0;
}

// This code is contributed by Potta Lokesh.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to print array elements at
    // every index by flipping whole array
    // after printing every element
    public static void printFlip(int[] arr)
    {

        // Initialize length of the array
        int N = arr.length;

        // Initialize both the pointers
        int p1 = 0, p2 = N - 2;

        // Iterate until both pointers
        // are not out of bounds
        while (p1 < N || p2 >= 0) {

            // Print the elements
            System.out.print(arr[p1] + " ");
            if (p2 > 0)
                System.out.print(arr[p2] + " ");

            // Increment p1 by 2
            p1 += 2;

            // Decrement p2 by 2
            p2 -= 2;
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the array
        int[] arr = { 0, 1, 2, 3, 4 };

        // Call the function
        // and print the array
        printFlip(arr);
    }
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to print array elements at
# every index by flipping whole array
# after printing every element
def printFlip(arr):

    # Initialize length of the array
    N = len(arr);

    # Initialize both the pointers
    p1 = 0
    p2 = N - 2;

    # Iterate until both pointers
    # are not out of bounds
    while (p1 < N or p2 >= 0):

        # Print the elements
        print(arr[p1], end=" ");
        if (p2 > 0):
            print(arr[p2], end=" ");

        # Increment p1 by 2
        p1 += 2;

        # Decrement p2 by 2
        p2 -= 2;

# Driver Code
# Initialize the array
arr = [ 0, 1, 2, 3, 4 ];

# Call the function
# and print the array
printFlip(arr);

# This code is contributed by gfgking.
```

## C#

```
// C# implementation for the above approach
using System;

class GFG {

    // Function to print array elements at
    // every index by flipping whole array
    // after printing every element
    static void printFlip(int []arr)
    {

        // Initialize length of the array
        int N = arr.Length;

        // Initialize both the pointers
        int p1 = 0, p2 = N - 2;

        // Iterate until both pointers
        // are not out of bounds
        while (p1 < N || p2 >= 0) {

            // Print the elements
            Console.Write(arr[p1] + " ");
            if (p2 > 0)
                Console.Write(arr[p2] + " ");

            // Increment p1 by 2
            p1 += 2;

            // Decrement p2 by 2
            p2 -= 2;
        }
    }

    // Driver code
    public static void Main()
    {

        // Initialize the array
        int []arr = { 0, 1, 2, 3, 4 };

        // Call the function
        // and print the array
        printFlip(arr);
    }
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to print array elements at
// every index by flipping whole array
// after printing every element
function printFlip(arr)
{

    // Initialize length of the array
    let N = arr.length;

    // Initialize both the pointers
    let p1 = 0, p2 = N - 2;

    // Iterate until both pointers
    // are not out of bounds
    while (p1 < N || p2 >= 0) {

        // Print the elements
        document.write(arr[p1] + " ");
        if (p2 > 0)
            document.write(arr[p2] + " ");

        // Increment p1 by 2
        p1 += 2;

        // Decrement p2 by 2
        p2 -= 2;
    }
}

// Driver Code
// Initialize the array
let arr = [ 0, 1, 2, 3, 4 ];

// Call the function
// and print the array
printFlip(arr);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
0 3 2 1 4 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)