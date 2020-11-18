# 修改和重新排列列表

给定一个单链表，其中包含一些正数（有效数）和零（无效数）。 转换链接列表的方式是，如果下一个有效数字与当前数字相同，则将其值加倍并将下一个数字替换为 0。修改后，重新排列链接列表，以使所有 0 都移到末尾。

**示例：**

```
Input : 2->2->0->4->0->8
Output : 4->4->8->0->0->0

Input :  0->2->2->2->0->6->6->0->0->8
Output : 4->2->12->8->0->0->0->0->0->0

```

**来源：** [Microsoft IDC 面试体验| 设置 156。](https://www.geeksforgeeks.org/microsoft-idc-interview-experience-set-156-off-campus-for-full-time/)

**方法：**首先按照上述说明修改链表，即，如果下一个有效数字与当前数字相同，则将其值加倍并将下一个数字替换为 0。

**修改算法：**

```
1\. ptr = head
2\. while (ptr && ptr->next)
3\. if (ptr->data == 0) || (ptr->data != ptr->next->data)
4\.     ptr = ptr->next
5\. else    
6\.     ptr->data = 2 * ptr->data
7\.     ptr->next->data = 0
8\.     ptr = ptr->next->next    

```

修改列表后，隔离有效（非零）和无效（零）元素。 它与[隔离链接列表](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)中的偶数和奇数节点相同。

## C++

```cpp

// C++ implementation to modify and 
// rearrange list 
#include <bits/stdc++.h> 
using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* newNode = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// function to segregate valid (non-zero) numbers and 
// invalid (zero) numbers in a list 
Node* segValidInvalidNum(Node* head) 
{ 
    // valid (non-zero numbers) list start and 
    // end pointers 
    Node *validStart = NULL, *validEnd = NULL; 

    // invalid (zero numbers) list start and 
    // end pointers 
    Node *invalidStart = NULL, *invalidEnd = NULL; 

    Node* currentNode = head; 

    // traverse the given list 
    while (currentNode != NULL) { 
        // current node's data 
        int element = currentNode->data; 

        // if it is a non-zero element, then 
        // add it to valid list 
        if (element != 0) { 
            if (validStart == NULL) { 
                validStart = currentNode; 
                validEnd = validStart; 
            } 
            else { 
                validEnd->next = currentNode; 
                validEnd = validEnd->next; 
            } 
        } 

        // else it is a zero element, so 
        // add it to invalid list 
        else { 
            if (invalidStart == NULL) { 
                invalidStart = currentNode; 
                invalidEnd = invalidStart; 
            } 
            else { 
                invalidEnd->next = currentNode; 
                invalidEnd = invalidEnd->next; 
            } 
        } 

        // Move to the next node 
        currentNode = currentNode->next; 
    } 

    // if true then return the original list as it is 
    if (validStart == NULL || invalidStart == NULL) 
        return head; 

    // add the invalid list to the end of valid list 
    validEnd->next = invalidStart; 
    invalidEnd->next = NULL; 
    head = validStart; 

    // required head of the new list 
    return head; 
} 

// function to modify and 
// rearrange list 
Node* modifyAndRearrangeList(Node* head) 
{ 
    // if list is empty or contains a single 
    // element only 
    if (head == NULL || head->next == NULL) 
        return head; 

    // traverse the list 
    Node* ptr = head; 
    while (ptr && ptr->next) { 

        // if current node's data is '0' or it is not equal 
        // to next nodes data, them move one node ahead 
        if ((ptr->data == 0) || (ptr->data != ptr->next->data)) 
            ptr = ptr->next; 

        else { 

            // double current node's data 
            ptr->data = 2 * ptr->data; 

            // put '0' in next node's data 
            ptr->next->data = 0; 

            // move two nodes ahead 
            ptr = ptr->next->next; 
        } 
    } 

    // segregate valid (non-zero) and 
    // invalid (non-zero) numbers 
    return segValidInvalidNum(head); 
} 

// function to print a linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    Node* head = getNode(2); 
    head->next = getNode(2); 
    head->next->next = getNode(0); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(0); 
    head->next->next->next->next->next = getNode(8); 

    cout << "Original List: "; 
    printList(head); 

    head = modifyAndRearrangeList(head); 

    cout << "\nModified List: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to modify and  
// rearrange list  
class GFG  
{ 

// ure of a node  
static class Node  
{  
    int data;  
    Node next;  
};  

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node newNode = new Node();  

    // put in the data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// function to segregate valid (non-zero) numbers  
// and invalid (zero) numbers in a list  
static Node segValidInvalidNum(Node head)  
{  
    // valid (non-zero numbers) list start  
    // and end pointers  
    Node validStart = null, validEnd = null;  

    // invalid (zero numbers) list start and  
    // end pointers  
    Node invalidStart = null, invalidEnd = null;  

    Node currentNode = head;  

    // traverse the given list  
    while (currentNode != null)  
    {  
        // current node's data  
        int element = currentNode.data;  

        // if it is a non-zero element, then  
        // add it to valid list  
        if (element != 0) 
        {  
            if (validStart == null) 
            {  
                validStart = currentNode;  
                validEnd = validStart;  
            }  
            else 
            {  
                validEnd.next = currentNode;  
                validEnd = validEnd.next;  
            }  
        }  

        // else it is a zero element, so  
        // add it to invalid list  
        else 
        {  
            if (invalidStart == null)  
            {  
                invalidStart = currentNode;  
                invalidEnd = invalidStart;  
            }  
            else 
            {  
                invalidEnd.next = currentNode;  
                invalidEnd = invalidEnd.next;  
            }  
        }  

        // Move to the next node  
        currentNode = currentNode.next;  
    }  

    // if true then return the original list as it is  
    if (validStart == null || invalidStart == null)  
        return head;  

    // add the invalid list to the end of valid list  
    validEnd.next = invalidStart;  
    invalidEnd.next = null;  
    head = validStart;  

    // required head of the new list  
    return head;  
}  

// function to modify and  
// rearrange list  
static Node modifyAndRearrangeList(Node head)  
{  
    // if list is empty or contains a single  
    // element only  
    if (head == null || head.next == null)  
        return head;  

    // traverse the list  
    Node ptr = head;  
    while (ptr != null && ptr.next != null)  
    {  

        // if current node's data is '0' or  
        // it is not equal to next nodes data,  
        // them move one node ahead  
        if ((ptr.data == 0) ||  
            (ptr.data != ptr.next.data))  
            ptr = ptr.next;  
        else 
        {  

            // double current node's data  
            ptr.data = 2 * ptr.data;  

            // put '0' in next node's data  
            ptr.next.data = 0;  

            // move two nodes ahead  
            ptr = ptr.next.next;  
        }  
    }  

    // segregate valid (non-zero) and  
    // invalid (non-zero) numbers  
    return segValidInvalidNum(head);  
}  

// function to print a linked list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
            System.out.print(head.data + " "); 
            head = head.next;  
    }  
}  

// Driver Code 
public static void main(String[] args) 
{ 
    Node head = getNode(2);  
    head.next = getNode(2);  
    head.next.next = getNode(0);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = getNode(0);  
    head.next.next.next.next.next = getNode(8);  

    System.out.print("Original List: ");  
    printList(head);  

    head = modifyAndRearrangeList(head);  

    System.out.print("\nModified List: ");  
    printList(head);  
} 
} 

// This code is contributed by Rajput-Ji 

```

## 蟒蛇

```

# Python implementation to modify and  
# rearrange list  

# structure of a node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to get a new node  
def getNode( data) : 

    # allocate space  
    newNode = Node(0)  

    # put in the data  
    newNode.data = data  
    newNode.next = None
    return newNode  

# function to segregate valid (non-zero) numbers  
# and invalid (zero) numbers in a list  
def segValidInvalidNum(head) : 

    # valid (non-zero numbers) list start  
    # and end pointers  
    validStart = None
    validEnd = None

    # invalid (zero numbers) list start and  
    # end pointers  
    invalidStart = None
    invalidEnd = None

    currentNode = head  

    # traverse the given list  
    while (currentNode != None) : 

        # current node's data  
        element = currentNode.data  

        # if it is a non-zero element, then  
        # add it to valid list  
        if (element != 0): 

            if (validStart == None): 
                validStart = currentNode  
                validEnd = validStart  

            else: 
                validEnd.next = currentNode  
                validEnd = validEnd.next

        # else it is a zero element, so  
        # add it to invalid list  
        else: 

            if (invalidStart == None):  
                invalidStart = currentNode  
                invalidEnd = invalidStart  

            else: 
                invalidEnd.next = currentNode  
                invalidEnd = invalidEnd.next

        # Move to the next node  
        currentNode = currentNode.next

    # if true then return the original list as it is  
    if (validStart == None or invalidStart == None): 
        return head  

    # add the invalid list to the end of valid list  
    validEnd.next = invalidStart  
    invalidEnd.next = None
    head = validStart  

    # required head of the new list  
    return head  

# function to modify and  
# rearrange list  
def modifyAndRearrangeList( head) : 

    # if list is empty or contains a single  
    # element only  
    if (head == None or head.next == None):  
        return head  

    # traverse the list  
    ptr = head  
    while (ptr != None and ptr.next != None) : 

        # if current node's data is '0' or  
        # it is not equal to next nodes data,  
        # them move one node ahead  
        if ((ptr.data == 0) or
            (ptr.data != ptr.next.data)) : 
            ptr = ptr.next
        else: 

            # double current node's data  
            ptr.data = 2 * ptr.data  

            # put '0' in next node's data  
            ptr.next.data = 0

            # move two nodes ahead  
            ptr = ptr.next.next

    # segregate valid (non-zero) and  
    # invalid (non-zero) numbers  
    return segValidInvalidNum(head)  

# function to print a linked list  
def printList( head) : 

    while (head != None): 

            print(head.data, end = " ") 
            head = head.next

# Driver Code 
head = getNode(2)  
head.next = getNode(2)  
head.next.next = getNode(0)  
head.next.next.next = getNode(4)  
head.next.next.next.next = getNode(0)  
head.next.next.next.next.next = getNode(8)  

print("Original List: ")  
printList(head)  

head = modifyAndRearrangeList(head)  

print("\nModified List: ")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to modify and  
// rearrange list  
using System; 

class GFG  
{ 

// ure of a node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node newNode = new Node();  

    // put in the data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// function to segregate valid (non-zero) numbers  
// and invalid (zero) numbers in a list  
static Node segValidInvalidNum(Node head)  
{  
    // valid (non-zero numbers) list 
    // start and end pointers  
    Node validStart = null,  
         validEnd = null;  

    // invalid (zero numbers) list start and  
    // end pointers  
    Node invalidStart = null,  
         invalidEnd = null;  

    Node currentNode = head;  

    // traverse the given list  
    while (currentNode != null)  
    {  
        // current node's data  
        int element = currentNode.data;  

        // if it is a non-zero element,   
        // then add it to valid list  
        if (element != 0) 
        {  
            if (validStart == null) 
            {  
                validStart = currentNode;  
                validEnd = validStart;  
            }  
            else
            {  
                validEnd.next = currentNode;  
                validEnd = validEnd.next;  
            }  
        }  

        // else it is a zero element,   
        // so add it to invalid list  
        else
        {  
            if (invalidStart == null)  
            {  
                invalidStart = currentNode;  
                invalidEnd = invalidStart;  
            }  
            else
            {  
                invalidEnd.next = currentNode;  
                invalidEnd = invalidEnd.next;  
            }  
        }  

        // Move to the next node  
        currentNode = currentNode.next;  
    }  

    // if true then return the  
    // original list as it is  
    if (validStart == null ||  
        invalidStart == null)  
        return head;  

    // add the invalid list to 
    // the end of valid list  
    validEnd.next = invalidStart;  
    invalidEnd.next = null;  
    head = validStart;  

    // required head of the new list  
    return head;  
}  

// function to modify and  
// rearrange list  
static Node modifyAndRearrangeList(Node head)  
{  
    // if list is empty or contains  
    // a single element only  
    if (head == null ||  
        head.next == null)  
        return head;  

    // traverse the list  
    Node ptr = head;  
    while (ptr != null &&  
           ptr.next != null)  
    {  

        // if current node's data is '0' or  
        // it is not equal to next nodes data,  
        // them move one node ahead  
        if ((ptr.data == 0) ||  
            (ptr.data != ptr.next.data))  
            ptr = ptr.next;  
        else
        {  

            // double current node's data  
            ptr.data = 2 * ptr.data;  

            // put '0' in next node's data  
            ptr.next.data = 0;  

            // move two nodes ahead  
            ptr = ptr.next.next;  
        }  
    }  

    // segregate valid (non-zero) and  
    // invalid (non-zero) numbers  
    return segValidInvalidNum(head);  
}  

// function to print a linked list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
        Console.Write(head.data + " "); 
        head = head.next;  
    }  
}  

// Driver Code 
public static void Main(String[] args) 
{ 
    Node head = getNode(2);  
    head.next = getNode(2);  
    head.next.next = getNode(0);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = getNode(0);  
    head.next.next.next.next.next = getNode(8);  

    Console.Write("Original List: ");  
    printList(head);  

    head = modifyAndRearrangeList(head);  

    Console.Write("\nModified List: ");  
    printList(head);  
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出：**

```
Original List: 2 2 0 4 0 8
Modified List: 4 4 8 0 0 0

```

**时间复杂度：** O（n）。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。