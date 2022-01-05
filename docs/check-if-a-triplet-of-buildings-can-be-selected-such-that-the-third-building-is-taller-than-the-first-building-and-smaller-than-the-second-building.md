# 检查是否可以选择三个建筑，使得第三个建筑比第一个建筑高，比第二个建筑小

> 原文:[https://www . geeksforgeeks . org/check-if-a-three-of-buildings-can-selected-third-third-the-third-first-building-比第一栋楼高，比第二栋楼小/](https://www.geeksforgeeks.org/check-if-a-triplet-of-buildings-can-be-selected-such-that-the-third-building-is-taller-than-the-first-building-and-smaller-than-the-second-building/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，其中每个数组元素表示位于 **X** 坐标上的建筑物的高度，任务是检查是否有可能选择 **3** 个建筑物，使得第三个选择的建筑物比第一个选择的建筑物高，比第二个选择的建筑物短。

**示例:**

> **输入:** arr[] = {4，7，11，5，13，2}
> **输出:**是
> **解释:**
> 一种可能的方法是选择高度分别为 4、7 和 5 的索引[0，1，3]处的建筑。
> 
> **输入:** arr[] = {11，11，12，9 }
> T3】输出:否

**方法:**给定的问题可以使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)来解决。按照以下步骤解决问题:

*   如果 **N** 小于 **3** ，则打印“ **No** ”。
*   初始化一个数组，说 **preMin[]，**来存储数组 **arr[]的**前缀最小数组**。**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并将 **preMin[i]** 更新为 **preMin[i] = min(preMin[i-1]，arr[i])。**
*   现在，初始化一个[栈，](https://www.geeksforgeeks.org/stack-in-cpp-stl/)说**栈，**以升序存储从末尾开始的元素。
*   使用变量反向遍历数组 **arr[]** ，说出 **i、**，并执行以下步骤:
    *   如果 **arr[i]** 大于 **preMin[i]** ，则执行以下操作:
        *   当**栈**不为空且栈的[顶部元素小于**preMin【I】、**时迭代，然后](https://www.geeksforgeeks.org/stack-top-c-stl/)[在每次迭代中弹出栈](https://www.geeksforgeeks.org/stack-top-c-stl/)的顶部元素。
        *   如果**栈**不为空且[栈顶元素](https://www.geeksforgeeks.org/stack-top-c-stl/)小于**arr【I】，**则打印“**是**”并返回。
        *   否则，完成上述步骤后，[将](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)**arr【I】**推入**栈**。
*   完成上述步骤后，如果上述情况都不满足，则打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to select three buildings that
// satisfy the given condition
string recreationalSpot(int arr[], int N)
{

    if (N < 3) {
        return "No";
    }

    // Stores prefix min array
    int preMin[N];
    preMin[0] = arr[0];

    // Iterate over the range [1, N-1]
    for (int i = 1; i < N; i++) {
        preMin[i] = min(preMin[i - 1], arr[i]);
    }

    // Stores the element from the
    // ending in increasing order
    stack<int> stack;

    // Iterate until j is greater than
    // or equal to 0
    for (int j = N - 1; j >= 0; j--) {

        // If current array element is
        // greater than the prefix min
        // upto j
        if (arr[j] > preMin[j]) {

            // Iterate while stack is not
            // empty and top element is
            // less than or equal to preMin[j]

            while (!stack.empty()
                   && stack.top() <= preMin[j]) {
                // Remove the top element
                stack.pop();
            }

            // If stack is not empty and top
            // element of the stack is less
            // than the current element
            if (!stack.empty() && stack.top() < arr[j]) {
                return "Yes";
            }
            // Push the arr[j] in stack
            stack.push(arr[j]);
        }
    }
    // If none of the above case
    // satisfy then return "No"
    return "No";
}

// Driver code
int main()
{
    // Input
    int arr[] = { 4, 7, 11, 5, 13, 2 };
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << recreationalSpot(arr, size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if it is possible
// to select three buildings that
// satisfy the given condition
static String recreationalSpot(int arr[], int N)
{
    if (N < 3)
    {
        return "No";
    }

    // Stores prefix min array
    int preMin[] = new int[N];
    preMin[0] = arr[0];

    // Iterate over the range [1, N-1]
    for(int i = 1; i < N; i++)
    {
        preMin[i] = Math.min(preMin[i - 1], arr[i]);
    }

    // Stores the element from the
    // ending in increasing order
    Stack<Integer> stack = new Stack<Integer>();

    // Iterate until j is greater than
    // or equal to 0
    for(int j = N - 1; j >= 0; j--)
    {

        // If current array element is
        // greater than the prefix min
        // upto j
        if (arr[j] > preMin[j])
        {

            // Iterate while stack is not
            // empty and top element is
            // less than or equal to preMin[j]
            while (stack.empty() == false &&
                   stack.peek() <= preMin[j])
            {

                // Remove the top element
                stack.pop();
            }

            // If stack is not empty and top
            // element of the stack is less
            // than the current element
            if (stack.empty() == false &&
                stack.peek() < arr[j])
            {
                return "Yes";
            }

            // Push the arr[j] in stack
            stack.push(arr[j]);
        }
    }

    // If none of the above case
    // satisfy then return "No"
    return "No";
}

// Driver code
public static void main(String[] args)
{

    // Input
    int arr[] = { 4, 7, 11, 5, 13, 2 };
    int size = arr.length;

    System.out.println(recreationalSpot(arr, size));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check if it is possible
# to select three buildings that
# satisfy the given condition
def recreationalSpot(arr, N):

    if (N < 3):
        return "No"

    # Stores prefix min array
    preMin = [0] * N
    preMin[0] = arr[0]

    # Iterate over the range [1, N-1]
    for i in range(1, N):
        preMin[i] = min(preMin[i - 1], arr[i])

    # Stores the element from the
    # ending in increasing order
    stack = []

    # Iterate until j is greater than
    # or equal to 0
    for j in range(N - 1, -1, -1):

        # If current array element is
        # greater than the prefix min
        # upto j
        if (arr[j] > preMin[j]):

            # Iterate while stack is not
            # empty and top element is
            # less than or equal to preMin[j]
            while (len(stack) > 0 and
                   stack[-1] <= preMin[j]):

                # Remove the top element
                del stack[-1]

            # If stack is not empty and top
            # element of the stack is less
            # than the current element
            if (len(stack) > 0 and stack[-1] < arr[j]):
                return "Yes"

            # Push the arr[j] in stack
            stack.append(arr[j])

    # If none of the above case
    # satisfy then return "No"
    return "No"

# Driver code
if __name__ == '__main__':

    # Input
    arr =  [ 4, 7, 11, 5, 13, 2 ]
    size = len(arr)

    print (recreationalSpot(arr, size))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
public class GFG{

// Function to check if it is possible
// to select three buildings that
// satisfy the given condition
static String recreationalSpot(int []arr, int N)
{
    if (N < 3)
    {
        return "No";
    }

    // Stores prefix min array  
    int []preMin = new int[N];
    preMin[0] = arr[0];

    // Iterate over the range [1, N-1]
    for(int i = 1; i < N; i++)
    {
        preMin[i] = Math.Min(preMin[i - 1], arr[i]);
    }

    // Stores the element from the
    // ending in increasing order
    Stack<int> stack = new Stack<int>();

    // Iterate until j is greater than
    // or equal to 0
    for(int j = N - 1; j >= 0; j--)
    {

        // If current array element is
        // greater than the prefix min
        // upto j
        if (arr[j] > preMin[j])
        {

            // Iterate while stack is not
            // empty and top element is
            // less than or equal to preMin[j]
            while (stack.Count!=0 &&
                   stack.Peek() <= preMin[j])
            {

                // Remove the top element
                stack.Pop();
            }

            // If stack is not empty and top
            // element of the stack is less
            // than the current element
            if (stack.Count!=0 &&
                stack.Peek() < arr[j])
            {
                return "Yes";
            }

            // Push the arr[j] in stack
            stack.Push(arr[j]);
        }
    }

    // If none of the above case
    // satisfy then return "No"
    return "No";
}

// Driver code
public static void Main(String[] args)
{

    // Input
    int []arr = { 4, 7, 11, 5, 13, 2 };
    int size = arr.Length;

    Console.WriteLine(recreationalSpot(arr, size));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to check if it is possible
// to select three buildings that
// satisfy the given condition
function recreationalSpot(arr, N)
{

    if (N < 3) {
        return "No";
    }

    // Stores prefix min array
    var preMin = new Array(N);
    preMin[0] = arr[0];
    var i;
    // Iterate over the range [1, N-1]
    for (i = 1; i < N; i++) {
        preMin[i] = Math.min(preMin[i - 1], arr[i]);
    }

    // Stores the element from the
    // ending in increasing order
    var st = [];
    var j;
    // Iterate until j is greater than
    // or equal to 0
    for (j = N - 1; j >= 0; j--) {

        // If current array element is
        // greater than the prefix min
        // upto j
        if (arr[j] > preMin[j]) {

            // Iterate while st is not
            // empty and top element is
            // less than or equal to preMin[j]

            while (st.length>0
                   && st[st.length-1] <= preMin[j]) {
                // Remove the top element
                st.pop();
            }

            // If st is not empty and top
            // element of the st is less
            // than the current element
            if (st.length>0 && st[st.length-1] < arr[j]) {
                return "Yes";
            }
            // Push the arr[j] in st
            st.push(arr[j]);
        }
    }
    // If none of the above case
    // satisfy then return "No"
    return "No";
}

// Driver code

    // Input
    var arr = [4, 7, 11, 5, 13, 2];
    var size = arr.length;

    document.write(recreationalSpot(arr, size));

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)