# 使用递归对堆栈进行排序

> 原文:[https://www.geeksforgeeks.org/sort-a-stack-using-recursion/](https://www.geeksforgeeks.org/sort-a-stack-using-recursion/)

给定一个堆栈，使用递归对其进行排序。使用任何循环构造，如 while，for..不允许使用 etc。我们只能在堆栈 S 上使用以下 ADT 函数:

```
is_empty(S)  : Tests whether stack is empty or not.
push(S)         : Adds new element to the stack.
pop(S)         : Removes top element from the stack.
top(S)         : Returns value of the top element. Note that this
               function does not remove element from the stack.
```

**示例:**

```
Input:  -3  <--- Top
        14 
        18 
        -5 
        30 

Output: 30  <--- Top
        18 
        14 
        -3 
        -5 
```

这个问题主要是[使用递归](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion)反栈的变体。
解决方案的思想是在函数调用栈中保存所有值，直到栈变空。当堆栈变空时，按排序顺序逐个插入所有保存的项目。在这里，排序很重要。

**算法**
我们可以用下面的算法对栈元素进行排序:

```
sortStack(stack S)
    if stack is not empty:
        temp = pop(S);  
        sortStack(S); 
        sortedInsert(S, temp);
```

下面的算法是对插入元素进行排序的顺序:

```
sortedInsert(Stack S, element)
    if stack is empty OR element > top element
        push(S, elem)
    else
        temp = pop(S)
        sortedInsert(S, element)
        push(S, temp)
```

插图:

```
Let given stack be
-3    <-- top of the stack
14
18
-5
30 
```

让我们用上面的例子来说明堆栈的排序:
首先从堆栈中弹出所有元素，并将弹出的元素存储在变量“temp”中。弹出所有元素后，函数的堆栈框架将如下所示:

```
temp = -3    --> stack frame #1
temp = 14    --> stack frame #2
temp = 18    --> stack frame #3
temp = -5    --> stack frame #4
temp = 30       --> stack frame #5
```

现在堆栈为空，调用“insert_in_sorted_order()”函数，并在堆栈底部插入 30(来自堆栈框架#5)。现在堆栈如下所示:

```
30    <-- top of the stack 
```

现在选择下一个元素，即-5(来自堆栈帧#4)。由于-5 < 30，-5 被插入堆栈的底部。现在堆栈变成:

```
30    <-- top of the stack
-5
```

接下来 18(来自堆栈帧#3)被拾取。因为 18 < 30，所以在 30 以下插入 18。现在堆栈变成:

```
30    <-- top of the stack
18    
-5
```

接下来 14(来自堆栈帧#2)被拾取。由于 14 < 30 和 14 < 18，它被插入到 18 以下。现在堆栈变成:

```
30    <-- top of the stack
18
14    
-5
```

现在-3(来自堆栈帧#1)被拾取，如-3 < 30 和-3 < 18 和-3 < 14，它被插入到 14 以下。现在堆栈变成:

```
30    <-- top of the stack
18
14
-3    
-5
```

**实施:**

下面是上述算法的实现。

## C++

```
// C++ program to sort a stack using recursion
#include <iostream>
using namespace std;

// Stack is represented using linked list
struct stack {
    int data;
    struct stack* next;
};

// Utility function to initialize stack
void initStack(struct stack** s) { *s = NULL; }

// Utility function to check if stack is empty
int isEmpty(struct stack* s)
{
    if (s == NULL)
        return 1;
    return 0;
}

// Utility function to push an item to stack
void push(struct stack** s, int x)
{
    struct stack* p = (struct stack*)malloc(sizeof(*p));

    if (p == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        return;
    }

    p->data = x;
    p->next = *s;
    *s = p;
}

// Utility function to remove an item from stack
int pop(struct stack** s)
{
    int x;
    struct stack* temp;

    x = (*s)->data;
    temp = *s;
    (*s) = (*s)->next;
    free(temp);

    return x;
}

// Function to find top item
int top(struct stack* s) { return (s->data); }

// Recursive function to insert an item x in sorted way
void sortedInsert(struct stack** s, int x)
{
    // Base case: Either stack is empty or newly inserted
    // item is greater than top (more than all existing)
    if (isEmpty(*s) or x > top(*s)) {
        push(s, x);
        return;
    }

    // If top is greater, remove the top item and recur
    int temp = pop(s);
    sortedInsert(s, x);

    // Put back the top item removed earlier
    push(s, temp);
}

// Function to sort stack
void sortStack(struct stack** s)
{
    // If stack is not empty
    if (!isEmpty(*s)) {
        // Remove the top item
        int x = pop(s);

        // Sort remaining stack
        sortStack(s);

        // Push the top item back in sorted stack
        sortedInsert(s, x);
    }
}

// Utility function to print contents of stack
void printStack(struct stack* s)
{
    while (s) {
        cout << s->data << " ";
        s = s->next;
    }
    cout << "\n";
}

// Driver code
int main(void)
{
    struct stack* top;

    initStack(&top);
    push(&top, 30);
    push(&top, -5);
    push(&top, 18);
    push(&top, 14);
    push(&top, -3);

    cout << "Stack elements before sorting:\n";
    printStack(top);

    sortStack(&top);
    cout << "\n";

    cout << "Stack elements after sorting:\n";
    printStack(top);

    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program to sort a stack using recursion
#include <stdio.h>
#include <stdlib.h>

// Stack is represented using linked list
struct stack {
    int data;
    struct stack* next;
};

// Utility function to initialize stack
void initStack(struct stack** s) { *s = NULL; }

// Utility function to check if stack is empty
int isEmpty(struct stack* s)
{
    if (s == NULL)
        return 1;
    return 0;
}

// Utility function to push an item to stack
void push(struct stack** s, int x)
{
    struct stack* p = (struct stack*)malloc(sizeof(*p));

    if (p == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        return;
    }

    p->data = x;
    p->next = *s;
    *s = p;
}

// Utility function to remove an item from stack
int pop(struct stack** s)
{
    int x;
    struct stack* temp;

    x = (*s)->data;
    temp = *s;
    (*s) = (*s)->next;
    free(temp);

    return x;
}

// Function to find top item
int top(struct stack* s) { return (s->data); }

// Recursive function to insert an item x in sorted way
void sortedInsert(struct stack** s, int x)
{
    // Base case: Either stack is empty or newly inserted
    // item is greater than top (more than all existing)
    if (isEmpty(*s) || x > top(*s)) {
        push(s, x);
        return;
    }

    // If top is greater, remove the top item and recur
    int temp = pop(s);
    sortedInsert(s, x);

    // Put back the top item removed earlier
    push(s, temp);
}

// Function to sort stack
void sortStack(struct stack** s)
{
    // If stack is not empty
    if (!isEmpty(*s)) {
        // Remove the top item
        int x = pop(s);

        // Sort remaining stack
        sortStack(s);

        // Push the top item back in sorted stack
        sortedInsert(s, x);
    }
}

// Utility function to print contents of stack
void printStack(struct stack* s)
{
    while (s) {
        printf("%d ", s->data);
        s = s->next;
    }
    printf("\n");
}

// Driver code
int main(void)
{
    struct stack* top;

    initStack(&top);
    push(&top, 30);
    push(&top, -5);
    push(&top, 18);
    push(&top, 14);
    push(&top, -3);

    printf("Stack elements before sorting:\n");
    printStack(top);

    sortStack(&top);
    printf("\n\n");

    printf("Stack elements after sorting:\n");
    printStack(top);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a Stack using recursion
// Note that here predefined Stack class is used
// for stack operation

import java.util.ListIterator;
import java.util.Stack;

class Test
{
    // Recursive Method to insert an item x in sorted way
    static void sortedInsert(Stack<Integer> s, int x)
    {
        // Base case: Either stack is empty or newly
        // inserted item is greater than top (more than all
        // existing)
        if (s.isEmpty() || x > s.peek())
        {
            s.push(x);
            return;
        }

        // If top is greater, remove the top item and recur
        int temp = s.pop();
        sortedInsert(s, x);

        // Put back the top item removed earlier
        s.push(temp);
    }

    // Method to sort stack
    static void sortStack(Stack<Integer> s)
    {
        // If stack is not empty
        if (!s.isEmpty())
        {
            // Remove the top item
            int x = s.pop();

            // Sort remaining stack
            sortStack(s);

            // Push the top item back in sorted stack
            sortedInsert(s, x);
        }
    }

    // Utility Method to print contents of stack
    static void printStack(Stack<Integer> s)
    {
        ListIterator<Integer> lt = s.listIterator();

        // forwarding
        while (lt.hasNext())
            lt.next();

        // printing from top to bottom
        while (lt.hasPrevious())
            System.out.print(lt.previous() + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        Stack<Integer> s = new Stack<>();
        s.push(30);
        s.push(-5);
        s.push(18);
        s.push(14);
        s.push(-3);

        System.out.println(
            "Stack elements before sorting: ");
        printStack(s);

        sortStack(s);

        System.out.println(
            " \n\nStack elements after sorting:");
        printStack(s);
    }
}
```

## 蟒蛇 3

```
# Python program to sort a stack using recursion

# Recursive method to insert element in sorted way

def sortedInsert(s, element):

    # Base case: Either stack is empty or newly inserted
    # item is greater than top (more than all existing)
    if len(s) == 0 or element > s[-1]:
        s.append(element)
        return
    else:

        # Remove the top item and recur
        temp = s.pop()
        sortedInsert(s, element)

        # Put back the top item removed earlier
        s.append(temp)

# Method to sort stack

def sortStack(s):

    # If stack is not empty
    if len(s) != 0:

        # Remove the top item
        temp = s.pop()

        # Sort remaining stack
        sortStack(s)

        # Push the top item back in sorted stack
        sortedInsert(s, temp)

# Printing contents of stack

def printStack(s):
    for i in s[::-1]:
        print(i, end=" ")
    print()

# Driver Code
if __name__ == '__main__':
    s = []
    s.append(30)
    s.append(-5)
    s.append(18)
    s.append(14)
    s.append(-3)

    print("Stack elements before sorting: ")
    printStack(s)

    sortStack(s)

    print("\nStack elements after sorting: ")
    printStack(s)

# This code is contributed by Muskan Kalra.
```

## C#

```
// C# program to sort a Stack using recursion
// Note that here predefined Stack class is used
// for stack operation
using System;
using System.Collections;

public class GFG
{
    // Recursive Method to insert an item x in sorted way
    static void sortedInsert(Stack s, int x)
    {
        // Base case: Either stack is empty or
        // newly inserted item is greater than top
        // (more than all existing)
        if (s.Count == 0 || x > (int)s.Peek()) {
            s.Push(x);
            return;
        }

        // If top is greater, remove
        // the top item and recur
        int temp = (int)s.Peek();
        s.Pop();
        sortedInsert(s, x);

        // Put back the top item removed earlier
        s.Push(temp);
    }

    // Method to sort stack
    static void sortStack(Stack s)
    {
        // If stack is not empty
        if (s.Count > 0) {
            // Remove the top item
            int x = (int)s.Peek();
            s.Pop();

            // Sort remaining stack
            sortStack(s);

            // Push the top item back in sorted stack
            sortedInsert(s, x);
        }
    }

    // Utility Method to print contents of stack
    static void printStack(Stack s)
    {
        foreach(int c in s) { Console.Write(c + " "); }
    }

    // Driver code
    public static void Main(String[] args)
    {
        Stack s = new Stack();
        s.Push(30);
        s.Push(-5);
        s.Push(18);
        s.Push(14);
        s.Push(-3);

        Console.WriteLine(
            "Stack elements before sorting: ");
        printStack(s);

        sortStack(s);

        Console.WriteLine(
            " \n\nStack elements after sorting:");
        printStack(s);
    }
}

// This code is Contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript program to sort a Stack using recursion
// Note that here predefined Stack class is used
// for stack operation

// Recursive Method to insert an item x in sorted way
function sortedInsert(s,x)
{
    // Base case: Either stack is empty or newly
        // inserted item is greater than top (more than all
        // existing)
        if (s.length==0 || x > s[s.length-1])
        {
            s.push(x);
            return;
        }

        // If top is greater, remove the top item and recur
        let temp = s.pop();
        sortedInsert(s, x);

        // Put back the top item removed earlier
        s.push(temp);
}

// Method to sort stack
function sortStack(s)
{
    // If stack is not empty
        if (s.length!=0)
        {
            // Remove the top item
            let x = s.pop();

            // Sort remaining stack
            sortStack(s);

            // Push the top item back in sorted stack
            sortedInsert(s, x);
        }
}

// Utility Method to print contents of stack
function printStack(s)
{
    for(let i=s.length-1;i>=0;i--)
    {
        document.write(s[i]+" ");
    }
    document.write("<br>")
}

 // Driver code   
let s=[];

s.push(30);
s.push(-5);
s.push(18);
s.push(14);
s.push(-3);

document.write(
"Stack elements before sorting: <br>");
printStack(s);

sortStack(s);

document.write(
" <br><br>Stack elements after sorting:<br>");
printStack(s);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Stack elements before sorting:
-3 14 18 -5 30 

Stack elements after sorting:
30 18 14 -3 -5 
```

**复杂度分析:**

*   **时间复杂度:** O(n <sup>2</sup> )。
    在最糟糕的情况下，对于每个 **sortstack()** ，sortedinsert()被递归调用' N '次，以将元素放在正确的位置
*   **辅助空间:** O(N)
    使用堆栈数据结构存储值

**练习:**修改上面的代码，以降序反转堆栈。

本文由纳伦德拉·康拉尔卡尔供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息