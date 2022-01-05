# 对左右两侧至少有一个较小元素的数组元素进行计数

> 原文:[https://www . geesforgeks . org/count-array-elements-在其左右侧至少有一个较小的元素/](https://www.geeksforgeeks.org/count-array-elements-having-at-least-one-smaller-element-on-its-left-and-right-side/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出数组 **arr[]** 中的元素数量，该数组在其**左侧**和**右侧**包含至少一个较小的元素**。**

**示例:**

> **输入:** arr[] = {3，9，4，6，7，5}
> **输出:** 3
> **说明:**以下 3 个数组元素满足必要条件:
> 
> 1.  arr[1] (= 4)左边的元素较小，为 3，右边的元素较小，为 4
> 2.  arr[3] (= 6)左边的元素较小，为 4，右边的元素较小，为 5。
> 3.  arr[4] (= 7)左边的元素较小，为 6，右边的元素较小，为 5。
> 
> **输入:** arr[] = {3，9，14，61，17，5，12，9，15 }
> T3】输出: 5

**简单方法:**最简单的方法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，计算其左右两边较小元素的数量。如果发现两个计数都至少为 **1** ，则将答案增加 **1** 。最后，打印得到的答案。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)。保持元素的**递增堆叠**，以恒定时间计数较小的元素。按照以下步骤解决问题:

*   初始化一个**堆栈**和一个变量**将**计数为 **0** 作为满足给定条件的数字计数。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   迭代直到[栈不为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)并且当前元素小于栈的[顶元素](https://www.geeksforgeeks.org/stack-top-c-stl/)为止，然后:
        *   堆栈顶部[的元素在右侧有一个较小的元素，即**arr【I】**。](https://www.geeksforgeeks.org/stack-top-c-stl/)
        *   如果**堆栈大小大于 1** ，那么左边还有一个较小的元素，因为堆栈一直保持为增加的堆栈。
        *   如果以上条件为**真**，则按 **1** 递增计数。
        *   [从堆栈中弹出顶部元素](https://www.geeksforgeeks.org/stack-pop-method-in-java/)。
    *   将当前元素推入堆栈。
*   经过上述步骤后，**计数**的值给出了结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to count the number of
// elements that have smaller on
// left and right side
void findElements(int* arr, int N)
{
    // Initialize stack
    stack<int> stack;

    // Stores the required count
    // of array elements
    int count = 0;

    // Traverse the array A{]
    for (int i = 0; i < N; i++) {

        // If stack is not empty
        // and stack top > arr[i]
        while (!stack.empty()
               && arr[i] < stack.top()) {

            // If stack size > 1
            if (stack.size() > 1)

                // Increment count
                count++;

            // Pop the top element
            stack.pop();
        }

        // Push the element arr[i]
        stack.push(arr[i]);
    }

    // Print the final count
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 9, 4, 6, 7, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findElements(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to count the number of
// elements that have smaller on
// left and right side
static void findElements(int[] arr,
                         int N)
{
  // Initialize stack
  Stack<Integer> stack = new Stack<>();

  // Stores the required count
  // of array elements
  int count = 0;

  // Traverse the array A{]
  for (int i = 0; i < N; i++)
  {
    // If stack is not empty
    // and stack top > arr[i]
    while (!stack.isEmpty() &&
           arr[i] < stack.peek())
    {
      // If stack size > 1
      if (stack.size() > 1)

        // Increment count
        count++;

      // Pop the top element
      stack.pop();
    }

    // Push the element arr[i]
    stack.add(arr[i]);
  }

  // Print the final count
  System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {3, 9, 4, 6, 7, 5};
  int N = arr.length;

  // Function Call
  findElements(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# elements that have smaller on
# left and right side
def findElements(arr, N):

    # Initialize stack
    stack = []

    # Stores the required count
    # of array elements
    count = 0

    # Traverse the array A{]
    for i in range(N):

        # If stack is not empty
        # and stack top > arr[i]
        while (len(stack) > 0 and
                   arr[i] < stack[-1]):

            # If stack size > 1
            if (len(stack) > 1):

                # Increment count
                count += 1

            # Pop the top element
            del stack[-1]

        # Push the element arr[i]
        stack.append(arr[i])

    # Print the final count
    print(count)

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 9, 4, 6, 7, 5 ]
    N = len(arr)

    # Function Call
    findElements(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// elements that have smaller on
// left and right side
static void findElements(int[] arr, int N)
{

    // Initialize stack
    Stack<int> stack = new Stack<int>();

    // Stores the required count
    // of array elements
    int count = 0;

    // Traverse the array A{]
    for(int i = 0; i < N; i++)
    {

        // If stack is not empty
        // and stack top > arr[i]
        while (stack.Count != 0 &&
               arr[i] < stack.Peek())
        {

            // If stack size > 1
            if (stack.Count > 1)

                // Increment count
                count++;

            // Pop the top element
            stack.Pop();
        }

        // Push the element arr[i]
        stack.Push(arr[i]);
    }

    // Print the readonly count
    Console.Write(count);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 9, 4, 6, 7, 5 };
    int N = arr.Length;

    // Function Call
    findElements(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of
// elements that have smaller on
// left and right side
function findElements(arr, N)
{
    // Initialize stack
    var stack = [];

    // Stores the required count
    // of array elements
    var count = 0;

    // Traverse the array A{]
    for (var i = 0; i < N; i++) {

        // If stack is not empty
        // and stack top > arr[i]
        while (stack.length!=0
               && arr[i] < stack[stack.length-1]) {

            // If stack size > 1
            if (stack.length > 1)

                // Increment count
                count++;

            // Pop the top element
            stack.pop();
        }

        // Push the element arr[i]
        stack.push(arr[i]);
    }

    // Print the final count
    document.write( count);
}

// Driver Code
var arr = [3, 9, 4, 6, 7, 5];
var N = arr.length;

// Function Call
findElements(arr, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)