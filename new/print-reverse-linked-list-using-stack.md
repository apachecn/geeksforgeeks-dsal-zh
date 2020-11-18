# 打印使用堆栈

反向链接列表

给定一个链表，在不修改链表的情况下将其打印出来。

**示例：**

```
Input : 1 2 3 4 5 6
Output : 6 5 4 3 2 1

Input : 12 23 34 45 56 67 78
Output : 78 67 56 45 34 23 12

```

下面是现在允许在此处使用的不同解决方案，因为我们不能使用额外的空间来修改列表。

1.  [递归解决方案，以打印反向链接列表](https://www.geeksforgeeks.org/write-a-recursive-function-to-print-reverse-of-a-linked-list/)。 需要额外的空间。
2.  [反向链接列表](https://www.geeksforgeeks.org/reverse-a-linked-list/)，然后打印。 这需要对原始列表进行修改。
3.  [一种O（n <sup>2</sup> ）解决方案，用于打印链表](https://www.geeksforgeeks.org/print-reverse-linked-list-without-extra-space-modifications/)的反向列表，该列表首先计数节点，然后从末尾打印第k个节点。

在这篇文章中，讨论了有效的基于堆栈的解决方案。

1.  首先，将所有元素插入堆栈
2.  打印纸叠，直到纸叠不为空

注意：不要将每个节点的数据插入堆栈，而是将节点的地址插入堆栈。 这是因为节点数据的大小通常会大于节点地址的大小。 因此，如果堆栈直接存储数据元素，则最终将需要更多的内存。 另外，如果每个节点包含多个数据成员，则我们无法将节点的数据插入堆栈。 因此，一种简单有效的解决方案是简单地插入节点的地址。

以下是上述想法的实现：

## C ++

```

// C/C++ program to print reverse of linked list
// using stack.
#include <bits/stdc++.h>
using namespace std;

// Link list node
struct Node {
    int data;
    struct Node* next;
};

// Given a reference (pointer to pointer) to the head
// of a list and an int,
// push a new node on the front of the list.
void push(struct Node**head_ref, int new_data)
{
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

// Counts no. of nodes in linked list
int getCount(struct Node* head)
{
    int count = 0; // Initialize count
    struct Node* current = head; // Initialize current
    while (current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}

// Takes head pointer of the linked list and index
// as arguments and return data at index
int getNth(struct Node* head, int n)
{
    struct Node* curr = head;
    for (int i = 0; i < n - 1 && curr != NULL; i++)
        curr = curr->next;
    return curr->data;
}

void printReverse(Node* head)
{
    // store Node addresses in stack
    stack<Node*> stk;
    Node* ptr = head;
    while (ptr != NULL) {
        stk.push(ptr);
        ptr = ptr->next;
    }

    // print data from stack
    while (!stk.empty()) {
        cout << stk.top()->data << " ";
        stk.pop(); // pop after print
    }
    cout << "\n";
}

// Driver code
int main()
{
    // Start with the empty list
    struct Node* head = NULL;

    // Use push() to construct below list
    // 1->2->3->4->5 
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    // Function call
    printReverse(head);

    return 0;
}

```

## 爪哇

```

// Java program to print reverse of linked list
// using stack.
import java.util.*;

class GFG {

    /* Link list node */
    static class Node {
        int data;
        Node next;
    };

    /* Given a reference (pointer to pointer) to the head
    of a list and an int, push a new node on the front
    of the list. */
    static Node push(Node head_ref, int new_data)
    {
        Node new_node = new Node();
        new_node.data = new_data;
        new_node.next = (head_ref);
        (head_ref) = new_node;
        return head_ref;
    }

    /* Counts no. of nodes in linked list */
    static int getCount(Node head)
    {
        int count = 0; // Initialize count
        Node current = head; // Initialize current
        while (current != null) {
            count++;
            current = current.next;
        }
        return count;
    }

    /* Takes head pointer of the linked list and index
        as arguments and return data at index*/
    static int getNth(Node head, int n)
    {
        Node curr = head;
        for (int i = 0; i < n - 1 && curr != null; i++)
            curr = curr.next;
        return curr.data;
    }

    static void printReverse(Node head)
    {
        // store Node addresses in stack
        Stack<Node> stk = new Stack<Node>();
        Node ptr = head;
        while (ptr != null) {
            stk.push(ptr);
            ptr = ptr.next;
        }

        // print data from stack
        while (stk.size() > 0) {
            System.out.print(stk.peek().data + " ");
            stk.pop(); // pop after print
        }
        System.out.println("\n");
    }

    // Driver code
    public static void main(String args[])
    {
        // Start with the empty list
        Node head = null;

        // Use push() to con below list
        // 1.2.3.4.5
        head = push(head, 5);
        head = push(head, 4);
        head = push(head, 3);
        head = push(head, 2);
        head = push(head, 1);

        // Function call
        printReverse(head);
    }
}

// This code is contributed by Arnab Kundu

```

## Python3

```

# Python3 program to print reverse of linked list
# using stack.

# Node of a linked list

class Node:
    def __init__(self, next=None, data=None):
        self.next = next
        self.data = data

# Given a reference (pointer to pointer) to the head
# of a list and an int, push a new node on the front
# of the list.

def push(head_ref, new_data):

    new_node = Node()
    new_node.data = new_data
    new_node.next = (head_ref)
    (head_ref) = new_node
    return head_ref

# Counts no. of nodes in linked list

def getCount(head):

    count = 0  # Initialize count
    current = head  # Initialize current
    while (current != None):

        count = count + 1
        current = current.next

    return count

# Takes head pointer of the linked list and index
# as arguments and return data at index

def getNth(head, n):

    curr = head
    i = 0
    while(i < n - 1 and curr != None):
        curr = curr.next
        i = i + 1
    return curr.data

def printReverse(head):

    # store Node addresses in stack
    stk = []
    ptr = head
    while (ptr != None):

        stk.append(ptr)
        ptr = ptr.next

    # print data from stack
    while (len(stk) > 0):

        print(stk[-1].data, end=" ")
        stk.pop()  # pop after print

    print(" ")

# Driver code

# Start with the empty list
head = None

# Use push() to con below list
# 1.2.3.4.5
head = push(head, 5)
head = push(head, 4)
head = push(head, 3)
head = push(head, 2)
head = push(head, 1)

# Function call
printReverse(head)

# This code is Contributed by Arnab Kundu

```

## C＃

```

// C# program to print reverse of linked list
// using stack.
using System;
using System.Collections.Generic;

class GFG {

    /* Link list node */
    public class Node {
        public int data;
        public Node next;
    };

    /* Given a reference (pointer to pointer) to the head
    of a list and an int, push a new node on the front
    of the list. */
    static Node push(Node head_ref, int new_data)
    {
        Node new_node = new Node();
        new_node.data = new_data;
        new_node.next = (head_ref);
        (head_ref) = new_node;
        return head_ref;
    }

    /* Counts no. of nodes in linked list */
    static int getCount(Node head)
    {
        int count = 0; // Initialize count
        Node current = head; // Initialize current
        while (current != null) {
            count++;
            current = current.next;
        }
        return count;
    }

    /* Takes head pointer of the linked list and index
        as arguments and return data at index*/
    static int getNth(Node head, int n)
    {
        Node curr = head;
        for (int i = 0; i < n - 1 && curr != null; i++)
            curr = curr.next;
        return curr.data;
    }

    static void printReverse(Node head)
    {
        // store Node addresses in stack
        Stack<Node> stk = new Stack<Node>();
        Node ptr = head;
        while (ptr != null) {
            stk.Push(ptr);
            ptr = ptr.next;
        }

        // print data from stack
        while (stk.Count > 0) {
            Console.Write(stk.Peek().data + " ");
            stk.Pop(); // pop after print
        }
        Console.WriteLine("\n");
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Start with the empty list
        Node head = null;

        // Use push() to con below list
        // 1.2.3.4.5
        head = push(head, 5);
        head = push(head, 4);
        head = push(head, 3);
        head = push(head, 2);
        head = push(head, 1);

        // Function call
        printReverse(head);
    }
}

// This code is contributed by Rajput-Ji

```

**Output**

```
5 4 3 2 1 

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。