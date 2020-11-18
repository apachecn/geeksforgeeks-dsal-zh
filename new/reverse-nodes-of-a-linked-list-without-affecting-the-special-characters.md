# 链表的反向节点而不影响特殊字符

给定一个字母和特殊字符的链接列表。 反转给定的链表，而不会影响特殊字符的位置。

**示例：**

> **输入**：g-> @-> e->＃-> e-> $-> k-> s-> NULL
> **输出**：s-> @-> k->＃-> e-> $-> e-> g-> NULL
> **解释**：在这里我们可以看到输出中特殊字符的位置不变，并且链表也相反。

想法是遍历链接列表，并将不包括特殊字符的字符存储在临时数组中。 再次遍历链表，并以相反的方式将元素从数组复制到链表的节点。

**以下是逐步算法**：

1.  取一个临时数组 TEMP_ARR。

2.  遍历链接列表并执行以下操作

    *   如果当前元素是字母，则将链接列表的该元素存储到 TEMP_ARR。

    *   否则，将节点指针增加一

下面是上述方法的实现：

## C++

```cpp

// CPP program to reverse a linked list 
// without affecting special characters 

#include <iostream> 

using namespace std; 

// Link list node  
struct Node { 
    char data; 
    struct Node* next; 
}; 

// Function to reverse the linked list 
// without affecting special characters 
void reverse(struct Node** head_ref, int size) 
{ 
    struct Node* current = *head_ref; 

    char TEMP_ARR[size]; 

    int i = 0; 

    // Traverse the linked list and insert 
    // linked list elements to TEMP_ARR 
    while (current != NULL) { 
        // if the cuurent data is any alphabet than 
        // store it in to TEMP_ARR 
        if ((current->data >= 97 && current->data <= 122) ||  
                (current->data >= 65 && current->data <= 90)) { 
            TEMP_ARR[i++] = current->data; 
            current = current->next; 
        } 
        // else increase the node position 
        else
            current = current->next; 
    } 

    current = *head_ref; 
    // Traverse the linked list again 
    while (current != NULL)  
    { 
        // if current character is an alphabet than 
        // replace the current element in the linked list 
        // with the last element of the TEMP_ARR 
        if ((current->data >= 97 && current->data <= 122) ||  
                (current->data >= 65 && current->data <= 90)) { 
            current->data = TEMP_ARR[--i]; 
            current = current->next; 
        } 
        // else increase the node 
        else
            current = current->next; 
    } 
} 

// Function to push a node  
void push(struct Node** head_ref, char new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        cout << temp->data; 
        temp = temp->next; 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    push(&head, 's'); 
    push(&head, '{content}apos;); 
    push(&head, 'k'); 
    push(&head, 'e'); 
    push(&head, 'e'); 
    push(&head, '@'); 
    push(&head, '#'); 
    push(&head, 'g'); 
    push(&head, 'r'); 
    push(&head, 'o'); 
    push(&head, 'f'); 
    push(&head, 's'); 
    push(&head, '{content}apos;); 
    push(&head, 'k'); 
    push(&head, 'e'); 
    push(&head, 'e'); 
    push(&head, 'g'); 

    cout << "Given linked list: "; 
    printList(head); 

    reverse(&head, 13); 

    cout << "\nReversed Linked list: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to reverse a  
// linked list without affecting  
// special characters 
class GFG 
{ 

// Link list node  
public static class Node  
{ 
    char data; 
    Node next; 
} 

// Function to reverse the linked 
// list without affecting special  
// characters 
static void reverse(Node head_ref, 
                    int size) 
{ 
Node current = head_ref; 

char TEMP_ARR[] = new char[size]; 

int i = 0; 

// Traverse the linked list  
// and insert linked list  
// elements to TEMP_ARR 
while (current != null) 
{ 
    // if the cuurent data  
    // is any alphabet than 
    // store it in to TEMP_ARR 
    if ((current.data >= 97 &&  
         current.data <= 122) ||  
        (current.data >= 65 &&  
         current.data <= 90)) 
    { 
        TEMP_ARR[i++] = current.data; 
        current = current.next; 
    } 

    // else increase the node position 
    else
        current = current.next; 
} 

current = head_ref; 

// Traverse the linked list again 
while (current != null)  
{ 
    // if current character is an  
    // alphabet than replace the  
    // current element in the linked 
    // list with the last element  
    // of the TEMP_ARR 
    if ((current.data >= 97 &&  
         current.data <= 122) ||  
        (current.data >= 65 &&  
         current.data <= 90))  
    { 
        current.data = TEMP_ARR[--i]; 
        current = current.next; 
    } 

    // else increase the node 
    else
        current = current.next; 
    } 
} 

// Function to push a node  
static Node push(Node head_ref, 
                 char new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list 
       off the new node */
    new_node.next = (head_ref); 

    /* move the head to point  
       to the new node */
    (head_ref) = new_node; 

    return head_ref; 
} 

/* Function to print linked list */
static void printList(Node head) 
{ 
    Node temp = head; 
    while (temp != null)  
    { 
        System.out.print(temp.data); 
        temp = temp.next; 
    } 
} 

// Driver Code 
public static void main(String rags[]) 
{ 
    /* Start with the empty list */
    Node head = null; 

    head = push(head, 's'); 
    head = push(head, '{content}apos;); 
    head = push(head, 'k'); 
    head = push(head, 'e'); 
    head = push(head, 'e'); 
    head = push(head, '@'); 
    head = push(head, '#'); 
    head = push(head, 'g'); 
    head = push(head, 'r'); 
    head = push(head, 'o'); 
    head = push(head, 'f'); 
    head = push(head, 's'); 
    head = push(head, '{content}apos;); 
    head = push(head, 'k'); 
    head = push(head, 'e'); 
    head = push(head, 'e'); 
    head = push(head, 'g'); 

    System.out.print( "Given linked list: "); 
    printList(head); 

    reverse(head, 13); 

    System.out.print("\nReversed Linked list: "); 
    printList(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to reverse a  
// linked list without affecting  
// special characters 
using System; 

class GFG 
{ 

    // Link list node  
    public class Node  
    { 
        public char data; 
        public Node next; 
    } 

    // Function to reverse the linked 
    // list without affecting special  
    // characters 
    static void reverse(Node head_ref, 
                        int size) 
    { 
        Node current = head_ref; 

        char []TEMP_ARR = new char[size]; 

        int i = 0; 

        // Traverse the linked list  
        // and insert linked list  
        // elements to TEMP_ARR 
        while (current != null) 
        { 
            // if the cuurent data  
            // is any alphabet than 
            // store it in to TEMP_ARR 
            if ((current.data >= 97 &&  
                current.data <= 122) ||  
                (current.data >= 65 &&  
                current.data <= 90)) 
            { 
                TEMP_ARR[i++] = current.data; 
                current = current.next; 
            } 

            // else increase the node position 
            else
                current = current.next; 
        } 

        current = head_ref; 

        // Traverse the linked list again 
        while (current != null)  
        { 
            // if current character is an  
            // alphabet than replace the  
            // current element in the linked 
            // list with the last element  
             // of the TEMP_ARR 
            if ((current.data >= 97 &&  
                current.data <= 122) ||  
                (current.data >= 65 &&  
                current.data <= 90))  
            { 
                current.data = TEMP_ARR[--i]; 
                current = current.next; 
            } 

            // else increase the node 
            else
                current = current.next; 
        } 
    } 

    // Function to push a node  
    static Node push(Node head_ref, 
                    char new_data) 
    { 
        /* allocate node */
        Node new_node = new Node(); 

        /* put in the data */
        new_node.data = new_data; 

        /* link the old list 
        off the new node */
        new_node.next = (head_ref); 

        /* move the head to point  
        to the new node */
        (head_ref) = new_node; 

        return head_ref; 
    } 

    /* Function to print linked list */
    static void printList(Node head) 
    { 
        Node temp = head; 
        while (temp != null)  
        { 
            Console.Write(temp.data); 
            temp = temp.next; 
        } 
    } 

    // Driver Code 
    public static void Main(String []rags) 
    { 
        /* Start with the empty list */
        Node head = null; 

        head = push(head, 's'); 
        head = push(head, '{content}apos;); 
        head = push(head, 'k'); 
        head = push(head, 'e'); 
        head = push(head, 'e'); 
        head = push(head, '@'); 
        head = push(head, '#'); 
        head = push(head, 'g'); 
        head = push(head, 'r'); 
        head = push(head, 'o'); 
        head = push(head, 'f'); 
        head = push(head, 's'); 
        head = push(head, '{content}apos;); 
        head = push(head, 'k'); 
        head = push(head, 'e'); 
        head = push(head, 'e'); 
        head = push(head, 'g'); 

        Console.Write( "Given linked list: "); 
        printList(head); 

        reverse(head, 13); 

        Console.Write("\nReversed Linked list: "); 
        printList(head); 
    } 
} 

// This code has been contributed  
// by 29AjayKumar 

```

**Output:**

```
Given linked list: geek$sforg#@eek$s
Reversed Linked list: skee$grofs#@kee$g

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。