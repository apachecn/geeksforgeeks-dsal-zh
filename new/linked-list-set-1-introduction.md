# 链表 | 系列 1（简介）

> 原文：[https://www.geeksforgeeks.org/linked-list-set-1-introduction/](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)

像数组一样，链表是线性数据结构。 与数组不同，链表元素不存储在连续位置； 元素使用指针链接。

![linkedlist](img/d97a233bf3c89e80c46e6a3193e851d6.png)

**为什么选择链表？**

数组可用于存储相似类型的线性数据，但是数组具有以下限制。

1.  数组的大小是固定的：因此，我们必须预先知道元素数量的上限。 而且，通常，所分配的存储器与用途无关而等于上限。

2.  在元素数组中插入新元素非常昂贵，因为必须为新元素创建空间，并且必须移动现有元素来创建空间。

例如，在系统中，如果我们在数组`id[]`中维护 ID 的排序列表。

```
id[] = [1000, 1010, 1050, 2000, 2040]
```

如果要插入新的 ID 1005，则要维持排序顺序，我们必须将所有元素都移到 1000（不包括 1000）之后。

除非使用某些特殊技术，否则数组删除也很昂贵。 例如，要删除`id[]`中的 1010，必须移动 1010 之后的所有内容。

**优于数组**

1.  动态大小

2.  易于插入/删除

**缺点**：

1.  不允许随机访问。 我们必须从第一个节点开始顺序访问元素。 因此，我们无法使用默认实现对链表进行有效的二分搜索。 在上阅读有关它的信息。

2.  列表的每个元素都需要用于指针的额外存储空间。

3.  不适合缓存。 由于数组元素是连续的位置，因此存在引用位置，而在链表的情况下则不存在。

**表示形式**：

链表由指向链表的第一个节点的指针表示。 第一个节点称为`head`。 如果链表为空，则`head`的值为`NULL`。

列表中的每个节点至少包括两部分：

1.  数据

2.  指向下一个节点的指针（或引用）

在 C 语言中，我们可以使用结构表示一个节点。 以下是带有整数数据的链表节点的示例。

在 Java 或 C# 中，`LinkedList`可以表示为一个类，而`Node`可以表示为单独的类。`LinkedList`类包含`Node`类类型的引用。

## C

```c

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

```

## C++

```cpp

class Node { 
public: 
    int data; 
    Node* next; 
}; 

```

## Java

```java

class LinkedList { 
    Node head; // head of the list 

    /* Linked list Node*/
    class Node { 
        int data; 
        Node next; 

        // Constructor to create a new node 
        // Next is by default initialized 
        // as null 
        Node(int d) { data = d; } 
    } 
}

```

## Python

```py

# Node class 
class Node: 

    # Function to initialize the node object 
    def __init__(self, data): 
        self.data = data  # Assign data 
        self.next = None  # Initialize  
                          # next as null 

# Linked List class 
class LinkedList: 

    # Function to initialize the Linked  
    # List object 
    def __init__(self):  
        self.head = None

```

## C#

```cs

class LinkedList { 
    // The first node(head) of the linked list 
    // Will be an object of type Node (null by default) 
    Node head; 

    class Node { 
        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) { data = d; } 
    } 
}

```

**C 中的第一个简单链表**：让我们创建一个包含 3 个节点的简单链表。

## C++

```cpp

// A simple CPP program to introduce 
// a linked list 
#include <bits/stdc++.h> 
using namespace std; 

class Node { 
public: 
    int data; 
    Node* next; 
}; 

// Program to create a simple linked 
// list with 3 nodes 
int main() 
{ 
    Node* head = NULL; 
    Node* second = NULL; 
    Node* third = NULL; 

    // allocate 3 nodes in the heap 
    head = new Node(); 
    second = new Node(); 
    third = new Node(); 

    /* Three blocks have been allocated dynamically.  
    We have pointers to these three blocks as head,  
    second and third      
    head         second         third  
        |             |             |  
        |             |             |  
    +---+-----+     +----+----+     +----+----+  
    | # | # |     | # | # |     | # | # |  
    +---+-----+     +----+----+     +----+----+  

# represents any random value.  
Data is random because we haven't assigned  
anything yet */

    head->data = 1; // assign data in first node 
    head->next = second; // Link first node with 
    // the second node 

    /* data has been assigned to the data part of first  
    block (block pointed by the head). And next  
    pointer of the first block points to second.  
    So they both are linked.  

    head         second         third  
        |             |             |  
        |             |             |  
    +---+---+     +----+----+     +-----+----+  
    | 1 | o----->| # | # |     | # | # |  
    +---+---+     +----+----+     +-----+----+      
*/

    // assign data to second node 
    second->data = 2; 

    // Link second node with the third node 
    second->next = third; 

    /* data has been assigned to the data part of the second  
    block (block pointed by second). And next  
    pointer of the second block points to the third  
    block. So all three blocks are linked.  

    head         second         third  
        |             |             |  
        |             |             |  
    +---+---+     +---+---+     +----+----+  
    | 1 | o----->| 2 | o-----> | # | # |  
    +---+---+     +---+---+     +----+----+     */

    third->data = 3; // assign data to third node 
    third->next = NULL; 

    /* data has been assigned to the data part of the third  
    block (block pointed by third). And next pointer  
    of the third block is made NULL to indicate  
    that the linked list is terminated here.  

    We have the linked list ready.  

        head      
            |  
            |  
        +---+---+     +---+---+     +----+------+  
        | 1 | o----->| 2 | o-----> | 3 | NULL |  
        +---+---+     +---+---+     +----+------+      

    Note that only the head is sufficient to represent  
    the whole list. We can traverse the complete  
    list by following the next pointers. */

    return 0; 
} 

// This code is contributed by rathbhupendra 

```

## C

```c

// A simple C program to introduce 
// a linked list 
#include <stdio.h> 
#include <stdlib.h> 

struct Node { 
    int data; 
    struct Node* next; 
}; 

// Program to create a simple linked 
// list with 3 nodes 
int main() 
{ 
    struct Node* head = NULL; 
    struct Node* second = NULL; 
    struct Node* third = NULL; 

    // allocate 3 nodes in the heap 
    head = (struct Node*)malloc(sizeof(struct Node)); 
    second = (struct Node*)malloc(sizeof(struct Node)); 
    third = (struct Node*)malloc(sizeof(struct Node)); 

    /* Three blocks have been allocated dynamically.  
     We have pointers to these three blocks as head, 
     second and third      
       head           second           third 
        |                |               | 
        |                |               | 
    +---+-----+     +----+----+     +----+----+ 
    | #  | #  |     | #  | #  |     |  # |  # | 
    +---+-----+     +----+----+     +----+----+ 

   # represents any random value. 
   Data is random because we haven't assigned  
   anything yet  */

    head->data = 1; // assign data in first node 
    head->next = second; // Link first node with 
    // the second node 

    /* data has been assigned to the data part of the first 
     block (block pointed by the head). And next 
     pointer of first block points to second.   
     So they both are linked. 

       head          second         third 
        |              |              | 
        |              |              | 
    +---+---+     +----+----+     +-----+----+ 
    | 1  | o----->| #  | #  |     |  #  | #  | 
    +---+---+     +----+----+     +-----+----+     
  */

    // assign data to second node 
    second->data = 2; 

    // Link second node with the third node 
    second->next = third; 

    /* data has been assigned to the data part of the second 
     block (block pointed by second). And next 
     pointer of the second block points to the third  
     block. So all three blocks are linked. 

       head         second         third 
        |             |             | 
        |             |             | 
    +---+---+     +---+---+     +----+----+ 
    | 1  | o----->| 2 | o-----> |  # |  # | 
    +---+---+     +---+---+     +----+----+      */

    third->data = 3; // assign data to third node 
    third->next = NULL; 

    /* data has been assigned to data part of third 
    block (block pointed by third). And next pointer 
    of the third block is made NULL to indicate 
    that the linked list is terminated here. 

     We have the linked list ready.   

           head     
             | 
             |  
        +---+---+     +---+---+       +----+------+ 
        | 1  | o----->|  2  | o-----> |  3 | NULL | 
        +---+---+     +---+---+       +----+------+        

    Note that only head is sufficient to represent  
    the whole list.  We can traverse the complete  
    list by following next pointers.    */

    return 0; 
} 

```

## Java

```java

// A simple Java program to introduce a linked list 
class LinkedList { 
    Node head; // head of list 

    /* Linked list Node.  This inner class is made static so that 
       main() can access it */
    static class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } // Constructor 
    } 

    /* method to create a simple linked list with 3 nodes*/
    public static void main(String[] args) 
    { 
        /* Start with the empty list. */
        LinkedList llist = new LinkedList(); 

        llist.head = new Node(1); 
        Node second = new Node(2); 
        Node third = new Node(3); 

        /* Three nodes have been allocated dynamically. 
          We have references to these three blocks as head,   
          second and third 

          llist.head        second              third 
             |                |                  | 
             |                |                  | 
         +----+------+     +----+------+     +----+------+ 
         | 1  | null |     | 2  | null |     |  3 | null | 
         +----+------+     +----+------+     +----+------+ */

        llist.head.next = second; // Link first node with the second node 

        /*  Now next of the first Node refers to the second.  So they 
            both are linked. 

         llist.head        second              third 
            |                |                  | 
            |                |                  | 
        +----+------+     +----+------+     +----+------+ 
        | 1  |  o-------->| 2  | null |     |  3 | null | 
        +----+------+     +----+------+     +----+------+ */

        second.next = third; // Link second node with the third node 

        /*  Now next of the second Node refers to third.  So all three 
            nodes are linked. 

         llist.head        second              third 
            |                |                  | 
            |                |                  | 
        +----+------+     +----+------+     +----+------+ 
        | 1  |  o-------->| 2  |  o-------->|  3 | null | 
        +----+------+     +----+------+     +----+------+ */
    } 
} 

```

## Python

```py

# A simple Python program to introduce a linked list 

# Node class 
class Node: 

    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data  # Assign data 
        self.next = None  # Initialize next as null 

# Linked List class contains a Node object 
class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

# Code execution starts here 
if __name__=='__main__': 

    # Start with the empty list 
    llist = LinkedList() 

    llist.head = Node(1) 
    second = Node(2) 
    third = Node(3) 

    ''' 
    Three nodes have been created. 
    We have references to these three blocks as head, 
    second and third 

    llist.head        second              third 
         |                |                  | 
         |                |                  | 
    +----+------+     +----+------+     +----+------+ 
    | 1  | None |     | 2  | None |     |  3 | None | 
    +----+------+     +----+------+     +----+------+ 
    '''

    llist.head.next = second; # Link first node with second  

    ''' 
    Now next of first Node refers to second.  So they 
    both are linked. 

    llist.head        second              third 
         |                |                  | 
         |                |                  | 
    +----+------+     +----+------+     +----+------+ 
    | 1  |  o-------->| 2  | null |     |  3 | null | 
    +----+------+     +----+------+     +----+------+  
    '''

    second.next = third; # Link second node with the third node 

    ''' 
    Now next of second Node refers to third.  So all three 
    nodes are linked. 

    llist.head        second              third 
         |                |                  | 
         |                |                  | 
    +----+------+     +----+------+     +----+------+ 
    | 1  |  o-------->| 2  |  o-------->|  3 | null | 
    +----+------+     +----+------+     +----+------+  
    '''

```

## C#

```cs

// A simple C# program to introduce a linked list 
using System; 

public class LinkedList { 
    Node head; // head of list 

    /* Linked list Node. This inner class is made static so that  
    main() can access it */
    public class Node { 
        public int data; 
        public Node next; 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } // Constructor 
    } 

    /* method to create a simple linked list with 3 nodes*/
    public static void Main(String[] args) 
    { 
        /* Start with the empty list. */
        LinkedList llist = new LinkedList(); 

        llist.head = new Node(1); 
        Node second = new Node(2); 
        Node third = new Node(3); 

        /* Three nodes have been allocated dynamically.  
        We have references to these three blocks as head,  
        second and third  

        llist.head     second             third  
            |             |                 |  
            |             |                 |  
        +----+------+     +----+------+     +----+------+  
        | 1 | null |     | 2 | null |     | 3 | null |  
        +----+------+     +----+------+     +----+------+ */

        llist.head.next = second; // Link first node with the second node 

        /* Now next of first Node refers to second. So they  
            both are linked.  

        llist.head     second             third  
            |             |                 |  
            |             |                 |  
        +----+------+     +----+------+     +----+------+  
        | 1 | o-------->| 2 | null |     | 3 | null |  
        +----+------+     +----+------+     +----+------+ */

        second.next = third; // Link second node with the third node 

        /* Now next of the second Node refers to third. So all three  
            nodes are linked.  

        llist.head     second             third  
            |             |                 |  
            |             |                 |  
        +----+------+     +----+------+     +----+------+  
        | 1 | o-------->| 2 | o-------->| 3 | null |  
        +----+------+     +----+------+     +----+------+ */
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**链表遍历**

在上一个程序中，我们创建了一个包含三个节点的简单链表。 让我们遍历创建的列表并打印每个节点的数据。 为了遍历，让我们编写一个通用函数`printList()`，该函数打印任何给定的列表。

## C++

```cpp

// A simple C++ program for traversal of a linked list 
#include <bits/stdc++.h> 
using namespace std; 

class Node { 
public: 
    int data; 
    Node* next; 
}; 

// This function prints contents of linked list 
// starting from the given node 
void printList(Node* n) 
{ 
    while (n != NULL) { 
        cout << n->data << " "; 
        n = n->next; 
    } 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 
    Node* second = NULL; 
    Node* third = NULL; 

    // allocate 3 nodes in the heap 
    head = new Node(); 
    second = new Node(); 
    third = new Node(); 

    head->data = 1; // assign data in first node 
    head->next = second; // Link first node with second 

    second->data = 2; // assign data to second node 
    second->next = third; 

    third->data = 3; // assign data to third node 
    third->next = NULL; 

    printList(head); 

    return 0; 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c

// A simple C program for traversal of a linked list 
#include <stdio.h> 
#include <stdlib.h> 

struct Node { 
    int data; 
    struct Node* next; 
}; 

// This function prints contents of linked list starting from 
// the given node 
void printList(struct Node* n) 
{ 
    while (n != NULL) { 
        printf(" %d ", n->data); 
        n = n->next; 
    } 
} 

int main() 
{ 
    struct Node* head = NULL; 
    struct Node* second = NULL; 
    struct Node* third = NULL; 

    // allocate 3 nodes in the heap 
    head = (struct Node*)malloc(sizeof(struct Node)); 
    second = (struct Node*)malloc(sizeof(struct Node)); 
    third = (struct Node*)malloc(sizeof(struct Node)); 

    head->data = 1; // assign data in first node 
    head->next = second; // Link first node with second 

    second->data = 2; // assign data to second node 
    second->next = third; 

    third->data = 3; // assign data to third node 
    third->next = NULL; 

    printList(head); 

    return 0; 
}

```

## Java

```java

// A simple Java program for traversal of a linked list 
class LinkedList { 
    Node head; // head of list 

    /* Linked list Node.  This inner class is made static so that 
       main() can access it */
    static class Node { 
        int data; 
        Node next; 
        Node(int d) 
        { 
            data = d; 
            next = null; 
        } // Constructor 
    } 

    /* This function prints contents of linked list starting from head */
    public void printList() 
    { 
        Node n = head; 
        while (n != null) { 
            System.out.print(n.data + " "); 
            n = n.next; 
        } 
    } 

    /* method to create a simple linked list with 3 nodes*/
    public static void main(String[] args) 
    { 
        /* Start with the empty list. */
        LinkedList llist = new LinkedList(); 

        llist.head = new Node(1); 
        Node second = new Node(2); 
        Node third = new Node(3); 

        llist.head.next = second; // Link first node with the second node 
        second.next = third; // Link second node with the third node 

        llist.printList(); 
    } 
}

```

## Python3

```py

# A simple Python program for traversal of a linked list 

# Node class 
class Node: 

    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data  # Assign data 
        self.next = None  # Initialize next as null 

# Linked List class contains a Node object 
class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # This function prints contents of linked list 
    # starting from head 
    def printList(self): 
        temp = self.head 
        while (temp): 
            print (temp.data) 
            temp = temp.next

# Code execution starts here 
if __name__=='__main__': 

    # Start with the empty list 
    llist = LinkedList() 

    llist.head = Node(1) 
    second = Node(2) 
    third = Node(3) 

    llist.head.next = second; # Link first node with second 
    second.next = third; # Link second node with the third node 

    llist.printList() 

```

## C#

```cs

// A simple C# program for traversal of a linked list 
using System; 

public class LinkedList { 
    Node head; // head of list 

    /* Linked list Node. This inner  
    class is made static so that 
    main() can access it */
    public class Node { 
        public int data; 
        public Node next; 
        public Node(int d) 
        { 
            data = d; 
            next = null; 

        } // Constructor 
    } 

    /* This function prints contents of  
    linked list starting from head */
    public void printList() 
    { 
        Node n = head; 
        while (n != null) { 
            Console.Write(n.data + " "); 
            n = n.next; 
        } 
    } 

    /* method to create a simple linked list with 3 nodes*/
    public static void Main(String[] args) 
    { 
        /* Start with the empty list. */
        LinkedList llist = new LinkedList(); 

        llist.head = new Node(1); 
        Node second = new Node(2); 
        Node third = new Node(3); 

        llist.head.next = second; // Link first node with the second node 
        second.next = third; // Link second node with the third node 

        llist.printList(); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
 1  2  3
```

**重要链接**：

*   [在链表上练习 MCQ 问题](http://quiz.geeksforgeeks.org/data-structure/linked-list/)

*   [链表数据结构页面](https://www.geeksforgeeks.org/data-structures/linked-list/)

*   [链表上的编码实践问题](https://practice.geeksforgeeks.org/topics/Linked%20List/)

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

