# 找到每个数组元素右边的下一个非零数组元素

> 原文:[https://www . geesforgeks . org/find-每个数组元素右边的下一个非零数组元素/](https://www.geeksforgeeks.org/find-the-next-non-zero-array-element-to-the-right-of-each-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在每个数组元素的右边找到下一个非零数组元素。如果不存在任何非零元素，则打印该元素本身。

**示例:**

> **输入:** arr[] = {1，2，0}
> **输出:** {2，2，0}
> **解释:**
> 对于每个数组元素，下一个非零元素是:
> arr[0]= 1->2
> arr[1]= 2->2(因为不存在任何非零元素)
> arr[2] = 0 - > 0(因为不存在)
> 
> **输入:** arr[] = {1，0，0，3}
> **输出:** {3，3，3，3}

**方法:**这个问题的简单方法是[从头到尾遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，跟踪遍历时得到的每个非零元素的变量，并用该变量替换数组中的整数。按照以下步骤解决给定的问题:

*   创建一个变量，比如 **tempValid** ，来跟踪有效的整数，并将其初始化为 **-1** 。
*   创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **结果[]** ，将下一个非零数组元素存储在每个数组元素的右侧。
*   [从索引**N–1**到 **0** 的末尾迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，如果 **tempValid** 的值为 **-1** ，则将当前索引的下一个非零元素指定为数字本身，即**arr【I】**。否则，将**结果[i]** 的值更新为**温度有效**。
*   完成以上步骤后，[打印数组**结果【】**T3】作为结果。](https://www.geeksforgeeks.org/java-program-to-print-the-elements-of-an-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the next non-zero
// element to the right of each array
// elements
void NextValidInteger(int arr[], int N)
{

    // Stores the resultant array
    int result[N];

    // Keeps the track of next non-zero
    // element for each array element
    int tempValid = -1;

    // Iterate the array from right to left
    // and update tempValid
    for (int i = N - 1; i >= 0; i--) {

        // If tempValid is -1, the valid
        // number at current index is the
        // number itself
        if (tempValid == -1) {
            result[i] = arr[i];
        }
        else {
            result[i] = tempValid;
        }

        // Update tempValid if the
        // current element is non-zero
        if (arr[i] != 0) {
            tempValid = arr[i];
        }
    }

    // Print the result
    for (int i = 0; i < N; i++) {
        cout << result[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 0, 2, 4, 5, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    NextValidInteger(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to find the next non-zero
    // element to the right of each array
    // elements
    static void NextValidInteger(int arr[], int N)
    {

        // Stores the resultant array
        int result[] = new int[N];

        // Keeps the track of next non-zero
        // element for each array element
        int tempValid = -1;

        // Iterate the array from right to left
        // and update tempValid
        for (int i = N - 1; i >= 0; i--) {

            // If tempValid is -1, the valid
            // number at current index is the
            // number itself
            if (tempValid == -1) {
                result[i] = arr[i];
            }
            else {
                result[i] = tempValid;
            }

            // Update tempValid if the
            // current element is non-zero
            if (arr[i] != 0) {
                tempValid = arr[i];
            }
        }

        // Print the result
        for (int i = 0; i < N; i++) {
            System.out.print(result[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 0, 2, 4, 5, 0 };
        int N = 7;
        NextValidInteger(arr, N);
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the next non-zero
# element to the right of each array
# elements
def NextValidInteger(arr, N):

    # Stores the resultant array
    result = [0 for _ in range(N)]

    # Keeps the track of next non-zero
    # element for each array element
    tempValid = -1

    # Iterate the array from right to left
    # and update tempValid
    for i in range(N-1, -1, -1):

        # If tempValid is -1, the valid
        # number at current index is the
        # number itself
        if (tempValid == -1):
            result[i] = arr[i]

        else:
            result[i] = tempValid

        # Update tempValid if the
        # current element is non-zero
        if (arr[i] != 0):
            tempValid = arr[i]

    # Print the result
    for i in range(0, N):
        print(result[i], end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 0, 2, 4, 5, 0]
    N = len(arr)
    NextValidInteger(arr, N)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the next non-zero
    // element to the right of each array
    // elements
    static void NextValidInteger(int[] arr, int N)
    {

        // Stores the resultant array
        int[] result = new int[N];

        // Keeps the track of next non-zero
        // element for each array element
        int tempValid = -1;

        // Iterate the array from right to left
        // and update tempValid
        for (int i = N - 1; i >= 0; i--) {

            // If tempValid is -1, the valid
            // number at current index is the
            // number itself
            if (tempValid == -1) {
                result[i] = arr[i];
            }
            else {
                result[i] = tempValid;
            }

            // Update tempValid if the
            // current element is non-zero
            if (arr[i] != 0) {
                tempValid = arr[i];
            }
        }

        // Print the result
        for (int i = 0; i < N; i++) {
            Console.Write(result[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 0, 2, 4, 5, 0 };
        int N = 7;
        NextValidInteger(arr, N);
    }
}

// This code is contributed by Saurabh
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the next non-zero
        // element to the right of each array
        // elements
        function NextValidInteger(arr, N) {

            // Stores the resultant array
            let result = new Array(N);

            // Keeps the track of next non-zero
            // element for each array element
            let tempValid = -1;

            // Iterate the array from right to left
            // and update tempValid
            for (let i = N - 1; i >= 0; i--) {

                // If tempValid is -1, the valid
                // number at current index is the
                // number itself
                if (tempValid == -1) {
                    result[i] = arr[i];
                }
                else {
                    result[i] = tempValid;
                }

                // Update tempValid if the
                // current element is non-zero
                if (arr[i] != 0) {
                    tempValid = arr[i];
                }
            }

            // Print the result
            for (let i = 0; i < N; i++) {
                document.write(result[i] + " ");
            }
        }

        // Driver Code
        let arr = [1, 2, 0, 2, 4, 5, 0];
        let N = arr.length;
        NextValidInteger(arr, N);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2 2 2 4 5 5 0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)