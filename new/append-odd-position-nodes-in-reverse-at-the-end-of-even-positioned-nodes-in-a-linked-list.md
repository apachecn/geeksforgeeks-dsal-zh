# 在链表

中偶数位置节点的末尾反向附加奇数位置节点

给定一个链表。 任务是以这样一种方式隔离其偶数和奇数位置节点：奇数位置节点出现在偶数位置的节点之前，所有偶数位置的节点必须以相反的顺序出现。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6->空
> **输出：** 1-> 3-> 5-> 6-> 4-> 2-> NULL
> 
> **输入：** 1-> 2-> 3-> 4-> 5->空
> **输出：** 1-> 3-> 5-> 4-> 2->空

**来源：** [微软访谈](https://www.geeksforgeeks.org/microsoft-interview-experience-set-133-campus-internship/)

**方法：**在给定的[链接](https://www.geeksforgeeks.org/rearrange-a-linked-list-such-that-all-even-and-odd-positioned-nodes-are-together/)中讨论了类似的问题，但偶数部分未反转。 对于当前节点，分别在奇数和偶数位置维护两个指针**奇数**和**甚至**。 还存储偶数链接列表的第一个节点，以便在将所有奇数和偶数节点连接到两个不同的列表中之后，我们可以将偶数列表附加到奇数列表的末尾。 偶数列表分离后，我们只需要反转即可。 在此处可以找到反向链接列表。 一旦偶数列表反向，将其附加到奇数链接列表。

下面是上述方法的实现：

## C ++

```

// C++ program to Append odd position nodes 
// in reverse at the end of even 
// positioned nodes in a Linked List 
#include <bits/stdc++.h> 
using namespace std; 

// Linked List Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// A utility function to create a new node 
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Rearranges given linked list such that all even 
// positioned nodes are before odd positioned  
// in a reverse 
Node* rearrangeEvenOdd(Node* head) 
{ 
    // Corner case 
    if (head == NULL) 
        return NULL; 

    // Initialize first nodes of even and 
    // odd lists 
    Node* odd = head; 
    Node* even = head->next; 

    // Remember the first node of even list so 
    // that we can connect the even list at the 
    // end of odd list. 
    Node* evenFirst = even; 

    while (1) { 

        // If there are no more nodes, then connect 
        // first node of even list to the last node 
        // of odd list 
        if (!odd || !even || !(even->next)) { 
            break; 
        } 

        // Connecting odd nodes 
        odd->next = even->next; 
        odd = even->next; 

        // If there are NO more even nodes after 
        // current odd. 
        if (odd->next == NULL) { 
            even->next = NULL; 
            break; 
        } 

        // Connecting evenevenFirs nodes 
        even->next = odd->next; 
        even = odd->next; 
    } 

    // Reversal of even linked list 
    Node* current = evenFirst; 
    Node* prev = NULL; 
    Node* front = NULL; 

    // Iterate in the complete linked list 
    while (current != NULL) { 
        front = current->next; 
        current->next = prev; 
        prev = current; 
        current = front; 
    } 

    evenFirst = prev; 

    // Attach the reversed even linked 
    // list to odd linked list 
    odd->next = evenFirst; 
    return head; 
} 

// A utility function to print a linked list 
void printlist(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " -> "; 
        node = node->next; 
    } 
    cout << "NULL" << endl; 
} 

// Driver code 
int main(void) 
{ 
    Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 
    head->next->next->next->next->next = newNode(6); 

    head = rearrangeEvenOdd(head); 

    printlist(head); 

    return 0; 
} 

```

## 爪哇

```

// Java program to Append odd position nodes  
// in reverse at the end of even  
// positioned nodes in a Linked List  
class sol 
{ 

// Linked List Node  
static class Node  
{  
    int data;  
    Node next;  
};  

// A utility function to create a new node  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Rearranges given linked list such that all even  
// positioned nodes are before odd positioned  
// in a reverse  
static Node rearrangeEvenOdd(Node head)  
{  
    // Corner case  
    if (head == null)  
        return null;  

    // Initialize first nodes of even and  
    // odd lists  
    Node odd = head;  
    Node even = head.next;  

    // Remember the first node of even list so  
    // that we can connect the even list at the  
    // end of odd list.  
    Node evenFirst = even;  

    while (true)  
    {  

        // If there are no more nodes, then connect  
        // first node of even list to the last node  
        // of odd list  
        if (odd == null || even == null || (even.next) == null)  
        {  
            break;  
        }  

        // Connecting odd nodes  
        odd.next = even.next;  
        odd = even.next;  

        // If there are NO more even nodes after  
        // current odd.  
        if (odd.next == null)  
        {  
            even.next = null;  
            break;  
        }  

        // Connecting evenevenFirs nodes  
        even.next = odd.next;  
        even = odd.next;  
    }  

    // Reversal of even linked list  
    Node current = evenFirst;  
    Node prev = null;  
    Node front = null;  

    // Iterate in the complete linked list  
    while (current != null) 
    {  
        front = current.next;  
        current.next = prev;  
        prev = current;  
        current = front;  
    }  

    evenFirst = prev;  

    // Attach the reversed even linked  
    // list to odd linked list  
    odd.next = evenFirst;  
    return head;  
}  

// A utility function to print a linked list  
static void printlist(Node node)  
{  
    while (node != null)  
    {  
        System.out.print( node.data + " -> ");  
        node = node.next;  
    }  
    System.out.println( "null" );  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(5);  
    head.next.next.next.next.next = newNode(6);  

    head = rearrangeEvenOdd(head);  

    printlist(head);  

}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 program to Append odd position nodes 
# in reverse at the end of even 
# positioned nodes in a Linked List 
import math 

# Linked List Node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# A utility function to create a new node 
def newNode(key): 
    temp = Node(key) 
    temp.data = key 
    temp.next = None
    return temp 

# Rearranges given linked list such that  
# all even positioned nodes are before  
# odd positioned in a reverse 
def rearrangeEvenOdd(head): 

    # Corner case 
    if (head == None): 
        return None

    # Initialize first nodes of even and 
    # odd lists 
    odd = head 
    even = head.next

    # Remember the first node of even list so 
    # that we can connect the even list at the 
    # end of odd list. 
    evenFirst = even 

    while True: 

        # If there are no more nodes, 
        # then connect first node of 
        # even list to the last node 
        # of odd list 
        if (odd == None or even == None or 
                    (even.next) == None): 
            break

        # Connecting odd nodes 
        odd.next = even.next
        odd = even.next

        # If there are NO more even nodes after 
        # current odd. 
        if (odd.next == None): 
            even.next = None
            break

        # Connecting evenevenFirs nodes 
        even.next = odd.next
        even = odd.next

    # Reversal of even linked list 
    current = evenFirst 
    prev = None
    front = None

    # Iterate in the complete linked list 
    while (current != None): 
        front = current.next
        current.next = prev 
        prev = current 
        current = front 

    evenFirst = prev 

    # Attach the reversed even linked 
    # list to odd linked list 
    odd.next = evenFirst 
    return head 

# A utility function to print a linked list 
def printlist(node): 
    while (node != None) : 
        print(node.data, end = "->") 
        node = node.next

    print("NULL") 

# Driver code 
if __name__=='__main__':  
    head = newNode(1) 
    head.next = newNode(2) 
    head.next.next = newNode(3) 
    head.next.next.next = newNode(4) 
    head.next.next.next.next = newNode(5) 
    head.next.next.next.next.next = newNode(6) 

    head = rearrangeEvenOdd(head) 

    printlist(head) 

# This code is contributed by Srathore 

```

## C＃

```

// C# program to Append odd position nodes  
// in reverse at the end of even  
// positioned nodes in a Linked List  
using System; 

class GFG 
{ 

// Linked List Node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// A utility function to create a new node  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Rearranges given linked list such that  
// all even positioned nodes are before  
// odd positioned in a reverse  
static Node rearrangeEvenOdd(Node head)  
{  
    // Corner case  
    if (head == null)  
        return null;  

    // Initialize first nodes of even and  
    // odd lists  
    Node odd = head;  
    Node even = head.next;  

    // Remember the first node of even list so  
    // that we can connect the even list at the  
    // end of odd list.  
    Node evenFirst = even;  

    while (true)  
    {  

        // If there are no more nodes,   
        // then connect first node of 
        // even list to the last node  
        // of odd list  
        if (odd == null || even == null || 
                          (even.next) == null)  
        {  
            break;  
        }  

        // Connecting odd nodes  
        odd.next = even.next;  
        odd = even.next;  

        // If there are NO more even nodes after  
        // current odd.  
        if (odd.next == null)  
        {  
            even.next = null;  
            break;  
        }  

        // Connecting evenevenFirs nodes  
        even.next = odd.next;  
        even = odd.next;  
    }  

    // Reversal of even linked list  
    Node current = evenFirst;  
    Node prev = null;  
    Node front = null;  

    // Iterate in the complete linked list  
    while (current != null) 
    {  
        front = current.next;  
        current.next = prev;  
        prev = current;  
        current = front;  
    }  

    evenFirst = prev;  

    // Attach the reversed even linked  
    // list to odd linked list  
    odd.next = evenFirst;  
    return head;  
}  

// A utility function to print a linked list  
static void printlist(Node node)  
{  
    while (node != null)  
    {  
        Console.Write( node.data + " -> ");  
        node = node.next;  
    }  
    Console.WriteLine( "null" );  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(5);  
    head.next.next.next.next.next = newNode(6);  

    head = rearrangeEvenOdd(head);  

    printlist(head);  
}  
} 

// This code is contributed by PrinciRaj1992  

```

**Output:**

```
1 -> 3 -> 5 -> 6 -> 4 -> 2 -> NULL

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。