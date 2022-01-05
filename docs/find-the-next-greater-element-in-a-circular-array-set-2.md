# 在圆形数组中找到下一个更大的元素|集合 2

> 原文:[https://www . geesforgeks . org/find-下一个更大的循环数组元素集-2/](https://www.geeksforgeeks.org/find-the-next-greater-element-in-a-circular-array-set-2/)

给定一个由 **N** 个整数组成的圆形[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为圆形数组的每个元素打印[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。不存在更大元素的元素，打印**-1”**。

**示例:**

> **输入:** arr[] = {5，6，7}
> **输出:** 6 7 -1
> **解释:**每个数组元素的下一个较大元素如下:
> 对于 arr[0] (= 5) - > 6
> 对于 arr[1] (= 6) - > 7
> 对于 arr[2] (= 7)，数组中不存在较大的元素。因此，打印-1。
> 
> **输入:** arr[] = {4，-2，5，3}
> **输出:** 5 5 -1 4
> **解释:**每个数组元素的下一个较大元素如下:
> For arr[0](= 4)->5
> For arr[1](=-2)->5
> For arr[2](= 5)，数组中不存在较大元素。因此，打印-1。
> 为 arr[3] (= 3) - > 4

**天真方法:**解决这个问题最简单的方法在本文[之前的帖子](https://www.geeksforgeeks.org/find-the-next-greater-element-in-a-circular-array/)中讨论过。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**替代方法:**参考本文的[前一篇文章](https://www.geeksforgeeks.org/find-the-next-greater-element-in-a-circular-array/)来获得空间优化的朴素方法。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，想法是使用[下一个更大元素](https://www.geeksforgeeks.org/next-greater-element/)的概念，该元素使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。按照以下步骤解决问题:

*   初始化一个**堆栈**来存储数组的索引，以及一个大小为 **N** 的数组**nge【】**，该数组存储每个数组元素的下一个较大元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个索引，执行以下操作:
    *   [如果堆栈非空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)且当前 **i** <sup>th</sup> 数组元素大于堆栈的[顶部元素，则](https://www.geeksforgeeks.org/stack-top-c-stl/)[弹出堆栈的顶部元素](https://www.geeksforgeeks.org/stack-pop-method-in-java/)并通过在其中存储 **arr[i % N]** 来更新**nge【ST . top()】**。重复此操作，直到[堆栈为空](https://www.geeksforgeeks.org/stack-empty-method-in-java/)或当前元素小于堆栈顶部的元素。
    *   如果堆栈为空或当前元素小于堆栈顶部，[将 **(i % N)** 推入堆栈](https://www.geeksforgeeks.org/stack-push-method-in-java/)。
*   在 **N** 元素的**单次遍历**之后，堆栈包含在**(N–1)<sup>第</sup>个索引**之前没有下一个更大元素的元素。由于数组是**圆形**，再次考虑 **0 <sup>第</sup>个索引**中的所有元素，找到剩余元素的下一个更大的元素。
*   由于数组遍历 **2 次**，所以最好使用 **i % N** 而不是 **i** 。
*   完成以上步骤后，打印数组 **nge[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the NGE for the
// given circular array arr[]
void printNGE(int* arr, int n)
{
    // Initialize stack and nge[] array
    stack<int> s;
    int nge[n], i = 0;

    // Initialize nge[] array to -1
    for (i = 0; i < n; i++) {
        nge[i] = -1;
    }
    i = 0;

    // Traverse the array
    while (i < 2 * n) {

        // If stack is not empty and
        // current element is greater
        // than top element of the stack
        while (!s.empty()
               && arr[i % n] > arr[s.top()]) {

            // Assign next greater element
            // for the top element of the stack
            nge[s.top()] = arr[i % n];

            // Pop the top element
            // of the stack
            s.pop();
        }

        s.push(i % n);
        i++;
    }

    // Print the nge[] array
    for (i = 0; i < n; i++) {
        cout << nge[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, -2, 5, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printNGE(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the NGE for the
// given circular array arr[]
static void printNGE(int arr[], int n)
{

    // Initialize stack and nge[] array
    Stack<Integer> s = new Stack<>();
    int nge[] = new int[n];
    int i = 0;

    // Initialize nge[] array to -1
    for(i = 0; i < n; i++)
    {
        nge[i] = -1;
    }
    i = 0;

    // Traverse the array
    while (i < 2 * n)
    {

        // If stack is not empty and
        // current element is greater
        // than top element of the stack
        while (!s.isEmpty() &&
               arr[i % n] > arr[s.peek()])
        {

            // Assign next greater element
            // for the top element of the stack
            nge[s.peek()] = arr[i % n];

            // Pop the top element
            // of the stack
            s.pop();
        }
        s.push(i % n);
        i++;
    }

    // Print the nge[] array
    for(i = 0; i < n; i++)
    {
        System.out.print(nge[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, -2, 5, 8 };
    int N = arr.length;

    // Function Call
    printNGE(arr, N);
}
}

// This code is contributed by yashbeersingh42
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the NGE for the
# given circular array arr[]
def printNGE(arr, n) :

    # create stack list
    s = [];

    # Initialize nge[] array to -1
    nge = [-1] * n;

    i = 0;

    # Traverse the array
    while (i < 2 * n) :

        # If stack is not empty and
        # current element is greater
        # than top element of the stack
        while (len(s) != 0 and arr[i % n] > arr[s[-1]]) :

            # Assign next greater element
            # for the top element of the stack
            nge[s[-1]] = arr[i % n];

            # Pop the top element
            # of the stack
            s.pop();

        s.append(i % n);
        i += 1;

    # Print the nge[] array
    for i in range(n) :
        print(nge[i], end= " ");

# Driver Code
if __name__ == "__main__" :

    arr = [ 4, -2, 5, 8 ];
    N = len(arr);

    # Function Call
    printNGE(arr, N);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the NGE for the
// given circular array []arr
static void printNGE(int []arr, int n)
{

    // Initialize stack and nge[] array
    Stack<int> s = new Stack<int>();
    int []nge = new int[n];
    int i = 0;

    // Initialize nge[] array to -1
    for(i = 0; i < n; i++)
    {
        nge[i] = -1;
    }
    i = 0;

    // Traverse the array
    while (i < 2 * n)
    {

        // If stack is not empty and
        // current element is greater
        // than top element of the stack
        while (s.Count != 0 &&
               arr[i % n] > arr[s.Peek()])
        {

            // Assign next greater element
            // for the top element of the stack
            nge[s.Peek()] = arr[i % n];

            // Pop the top element
            // of the stack
            s.Pop();
        }
        s.Push(i % n);
        i++;
    }

    // Print the nge[] array
    for(i = 0; i < n; i++)
    {
        Console.Write(nge[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, -2, 5, 8 };
    int N = arr.Length;

    // Function Call
    printNGE(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the NGE for the
    // given circular array []arr
    function printNGE(arr, n)
    {

        // Initialize stack and nge[] array
        let s = [];
        let nge = new Array(n);
        let i = 0;

        // Initialize nge[] array to -1
        for(i = 0; i < n; i++)
        {
            nge[i] = -1;
        }
        i = 0;

        // Traverse the array
        while (i < 2 * n)
        {

            // If stack is not empty and
            // current element is greater
            // than top element of the stack
            while (s.length != 0 &&
                   arr[i % n] > arr[s[s.length - 1]])
            {

                // Assign next greater element
                // for the top element of the stack
                nge[s[s.length - 1]] = arr[i % n];

                // Pop the top element
                // of the stack
                s.pop();
            }
            s.push(i % n);
            i++;
        }

        // Print the nge[] array
        for(i = 0; i < n; i++)
        {
            document.write(nge[i] + " ");
        }
    }

    let arr = [ 4, -2, 5, 8 ];
    let N = arr.length;

    // Function Call
    printNGE(arr, N);

// This code is contributed by suresh07.
</script>
```

**输出:**

```
5 5 8 -1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)