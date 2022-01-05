# 在 O(n)时间内使用堆栈的滑动窗口最大值(k 大小的所有子阵列的最大值)

> 原文:[https://www . geeksforgeeks . org/滑动窗口-最大值-最大值-所有大小的子阵列-k-使用堆叠在时间上/](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k-using-stack-in-on-time/)

给出一个由 **N** 个整数和另一个整数 **k ≤ N** 组成的数组 **arr[]** 。任务是找到大小为 **k** 的每个子数组的最大元素。

**示例:**

```
Input: arr[] = {9, 7, 2, 4, 6, 8, 2, 1, 5}
 k = 3
Output: 9 7 6 8 8 8 5
Explanation:
Window 1: {9, 7, 2}, max = 9
Window 2: {7, 2, 4}, max = 7
Window 3: {2, 4, 6}, max = 6
Window 4: {4, 6, 8}, max = 8
Window 5: {6, 8, 2}, max = 8
Window 6: {8, 2, 1}, max = 8
Window 7: {2, 1, 5}, max = 5

Input: arr[] = {6, 7, 5, 2, 1, 7, 2, 1, 10}
 k = 2
Output: 7 7 5 2 7 7 2 10
Explanation:
Window 1: {6, 7}, max = 7
Window 2: {7, 5}, max = 7
Window 3: {5, 2}, max = 5
Window 4: {2, 1}, max = 2
Window 5: {1, 7}, max = 7
Window 6: {7, 2}, max = 7
Window 7: {2, 1}, max = 2
Window 8: {1, 10}, max = 10
```

***先决条件:*** [*下一个更大的元素*](https://www.geeksforgeeks.org/next-greater-element/)

**<u>方法:</u>**
对于每个指标，计算子阵列从该指标开始时当前元素最大的指标，即对于每个指标 **i** 一个指标 **j ≥ i** ，使得**最大(a[i]，a[i + 1]，… a[j]) = a[i]** 。我们称之为**max _ up[I]**。
然后从 **i <sup>th</sup>** 索引开始的长度 **k** 子数组中的最大元素，可以通过检查从 **i** 到**I+k–1**的每个索引来找到，其中**max _ up[I]≥I+k–1**(该窗口的最后一个索引)。

**堆栈**数据结构可用于将值存储在窗口中，即最后访问的元素或前一个插入的元素将位于顶部(索引最接近当前元素的元素)。

**算法:**

1.  创建一个数组*max _ up*和一个堆栈来存储索引。在堆栈中按 0。
2.  运行从索引 1 到索引 n-1 的循环。
3.  从堆栈中弹出所有索引，哪些元素*(数组[s.top()])* 小于当前元素并更新*max _ up[s . top()]= I–1*，然后在堆栈中插入 I。
4.  从堆栈中弹出所有索引，并分配*max _ upto[s . top()]= n–1*。
5.  创建变量 *j = 0*
6.  运行从 0 到 n–k 的循环，循环计数器为 I
7.  运行嵌套循环，直到 j < i 或 max _ upto[j]< I+k–1，在每次迭代中递增 j。
8.  打印 jth 数组元素。

**实施:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum for
// every k size sub-array
void print_max(int a[], int n, int k)
{
    // max_upto array stores the index
    // upto which the maximum element is a[i]
    // i.e. max(a[i], a[i + 1], ... a[max_upto[i]]) = a[i]

    int max_upto[n];

    // Update max_upto array similar to
    // finding next greater element
    stack<int> s;
    s.push(0);
    for (int i = 1; i < n; i++) {
        while (!s.empty() && a[s.top()] < a[i]) {
            max_upto[s.top()] = i - 1;
            s.pop();
        }
        s.push(i);
    }
    while (!s.empty()) {
        max_upto[s.top()] = n - 1;
        s.pop();
    }
    int j = 0;
    for (int i = 0; i <= n - k; i++) {

        // j < i is to check whether the
        // jth element is outside the window
        while (j < i || max_upto[j] < i + k - 1)
            j++;
        cout << a[j] << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    int a[] = { 9, 7, 2, 4, 6, 8, 2, 1, 5 };
    int n = sizeof(a) / sizeof(int);
    int k = 3;
    print_max(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to print the maximum for
    // every k size sub-array
    static void print_max(int a[], int n, int k)
    {
        // max_upto array stores the index
        // upto which the maximum element is a[i]
        // i.e. max(a[i], a[i + 1], ... a[max_upto[i]]) = a[i]

        int[] max_upto = new int[n];

        // Update max_upto array similar to
        // finding next greater element
        Stack<Integer> s = new Stack<>();
        s.push(0);
        for (int i = 1; i < n; i++)
        {
            while (!s.empty() && a[s.peek()] < a[i])
            {
                max_upto[s.peek()] = i - 1;
                s.pop();
            }
            s.push(i);
        }
        while (!s.empty())
        {
            max_upto[s.peek()] = n - 1;
            s.pop();
        }
        int j = 0;
        for (int i = 0; i <= n - k; i++)
        {

            // j < i is to check whether the
            // jth element is outside the window
            while (j < i || max_upto[j] < i + k - 1)
            {
                j++;
            }
            System.out.print(a[j] + " ");
        }
        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {9, 7, 2, 4, 6, 8, 2, 1, 5};
        int n = a.length;
        int k = 3;
        print_max(a, n, k);

    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the maximum for
# every k size sub-array
def print_max(a, n, k):

    # max_upto array stores the index
    # upto which the maximum element is a[i]
    # i.e. max(a[i], a[i + 1], ... a[max_upto[i]]) = a[i]

    max_upto=[0 for i in range(n)]

    # Update max_upto array similar to
    # finding next greater element
    s=[]
    s.append(0)

    for i in range(1,n):
        while (len(s) > 0 and a[s[-1]] < a[i]):
            max_upto[s[-1]] = i - 1
            del s[-1]

        s.append(i)

    while (len(s) > 0):
        max_upto[s[-1]] = n - 1
        del s[-1]

    j = 0
    for i in range(n - k + 1):

        # j < i is to check whether the
        # jth element is outside the window
        while (j < i or max_upto[j] < i + k - 1):
            j += 1
        print(a[j], end=" ")
    print()

# Driver code

a = [9, 7, 2, 4, 6, 8, 2, 1, 5]
n = len(a)
k = 3
print_max(a, n, k)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to print the maximum for
    // every k size sub-array
    static void print_max(int []a, int n, int k)
    {
        // max_upto array stores the index
        // upto which the maximum element is a[i]
        // i.e. max(a[i], a[i + 1], ... a[max_upto[i]]) = a[i]

        int[] max_upto = new int[n];

        // Update max_upto array similar to
        // finding next greater element
        Stack<int> s = new Stack<int>();
        s.Push(0);
        for (int i = 1; i < n; i++)
        {
            while (s.Count!=0 && a[s.Peek()] < a[i])
            {
                max_upto[s.Peek()] = i - 1;
                s.Pop();
            }
            s.Push(i);
        }
        while (s.Count!=0)
        {
            max_upto[s.Peek()] = n - 1;
            s.Pop();
        }
        int j = 0;
        for (int i = 0; i <= n - k; i++)
        {

            // j < i is to check whether the
            // jth element is outside the window
            while (j < i || max_upto[j] < i + k - 1)
            {
                j++;
            }
            Console.Write(a[j] + " ");
        }
        Console.WriteLine();
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = {9, 7, 2, 4, 6, 8, 2, 1, 5};
        int n = a.Length;
        int k = 3;
        print_max(a, n, k);

    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the maximum for
// every k size sub-array
function print_max(a, n, k)
{

    // max_upto array stores the index
    // upto which the maximum element is a[i]
    // i.e. max(a[i], a[i + 1], ... a[max_upto[i]]) = a[i]
    let max_upto = new Array(n);

    // Update max_upto array similar to
    // finding next greater element
    let s = [];
    s.push(0);

    for(let i = 1; i < n; i++)
    {
        while (s.length != 0 &&
           a[s[s.length - 1]] < a[i])
        {
            max_upto[s[s.length - 1]] = i - 1;
            s.pop();
        }
        s.push(i);
    }

    while (s.length != 0)
    {
        max_upto[s[s.length - 1]] = n - 1;
        s.pop();
    }
    let j = 0;
    for(let i = 0; i <= n - k; i++)
    {

        // j < i is to check whether the
        // jth element is outside the window
        while (j < i || max_upto[j] < i + k - 1)
        {
            j++;
        }
        document.write(a[j] + " ");
    }
    document.write("<br>");
}

// Driver code
let a = [ 9, 7, 2, 4, 6, 8, 2, 1, 5 ];
let n = a.length;
let k = 3;

print_max(a, n, k);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
9 7 6 8 8 8 5
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要遍历两次数组。所以时间复杂度是 O(n)。
*   **空间复杂度:** O(n)。
    需要两个尺寸为 n 的额外空间。

https://youtu.be/m

-Dqu7csdJk？list = plqm 7 alhxfysqdk 2 mdfbwedjd 2 svv JH 9p