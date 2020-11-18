# 修改链接列表的内容-递归方法

给定一个包含 **n** 个节点的单链列表。 修改前半个节点的值，以使第一个节点的新值等于最后一个节点的值减去第一个节点的当前值，第二个节点的新值等于后一个节点的值减去第二个节点的当前值，对于前半个节点也是如此。 如果 **n** 为奇数，则中间节点的值保持不变。

**示例：**

> **输入：** 10-> 4-> 5-> 3-> 6
> **输出：** -4-> -1-> 5-> 3-> 6
> 
> **输入：** 2-> 9-> 8-> 12-> 7-> 10
> **输出：** 8-> -2-> 4-> 12-> 7-> 10

**方法：**仅对列表的后半部分使用递归遍历链接列表，而不是对整个列表进行递归，从而减少了堆栈帧。 根据列表中的节点数，我们计算列表后半部分的起点，然后将列表递归到后半部分。 一旦后半部分完全递归，就减去堆栈中存在的节点的值和当前节点的值。

下面是上述方法的实现：

## C ++

```

// C++ program to modify the contents 
// of the linked list with recursion 

#include <bits/stdc++.h> 
using namespace std; 

// Represents a Node of the linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to create and return a new node 
Node* insert(int data) 
{ 
    Node* temp; 
    temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Function which returns the total number of  
// node present in the list 
int getTotalNodeCount(Node* head) 
{ 
    int totalNodesCount = 0; 

    while(head != NULL) 
    { 
        totalNodesCount++; 
        head = head->next; 
    } 
    return totalNodesCount; 
} 

// Function to modify the contents 
// of the given linked lists 
void modifyContents(Node** first_half ,  
                        Node* second_half)  
{ 
    if (second_half == NULL) 
    { 
        return; 
    } 

    modifyContents(first_half,second_half->next); 

    (*first_half)->data = second_half->data - (*first_half)->data; 
    (*first_half) = (*first_half)->next; 

    return; 
} 

// Wrapper function which calculates the starting  
// point for second half of the list 
void modifyContentsWrapper(Node** head) 
{ 
    Node *ptr = NULL; // pointer to second half of list 
    Node *temp = NULL;  
    int diff = 0;  
    int length = 0; // number of nodes in the list 

    if (*head == NULL) 
    { 
        return; 
    } 
    length = getTotalNodeCount(*head); 

    // If link list has odd number of nodes, then pointer  
    // for second half starts from (length of link list + 1). 
    // Say for an example, for the list 10->4->5->3->6 pointer  
    // should start from 3\. 
    // If list has even number of nodes, 10->4->5->9->6->8,  
    // pointer starts from 9\. 
    diff = (length%2 == 0? (length/2) :(length/2)+1 ); 

    ptr = *head; 

    while(diff--) 
        ptr = ptr->next; 

    temp = *head; 

    modifyContents(&temp,ptr); 

    return; 
} 

// Function to print the contents of the linked list 
void print(Node* nod) 
{ 
    if (nod == NULL) { 
        return; 
    } 

    cout << nod->data; 

    if (nod->next != NULL) 
        cout << " -> "; 

    print(nod->next); 
} 

// Driver code 
int main() 
{ 
    Node* head = insert(2); 
    head->next = insert(9); 
    head->next->next = insert(8); 
    head->next->next->next = insert(12); 
    head->next->next->next->next = insert(7); 
    head->next->next->next->next->next = insert(10); 

    // Modify the linked list 
    modifyContentsWrapper(&head); 

    // Print the modified linked list 
    print(head); 

    return 0; 
} 

```

## 爪哇

```

// Java program to modify the contents 
// of the linked list with recursion 
class GFG 
{ 

// Represents a Node of the linked list 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to create and return a new node 
static Node insert(int data) 
{ 
    Node temp; 
    temp = new Node(); 
    temp.data = data; 
    temp.next = null; 
    return temp; 
} 

// Function which returns the total number  
// of node present in the list 
static int getTotalNodeCount(Node head) 
{ 
    int totalNodesCount = 0; 

    while(head != null) 
    { 
        totalNodesCount++; 
        head = head.next; 
    } 
    return totalNodesCount; 
} 

static Node temp = null; 

// Function to modify the contents 
// of the given linked lists 
static void modifyContents(Node second_half)  
{ 
    if (second_half == null) 
    { 
        return; 
    } 

    modifyContents(second_half.next); 

    (temp).data = second_half.data - (temp).data; 
    (temp) = (temp).next; 

    return; 
} 

// Wrapper function which calculates the starting  
// point for second half of the list 
static Node modifyContentsWrapper(Node head) 
{ 
    Node ptr = null; // pointer to second half of list 
    temp = null;  
    int diff = 0;  
    int length = 0; // number of nodes in the list 

    if (head == null) 
    { 
        return null; 
    } 
    length = getTotalNodeCount(head); 

    // If link list has odd number of nodes,  
    // then pointer for second half starts  
    // from (length of link list + 1).  
    // Say for an example, for the list 10.4.5.3.6   
    // pointer should start from 3\. 
    // If list has even number of nodes,  
    // 10.4.5.9.6.8, pointer starts from 9\. 
    diff = (length % 2 == 0 ?  
               (length / 2) : (length / 2) + 1); 

    ptr = head; 

    while(diff-->0) 
        ptr = ptr.next; 

    temp = head; 

    modifyContents(ptr); 

    return head; 
} 

// Function to print the contents 
// of the linked list 
static void print(Node nod) 
{ 
    if (nod == null) 
    { 
        return; 
    } 

    System.out.print( nod.data); 

    if (nod.next != null) 
        System.out.print( " -> "); 

    print(nod.next); 
} 

// Driver code 
public static void main(String args[]) 
{ 
    Node head = insert(2); 
    head.next = insert(9); 
    head.next.next = insert(8); 
    head.next.next.next = insert(12); 
    head.next.next.next.next = insert(7); 
    head.next.next.next.next.next = insert(10); 

    // Modify the linked list 
    head = modifyContentsWrapper(head); 

    // Print the modified linked list 
    print(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python program to modify the contents  
# of the linked list with recursion  

# Represents a Node of the linked list  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to create and return a new node  
def insert( data) : 

    temp = Node(0)  
    temp.data = data  
    temp.next = None
    return temp  

# Function which returns the total number  
# of node present in the list  
def getTotalNodeCount( head) : 

    totalNodesCount = 0

    while(head != None):  

        totalNodesCount = totalNodesCount + 1
        head = head.next

    return totalNodesCount  

temp = None

# Function to modify the contents  
# of the given linked lists  
def modifyContents( second_half) : 

    if (second_half == None):  
        return
    global temp 

    modifyContents(second_half.next)  

    (temp).data = second_half.data - (temp).data  
    (temp) = (temp).next
    return

# Wrapper function which calculates the starting  
# point for second half of the list  
def modifyContentsWrapper(head) : 

    # pointer to second half of list  
    ptr = None
    diff = 0

    # number of nodes in the list  
    length = 0
    global temp 
    temp = None

    if (head == None) : 
        return None

    length = getTotalNodeCount(head)  

    # If link list has odd number of nodes,  
    # then pointer for second half starts  
    # from (length of link list + 1).  
    # Say for an example, for the list 10.4.5.3.6  
    # pointer should start from 3.  
    # If list has even number of nodes,  
    # 10.4.5.9.6.8, pointer starts from 9.  
    if(length % 2 == 0):  
        diff = (length / 2)  
    else: 
        diff = (length / 2) + 1

    ptr = head  

    while(diff > 0): 
        diff = diff - 1
        ptr = ptr.next

    temp = head  
    modifyContents(ptr)  
    return head  

# Function to print the contents  
# of the linked list  
def print_(nod):  

    if (nod == None) : 
        return

    print(nod.data, end = " ") 

    if (nod.next != None):  
        print( " -> ",end = "")  

    print_(nod.next)  

# Driver code  
head = insert(2)  
head.next = insert(9)  
head.next.next = insert(8)  
head.next.next.next = insert(12)  
head.next.next.next.next = insert(7)  
head.next.next.next.next.next = insert(10)  

# Modify the linked list  
head = modifyContentsWrapper(head)  

# Print the modified linked list  
print_(head)  

# This code is contributed by Arnab Kundu  

```

## C＃

```

// C# program to modify the contents 
// of the linked list with recursion 
using System; 

class GFG 
{ 

// Represents a Node of the linked list 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to create and return a new node 
static Node insert(int data) 
{ 
    Node temp; 
    temp = new Node(); 
    temp.data = data; 
    temp.next = null; 
    return temp; 
} 

// Function which returns the total number  
// of node present in the list 
static int getTotalNodeCount(Node head) 
{ 
    int totalNodesCount = 0; 

    while(head != null) 
    { 
        totalNodesCount++; 
        head = head.next; 
    } 
    return totalNodesCount; 
} 

static Node temp = null; 

// Function to modify the contents 
// of the given linked lists 
static void modifyContents(Node second_half)  
{ 
    if (second_half == null) 
    { 
        return; 
    } 

    modifyContents(second_half.next); 

    (temp).data = second_half.data - (temp).data; 
    (temp) = (temp).next; 

    return; 
} 

// Wrapper function which calculates the starting  
// point for second half of the list 
static Node modifyContentsWrapper(Node head) 
{ 
    // pointer to second half of list 
    Node ptr = null;  
    temp = null;  
    int diff = 0;  

    // number of nodes in the list 
    int length = 0;  

    if (head == null) 
    { 
        return null; 
    } 
    length = getTotalNodeCount(head); 

    // If link list has odd number of nodes,  
    // then pointer for second half starts  
    // from (length of link list + 1).  
    // Say for an example, for the list 10.4.5.3.6  
    // pointer should start from 3\. 
    // If list has even number of nodes,  
    // 10.4.5.9.6.8, pointer starts from 9\. 
    diff = (length % 2 == 0 ?  
           (length / 2) : (length / 2) + 1); 

    ptr = head; 

    while(diff-->0) 
        ptr = ptr.next; 

    temp = head; 

    modifyContents(ptr); 

    return head; 
} 

// Function to print the contents 
// of the linked list 
static void print(Node nod) 
{ 
    if (nod == null) 
    { 
        return; 
    } 

    Console.Write(nod.data); 

    if (nod.next != null) 
        Console.Write(" -> "); 

    print(nod.next); 
} 

// Driver code 
public static void Main(String []args) 
{ 
    Node head = insert(2); 
    head.next = insert(9); 
    head.next.next = insert(8); 
    head.next.next.next = insert(12); 
    head.next.next.next.next = insert(7); 
    head.next.next.next.next.next = insert(10); 

    // Modify the linked list 
    head = modifyContentsWrapper(head); 

    // Print the modified linked list 
    print(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
8 -> -2 -> 4 -> 12 -> 7 -> 10

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。