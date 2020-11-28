# 使用递归

> 原文：[https://www.geeksforgeeks.org/delete-nodes-which-have-a-greater-value-on-right-side-using-recursion/](https://www.geeksforgeeks.org/delete-nodes-which-have-a-greater-value-on-right-side-using-recursion/)

删除右侧值较大的节点

给定一个单链表，请删除右侧所有具有较大值的所有节点。

**示例**：

a）列表`12 -> 15 -> 10 -> 11 -> 5 -> 6 -> 2 -> 3 -> NULL`应更改为`15 -> 11 -> 6 -> 3 -> NULL`。 请注意，已删除 12、10、5 和 2，因为右侧的值更大。

当我们检查 12 时，我们发现在 12 之后有一个值大于 12（即 15）的节点，因此我们删除了 12。

当我们检查 15 时，我们发现在 15 之后没有节点的值大于 12。 15，所以我们保留此节点。

这样下去，我们得到`15 -> 6 -> 3`

b）列表`10 -> 20 -> 30 -> 40 -> 50 -> 60 -> NULL`应该更改为`60 -> NULL`。 请注意，已删除 10、20、30、40 和 50，因为它们在右侧都具有较大的值。

c）列表`60 -> 50 -> 40 -> 30 -> 20 -> 10 -> NULL`不应更改。

**方法**：[在删除右侧具有较大值的节点的帖子中](https://www.geeksforgeeks.org/delete-nodes-which-have-a-greater-value-on-right-side/)，我们已经通过使用 2 个循环并反转的链表来解决此问题。

在这里，我们将讨论解决方案，而无需反转列表。 我们将使用递归来解决此问题，其中基本情况是当头部指向`NULL`时。 否则，如果`currentNode->data > currentMax`，我们将递归调用下一个节点的函数并更新最大值。 这样，整个列表将被更新。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

/* structure of a linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/*Utility function to find maximum value*/
int maxVal(int a, int b) 
{ 
    if (a > b) 
        return a; 
    return b; 
} 

/* Function to delete nodes which have  
a node with greater value node  
on left side */
struct Node* delNodes(struct Node* head, int* max) 
{ 

    // Base case 
    if (head == NULL) { 
        return head; 
    } 

    head->next = delNodes(head->next, max); 
    if (head->data < *max) { 
        return head->next; 
    } 
    *max = maxVal(head->data, *max); 
    return head; 
} 

/* Utility function to insert a node at the beginning */
void push(struct Node** head, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head; 
    *head = new_node; 
} 

/* Utility function to print a linked list */
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 

/* Driver program to test above functions */
int main() 
{ 
    struct Node* head = NULL; 

    /* Create following linked list  
    12->15->10->11->5->6->2->3 */
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 11); 
    push(&head, 10); 
    push(&head, 15); 
    push(&head, 12); 

    cout << "Given Linked List" << endl; 
    printList(head); 
    int max = INT_MIN; 
    head = delNodes(head, &max); 

    cout << "Modified Linked List" << endl; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
class GFG  
{ 

/* structure of a linked list node */
static class Node 
{  
    int data;  
    Node next;  
};  
static Node head; 
static int max; 

/*Utility function to find maximum value*/
static int maxVal(int a, int b)  
{  
    if (a > b)  
        return a;  
    return b;  
}  

/* Function to delete nodes which have  
a node with greater value node  
on left side */
static Node delNodes(Node head)  
{  

    // Base case  
    if (head == null)  
    {  
        return head;  
    }  

    head.next = delNodes(head.next);  
    if (head.data < max) 
    {  
        return head.next;  
    }  
    max = maxVal(head.data, max);  
    return head;  
}  

/* Utility function to insert a node 
at the beginning */
static void push(Node head_ref,  
                 int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
        head = head_ref; 
}  

/* Utility function to print a linked list */
static void printList(Node head)  
{  
    while (head != null)  
    {  
        System.out.print(head.data + " ");  
        head = head.next;  
    }  
    System.out.println();  
}  

// Driver Code 
public static void main(String[] args)  
{ 
    head = null;  

    /* Create following linked list  
    12.15.10.11.5.6.2.3 */
    push(head, 3);  
    push(head, 2);  
    push(head, 6);  
    push(head, 5);  
    push(head, 11);  
    push(head, 10);  
    push(head, 15);  
    push(head, 12);  

    System.out.println("Given Linked List");  
    printList(head);  
    max = Integer.MIN_VALUE;  
    head = delNodes(head);  

    System.out.println("Modified Linked List");  
    printList(head); 
} 
}  

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to reverse a linked 
# list using a stack  

# Link list node  
class Node: 

    def __init__(self, data, next): 
        self.data = data 
        self.next = next

class LinkedList: 

    def __init__(self): 
        self.head = None

    # Function to push a new Node in 
    # the linked list  
    def push(self, new_data):  

        new_node = Node(new_data, self.head)  
        self.head = new_node 

    # Function to delete nodes which have a node 
    # with greater value node on left side 
    def delNodes(self, head):  

        # Base case  
        if head == None:  
            return head 

        global Max

        head.next = self.delNodes(head.next) 
        if head.data < Max:  
            return head.next

        Max = max(head.data, Max)  
        return head  

    # Function to print the Linked list  
    def printList(self): 

        curr = self.head 
        while curr:  
            print(curr.data, end = " ")  
            curr = curr.next
        print() 

# Driver Code  
if __name__ == "__main__": 

    # Start with the empty list 
    linkedList = LinkedList()  

    # Create following linked list  
    # 12->15->10->11->5->6->2->3  
    linkedList.push(3)  
    linkedList.push(2)  
    linkedList.push(6)  
    linkedList.push(5)  
    linkedList.push(11)  
    linkedList.push(10)  
    linkedList.push(15)  
    linkedList.push(12)  

    print("Given Linked List") 
    linkedList.printList()  
    Max = float('-inf') 
    linkedList.head = linkedList.delNodes(linkedList.head) 

    print("Modified Linked List") 

    linkedList.printList()  

# This code is contributed by Rituraj Jain  

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG  
{ 

/* structure of a linked list node */
public class Node 
{  
    public int data;  
    public Node next;  
};  
static Node head; 
static int max; 

/*Utility function to find maximum value*/
static int maxVal(int a, int b)  
{  
    if (a > b)  
        return a;  
    return b;  
}  

/* Function to delete nodes which have  
a node with greater value node  
on left side */
static Node delNodes(Node head)  
{  

    // Base case  
    if (head == null)  
    {  
        return head;  
    }  

    head.next = delNodes(head.next);  
    if (head.data < max) 
    {  
        return head.next;  
    }  
    max = maxVal(head.data, max);  
    return head;  
}  

/* Utility function to insert a node 
at the beginning */
static void push(Node head_ref,  
                 int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
        head = head_ref; 
}  

/* Utility function to print a linked list */
static void printList(Node head)  
{  
    while (head != null)  
    {  
        Console.Write(head.data + " ");  
        head = head.next;  
    }  
    Console.WriteLine();  
}  

// Driver Code 
public static void Main(String[] args)  
{ 
    head = null;  

    /* Create following linked list  
    12.15.10.11.5.6.2.3 */
    push(head, 3);  
    push(head, 2);  
    push(head, 6);  
    push(head, 5);  
    push(head, 11);  
    push(head, 10);  
    push(head, 15);  
    push(head, 12);  

    Console.WriteLine("Given Linked List");  
    printList(head);  
    max = int.MinValue;  
    head = delNodes(head);  

    Console.WriteLine("Modified Linked List");  
    printList(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Given Linked List
12 15 10 11 5 6 2 3 
Modified Linked List
15 11 6 3

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。