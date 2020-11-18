# 在链接列表

> 原文：[https://www.geeksforgeeks.org/find-length-of-loop-in-linked-list/](https://www.geeksforgeeks.org/find-length-of-loop-in-linked-list/)

中查找循环长度

编写一个函数 *detectAndCountLoop（）*，该函数检查给定的链表是否包含循环，如果存在循环，则返回循环中的节点数。 例如，该循环存在于以下链接的列表中，并且循环的长度为 4。如果不存在该循环，则该函数应返回 0。

[![](img/de522899e01a1322ab2808eeff1ad73e.png "Linked List Loop")](https://media.geeksforgeeks.org/wp-content/cdn-uploads/2009/04/Linked-List-Loop.gif)

<u>**方法**</u> ：众所周知，当快速指针和慢速指针在同一点相遇时，[弗洛伊德循环检测算法](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)终止。 还已知该公共点是循环节点之一。 将此公共点的地址存储在指针变量 say（ptr）中。 然后用 1 初始化一个计数器，并从公共点开始，继续访问下一个节点并增加计数器，直到再次到达公共指针为止。

此时，计数器的值将等于循环的长度。

**算法**：

1.  使用 [Floyd 的循环检测算法](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)查找循环中的公共点

2.  将指针存储在一个临时变量中，并保持*计数= 0*

3.  遍历链接列表，直到再次到达同一节点，并在移至下一个节点时增加计数。

4.  将计数打印为循环长度

## C++

```cpp

// C++ program to count number of nodes  
// in loop in a linked list if loop is  
// present  
#include<bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node  
{  
    int data;  
    struct Node* next;  
};  

// Returns count of nodes present in loop.  
int countNodes(struct Node *n)  
{  
    int res = 1;  
    struct Node *temp = n;  
    while (temp->next != n)  
    {  
        res++;  
        temp = temp->next;  
    }  
    return res;  
}  

/* This function detects and counts loop  
nodes in the list. If loop is not there  
in then returns 0 */
int countNodesinLoop(struct Node *list)  
{  
    struct Node *slow_p = list, *fast_p = list;  

    while (slow_p && fast_p &&  
                     fast_p->next)  
    {  
        slow_p = slow_p->next;  
        fast_p = fast_p->next->next;  

        /* If slow_p and fast_p meet at  
        some point then there is a loop */
        if (slow_p == fast_p)  
            return countNodes(slow_p);  
    }  

    /* Return 0 to indeciate that  
       their is no loop*/
    return 0;  
}  

struct Node *newNode(int key)  
{  
    struct Node *temp =  
   (struct Node*)malloc(sizeof(struct Node));  
    temp->data = key;  
    temp->next = NULL;  
    return temp;  
}  

// Driver Code 
int main()  
{  
    struct Node *head = newNode(1);  
    head->next = newNode(2);  
    head->next->next = newNode(3);  
    head->next->next->next = newNode(4);  
    head->next->next->next->next = newNode(5);  

    /* Create a loop for testing */
    head->next->next->next->next->next = head->next;  

    cout << countNodesinLoop(head) << endl;  

    return 0;  
}  

// This code is contributed by SHUBHAMSINGH10 

```

## C

```c

// C program to count number of nodes 
// in loop in a linked list if loop is 
// present 
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// Returns count of nodes present in loop. 
int countNodes(struct Node *n) 
{ 
   int res = 1; 
   struct Node *temp = n; 
   while (temp->next != n) 
   { 
      res++; 
      temp = temp->next; 
   } 
   return res; 
} 

/* This function detects and counts loop 
   nodes in the list. If loop is not there 
   in then returns 0 */
int countNodesinLoop(struct Node *list) 
{ 
    struct Node  *slow_p = list, *fast_p = list; 

    while (slow_p && fast_p && fast_p->next) 
    { 
        slow_p = slow_p->next; 
        fast_p  = fast_p->next->next; 

        /* If slow_p and fast_p meet at some point 
           then there is a loop */
        if (slow_p == fast_p) 
            return countNodes(slow_p); 
    } 

    /* Return 0 to indeciate that ther is no loop*/
    return 0; 
} 

struct Node *newNode(int key) 
{ 
    struct Node *temp = 
        (struct Node*)malloc(sizeof(struct Node)); 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above function*/
int main() 
{ 
    struct Node *head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 

    /* Create a loop for testing */
    head->next->next->next->next->next = head->next; 

    printf("%d \n", countNodesinLoop(head)); 

    return 0; 
} 

```

## Java

```java

// Java program to count number of nodes  
// in loop in a linked list if loop is  
// present  
import java.io.*; 

class GFG { 

/* Link list node */
static class Node  
{  
    int data; 
    Node next; 
    Node(int data) 
    { 
        this.data =data; 
        next =null; 
    } 
} 

// Returns count of nodes present in loop.  
static int countNodes( Node n)  
{  
int res = 1;  
Node temp = n;  
while (temp.next != n)  
{  
    res++;  
    temp = temp.next;  
}  
return res;  
}  

/* This function detects and counts loop  
nodes in the list. If loop is not there  
in then returns 0 */
static int countNodesinLoop( Node list)  
{  
    Node slow_p = list, fast_p = list;  

    while (slow_p !=null && fast_p!=null && fast_p.next!=null)  
    {  
        slow_p = slow_p.next;  
        fast_p = fast_p.next.next;  

        /* If slow_p and fast_p meet at some point  
        then there is a loop */
        if (slow_p == fast_p)  
            return countNodes(slow_p);  
    }  

    /* Return 0 to indeciate that ther is no loop*/
    return 0;  
}  

static Node newNode(int key)  
{  
    Node temp = new Node(key); 

    return temp;  
}  

/* Driver program to test above function*/
    public static void main (String[] args) { 
        Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(5);  

    /* Create a loop for testing */
    head.next.next.next.next.next = head.next;  

    System.out.println( countNodesinLoop(head));  
    } 
} 
// This code is contributed by inder_verma. 

```

## Python3

```py

# Python 3 program to find the number 
# of nodes in looop in a linked list  
# if loop is present 

# Python Code to detect a loop and  
# find the length of the loop 
# Node defining class 
class Node: 

    # Function to make a node 
    def __init__(self, val): 
        self.val = val 
        self.next = None

# Linked List defining and loop  
# length finding class  
class LinkedList: 

    # Function to initialize the  
    # head of the linked list 
    def __init__(self): 
        self.head = None        

    # Function to insert a new  
    # node at the end  
    def AddNode(self, val): 
        if self.head is None: 
            self.head = Node(val) 
        else: 
            curr = self.head 
            while(curr.next): 
                curr = curr.next
            curr.next = Node(val) 

    # Function to create a loop in the  
    # Linked List. This function creates  
    # a loop by connnecting the last node  
    # to n^th node of the linked list,  
    # (counting first node as 1) 
    def CreateLoop(self, n): 

        # LoopNode is the connecting node to 
        # the last node of linked list 
        LoopNode = self.head 
        for _ in range(1, n): 
            LoopNode = LoopNode.next

        # end is the last node of the Linked List 
        end = self.head 
        while(end.next): 
            end = end.next

        # Creating the loop 
        end.next = LoopNode 

    # Function to detect the loop and return 
    # the length of the loop if the returned  
    # value is zero, that means that either  
    # the linked list is empty or the linked  
    # list doesn't have any loop 
    def detectLoop(self): 

        # if linked list is empty then there  
        # is no loop, so return 0 
        if self.head is None: 
            return 0

        # Using Floyd’s Cycle-Finding  
        # Algorithm/ Slow-Fast Pointer Method 
        slow = self.head 
        fast = self.head 
        flag = 0 # to show that both slow and fast  
                 # are at start of the Linked List 
        while(slow and slow.next and fast and
              fast.next and fast.next.next): 
            if slow == fast and flag != 0: 

                # Means loop is confirmed in the  
                # Linked List. Now slow and fast  
                # are both at the same node which 
                # is part of the loop 
                count = 1
                slow = slow.next
                while(slow != fast): 
                    slow = slow.next
                    count += 1
                return count 

            slow = slow.next
            fast = fast.next.next
            flag = 1
        return 0 # No loop 

# Setting up the code 
# Making a Linked List and adding the nodes 
myLL = LinkedList() 
myLL.AddNode(1) 
myLL.AddNode(2) 
myLL.AddNode(3) 
myLL.AddNode(4) 
myLL.AddNode(5) 

# Creating a loop in the linked List 
# Loop is created by connecting the  
# last node of linked list to n^th node 
# 1<= n <= len(LinkedList) 
myLL.CreateLoop(2) 

# Checking for Loop in the Linked List  
# and printing the length of the loop 
loopLength = myLL.detectLoop() 
if myLL.head is None: 
    print("Linked list is empty") 
else: 
    print(str(loopLength)) 

# This code is contributed by _Ashutosh 

```

## C#

```cs

// C# program to count number of nodes  
// in loop in a linked list if loop is  
// present  
using System; 

class GFG  
{ 

    /* Link list node */
    class Node  
    {  
        public int data; 
        public Node next; 
        public Node(int data) 
        { 
            this.data = data; 
            next = null; 
        } 
    } 

    // Returns count of nodes present in loop.  
    static int countNodes( Node n)  
    {  
        int res = 1;  
        Node temp = n;  
        while (temp.next != n)  
        {  
            res++;  
            temp = temp.next;  
        }  
        return res;  
    }  

    /* This function detects and counts loop  
    nodes in the list. If loop is not there  
    in then returns 0 */
    static int countNodesinLoop( Node list)  
    {  
        Node slow_p = list, fast_p = list;  

        while (slow_p != null && fast_p != null && 
                            fast_p.next != null)  
        {  
            slow_p = slow_p.next;  
            fast_p = fast_p.next.next;  

            /* If slow_p and fast_p meet at some point  
            then there is a loop */
            if (slow_p == fast_p)  
                return countNodes(slow_p);  
        }  

        /* Return 0 to indeciate that ther is no loop*/
        return 0;  
    }  

    static Node newNode(int key)  
    {  
        Node temp = new Node(key); 

        return temp;  
    }  

    /* Driver code*/
    public static void Main (String[] args)  
    { 
        Node head = newNode(1);  
        head.next = newNode(2);  
        head.next.next = newNode(3);  
        head.next.next.next = newNode(4);  
        head.next.next.next.next = newNode(5);  

        /* Create a loop for testing */
        head.next.next.next.next.next = head.next;  

        Console.WriteLine( countNodesinLoop(head));  
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output :**

```
4
```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    只需遍历链接列表。

*   **辅助空间**：`O(1)`。

    由于不需要额外的空间。

**相关文章**：

*   [检测到链表](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)中的循环

*   [检测并删除链接列表中的循环](https://www.geeksforgeeks.org/detect-and-remove-loop-in-a-linked-list/)

本文由 **Shubham Gupta** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

