# 将一个数字添加到一个表示为链表的数字| 设置 2

给定一个表示一个数字的单链表，其中每个节点仅包含一个数字 **[0 – 9]** 。 任务是将 **1** 添加到给定链表表示的号码中，并打印新链表。

**示例：**

> **输入：** 1-> 2-> 9-> 9->空
> **输出：**
> 原始列表是：1 2 9 9
> 结果列表是：1 3 0 0
> 
> **输入：** 9-> 9-> 9-> 9->空
> **输出：**
> 原始列表是：9 9 9 9
> 结果列表是：1 0 0 0 0

**方法：**此帖子中的[中讨论了上述问题的先前实现。 但是，一种实现方式要求反向链接列表，而另一种则使用递归。 此处讨论了 O（1）空间复杂度解决方案，该解决方案不需要反向链接列表。
这个问题的主要重点是数字 9，它会创建所有更改，否则对于其他数字，我们只需要将其值增加 1，但是如果我们将节点的值更改为 9，则产生一个进位，然后必须进行 通过链表。](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)

在链接列表中找到不等于 9 的最后一个节点。现在有三种情况：

1.  如果没有这样的节点，即每个节点的值为 9，则新的链表将包含全 0，并在链表的开头插入一个 1。
2.  如果最右边的节点（不等于 9）是链表中的最后一个节点，则将该节点加 1 并返回链表的头。
3.  如果该节点不是最后一个节点，即它之后的每个节点等于 9，则将 1 添加到当前节点并将其之后的所有节点更改为 0。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Node of the linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to create a new node 
Node* create_Node(int data) 
{ 
    Node* temp = new Node(); 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Function to print the linked list 
void print(Node* head) 
{ 

    Node* temp = head; 
    while (temp != NULL) { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } 
    cout << endl; 
} 

// Function to add one to a number 
// represented as linked list 
Node* addOne(Node* head) 
{ 

    // To store the last node in the linked 
    // list which is not equal to 9 
    Node* last = NULL; 
    Node* cur = head; 

    // Iterate till the last node 
    while (cur->next != NULL) { 

        if (cur->data != 9) { 
            last = cur; 
        } 
        cur = cur->next; 
    } 

    // If last node is not equal to 9 
    // add 1 to it and return the head 
    if (cur->data != 9) { 
        cur->data++; 
        return head; 
    } 

    // If list is of the type 9 -> 9 -> 9 ... 
    if (last == NULL) { 
        last = new Node(); 
        last->data = 0; 
        last->next = head; 
        head = last; 
    } 

    // For cases when the righmost node which 
    // is not equal to 9 is not the last 
    // node in the linked list 
    last->data++; 
    last = last->next; 

    while (last != NULL) { 
        last->data = 0; 
        last = last->next; 
    } 

    return head; 
} 

// Driver code 
int main() 
{ 
    Node* head = create_Node(1); 
    head->next = create_Node(2); 
    head->next->next = create_Node(9); 
    head->next->next->next = create_Node(9); 

    cout << "Original list is : "; 
    print(head); 

    head = addOne(head); 

    cout << "Resultant list is : "; 
    print(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 

class GFG 
{ 

// Node of the linked list 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to create a new node 
static Node create_Node(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 
    return temp; 
} 

// Function to print the linked list 
static void print(Node head) 
{ 
    Node temp = head; 
    while (temp != null)  
    { 
        System.out.print(temp.data + " "); 
        temp = temp.next; 
    } 
    System.out.println(); 
} 

// Function to add one to a number 
// represented as linked list 
static Node addOne(Node head) 
{ 

    // To store the last node in the linked 
    // list which is not equal to 9 
    Node last = null; 
    Node cur = head; 

    // Iterate till the last node 
    while (cur.next != null) 
    { 
        if (cur.data != 9) 
        { 
            last = cur; 
        } 
        cur = cur.next; 
    } 

    // If last node is not equal to 9 
    // add 1 to it and return the head 
    if (cur.data != 9) 
    { 
        cur.data++; 
        return head; 
    } 

    // If list is of the type 9 . 9 . 9 ... 
    if (last == null) 
    { 
        last = new Node(); 
        last.data = 0; 
        last.next = head; 
        head = last; 
    } 

    // For cases when the righmost node which 
    // is not equal to 9 is not the last 
    // node in the linked list 
    last.data++; 
    last = last.next; 

    while (last != null)  
    { 
        last.data = 0; 
        last = last.next; 
    } 
    return head; 
} 

// Driver code 
public static void main(String[] args)  
{ 
    Node head = create_Node(1); 
    head.next = create_Node(2); 
    head.next.next = create_Node(9); 
    head.next.next.next = create_Node(9); 

    System.out.print("Original list is : "); 
    print(head); 

    head = addOne(head); 

    System.out.print("Resultant list is : "); 
    print(head); 
} 
} 

// This code is contributed  
// by PrinciRaj1992 

```

## Python3

```py

# A Python3 implementation of the approach 

# Node of the linked list 
class Node(): 
    def __init__(self): 
        self.data = None
        self.next = None

# Function to create a new node 
def create_Node(data): 
    temp = Node() 
    temp.data = data 
    temp.next = None
    return temp 

# Function to print the linked list 
def printList(head): 
    temp = head 
    while (temp != None): 
        print(temp.data, end = ' ') 
        temp = temp.next
    print() 

# Function to add one to a number 
# represented as linked list 
def addOne(head): 

    # To store the last node in the 
    # linked list which is not equal to 9 
    last = None
    cur = head 

    # Iterate till the last node 
    while(cur.next != None): 
        if(cur.data != 9): 
            last = cur 
        cur = cur.next

    # If last node is not equal to 9 
    # add 1 to it and return the head 
    if(cur.data != 9): 
        cur.data += 1
        return head 

    # If list is of the type 9 -> 9 -> 9 ... 
    if(last == None): 
        last = Node() 
        last.data = 0
        last.next = head 
        head = last 

    # For cases when the rightmost node which 
    # is not equal to 9 is not the last 
    # node in the linked list 
    last.data += 1
    last = last.next

    while(last != None): 
        last.data = 0
        last = last.next

    return head 

# Driver code 
if __name__=='__main__': 
    head = create_Node(1) 
    head.next = create_Node(2) 
    head.next.next = create_Node(9) 
    head.next.next.next = create_Node(9) 

    print("Original list is : ", end = "") 
    printList(head) 

    head = addOne(head) 

    print("Resultant list is : ", end = "") 
    printList(head) 

# This code is contributed by Yashyasvi Agarwal 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// Node of the linked list 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to create a new node 
static Node create_Node(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 
    return temp; 
} 

// Function to print the linked list 
static void print(Node head) 
{ 
    Node temp = head; 
    while (temp != null)  
    { 
        Console.Write(temp.data + " "); 
        temp = temp.next; 
    } 
    Console.WriteLine(); 
} 

// Function to add one to a number 
// represented as linked list 
static Node addOne(Node head) 
{ 

    // To store the last node in the linked 
    // list which is not equal to 9 
    Node last = null; 
    Node cur = head; 

    // Iterate till the last node 
    while (cur.next != null) 
    { 
        if (cur.data != 9) 
        { 
            last = cur; 
        } 
        cur = cur.next; 
    } 

    // If last node is not equal to 9 
    // add 1 to it and return the head 
    if (cur.data != 9) 
    { 
        cur.data++; 
        return head; 
    } 

    // If list is of the type 9 . 9 . 9 ... 
    if (last == null) 
    { 
        last = new Node(); 
        last.data = 0; 
        last.next = head; 
        head = last; 
    } 

    // For cases when the righmost node which 
    // is not equal to 9 is not the last 
    // node in the linked list 
    last.data++; 
    last = last.next; 

    while (last != null)  
    { 
        last.data = 0; 
        last = last.next; 
    } 
    return head; 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    Node head = create_Node(1); 
    head.next = create_Node(2); 
    head.next.next = create_Node(9); 
    head.next.next.next = create_Node(9); 

    Console.Write("Original list is : "); 
    print(head); 

    head = addOne(head); 

    Console.Write("Resultant list is : "); 
    print(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Original list is : 1 2 9 9 
Resultant list is : 1 3 0 0

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。