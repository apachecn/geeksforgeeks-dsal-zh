# 一个数组的所有可能子数组的最小元素之和

> 原文:[https://www . geesforgeks . org/所有可能子数组的最小元素之和/一个数组的子数组/](https://www.geeksforgeeks.org/sum-of-minimum-elements-of-all-possible-sub-arrays-of-an-array/)

给定一个数组 **arr[]** ，任务是找到该数组中每个可能子数组的最小元素的和。

**示例:**

> **输入:** arr[] = {1，3，2}
> **输出:** 15
> 所有可能的子数组为{1}、{2}、{3}、{1，3}、{3，2}和{1，3，2}
> 并且，所有最小元素的和为 1 + 2 + 3 + 1 + 2 + 1 = 10
> **输入:** arr[] = {3，1}
> **输出::**

一个**简单的方法**就是生成所有的子数组，然后将所有子数组中的最小元素求和。该解决方案的时间复杂度为 0(n<sup>3</sup>)。
**更好的方法:**
优化的关键是问题——

> 在多少个细分市场中，一个指数的价值是最小的？

我们可能会想到的下一个想法是，对于数组 **arr** 中的每个索引 **i** ，我们试图找到:
**左计数:**我们向索引 **i** 的左侧迭代，直到我们没有遇到严格小于**arr【I】**的元素**或者我们没有到达数组的左端。让我们将给定数组的索引 **i** 的计数称为 **CLi** 。
**右计数:**我们向索引的右侧迭代，直到没有遇到小于或等于索引处的值**的元素**，或者我们没有到达右端。让我们将给定数组的索引 **i** 的计数称为 **CRi** 。
**(CLi + 1) * (CRi + 1)** 将是当前索引 **i** 的子数组数量，其中其值将最小，因为有 **CLi + 1** 方式从左侧选择元素(包括不选择元素)和 **CRi + 1** 方式从右侧选择元素。**

> 这种方法的时间复杂度为 0(n<sup>2</sup>)

**最佳方法:**
这个问题可以用 **O(n)** 时间内的堆栈数据结构来解决。这个想法和以前的方法一样。为了节省一些时间，我们将使用 C++标准模板库中的一个堆栈。
**左计数:**让 **CLi** 代表一个索引 **i** 的左计数。 **CLi** 对于一个索引 **i** 可以定义为索引 **i** 和其值严格小于**arr【I】**且索引小于 **i** 的最右边元素之间的元素数。如果没有这样的元素，那么一个元素的 **CLi** 将等于索引 **i** 左边的元素数量。
为了实现这一点，我们将只把元素的索引从左到右插入到堆栈中。让我们假设，我们正在堆栈中插入一个索引 **i** ，而 **j** 是当前堆栈中最顶层元素的索引。当值**arr[I]****小于或等于**堆栈中最顶层索引处的值且堆栈不为空时，继续弹出堆栈中的元素。每当弹出一个元素时，当前索引(I)的左计数(CLi)更新为 **CLi = CLi + CLj + 1** 。
**正确计数:**我们对所有指标计算正确计数的方法类似。唯一的区别是，我们在数组中从右向左遍历的同时推送堆栈中的元素。虽然 **arr[i]** 严格来说比栈中最顶层索引处的值少**，并且栈不是空的，但是继续弹出元素。每当弹出一个元素时，当前索引(I)的正确计数更新为 **CRi = CRi + CRj + 1** 。
**最终步骤:**让 **ans** 成为包含最终答案的变量。我们将用 **0** 初始化。然后，我们将遍历数组中从 **1** 到 **n** 的所有索引，并将 **ans** 更新为**ans = ans+(CLi+1)*(CRi+1)* arr[I]**，以获取从 **1** 到 **n** 的所有可能值。
以下是上述方法的实施:**

## **C++**

```
// C++ implementation of the approach
#include <iostream>
#include <stack>
using namespace std;

// Function to return the required sum
int findMinSum(int arr[], int n)
{
    // Arrays for maintaining left and right count
    int CL[n] = { 0 }, CR[n] = { 0 };

    // Stack for storing the indexes
    stack<int> q;

    // Calculate left count for every index
    for (int i = 0; i < n; i++) {
        while (q.size() != 0 && arr[q.top()] >= arr[i]) {
            CL[i] += CL[q.top()] + 1;
            q.pop();
        }
        q.push(i);
    }

    // Clear the stack
    while (q.size() != 0)
        q.pop();

    // Calculate right count for every index
    for (int i = n - 1; i >= 0; i--) {
        while (q.size() != 0 && arr[q.top()] > arr[i]) {
            CR[i] += CR[q.top()] + 1;
            q.pop();
        }
        q.push(i);
    }

    // Clear the stack
    while (q.size() != 0)
        q.pop();

    // To store the required sum
    int ans = 0;

    // Calculate the final sum
    for (int i = 0; i < n; i++)
        ans += (CL[i] + 1) * (CR[i] + 1) * arr[i];

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMinSum(arr, n);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to return the required sum
static int findMinSum(int arr[], int n)
{
    // Arrays for maintaining left and right count
    int CL[] = new int[n], CR[] = new int[n];

    // Stack for storing the indexes
    Stack<Integer> q = new Stack<Integer>();

    // Calculate left count for every index
    for (int i = 0; i < n; i++)
    {
        while (q.size() != 0 && arr[q.peek()] >= arr[i])
        {
            CL[i] += CL[q.peek()] + 1;
            q.pop();
        }
        q.push(i);
    }

    // Clear the stack
    while (q.size() != 0)
        q.pop();

    // Calculate right count for every index
    for (int i = n - 1; i >= 0; i--)
    {
        while (q.size() != 0 && arr[q.peek()] > arr[i])
        {
            CR[i] += CR[q.peek()] + 1;
            q.pop();
        }
        q.push(i);
    }

    // Clear the stack
    while (q.size() != 0)
        q.pop();

    // To store the required sum
    int ans = 0;

    // Calculate the final sum
    for (int i = 0; i < n; i++)
        ans += (CL[i] + 1) * (CR[i] + 1) * arr[i];

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 2 };
    int n = arr.length;
    System.out.println(findMinSum(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to return the required sum
def findMinSum(arr, n):

    # Arrays for maintaining left and
    # right count
    CL = [0] * n
    CR = [0] * n

    # Stack for storing the indexes
    q = []

    # Calculate left count for every index
    for i in range(0, n):
        while (len(q) != 0 and
               arr[q[-1]] >= arr[i]):
            CL[i] += CL[q[-1]] + 1
            q.pop()

        q.append(i)

    # Clear the stack
    while len(q) != 0:
        q.pop()

    # Calculate right count for every index
    for i in range(n - 1, -1, -1):
        while (len(q) != 0 and
               arr[q[-1]] > arr[i]):
            CR[i] += CR[q[-1]] + 1
            q.pop()

        q.append(i)

    # Clear the stack
    while len(q) != 0:
        q.pop()

    # To store the required sum
    ans = 0

    # Calculate the final sum
    for i in range(0, n):
        ans += (CL[i] + 1) * (CR[i] + 1) * arr[i]

    return ans

# Driver code
if __name__ == "__main__":

    arr = [1, 3, 2]
    n = len(arr)
    print(findMinSum(arr, n))

# This code is contributed by Rituraj Jain
```

## **C#**

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the required sum
static int findMinSum(int []arr, int n)
{
    // Arrays for maintaining left and right count
    int []CL = new int[n];
    int []CR = new int[n];

    // Stack for storing the indexes
    Stack<int> q = new Stack<int>();

    // Calculate left count for every index
    for (int i = 0; i < n; i++)
    {
        while (q.Count != 0 && arr[q.Peek()] >= arr[i])
        {
            CL[i] += CL[q.Peek()] + 1;
            q.Pop();
        }
        q.Push(i);
    }

    // Clear the stack
    while (q.Count != 0)
        q.Pop();

    // Calculate right count for every index
    for (int i = n - 1; i >= 0; i--)
    {
        while (q.Count != 0 && arr[q.Peek()] > arr[i])
        {
            CR[i] += CR[q.Peek()] + 1;
            q.Pop();
        }
        q.Push(i);
    }

    // Clear the stack
    while (q.Count != 0)
        q.Pop();

    // To store the required sum
    int ans = 0;

    // Calculate the final sum
    for (int i = 0; i < n; i++)
        ans += (CL[i] + 1) * (CR[i] + 1) * arr[i];

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 3, 2 };
    int n = arr.Length;
    Console.WriteLine(findMinSum(arr, n));
}
}

// This code has been contributed
// by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

// Function to return the required sum
function findMinSum(arr, n)
{
    // Arrays for maintaining left and right count
    var CL = Array(n).fill(0);
    var CR = Array(n).fill(0);

    // Stack for storing the indexes
    var q = [];

    // Calculate left count for every index
    for (var i = 0; i < n; i++) {
        while (q.length != 0 && arr[q[q.length-1]] >= arr[i]) {
            CL[i] += CL[q[q.length-1]] + 1;
            q.pop();
        }
        q.push(i);
    }

    // Clear the stack
    while((q.length) != 0)
        q.pop();

    // Calculate right count for every index
    for (var i = n - 1; i >= 0; i--) {
        while (q.length != 0 && arr[q[q.length-1]] > arr[i]) {
            CR[i] += CR[q[q.length-1]] + 1;
            q.pop();
        }
        q.push(i);
    }

    // Clear the stack
    while((q.length) != 0)
        q.pop();

    // To store the required sum
    var ans = 0;

    // Calculate the final sum
    for (var i = 0; i < n; i++)
        ans += (CL[i] + 1) * (CR[i] + 1) * arr[i];

    return ans;
}

// Driver code
var arr = [1, 3, 2 ];
var n = arr.length;
document.write( findMinSum(arr, n));

</script>
```

****Output:** 

```
10
```** 

****时间复杂度:**O(n)
T3】辅助空间 : O(n)**