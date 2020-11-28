# 栈数据结构（简介和程序）

> 原文：[https://www.geeksforgeeks.org/stack-data-structure-introduction-program/](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)

栈是一种线性数据结构，遵循特定的操作顺序。 该订单可以是 LIFO（后进先出）或 FILO（后进先出）。

主要在栈中执行以下三个基本操作：

*   **推入**：在栈中添加一个项目。 如果栈已满，则称其为溢出条件。

*   **弹出**：从栈中删除一个项目。 这些项目以推入的相反顺序弹出。 如果栈为空，则称其为下溢条件。

*   **窥视或顶部**：返回栈的顶部元素。

*   **isEmpty**：如果堆栈为空，则返回`true`，否则返回`false`。

![stack](img/91f929ba5f7179300fc713d1f8126678.png)

**如何实际理解栈？**

有很多现实生活中的例子。 考虑一下在食堂中相互堆叠的盘子的简单示例。 位于顶部的板是第一个要卸下的板，即已放置在最底部位置的板在栈中保留的时间最长。 因此，可以简单地看出它遵循 LIFO/FILO 命令。

**栈上操作的时间复杂度**：

`push()`，`pop()`，`isEmpty()`和`peek()`都需要`O(1)`时间。 在任何这些操作中，我们都不会运行任何循环。

**栈的应用**：

*   [符号平衡](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)

*   [后缀](http://quiz.geeksforgeeks.org/stack-set-2-infix-to-postfix/) /前缀转换的前缀

*   在许多地方（例如编辑器，photoshop）重做-撤消功能。

*   Web 浏览器中的前进和后退功能

*   用于许多算法中，例如[河内塔](https://www.geeksforgeeks.org/recursive-functions/) [树遍历](https://www.geeksforgeeks.org/618/)，[库存跨度问题](https://www.geeksforgeeks.org/the-stock-span-problem/)，[直方图问题](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/)。

*   其他应用包括回溯，[骑士旅行问题](https://www.geeksforgeeks.org/backtracking-set-1-the-knights-tour-problem/)，[迷宫中的老鼠](https://www.geeksforgeeks.org/backttracking-set-2-rat-in-a-maze/)，[`N`皇后问题](https://www.geeksforgeeks.org/backtracking-set-3-n-queen-problem/)和[数独解算器](https://www.geeksforgeeks.org/backtracking-set-7-suduku/)

*   在图算法中，例如[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)和[强连接的组件](https://www.geeksforgeeks.org/strongly-connected-components/)

**实现**：

有两种实现栈的方法：

*   使用数组

*   使用链表

**使用数组实现栈**

## C++

```cpp

/* C++ program to implement basic stack 
   operations */
#include <bits/stdc++.h> 

using namespace std; 

#define MAX 1000 

class Stack { 
    int top; 

public: 
    int a[MAX]; // Maximum size of Stack 

    Stack() { top = -1; } 
    bool push(int x); 
    int pop(); 
    int peek(); 
    bool isEmpty(); 
}; 

bool Stack::push(int x) 
{ 
    if (top >= (MAX - 1)) { 
        cout << "Stack Overflow"; 
        return false; 
    } 
    else { 
        a[++top] = x; 
        cout << x << " pushed into stack\n"; 
        return true; 
    } 
} 

int Stack::pop() 
{ 
    if (top < 0) { 
        cout << "Stack Underflow"; 
        return 0; 
    } 
    else { 
        int x = a[top--]; 
        return x; 
    } 
} 
int Stack::peek() 
{ 
    if (top < 0) { 
        cout << "Stack is Empty"; 
        return 0; 
    } 
    else { 
        int x = a[top]; 
        return x; 
    } 
} 

bool Stack::isEmpty() 
{ 
    return (top < 0); 
} 

// Driver program to test above functions 
int main() 
{ 
    class Stack s; 
    s.push(10); 
    s.push(20); 
    s.push(30); 
    cout << s.pop() << " Popped from stack\n"; 

    return 0; 
} 

```

## C

```c

// C program for array implementation of stack 
#include <limits.h> 
#include <stdio.h> 
#include <stdlib.h> 

// A structure to represent a stack 
struct Stack { 
    int top; 
    unsigned capacity; 
    int* array; 
}; 

// function to create a stack of given capacity. It initializes size of 
// stack as 0 
struct Stack* createStack(unsigned capacity) 
{ 
    struct Stack* stack = (struct Stack*)malloc(sizeof(struct Stack)); 
    stack->capacity = capacity; 
    stack->top = -1; 
    stack->array = (int*)malloc(stack->capacity * sizeof(int)); 
    return stack; 
} 

// Stack is full when top is equal to the last index 
int isFull(struct Stack* stack) 
{ 
    return stack->top == stack->capacity - 1; 
} 

// Stack is empty when top is equal to -1 
int isEmpty(struct Stack* stack) 
{ 
    return stack->top == -1; 
} 

// Function to add an item to stack.  It increases top by 1 
void push(struct Stack* stack, int item) 
{ 
    if (isFull(stack)) 
        return; 
    stack->array[++stack->top] = item; 
    printf("%d pushed to stack\n", item); 
} 

// Function to remove an item from stack.  It decreases top by 1 
int pop(struct Stack* stack) 
{ 
    if (isEmpty(stack)) 
        return INT_MIN; 
    return stack->array[stack->top--]; 
} 

// Function to return the top from stack without removing it 
int peek(struct Stack* stack) 
{ 
    if (isEmpty(stack)) 
        return INT_MIN; 
    return stack->array[stack->top]; 
} 

// Driver program to test above functions 
int main() 
{ 
    struct Stack* stack = createStack(100); 

    push(stack, 10); 
    push(stack, 20); 
    push(stack, 30); 

    printf("%d popped from stack\n", pop(stack)); 

    return 0; 
} 

```

## Java

```java

/* Java program to implement basic stack 
operations */
class Stack { 
    static final int MAX = 1000; 
    int top; 
    int a[] = new int[MAX]; // Maximum size of Stack 

    boolean isEmpty() 
    { 
        return (top < 0); 
    } 
    Stack() 
    { 
        top = -1; 
    } 

    boolean push(int x) 
    { 
        if (top >= (MAX - 1)) { 
            System.out.println("Stack Overflow"); 
            return false; 
        } 
        else { 
            a[++top] = x; 
            System.out.println(x + " pushed into stack"); 
            return true; 
        } 
    } 

    int pop() 
    { 
        if (top < 0) { 
            System.out.println("Stack Underflow"); 
            return 0; 
        } 
        else { 
            int x = a[top--]; 
            return x; 
        } 
    } 

    int peek() 
    { 
        if (top < 0) { 
            System.out.println("Stack Underflow"); 
            return 0; 
        } 
        else { 
            int x = a[top]; 
            return x; 
        } 
    } 
} 

// Driver code 
class Main { 
    public static void main(String args[]) 
    { 
        Stack s = new Stack(); 
        s.push(10); 
        s.push(20); 
        s.push(30); 
        System.out.println(s.pop() + " Popped from stack"); 
    } 
} 

```

## Python

```py

# Python program for implementation of stack 

# import maxsize from sys module  
# Used to return -infinite when stack is empty 
from sys import maxsize 

# Function to create a stack. It initializes size of stack as 0 
def createStack(): 
    stack = [] 
    return stack 

# Stack is empty when stack size is 0 
def isEmpty(stack): 
    return len(stack) == 0

# Function to add an item to stack. It increases size by 1 
def push(stack, item): 
    stack.append(item) 
    print(item + " pushed to stack ") 

# Function to remove an item from stack. It decreases size by 1 
def pop(stack): 
    if (isEmpty(stack)): 
        return str(-maxsize -1) # return minus infinite 

    return stack.pop() 

# Function to return the top from stack without removing it 
def peek(stack): 
    if (isEmpty(stack)): 
        return str(-maxsize -1) # return minus infinite 
    return stack[len(stack) - 1] 

# Driver program to test above functions     
stack = createStack() 
push(stack, str(10)) 
push(stack, str(20)) 
push(stack, str(30)) 
print(pop(stack) + " popped from stack") 

```

## C#

```cs

// C# program to implement basic stack 
// operations 
using System; 

namespace ImplementStack { 
class Stack { 
    private int[] ele; 
    private int top; 
    private int max; 
    public Stack(int size) 
    { 
        ele = new int[size]; // Maximum size of Stack 
        top = -1; 
        max = size; 
    } 

    public void push(int item) 
    { 
        if (top == max - 1) { 
            Console.WriteLine("Stack Overflow"); 
            return; 
        } 
        else { 
            ele[++top] = item; 
        } 
    } 

    public int pop() 
    { 
        if (top == -1) { 
            Console.WriteLine("Stack is Empty"); 
            return -1; 
        } 
        else { 
            Console.WriteLine("{0} popped from stack ", ele[top]); 
            return ele[top--]; 
        } 
    } 

    public int peek() 
    { 
        if (top == -1) { 
            Console.WriteLine("Stack is Empty"); 
            return -1; 
        } 
        else { 
            Console.WriteLine("{0} popped from stack ", ele[top]); 
            return ele[top]; 
        } 
    } 

    public void printStack() 
    { 
        if (top == -1) { 
            Console.WriteLine("Stack is Empty"); 
            return; 
        } 
        else { 
            for (int i = 0; i <= top; i++) { 
                Console.WriteLine("{0} pushed into stack", ele[i]); 
            } 
        } 
    } 
} 

// Driver program to test above functions 
class Program { 
    static void Main() 
    { 
        Stack p = new Stack(5); 

        p.push(10); 
        p.push(20); 
        p.push(30); 
        p.printStack(); 
        p.pop(); 
    } 
} 
} 

```

**优点**：易于实现。 内存被保存，因为不涉及指针。

**缺点**：它不是动态的。 它不会根据运行时的需要而增长和收缩。

**输出**：

```
10 pushed into stack
20 pushed into stack
30 pushed into stack
30 popped from stack

```

**使用链表**实现栈

## C++

```cpp

// C++ program for linked list implementation of stack 
#include <bits/stdc++.h> 
using namespace std; 

// A structure to represent a stack 
class StackNode { 
public: 
    int data; 
    StackNode* next; 
}; 

StackNode* newNode(int data) 
{ 
    StackNode* stackNode = new StackNode(); 
    stackNode->data = data; 
    stackNode->next = NULL; 
    return stackNode; 
} 

int isEmpty(StackNode* root) 
{ 
    return !root; 
} 

void push(StackNode** root, int data) 
{ 
    StackNode* stackNode = newNode(data); 
    stackNode->next = *root; 
    *root = stackNode; 
    cout << data << " pushed to stack\n"; 
} 

int pop(StackNode** root) 
{ 
    if (isEmpty(*root)) 
        return INT_MIN; 
    StackNode* temp = *root; 
    *root = (*root)->next; 
    int popped = temp->data; 
    free(temp); 

    return popped; 
} 

int peek(StackNode* root) 
{ 
    if (isEmpty(root)) 
        return INT_MIN; 
    return root->data; 
} 

int main() 
{ 
    StackNode* root = NULL; 

    push(&root, 10); 
    push(&root, 20); 
    push(&root, 30); 

    cout << pop(&root) << " popped from stack\n"; 

    cout << "Top element is " << peek(root) << endl; 

    return 0; 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program for linked list implementation of stack 
#include <limits.h> 
#include <stdio.h> 
#include <stdlib.h> 

// A structure to represent a stack 
struct StackNode { 
    int data; 
    struct StackNode* next; 
}; 

struct StackNode* newNode(int data) 
{ 
    struct StackNode* stackNode = (struct StackNode*)malloc(sizeof(struct StackNode)); 
    stackNode->data = data; 
    stackNode->next = NULL; 
    return stackNode; 
} 

int isEmpty(struct StackNode* root) 
{ 
    return !root; 
} 

void push(struct StackNode** root, int data) 
{ 
    struct StackNode* stackNode = newNode(data); 
    stackNode->next = *root; 
    *root = stackNode; 
    printf("%d pushed to stack\n", data); 
} 

int pop(struct StackNode** root) 
{ 
    if (isEmpty(*root)) 
        return INT_MIN; 
    struct StackNode* temp = *root; 
    *root = (*root)->next; 
    int popped = temp->data; 
    free(temp); 

    return popped; 
} 

int peek(struct StackNode* root) 
{ 
    if (isEmpty(root)) 
        return INT_MIN; 
    return root->data; 
} 

int main() 
{ 
    struct StackNode* root = NULL; 

    push(&root, 10); 
    push(&root, 20); 
    push(&root, 30); 

    printf("%d popped from stack\n", pop(&root)); 

    printf("Top element is %d\n", peek(root)); 

    return 0; 
} 

```

## Java

```java

// Java Code for Linked List Implementation 

public class StackAsLinkedList { 

    StackNode root; 

    static class StackNode { 
        int data; 
        StackNode next; 

        StackNode(int data) 
        { 
            this.data = data; 
        } 
    } 

    public boolean isEmpty() 
    { 
        if (root == null) { 
            return true; 
        } 
        else
            return false; 
    } 

    public void push(int data) 
    { 
        StackNode newNode = new StackNode(data); 

        if (root == null) { 
            root = newNode; 
        } 
        else { 
            StackNode temp = root; 
            root = newNode; 
            newNode.next = temp; 
        } 
        System.out.println(data + " pushed to stack"); 
    } 

    public int pop() 
    { 
        int popped = Integer.MIN_VALUE; 
        if (root == null) { 
            System.out.println("Stack is Empty"); 
        } 
        else { 
            popped = root.data; 
            root = root.next; 
        } 
        return popped; 
    } 

    public int peek() 
    { 
        if (root == null) { 
            System.out.println("Stack is empty"); 
            return Integer.MIN_VALUE; 
        } 
        else { 
            return root.data; 
        } 
    } 

    public static void main(String[] args) 
    { 

        StackAsLinkedList sll = new StackAsLinkedList(); 

        sll.push(10); 
        sll.push(20); 
        sll.push(30); 

        System.out.println(sll.pop() + " popped from stack"); 

        System.out.println("Top element is " + sll.peek()); 
    } 
} 

```

## Python

```py

# Python program for linked list implementation of stack 

# Class to represent a node 
class StackNode: 

    # Constructor to initialize a node 
    def __init__(self, data): 
        self.data = data  
        self.next = None

class Stack: 

    # Constructor to initialize the root of linked list 
    def __init__(self): 
        self.root = None

    def isEmpty(self): 
        return True if self.root is None else  False 

    def push(self, data): 
        newNode = StackNode(data) 
        newNode.next = self.root  
        self.root = newNode 
        print "% d pushed to stack" %(data) 

    def pop(self): 
        if (self.isEmpty()): 
            return float("-inf") 
        temp = self.root  
        self.root = self.root.next 
        popped = temp.data 
        return popped 

    def peek(self): 
        if self.isEmpty(): 
            return float("-inf") 
        return self.root.data 

# Driver program to test above class  
stack = Stack() 
stack.push(10)         
stack.push(20) 
stack.push(30) 

print "% d popped from stack" %(stack.pop()) 
print "Top element is % d " %(stack.peek()) 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C#

```cs

// C# Code for Linked List Implementation 
using System; 

public class StackAsLinkedList { 

    StackNode root; 

    public class StackNode { 
        public int data; 
        public StackNode next; 

        public StackNode(int data) 
        { 
            this.data = data; 
        } 
    } 

    public bool isEmpty() 
    { 
        if (root == null) { 
            return true; 
        } 
        else
            return false; 
    } 

    public void push(int data) 
    { 
        StackNode newNode = new StackNode(data); 

        if (root == null) { 
            root = newNode; 
        } 
        else { 
            StackNode temp = root; 
            root = newNode; 
            newNode.next = temp; 
        } 
        Console.WriteLine(data + " pushed to stack"); 
    } 

    public int pop() 
    { 
        int popped = int.MinValue; 
        if (root == null) { 
            Console.WriteLine("Stack is Empty"); 
        } 
        else { 
            popped = root.data; 
            root = root.next; 
        } 
        return popped; 
    } 

    public int peek() 
    { 
        if (root == null) { 
            Console.WriteLine("Stack is empty"); 
            return int.MinValue; 
        } 
        else { 
            return root.data; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 

        StackAsLinkedList sll = new StackAsLinkedList(); 

        sll.push(10); 
        sll.push(20); 
        sll.push(30); 

        Console.WriteLine(sll.pop() + " popped from stack"); 

        Console.WriteLine("Top element is " + sll.peek()); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

输出：

```
10 pushed to stack
20 pushed to stack
30 pushed to stack
30 popped from stack
Top element is 20
```

**优点**：栈的链表实现可以在运行时根据需要进行扩展和收缩。

**缺点**：由于涉及指针，因此需要额外的内存。

我们将在单独的文章中介绍栈应用程序的实现。

[栈 | 系列 2（中缀转后缀）](http://quiz.geeksforgeeks.org/stack-set-2-infix-to-postfix/)

**测验**：[栈问题](http://quiz.geeksforgeeks.org/data-structure/stack/)

**参考**：

[http://en.wikipedia.org/wiki/Stack_%28abstract_data_type%29#Problem_Description](http://en.wikipedia.org/wiki/Stack_%28abstract_data_type%29#Problem_Description)

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

