# 全为 1 的最大尺寸矩形二进制子矩阵

> 原文： [https://www.geeksforgeeks.org/maximum-size-rectangle-binary-sub-matrix-1s/](https://www.geeksforgeeks.org/maximum-size-rectangle-binary-sub-matrix-1s/)

给定一个二进制矩阵，找到最大大小为 1 的矩形二元子矩阵。

**例如**：

```
Input:
0 1 1 0
1 1 1 1
1 1 1 1
1 1 0 0
Output :
1 1 1 1
1 1 1 1
Explanation : 
The largest rectangle with only 1's is from 
(1, 0) to (2, 3) which is
1 1 1 1
1 1 1 1 

Input:
0 1 1
1 1 1
0 1 1      
Output:
1 1
1 1
1 1
Explanation : 
The largest rectangle with only 1's is from 
(0, 1) to (2, 2) which is
1 1
1 1
1 1

```



已经有一种算法讨论了一种用于寻找 1s 的最大平方的基于[动态规划的解决方案](https://www.geeksforgeeks.org/maximum-size-sub-matrix-with-all-1s-in-a-binary-matrix/)。

**方法**：在本文中讨论了一种有趣的方法，该方法将直方图下的[最大矩形用作子例程。

如果给出直方图的条形高度，则可以找到直方图的最大面积。 这样，在每一行中，可以找到直方图的最大条形区域。 要使最大的矩形充满 1，请在上一行的基础上更新下一行，并找到[直方图下最大的面积](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)，即，将每个 1 填充为正方形，将 0 填充为一个空正方形，并以每行为基础。

**示例**：

```
Input :
0 1 1 0
1 1 1 1
1 1 1 1
1 1 0 0
Step 1: 
    0 1 1 0  maximum area  = 2
Step 2:
    row 1  1 2 2 1  area = 4, maximum area becomes 4
    row 2  2 3 3 2  area = 8, maximum area becomes 8
    row 3  3 4 0 0  area = 6, maximum area remains 8

```

**算法**：

1.  运行循环以遍历各行。

2.  现在，如果当前行不是第一行，则按如下方式更新该行，如果`matrix[i][j]`不为零，则 `matrix[i][j] = matrix[i-1][j] + matrix[i][j]`。

3.  找到直方图下方的最大矩形区域，将第`i`行视为直方图的条形高度。 可以按照本文给出的方法进行计算。[直方图中的最大矩形面积](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)。

4.  对所有行执行前两个步骤，并打印所有行的最大面积。

**注**：强烈建议首先参考此帖子，因为那里的大多数代码都来自此。

**实现**：

## C++

```
// C++ program to find largest rectangle with all 1s 
// in a binary matrix 
#include <bits/stdc++.h> 
using namespace std; 
  
// Rows and columns in input matrix 
#define R 4 
#define C 4 
  
// Finds the maximum area under the histogram represented 
// by histogram.  See below article for details. 
// https:// www.geeksforgeeks.org/largest-rectangle-under-histogram/ 
int maxHist(int row[]) 
{ 
    // Create an empty stack. The stack holds indexes of 
    // hist[] array/ The bars stored in stack are always 
    // in increasing order of their heights. 
    stack<int> result; 
  
    int top_val; // Top of stack 
  
    int max_area = 0; // Initialize max area in current 
    // row (or histogram) 
  
    int area = 0; // Initialize area with current top 
  
    // Run through all bars of given histogram (or row) 
    int i = 0; 
    while (i < C) { 
        // If this bar is higher than the bar on top stack, 
        // push it to stack 
        if (result.empty() || row[result.top()] <= row[i]) 
            result.push(i++); 
  
        else { 
            // If this bar is lower than top of stack, then 
            // calculate area of rectangle with stack top as 
            // the smallest (or minimum height) bar. 'i' is 
            // 'right index' for the top and element before 
            // top in stack is 'left index' 
            top_val = row[result.top()]; 
            result.pop(); 
            area = top_val * i; 
  
            if (!result.empty()) 
                area = top_val * (i - result.top() - 1); 
            max_area = max(area, max_area); 
        } 
    } 
  
    // Now pop the remaining bars from stack and calculate area 
    // with every popped bar as the smallest bar 
    while (!result.empty()) { 
        top_val = row[result.top()]; 
        result.pop(); 
        area = top_val * i; 
        if (!result.empty()) 
            area = top_val * (i - result.top() - 1); 
  
        max_area = max(area, max_area); 
    } 
    return max_area; 
} 
  
// Returns area of the largest rectangle with all 1s in A[][] 
int maxRectangle(int A[][C]) 
{ 
    // Calculate area for first row and initialize it as 
    // result 
    int result = maxHist(A[0]); 
  
    // iterate over row to find maximum rectangular area 
    // considering each row as histogram 
    for (int i = 1; i < R; i++) { 
  
        for (int j = 0; j < C; j++) 
  
            // if A[i][j] is 1 then add A[i -1][j] 
            if (A[i][j]) 
                A[i][j] += A[i - 1][j]; 
  
        // Update result if area with current row (as last row) 
        // of rectangle) is more 
        result = max(result, maxHist(A[i])); 
    } 
  
    return result; 
} 
  
// Driver code 
int main() 
{ 
    int A[][C] = { 
        { 0, 1, 1, 0 }, 
        { 1, 1, 1, 1 }, 
        { 1, 1, 1, 1 }, 
        { 1, 1, 0, 0 }, 
    }; 
  
    cout << "Area of maximum rectangle is "
         << maxRectangle(A); 
  
    return 0; 
}
```

## Java

```
// Java program to find largest rectangle with all 1s 
// in a binary matrix 
import java.io.*; 
import java.util.*; 
  
class GFG { 
    // Finds the maximum area under the histogram represented 
    // by histogram.  See below article for details. 
    // https:// www.geeksforgeeks.org/largest-rectangle-under-histogram/ 
    static int maxHist(int R, int C, int row[]) 
    { 
        // Create an empty stack. The stack holds indexes of 
        // hist[] array/ The bars stored in stack are always 
        // in increasing order of their heights. 
        Stack<Integer> result = new Stack<Integer>(); 
  
        int top_val; // Top of stack 
  
        int max_area = 0; // Initialize max area in current 
        // row (or histogram) 
  
        int area = 0; // Initialize area with current top 
  
        // Run through all bars of given histogram (or row) 
        int i = 0; 
        while (i < C) { 
            // If this bar is higher than the bar on top stack, 
            // push it to stack 
            if (result.empty() || row[result.peek()] <= row[i]) 
                result.push(i++); 
  
            else { 
                // If this bar is lower than top of stack, then 
                // calculate area of rectangle with stack top as 
                // the smallest (or minimum height) bar. 'i' is 
                // 'right index' for the top and element before 
                // top in stack is 'left index' 
                top_val = row[result.peek()]; 
                result.pop(); 
                area = top_val * i; 
  
                if (!result.empty()) 
                    area = top_val * (i - result.peek() - 1); 
                max_area = Math.max(area, max_area); 
            } 
        } 
  
        // Now pop the remaining bars from stack and calculate 
        // area with every popped bar as the smallest bar 
        while (!result.empty()) { 
            top_val = row[result.peek()]; 
            result.pop(); 
            area = top_val * i; 
            if (!result.empty()) 
                area = top_val * (i - result.peek() - 1); 
  
            max_area = Math.max(area, max_area); 
        } 
        return max_area; 
    } 
  
    // Returns area of the largest rectangle with all 1s in 
    // A[][] 
    static int maxRectangle(int R, int C, int A[][]) 
    { 
        // Calculate area for first row and initialize it as 
        // result 
        int result = maxHist(R, C, A[0]); 
  
        // iterate over row to find maximum rectangular area 
        // considering each row as histogram 
        for (int i = 1; i < R; i++) { 
  
            for (int j = 0; j < C; j++) 
  
                // if A[i][j] is 1 then add A[i -1][j] 
                if (A[i][j] == 1) 
                    A[i][j] += A[i - 1][j]; 
  
            // Update result if area with current row (as last 
            // row of rectangle) is more 
            result = Math.max(result, maxHist(R, C, A[i])); 
        } 
  
        return result; 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int R = 4; 
        int C = 4; 
  
        int A[][] = { 
            { 0, 1, 1, 0 }, 
            { 1, 1, 1, 1 }, 
            { 1, 1, 1, 1 }, 
            { 1, 1, 0, 0 }, 
        }; 
        System.out.print("Area of maximum rectangle is " + maxRectangle(R, C, A)); 
    } 
} 
  
// Contributed by Prakriti Gupta
```

## Python3

```
# Python3 program to find largest rectangle  
# with all 1s in a binary matrix  
  
# Rows and columns in input matrix  
R = 4
C = 4
  
# Finds the maximum area under the histogram represented  
# by histogram. See below article for details.  
# https:# www.geeksforgeeks.org / largest-rectangle-under-histogram / def maxHist(row): 
  
    # Create an empty stack. The stack holds  
    # indexes of hist array / The bars stored   
    # in stack are always in increasing order  
    # of their heights.  
    result = [] 
  
    top_val = 0     # Top of stack  
  
    max_area = 0 # Initialize max area in current  
                 # row (or histogram)  
  
    area = 0 # Initialize area with current top  
  
    # Run through all bars of given 
    # histogram (or row)  
    i = 0
    while (i < C):  
      
        # If this bar is higher than the  
        # bar on top stack, push it to stack  
        if (len(result) == 0) or (row[result[0]] <= row[i]): 
            result.append(i) 
            i += 1
        else: 
          
            # If this bar is lower than top of stack,  
            # then calculate area of rectangle with  
            # stack top as the smallest (or minimum  
            # height) bar. 'i' is 'right index' for  
            # the top and element before top in stack 
            # is 'left index'  
            top_val = row[result[0]]  
            result.pop(0)  
            area = top_val * i  
  
            if (len(result)): 
                area = top_val * (i - result[0] - 1 )  
            max_area = max(area, max_area)  
          
    # Now pop the remaining bars from stack  
    # and calculate area with every popped 
    # bar as the smallest bar  
    while (len(result)): 
        top_val = row[result[0]]  
        result.pop(0)  
        area = top_val * i  
        if (len(result)):  
            area = top_val * (i - result[0] - 1 )  
  
        max_area = max(area, max_area)  
      
    return max_area  
  
# Returns area of the largest rectangle  
# with all 1s in A  
def maxRectangle(A): 
      
    # Calculate area for first row and  
    # initialize it as result  
    result = maxHist(A[0])  
  
    # iterate over row to find maximum rectangular  
    # area considering each row as histogram  
    for i in range(1, R): 
      
        for j in range(C): 
  
            # if A[i][j] is 1 then add A[i -1][j]  
            if (A[i][j]): 
                A[i][j] += A[i - 1][j]  
  
        # Update result if area with current  
        # row (as last row) of rectangle) is more  
        result = max(result, maxHist(A[i]))  
      
    return result  
      
# Driver Code  
if __name__ == '__main__': 
    A = [[0, 1, 1, 0], 
         [1, 1, 1, 1],  
         [1, 1, 1, 1],  
         [1, 1, 0, 0]]  
  
    print("Area of maximum rectangle is",  
                         maxRectangle(A)) 
      
# This code is contributed  
# by SHUBHAMSINGH10
```

## C#

```
// C# program to find largest rectangle 
// with all 1s in a binary matrix 
using System; 
using System.Collections.Generic; 
  
class GFG { 
    // Finds the maximum area under the 
    // histogram represented by histogram. 
    // See below article for details. 
    // https:// www.geeksforgeeks.org/largest-rectangle-under-histogram/ 
    public static int maxHist(int R, int C, 
                              int[] row) 
    { 
        // Create an empty stack. The stack 
        // holds indexes of hist[] array. 
        // The bars stored in stack are always 
        // in increasing order of their heights. 
        Stack<int> result = new Stack<int>(); 
  
        int top_val; // Top of stack 
  
        int max_area = 0; // Initialize max area in 
        // current row (or histogram) 
  
        int area = 0; // Initialize area with 
        // current top 
  
        // Run through all bars of 
        // given histogram (or row) 
        int i = 0; 
        while (i < C) { 
            // If this bar is higher than the 
            // bar on top stack, push it to stack 
            if (result.Count == 0 || row[result.Peek()] <= row[i]) { 
                result.Push(i++); 
            } 
  
            else { 
                // If this bar is lower than top 
                // of stack, then calculate area of 
                // rectangle with stack top as 
                // the smallest (or minimum height) 
                // bar. 'i' is 'right index' for 
                // the top and element before 
                // top in stack is 'left index' 
                top_val = row[result.Peek()]; 
                result.Pop(); 
                area = top_val * i; 
  
                if (result.Count > 0) { 
                    area = top_val * (i - result.Peek() - 1); 
                } 
                max_area = Math.Max(area, max_area); 
            } 
        } 
  
        // Now pop the remaining bars from 
        // stack and calculate area with 
        // every popped bar as the smallest bar 
        while (result.Count > 0) { 
            top_val = row[result.Peek()]; 
            result.Pop(); 
            area = top_val * i; 
            if (result.Count > 0) { 
                area = top_val * (i - result.Peek() - 1); 
            } 
  
            max_area = Math.Max(area, max_area); 
        } 
        return max_area; 
    } 
  
    // Returns area of the largest 
    // rectangle with all 1s in A[][] 
    public static int maxRectangle(int R, int C, 
                                   int[][] A) 
    { 
        // Calculate area for first row 
        // and initialize it as result 
        int result = maxHist(R, C, A[0]); 
  
        // iterate over row to find 
        // maximum rectangular area 
        // considering each row as histogram 
        for (int i = 1; i < R; i++) { 
            for (int j = 0; j < C; j++) { 
  
                // if A[i][j] is 1 then 
                // add A[i -1][j] 
                if (A[i][j] == 1) { 
                    A[i][j] += A[i - 1][j]; 
                } 
            } 
  
            // Update result if area with current 
            // row (as last row of rectangle) is more 
            result = Math.Max(result, maxHist(R, C, A[i])); 
        } 
  
        return result; 
    } 
  
    // Driver code 
    public static void Main(string[] args) 
    { 
        int R = 4; 
        int C = 4; 
  
        int[][] A = new int[][] { 
            new int[] { 0, 1, 1, 0 }, 
            new int[] { 1, 1, 1, 1 }, 
            new int[] { 1, 1, 1, 1 }, 
            new int[] { 1, 1, 0, 0 } 
        }; 
        Console.Write("Area of maximum rectangle is " + maxRectangle(R, C, A)); 
    } 
} 
  
// This code is contributed by Shrikant13
```

输出：

```
Area of maximum rectangle is 8
```

复杂度分析：

+   时间复杂度：`O(R x C)`。

    矩阵只需要遍历一次，因此时间复杂度为`O(R X C)`。

+   空间复杂度：`O(C)`。

    需要使用堆栈来存储列，因此空间复杂度为`O(C)`。