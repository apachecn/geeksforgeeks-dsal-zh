# 从下往上打印堆栈元素

> 原文:[https://www . geesforgeks . org/print-stack-elements-自下而上/](https://www.geeksforgeeks.org/print-stack-elements-from-bottom-to-top/)

给定一个堆栈，任务是从底部到顶部打印堆栈的元素，这样元素仍然存在于堆栈中，而它们在堆栈中的顺序不会改变。

**示例:**

```
Input : 

|   4    |
|   3    |
|   2    |
|   1    |
|________|

Output :1 2 3 4
```

**方法 1(递归):**思路是弹出栈的元素，调用递归函数 PrintStack。一旦堆栈变空，开始打印最后弹出的元素，最后弹出的元素是最底部的元素。因此，元素将从下往上打印。现在推回被打印的元素，这将保持元素在堆栈中的顺序。

下面是上述方法的实现:

## C++

```
// C++ program to print the elements of a
// stack from bottom to top
#include <bits/stdc++.h>
using namespace std;

// Recursive function to print stack elements
// from bottom to top without changing
// their order
void PrintStack(stack<int> s)
{
    // If stack is empty then return
    if (s.empty())
        return;

    int x = s.top();

    // Pop the top element of the stack
    s.pop();

    // Recursively call the function PrintStack
    PrintStack(s);

    // Print the stack element starting
    // from the bottom
    cout << x << " ";

    // Push the same element onto the stack
    // to preserve the order
    s.push(x);
}

// Driver code
int main()
{
    // Stack s
    stack<int> s;

    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);

    PrintStack(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the elements of a
// stack from bottom to top
import java.util.*;

class GfG
{

// Recursive function to print stack elements
// from bottom to top without changing
// their order
static void PrintStack(Stack<Integer> s)
{
    // If stack is empty then return
    if (s.isEmpty())
        return;

    int x = s.peek();

    // Pop the top element of the stack
    s.pop();

    // Recursively call the function PrintStack
    PrintStack(s);

    // Print the stack element starting
    // from the bottom
    System.out.print(x + " ");

    // Push the same element onto the stack
    // to preserve the order
    s.push(x);
}

// Driver code
public static void main(String[] args)
{
    // Stack s
    Stack<Integer> s = new Stack<Integer> ();

    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);

    PrintStack(s);
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to print the elements of a
# stack from bottom to top

# Stack class with all functionality of a stack
import sys
class Stack:
    def __init__(self):
        self.s = []

    def push(self, data):
        self.s.append(data)

    def pop(self):
        return self.s.pop()

    def peek(self):
        return self.s[-1]
    def count(self):
        return len(self.s)

# Recursive function to print stack elements
# from bottom to top without changing
# their order
def printStack(s):

    # if stack is empty then simply return
    if s.count() == 0:
        return
    x = s.peek()

    # pop top most element of the stack
    s.pop()

    # recursively call the function printStack
    printStack(s)

    # Print the stack element starting
    # from the bottom
    print("{} ".format(x), end = "")

    # Push the same element onto the stack
    # to preserve the order
    s.push(x)

# Driver code
if __name__=='__main__':
    s=Stack()
    s.push(1)
    s.push(2)
    s.push(3)
    s.push(4)

    printStack(s)

# This code is contributed by Vikas Kumar
```

## C#

```
// C# program to print the elements of a
// stack from bottom to top
using System;
using System.Collections.Generic;

class GfG
{

// Recursive function to print stack elements
// from bottom to top without changing
// their order
static void PrintStack(Stack<int> s)
{
    // If stack is empty then return
    if (s.Count == 0)
        return;

    int x = s.Peek();

    // Pop the top element of the stack
    s.Pop();

    // Recursively call the function PrintStack
    PrintStack(s);

    // Print the stack element starting
    // from the bottom
    Console.Write(x + " ");

    // Push the same element onto the stack
    // to preserve the order
    s.Push(x);
}

// Driver code
public static void Main()
{
    // Stack s
    Stack<int> s = new Stack<int> ();

    s.Push(1);
    s.Push(2);
    s.Push(3);
    s.Push(4);

    PrintStack(s);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to print the elements
// of a stack from bottom to top

// Recursive function to print stack
// elements from bottom to top without
// changing their order
function PrintStack(s)
{

    // If stack is empty then return
    if (s.length == 0)
        return;

    var x = s[s.length - 1];

    // Pop the top element of the stack
    s.pop();

    // Recursively call the function PrintStack
    PrintStack(s);

    // Print the stack element starting
    // from the bottom
    document.write(x + " ");

    // Push the same element onto the stack
    // to preserve the order
    s.push(x);
}

// Driver code

// Stack s
var s = [];
s.push(1);
s.push(2);
s.push(3);
s.push(4);

PrintStack(s);

// This code is contributed by importantly

</script>
```

**Output:** 

```
1 2 3 4
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)

**方法 2(使用另一个堆栈):**想法是将每个元素推入另一个临时堆栈，然后打印临时堆栈的元素。

## C++

```
// C++ program to print the elements of a
// stack from bottom to top
#include <bits/stdc++.h>
using namespace std;

// Recursive function to print stack elements
// from bottom to top without changing
// their order
void PrintStack(stack<int> s)
{
    stack<int> temp;
    while (s.empty() == false)
    {
        temp.push(s.top());
        s.pop();
    }  

    while (temp.empty() == false)
    {
        int t = temp.top();
        cout << t << " ";
        temp.pop();

        // To restore contents of
        // the original stack.
        s.push(t); 
    }
}

// Driver code
int main()
{
    // Stack s
    stack<int> s;

    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);

    PrintStack(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// elements of a stack from
// bottom to top
import java.util.*;
class Main{

// Recursive function to print
// stack elements from bottom
// to top without changing
// their order
public static void PrintStack(Stack<Integer> s)
{
  Stack<Integer> temp = new Stack<Integer>();

  while (s.empty() == false)
  {
    temp.push(s.peek());
    s.pop();
  }  

  while (temp.empty() == false)
  {
    int t = temp.peek();
    System.out.print(t + " ");
    temp.pop();

    // To restore contents of
    // the original stack.
    s.push(t); 
  }
}

// Driver code
public static void main(String[] args)
{
  // Stack s
  Stack<Integer> s = new Stack<Integer>();

  s.push(1);
  s.push(2);
  s.push(3);
  s.push(4);
  PrintStack(s);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to print the elements of a
# stack from bottom to top

# Stack class with all functionality of a stack
import sys
class Stack:
    def __init__(self):
        self.s = []

    def push(self, data):
        self.s.append(data)

    def pop(self):
        return self.s.pop()

    def peek(self):
        return self.s[-1]
    def count(self):
        return len(self.s)

# Recursive function to print stack elements
# from bottom to top without changing
# their order
def printStack(s):
    temp = Stack()
    while(s.count() > 0):
        temp.push(s.peek())
        s.pop()

    while(temp.count() > 0):
        t = temp.peek()
        print("{} " . format(temp.peek()), end = "")
        temp.pop()

        # Restore the contents of original stack
        s.push(t)

# Driver code
if __name__=='__main__':
    s = Stack()
    s.push(1)
    s.push(2)
    s.push(3)
    s.push(4)

    printStack(s)

# This code is contributed by Vikash Kumar 37
```

## C#

```
// C# program to print the elements of
// a stack from bottom to top
using System;
using System.Collections;

class GFG{

// Recursive function to print stack
// elements from bottom to top without
// changing their order
static void PrintStack(Stack s)
{
    Stack temp = new Stack();
    while (s.Count != 0)
    {
        temp.Push(s.Peek());
        s.Pop();
    }  

    while (temp.Count != 0)
    {
        int t = (int)temp.Peek();
        Console.Write(t + " ");
        temp.Pop();

        // To restore contents of
        // the original stack.
        s.Push(t); 
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Stack s
    Stack s = new Stack();
    s.Push(1);
    s.Push(2);
    s.Push(3);
    s.Push(4);

    PrintStack(s);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to print the elements of a
// stack from bottom to top

// Recursive function to print stack elements
// from bottom to top without changing
// their order
function PrintStack(s)
{
    var temp = [];
    while (s.length!=0)
    {
        temp.push(s[s.length-1]);
        s.pop();
    }  

    while (temp.length!=0)
    {
        var t = temp[temp.length-1];
        document.write( t + " ");
        temp.pop();

        // To restore contents of
        // the original stack.
        s.push(t); 
    }
}

// Driver code
// Stack s
var s = [];
s.push(1);
s.push(2);
s.push(3);
s.push(4);
PrintStack(s);

</script>
```

**Output:** 

```
1 2 3 4
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)