# 使用递归

从中间到左右顺序遍历链接列表

给定一个链表。 任务是使用递归从中间顺序到左右顺序遍历链接列表。

**例如：**

> 如果给定的链表是：2-> 5-> 8-> 3-> 7-> 9-> 12-> NULL
> 中间到左右顺序是：3、8、7、5、9 ，2，12

**说明：**给定链表的中间是'3'，因此，我们从中间开始依次打印3，然后在3的左边和右边进行遍历，因此我们打印8、7，然后打印8的左边和7的右边 ，因此我们打印5、9，然后向左打印5，向右打印9，因此我们打印2、12。

**注意：**如果“链表”中的节点数为偶数，则仅左右打印。 对于此链接列表（包含偶数个节点）2-> 5-> 8-> 7-> 9-> 12->为空。

输出应为8、7、5、9、2、12。

**示例：**

> **输入：** 20-> 15-> 23-> 13-> 19-> 32-> 16-> 41-> 11- > NULL
> **输出：** 19、13、32、23、16、15、41、20、11。
> 
> **输入：** 12-> 25-> 51-> 16-> 9-> 90-> 7-> 2->空
> **输出：** 16，9，51，90，25，7，12，2。

**方法：**

首先，计算链表的大小：

*   如果大小为奇数：
    ->然后使用递归转到第（n + 1）/ 2个节点。
*   如果大小为偶数：
    ->然后使用递归转到第n / 2个节点。
*   现在打印节点数据并返回下一个节点地址，除非函数调用堆栈为空，否则请执行此步骤。

下面是上述方法的实现：

## C++

```cpp

// A C++ program to demonstrate 
// the printing of Linked List middle 
// to left right order 

#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
class Node { 
public: 
    int data; 
    Node* next; 
}; 

// Given a reference (pointer to pointer) 
// to the head of a list and an int, appends 
// a new node at the end 

void append(Node** head_ref, int new_data) 
{ 
    // Allocate node 
    Node* new_node = new Node(); 

    // Used in step 5 
    Node* last = *head_ref; 

    // Put in the data 
    new_node->data = new_data; 

    // This new node is going to be 
    // the last node, so make next of 
    // it as NULL 
    new_node->next = NULL; 

    // If the Linked List is empty, 
    // then make the new node as head 
    if (*head_ref == NULL) { 
        *head_ref = new_node; 
        return; 
    } 

    // Else traverse till the last node 
    while (last->next != NULL) 
        last = last->next; 

    // Change the next of last node 
    last->next = new_node; 
    return; 
} 

// This function prints contents of 
// linked list starting from head 

void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << " " << node->data; 

        if (node->next != NULL) 
            cout << "->"; 
        node = node->next; 
    } 
} 

// Function to get the size of linked list 
int getSize(Node* head) 
{ 
    if (head == NULL) 
        return 0; 
    return 1 + getSize(head->next); 
} 

// Utility function to print the Linked List 
// from middle to left right order 
Node* printMiddleToLeftRightUtil(Node* head, 
                                 int counter, int lSize) 
{ 
    // Base Condition 
    // When size of list is odd 
    if (counter == 1 && lSize % 2 != 0) { 

        // Print node value 
        cout << head->data; 

        // Returns address of next node 
        return head->next; 
    } 

    // Base Condition 
    // When size of list is even 
    else if (counter == 1) { 

        // Print node value 
        // and next node value 
        cout << head->data; 
        cout << " , " << head->next->data; 

        // Returns address of next to next node 
        return head->next->next; 
    } 
    else { 

        // Recursive function call and 
        // store return address 
        Node* ptr = printMiddleToLeftRightUtil( 
            head->next, 
            counter - 1, 
            lSize); 

        // Print head data 
        cout << " , " << head->data; 

        // Print ptr data 
        cout << " , " << ptr->data; 

        // Returns address of next node 
        return ptr->next; 
    } 
} 

// Function to print Middle to 
// Left-right order 
void printMiddleToLeftRight(Node* head) 
{ 
    // Function call to get the size 
    // Of Linked List 
    int listSize = getSize(head); 

    int middle = 0; 

    // Store middle when Linked 
    // List size is odd 
    if (listSize % 2 != 0) { 
        middle = (listSize + 1) / 2; 
    } 

    // Store middle when Linked 
    // List size is even 

    else { 
        middle = listSize / 2; 
    } 

    // Utility function call print 
    // Linked List from Middle 
    // to left right order 
    cout << "Output : "; 

    printMiddleToLeftRightUtil(head, 
                               middle, 
                               listSize); 
} 

// Driver code 
int main() 
{ 
    // Start with the empty list 
    Node* head = NULL; 

    // Insert 6\. So linked list 
    // becomes 6->NULL 
    append(&head, 6); 

    // Insert 6\. So linked list 
    // becomes 6->4->NULL 
    append(&head, 4); 
    append(&head, 8); 
    append(&head, 7); 
    append(&head, 9); 
    append(&head, 11); 
    append(&head, 2); 

    // After inserting linked list 
    // becomes 6->4->8->7->9->11->2->NULL 
    cout << "Created Linked list is: "; 

    // Function to display Linked List content 
    printList(head); 
    cout << endl; 

    // Function call print Linked List from 
    // Middle to left right order 
    printMiddleToLeftRight(head); 
    return 0; 
} 

```

## Java

```java

// A Java program to demonstrate 
// the printing of Linked List middle 
// to left right order 
class GFG 
{ 

// A linked list node 
static class Node 
{ 
    int data; 
    Node next; 
}; 

// Given a reference (pointer to pointer) 
// to the head of a list and an int, appends 
// a new node at the end 
static Node append(Node head_ref, int new_data) 
{ 
    // Allocate node 
    Node new_node = new Node(); 

    // Used in step 5 
    Node last = head_ref; 

    // Put in the data 
    new_node.data = new_data; 

    // This new node is going to be 
    // the last node, so make next of 
    // it as null 
    new_node.next = null; 

    // If the Linked List is empty, 
    // then make the new node as head 
    if (head_ref == null) 
    { 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Else traverse till the last node 
    while (last.next != null) 
        last = last.next; 

    // Change the next of last node 
    last.next = new_node; 
    return head_ref; 
} 

// This function prints contents of 
// linked list starting from head 
static void printList(Node node) 
{ 
    while (node != null)  
    { 
        System.out.print( " " + node.data); 

        if (node.next != null) 
            System.out.print("->"); 
        node = node.next; 
    } 
} 

// Function to get the size of linked list 
static int getSize(Node head) 
{ 
    if (head == null) 
        return 0; 
    return 1 + getSize(head.next); 
} 

// Utility function to print the Linked List 
// from middle to left right order 
static Node printMiddleToLeftRightUtil(Node head, 
                          int counter, int lSize) 
{ 
    // Base Condition 
    // When size of list is odd 
    if (counter == 1 && lSize % 2 != 0) 
    { 

        // Print node value 
        System.out.print( head.data); 

        // Returns address of next node 
        return head.next; 
    } 

    // Base Condition 
    // When size of list is even 
    else if (counter == 1) 
    { 

        // Print node value 
        // and next node value 
        System.out.print(head.data); 
        System.out.print( " , " + head.next.data); 

        // Returns address of next to next node 
        return head.next.next; 
    } 
    else 
    { 

        // Recursive function call and 
        // store return address 
        Node ptr = printMiddleToLeftRightUtil(head.next,  
                                    counter - 1, lSize); 

        // Print head data 
        System.out.print(" , " + head.data); 

        // Print ptr data 
        System.out.print(" , " + ptr.data); 

        // Returns address of next node 
        return ptr.next; 
    } 
} 

// Function to print Middle to 
// Left-right order 
static void printMiddleToLeftRight(Node head) 
{ 
    // Function call to get the size 
    // Of Linked List 
    int listSize = getSize(head); 

    int middle = 0; 

    // Store middle when Linked 
    // List size is odd 
    if (listSize % 2 != 0)  
    { 
        middle = (listSize + 1) / 2; 
    } 

    // Store middle when Linked 
    // List size is even 
    else 
    { 
        middle = listSize / 2; 
    } 

    // Utility function call print 
    // Linked List from Middle 
    // to left right order 
    System.out.print("Output : "); 

    printMiddleToLeftRightUtil(head, middle, listSize); 
} 

// Driver code 
public static void main(String args[]) 
{ 
    // Start with the empty list 
    Node head = null; 

    // Insert 6\. So linked list 
    // becomes 6.null 
    head = append(head, 6); 

    // Insert 6\. So linked list 
    // becomes 6.4.null 
    head = append(head, 4); 
    head = append(head, 8); 
    head = append(head, 7); 
    head = append(head, 9); 
    head = append(head, 11); 
    head = append(head, 2); 

    // After inserting linked list 
    // becomes 6.4.8.7.9.11.2.null 
    System.out.print("Created Linked list is: "); 

    // Function to display Linked List content 
    printList(head); 
    System.out.println(); 

    // Function call print Linked List from 
    // Middle to left right order 
    printMiddleToLeftRight(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// A C# program to demonstrate 
// the printing of Linked List middle 
// to left right order 
using System; 

public class GFG 
{ 

// A linked list node 
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Given a reference (pointer to pointer) 
// to the head of a list and an int, appends 
// a new node at the end 
static Node append(Node head_ref, int new_data) 
{ 
    // Allocate node 
    Node new_node = new Node(); 

    // Used in step 5 
    Node last = head_ref; 

    // Put in the data 
    new_node.data = new_data; 

    // This new node is going to be 
    // the last node, so make next of 
    // it as null 
    new_node.next = null; 

    // If the Linked List is empty, 
    // then make the new node as head 
    if (head_ref == null) 
    { 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Else traverse till the last node 
    while (last.next != null) 
        last = last.next; 

    // Change the next of last node 
    last.next = new_node; 
    return head_ref; 
} 

// This function prints contents of 
// linked list starting from head 
static void printList(Node node) 
{ 
    while (node != null)  
    { 
        Console.Write( " " + node.data); 

        if (node.next != null) 
            Console.Write("->"); 
        node = node.next; 
    } 
} 

// Function to get the size of linked list 
static int getSize(Node head) 
{ 
    if (head == null) 
        return 0; 
    return 1 + getSize(head.next); 
} 

// Utility function to print the Linked List 
// from middle to left right order 
static Node printMiddleToLeftRightUtil(Node head, 
                          int counter, int lSize) 
{ 
    // Base Condition 
    // When size of list is odd 
    if (counter == 1 && lSize % 2 != 0) 
    { 

        // Print node value 
        Console.Write( head.data); 

        // Returns address of next node 
        return head.next; 
    } 

    // Base Condition 
    // When size of list is even 
    else if (counter == 1) 
    { 

        // Print node value 
        // and next node value 
        Console.Write(head.data); 
        Console.Write( " , " + head.next.data); 

        // Returns address of next to next node 
        return head.next.next; 
    } 
    else
    { 

        // Recursive function call and 
        // store return address 
        Node ptr = printMiddleToLeftRightUtil(head.next,  
                                    counter - 1, lSize); 

        // Print head data 
        Console.Write(" , " + head.data); 

        // Print ptr data 
        Console.Write(" , " + ptr.data); 

        // Returns address of next node 
        return ptr.next; 
    } 
} 

// Function to print Middle to 
// Left-right order 
static void printMiddleToLeftRight(Node head) 
{ 
    // Function call to get the size 
    // Of Linked List 
    int listSize = getSize(head); 

    int middle = 0; 

    // Store middle when Linked 
    // List size is odd 
    if (listSize % 2 != 0)  
    { 
        middle = (listSize + 1) / 2; 
    } 

    // Store middle when Linked 
    // List size is even 
    else
    { 
        middle = listSize / 2; 
    } 

    // Utility function call print 
    // Linked List from Middle 
    // to left right order 
    Console.Write("Output : "); 

    printMiddleToLeftRightUtil(head, middle, listSize); 
} 

// Driver code 
public static void Main(String []args) 
{ 
    // Start with the empty list 
    Node head = null; 

    // Insert 6\. So linked list 
    // becomes 6.null 
    head = append(head, 6); 

    // Insert 6\. So linked list 
    // becomes 6.4.null 
    head = append(head, 4); 
    head = append(head, 8); 
    head = append(head, 7); 
    head = append(head, 9); 
    head = append(head, 11); 
    head = append(head, 2); 

    // After inserting linked list 
    // becomes 6.4.8.7.9.11.2.null 
    Console.Write("Created Linked list is: "); 

    // Function to display Linked List content 
    printList(head); 
    Console.WriteLine(); 

    // Function call print Linked List from 
    // Middle to left right order 
    printMiddleToLeftRight(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Created Linked list is:  6-> 4-> 8-> 7-> 9-> 11-> 2
Output : 7 , 8 , 9 , 4 , 11 , 6 , 2

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。