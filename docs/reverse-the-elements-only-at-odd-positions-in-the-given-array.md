# 仅在给定数组的奇数位置反转元素

> 原文:[https://www . geeksforgeeks . org/仅在给定数组的奇数位置反转元素/](https://www.geeksforgeeks.org/reverse-the-elements-only-at-odd-positions-in-the-given-array/)

给定一个包含 **N** 整数的**数组 arr[]** ，任务是重新排列数组，使奇数索引元素的顺序相反。

**示例:**

> **输入:** arr[] = {5，7，6，2，9，18，11，15}
> **输出:** {5，15，6，18，9，2，11，7}
> **解释:**
> 偶数索引【5，6，9，11】处的元素不变，奇数索引处的元素从【7，2，18，15】反转为【15，18，2，7】。
> 
> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** {1，6，3，4，5，2}
> **解释:**
> 偶数索引处的元素不变，奇数索引处的元素从[2，4，6]反转为[6，4，2]。

**方法:**要解决上述问题，请遵循以下步骤:

*   将给定数组奇数索引的元素推入 [**堆栈数据结构**](https://www.geeksforgeeks.org/stack-data-structure/) **。**
*   用堆栈顶部的元素替换奇数索引处的当前数组元素，并一直弹出，直到堆栈为空。

**以下是上述方法的实现:**

## C++

```
// C++ program to reverse the
// elements only at odd positions
// in the given Array

#include <bits/stdc++.h>
using namespace std;

// Function to display elements
void show(int arr[], int n)
{
    cout << "{";

    for (int i = 0; i < n - 1; i++)
        cout << arr[i] << ", ";

    cout << arr[n - 1] << "}";
}

// Function to flip elements
// at odd indexes
void flipHalf(int arr[], int n)
{
    int c = 0;
    int dup = n;

    stack<int> st;

    // Pushing elements at odd indexes
    // of a array to a stack
    for (int i = 0; i < n; i++) {
        int x = arr[i];

        if (c % 2 == 1)
            st.push(x);
        c++;
    }

    c = 0;

    // Replacing current elements at odd
    // indexes with element at top of stack
    for (int i = 0; i < n; i++) {
        int x = arr[i];

        if (c % 2 == 1) {
            x = st.top();
            st.pop();
        }
        arr[i] = x;
        c++;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };

    int n = sizeof(arr) / sizeof(arr[0]);

    flipHalf(arr, n);

    show(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse the
// elements only at odd positions
// in the given array
import java.io.*;
import java.util.*;

class GFG {

// Function to count the valley points
// in the given character array
static void show(int arr[], int n)
{
    System.out.print("{");

    for(int i = 0; i < n - 1; i++)
       System.out.print(arr[i] + ", ");

    System.out.print(arr[n - 1] + "}");        
}

// Function to flip elements
// at odd indexes
public static void flipHalf(int arr[], int n)
{
    int c = 0;
    int dup = n;
    Stack<Integer> st = new Stack<>();

    // Pushing elements at odd indexes
    // of a array to a stack
    for(int i = 0; i < n; i++)
    {
       int x = arr[i];

       if (c % 2 == 1)
       {
           st.push(x);
       }
       c++;
    }
    c = 0;

    // Replacing current elements at odd
    // indexes with element at top of stack
    for(int i = 0; i < n; i++)
    {
       int x = arr[i];

       if (c % 2 == 1)
       {
           x = st.peek();
           st.pop();
       }
       arr[i] = x;
       c++;
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = arr.length;

    flipHalf(arr, n);
    show(arr, n);
}    
}

// This code is contributed by Aman Kumar 27
```

## 蟒蛇 3

```
# Python3 program to reverse the
# elements only at odd positions
# in the given Array

# Function to get top of the stack
def peek_stack(stack):

    if stack:
        return stack[-1]

# Function to display elements
def show(arr, n):

    print("{", end = " ")
    for i in range(0, n - 1):
        print(arr[i], ",", end = " ")

    print(arr[n - 1] , "}")

# Function to flip elements
# at odd indexes
def flipHalf(arr, n):

    c = 0
    dup = n
    stack = []

    # Pushing elements at odd indexes
    # of a array to a stack
    for i in range(0, n):
        x = arr[i]

        if c % 2 == 1:
            stack.append(x)

        c = c + 1

    c = 0

    # Replacing current elements at odd
    # indexes with element at top of stack
    for i in range(0, n):
        x = arr[i]

        if c % 2 == 1:
            x = peek_stack(stack)
            stack.pop()

        arr[i] = x
        c = c + 1

# Driver Code
if __name__ == "__main__":

  arr = [ 1, 2, 3, 4, 5, 6 ]
  n = len(arr)

  flipHalf(arr, n)

  show(arr, n)

# This code is contributed by akhilsaini
```

## C#

```
// C# program to reverse the
// elements only at odd positions
// in the given array
using System;
using System.Collections.Generic;

class GFG{

// Function to count the valley points
// in the given character array
static void show(int []arr, int n)
{
    Console.Write("{");

    for(int i = 0; i < n - 1; i++)
    Console.Write(arr[i] + ", ");

    Console.Write(arr[n - 1] + "}");        
}

// Function to flip elements
// at odd indexes
public static void flipHalf(int []arr, int n)
{
    int c = 0;
    int dup = n;
    Stack<int> st = new Stack<int>();

    // Pushing elements at odd indexes
    // of a array to a stack
    for(int i = 0; i < n; i++)
    {
        int x = arr[i];

        if (c % 2 == 1)
        {
            st.Push(x);
        }
        c++;
    }
    c = 0;

    // Replacing current elements at odd
    // indexes with element at top of stack
    for(int i = 0; i < n; i++)
    {
        int x = arr[i];

        if (c % 2 == 1)
        {
            x = st.Peek();
            st.Pop();
        }
        arr[i] = x;
        c++;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6 };
    int n = arr.Length;

    flipHalf(arr, n);
    show(arr, n);
}    
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to reverse the
    // elements only at odd positions
    // in the given Array

    // Function to display elements
    function show(arr, n)
    {
        document.write("{");

        for (let i = 0; i < n - 1; i++)
            document.write(arr[i] + ", ");

        document.write(arr[n - 1] + "}");
    }

    // Function to flip elements
    // at odd indexes
    function flipHalf(arr, n)
    {
        let c = 0;
        let dup = n;

        let st = [];

        // Pushing elements at odd indexes
        // of a array to a stack
        for (let i = 0; i < n; i++) {
            let x = arr[i];

            if (c % 2 == 1)
                st.push(x);
            c++;
        }

        c = 0;

        // Replacing current elements at odd
        // indexes with element at top of stack
        for (let i = 0; i < n; i++) {
            let x = arr[i];

            if (c % 2 == 1) {
                x = st[st.length - 1];
                st.pop();
            }
            arr[i] = x;
            c++;
        }
    }

    let arr = [ 1, 2, 3, 4, 5, 6 ];

    let n = arr.length;

    flipHalf(arr, n);

    show(arr, n);

</script>
```

**Output:** 

```
{1, 6, 3, 4, 5, 2}
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(N/2)*