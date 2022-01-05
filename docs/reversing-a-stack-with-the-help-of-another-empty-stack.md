# 借助另一个空堆栈反转一个堆栈

> 原文:[https://www . geeksforgeeks . org/借助另一个空堆栈反转堆栈/](https://www.geeksforgeeks.org/reversing-a-stack-with-the-help-of-another-empty-stack/)

给定一个由 **N** 元素组成的[堆叠](https://www.geeksforgeeks.org/stack-data-structure/)，任务是使用额外的[堆叠](https://www.geeksforgeeks.org/stack-data-structure/)来反转[堆叠](https://www.geeksforgeeks.org/stack-data-structure/)。

**示例:**

> **输入:**栈= {1，2，3，4，5 }
> T3】输出:T5】1
> 2
> 3
> 4
> 5
> T11】解释:T13】输入栈:
> 5
> 4
> 3
> 2
> 1
> 反转栈:
> 1
> 2
> 3
> 4
> 
> **输入:**堆叠= {1，3，5，4，2}
> **输出:**
> 1
> 3
> 5
> 4
> 2

**方法:**按照以下步骤解决问题:

*   初始化一个空的[栈](https://www.geeksforgeeks.org/stack-data-structure/)。
*   弹出给定堆栈的[顶部元素，并将其存储在临时变量中。](https://www.geeksforgeeks.org/stack-top-c-stl/)
*   将给定堆栈的所有元素转移到上面初始化的堆栈。
*   [将临时变量推入原始堆栈](https://www.geeksforgeeks.org/stack-push-method-in-java/)。
*   将新堆栈中的所有元素转移到原始堆栈中。

下面是上述方法的实现。

## C++

```
// C++ program to reverse a stack
// by using an extra stack
#include <bits/stdc++.h>
using namespace std;

// Function to transfer elements of
// the stack s1 to the stack s2
void transfer(stack<int>& s1,
              stack<int>& s2, int n)
{
    for (int i = 0; i < n; i++) {

        // Store the top element
        // in a temporary variable
        int temp = s1.top();

        // Pop out of the stack
        s1.pop();

        // Push it into s2
        s2.push(temp);
    }
}

// Function to reverse a stack using another stack
void reverse_stack_by_using_extra_stack(stack<int>& s,
                                        int n)
{
    stack<int> s2;

    for (int i = 0; i < n; i++) {

        // Store the top element
        // of the given stack
        int x = s.top();

        // Pop that element
        // out of the stack
        s.pop();

        transfer(s, s2, n - i - 1);
        s.push(x);
        transfer(s2, s, n - i - 1);
    }
}

// Driver Code
int main()
{
    int n = 5;

    stack<int> s;
    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);
    s.push(5);

    reverse_stack_by_using_extra_stack(s, n);

    for (int i = 0; i < n; i++) {
        cout << s.top() << " ";
        s.pop();
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a stack
// by using an extra stack
import java.io.*;
import java.util.*;

class GFG{

// Function to transfer elements of
// the stack s1 to the stack s2
static void transfer(Stack<Integer> s1,
                     Stack<Integer> s2, int n)
{
    for(int i = 0; i < n; i++)
    {

        // Store the top element
        // in a temporary variable
        int temp = s1.peek();

        // Pop out of the stack
        s1.pop();

        // Push it into s2
        s2.push(temp);
    }
}

// Function to reverse a stack using another stack
static void reverse_stack_by_using_extra_stack(Stack<Integer> s,
                                               int n)
{
    Stack<Integer> s2 = new Stack<Integer>();

    for(int i = 0; i < n; i++)
    {

        // Store the top element
        // of the given stack
        int x = s.peek();

        // Pop that element
        // out of the stack
        s.pop();

        transfer(s, s2, n - i - 1);
        s.push(x);
        transfer(s2, s, n - i - 1);
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    Stack<Integer> s = new Stack<Integer>();
    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);
    s.push(5);

    reverse_stack_by_using_extra_stack(s, n);

    for(int i = 0; i < n; i++)
    {
        System.out.print(s.peek() + " ");
        s.pop();
    }
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program to reverse a stack
# by using an extra stack

# Function to transfer elements of
# the stack s1 to the stack s2
def transfer(s1, s2, n):

    for i in range(n):

        # Store the top element
        # in a temporary variable
        temp = s1[-1]

        # Pop out of the stack
        s1.pop()

        # Push it into s2
        s2.append(temp)

# Function to reverse a stack using another stack
def reverse_stack_by_using_extra_stack(s, n):

    s2 = []

    for i in range(n):

        # Store the top element
        # of the given stack
        x = s[-1]

        # Pop that element
        # out of the stack
        s.pop()

        transfer(s, s2, n - i - 1)
        s.append(x)
        transfer(s2, s, n - i - 1)

# Driver Code
if __name__ == "__main__":

    n = 5

    s = []
    s.append(1)
    s.append(2)
    s.append(3)
    s.append(4)
    s.append(5)

    reverse_stack_by_using_extra_stack(s, n)

    for i in range(n):
        print(s[-1], end = " ")
        s.pop()

# This code is contributed by ukasp
```

## C#

```
// C# program to reverse a stack
// by using an extra stack
using System;
using System.Collections.Generic;

class GFG{

// Function to transfer elements of
// the stack s1 to the stack s2
static void transfer(Stack<int> s1,
              Stack<int> s2, int n)
{
    for (int i = 0; i < n; i++) {

        // Store the top element
        // in a temporary variable
        int temp = s1.Peek();

        // Pop out of the stack
        s1.Pop();

        // Push it into s2
        s2.Push(temp);
    }
}

// Function to reverse a stack using another stack
static void reverse_stack_by_using_extra_stack(Stack<int> s,
                                        int n)
{
    Stack<int> s2 = new Stack<int>();

    for (int i = 0; i < n; i++) {

        // Store the top element
        // of the given stack
        int x = s.Peek();

        // Pop that element
        // out of the stack
        s.Pop();

        transfer(s, s2, n - i - 1);
        s.Push(x);
        transfer(s2, s, n - i - 1);
    }
}

// Driver Code
public static void Main()
{
    int n = 5;

    Stack<int> s = new Stack<int>();

    s.Push(1);
    s.Push(2);
    s.Push(3);
    s.Push(4);
    s.Push(5);

    reverse_stack_by_using_extra_stack(s, n);

    for (int i = 0; i < n; i++) {
        Console.Write(s.Peek() + " ");
        s.Pop();
    }
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program to reverse a stack
// by using an extra stack

// Function to transfer elements of
// the stack s1 to the stack s2
function transfer(s1, s2, n)
{
    for (i = 0; i < n; i++) {

        // Store the top element
        // in a temporary variable
        var temp = s1[s1.length-1];

        // Pop out of the stack
        s1.pop();

        // Push it into s2
        s2.push(temp);
    }
}

// Function to reverse a stack using another stack
function reverse_stack_by_using_extra_stack(s,n)
{
    var s2 = [];
    var i;
    for (i = 0; i < n; i++) {

        // Store the top element
        // of the given stack
        var x = s[s.length-1];

        // Pop that element
        // out of the stack
        s.pop();

        transfer(s, s2, n - i - 1);
        s.push(x);
        transfer(s2, s, n - i - 1);
    }
}

// Driver Code
    var n = 5;

    var s = []
    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);
    s.push(5);

    reverse_stack_by_using_extra_stack(s, n);
    var i;
    for (i = 0; i < n; i++) {
        document.write(s[s.length-1] + ' ');
        s.pop();
    }

</script>
```

**Output:** 

```
1 2 3 4 5
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*