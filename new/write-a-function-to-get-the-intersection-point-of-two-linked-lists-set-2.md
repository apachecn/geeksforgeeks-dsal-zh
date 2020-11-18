# 编写函数以获取两个链表的交点| 设置2

系统中有两个单链表。 由于编程错误，链接列表之一的末端节点链接到第二个列表，从而形成了一个倒Y形列表。 编写程序以获取两个链接列表合并的点。

![Y ShapedLinked List](img/ab40c195e60241fe31989a627ddf41fc.png "Y ShapedLinked List")
上图显示了一个示例，其中两个链表的交点为15。

**方法：**可以观察到，遍历第一个链表然后从第二链表的头到交点的节点数等于遍历第二链表的节点数 然后从第一个列表的头到交点。 考虑上面给出的示例，开始分别使用两个指针 **curr1** 和 **curr2** 遍历两个链接列表，这两个指针分别指向给定链接列表的头部。

1.  如果 **curr1！= null** ，则将其更新为指向下一个节点，否则将其更新为指向第二个列表的第一个节点。
2.  如果 **curr2！= null** ，则将其更新为指向下一个节点，否则将其更新为指向第一个列表的第一个节点。
3.  当 **curr1** 不等于 **curr2** 时，重复上述步骤。

现在，两个指针 **curr1** 和 **curr2** 将指向同一节点，即合并点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Link list node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to get the intersection point 
// of the given linked lists 
int getIntersectionNode(Node* head1, Node* head2) 
{ 
    Node *curr1 = head1, *curr2 = head2; 

    // While both the pointers are not equal 
    while (curr1 != curr2) { 

        // If the first pointer is null then 
        // set it to point to the head of 
        // the second linked list 
        if (curr1 == NULL) { 
            curr1 = head2; 
        } 

        // Else point it to the next node 
        else { 
            curr1 = curr1->next; 
        } 

        // If the second pointer is null then 
        // set it to point to the head of 
        // the first linked list 
        if (curr2 == NULL) { 
            curr2 = head1; 
        } 

        // Else point it to the next node 
        else { 
            curr2 = curr2->next; 
        } 
    } 

    // Return the intersection node 
    return curr1->data; 
} 

// Driver code 
int main() 
{ 
    /* 
    Create two linked lists 

    1st Linked list is 3->6->9->15->30 
    2nd Linked list is 10->15->30 

    15 is the intersection point 
    */

    Node* newNode; 
    Node* head1 = new Node(); 
    head1->data = 10; 
    Node* head2 = new Node(); 
    head2->data = 3; 
    newNode = new Node(); 
    newNode->data = 6; 
    head2->next = newNode; 
    newNode = new Node(); 
    newNode->data = 9; 
    head2->next->next = newNode; 
    newNode = new Node(); 
    newNode->data = 15; 
    head1->next = newNode; 
    head2->next->next->next = newNode; 
    newNode = new Node(); 
    newNode->data = 30; 
    head1->next->next = newNode; 
    head1->next->next->next = NULL; 

    // Print the intersection node 
    cout << getIntersectionNode(head1, head2); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

// Link list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to get the intersection point 
// of the given linked lists 
static int getIntersectionNode(Node head1, Node head2) 
{ 
    Node curr1 = head1, curr2 = head2; 

    // While both the pointers are not equal 
    while (curr1 != curr2)  
    { 

        // If the first pointer is null then 
        // set it to point to the head of 
        // the second linked list 
        if (curr1 == null) 
        { 
            curr1 = head2; 
        } 

        // Else point it to the next node 
        else 
        { 
            curr1 = curr1.next; 
        } 

        // If the second pointer is null then 
        // set it to point to the head of 
        // the first linked list 
        if (curr2 == null) 
        { 
            curr2 = head1; 
        } 

        // Else point it to the next node 
        else
        { 
            curr2 = curr2.next; 
        } 
    } 

    // Return the intersection node 
    return curr1.data; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    /* 
    Create two linked lists 

    1st Linked list is 3.6.9.15.30 
    2nd Linked list is 10.15.30 

    15 is the intersection point 
    */

    Node newNode; 
    Node head1 = new Node(); 
    head1.data = 10; 
    Node head2 = new Node(); 
    head2.data = 3; 
    newNode = new Node(); 
    newNode.data = 6; 
    head2.next = newNode; 
    newNode = new Node(); 
    newNode.data = 9; 
    head2.next.next = newNode; 
    newNode = new Node(); 
    newNode.data = 15; 
    head1.next = newNode; 
    head2.next.next.next = newNode; 
    newNode = new Node(); 
    newNode.data = 30; 
    head1.next.next = newNode; 
    head1.next.next.next = null; 

    // Print the intersection node 
    System.out.print(getIntersectionNode(head1, head2)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation of the approach 

# Link list node 
class Node: 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to get the intersection point 
# of the given linked lists 
def getIntersectionNode( head1, head2): 

    curr1 = head1 
    curr2 = head2 

    # While both the pointers are not equal 
    while (curr1 != curr2):  

        # If the first pointer is None then 
        # set it to point to the head of 
        # the second linked list 
        if (curr1 == None) : 
            curr1 = head2 

        # Else point it to the next node 
        else:  
            curr1 = curr1.next

        # If the second pointer is None then 
        # set it to point to the head of 
        # the first linked list 
        if (curr2 == None):  
            curr2 = head1 

        # Else point it to the next node 
        else:  
            curr2 = curr2.next

    # Return the intersection node 
    return curr1.data 

# Driver code 

# Create two linked lists 

# 1st Linked list is 3.6.9.15.30 
# 2nd Linked list is 10.15.30 

# 15 is the intersection point 

newNode = None
head1 = Node() 
head1.data = 10
head2 = Node() 
head2.data = 3
newNode = Node() 
newNode.data = 6
head2.next = newNode 
newNode = Node() 
newNode.data = 9
head2.next.next = newNode 
newNode = Node() 
newNode.data = 15
head1.next = newNode 
head2.next.next.next = newNode 
newNode = Node() 
newNode.data = 30
head1.next.next = newNode 
head1.next.next.next = None

# Print the intersection node 
print( getIntersectionNode(head1, head2)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// Link list node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to get the intersection point 
// of the given linked lists 
static int getIntersectionNode(Node head1,  
                               Node head2) 
{ 
    Node curr1 = head1, curr2 = head2; 

    // While both the pointers are not equal 
    while (curr1 != curr2)  
    { 

        // If the first pointer is null then 
        // set it to point to the head of 
        // the second linked list 
        if (curr1 == null) 
        { 
            curr1 = head2; 
        } 

        // Else point it to the next node 
        else
        { 
            curr1 = curr1.next; 
        } 

        // If the second pointer is null then 
        // set it to point to the head of 
        // the first linked list 
        if (curr2 == null) 
        { 
            curr2 = head1; 
        } 

        // Else point it to the next node 
        else
        { 
            curr2 = curr2.next; 
        } 
    } 

    // Return the intersection node 
    return curr1.data; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    /* 
    Create two linked lists 

    1st Linked list is 3.6.9.15.30 
    2nd Linked list is 10.15.30 

    15 is the intersection point 
    */
    Node newNode; 
    Node head1 = new Node(); 
    head1.data = 10; 
    Node head2 = new Node(); 
    head2.data = 3; 
    newNode = new Node(); 
    newNode.data = 6; 
    head2.next = newNode; 
    newNode = new Node(); 
    newNode.data = 9; 
    head2.next.next = newNode; 
    newNode = new Node(); 
    newNode.data = 15; 
    head1.next = newNode; 
    head2.next.next.next = newNode; 
    newNode = new Node(); 
    newNode.data = 30; 
    head1.next.next = newNode; 
    head1.next.next.next = null; 

    // Print the intersection node 
    Console.Write(getIntersectionNode(head1, head2)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
15

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。