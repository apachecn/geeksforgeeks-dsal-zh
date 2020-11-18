# 使用单链表

实现堆栈

使用单个链表概念实现[堆栈](http://www.geeksforgeeks.org/stack-data-structure/)。 所有单个[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)操作都是基于堆栈操作LIFO（后进先出）执行的，借助这一知识，我们将使用单个链表实现堆栈。 使用单个链表，所以在这里如何实现链表意味着我们以节点的形式存储信息，我们需要遵循堆栈规则，并且需要使用单个链表节点来实现，所以我们需要什么规则 在堆栈的实现中遵循一个简单的规则，即后进先出，我们应该在top变量的帮助下执行的所有操作仅在top变量的帮助下如何插入元素

![](img/2ff65df4659cd0868f221729a88fc111.png)

![](img/4f4e79365f04c526881b5ee8cdef77bc.png)

![](img/bb9d68ec1e8e118b1f80c4a99642d325.png)

通过链接列表可以轻松实现堆栈。 在堆栈实现中，堆栈包含顶部指针。 这是堆栈的“头”，其中推送和弹出项发生在列表的头。 第一个节点在链接字段中为空，第二个节点链接在链接字段中具有第一个节点地址，依此类推，最后一个节点地址在“ top”指针中。

在数组上使用链接列表的主要优点是可以实现可根据需要缩小或增长的堆栈。 使用数组会限制数组的最大容量，这可能导致堆栈溢出。 在这里，每个新节点将被动态分配。 因此不可能发生溢出。

**堆栈操作：**

1.  **[push（）](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)：**将该元素插入到链表中，只是栈的顶部节点。
2.  **[pop（）](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)：**从堆栈中返回顶部元素，并将顶部指针移至链接列表或堆栈的第二个节点。
3.  **[peek（）](https://www.geeksforgeeks.org/stack-peek-method-in-java/)：**返回顶部元素。
4.  **display（）：**打印堆栈的所有元素。

**下面是上述方法的实现：**

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to Implement a stack ``//using singly linked list ``#include <bits/stdc++.h> ``using` `namespace` `std; ``// Declare linked list node ``struct` `Node ``{ ` `int` `data; ` `struct` `Node* link; ``}; ``struct` `Node* top; ``// Utility function to add an element ``// data in the stack insert at the beginning ``void` `push(` `int` `data) ``{ ` `// Create new node temp and allocate memory ` `struct` `Node* temp; ` `temp =` `new` `Node(); ` `// Check if stack (heap) is full. ` `// Then inserting an element would ` `// lead to stack overflow ` `if` `(!temp)` `{ ` `cout <<` `"\nHeap Overflow"` `; ` `exit` `(1); ` `} ` `// Initialize data into temp data field ` ] `temp->data = data; ` `// Put top pointer reference into temp link ` `temp->link = top; ` `// Make temp as top of Stack ` `top = temp; ``} ``// Utility function to check if ``// the stack is empty or not ``int` `isEmpty() ``{ ` `return` `top == NULL; ``} ``// Utility function to return top element in a stack ``int` `peek() ``{ ` HTG381] [H TG382]  `// Check for empty stack ` `if` `(!isEmpty()) ` `return` `top->data; ` `else` `exit` `(1); ``} ``// Utility function to pop top ``// element from the stack ``void` `pop() ``{ ` `struct` `Node* temp; ` `// Check for stack underflow ` `if` `(top == NULL) ` `{ ` `cout <<` `"\nStack Underflow"` `<< endl; ` `exit` `(1); ` `} ` `else` `{ ` `// Top assign into temp ` `temp = top; `[HTG43 0]  `// Assign second node to top ` `top = top->link; ` `// Destroy connection between` `// first and second ` `temp->link = NULL; ` `// Release memory of top node `]  `free` `(temp); ` `} ``} ``// Function to print all the ``// elements of the stack ``void` `display() ``{ ` `struct` `Node* temp; ` `// Check for stack underflow ` `if` `(top == NULL)` `{ ` `cout <<` `"\nStack Underflow"` `; ` `exit` `(1); ` `} `[HT G480]  `else` `{ ` `temp = top; ` `while` `(temp != NULL)` `{ ` `// Print node data ` `cout << temp->data <<` `"-> "` `; `] `// Assign temp link to temp ` `temp = temp->link; ` `} ` `} ``} ``// Driver Code ``int` `main() ``{ ` `// Push the elements of stack ` `push(11); ` `push(22); ` `push(33); ` `push(44); ` `// Display stack elements ` `display(); ` `// Print top element of stack ` `cout <<` `"\nTop element is "` `<< peek() << endl; ` `// Delete top elements of stack ` `pop(); ` `pop(); ` `// Display stack elements ` `display(); ` `// Print top element of stack ` `cout <<` `"\nTop element is "` `<< peek() << endl; ` ] `return` `0; ``}` ​​`// This code is contributed by Striver ` |

*chevron_right**filter_none*