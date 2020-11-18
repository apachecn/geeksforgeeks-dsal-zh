# 反转堆栈，而无需在 O（n）中使用多余的空间

在不使用递归和多余空间的情况下反转[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)。 甚至连功能堆栈都不允许。

**示例：**

```
Input : 1->2->3->4
Output : 4->3->2->1

Input :  6->5->4
Output : 4->5->6

```

我们在下面的文章中讨论了一种反转字符串的方法。

[使用递归](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)反转堆栈

上述解决方案需要 O（n）额外空间。 如果我们内部将堆栈表示为链表，则可以在 O（1）时间内反转字符串。 反转堆栈需要反转链表，这可以用 O（n）时间和 O（1）额外空间来完成。

请注意，push（）和 pop（）操作仍然需要 O（1）时间。

## C++

```cpp

// CPP program to implement Stack  
// using linked list so that reverse 
// can be done with O(1) extra space. 
#include<bits/stdc++.h> 
using namespace std; 

class StackNode { 
    public: 
    int data; 
    StackNode *next; 

    StackNode(int data) 
    { 
        this->data = data; 
        this->next = NULL; 
    } 
}; 

class Stack { 

    StackNode *top; 

    public: 

    // Push and pop operations 
    void push(int data) 
    { 
        if (top == NULL) { 
            top = new StackNode(data); 
            return; 
        } 
        StackNode *s = new StackNode(data); 
        s->next = top; 
        top = s; 
    } 

    StackNode* pop() 
    { 
        StackNode *s = top; 
        top = top->next; 
        return s; 
    } 

    // prints contents of stack 
    void display() 
    { 
        StackNode *s = top; 
        while (s != NULL) { 
            cout << s->data << " "; 
            s = s->next; 
        } 
        cout << endl; 
    } 

    // Reverses the stack using simple 
    // linked list reversal logic. 
    void reverse() 
    { 
        StackNode *prev, *cur, *succ; 
        cur = prev = top; 
        cur = cur->next; 
        prev->next = NULL; 
        while (cur != NULL) { 

            succ = cur->next; 
            cur->next = prev; 
            prev = cur; 
            cur = succ; 
        } 
        top = prev; 
    } 
}; 

// driver code 
int main() 
{ 
    Stack *s = new Stack(); 
    s->push(1); 
    s->push(2); 
    s->push(3); 
    s->push(4); 
    cout << "Original Stack" << endl;; 
    s->display(); 
    cout << endl; 

    // reverse 
    s->reverse(); 

    cout << "Reversed Stack" << endl; 
    s->display(); 

    return 0; 
} 
// This code is contribute by Chhavi. 

```

## Java

```java

// Java program to implement Stack using linked 
// list so that reverse can be done with O(1)  
// extra space. 
class StackNode { 
    int data; 
    StackNode next; 
    public StackNode(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
} 

class Stack { 
    StackNode top; 

    // Push and pop operations 
    public void push(int data) 
    { 
        if (this.top == null) { 
            top = new StackNode(data); 
            return; 
        } 
        StackNode s = new StackNode(data); 
        s.next = this.top; 
        this.top = s; 
    } 
    public StackNode pop() 
    { 
        StackNode s = this.top; 
        this.top = this.top.next; 
        return s; 
    } 

    // prints contents of stack 
    public void display() 
    { 
        StackNode s = this.top; 
        while (s != null) { 
            System.out.print(s.data + " "); 
            s = s.next; 
        } 
        System.out.println(); 
    } 

    // Reverses the stack using simple 
    // linked list reversal logic. 
    public void reverse() 
    { 
        StackNode prev, cur, succ; 
        cur = prev = this.top; 
        cur = cur.next; 
        prev.next = null; 
        while (cur != null) { 

            succ = cur.next; 
            cur.next = prev; 
            prev = cur; 
            cur = succ; 
        } 
        this.top = prev; 
    } 
} 

public class reverseStackWithoutSpace { 
    public static void main(String[] args) 
    { 
        Stack s = new Stack(); 
        s.push(1); 
        s.push(2); 
        s.push(3); 
        s.push(4); 
        System.out.println("Original Stack"); 
        s.display(); 

        // reverse 
        s.reverse(); 

        System.out.println("Reversed Stack"); 
        s.display(); 
    } 
} 

```

## C#

```cs

// C# program to implement Stack using linked 
// list so that reverse can be done with O(1)  
// extra space. 
using System;  

public class StackNode 
{ 
    public int data; 
    public StackNode next; 
    public StackNode(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
} 

public class Stack  
{ 
    public StackNode top; 

    // Push and pop operations 
    public void push(int data) 
    { 
        if (this.top == null) 
        { 
            top = new StackNode(data); 
            return; 
        } 
        StackNode s = new StackNode(data); 
        s.next = this.top; 
        this.top = s; 
    } 

    public StackNode pop() 
    { 
        StackNode s = this.top; 
        this.top = this.top.next; 
        return s; 
    } 

    // prints contents of stack 
    public void display() 
    { 
        StackNode s = this.top; 
        while (s != null)  
        { 
            Console.Write(s.data + " "); 
            s = s.next; 
        } 
        Console.WriteLine(); 
    } 

    // Reverses the stack using simple 
    // linked list reversal logic. 
    public void reverse() 
    { 
        StackNode prev, cur, succ; 
        cur = prev = this.top; 
        cur = cur.next; 
        prev.next = null; 
        while (cur != null) 
        { 
            succ = cur.next; 
            cur.next = prev; 
            prev = cur; 
            cur = succ; 
        } 
        this.top = prev; 
    } 
} 

public class reverseStackWithoutSpace  
{ 
    // Driver code 
    public static void Main(String []args) 
    { 
        Stack s = new Stack(); 
        s.push(1); 
        s.push(2); 
        s.push(3); 
        s.push(4); 
        Console.WriteLine("Original Stack"); 
        s.display(); 

        // reverse 
        s.reverse(); 

        Console.WriteLine("Reversed Stack"); 
        s.display(); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Original Stack 
4 3 2 1
Reversed Stack 
1 2 3 4

```

本文由 **Niharika Sahai** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

