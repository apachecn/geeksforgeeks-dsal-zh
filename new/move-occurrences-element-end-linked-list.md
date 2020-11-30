# 将所有出现的元素移到链表末尾

> 原文：[https://www.geeksforgeeks.org/move-occurrences-element-end-linked-list/](https://www.geeksforgeeks.org/move-occurrences-element-end-linked-list/)

给定一个链表和链表中的一个键，任务是将所有出现的给定键移动到链表的末尾，同时保持所有其他元素的顺序相同。

例子：

```
Input  : 1 -> 2 -> 2 -> 4 -> 3
         key = 2 
Output : 1 -> 4 -> 3 -> 2 -> 2

Input  : 6 -> 6 -> 7 -> 6 -> 3 -> 10
         key = 6
Output : 7 -> 3 -> 10 -> 6 -> 6 -> 6
```

一个**简单解决方案**是一个一个地找到链表中所有给定密钥的出现。 对于每个发现的事件，将其插入末尾。 直到所有出现的给定键都移到结尾为止。

时间复杂度：`O(N ^ 2)`

**高效解决方案 1**：保留两个指针：

`pCrawl`：用来遍历整个列表的指针。

`pKey`：如果找到了密钥，则指向发生密钥的指针。 其他与`pCrawl`相同。

我们从链表的开头开始上述两个指针。 仅当`pKey`未指向键时，才移动`pKey`。 我们总是移动`pCrawl`。 因此，当`pCrawl`和`pKey`不相同时，我们必须找到一个位于`pCrawl`之前的密钥，因此我们交换`pCrawl`的数据 和`pKey`，然后将`pKey`移动到下一个位置。 循环不变是交换数据后，从`pKey`到`pCrawl`的所有元素都是键。

下面是此方法的实现。

## C++

```cpp

// C++ program to move all occurrences of a 
// given key to end. 
#include <bits/stdc++.h> 

// A Linked list Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// A urility function to create a new node. 
struct Node* newNode(int x) 
{ 
    Node* temp = new Node; 
    temp->data = x; 
    temp->next = NULL; 
} 

// Utility function to print the elements 
// in Linked list 
void printList(Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d ", temp->data); 
        temp = temp->next; 
    } 
    printf("\n"); 
} 

// Moves all occurrences of given key to 
// end of linked list. 
void moveToEnd(Node* head, int key) 
{ 
    // Keeps track of locations where key 
    // is present. 
    struct Node* pKey = head; 

    // Traverse list 
    struct Node* pCrawl = head; 
    while (pCrawl != NULL) { 
        // If current pointer is not same as pointer 
        // to a key location, then we must have found 
        // a key in linked list. We swap data of pCrawl 
        // and pKey and move pKey to next position. 
        if (pCrawl != pKey && pCrawl->data != key) { 
            pKey->data = pCrawl->data; 
            pCrawl->data = key; 
            pKey = pKey->next; 
        } 

        // Find next position where key is present 
        if (pKey->data != key) 
            pKey = pKey->next; 

        // Moving to next Node 
        pCrawl = pCrawl->next; 
    } 
} 

// Driver code 
int main() 
{ 
    Node* head = newNode(10); 
    head->next = newNode(20); 
    head->next->next = newNode(10); 
    head->next->next->next = newNode(30); 
    head->next->next->next->next = newNode(40); 
    head->next->next->next->next->next = newNode(10); 
    head->next->next->next->next->next->next = newNode(60); 

    printf("Before moveToEnd(), the Linked list is\n"); 
    printList(head); 

    int key = 10; 
    moveToEnd(head, key); 

    printf("\nAfter moveToEnd(), the Linked list is\n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to move all occurrences of a 
// given key to end. 
class GFG { 

    // A Linked list Node 
    static class Node { 
        int data; 
        Node next; 
    } 

    // A urility function to create a new node. 
    static Node newNode(int x) 
    { 
        Node temp = new Node(); 
        temp.data = x; 
        temp.next = null; 
        return temp; 
    } 

    // Utility function to print the elements 
    // in Linked list 
    static void printList(Node head) 
    { 
        Node temp = head; 
        while (temp != null) { 
            System.out.printf("%d ", temp.data); 
            temp = temp.next; 
        } 
        System.out.printf("\n"); 
    } 

    // Moves all occurrences of given key to 
    // end of linked list. 
    static void moveToEnd(Node head, int key) 
    { 
        // Keeps track of locations where key 
        // is present. 
        Node pKey = head; 

        // Traverse list 
        Node pCrawl = head; 
        while (pCrawl != null) { 
            // If current pointer is not same as pointer 
            // to a key location, then we must have found 
            // a key in linked list. We swap data of pCrawl 
            // and pKey and move pKey to next position. 
            if (pCrawl != pKey && pCrawl.data != key) { 
                pKey.data = pCrawl.data; 
                pCrawl.data = key; 
                pKey = pKey.next; 
            } 

            // Find next position where key is present 
            if (pKey.data != key) 
                pKey = pKey.next; 

            // Moving to next Node 
            pCrawl = pCrawl.next; 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        Node head = newNode(10); 
        head.next = newNode(20); 
        head.next.next = newNode(10); 
        head.next.next.next = newNode(30); 
        head.next.next.next.next = newNode(40); 
        head.next.next.next.next.next = newNode(10); 
        head.next.next.next.next.next.next = newNode(60); 

        System.out.printf("Before moveToEnd(), the Linked list is\n"); 
        printList(head); 

        int key = 10; 
        moveToEnd(head, key); 

        System.out.printf("\nAfter moveToEnd(), the Linked list is\n"); 
        printList(head); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python program to move all occurrences of a 
# given key to end. 

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# A urility function to create a new node. 
def newNode(x): 

    temp = Node(0) 
    temp.data = x 
    temp.next = None
    return temp 

# Utility function to print the elements 
# in Linked list 
def printList( head): 

    temp = head 
    while (temp != None) : 
        print( temp.data,end = " ") 
        temp = temp.next

    print() 

# Moves all occurrences of given key to 
# end of linked list. 
def moveToEnd(head, key): 

    # Keeps track of locations where key 
    # is present. 
    pKey = head 

    # Traverse list 
    pCrawl = head 
    while (pCrawl != None) : 

        # If current pointer is not same as pointer 
        # to a key location, then we must have found 
        # a key in linked list. We swap data of pCrawl 
        # and pKey and move pKey to next position. 
        if (pCrawl != pKey and pCrawl.data != key) : 
            pKey.data = pCrawl.data 
            pCrawl.data = key 
            pKey = pKey.next

        # Find next position where key is present 
        if (pKey.data != key): 
            pKey = pKey.next

        # Moving to next Node 
        pCrawl = pCrawl.next

    return head 

# Driver code 
head = newNode(10) 
head.next = newNode(20) 
head.next.next = newNode(10) 
head.next.next.next = newNode(30) 
head.next.next.next.next = newNode(40) 
head.next.next.next.next.next = newNode(10) 
head.next.next.next.next.next.next = newNode(60) 

print("Before moveToEnd(), the Linked list is\n") 
printList(head) 

key = 10
head = moveToEnd(head, key) 

print("\nAfter moveToEnd(), the Linked list is\n") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to move all occurrences of a 
// given key to end. 
using System; 

class GFG { 

    // A Linked list Node 
    public class Node { 
        public int data; 
        public Node next; 
    } 

    // A urility function to create a new node. 
    static Node newNode(int x) 
    { 
        Node temp = new Node(); 
        temp.data = x; 
        temp.next = null; 
        return temp; 
    } 

    // Utility function to print the elements 
    // in Linked list 
    static void printList(Node head) 
    { 
        Node temp = head; 
        while (temp != null) { 
            Console.Write("{0} ", temp.data); 
            temp = temp.next; 
        } 
        Console.Write("\n"); 
    } 

    // Moves all occurrences of given key to 
    // end of linked list. 
    static void moveToEnd(Node head, int key) 
    { 
        // Keeps track of locations where key 
        // is present. 
        Node pKey = head; 

        // Traverse list 
        Node pCrawl = head; 
        while (pCrawl != null) { 
            // If current pointer is not same as pointer 
            // to a key location, then we must have found 
            // a key in linked list. We swap data of pCrawl 
            // and pKey and move pKey to next position. 
            if (pCrawl != pKey && pCrawl.data != key) { 
                pKey.data = pCrawl.data; 
                pCrawl.data = key; 
                pKey = pKey.next; 
            } 

            // Find next position where key is present 
            if (pKey.data != key) 
                pKey = pKey.next; 

            // Moving to next Node 
            pCrawl = pCrawl.next; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head = newNode(10); 
        head.next = newNode(20); 
        head.next.next = newNode(10); 
        head.next.next.next = newNode(30); 
        head.next.next.next.next = newNode(40); 
        head.next.next.next.next.next = newNode(10); 
        head.next.next.next.next.next.next = newNode(60); 

        Console.Write("Before moveToEnd(), the Linked list is\n"); 
        printList(head); 

        int key = 10; 
        moveToEnd(head, key); 

        Console.Write("\nAfter moveToEnd(), the Linked list is\n"); 
        printList(head); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
Before moveToEnd(), the Linked list is
10 20 10 30 40 10 60 

After moveToEnd(), the Linked list is
20 30 40 60 10 10 10 

```

**时间复杂度**：`O(n)`仅需要遍历列表。

**有效解决方案 2**：

1.  遍历链表，并在末尾使用指针。

2.  现在，检查密钥和节点->数据是否相等，将节点移至倒数第二个，否则向前移

。

## C++

```cpp

// C++ code to remove key element to end of linked list 
#include<bits/stdc++.h> 
using namespace std; 

// A Linked list Node 
struct Node  
{ 
    int data; 
    struct Node* next; 
}; 

// A urility function to create a new node. 
struct Node* newNode(int x) 
{ 
    Node* temp = new Node; 
    temp->data = x; 
    temp->next = NULL; 
} 

// Function to remove key to end 
Node *keyToEnd(Node* head, int key) 
{ 

    // Node to keep pointing to tail 
    Node* tail = head; 
    if (head == NULL)  
    { 
        return NULL; 
    } 
    while (tail->next != NULL)  
    { 
        tail = tail->next; 
    } 

    // Node to point to last of linked list 
    Node* last = tail; 
    Node* current = head; 
    Node* prev = NULL; 

    // Node prev2 to point to previous when head.data!=key 
    Node* prev2 = NULL; 

    // loop to perform operations to remove key to end 
    while (current != tail)  
    { 
        if (current->data == key && prev2 == NULL)  
        { 
            prev = current; 
            current = current->next; 
            head = current; 
            last->next = prev; 
            last = last->next; 
            last->next = NULL; 
            prev = NULL; 
        } 
        else
        { 
            if (current->data == key && prev2 != NULL) 
            { 
                prev = current; 
                current = current->next; 
                prev2->next = current; 
                last->next = prev; 
                last = last->next; 
                last->next = NULL; 
            } 
            else if (current != tail)  
            { 
                prev2 = current; 
                current = current->next; 
            } 
        } 
    } 
    return head; 
} 

// Function to display linked list 
void printList(Node* head)  
{ 
    struct Node* temp = head; 
    while (temp != NULL)  
    { 
        printf("%d ", temp->data); 
        temp = temp->next; 
    } 
    printf("\n"); 
} 

// Driver Code 
int main() 
{ 
    Node* root = newNode(5); 
    root->next = newNode(2); 
    root->next->next = newNode(2); 
    root->next->next->next = newNode(7); 
    root->next->next->next->next = newNode(2); 
    root->next->next->next->next->next = newNode(2); 
    root->next->next->next->next->next->next = newNode(2); 

    int key = 2; 
    cout << "Linked List before operations :"; 
    printList(root); 
    cout << "\nLinked List after operations :"; 
    root = keyToEnd(root, key); 
    printList(root); 
    return 0; 
} 

// This code is contributed by Rajout-Ji 

```

## Java

```java

// Java code to remove key element to end of linked list 
import java.util.*; 

// Node class 
class Node { 
    int data; 
    Node next; 

    public Node(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
} 

class gfg { 

    static Node root; 

    // Function to remove key to end 
    public static Node keyToEnd(Node head, int key) 
    { 

        // Node to keep pointing to tail 
        Node tail = head; 

        if (head == null) { 
            return null; 
        } 

        while (tail.next != null) { 
            tail = tail.next; 
        } 

        // Node to point to last of linked list 
        Node last = tail; 

        Node current = head; 
        Node prev = null; 

        // Node prev2 to point to previous when head.data!=key 
        Node prev2 = null; 

        // loop to perform operations to remove key to end 
        while (current != tail) { 
            if (current.data == key && prev2 == null) { 
                prev = current; 
                current = current.next; 
                head = current; 
                last.next = prev; 
                last = last.next; 
                last.next = null; 
                prev = null; 
            } 
            else { 
                if (current.data == key && prev2 != null) { 
                    prev = current; 
                    current = current.next; 
                    prev2.next = current; 
                    last.next = prev; 
                    last = last.next; 
                    last.next = null; 
                } 
                else if (current != tail) { 
                    prev2 = current; 
                    current = current.next; 
                } 
            } 
        } 
        return head; 
    } 

    // Function to display linked list 
    public static void display(Node root) 
    { 
        while (root != null) { 
            System.out.print(root.data + " "); 
            root = root.next; 
        } 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        root = new Node(5); 
        root.next = new Node(2); 
        root.next.next = new Node(2); 
        root.next.next.next = new Node(7); 
        root.next.next.next.next = new Node(2); 
        root.next.next.next.next.next = new Node(2); 
        root.next.next.next.next.next.next = new Node(2); 

        int key = 2; 
        System.out.println("Linked List before operations :"); 
        display(root); 
        System.out.println("\nLinked List after operations :"); 
        root = keyToEnd(root, key); 
        display(root); 
    } 
} 

```

## C#

```cs

// C# code to remove key 
// element to end of linked list 
using System; 

// Node class 
public class Node { 
    public int data; 
    public Node next; 

    public Node(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
} 

class GFG { 

    static Node root; 

    // Function to remove key to end 
    public static Node keyToEnd(Node head, int key) 
    { 

        // Node to keep pointing to tail 
        Node tail = head; 

        if (head == null) { 
            return null; 
        } 

        while (tail.next != null) { 
            tail = tail.next; 
        } 

        // Node to point to last of linked list 
        Node last = tail; 

        Node current = head; 
        Node prev = null; 

        // Node prev2 to point to 
        // previous when head.data!=key 
        Node prev2 = null; 

        // loop to perform operations 
        // to remove key to end 
        while (current != tail) { 
            if (current.data == key && prev2 == null) { 
                prev = current; 
                current = current.next; 
                head = current; 
                last.next = prev; 
                last = last.next; 
                last.next = null; 
                prev = null; 
            } 
            else { 
                if (current.data == key && prev2 != null) { 
                    prev = current; 
                    current = current.next; 
                    prev2.next = current; 
                    last.next = prev; 
                    last = last.next; 
                    last.next = null; 
                } 
                else if (current != tail) { 
                    prev2 = current; 
                    current = current.next; 
                } 
            } 
        } 
        return head; 
    } 

    // Function to display linked list 
    public static void display(Node root) 
    { 
        while (root != null) { 
            Console.Write(root.data + " "); 
            root = root.next; 
        } 
    } 

    // Driver Code 
    public static void Main() 
    { 
        root = new Node(5); 
        root.next = new Node(2); 
        root.next.next = new Node(2); 
        root.next.next.next = new Node(7); 
        root.next.next.next.next = new Node(2); 
        root.next.next.next.next.next = new Node(2); 
        root.next.next.next.next.next.next = new Node(2); 

        int key = 2; 
        Console.WriteLine("Linked List before operations :"); 
        display(root); 
        Console.WriteLine("\nLinked List after operations :"); 
        root = keyToEnd(root, key); 
        display(root); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Linked List before operations :
5 2 2 7 2 2 2 
Linked List after operations :
5 7 2 2 2 2 2 
```

感谢 **Ravinder Kumar** 提出了此方法。

**高效解决方案 3**：将维护单独的密钥列表。 我们将此键列表初始化为空。 我们遍历给定的列表。 对于找到的每个密钥，我们将其从原始列表中删除，然后插入单独的密钥列表中。 最后，我们在剩余给定列表的末尾链接关键字列表。 该解决方案的时间复杂度也是`O(n)`，并且它只需要遍历列表。

本文由 MAZHAR IMAM KHAN 撰写。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

