# 找出给定数组中每个窗口大小的最小值的最大值

> 原文:[https://www . geeksforgeeks . org/find-给定阵列中每个窗口大小的最小值中的最大值/](https://www.geeksforgeeks.org/find-the-maximum-of-minimums-for-every-window-size-in-a-given-array/)

给定大小为 n 的整数数组，求数组中每个窗口大小的最小值的最大值。请注意，窗口大小从 1 到 n 不等。
**示例:**

> 输入:arr[] = {10，20，30，50，10，70，30}
> 输出:70，30，20，10，10，10，10
> 输出中的第一个元素表示大小为 1 的所有
> 窗口的最小值的最大值。
> 1 号车窗的最小尺寸为{10}、{20}、{30}、{50}、{10}、
> 、{70}和{30}。这些最小值的最大值是 70
> 输出中的第二个元素表示大小为 2 的所有
> 窗口的最小值的最大值。
> 大小为 2 的窗口的最小值为{10}、{20}、{30}、{10}、{10}、
> 和{30}。这些最小值的最大值为 30
> 输出中的第三个元素表示大小为 3 的所有
> 窗口的最小值的最大值。
> 大小为 3 的窗口的最小值为{10}、{20}、{10}、{10}和{10}。
> 这些最小值的最大值为 20
> 同样，计算输出的其他元素。

**<u>天真大法</u> :** 蛮力。
**方法:**解决这个问题的一个简单的蛮力方法可以是生成特定长度的所有可能的窗口，比如“L”，并在所有这样的窗口中找到最小元素。然后找到所有这些元素的最大值并存储起来。现在，窗口的长度是 1 < =L < =N。因此，我们必须生成大小为“1”到“N”的所有可能的窗口，为了生成每个这样的窗口，我们必须标记该窗口的端点。为此，我们必须使用嵌套循环来分别固定窗口的起点和终点。因此，在强力方法中将使用三重嵌套循环，主要用于固定窗口的长度、起点和终点。

## C++

```
// A naive method to find maximum of
// minimum of all windows of different
// sizes
#include <bits/stdc++.h>
using namespace std;

void printMaxOfMin(int arr[], int n)
{
    // Consider all windows of different
    // sizes starting from size 1
    for (int k = 1; k <= n; k++) {
        // Initialize max of min for
        // current window size k
        int maxOfMin = INT_MIN;

        // Traverse through all windows
        // of current size k
        for (int i = 0; i <= n - k; i++) {
            // Find minimum of current window
            int min = arr[i];
            for (int j = 1; j < k; j++) {
                if (arr[i + j] < min)
                    min = arr[i + j];
            }

            // Update maxOfMin if required
            if (min > maxOfMin)
                maxOfMin = min;
        }

        // Print max of min for current
        // window size
        cout << maxOfMin << " ";
    }
}

// Driver program
int main()
{
    int arr[] = { 10, 20, 30, 50, 10, 70, 30 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printMaxOfMin(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive method to find maximum of
// minimum of all windows of different sizes

class Test {
    static int arr[] = { 10, 20, 30, 50, 10, 70, 30 };

    static void printMaxOfMin(int n)
    {
        // Consider all windows of different
        // sizes starting from size 1
        for (int k = 1; k <= n; k++) {
            // Initialize max of min for current
            // window size k
            int maxOfMin = Integer.MIN_VALUE;

            // Traverse through all windows of
            // current size k
            for (int i = 0; i <= n - k; i++) {
                // Find minimum of current window
                int min = arr[i];
                for (int j = 1; j < k; j++) {
                    if (arr[i + j] < min)
                        min = arr[i + j];
                }

                // Update maxOfMin if required
                if (min > maxOfMin)
                    maxOfMin = min;
            }

            // Print max of min for current
            // window size
            System.out.print(maxOfMin + " ");
        }
    }

    // Driver method
    public static void main(String[] args)
    {
        printMaxOfMin(arr.length);
    }
}
```

## 蟒蛇 3

```
# A naive method to find maximum of
# minimum of all windows of different sizes
INT_MIN = -1000000
def printMaxOfMin(arr, n):

    # Consider all windows of different
    # sizes starting from size 1
    for k in range(1, n + 1):

        # Initialize max of min for
        # current window size k
        maxOfMin = INT_MIN;

        # Traverse through all windows
        # of current size k
        for i in range(n - k + 1):

            # Find minimum of current window
            min = arr[i]
            for j in range(k):
                if (arr[i + j] < min):
                    min = arr[i + j]

            # Update maxOfMin if required
            if (min > maxOfMin):
                maxOfMin = min

        # Print max of min for current window size
        print(maxOfMin, end = " ")

# Driver Code
arr = [10, 20, 30, 50, 10, 70, 30]
n = len(arr)
printMaxOfMin(arr, n)

# This code is contributed by sahilshelangia
```

## C#

```
// C# program using Naive approach to find
// maximum of minimum of all windows of
// different sizes
using System;

class GFG{

    static int []arr = {10, 20, 30, 50, 10, 70, 30};

    // Function to print maximum of minimum
    static void printMaxOfMin(int n)
    {

        // Consider all windows of different
        // sizes starting from size 1
        for (int k = 1; k <= n; k++)
        {

            // Initialize max of min for
            // current window size k
            int maxOfMin = int.MinValue;

            // Traverse through all windows
            // of current size k
            for (int i = 0; i <= n - k; i++)
            {

                // Find minimum of current window
                int min = arr[i];
                for (int j = 1; j < k; j++)
                {
                    if (arr[i + j] < min)
                        min = arr[i + j];
                }

                // Update maxOfMin if required
                if (min > maxOfMin)
                    maxOfMin = min;
            }

            // Print max of min for current window size
            Console.Write(maxOfMin + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        printMaxOfMin(arr.Length);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum of
// minimum of all windows of
// different sizes

// Method to find maximum of
// minimum of all windows of
// different sizes
function printMaxOfMin($arr, $n)
{

    // Consider all windows of
    // different sizes starting
    // from size 1
    for($k = 1; $k <= $n; $k++)
    {

        // Initialize max of min for
        // current window size k
        $maxOfMin = PHP_INT_MIN;

        // Traverse through all windows
        // of current size k
        for ($i = 0; $i <= $n-$k; $i++)
        {

            // Find minimum of current window
            $min = $arr[$i];
            for ($j = 1; $j < $k; $j++)
            {
                if ($arr[$i + $j] < $min)
                    $min = $arr[$i + $j];
            }

            // Update maxOfMin
            // if required
            if ($min > $maxOfMin)
            $maxOfMin = $min;
        }

        // Print max of min for
        // current window size
        echo $maxOfMin , " ";
    }
}

    // Driver Code
    $arr= array(10, 20, 30, 50, 10, 70, 30);
    $n = sizeof($arr);
    printMaxOfMin($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// A naive method to find maximum of
// minimum of all windows of different sizes

    var arr = [ 10, 20, 30, 50, 10, 70, 30 ];

    function printMaxOfMin(n) {
        // Consider all windows of different
        // sizes starting from size 1
        for (k = 1; k <= n; k++) {
            // Initialize max of min for current
            // window size k
            var maxOfMin = Number.MIN_VALUE;

            // Traverse through all windows of
            // current size k
            for (i = 0; i <= n - k; i++) {
                // Find minimum of current window
                var min = arr[i];
                for (j = 1; j < k; j++) {
                    if (arr[i + j] < min)
                        min = arr[i + j];
                }

                // Update maxOfMin if required
                if (min > maxOfMin)
                    maxOfMin = min;
            }

            // Print max of min for current
            // window size
            document.write(maxOfMin + " ");
        }
    }

    // Driver method

        printMaxOfMin(arr.length);

// This code contributed by aashish1995
</script>
```

**输出:**

```
70 30 20 10 10 10 10
```

**复杂度分析:**

*   **时间复杂度:** O(n <sup>3</sup> )。
    因为在这种方法中使用了三重嵌套循环。
*   **辅助空间:** O(1)
    因为没有使用额外的数据结构来存储这些值。

**<u>高效解决方案</u> :** 我们可以在 O(n)时间内解决这个问题。这个想法是利用额外的空间。下面是详细的步骤。
**第一步:**为每个元素寻找下一个更小的和上一个更小的索引。下一个较小的元素是 arr[i]右侧最近的最小元素。类似地，前一个较小的元素是 arr[i]左侧最近的最小元素。
如果右侧没有更小的元素，那么下一个更小的就是 n，如果左侧没有更小的，那么上一个更小的就是-1。
对于输入{10，20，30，50，10，70，30}，下一个较小的索引数组是{7，4，4，4，7，6，7}。
对于输入{10，20，30，50，10，70，30}，先前较小的索引数组是{-1，0，1，2，-1，4，4}
这一步可以使用[下一个较大的元素](https://www.geeksforgeeks.org/next-greater-element/)中讨论的方法在 O(n)时间内完成。
**步骤 2:** 一旦我们有了下一个和上一个更小的索引，我们就知道 arr[i]是长度为“右[I]–左[I]–1”的窗口的最小值。元素最少的窗口长度为{7，3，2，1，7，1，2}。该数组表示，第一个元素在大小为 7 的窗口中最小，第二个元素在大小为 3 的窗口中最小，依此类推。
创建一个辅助数组 ans[n+1]来存储结果。ans[]中的值可以通过迭代右[]和左[]来填充

```
    for (int i=0; i < n; i++)
    {
        // length of the interval
        int len = right[i] - left[i] - 1;

        // arr[i] is a possible answer for
        // this length len interval
        ans[len] = max(ans[len], arr[i]);
    }
```

我们得到的 ans[]数组为{0，70，30，20，0，0，0，10}。请注意，ans[0]或长度为 0 的答案是无用的。
**第三步:**ans[]中有些条目为 0，尚未填写。例如，我们知道长度 1、2、3 和 7 的最小值的最大值分别是 70、30、20 和 10，但是我们不知道长度 4、5 和 6 的最小值。
以下是填充剩余条目的一些重要观察结果
a)长度 I 的结果，即 ans[i]将总是大于或等于长度 i+1 的结果，即 ans[i+1]。
b)如果 ans[i]没有被填充，这意味着没有长度 I 最小的直接元素，因此长度 ans[i+1]或 ans[i+2]的元素与 ans[i]
相同，因此我们使用下面的循环填充其余条目。

```
    for (int i=n-1; i>=1; i--)
        ans[i] = max(ans[i], ans[i+1]);
```

下面是上述算法的实现。

## C++

```
// An efficient C++ program to find
// maximum of all minimums of
// windows of different sizes
#include <iostream>
#include<stack>
using namespace std;

void printMaxOfMin(int arr[], int n)
{
// Used to find previous and next smaller
    stack<int> s;

    // Arrays to store previous and next smaller
    int left[n+1]; 
    int right[n+1];

    // Initialize elements of left[] and right[]
    for (int i=0; i<n; i++)
    {
        left[i] = -1;
        right[i] = n;
    }

    // Fill elements of left[] using logic discussed on
    // https://www.geeksforgeeks.org/next-greater-element/
    for (int i=0; i<n; i++)
    {
        while (!s.empty() && arr[s.top()] >= arr[i])
            s.pop();

        if (!s.empty())
            left[i] = s.top();

        s.push(i);
    }

    // Empty the stack as stack is
// going to be used for right[]
    while (!s.empty())
        s.pop();

    // Fill elements of right[] using same logic
    for (int i = n-1 ; i>=0 ; i-- )
    {
        while (!s.empty() && arr[s.top()] >= arr[i])
            s.pop();

        if(!s.empty())
            right[i] = s.top();

        s.push(i);
    }

    // Create and initialize answer array
    int ans[n+1];
    for (int i=0; i<=n; i++)
        ans[i] = 0;

    // Fill answer array by comparing minimums of all
    // lengths computed using left[] and right[]
    for (int i=0; i<n; i++)
    {
        // length of the interval
        int len = right[i] - left[i] - 1;

        // arr[i] is a possible answer for this length
        // 'len' interval, check if arr[i] is more than
        // max for 'len'
        ans[len] = max(ans[len], arr[i]);
    }

    // Some entries in ans[] may not be filled yet. Fill
    // them by taking values from right side of ans[]
    for (int i=n-1; i>=1; i--)
        ans[i] = max(ans[i], ans[i+1]);

    // Print the result
    for (int i=1; i<=n; i++)
        cout << ans[i] << " ";
}

// Driver program
int main()
{
    int arr[] = {10, 20, 30, 50, 10, 70, 30};
    int n = sizeof(arr)/sizeof(arr[0]);
    printMaxOfMin(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to find
// maximum of all minimums of
// windows of different size

import java.util.Stack;

class Test
{
    static int arr[] = {10, 20, 30, 50, 10, 70, 30};

    static void printMaxOfMin(int n)
    {
        // Used to find previous and next smaller
        Stack<Integer> s = new Stack<>();

        // Arrays to store previous and next smaller
        int left[] = new int[n+1]; 
        int right[]  = new int[n+1];

        // Initialize elements of left[] and right[]
        for (int i=0; i<n; i++)
        {
            left[i] = -1;
            right[i] = n;
        }

        // Fill elements of left[] using logic discussed on
        // https://www.geeksforgeeks.org/next-greater-element/
        for (int i=0; i<n; i++)
        {
            while (!s.empty() && arr[s.peek()] >= arr[i])
                s.pop();

            if (!s.empty())
                left[i] = s.peek();

            s.push(i);
        }

        // Empty the stack as stack is
// going to be used for right[]
        while (!s.empty())
            s.pop();

        // Fill elements of right[] using same logic
        for (int i = n-1 ; i>=0 ; i-- )
        {
            while (!s.empty() && arr[s.peek()] >= arr[i])
                s.pop();

            if(!s.empty())
                right[i] = s.peek();

            s.push(i);
        }

        // Create and initialize answer array
        int ans[] = new int[n+1];
        for (int i=0; i<=n; i++)
            ans[i] = 0;

        // Fill answer array by comparing minimums of all
        // lengths computed using left[] and right[]
        for (int i=0; i<n; i++)
        {
            // length of the interval
            int len = right[i] - left[i] - 1;

            // arr[i] is a possible answer for this length
            // 'len' interval, check if arr[i] is more than
            // max for 'len'
            ans[len] = Math.max(ans[len], arr[i]);
        }

        // Some entries in ans[] may not be filled yet. Fill
        // them by taking values from right side of ans[]
        for (int i=n-1; i>=1; i--)
            ans[i] = Math.max(ans[i], ans[i+1]);

        // Print the result
        for (int i=1; i<=n; i++)
            System.out.print(ans[i] + " ");
    }

    // Driver method
    public static void main(String[] args)
    {
        printMaxOfMin(arr.length);
    }
}
```

## 蟒蛇 3

```
# An efficient Python3 program to find
# maximum of all minimums of windows of
# different sizes

def printMaxOfMin(arr, n):

    s = [] # Used to find previous
           # and next smaller

    # Arrays to store previous and next
    # smaller. Initialize elements of
    # left[] and right[]
    left = [-1] * (n + 1)
    right = [n] * (n + 1)

    # Fill elements of left[] using logic discussed on
    # https:#www.geeksforgeeks.org/next-greater-element
    for i in range(n):
        while (len(s) != 0 and
               arr[s[-1]] >= arr[i]):
            s.pop()

        if (len(s) != 0):
            left[i] = s[-1]

        s.append(i)

    # Empty the stack as stack is going
    # to be used for right[]
    while (len(s) != 0):
        s.pop()

    # Fill elements of right[] using same logic
    for i in range(n - 1, -1, -1):
        while (len(s) != 0 and arr[s[-1]] >= arr[i]):
            s.pop()

        if(len(s) != 0):
            right[i] = s[-1]

        s.append(i)

    # Create and initialize answer array
    ans = [0] * (n + 1)
    for i in range(n + 1):
        ans[i] = 0

    # Fill answer array by comparing minimums
    # of all. Lengths computed using left[]
    # and right[]
    for i in range(n):

        # Length of the interval
        Len = right[i] - left[i] - 1

        # arr[i] is a possible answer for this
        #  Length 'Len' interval, check if arr[i]
        # is more than max for 'Len'
        ans[Len] = max(ans[Len], arr[i])

    # Some entries in ans[] may not be filled
    # yet. Fill them by taking values from
    # right side of ans[]
    for i in range(n - 1, 0, -1):
        ans[i] = max(ans[i], ans[i + 1])

    # Print the result
    for i in range(1, n + 1):
        print(ans[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [10, 20, 30, 50, 10, 70, 30]
    n = len(arr)
    printMaxOfMin(arr, n)

# This code is contributed by PranchalK
```

## C#

```
// An efficient C# program to find maximum
// of all minimums of windows of different size
using System;
using System.Collections.Generic;

class GFG
{
public static int[] arr = new int[] {10, 20, 30, 50,
                                     10, 70, 30};

public static void printMaxOfMin(int n)
{
    // Used to find previous and next smaller
    Stack<int> s = new Stack<int>();

    // Arrays to store previous
    // and next smaller
    int[] left = new int[n + 1];
    int[] right = new int[n + 1];

    // Initialize elements of left[]
    // and right[]
    for (int i = 0; i < n; i++)
    {
        left[i] = -1;
        right[i] = n;
    }

    // Fill elements of left[] using logic discussed on
    // https://www.geeksforgeeks.org/next-greater-element/
    for (int i = 0; i < n; i++)
    {
        while (s.Count > 0 &&
               arr[s.Peek()] >= arr[i])
        {
            s.Pop();
        }

        if (s.Count > 0)
        {
            left[i] = s.Peek();
        }

        s.Push(i);
    }

    // Empty the stack as stack is going
    // to be used for right[]
    while (s.Count > 0)
    {
        s.Pop();
    }

    // Fill elements of right[] using
    // same logic
    for (int i = n - 1 ; i >= 0 ; i--)
    {
        while (s.Count > 0 &&
               arr[s.Peek()] >= arr[i])
        {
            s.Pop();
        }

        if (s.Count > 0)
        {
            right[i] = s.Peek();
        }

        s.Push(i);
    }

    // Create and initialize answer array
    int[] ans = new int[n + 1];
    for (int i = 0; i <= n; i++)
    {
        ans[i] = 0;
    }

    // Fill answer array by comparing
    // minimums of all lengths computed
    // using left[] and right[]
    for (int i = 0; i < n; i++)
    {
        // length of the interval
        int len = right[i] - left[i] - 1;

        // arr[i] is a possible answer for
        // this length 'len' interval, check x
        // if arr[i] is more than max for 'len'
        ans[len] = Math.Max(ans[len], arr[i]);
    }

    // Some entries in ans[] may not be
    // filled yet. Fill them by taking
    // values from right side of ans[]
    for (int i = n - 1; i >= 1; i--)
    {
        ans[i] = Math.Max(ans[i], ans[i + 1]);
    }

    // Print the result
    for (int i = 1; i <= n; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Driver Code
public static void Main(string[] args)
{
    printMaxOfMin(arr.Length);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // An efficient Javascript program to find maximum
    // of all minimums of windows of different size
    let arr = [10, 20, 30, 50, 10, 70, 30];
    function printMaxOfMin(n)
    {

        // Used to find previous and next smaller
        let s = [];

        // Arrays to store previous
        // and next smaller
        let left = new Array(n + 1);
        left.fill(0);
        let right = new Array(n + 1);
        right.fill(0);

        // Initialize elements of left[]
        // and right[]
        for (let i = 0; i < n; i++)
        {
            left[i] = -1;
            right[i] = n;
        }

        // Fill elements of left[] using logic discussed on
        // https://www.geeksforgeeks.org/next-greater-element/
        for (let i = 0; i < n; i++)
        {
            while (s.length > 0 && arr[s[s.length - 1]] >= arr[i])
            {
                s.pop();
            }

            if (s.length > 0)
            {
                left[i] = s[s.length - 1];
            }

            s.push(i);
        }

        // Empty the stack as stack is going
        // to be used for right[]
        while (s.length > 0)
        {
            s.pop();
        }

        // Fill elements of right[] using
        // same logic
        for (let i = n - 1 ; i >= 0 ; i--)
        {
            while (s.length > 0 && arr[s[s.length - 1]] >= arr[i])
            {
                s.pop();
            }

            if (s.length > 0)
            {
                right[i] = s[s.length - 1];
            }

            s.push(i);
        }

        // Create and initialize answer array
        let ans = new Array(n + 1);
        ans.fill(0);
        for (let i = 0; i <= n; i++)
        {
            ans[i] = 0;
        }

        // Fill answer array by comparing
        // minimums of all lengths computed
        // using left[] and right[]
        for (let i = 0; i < n; i++)
        {

            // length of the interval
            let len = right[i] - left[i] - 1;

            // arr[i] is a possible answer for
            // this length 'len' interval, check x
            // if arr[i] is more than max for 'len'
            ans[len] = Math.max(ans[len], arr[i]);
        }

        // Some entries in ans[] may not be
        // filled yet. Fill them by taking
        // values from right side of ans[]
        for (let i = n - 1; i >= 1; i--)
        {
            ans[i] = Math.max(ans[i], ans[i + 1]);
        }

        // Print the result
        for (let i = 1; i <= n; i++)
        {
            document.write(ans[i] + " ");
        }
    }

    printMaxOfMin(arr.length);

   // This code is contributed by decode2207.
</script>
```

**输出:**

```
70 30 20 10 10 10 10
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    这种方法中的每个子任务都需要线性时间。
*   **辅助空间:** O(n)。
    使用堆栈计算下一个最小值，并使用数组存储中间结果。

本文由[**Ekta Goel**](https://www.linkedin.com/pub/ekta-goel/75/12a/3a6)**Ayush Govil**供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论