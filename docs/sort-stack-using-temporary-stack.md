# 使用临时堆栈对堆栈进行排序

> 原文:[https://www . geesforgeks . org/sort-stack-using-暂存-stack/](https://www.geeksforgeeks.org/sort-stack-using-temporary-stack/)

给定一个整数堆栈，使用另一个临时堆栈按升序排序。

**示例:**

```
Input : [34, 3, 31, 98, 92, 23]
Output : [3, 23, 31, 34, 92, 98]

Input : [3, 5, 1, 4, 2, 8]
Output : [1, 2, 3, 4, 5, 8] 
```

我们遵循这个算法。

1.  创建一个临时堆栈，比如 **tmpStack** 。
2.  当输入堆栈不为空时，执行以下操作:
    *   从输入堆栈中弹出一个元素，称之为**温度**
    *   当临时堆栈不为空且临时堆栈顶部大于临时堆栈时，
        从临时堆栈弹出并将其推入输入堆栈
    *   将**温度**推入临时堆栈
3.  排序后的数字在 tmpStack 中

这里是上面伪代码的一个模拟运行。

```
input: [34, 3, 31, 98, 92, 23]

Element taken out: 23
input: [34, 3, 31, 98, 92]
tmpStack: [23]

Element taken out: 92
input: [34, 3, 31, 98]
tmpStack: [23, 92]

Element taken out: 98
input: [34, 3, 31]
tmpStack: [23, 92, 98]

Element taken out: 31
input: [34, 3, 98, 92]
tmpStack: [23, 31]

Element taken out: 92
input: [34, 3, 98]
tmpStack: [23, 31, 92]

Element taken out: 98
input: [34, 3]
tmpStack: [23, 31, 92, 98]

Element taken out: 3
input: [34, 98, 92, 31, 23]
tmpStack: [3]

Element taken out: 23
input: [34, 98, 92, 31]
tmpStack: [3, 23]

Element taken out: 31
input: [34, 98, 92]
tmpStack: [3, 23, 31]

Element taken out: 92
input: [34, 98]
tmpStack: [3, 23, 31, 92]

Element taken out: 98
input: [34]
tmpStack: [3, 23, 31, 92, 98]

Element taken out: 34
input: [98, 92]
tmpStack: [3, 23, 31, 34]

Element taken out: 92
input: [98]
tmpStack: [3, 23, 31, 34, 92]

Element taken out: 98
input: []
tmpStack: [3, 23, 31, 34, 92, 98]

final sorted list: [3, 23, 31, 34, 92, 98]
```

## C++

```
// C++ program to sort a stack using an
// auxiliary stack.
#include <bits/stdc++.h>
using namespace std;

// This function return the sorted stack
stack<int> sortStack(stack<int> &input)
{
    stack<int> tmpStack;

    while (!input.empty())
    {
        // pop out the first element
        int tmp = input.top();
        input.pop();

        // while temporary stack is not empty and top
        // of stack is greater than temp
        while (!tmpStack.empty() && tmpStack.top() > tmp)
        {
            // pop from temporary stack and push
            // it to the input stack
            input.push(tmpStack.top());
            tmpStack.pop();
        }

        // push temp in temporary of stack
        tmpStack.push(tmp);
    }

    return tmpStack;
}

// main function
int main()
{
    stack<int> input;
    input.push(34);
    input.push(3);
    input.push(31);
    input.push(98);
    input.push(92);
    input.push(23);

    // This is the temporary stack
    stack<int> tmpStack = sortStack(input);
    cout << "Sorted numbers are:\n";

    while (!tmpStack.empty())
    {
        cout << tmpStack.top()<< " ";
        tmpStack.pop();
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a stack using
// a auxiliary stack.
import java.util.*;

class SortStack
{
    // This function return the sorted stack
    public static Stack<Integer> sortstack(Stack<Integer>
                                             input)
    {
        Stack<Integer> tmpStack = new Stack<Integer>();
        while(!input.isEmpty())
        {
            // pop out the first element
            int tmp = input.pop();

            // while temporary stack is not empty and
            // top of stack is greater than temp
            while(!tmpStack.isEmpty() && tmpStack.peek()
                                                 > tmp)
            {
                // pop from temporary stack and
                // push it to the input stack
            input.push(tmpStack.pop());
            }

            // push temp in temporary of stack
            tmpStack.push(tmp);
        }
        return tmpStack;
    }

    // Driver Code
    public static void main(String args[])
    {
        Stack<Integer> input = new Stack<Integer>();
        input.add(34);
        input.add(3);
        input.add(31);
        input.add(98);
        input.add(92);
        input.add(23);

        // This is the temporary stack
        Stack<Integer> tmpStack=sortstack(input);
        System.out.println("Sorted numbers are:");

        while (!tmpStack.empty())
        {
            System.out.print(tmpStack.pop()+" ");
        }
    }
}
// This code is contributed by Danish Kaleem
```

## 蟒蛇 3

```
# Python program to sort a
# stack using auxiliary stack.

# This function return the sorted stack
def sortStack ( stack ):
    tmpStack = createStack()
    while(isEmpty(stack) == False):

        # pop out the first element
        tmp = top(stack)
        pop(stack)

        # while temporary stack is not
        # empty and top of stack is
        # greater than temp
        while(isEmpty(tmpStack) == False and
             int(top(tmpStack)) > int(tmp)):

            # pop from temporary stack and
            # push it to the input stack
            push(stack,top(tmpStack))
            pop(tmpStack)

        # push temp in temporary of stack
        push(tmpStack,tmp)

    return tmpStack

# Below is a complete running
# program for testing above
# function.

# Function to create a stack.
# It initializes size of stack
# as 0
def createStack():
    stack = []
    return stack

# Function to check if
# the stack is empty
def isEmpty( stack ):
    return len(stack) == 0

# Function to push an
# item to stack
def push( stack, item ):
    stack.append( item )

# Function to get top
# item of stack
def top( stack ):
    p = len(stack)
    return stack[p-1]

# Function to pop an
# item from stack
def pop( stack ):

    # If stack is empty
    # then error
    if(isEmpty( stack )):
        print("Stack Underflow ")
        exit(1)

    return stack.pop()

# Function to print the stack
def prints(stack):
    for i in range(len(stack)-1, -1, -1):
        print(stack[i], end = ' ')
    print()

# Driver Code
stack = createStack()
push( stack, str(34) )
push( stack, str(3) )
push( stack, str(31) )
push( stack, str(98) )
push( stack, str(92) )
push( stack, str(23) )

print("Sorted numbers are: ")
sortedst = sortStack ( stack )
prints(sortedst)

# This code is contributed by
# Prasad Kshirsagar
```

## C#

```
// C# program to sort a stack using
// a auxiliary stack.
using System;
using System.Collections.Generic;

class GFG
{
// This function return the sorted stack
public static Stack<int> sortstack(Stack<int> input)
{
    Stack<int> tmpStack = new Stack<int>();
    while (input.Count > 0)
    {
        // pop out the first element
        int tmp = input.Pop();

        // while temporary stack is not empty and
        // top of stack is greater than temp
        while (tmpStack.Count > 0 && tmpStack.Peek() > tmp)
        {
            // pop from temporary stack and
            // push it to the input stack
            input.Push(tmpStack.Pop());
        }

        // push temp in temporary of stack
        tmpStack.Push(tmp);
    }
    return tmpStack;
}

// Driver Code
public static void Main(string[] args)
{
    Stack<int> input = new Stack<int>();
    input.Push(34);
    input.Push(3);
    input.Push(31);
    input.Push(98);
    input.Push(92);
    input.Push(23);

    // This is the temporary stack
    Stack<int> tmpStack = sortstack(input);
    Console.WriteLine("Sorted numbers are:");

    while (tmpStack.Count > 0)
    {
        Console.Write(tmpStack.Pop() + " ");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to sort a stack using
    // a auxiliary stack.

    // This function return the sorted stack
    function sortstack(input)
    {
        let tmpStack = [];
        while (input.length > 0)
        {
            // pop out the first element
            let tmp = input.pop();

            // while temporary stack is not empty and
            // top of stack is greater than temp
            while (tmpStack.length > 0 && tmpStack[tmpStack.length - 1] > tmp)
            {
                // pop from temporary stack and
                // push it to the input stack
                input.push(tmpStack[tmpStack.length - 1]);
                tmpStack.pop()
            }

            // push temp in temporary of stack
            tmpStack.push(tmp);
        }
        return tmpStack;
    }

    let input = [];
    input.push(34);
    input.push(3);
    input.push(31);
    input.push(98);
    input.push(92);
    input.push(23);

    // This is the temporary stack
    let tmpStack = sortstack(input);
    document.write("Sorted numbers are:" + "</br>");

    while (tmpStack.length > 0)
    {
        document.write(tmpStack[tmpStack.length - 1] + " ");
        tmpStack.pop();
    }

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Sorted numbers are:
98 92 34 31 23 3
```

Microsoft

本文由**阿迪蒂亚·尼哈尔·库马尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。