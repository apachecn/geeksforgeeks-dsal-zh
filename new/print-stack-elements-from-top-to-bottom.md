# 从顶部到底部打印栈元素

> 原文：[https://www.geeksforgeeks.org/print-stack-elements-from-top-to-bottom/](https://www.geeksforgeeks.org/print-stack-elements-from-top-to-bottom/)

给定[栈](http://www.geeksforgeeks.org/stack-data-structure/)`S`，任务是[从上至下打印栈的元素](https://www.geeksforgeeks.org/print-stack-elements-from-bottom-to-top/)，以使元素仍然存在于栈中，而不改变它们的顺序。

**示例**：

> **输入**：`S = {2, 3, 4, 5}`
>
> **输出**：`5 4 3 2`
> 
> **输入**：`S = {3, 3, 2, 2}`
>
> **输出**：`2 2 3 3`

[**递归方法**](http://www.geeksforgeeks.org/recursion/)：请按照以下步骤解决问题：

1.  创建一个具有[栈](https://www.geeksforgeeks.org/stack-data-structure/)作为参数的递归函数。

2.  添加基本​​条件，如果**栈**为空，则从函数返回。

3.  否则，将顶部元素存储在某个变量`X`中，然后将其删除。

4.  打印`X`，调用递归函数并在其中传递相同的栈。

5.  将存储的`X`推回栈。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print stack elements
// from top to bottom with the
// order of elements unaltered
void PrintStack(stack<int> s)
{
    // If stack is empty
    if (s.empty())
        return;

// Extract top of the stack
    int x = s.top();

    // Pop the top element
    s.pop();

    // Print the current top
    // of the stack i.e., x
    cout << x << ' ';

    // Proceed to print
// remaining stack
    PrintStack(s);

    // Push the element back
    s.push(x);
}

// Driver Code
int main()
{
    stack<int> s;

    // Given stack s
    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);

    // Function Call
    PrintStack(s);

    return 0;
}

```

## Java

```java

// Java program for the above approach 
import java.util.*;

class GFG{

// Function to print stack elements 
// from top to bottom with the 
// order of elements unaltered 
public static void PrintStack(Stack<Integer> s) 
{ 

    // If stack is empty 
    if (s.empty()) 
        return; 

    // Extract top of the stack 
    int x = s.peek(); 

    // Pop the top element 
    s.pop(); 

    // Print the current top 
    // of the stack i.e., x 
    System.out.print(x + " ");

    // Proceed to print 
    // remaining stack 
    PrintStack(s); 

    // Push the element back 
    s.push(x); 
} 

// Driver code
public static void main(String[] args) 
{
    Stack<Integer> s = new Stack<Integer>(); 

    // Given stack s 
    s.push(1); 
    s.push(2); 
    s.push(3); 
    s.push(4); 

    // Function call 
    PrintStack(s); 
}
}

// This code is contributed divyeshrabadiya07

```

## Python3

```py

# Python3 program for the 
# above approach
from queue import LifoQueue

# Function to prstack elements
# from top to bottom with the
# order of elements unaltered
def PrintStack(s):

    # If stack is empty
    if (s.empty()):
        return;

    # Extract top of the 
    # stack
    x = s.get();

    # Pop the top element
    #s.pop();

    # Print current top
    # of the stack i.e., x
    print(x, end = " ");

    # Proceed to print
    # remaining stack
    PrintStack(s);

    # Push the element 
    # back
    s.put(x);

# Driver code
if __name__ == '__main__':

    s = LifoQueue();

    # Given stack s
    s.put(1);
    s.put(2);
    s.put(3);
    s.put(4);

    # Function call
    PrintStack(s);

# This code is contributed by Amit Katiyar

```

## C#

```cs

// C# program for 
// the above approach 
using System;
using System.Collections.Generic;
class GFG{

// Function to print stack elements 
// from top to bottom with the 
// order of elements unaltered 
public static void PrintStack(Stack<int> s) 
{ 
  // If stack is empty 
  if (s.Count == 0) 
    return; 

  // Extract top of the stack 
  int x = s.Peek(); 

  // Pop the top element 
  s.Pop(); 

  // Print the current top 
  // of the stack i.e., x 
  Console.Write(x + " ");

  // Proceed to print 
  // remaining stack 
  PrintStack(s); 

  // Push the element back 
  s.Push(x); 
} 

// Driver code
public static void Main(String[] args) 
{
  Stack<int> s = new Stack<int>(); 

  // Given stack s 
  s.Push(1); 
  s.Push(2); 
  s.Push(3); 
  s.Push(4); 

  // Function call 
  PrintStack(s); 
}
}

// This code is contributed by Rajput-Ji

```

**输出**：

```
4 3 2 1 

```

**时间复杂度**：`O(n)`，其中`N`是给定栈中元素的数量。

**辅助空间**：`O(n)`

[**单链表栈方法**](https://www.geeksforgeeks.org/implement-a-stack-using-singly-linked-list/)：此方法讨论解决[单链表栈](https://www.geeksforgeeks.org/implement-a-stack-using-singly-linked-list/)表示法的问题的解决方案。 步骤如下：

1.  将给定栈中的顶部元素推入[链表栈](https://www.geeksforgeeks.org/implement-a-stack-using-singly-linked-list/)。

2.  打印[单链表栈](https://www.geeksforgeeks.org/implement-a-stack-using-singly-linked-list/)的顶部元素。

3.  从给定的主栈中弹出顶部元素。

4.  按顺序重复上述步骤，直到给定的栈为空。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach

import static java.lang.System.exit;

// Create Stack Using Linked list
class StackUsingLinkedlist {

    // A linked list node
    private class Node {
        int data;
        Node link;
    }

    // Reference variable
    Node top;

    // Constructor
    StackUsingLinkedlist()
    {
        this.top = null;
    }

    // Function to add an element x
    // in the stack by inserting
    // at the beginning of LL
    public void push(int x)
    {
        // Create new node temp
        Node temp = new Node();

        // If stack is full
        if (temp == null) {
            System.out.print("\nHeap Overflow");
            return;
        }

        // Initialize data into temp
        temp.data = x;

        // Reference into temp link
        temp.link = top;

        // Update top reference
        top = temp;
    }

    // Function to check if the stack
    // is empty or not
    public boolean isEmpty()
    {
        return top == null;
    }

    // Function to return top element
    // in a stack
    public int peek()
    {
        // Check for empty stack
        if (!isEmpty()) {

            // Return the top data
            return top.data;
        }

        // Otherwise stack is empty
        else {
            System.out.println("Stack is empty");
            return -1;
        }
    }

    // Function to pop top element from
    // the stack by removing element
    // at the beginning
    public void pop()
    {
        // Check for stack underflow
        if (top == null) {
            System.out.print("\nStack Underflow");
            return;
        }

        // Update the top pointer to
        // point to the next node
        top = (top).link;
    }

    // Function to print the elements and
    // restore the stack
    public static void
    DisplayStack(StackUsingLinkedlist s)
    {
        // Create another stack
        StackUsingLinkedlist s1
            = new StackUsingLinkedlist();

        // Until stack is empty
        while (!s.isEmpty()) {
            s1.push(s.peek());

            // Print the element
            System.out.print(s1.peek()
                             + " ");
            s.pop();
        }
    }
}

// Driver Code
public class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        // Create Object of class
        StackUsingLinkedlist obj
            = new StackUsingLinkedlist();

        // Insert Stack value
        obj.push(1);
        obj.push(2);
        obj.push(3);
        obj.push(4);

        // Function Call
        obj.DisplayStack(obj);
    }
}

```

## C#

```cs

// C# program for the above approach
using System;

// Create Stack Using Linked list
class StackUsingLinkedlist{

// A linked list node
public class Node 
{
    public int data;
    public Node link;
}

// Reference variable
Node top;

// Constructor
public StackUsingLinkedlist()
{
    this.top = null;
}

// Function to add an element x
// in the stack by inserting
// at the beginning of LL
public void push(int x)
{

    // Create new node temp
    Node temp = new Node();

    // If stack is full
    if (temp == null)
    {
        Console.Write("\nHeap Overflow");
        return;
    }

    // Initialize data into temp
    temp.data = x;

    // Reference into temp link
    temp.link = top;

    // Update top reference
    top = temp;
}

// Function to check if the stack
// is empty or not
public bool isEmpty()
{
    return top == null;
}

// Function to return top element
// in a stack
public int peek()
{

    // Check for empty stack
    if (isEmpty() != true)
    {

        // Return the top data
        return top.data;
    }

    // Otherwise stack is empty
    else
    {
        Console.WriteLine("Stack is empty");
        return -1;
    }
}

// Function to pop top element from
// the stack by removing element
// at the beginning
public void pop()
{

    // Check for stack underflow
    if (top == null)
    {
        Console.Write("\nStack Underflow");
        return;
    }

    // Update the top pointer to
    // point to the next node
    top = (top).link;
}

// Function to print the elements and
// restore the stack
public void DisplayStack(StackUsingLinkedlist s)
{

    // Create another stack
    StackUsingLinkedlist s1 = new StackUsingLinkedlist();

    // Until stack is empty
    while (s.isEmpty() != true) 
    {
        s1.push(s.peek());

        // Print the element
        Console.Write(s1.peek() + " ");
        s.pop();
    }
}
}

class GFG{

// Driver Code
public static void Main(String[] args)
{

    // Create Object of class
    StackUsingLinkedlist obj = new StackUsingLinkedlist();

    // Insert Stack value
    obj.push(1);
    obj.push(2);
    obj.push(3);
    obj.push(4);

    // Function Call
    obj.DisplayStack(obj);
}
}

// This code is contributed by Amit Katiyar

```

**输出**：

```
4 3 2 1 

```

**时间复杂度**：`O(n)`，其中`N`是给定栈中元素的数量。

**辅助空间**：`O(n)`

[**数组栈方法**](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)：此方法讨论[数组栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)实现中问题的解决方案。 步骤如下：

1.  将给定栈中的顶部元素推入[数组栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)。

2.  打印[数组栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)的顶部元素。

3.  从给定的主栈中弹出顶部元素。

4.  按顺序重复上述步骤，直到给定的栈为空。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach

class Stack {

    static final int MAX = 1000;

    // Stores the index where element
    // needs to be inserted
    int top;

    // Array to store the stack elements
    int a[] = new int[MAX];

    // Function that check whether stack
    // is empty or not
    boolean isEmpty()
    {
        return (top < 0);
    }

    // Constructor
    Stack() { top = -1; }

    // Function that pushes the element
    // to the top of the stack
    boolean push(int x)
    {
        // If stack is full
        if (top >= (MAX - 1)) {
            System.out.println(
                "Stack Overflow");
            return false;
        }

        // Otherwise insert element x
        else {
            a[++top] = x;
            return true;
        }
    }

    // Function that removes the top
    // element from the stack
    int pop()
    {
        // If stack is empty
        if (top < 0) {
            System.out.println(
                "Stack Underflow");
            return 0;
        }

        // Otherwise remove element
        else {
            int x = a[top--];
            return x;
        }
    }

    // Function to get the top element
    int peek()
    {
        // If stack is empty
        if (top < 0) {
            System.out.println(
                "Stack Underflow");
            return 0;
        }

        // Otherwise remove element
        else {
            int x = a[top];
            return x;
        }
    }

    // Function to print the elements
    // and restore the stack
    static void DisplayStack(Stack s)
    {
        // Create another stack
        Stack s1 = new Stack();

        // Until stack is empty
        while (!s.isEmpty()) {
            s1.push(s.peek());

            // Print the element
            System.out.print(s1.peek()
                             + " ");
            s.pop();
        }
    }
}

// Driver Code
class Main {

    // Driver Code
    public static void main(String args[])
    {
        Stack s = new Stack();

        // Given stack
        s.push(1);
        s.push(2);
        s.push(3);
        s.push(4);

        // Function Call
        s.DisplayStack(s);
    }
}

```

## C#

```cs

// C# program for 
// the above approach
using System;
class Stack{

static int MAX = 1000;

// Stores the index where 
// element needs to be inserted
int top;

// Array to store the 
// stack elements
int []a = new int[MAX];

// Function that check 
// whether stack
// is empty or not
bool isEmpty()
{
  return (top < 0);
}

// Constructor
public Stack() 
{ 
  top = -1; 
}

// Function that pushes 
// the element to the 
// top of the stack
public bool push(int x)
{
  // If stack is full
  if (top >= (MAX - 1)) 
  {
    Console.WriteLine("Stack Overflow");
    return false;
  }

  // Otherwise insert element x
  else
  {
    a[++top] = x;
    return true;
  }
}

// Function that removes the top
// element from the stack
public int pop()
{
  // If stack is empty
  if (top < 0) 
  {
    Console.WriteLine("Stack Underflow");
    return 0;
  }

  // Otherwise remove element
  else
  {
    int x = a[top--];
    return x;
  }
}

// Function to get the top element
public int peek()
{
  // If stack is empty
  if (top < 0) 
  {
    Console.WriteLine("Stack Underflow");
    return 0;
  }

  // Otherwise remove element
  else
  {
    int x = a[top];
    return x;
  }
}

// Function to print the elements
// and restore the stack
public void DisplayStack(Stack s)
{
  // Create another stack
  Stack s1 = new Stack();

  // Until stack is empty
  while (!s.isEmpty()) 
  {
    s1.push(s.peek());

    // Print the element
    Console.Write(s1.peek() + " ");
    s.pop();
  }
}
}

class GFG{

// Driver Code
public static void Main(String []args)
{
  Stack s = new Stack();

  // Given stack
  s.push(1);
  s.push(2);
  s.push(3);
  s.push(4);

  // Function Call
  s.DisplayStack(s);
}
}

// This code is contributed by 29AjayKumar

```

**输出**：

```
4 3 2 1 

```

**时间复杂度**：`O(n)`，其中`N`是给定栈中元素的数量。

**辅助空间**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。