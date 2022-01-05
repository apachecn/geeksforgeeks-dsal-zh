# 所有元素相等的最大子矩阵

> 原文:[https://www . geesforgeks . org/最大子矩阵全等元/](https://www.geeksforgeeks.org/largest-sub-matrix-with-all-equal-elements/)

给定大小为 **N * M** 的二进制矩阵，任务是找到面积最大的子矩阵，使其中的所有元素都相同，即要么都是 **0** 要么都是 **1** 。打印这种矩阵的最大可能区域。

**示例:**

> **输入:** mat[][] = {
> {1，1，0，1，0，0，0，0}，
> {0，1，1，1，0，0，1}，
> {1，0，0，1，1，1，0，0}，
> {0，1，1，0，1，0，0}，
> {1，0，1，1，1，1，1，1，0}，
> {0，0，0
> 
> **输入:** mat[][] = {
> {1，0}，
> {0，1}}
> **输出:** 1

**进场:**

1.  尝试寻找所有 **1s** 的最大子矩阵，同样可以应用于寻找所有 **0s** 的最大子矩阵。
2.  维护一个矩阵 **dp[N][M]** ，其中 **dp[i][j]** 代表从 **i <sup>第</sup>T13】行开始到最后一行的 **j <sup>第</sup>列中出现的连续 **1s** 的数量。通过从下到上遍历每一列，可以很容易地填充这个矩阵。****
3.  现在利用以下事实:对于每一行 **i** ， **dp[i][j]** 代表直到第**j**列中最后一行的最大连续 **1s** 。这个问题现在与在[这篇](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)文章中讨论的寻找直方图中存在的最大面积矩形的问题相同。
4.  前面提到的方法必须应用于矩阵的每一行，以找到最大面积子矩阵。

同样的方法也可以用于寻找全为 0 的最大面积子矩阵。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define row 6
#define col 8
using namespace std;

// Function to find the maximum rectangular
// area under given histogram with n bars
int cal(int hist[], int n)
{
    // Create an empty stack. The stack holds indexes
    // of hist[] array. The bars stored in stack are
    // always in increasing order of their heights.
    stack<int> s;

    // Initialize max area
    int max_area = 0;

    // To store top of the stack
    int tp;

    // To store area with top bar
    int area_with_top;
    // as the smallest bar

    // Run through all bars of given histogram
    int i = 0;
    while (i < n) {

        // If this bar is higher than the bar on top
        // stack, push it to stack
        if (s.empty() || hist[s.top()] <= hist[i])
            s.push(i++);

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with stack
        // top as the smallest (or minimum height) bar.
        // 'i' is 'right index' for the top and element
        // before top in stack is 'left index'
        else {

            // Store the top index
            tp = s.top();

            // Pop the top
            s.pop();

            // Calculate the area with hist[tp] stack
            // as smallest bar
            area_with_top = hist[tp]
                            * (s.empty() ? i : i - s.top() - 1);

            // Update max area, if needed
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }

    // Now pop the remaining bars from stack and calculate
    // area with every popped bar as the smallest bar
    while (s.empty() == false) {
        tp = s.top();
        s.pop();
        area_with_top = hist[tp]
                        * (s.empty() ? i : i - s.top() - 1);

        if (max_area < area_with_top)
            max_area = area_with_top;
    }

    return max_area;
}

// Function to find largest sub matrix
// with all equal elements
int largestMatrix(int a[][col])
{
    // To find largest sub matrix
    // with all elements 1
    int dp[row][col];

    // Fill dp[][] by traversing each
    // column from bottom to up
    for (int i = 0; i < col; i++) {
        int cnt = 0;
        for (int j = row - 1; j >= 0; j--) {
            dp[j][i] = 0;
            if (a[j][i] == 1) {
                cnt++;
                dp[j][i] = cnt;
            }
            else {
                cnt = 0;
            }
        }
    }

    int ans = -1;

    for (int i = 0; i < row; i++) {

        // Maintain the histogram array
        int hist[col];
        for (int j = 0; j < col; j++) {
            hist[j] = dp[i][j];
        }

        // Find maximum area rectangle in Histogram
        ans = max(ans, cal(hist, col));
    }

    // To fill dp[][] for finding largest
    // sub matrix with all elements 0
    for (int i = 0; i < col; i++) {
        int cnt = 0;
        for (int j = row - 1; j >= 0; j--) {
            dp[j][i] = 0;
            if (a[j][i] == 0) {
                cnt++;
                dp[j][i] = cnt;
            }
            else {
                cnt = 0;
            }
        }
    }

    for (int i = 0; i < row; i++) {

        // Maintain the histogram array
        int hist[col];
        for (int j = 0; j < col; j++) {
            hist[j] = dp[i][j];
        }

        // Find maximum area rectangle in Histogram
        ans = max(ans, cal(hist, col));
    }

    return ans;
}

// Driver code
int main()
{

    int a[row][col] = { { 1, 1, 0, 1, 0, 0, 0, 0 },
                        { 0, 1, 1, 1, 1, 0, 0, 1 },
                        { 1, 0, 0, 1, 1, 1, 0, 0 },
                        { 0, 1, 1, 0, 1, 1, 0, 0 },
                        { 1, 0, 1, 1, 1, 1, 1, 0 },
                        { 0, 0, 1, 1, 1, 1, 1, 1 } };

    cout << largestMatrix(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int row = 6;
static int col = 8;

// Function to find the maximum rectangular
// area under given histogram with n bars
static int cal(int hist[], int n)
{
    // Create an empty stack. The stack holds indexes
    // of hist[] array. The bars stored in stack are
    // always in increasing order of their heights.
    Stack<Integer> s = new Stack<>();

    // Initialize max area
    int max_area = 0;

    // To store top of the stack
    int tp;

    // To store area with top bar
    int area_with_top;
    // as the smallest bar

    // Run through all bars of given histogram
    int i = 0;
    while (i < n)
    {

        // If this bar is higher than the bar on top
        // stack, push it to stack
        if (s.empty() || hist[s.peek()] <= hist[i])
            s.push(i++);

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with stack
        // top as the smallest (or minimum height) bar.
        // 'i' is 'right index' for the top and element
        // before top in stack is 'left index'
        else
        {

            // Store the top index
            tp = s.peek();

            // Pop the top
            s.pop();

            // Calculate the area with hist[tp] stack
            // as smallest bar
            area_with_top = hist[tp] * (s.empty() ? i :
                                     i - s.peek() - 1);

            // Update max area, if needed
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }

    // Now pop the remaining bars from stack and calculate
    // area with every popped bar as the smallest bar
    while (s.empty() == false)
    {
        tp = s.peek();
        s.pop();
        area_with_top = hist[tp] * (s.empty() ? i :
                                 i - s.peek() - 1);

        if (max_area < area_with_top)
            max_area = area_with_top;
    }
    return max_area;
}

// Function to find largest sub matrix
// with all equal elements
static int largestMatrix(int a[][])
{
    // To find largest sub matrix
    // with all elements 1
    int [][]dp = new int[row][col];

    // Fill dp[][] by traversing each
    // column from bottom to up
    for (int i = 0; i < col; i++)
    {
        int cnt = 0;
        for (int j = row - 1; j >= 0; j--)
        {
            dp[j][i] = 0;
            if (a[j][i] == 1)
            {
                cnt++;
                dp[j][i] = cnt;
            }
            else
            {
                cnt = 0;
            }
        }
    }

    int ans = -1;

    for (int i = 0; i < row; i++)
    {

        // Maintain the histogram array
        int []hist = new int[col];
        for (int j = 0; j < col; j++)
        {
            hist[j] = dp[i][j];
        }

        // Find maximum area rectangle in Histogram
        ans = Math.max(ans, cal(hist, col));
    }

    // To fill dp[][] for finding largest
    // sub matrix with all elements 0
    for (int i = 0; i < col; i++)
    {
        int cnt = 0;
        for (int j = row - 1; j >= 0; j--)
        {
            dp[j][i] = 0;
            if (a[j][i] == 0)
            {
                cnt++;
                dp[j][i] = cnt;
            }
            else
            {
                cnt = 0;
            }
        }
    }

    for (int i = 0; i < row; i++)
    {

        // Maintain the histogram array
        int []hist = new int[col];
        for (int j = 0; j < col; j++)
        {
            hist[j] = dp[i][j];
        }

        // Find maximum area rectangle in Histogram
        ans = Math.max(ans, cal(hist, col));
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[][] = {{ 1, 1, 0, 1, 0, 0, 0, 0 },
                 { 0, 1, 1, 1, 1, 0, 0, 1 },
                 { 1, 0, 0, 1, 1, 1, 0, 0 },
                 { 0, 1, 1, 0, 1, 1, 0, 0 },
                 { 1, 0, 1, 1, 1, 1, 1, 0 },
                 { 0, 0, 1, 1, 1, 1, 1, 1 }};

    System.out.println(largestMatrix(a));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
row = 6
col = 8

# Function to find the maximum rectangular
# area under given histogram with n bars
def cal(hist, n):

    # Create an empty stack. The stack holds indexes
    # of hist[] array. The bars stored in stack are
    # always in increasing order of their heights.
    s = [];

    # Initialize max area
    max_area = 0

    # Run through all bars of given histogram
    i = 0
    while (i < n) :

        # If this bar is higher than the bar on top
        # stack, push it to stack

        if (len(s) == 0 or( hist[s[-1]] <= hist[i])):
            s.append(i)
            i += 1

        # If this bar is lower than top of stack,
        # then calculate area of rectangle with stack
        # top as the smallest (or minimum height) bar.
        # 'i' is 'right index' for the top and element
        # before top in stack is 'left index'
        else :

            # Store the top index
            tp = s[-1]

            # Pop the top
            s.pop()

            # Calculate the area with hist[tp] stack
            # as smallest bar
            if len(s) == 0:
                area_with_top = hist[tp]*i
            else:
                area_with_top = hist[tp]*(i -s[-1] - 1)

            # Update max area, if needed
            if (max_area < area_with_top):
                max_area = area_with_top

    # Now pop the remaining bars from stack and calculate
    # area with every popped bar as the smallest bar
    while (len(s)!=0):
        tp = s[-1]
        s.pop()
        if len(s)==0:
            area_with_top = hist[tp]*i
        else:
            area_with_top = hist[tp]*(i - s[-1] - 1)

        if (max_area < area_with_top):
            max_area = area_with_top

    return max_area

# Function to find largest sub matrix
# with all equal elements
def largestMatrix(a):

    # To find largest sub matrix
    # with all elements 1
    dp = [[ 0 for x in range(col)] for y in range(row)]

    # Fill dp[][] by traversing each
    # column from bottom to up
    for i in range(col):
        cnt = 0
        for j in range( row - 1, -1 ,-1):
            dp[j][i] = 0
            if (a[j][i] == 1) :
                cnt+=1
                dp[j][i] = cnt

            else :
                cnt = 0

        # print("cnt ",cnt)
    ans = -1

    for i in range( row ):

        # Maintain the histogram array
        hist = [0]*col
        for j in range(col):
            hist[j] = dp[i][j]

        # Find maximum area rectangle in Histogram
        ans = max(ans, cal(hist, col))

    # To fill dp[][] for finding largest
    # sub matrix with all elements 0
    for i in range( col):
        cnt = 0
        for j in range( row - 1, -1 ,-1):
            dp[j][i] = 0
            if (a[j][i] == 0):
                cnt +=1
                dp[j][i] = cnt

            else:
                cnt = 0

    for i in range( row) :

        # Maintain the histogram array
        hist = [0]*col
        for j in range(col):
            hist[j] = dp[i][j]

        # Find maximum area rectangle in Histogram
        ans = max(ans, cal(hist, col))

    return ans

# Driver code
if __name__ == "__main__":

    a = [ [1, 1, 0, 1, 0, 0, 0, 0 ],
        [ 0, 1, 1, 1, 1, 0, 0, 1 ],
        [ 1, 0, 0, 1, 1, 1, 0, 0 ],
        [ 0, 1, 1, 0, 1, 1, 0, 0 ],
        [ 1, 0, 1, 1, 1, 1, 1, 0 ],
        [ 0, 0, 1, 1, 1, 1, 1, 1 ]]

    print(largestMatrix(a))

# This code is contributed by chitranayal   
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int row = 6;
static int col = 8;

// Function to find the maximum rectangular
// area under given histogram with n bars
static int cal(int []hist, int n)
{
    // Create an empty stack. The stack holds indexes
    // of hist[] array. The bars stored in stack are
    // always in increasing order of their heights.
    Stack<int> s = new Stack<int>();

    // Initialize max area
    int max_area = 0;

    // To store top of the stack
    int tp;

    // To store area with top bar
    int area_with_top;
    // as the smallest bar

    // Run through all bars of given histogram
    int i = 0;
    while (i < n)
    {

        // If this bar is higher than the bar on top
        // stack, push it to stack
        if (s.Count == 0 || hist[s.Peek()] <= hist[i])
            s.Push(i++);

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with stack
        // top as the smallest (or minimum height) bar.
        // 'i' is 'right index' for the top and element
        // before top in stack is 'left index'
        else
        {

            // Store the top index
            tp = s.Peek();

            // Pop the top
            s.Pop();

            // Calculate the area with hist[tp] stack
            // as smallest bar
            area_with_top = hist[tp] * (s.Count == 0 ? i :
                                        i - s.Peek() - 1);

            // Update max area, if needed
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }

    // Now pop the remaining bars from stack and calculate
    // area with every popped bar as the smallest bar
    while (s.Count == 0 == false)
    {
        tp = s.Peek();
        s.Pop();
        area_with_top = hist[tp] * (s.Count == 0 ? i :
                                    i - s.Peek() - 1);

        if (max_area < area_with_top)
            max_area = area_with_top;
    }
    return max_area;
}

// Function to find largest sub matrix
// with all equal elements
static int largestMatrix(int [,]a)
{
    // To find largest sub matrix
    // with all elements 1
    int [,]dp = new int[row, col];

    // Fill dp[,] by traversing each
    // column from bottom to up
    for (int i = 0; i < col; i++)
    {
        int cnt = 0;
        for (int j = row - 1; j >= 0; j--)
        {
            dp[j, i] = 0;
            if (a[j, i] == 1)
            {
                cnt++;
                dp[j, i] = cnt;
            }
            else
            {
                cnt = 0;
            }
        }
    }

    int ans = -1;

    for (int i = 0; i < row; i++)
    {

        // Maintain the histogram array
        int []hist = new int[col];
        for (int j = 0; j < col; j++)
        {
            hist[j] = dp[i, j];
        }

        // Find maximum area rectangle in Histogram
        ans = Math.Max(ans, cal(hist, col));
    }

    // To fill dp[,] for finding largest
    // sub matrix with all elements 0
    for (int i = 0; i < col; i++)
    {
        int cnt = 0;
        for (int j = row - 1; j >= 0; j--)
        {
            dp[j, i] = 0;
            if (a[j, i] == 0)
            {
                cnt++;
                dp[j, i] = cnt;
            }
            else
            {
                cnt = 0;
            }
        }
    }

    for (int i = 0; i < row; i++)
    {

        // Maintain the histogram array
        int []hist = new int[col];
        for (int j = 0; j < col; j++)
        {
            hist[j] = dp[i, j];
        }

        // Find maximum area rectangle in Histogram
        ans = Math.Max(ans, cal(hist, col));
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int [,]a = {{ 1, 1, 0, 1, 0, 0, 0, 0 },
                { 0, 1, 1, 1, 1, 0, 0, 1 },
                { 1, 0, 0, 1, 1, 1, 0, 0 },
                { 0, 1, 1, 0, 1, 1, 0, 0 },
                { 1, 0, 1, 1, 1, 1, 1, 0 },
                { 0, 0, 1, 1, 1, 1, 1, 1 }};

    Console.WriteLine(largestMatrix(a));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let row = 6;
let col = 8;

// Function to find the maximum rectangular
// area under given histogram with n bars
function cal(hist, n)
{

    // Create an empty stack. The stack holds indexes
    // of hist[] array. The bars stored in stack are
    // always in increasing order of their heights.
    let s = [];

    // Initialize max area
    let max_area = 0;

    // To store top of the stack
    let tp;

    // To store area with top bar
    let area_with_top;

    // as the smallest bar
    // Run through all bars of given histogram
    let i = 0;

    while (i < n)
    {

        // If this bar is higher than the bar on top
        // stack, push it to stack
        if (s.length == 0 ||
     hist[s[s.length - 1]] <= hist[i])
            s.push(i++);

        // If this bar is lower than top of stack,
        // then calculate area of rectangle with stack
        // top as the smallest (or minimum height) bar.
        // 'i' is 'right index' for the top and element
        // before top in stack is 'left index'
        else
        {

            // Store the top index
            tp = s[s.length - 1];

            // Pop the top
            s.pop();

            // Calculate the area with hist[tp] stack
            // as smallest bar
            area_with_top = hist[tp] * (s.length == 0 ? i :
                                   i - s[s.length - 1] - 1);

            // Update max area, if needed
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }

    // Now pop the remaining bars from
    // stack and calculate area with
    // every popped bar as the smallest bar
    while (s.length != 0)
    {
        tp = s[s.length - 1];
        s.pop();
        area_with_top = hist[tp] * (s.length == 0 ? i :
                               i - s[s.length - 1] - 1);

        if (max_area < area_with_top)
            max_area = area_with_top;
    }
    return max_area;
}

// Function to find largest sub matrix
// with all equal elements
function largestMatrix(a)
{

    // To find largest sub matrix
    // with all elements 1
    let dp = new Array(row);
    for(let i = 0; i < row; i++)
    {
        dp[i] = new Array(col);
    }

    // Fill dp[][] by traversing each
    // column from bottom to up
    for(let i = 0; i < col; i++)
    {
        let cnt = 0;
        for(let j = row - 1; j >= 0; j--)
        {
            dp[j][i] = 0;
            if (a[j][i] == 1)
            {
                cnt++;
                dp[j][i] = cnt;
            }
            else
            {
                cnt = 0;
            }
        }
    }

    let ans = -1;

    for(let i = 0; i < row; i++)
    {

        // Maintain the histogram array
        let hist = new Array(col);
        for(let j = 0; j < col; j++)
        {
            hist[j] = dp[i][j];
        }

        // Find maximum area rectangle in Histogram
        ans = Math.max(ans, cal(hist, col));
    }

    // To fill dp[][] for finding largest
    // sub matrix with all elements 0
    for(let i = 0; i < col; i++)
    {
        let cnt = 0;
        for(let j = row - 1; j >= 0; j--)
        {
            dp[j][i] = 0;
            if (a[j][i] == 0)
            {
                cnt++;
                dp[j][i] = cnt;
            }
            else
            {
                cnt = 0;
            }
        }
    }

    for(let i = 0; i < row; i++)
    {

        // Maintain the histogram array
        let hist = new Array(col);
        for(let j = 0; j < col; j++)
        {
            hist[j] = dp[i][j];
        }

        // Find maximum area rectangle in Histogram
        ans = Math.max(ans, cal(hist, col));
    }
    return ans;
}

// Driver code
let a = [ [ 1, 1, 0, 1, 0, 0, 0, 0 ],
          [ 0, 1, 1, 1, 1, 0, 0, 1 ],
          [ 1, 0, 0, 1, 1, 1, 0, 0 ],
          [ 0, 1, 1, 0, 1, 1, 0, 0 ],
          [ 1, 0, 1, 1, 1, 1, 1, 0 ],
          [ 0, 0, 1, 1, 1, 1, 1, 1 ]];

document.write(largestMatrix(a));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
10
```